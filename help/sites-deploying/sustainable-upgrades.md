---
title: Atualizações sustentáveis
seo-title: Sustainable Upgrades
description: Saiba mais sobre atualizações sustentáveis no AEM 6.4.
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Atualizações sustentáveis{#sustainable-upgrades}

## Estrutura de personalização {#customization-framework}

### Arquitetura (funcional/infraestrutura/conteúdo/aplicativo)  {#architecture-functional-infrastructure-content-application}

O recurso Estrutura de personalização foi projetado para ajudar a reduzir as violações em áreas não extensíveis do código (como APIS) ou conteúdo (como sobreposições), que não são amigáveis para atualização.

Há dois componentes da estrutura de personalização: a variável **Superfície da API** e a variável **Classificação de conteúdo**.

#### Superfície da API {#api-surface}

Em versões anteriores do AEM, muitas APIs foram expostas por meio do Uber Jar. Algumas dessas APIs não eram destinadas a serem usadas por clientes, mas foram expostas à funcionalidade AEM compatível em pacotes. Além disso, as APIs do Java serão marcadas como Públicas ou Privadas para indicar aos clientes quais APIs são seguras para usar no contexto de atualizações. Outras especificidades incluem:

* APIs Java marcadas como `Public` podem ser usados e referenciados por pacotes de implementação personalizados.

* As APIs públicas serão compatíveis com a instalação de um pacote de compatibilidade.
* O pacote de compatibilidade conterá uma compatibilidade Uber JAR para garantir a compatibilidade com versões anteriores
* APIs Java marcadas como `Private` destinam-se a ser usados apenas por pacotes internos AEM e não devem ser usados por pacotes personalizados.

>[!NOTE]
>
>O conceito de `Private` e `Public` neste contexto, não devem ser confundidas com noções Java de classes públicas e privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificações de conteúdo {#content-classifications}

O AEM há muito tempo usa o principal das sobreposições e do Sling Resource Merger para permitir que os clientes estendam e personalizem a funcionalidade do AEM. Funcionalidade predefinida na qual os consoles e a interface do usuário do AEM são armazenados **/libs**. Os clientes nunca devem modificar nada abaixo de **/libs** mas pode adicionar conteúdo adicional abaixo de **/apps** para sobrepor e estender a funcionalidade definida em **/libs** (Consulte Desenvolvimento com sobreposições para obter mais informações). Isso ainda causava vários problemas ao atualizar o AEM como o conteúdo no **/libs** pode mudar, fazendo com que a funcionalidade de sobreposição seja interrompida de maneiras inesperadas. Os clientes também podem estender os componentes do AEM por meio da herança via `sling:resourceSuperType`ou simplesmente referenciar um componente no **/libs** diretamente via sling:resourceType. Problemas de atualização semelhantes podem ocorrer com casos de uso de referência e substituição.

Para tornar mais seguro e fácil para os clientes compreenderem quais as áreas de **/libs** são seguros para usar e sobrepor o conteúdo no **/libs** foi classificado com as seguintes misturas:

* **Público (granite:PublicArea)** - Define um nó como público para que ele possa ser sobreposto, herdado ( `sling:resourceSuperType`) ou utilizados diretamente ( `sling:resourceType`). É seguro atualizar os nós abaixo de /libs marcados como Public com a adição de um pacote de compatibilidade. Em geral, os clientes devem utilizar somente os nós marcados como Públicos.

* **Abstrato (granito:AbstractArea)** - Define um nó como abstrato. Os nós podem ser sobrepostos ou herdados ( `sling:resourceSupertype`), mas não deve ser utilizado diretamente ( `sling:resourceType`).

* **Final (granite:FinalArea)** - Define um nó como final. Idealmente, os nós classificados como finais não devem ser sobrepostos ou herdados. Os nós finais podem ser usados diretamente via `sling:resourceType`. Os subnós no nó final são considerados internos por padrão.

* ***Interno (granite:InternalArea)*** *- *Define um nó como interno. Os nós classificados como internos idealmente não devem ser sobrepostos, herdados ou usados diretamente. Esses nós se destinam apenas à funcionalidade interna do AEM

* **Sem Anotação** - Os nós herdam a classificação com base na hierarquia de árvore. A raiz / é, por padrão, pública. **Os nós com um pai classificado como Interno ou Final também devem ser tratados como Internos.**

>[!NOTE]
>
>Essas políticas só são aplicadas em relação aos mecanismos baseados no caminho de pesquisa do Sling. Outras áreas de **/libs** como uma biblioteca do lado do cliente pode ser marcada como `Internal`, mas ainda pode ser usado com a inclusão padrão clientlib. É importante que um cliente continue a respeitar a classificação Interna nesses casos.

#### Indicadores de tipo de conteúdo do CRXDE Lite {#crxde-lite-content-type-indicators}

Os mixins aplicados no CRXDE Lite mostrarão nós de conteúdo e árvores marcados como `INTERNAL` como acinzentado. Para `FINAL` somente o ícone fica esmaecido. Os filhos desses nós também aparecerão em cinza. A funcionalidade Sobrepor nó está desativada em ambos os casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Verificação de integridade do conteúdo**

>[!NOTE]
>
>A partir do AEM 6.5, o Adobe recomenda o uso do Detector de padrões para detectar violações de acesso ao conteúdo. Os relatórios do detector de padrões são mais detalhados, detectam mais problemas e reduzem a probabilidade de falsos positivos.
>
>Para obter mais informações, consulte [Avaliando a complexidade da atualização com o Detector de padrões](/help/sites-deploying/pattern-detector.md).

O AEM 6.5 será enviado com uma verificação de integridade para alertar os clientes se um conteúdo sobreposto ou referenciado for usado de forma inconsistente com a classificação do conteúdo.

A ** Verificação de acesso de conteúdo do Sling/Granite** é uma nova verificação de integridade que monitora o repositório para ver se o código do cliente está acessando incorretamente os nós protegidos no AEM.

Isso fará a varredura **/apps** e normalmente leva vários segundos para ser concluída.

Para acessar essa nova verificação de integridade, é necessário fazer o seguinte:

1. Na tela inicial do AEM, navegue até **Ferramentas > Operações > Relatórios de Integridade**
1. Clique no link **Verificação de acesso ao conteúdo do Sling/Granite** conforme mostrado abaixo:

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Após a conclusão da verificação, uma lista de avisos será exibida notificando um usuário final sobre o nó protegido que está sendo referenciado incorretamente:

![screenshot-2018-2-5](assets/screenshot-2018-2-5healthreports.png)

Após corrigir as violações, ele retornará ao estado verde:

![screenshot-2018-2-5heartthereports-violações](assets/screenshot-2018-2-5healthreports-violations.png)

A verificação de integridade exibe informações coletadas por um serviço em segundo plano que verifica de forma assíncrona sempre que uma sobreposição ou tipo de recurso é usado em todos os caminhos de pesquisa do Sling. Se os mixins de conteúdo forem usados incorretamente, será relatada uma violação.
