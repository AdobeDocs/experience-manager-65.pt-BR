---
title: Atualizações sustentáveis
seo-title: Atualizações sustentáveis
description: Saiba mais sobre atualizações sustentáveis no AEM 6.4.
seo-description: Saiba mais sobre atualizações sustentáveis no AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Atualizações sustentáveis{#sustainable-upgrades}

## Estrutura de personalização {#customization-framework}

### Arquitetura (Funcional / Infraestrutura / Conteúdo / Aplicativo) {#architecture-functional-infrastructure-content-application}

O recurso de Estrutura de personalização foi criado para ajudar a reduzir as violações em áreas não extensíveis do código (como APIS) ou conteúdo (como sobreposições) que não são amigáveis à atualização.

Há dois componentes da estrutura de personalização: a superfície **da** API e a classificação **do** conteúdo.

#### Superfície da API {#api-surface}

Em versões anteriores do AEM, muitas APIs eram expostas por meio do Jar do Uber. Algumas dessas APIs não foram destinadas aos clientes, mas foram expostas ao suporte à funcionalidade do AEM em pacotes. A partir de agora, as APIs de Java serão marcadas como Públicas ou Privadas para indicar aos clientes quais APIs são seguras para usar no contexto de atualizações. Outras especificações incluem:

* APIs Java marcadas como `Public` podem ser usadas e referenciadas por pacotes de implementação personalizados.

* As APIs públicas serão compatíveis com a instalação de um pacote de compatibilidade.
* O pacote de compatibilidade conterá um Uber JAR compatível para garantir compatibilidade com versões anteriores
* As APIs Java marcadas como `Private` são destinadas a serem usadas apenas por pacotes internos do AEM e não devem ser usadas por pacotes personalizados.

>[!NOTE]
>
>O conceito de `Private` e `Public` neste contexto não deve ser confundido com noções Java de classes públicas e privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classificações de conteúdo {#content-classifications}

O AEM utiliza há muito o principal das sobreposições e da Fusão de recursos Sling para permitir que os clientes estendam e personalizem a funcionalidade do AEM. A funcionalidade predefinida que alimenta os consoles do AEM e a interface do usuário são armazenados em **/libs**. Os clientes nunca devem modificar nada abaixo **/libs** , mas podem adicionar conteúdo adicional abaixo **/aplicativos** para sobrepor e estender a funcionalidade definida em **/libs** (consulte Desenvolvimento com sobreposições para obter mais informações). Isso ainda causou vários problemas ao atualizar o AEM, pois o conteúdo em **/libs** pode mudar, fazendo com que a funcionalidade de sobreposição quebre de maneiras inesperadas. Os clientes também podem estender os componentes do AEM por herança via `sling:resourceSuperType`, ou simplesmente fazer referência a um componente em **/libs** diretamente por sling:resourceType. Problemas semelhantes de atualização podem ocorrer com casos de referência e substituição de uso.

Para tornar mais seguro e fácil para os clientes compreender quais áreas de **/libs** são seguras para usar e sobrepor o conteúdo em **/libs** , foi classificado com as seguintes combinações:

* **Public (granite:PublicArea)** - Define um nó como público para que possa ser sobreposto, herdado ( `sling:resourceSuperType`) ou usado diretamente ( `sling:resourceType`). Os nós abaixo de /libs marcados como Público serão seguros para atualizar com a adição de um Pacote de compatibilidade. Em geral, os clientes devem aproveitar apenas os nós marcados como Público.

* **Abstrato (granite:AbstractArea)** - Define um nó como abstrato. Os nós podem ser sobrepostos ou herdados ( `sling:resourceSupertype`), mas não devem ser usados diretamente ( `sling:resourceType`).

* **Final (granite:FinalArea)** - Define um nó como final. Os nós classificados como finais idealmente não devem ser sobrepostos ou herdados. Os nós finais podem ser usados diretamente via `sling:resourceType`. Os subnós no nó final são considerados internos por padrão.

* ***Interno (granite:InternalArea)*** *- *Define um nó como interno. Os nós classificados como internos idealmente não devem ser sobrepostos, herdados ou usados diretamente. Esses nós são destinados apenas à funcionalidade interna do AEM

* **Sem anotação** - os nós herdam a classificação com base na hierarquia da árvore. A raiz / é, por padrão, Público. **Os nós com um pai classificado como Interno ou Final também devem ser tratados como Interno.**

>[!NOTE]
>
>Essas políticas só são aplicadas contra mecanismos baseados em caminho de pesquisa Sling. Outras áreas de **/libs** como uma biblioteca do lado do cliente podem ser marcadas como `Internal`, mas ainda podem ser usadas com a inclusão padrão do clientlib. É importante que um cliente continue a respeitar a classificação Interna nesses casos.

#### Indicadores de tipo de conteúdo CRXDE Lite {#crxde-lite-content-type-indicators}

As misturas aplicadas no CRXDE Lite mostrarão os nós de conteúdo e as árvores marcadas como `INTERNAL` esmaecidas. Apenas `FINAL` o ícone fica acinzentado. Os filhos desses nós também aparecerão em cinza. A funcionalidade Nó de sobreposição está desativada em ambos os casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Verificação de integridade do conteúdo**

>[!NOTE]
>
>A partir do AEM 6.5, a Adobe recomenda usar o Detector de padrão para detectar violações de acesso ao conteúdo. Os relatórios de detector de padrões são mais detalhados, detectam mais problemas e reduzem a probabilidade de falsos positivos.
>
>Para obter mais informações, consulte [Avaliação da complexidade de atualização com o Detector](/help/sites-deploying/pattern-detector.md)de padrões.

O AEM 6.5 será enviado com uma verificação de integridade para alertar os clientes se o conteúdo sobreposto ou referenciado for usado de uma forma inconsistente com a classificação do conteúdo.

A** Sling/Granite Content Access Check** é uma nova verificação de integridade que monitora o repositório para verificar se o código do cliente está acessando indevidamente nós protegidos no AEM.

Isso fará a varredura **/aplicativos** e, normalmente, levará vários segundos para ser concluído.

Para acessar essa nova verificação de integridade, é necessário fazer o seguinte:

1. Na tela inicial do AEM, navegue até **Ferramentas > Operações > Relatórios de integridade**
1. Clique em **Sling/Granite Content Access Check (Verificação** de acesso ao conteúdo Sling/Granite) conforme mostrado abaixo:

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Após a verificação ser concluída, uma lista de avisos será exibida, notificando um usuário final do nó protegido que está sendo referenciado incorretamente:

![screenshot-2018-2-5relatórios de saúde](assets/screenshot-2018-2-5healthreports.png)

Depois de corrigir as violações, ele voltará ao estado verde:

![screenshot-2018-2-5relatórios de saúde-violações](assets/screenshot-2018-2-5healthreports-violations.png)

A verificação de integridade exibe informações coletadas por um serviço em segundo plano que verifica de forma assíncrona sempre que uma sobreposição ou tipo de recurso é usado em todos os caminhos de pesquisa Sling. Se as mixagens de conteúdo forem usadas incorretamente, isso reporta uma violação.
