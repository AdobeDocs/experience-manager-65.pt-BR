---
title: Notas de versão do [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre versões, novidades, instruções de instalação e uma lista de alterações detalhada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: e3219d57e069e546b177015e675666a8b927fb49
workflow-type: tm+mt
source-wordcount: '3825'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] Notas de versão do Service Pack 6.5 mais recente {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 6 de junho de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] O 6.5.21.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de desempenho, estabilidade e segurança lançadas desde a disponibilização inicial do 6.5, em abril de 2019. [Instalar este Service Pack](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principais recursos e melhorias

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Alguns dos principais recursos e aprimoramentos desta versão incluem:

* Uma credencial nova e mais fácil de usar para autenticação de servidor para servidor, substituindo a credencial existente da Conta de serviço (JWT). (NPR-41994)

* Aprimoramentos do Editor de regras no AEM Forms:
   * Suporte para implementar condições aninhadas com `When-then-else` funcionalidade.
   * Validar ou redefinir painéis e formulários, incluindo campos.
   * Suporte para recursos modernos do JavaScript, como funções de esquerda e seta (suporte para ES10) nas Funções personalizadas.
* API AutoTag para acessibilidade de PDF: O AEM Forms no OSGi agora oferece suporte à nova API AutoTag para aprimorar o PDF para padrões de acessibilidade, adicionando tags: parágrafos e listas. Isso torna os PDF mais acessíveis para usuários com tecnologia assistiva.
* Suporte a PNG de 16 bits: o serviço PDF Generator ImageToPdf agora oferece suporte à conversão de PNGs com intensidade de cor de 16 bits.
* Aplicar artefatos a blocos de texto individuais em XDPs: o Forms Designer agora permite que os usuários definam configurações em blocos de texto individuais em arquivos XDP. Essa capacidade permite controlar os elementos que são tratados como artefatos nos PDF resultantes. Esses elementos, como cabeçalhos e rodapés, são acessíveis para as tecnologias assistivas. Os principais recursos incluem marcar blocos de texto como artefatos e incorporar essas configurações nos metadados XDP. O serviço Forms Output aplica essas configurações durante a geração do PDF, garantindo a marcação adequada de PDF / UA.
* O AEM Forms Designer é certificado com `GB18030:2022` padrão. Com essa certificação, agora o Forms Designer oferece suporte ao conjunto de caracteres Unicode chinês que permite inserir caracteres chineses em todos os campos editáveis e caixas de diálogo.


### [!DNL Assets]

#### Aprimoramentos

Veja a seguir uma lista das melhorias incluídas nesta versão:

* A guia IPTC agora suporta [!UICONTROL Texto Alternativo] e [!UICONTROL Descrição Estendida] campos de texto. (ASSETS-34918)

#### Correções de acessibilidade

Esta é a lista de correções de acessibilidade incluídas nesta versão:

* Se o status de processamento de um ativo for Falha ou Metadados falharam, as legendas e a interface de rastreamento de áudio não funcionam adequadamente. (ASSETS-37281)
* Quando você salva um metadado de ativo e tenta editá-lo, o nome do idioma não é exibido. (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correção de problemas no Service Pack 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Acessibilidade {#sites-accessibility-6521}

* A variável **[!UICONTROL Pesquisas salvas]** rótulo não é persistente. O espaço reservado está sendo usado como o único rótulo visual de um campo de texto. (SITES-3050)

#### Interface do usuário do administrador{#sites-adminui-6521}

* Ao clicar em **[!UICONTROL Sites]** > **[!UICONTROL Componentes principais]** > **[!UICONTROL Propriedades]** > **[!UICONTROL Permissões]** guia > **[!UICONTROL Permissão efetiva]**, o **Permissões eficazes** A caixa de diálogo do não abre no. (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* Correção da dupla inclusão dos elementos de formulário. (SITES-21109)
* Ao criar um fragmento de conteúdo, o botão Fechar às vezes não responde, fazendo com que a página inteira congele e exigindo uma atualização de página para fechar o fragmento de conteúdo. Quanto ao problema de criação de versão, o sistema está criando uma nova versão de um fragmento de conteúdo. Esse problema ocorre mesmo quando o usuário não faz alterações, simplesmente interagindo com o RTE ou um campo de texto. (SITES-21187)

#### [!DNL Content Fragments] - API do GraphQL {#sites-graphql-api-6521}

* Ao atualizar o Adobe Experience Manager de 6.5.19.0 para 6.5.20.0, o caminho `/libs/cq/graphql/sites/graphiql` foi sendo excluído. (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### Fragmentos de experiência{#sites-experiencefragments-6521}

* Implantação de fragmentos de experiência do `masters/language` para `country/language` não atualiza referências cruzadas. (SITES-21172)
* Os modelos não são especificados apenas na variável `cq:allowedTemplates`, mas modelos que têm `allowedPaths` configurados no nível do modelo, aparecem como opções ao criar um novo Fragmento de experiência. (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->


<!-- ### [!DNL Forms]-->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->


#### MSM - Live Copies{#sites-msm-live-copies-6521}

* Sobrepor o componente Página para adicionar guias nas propriedades da página. Uma delas é a configuração de página e tem uma propriedade para adicionar um URL de fragmento de experiência. O link configurado nas propriedades da página do Fragmento de experiência não é alterado para nenhuma cópia de idioma criada para essa página. O link configurado deve ser alterado com o URL da cópia de idioma. (SITES-19580)

#### Editor de página{#sites-pageeditor-6521}

* O modo de edição aplica um plano de fundo cinza de forma inconsistente, o que não atende aos padrões de contraste de cores da WCAG (Web Content Accessibility Guidelines). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* Se um ativo for publicado no Brand Portal, o status de publicação permanecerá inconsistente. (ASSETS-36807)
* Os ativos não são excluídos quando você os exclui de uma instância usando uma chamada de API. (ASSETS-35131)
* Ao tentar importar metadados, uma variável `question mark (?)` O substitui a inserção de caracteres em qualquer idioma que não seja o inglês.  (ASSETS-35091)
* Quando `dc:title` for usada com a cadeia de caracteres de tipo de dados, a árvore de conteúdo do Assets não estará funcionando corretamente após a instalação do Service Pack 6.5.19. (ASSETS-34684)
* Um erro é mostrado se houver qualquer caractere especial no nome de um ativo. (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* No AEM 6.5.18, ele não mostra todos os pontos de acesso adicionados a um ativo ao editar os pontos de acesso. No entanto, todos os pontos de acesso funcionam em um ativo publicado, mas não podem ser editados posteriormente, se necessário. (ASSETS-33609)
* Os arquivos mais recentes do EPS que são carregados não geram miniaturas após o reprocessamento. (ASSETS-32617)
* Em Ferramentas > Ativos > Configuração de publicação do Dynamic Media > Atributos de solicitação, as entradas `Width(px)` e `Height(px)` são diferentes em espanhol, italiano e português. Eles não estão alinhados entre si nesses locais. (ASSETS-31896)
* A partir de 1 de maio de 2024, o Adobe Dynamic Media encerrou o suporte para o seguinte:
   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * As seguintes cifras fracas no TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

#### [!DNL Adaptive Forms] {#forms-6520}

* Quando um Formulário adaptável é enviado de uma instância de publicação do Adobe Experience Manager para um fluxo de trabalho do Adobe Experience Manager, o fluxo de trabalho não salva os anexos. (FORMS-14209)
* Quando um usuário clica em **Imprimir em PDF** No AEM Forms Service Pack 15 (6.5.15.0) no OSGi, a validação no lado do cliente falha, é evidente pelas mensagens de erro mostradas na janela Developer Tools Console. (FORMS-14029)
* Quando um usuário envia um formulário no AEM 6.5 Forms Service Pack 17 (6.5.17.0) ou Service Pack 18 (6.5.18.0), Service Pack 19 (6.5.19.0), a tradução das mensagens de &quot;Obrigado&quot; não funciona corretamente. No entanto, as mensagens são traduzidas corretamente no dicionário. (FORMS-13846)
* Quando um usuário pré-visualiza um formulário com um componente Seletor de data, o campo Seletor de data está desalinhado com os outros campos de formulário. (FORMS-13763)
* Quando um usuário no ambiente do AEM Forms Service Pack 19 (6.5.19.0) chama a API para formatar números, os números formatados não estão alinhados com as respectivas localidades. Como resultado, os sinais de moeda não são exibidos corretamente. O problema persiste independentemente do parâmetro Locale definido como &quot;de_DE&quot; ou &quot;en_US&quot;. (FORMS-13759)
* Quando um usuário no ambiente do AEM Forms Service Pack 19 (6.5.19.0) converte PNGs de 16 bits em PDF usando o serviço PDFG Img2Pdf, ocorre uma falha e não é possível &quot;Usar o serviço de conversão de imagem do Acrobat&quot;. (FORMS-13754)
* No AEM Forms Service Pack 19 (6.5.19.1), quando um usuário carrega um arquivo JobOptions existente na seção Services / PDF Generator / Adobe PDF AEM Settings do adminui do forms JEE, o upload falha. Ela também mostra a seguinte mensagem de erro (FORMS-13597):
  `"An error has occurred while processing your request. Please use the breadcrumb links to navigate to another page."`
* Quando um usuário migra do AEM Forms Service Pack 15 (6.5.15.0) para o AEM Forms Service Pack (6.5.17.0) ou o AEM Forms Service Pack (6.5.19.0), a chave FD é duplicada, o que faz com que os formulários não sejam traduzidos corretamente. (FORMS-13461)
* Quando um usuário coloca dispatchers na frente dos autores compatíveis com a topologia de implantação no AMS, o envio da Tarefa de atribuição trava ou falha. (FORMS-8010)
* Correções relacionadas à acessibilidade:
   * Os ícones na página &quot;formulários e documentos&quot; agora estão acessíveis de acordo com o padrão ANDI. (FORMS-13094)
   * Os usuários podem acessar a barra de ferramentas por meio do teclado para salvar ou editar conteúdo na página de edição, a barra de ferramentas é aprimorada de acordo com o padrão ANDI. (FORMS-13102)
   * Os campos de formulário &quot;Obrigatório ou Obrigatório&quot; podem ser acessados de acordo com o padrão ANDI. (FORMS-13097)

* Quando um usuário tenta visualizar um formulário no carregamento da página, ele não é renderizado. (FORMS-13594)
* O componente de campo de entrada de data não funciona corretamente no Microsoft Edge no modo de compatibilidade do Internet Explorer. (FORMS-13170)
* A notificação por email paralisado com anexo falhou ao ser enviada quando a correção para [etapas adicionais para usar o email com anexos](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/troubleshooting/additional-steps-to-use-email-with-attachments) é executado no servidor. (FORMS-14227)
* No AEM Forms Workspace no Service Pack 18 (6.5.18.0), ao comentar em qualquer documento carregado, o arquivo de documento é corrompido. (FORMS-13735)
* No AEM Forms Service Pack 18 (6.5.18.0), Service Pack 19 (6.5.19.0) ou Service Pack 20 (6.5.20.0), quando um usuário tenta procurar um Formulário adaptável no painel lateral, a pesquisa falha. (FORMS-14117)
* Quando um usuário edita um formulário criado em alemão e traduzido para inglês, isso resulta em exibições de idioma inconsistentes entre os modos &quot;Visualização&quot; e &quot;Editar&quot;. Isso faz com que os componentes RadioButton e Caixa de seleção sejam exibidos em inglês durante o modo &quot;Editar&quot;, enquanto aparecem corretamente em alemão durante o modo &quot;Visualização&quot;. (FORMS-13910)
* A ferramenta de processo de limpeza de processos falha com o erro `NoClassDefFoundError: org/omg/CORBA/UserException`. (FORMS-13751)
* Quando um usuário tenta incorporar um Formulário adaptável (AF) em uma página da Web, externa ou no AEM Sites, usando um contêiner incorporado, o contêiner do Guia de formulário adaptável introduz um RÓTULO ARIA. O rótulo tem o role=&quot;main&quot; para o formulário incorporado. De acordo com as diretrizes ARIA, deve haver apenas um role=&quot;main&quot; por página. Portanto, quando um usuário adiciona outro role=&quot;main&quot; para o conteúdo principal de sua página, ele é sinalizado como um problema de acessibilidade. (FORMS-13538)
* No AEM Forms Service Pack 19 (6.5.19.0), ao usar o menu suspenso em um Formulário adaptável, os menus suspensos com texto de espaço reservado retêm o valor de `id="emptyValue"`. Dessa forma, se um formulário tiver vários componentes suspensos, cada um terá `id="emptyValue"` que não está correto de acordo com as diretrizes ARIA. (FORMS-13370).
* Quando um usuário recarrega uma comunicação interativa depois que os dados são enviados por XML, ocorre um espaço em branco entre o bloco de texto no PDF gerado. (FORMS-13481)
* IPH ausente para a tela &quot;Preparar para a etapa de implantação do DSC&quot; ao executar o ConfigurationManager. (FORMS-10699)
* Quando um usuário adiciona um novo dicionário para traduzir um formulário com dicionários existentes, as traduções antigas são invalidadas. Os seguintes problemas surgem: (FORMS-13576)
   * Alguns campos não preenchem os dados traduzidos.
   * Alguns campos não são traduzidos para o novo idioma, mesmo que os dados sejam salvos no dicionário com êxito.

#### [!DNL Forms Designer] {#forms-desgner-6521}

* Quando um usuário adiciona uma nova tabela a um formulário existente usando o AEM Forms Designer no ambiente do AEM Forms Service Pack 19 (6.5.19.0), ele trava. (LC-3921978)
* Quando um usuário renderiza um formulário adaptável em um ambiente Linux®, ocorre um espaço extra entre os componentes do campo. (LC-3921957)
* Quando um usuário converte um arquivo XTG no formato PostScript usando o Serviço de saída, ocorre uma falha com o erro:           `(AEM_OUT_001_003:Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE)`. (LC-3921720)

  Para resolver o problema: verifique se os dados contêm caracteres especiais como Espaço de largura zero (0x200b). Se sim, use o sinalizador adicionando a tag `<behaviorOverride>patch-LC3921720:1</behaviorOverride>` no arquivo XCI, conforme especificado em [custom_xfa.xci](/help/forms/using/assets/custom_xfa.xci) arquivo.

* Ao usar o AEM Forms Service Pack 18 (6.5.18.0) em um ambiente Linux®, o XMLFM trava nas CPUs sem suporte à instrução AVX/AVX2 com processadores AMD®. (LC-3921718)
* Quando um usuário cria um PDF do XDP usando o serviço de saída do Forms, ele não pode definir &quot;configurações&quot; em &quot;blocos de texto individuais&quot; no XDP para controlar o que é &quot;artefato&quot;. (LC-3921954)

<!--
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.21.0 Forms add-on package release is scheduled for Thursday, June 13, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->


<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}


* Problema de atualização com AEM 6.5 Service Pack 19 (SP19) em que o caminho raiz de contexto do servidor de aplicativos está ausente para solicitações não autorizadas para o Apache Felix após a instalação do SP19. Atualização para o Apache Felix Web Management Console 4.9.8. (NPR-41933)

#### Campaign{#foundation-campaign-6521}

* O AEM 6.5 Service Pack 15 está produzindo registros de erros contínuos com entradas significativas. Os seguintes problemas foram relatados:
   * Erro 404 INFO para recurso ausente no caminho `/libs/granite/ui/content/shell/start.html`
   * Entrada de log de erros para uma SlingException não capturada devido a `NullPointerException` em `CampaignsDataSourceServlet.java:147`

  Os registros de erros não devem ser preenchidos com entradas de erros frequentes e volumosas, e a instância do AEM deve funcionar sem problemas relacionados à falta de recursos ou exceções. (CQ-4357064)

#### Cloud Services{#foundation-cloudservices-6521}

* Remova o Google Guava do AEM Cloud Service. (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->


<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* Não é possível selecionar **Excluir** ou **Modificar** sem **Procurar** no Navegador de configuração. (GRANITE-51002)

#### Integrações{#foundation-integrations-6521}

* Sobre `cq-target-integration`, é necessário remover o uso do Google Guava que não seja de teste. (CQ-4357101)
* Substituição de credenciais da conta de serviço (JSON Web Token ou JWT) por credenciais de servidor para servidor OAuth2 (também conhecidas como Entidades de Serviço). (NPR-41994)
* A solicitação de criação de público-alvo falha com a configuração do IMS (Identity Management System). (NPR-41888)
* Quando um cliente tenta visualizar a página de Carga, o conteúdo não é exibido corretamente devido a um URL malformado; um erro 404 é exibido. Um símbolo de ponto de interrogação ausente no URL, antes dos parâmetros de consulta, causou o erro. Esse problema exige que o cliente insira o símbolo do ponto de interrogação para visualizar a página Carga corretamente. (NPR-41957)
* Remover o código e a dependência do Adobe Search &amp; Promote do AEM 6.5, que chegou ao fim da vida útil em [Setembro de 2022 conforme aviso](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)

#### Localização{#foundation-localization-6521}

* No editor de modelos, a sequência de caracteres de texto *`No video available.`* não está localizado. (SITES-13190)
* A cadeia de caracteres após ativar ou desativar um usuário não está localizada em **Ferramentas** > **Segurança** > **Usuários** > *any_user_name* > **Ativar** > **OK** e selecione *any_user_name* > **Desativar** > **OK**. (NPR-41737)

#### Oak {#foundation-oak-6521}

* Correção de regressão de desempenho - Evite consultas de intervalo em condições semelhantes. (OAK-9481)
* A nova versão do Oak é a 1.22.20.

#### Platform{#foundation-platform-6521}

* A variável `Unclosed resource resolver` ocorreu um erro para `com.day.cq.mailer.impl.DefaultMailService`. A variável `MessageGatewayService` A classe, que estava pronta para uso, estava sendo usada sem um resolvedor de recursos. O problema ocorria em qualquer página com um botão de envio de formulário que envia um email usando essa classe. (NPR-41853)
* No **Sobre o Adobe Experience Manager** ainda é 2023. (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### Tradução{#foundation-translation-6521}

* Um problema com o status de tradução pronto para uso do AEM 6.5.19 não é atualizado conforme esperado para um lançamento. Após importar um arquivo traduzido para um trabalho de tradução associado a um lançamento do AEM, o status deveria ser `Approved`. Em vez disso, o status se tornou `Ready for Review`, que não é o comportamento esperado. (NPR-41756)
* Ao criar várias configurações e acessar as configurações de Cloud Service de tradução, nem todos os elementos são exibidos na interface. Somente os primeiros 40 elementos/pastas são exibidos; o carregamento lento é acionado, mas não é necessário adicionar mais conteúdo. (NPR-41829)
* Caracteres distorcidos ocorrem se houver japonês na página Permissões da interface do usuário de toque. (NPR-41794)
* O AEM 6.5.14 e 6.5.9 não envia um emoji para tradução. (CQ-4357000)

#### Interface do usuário{#foundation-ui-6521}

* Em Ferramentas > Segurança > Usuários > &lt;user_name> > Perfis, na guia **Editar configurações de usuário** não fecha a caixa de diálogo. (NPR-41793)
* O Granite `pathfield` componente em `/libs/granite/ui/components/coral/foundation/form/pathfield` falha ao ativar o **[!UICONTROL Selecionar]** quando um ativo é selecionado. Depois que o campo de caminho é exibido e o usuário seleciona a caixa de seleção do ativo, a variável **[!UICONTROL Selecionar]** O botão não está ativado; ele não muda de cinza para azul. (NPR-41970)
* Existe um problema com o campo de referência do Modelo de fragmento de conteúdo (CFM) no AEM. Apesar de o campo de referência CFM ser definido como obrigatório, o sistema permite que os usuários cliquem em Salvar para salvar conteúdo com valores não CFM em determinados cenários. O botão Salvar deve estar esmaecido (indisponível). (NPR-41894)
* As caixas de diálogo da interface do usuário Coral padrão que usam a `successresponse` A ação deve acionar uma Resposta de sucesso após a ação. Mas no AEM 6.5 Service Pack 19, a ação de recarregamento não é chamada e nenhuma mensagem é exibida. (NPR-41797)
* Os links de Notificações de AEM não estão funcionando no AEM 6.5 Service Pack 18. Ao atualizar para o Service Pack 18, os links de Notificações do AEM não funcionam ao selecionar as mensagens por meio do botão de notificações. (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### Fluxo de trabalho{#foundation-workflow-6521}

* No AEM 6.5.18, erros repetidos ao remover do cache de metadados do usuário durante a limpeza. (NPR-41762)

## Instalar [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] O 6.5.21.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.21.0 em uma das instâncias do Autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda que você remova ou desinstale o [!DNL Experience Manager] 6.5.21.0 pacote. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-la. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.

1. Baixe o Service Sack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes sai durante a instalação do Service Pack. A Adobe recomenda que você aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no [!DNL Safari] navegador, mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.21.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.21.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.21.0)` em [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` O é versão 1.22.20 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar o Service Pack do [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o Service Pack no Experience Manager Forms, consulte [Instruções de instalação do Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>O recurso de formulários adaptáveis, disponível no [Início rápido do AEM 6.5](https://experienceleague.adobe.com/br/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager{#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [Fragmento de conteúdo do Experience Manager com pacote de índice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam.

A falha na instalação deste pacote pode resultar em consultas lentas ou com falha do GraphQL.

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar{#uber-jar}

O UberJar para [!DNL Experience Manager] O 6.5.21.0 está disponível na [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
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

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas. Falha na consulta em segundo plano. Ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se você atualizar seu [!DNL Experience Manager] 6.5.0 - 6.5.4 para o Service Pack mais recente no Java™ 11, você verá `RRD4JReporter` exceções na `error.log` arquivo. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada no [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado no [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usar a API do Target Standard (autenticação IMS) e, em seguida, exportar os Fragmentos de experiência para o Target resulta na criação de tipos de oferta errados. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão não registrada da alteração de registro.

* A partir do AEM 6.5.15, o mecanismo Rhino JavaScript fornecido pelo ```org.apache.servicemix.bundles.rhino``` tem um novo comportamento de elevação. Scripts que usam o modo estrito (```use strict;```) têm que declarar suas variáveis corretas. Caso contrário, eles não serão executados e acabarão gerando um erro de tempo de execução.

* A instalação de marcação relacionada ao conteúdo pronto para uso por meio de um pacote de atualização oficial redefine a propriedade languages do `/content/cq:tags` para o padrão. Essa ação é verdadeira para Service Packs, Service Packs de segurança, Pacotes de recursos estendidos, Pacotes de recursos cumulativos, patches e assim por diante. Portanto, é necessário adicioná-lo das propriedades antes da instalação.

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Fragmentos de conteúdo - A visualização falha devido à proteção DoS para uma grande árvore de fragmentos. Consulte a [Artigo da KB sobre opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

<!--

### Known issues for AEM Forms {#known-issues-aem-forms-6521}
-->

### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6521}


* Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` no `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926).

  Execute as seguintes etapas para resolver o problema:

   1. Pare os localizadores e o servidor na ordem especificada, se estiverem em execução.
   1. Reinstale o patch executando o instalador de patches no modo administrador (Importante).
   1. Confirme se somente o Geode é compatível com `version 1.15.1.2` estão presentes.

  >[!NOTE]
  > Nenhuma ação é necessária se somente os jars de Geode com `version 1.15.1.2` estão presentes.

## Pacotes OSGi e pacotes de conteúdo incluídos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos neste [!DNL Experience Manager] Versão 6.5 do Service Pack:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.21.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos no Experience Manager 6.5.21.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites só estão disponíveis para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao cliente do Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Inscrever-se para obter atualizações de produtos de prioridade Adobe](https://www.adobe.com/subscription/priority-product-update.html)
