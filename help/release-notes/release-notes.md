---
title: Notas de versão do [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre versões, novidades, instruções de instalação e uma lista de alterações detalhada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 19fe527ce44d8ec5be50ebd32b46f13df96c52cc
workflow-type: tm+mt
source-wordcount: '2928'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] Notas de versão do Service Pack 6.5 mais recente {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 22 de fevereiro de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] O 6.5.20.0 inclui novos recursos, importantes melhorias solicitadas por clientes, correções de erros e melhorias de desempenho, estabilidade e segurança que foram lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este pacote de serviços](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principais recursos e melhorias

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alguns dos principais recursos e aprimoramentos desta versão incluem:

* O Dynamic Media agora é compatível com o formato de imagem HEIC sem perdas para Apple iOS/iPadOS. Consulte [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) na API do Dynamic Media Image Serving and Rendering.

* O Gerenciador de vários sites (MSM) agora é compatível com estruturas de Fragmento de experiência, incluindo pastas e subpastas, para a implantação eficiente em massa de Fragmentos de experiência em Live Copies.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correção de problemas no Service Pack 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interface do usuário do administrador{#sites-adminui-6520}

* A variável `Workflow Title` o campo está marcado com `*` conforme necessário, mas não há validação. (SITES-16491) NORMAL

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* As pastas de configuração aninhadas não eram mais suportadas e as pastas de modelo de fragmento de conteúdo não eram mais visíveis após a atualização para AEM 6.5.18 ou AEM 6.5.19. (SITES-18110) PRINCIPAL
* Algumas subpastas não conseguem selecionar modelos de fragmento de conteúdo herdados. Ele deve aceitar pastas sem ter um `jcr:content` mesmo que as pastas do DAM criadas por meio da interface do usuário tenham esse nó. (SITES-17943) NORMAL

#### [!DNL Content Fragments] - API do GraphQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Ao executar uma consulta do GraphQL para [filtrar resultados](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) usando variáveis opcionais, se um valor específico for **não** for fornecida para a variável opcional, a variável será ignorada na avaliação do filtro. (SITES-17051) NORMAL

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* Com a atualização do `org.json` houve uma mudança na forma como os números decimais eram desserializados. Antes eles eram convertidos &quot;por padrão&quot; em duplas e agora em BigDecimals. Em vez disso, os valores da propriedade de metadados, armazenados por meio da API REST, devem ser convertidos para Double a partir do BigDecimal. (SITES-16857) NORMAL

#### Infraestrutura principal{#sites-core-backend-6520}

* Quando a Publicação rápida de um fragmento de conteúdo é usada, ela continua sendo carregada e não é publicada. Ou seja, a Publicação rápida não está funcionando para Fragmentos de conteúdo após uma atualização do service pack de AEM 6.5.7 para AEM 6.5.17. Quando o usuário tentava publicar gerenciado, funcionava. No entanto, quando eles tentaram a Publicação rápida, ela não estava sendo publicada. Especificamente, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` causou a queda do sistema. (SITES-17311) PRINCIPAL
* Os fragmentos de conteúdo não são serializáveis com o exportador Jackson: o carregamento da página é interrompido quando há um fragmento de conteúdo referido em uma página (usa o código do exportador Jackson) e qualquer tag adicionada a um fragmento de conteúdo. (SITES-18096) NORMAL

#### Componentes principais{#sites-core-components-6520}

* A instalação do pacote dos Componentes principais do CIF nas causas do AEM `:type` valor dos componentes existentes a ser alterado. A alteração significa que eles não serão mais renderizados nas páginas às quais foram adicionados. (SITES-17601) PRINCIPAL

#### Integração do Campaign{#sites-campaign-integration-6520}

* AEM estava usando uma inclui na lista de permissões, também conhecida como `whitelist`- devido a um relatório de vulnerabilidade. A inclui na lista de permissões ➡ impedia que os clientes usassem a funcionalidade necessária. (SITES-16822) CRÍTICO

#### Fragmentos de experiência{#sites-experiencefragments-6520}

* O MSM para fragmentos de experiência agora oferece suporte à implantação em massa em estruturas de conteúdo de fragmento de experiência, incluindo pastas e subpastas. (SITES-16004) MAJOR

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live Copies{#sites-msm-live-copies-6520}

* Um &quot;`Is not modifiable`&quot;a exceção é lançada ao implantar o componente. Especificamente, um `org.apache.sling.servlets.post.impl.operations.ModifyOperation` ocorre uma exceção durante o processamento da resposta. (SITES-18809) MAJOR
* Não foi possível implantar alterações em Live Copies específicas de Fragmentos de experiência. (SITES-17930) MAJOR
* Quando um usuário adiciona uma anotação a um componente em uma página do blueprint e a implanta, a contagem de anotações na Live Copy é exibida incorretamente. (SITES-17099) PRINCIPAL
* O botão Implantação do MSM da página principal para a página secundária é dividido na interface gráfica do usuário de toque; quando selecionado, o seguinte erro é exibido: `Uncaught TypeError: _g.shared is undefined`. (SITES-16991) PRINCIPAL

#### Editor de página{#sites-pageeditor-6520}

* A visualização do Editor de temas do Forms está corrompida. Quando a opção Visualizar estiver selecionada, somente um ícone de carregamento ficará visível. BLOQUEADOR (SITES-17164)

### [!DNL Assets]{#assets-6520}

* Não é possível validar campos baseados em regras no auxiliar do editor de metadados e exibe uma mensagem de erro &quot;Campos obrigatórios ausentes&quot;. (ASSETS-31396) PRINCIPAL
* Depois que um PDF é movido para outro local, a variável **[!UICONTROL Exibir página]** desaparece. (ASSETS-30538) PRINCIPAL
* Não é possível selecionar uma imagem com permissões de leitura. (ASSETS-32199) NORMAL
* Não é possível alterar o tamanho do cartão nas configurações de exibição. (ASSETS-31667) NORMAL
* Falha no upload ao carregar o tipo de arquivo .oft. (ASSETS-30109) NORMAL
* Quando você tenta adicionar um campo de metadados personalizado como uma coluna adicional ao relatório, as caixas de seleção não são selecionadas. (ASSETS-31671) PEQUENO
* A operação de movimentação de ativos não funciona adequadamente no Experience Manager Service Pack 16. (ASSETS-30598) PEQUENO

#### [!DNL Dynamic Media]{#assets-dm-6520}

* Quando um ativo é carregado para AEM, a variável `Update_asset` fluxo de trabalho é acionado. No entanto, o workflow nunca é concluído. O fluxo de trabalho só é concluído até a etapa de upload do produto. A próxima etapa é o upload em lote do Scene7, mas esse processo não está sendo direcionado para o AEM. (ASSETS-30443) CRÍTICO
* Você precisa de uma maneira melhor de lidar com vídeos que não sejam do Dynamic Media normalmente no componente do Dynamic Media. Esse problema estava dando uma exceção ao instanciar `dynamicmedia_sly.js`. (ASSETS-31301) PRINCIPAL
* A visualização funciona para todos os ativos, conjuntos de vídeos adaptáveis e vídeos. No entanto, ele emite um erro 403 para `.m3u8` (que, aliás, ainda funcionam através de ligações públicas). (ASSETS-31882) PRINCIPAL
* A variável `scene7SmartCropProcessingStatus` Status de corrigido. Os metadados de vídeo de Recorte inteligente usados para mostrar falha mesmo quando era bem-sucedido. (ASSETS-31255) PEQUENO

### [!DNL Forms]{#forms-6520}

Correções na [!DNL Experience Manager] Os Forms são entregues por meio de um pacote complementar separado uma semana após o agendamento [!DNL Experience Manager] Data de lançamento do Service Pack. Nesse caso, a versão do pacote complementar do AEM 6.5.20.0 Forms está programada para quinta-feira, 29 de fevereiro de 2024. Uma lista de correções e aprimoramentos do Forms foi adicionada a esta seção após a versão.

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

#### [!DNL Forms Designer]{#forms-designer-6520}

* text

<!-- ### Foundation{#foundation-6520}

* text -->

#### Communities {#communities-6520}

* O diagnóstico de sincronização de usuário falha após a configuração bem-sucedida da sincronização de usuário. (NPR-41693) NORMAL

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Integrações{#integrations-6520}

* Remova todos os códigos e dependências do Adobe Search &amp; Promote do AEM 6.5. (NPR-40856) NORMAL

#### Localização{#localization-6520}

* O rótulo &quot;close&quot; de Aria não está localizado em **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**, selecione uma pasta e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]** > **[!UICONTROL Permissões]** guia > nome do membro. (NPR-41705) PRINCIPAL
* Há uma dica de ferramenta truncada para o **[!UICONTROL Senha da chave de armazenamento]** na página Configuração do SSL das localidades ENG, FRA, KOR, DEU e PTB. (NPR-41367) NORMAL

<!-- #### Oak{#oak-6520}

* text -->

#### Platform{#foundation-platform-6520}

* Problema na integração do Campaign com o AEM causado pelo servlet /api não retornar o esquema correto no json href. O motivo era porque o AEM não estava recebendo o cabeçalho X-Forward-Proto, o que forçou a solicitação a responder com um esquema HTTP em vez de HTTPS. Dessa forma, a capacidade de alternar a seleção do esquema com base em uma configuração OSGI deve ser adicionada. (GRANITE-48454) MAJOR

<!-- #### Replication{#foundation-replication-6520}

* text -->

#### Sling{#foundation-sling-6520}

* A variável `org.apache.sling.resourceMerger` O pacote 1.4.2 gera uma exceção do AEM 6.5, Service Pack 17 e posterior. A Sling resource fusion 1.4.4 deve ser incluída no Service Pack 20. (NPR-41630) NORMAL

#### Tradução{#foundation-translation-6520}

* Após a implantação do AEM 6.5 Service Pack 18, houve um problema com a guia Filtros no Editor de regras de tradução. Quando um Contexto for selecionado, ao clicar em Editar > Salvar, uma aspa dupla como caractere de HTML será exibida na próxima vez que você abrir o mesmo Contexto. Basicamente, as regras de tradução não eram salvas corretamente. (NPR-41624) PRINCIPAL
* Problemas relacionados às traduções do Fragmento do conteúdo, em que as cadeias de caracteres traduzidas estão sendo enviadas de volta do provedor de tradução para o AEM, mas estão travadas no `/content/projects` e não atualizar os Fragmentos de conteúdo. (NPR-41516) PRINCIPAL
* Uma mensagem de erro é exibida ao criar uma cópia de idioma. Ele ocorre em uma página que tem um fragmento de conteúdo referenciado em uma propriedade de página, usando modelos de fragmento de conteúdo. (NPR-41441) PRINCIPAL
* Os links nos Fragmentos de experiência não são ajustados para o idioma correto durante a Cópia de idioma. Em vez disso, o Fragmento de experiência aponta para o local principal. (NPR-41343) NORMAL

#### Interface do usuário{#foundation-ui-6520}

* Ocorre um erro de console após uma atualização para AEM 6.5, Service Pack 18. O erro está no estado `coralUI3.js` e ocorre ao selecionar qualquer menu suspenso no AEM. Especificamente, isso acontece com um `onOverlayToggle` evento. O erro `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` é exibido. (NPR-41467) PRINCIPAL
* No AEM, **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Marcação]** > **[!UICONTROL Criar]** > **[!UICONTROL Criar tag]**, inserindo caracteres não latinos no **Título** o campo causa a **Nome** campo a ser preenchido apenas com o caractere de hífen ( `-` ). (NPR-41623) NORMAL
* O ano de direitos autorais está incorreto no `About Adobe Experience Manager` caixa de diálogo. (NPR-41526) NORMAL
* Há não traduzidos **[!UICONTROL Propriedades do perfil]** strings ao editar as configurações do usuário. Ocorre em todas as localidades. (NPR-41365) NORMAL

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Instalar [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do pacote de serviços está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.20.0 em uma das instâncias do Autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda que você remova ou desinstale o [!DNL Experience Manager] 6.5.20.0 pacote. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-la. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o pacote de serviços em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.

1. Baixe o pacote de serviços de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, um diálogo na interface do usuário do Gerenciador de pacotes é fechado durante a instalação do pacote de serviços. A Adobe recomenda que você aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no [!DNL Safari] navegador, mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL Experience Manager] 6.5.20.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.20.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.20.0)` em [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.18 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar o Service Pack do [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o pacote de serviços no Experience Manager Forms, consulte [Instruções de instalação do Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>O recurso de formulários adaptáveis, disponível no [Início rápido do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager{#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [Fragmento de conteúdo do Experience Manager com pacote de índice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam.

A falha na instalação deste pacote pode resultar em consultas lentas ou com falha do GraphQL.

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar{#uber-jar}

O UberJar para [!DNL Experience Manager] O 6.5.20.0 está disponível na [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Então, não há `classifier`, com `apis` como o valor, para o `dependency` tag.

## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md/).

## Problemas conhecidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **Relacionado ao Oak**
A partir do Service Pack 13 e superior, o seguinte log de erros começou a aparecer, afetando o cache de persistência:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Para resolver essa exceção, faça o seguinte:

   1. Exclua as duas pastas a seguir de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale o Service Pack ou reinicie o Experience Manager as a Cloud Service.
Novas pastas de `cache` e `diff-cache` são criadas automaticamente e você não enfrenta mais uma exceção relacionada ao `mvstore` no `error.log`.

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Uma consulta do GraphQL pode usar o `damAssetLucene` índice em vez de `fragments` índice. Essa ação pode resultar em consultas GraphQL que falham ou demorar muito para ser executada.

  Para corrigir o problema, `damAssetLucene` deve ser configurado para incluir as duas propriedades a seguir em `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Depois que a definição do índice é alterada, é necessária uma reindexação (`reindex` = `true`).

  Após essas etapas, as consultas do GraphQL devem ser executadas mais rapidamente.

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas, já que a consulta em segundo plano falha. Ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se você atualizar seu [!DNL Experience Manager] 6.5.0 - 6.5.4 para o pacote de serviços mais recente no Java™ 11, você verá `RRD4JReporter` exceções na `error.log` arquivo. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada no [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado no [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usar a API do Target Standard (autenticação IMS) e, em seguida, exportar os Fragmentos de experiência para o Target resulta na criação de tipos de oferta errados. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão não registrada da alteração de registro.

* A partir do AEM 6.5.15, o mecanismo Rhino JavaScript fornecido pelo ```org.apache.servicemix.bundles.rhino``` tem um novo comportamento de elevação. Scripts que usam o modo estrito (```use strict;```) precisam declarar corretamente as variáveis, caso contrário, elas não serão executadas, gerando um erro de tempo de execução.

### Problemas conhecidos do AEM Forms

#### Plataformas compatíveis

* O JDK 11.0.20 não é compatível com a instalação do AEM Forms no instalador do JEE. Somente o JDK 11.0.19 ou versões anteriores são compatíveis com a instalação do AEM Forms no instalador do JEE. (FORMS-10659)

#### Instalação

* Na plataforma JBoss® 7.1.4, quando o usuário instala o Experience Manager 6.5.16.0 ou o service pack posterior, `adobe-livecycle-jboss.ear` falha na implantação. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* Após instalar o instalador completo do AEM Service Pack 6.5.20.0, a implantação do EAR falha no JEE usando o JBoss® Turnkey. <!-- UPDATE FOR EACH NEW RELEASE -->

Para resolver o problema, localize o `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` arquivo e atualização `Adobe_Adobe_JAVA_HOME` para `Adobe_JAVA_HOME` para todas as ocorrências antes de executar o gerenciador de configurações. (CQDOC-20803)

#### Instalar o fragmento do servlet (AEM Service Pack 6.5.14.0 ou anterior)

* Se você estiver atualizando para o AEM Service Pack 6.5.15.0 ou superior e sua instância AEM estiver operando no Tomcat 8.5.88, é obrigatório instalar o fragmento de servlet. Fazer esta instalação *antes* você continua com a instalação do Service Pack 6.5.15.0 ou superior.
* É obrigatório instalar o fragmento de servlet para todos os servidores de aplicações, exceto aqueles executados no JBoss® EAP 7.4.0.

**Para instalar o fragmento de servlet:**

1. Baixe o fragmento do servlet de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Inicie o servidor de aplicativos.
1. Aguarde os registros estabilizarem e verifique o estado do pacote.
1. Abra os Pacotes de console da Web. O URL padrão é `http://[Server]:[Port]/system/console/bundles`.
1. Selecionar **[!UICONTROL Instalar]** ou **[!UICONTROL Atualizar]**.
1. Selecionar o fragmento baixado
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Selecionar **[!UICONTROL Instalar]** ou **[!UICONTROL Atualizar]**.
1. Aguarde o servidor de aplicativos estabilizar.
1. Interrompa o servidor de aplicativos.

#### Adaptive Forms

* Quando um Formulário adaptável é publicado, todas as suas dependências, incluindo políticas, são republicadas, mesmo que nenhuma modificação tenha sido feita nelas. (FORMS-10454)
* Quando um usuário opta por configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar algum outro campo do Formulário adaptável no mesmo editor resolve o problema.
* Quando os usuários executam a ação de envio, o envio falha com um erro:
  `javax.servlet.ServletException: java.lang.NoSuchMethodError`
Para resolver o problema, [recompile os scripts do Sling, como JSP, Java™ e Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html#resolution). (FORMS-8542)
* Após instalar o AEM Service Pack 6.5.14.0 e posteriores, os usuários não podem selecionar uma fonte na interface do usuário do JEE Admin para documentos do PDF ao navegar até `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`, pois a lista de fontes aparece vazia. (FORMS-12095)
<!-- When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) -->
* No AEM Forms no JEE, o Forms HTML5 que usa o caminho de contexto não é renderizado. (FORMS-12485, FORMS-12691). Uma correção está disponível para esse problema. Para baixar e instalar o hotfix, consulte [Hotfixes do Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md).
* O Forms adaptável permite usar funções personalizadas com o ECMAScript versão 5 ou anterior. Quando uma função personalizada usa o ECMAScript versão 6 ou posterior, como &quot;let&quot;, &quot;const&quot; ou funções de seta, o editor de regras pode não abrir corretamente.

#### AEM Forms no JEE

* Vulnerabilidades críticas de segurança foram relatadas para Struts 2 RCE, uma estrutura de aplicativo Web popular e de código aberto para o desenvolvimento de aplicativos Web Java™ EE. O Adobe lançou [AEM 6.5 Service Pack 19.1 (6.5.19.1)](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) para lidar com a vulnerabilidade no AEM Forms no JEE.

<!--The font enumeration fails due to the missing Ps2Pdf service file.-->

## Pacotes OSGi e pacotes de conteúdo incluídos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos neste [!DNL Experience Manager] Versão 6.5 do Service Pack:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos no Experience Manager 6.5.20.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites só estão disponíveis para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscrever-se para obter atualizações de produtos de prioridade Adobe](https://www.adobe.com/subscription/priority-product-update.html)
