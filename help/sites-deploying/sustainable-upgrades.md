---
title: Atualizações sustentáveis
description: Saiba mais sobre atualizações sustentáveis no Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Atualizações sustentáveis{#sustainable-upgrades}

## Estrutura de personalização {#customization-framework}

### Arquitetura (funcional/infraestrutura/conteúdo/aplicativo)  {#architecture-functional-infrastructure-content-application}

O recurso Estrutura de personalização foi projetado para ajudar a reduzir as violações em áreas não extensíveis do código (como APIS) ou conteúdo (como sobreposições) que não são amigáveis para atualização.

Há dois componentes da estrutura de personalização: a variável **Superfície da API** e a variável **Classificação de conteúdo**.

#### Superfície da API {#api-surface}

Em versões anteriores do Adobe Experience Manager (AEM), muitas APIs eram expostas por meio do Uber Jar. Algumas dessas APIs não eram destinadas ao uso por clientes, mas foram expostas à funcionalidade AEM de suporte em pacotes. Além disso, as APIs do Java™ são marcadas como Públicas ou Privadas para indicar aos clientes quais APIs são seguras para usar no contexto de atualizações. Outras especificidades incluem:

* APIs Java™ marcadas como `Public` podem ser usados e referenciados por pacotes de implementação personalizados.

* As APIs públicas são compatíveis com a instalação de um pacote de compatibilidade.
* O pacote de compatibilidade contém um Uber JAR compatível para garantir a compatibilidade com versões anteriores
* APIs Java™ marcadas como `Private` destinam-se a ser usados somente por pacotes internos AEM, não por pacotes personalizados.

>[!NOTE]
>
>O conceito de `Private` e `Public` neste contexto, não deve ser confundido com noções Java™ de classes públicas e privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificações de conteúdo {#content-classifications}

O AEM há muito tempo usa o principal das sobreposições e do Sling Resource Merger para permitir que os clientes estendam e personalizem a funcionalidade do AEM. Funcionalidade predefinida na qual os consoles e a interface do usuário do AEM são armazenados **/libs**. Os clientes nunca devem modificar nada abaixo de **/libs** mas pode adicionar conteúdo adicional abaixo de **/apps** para sobrepor e estender a funcionalidade definida em **/libs** (Consulte Desenvolvimento com sobreposições para obter mais informações). Isso ainda causava vários problemas ao atualizar o AEM como o conteúdo no **/libs** pode mudar, fazendo com que a funcionalidade de sobreposição seja interrompida de maneiras inesperadas. Os clientes também podem estender os componentes do AEM por meio da herança, por meio de `sling:resourceSuperType`ou simplesmente referenciar um componente no **/libs** diretamente por meio de sling:resourceType. Problemas de atualização semelhantes podem ocorrer com casos de uso de referência e substituição.

Para tornar mais seguro e fácil para os clientes compreenderem quais as áreas de **/libs** são seguros para usar e sobrepor o conteúdo no **/libs** foi classificado com as seguintes misturas:

* **Público (granite:PublicArea)** - Define um nó como público para que ele possa ser sobreposto, herdado ( `sling:resourceSuperType`) ou utilizados diretamente ( `sling:resourceType`). Os nós abaixo de /libs marcados como Public são seguros para atualização com a adição de um Pacote de compatibilidade. Em geral, os clientes devem usar somente nós marcados como Public.

* **Abstrato (granito:AbstractArea)** - Define um nó como abstrato. Os nós podem ser sobrepostos ou herdados ( `sling:resourceSupertype`), mas não utilizado diretamente ( `sling:resourceType`).

* **Final (granite:FinalArea)** - Define um nó como final. Idealmente, os nós classificados como finais não devem ser sobrepostos ou herdados. Os nós finais podem ser usados diretamente por meio de `sling:resourceType`. Os subnós no nó final são considerados internos por padrão.

* ***Interno (granite:InternalArea)*** *- *Define um nó como interno. Os nós classificados como internos idealmente não devem ser sobrepostos, herdados ou usados diretamente. Esses nós se destinam apenas à funcionalidade interna do AEM

* **Sem Anotação** - Os nós herdam a classificação com base na hierarquia de árvore. A raiz / é, por padrão, pública. **Os nós com um pai classificado como Interno ou Final também devem ser tratados como Internos.**

>[!NOTE]
>
Essas políticas só são aplicadas contra mecanismos baseados em caminho de pesquisa Sling. Outras áreas de **/libs** como uma biblioteca do lado do cliente pode ser marcada como `Internal`, mas ainda pode ser usado com a inclusão padrão clientlib. É importante que um cliente continue a respeitar a classificação Interna nesses casos.

#### Indicadores de tipo de conteúdo do CRXDE Lite {#crxde-lite-content-type-indicators}

Os mixins aplicados no CRXDE Lite mostram nós de conteúdo e árvores marcados como `INTERNAL` como esmaecida (acinzentada). Para `FINAL`, somente o ícone fica esmaecido. Os filhos desses nós também aparecem esmaecidos. A funcionalidade Sobrepor nó está desativada em ambos os casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Verificação de integridade do conteúdo**

>[!NOTE]
>
A partir do AEM 6.5, o Adobe recomenda o uso do Detector de padrões para detectar violações de acesso ao conteúdo. Os relatórios do detector de padrões são mais detalhados, detectam mais problemas e reduzem a probabilidade de falsos positivos.
>
Para obter mais informações, consulte [Avaliando a complexidade da atualização com o Detector de padrões](/help/sites-deploying/pattern-detector.md).

O AEM 6.5 é enviado com uma verificação de integridade para alertar os clientes se o conteúdo sobreposto ou referenciado for usado de forma inconsistente com a classificação do conteúdo.

A ** Verificação de acesso de conteúdo do Sling/Granite** é uma nova verificação de integridade que monitora o repositório para ver se o código do cliente está acessando incorretamente os nós protegidos no AEM.

Esta varredura **/apps** e normalmente leva vários segundos para ser concluída.

Para acessar essa nova verificação de integridade, faça o seguinte:

1. Na tela inicial do AEM, navegue até **Ferramentas > Operações > Relatórios de Integridade**
1. Clique em **Verificação de acesso ao conteúdo do Sling/Granite**.

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Após a conclusão da verificação, uma lista de avisos é exibida, notificando um usuário final sobre o nó protegido que está sendo referenciado incorretamente:

![screenshot-2018-2-5](assets/screenshot-2018-2-5healthreports.png)

Após corrigir as violações, ele retorna ao estado verde:

![screenshot-2018-2-5heartthereports-violações](assets/screenshot-2018-2-5healthreports-violations.png)

A verificação de integridade exibe informações coletadas por um serviço em segundo plano que verifica de forma assíncrona sempre que uma sobreposição ou tipo de recurso é usado em todos os caminhos de pesquisa do Sling. Se os mixins de conteúdo forem usados incorretamente, será relatada uma violação.
