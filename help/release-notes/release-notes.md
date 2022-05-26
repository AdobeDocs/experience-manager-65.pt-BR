---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] 6.5 notas descrevendo as informações da versão, novidades, como instalar e listas detalhadas de alterações."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 6c9e8f1e62fe1a193cb9938e5f789e1e08b8339d
workflow-type: tm+mt
source-wordcount: '3546'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5 Notas de versão mais recentes do Service Pack {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.13.0 |
| Tipo | Versão do Service Pack |
| Data | 26 de maio de 2022 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## O que está incluído em [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] O 6.5.13.0 inclui novos recursos, principais melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este service pack](#install) on [!DNL Experience Manager] 6.5.

As seguintes correções de erros, principais recursos e melhorias foram introduzidas em [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* Ao tentar editar um campo suspenso somente leitura, o valor suspenso é redefinido como vazio. (NPR-38389)
* O usuário não pode assimilar um ativo de vídeo (.mp4) se não houver áudio no arquivo de vídeo. O fluxo de trabalho Ativo de atualização do DAM falha e reflete uma mensagem de erro. (NPR-38116)
* Ao usar o Assistente para mover ativos para mover uma pasta contendo ativos, o fluxo de trabalho falha e reflete uma mensagem de erro. (NPR-38061)
* Falha do fluxo de trabalho de transcodificação FFmpeg para o perfil FLV Video. (CQ-4343249)
* Depois de atualizar para [!DNL Experience Manager] 6.5 SP10, o editor de metadados de ativos não está funcionando corretamente. (CQ-4341359)
* Ao abrir uma Coleção inteligente salva com o filtro de pesquisa aplicado como Publicar, o filtro de pesquisa muda automaticamente para Não publicado. (CQ-4341191)
* Ao alternar o idioma em **[!UICONTROL Preferência do usuário]**, o rótulo **[!UICONTROL Ordenar por]**, o botão suspenso e outras opções nas opções de classificação na página inicial do Ativo não são refletidas no idioma selecionado. (CQ-4339306)
* Ao adicionar uma regra a um campo suspenso em **[!UICONTROL Esquema de metadados]**, o **[!UICONTROL Dependente de]** lista não reflete o rótulo do campo da lista suspensa. (ATIVO-9442)
* O menu suspenso Metadados de ativos desativados não retém valores. (ASSETS-8918)
* Ao visualizar o ativo usando **[!UICONTROL Mais detalhes]** em **[!UICONTROL Coluna]** , anotações incorretas são exibidas. (ASSETS-8851)
* Ao criar um ativo duplicado com uma versão diferente, as renderizações não são geradas. (ATIVO-8607)

* Um usuário não administrador pode publicar um ativo que já tenha sido check-out por outro usuário. (NPR-38128)
* O visualizador dimensional não funciona no Chrome 97. (CQ-4340456)
* O botão Download de ativo não mostra o menu completo na página Detalhes do ativo. (CQ-4336703)
* Ao usar o Compartilhamento de links, algumas das cadeias de caracteres na janela de compartilhamento de links não são localizadas. (CQ-4330540)
* Ao adicionar itens em Gerenciar publicação, a sequência de caracteres que reflete a contagem de itens selecionados não é localizada. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* Visualização segura baseada em token para ativos Dynamic Media nos Autores do AEM. (ATIVO-4995)
* Ao criar uma predefinição de imagem para o Dynamic Media em [!DNL Experience Manager], o máximo permitido é limitado a 2000x2000 pixels na interface do usuário. Quando o valor é aumentado para 2001 pixels para largura ou altura, a variável **[!UICONTROL Salvar]** for desativado. (ATIVO-5691)
* O usuário pode impedir que determinados formatos de arquivo sejam carregados no Dynamic Media. (ATIVO-5693)
* Acessibilidade - usuários com deficiência visual que dependem de leitores de tela serão afetados se o atributo Alt não for implementado em uma imagem na interface do usuário de predefinições de imagem . (ATIVO-9817)
* Acessibilidade - Os leitores de tela são afetados, pois os leitores de tela narram imagens não rotuladas para as imagens presentes no &quot;Segmento de linha do tempo&quot; e na guia &quot;Ações&quot;, quando navegados para o no modo de seta para baixo. (ATIVO-5651)
* Acessibilidade - Os leitores de tela estão sendo afetados, pois os leitores de tela (NVDA/JAWS) não narram o nome descritivo (enviar email) do botão &quot;Enviar email&quot; na caixa de diálogo &quot;EmailLink&quot; no player de vídeo, enquanto navegam usando os modos (Procurar/Cursor). (ATIVO-5641)
* Acessibilidade - O foco do teclado não está se movendo para o botão &quot;Refazer&quot;, que aparece após chamar o botão &quot;Desfazer&quot; na página Editor do conjunto de imagens, enquanto navega usando a tecla TAB no teclado. (ATIVO-5582)
* Acessibilidade - Os usuários que dependem de leitores de tela estão sendo afetados, pois o atributo Alt não é fornecido para uma imagem do Conjunto de imagens que está presente no cabeçalho Propriedades . (ATIVO-5576)
* Acessibilidade - Os leitores de tela não estão narrando a função de cabeçalho para `Cannot save this set` texto na `Cannot save this set` alerta, ao navegar usando a tecla de atalho de cabeçalho `H`e tecla de Seta para baixo. (ATIVO-5569)
* Acessibilidade - Os usuários que dependem de leitores de tela são afetados a navegar pelos formulários. Eles encontram dificuldades para entender as informações sobre os controles do formulário se a NVDA não estiver narrando as informações do rótulo para os controles de rotação &quot;Largura e altura&quot;. Esses controles que estão presentes no cabeçalho Corte responsivo de imagem ao navegar no modo de formulário NVDA &#39;F&#39;. (ATIVO-5393)
* Depois de adicionar um componente do Dynamic Media em um site e depois de publicar a página, o ativo recém-adicionado do Dynamic Media não fica visível na página publicada, nem é visualizado na página Visualização. Esse problema ocorreu para os tipos de ativos de imagem e vídeo. (ATIVO-9467)

## Commerce {#commerce-6513}

* &quot;todos&quot; tem jcr:write em `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* A classificação local de Produtos de comércio não funciona mais. (CQ-4343750)
* Não é possível publicar um produto rapidamente na página de resultados da pesquisa depois de alterar as propriedades. (CQ-4343318)

## CRX {#crx-6513}

* Não é possível baixar um pacote se ele tiver o caractere especial `+` no nome do pacote. (NPR-38102)

## [!DNL Forms] {#forms-65130}

* Quando o serviço de preenchimento prévio é usado para preencher um formulário adaptável que contém um fragmento e um fragmento contém uma caixa de texto que suporta rich text, o formulário não é enviado e ocorre o seguinte erro:

   `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542)

* Os componentes do botão de opção, caixa de seleção e Upload de arquivo não são traduzidos corretamente do idioma alemão para o idioma inglês. (NPR-38527)
* A codificação de código de barras PDF417 produzida por [!DNL Experience Manager] Forms é inválido para um grupo de botões de opção. (NPR-38525)
* O seguinte erro ocorre ao enviar um formulário adaptável.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* A opção Excluir campos ocultos do Documento de registro não funciona. (NPR-38512)
* Depois de adicionar o componente Contêiner do Forms a uma página Sites, os usuários não conseguem navegar para uma página Sites diferente e a página Sites trava em algumas ocasiões. O problema aparece intermitentemente. (NPR-38506)
* Os usuários experimentam a sobreposição do texto no Adaptive Forms após aplicar [!DNL Experience Manager] 6.5 Service Pack 11. (NPR-38376, CQ-4342472)
* Os usuários encontram uma exceção ao mover painéis de formulário adaptáveis para um novo layout responsivo. (NPR-38369)
* O suporte ao ECMASCRIPT 6 (ES6) não está habilitado para a biblioteca do cliente ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* Ao usar um [!DNL Experience Manager] Fluxo de trabalho para enviar um email em hebraico, o email recebido no final do usuário contém pontos de interrogação (??) em vez do texto em hebraico (NPR-38296).
* Os usuários são desconectados aleatoriamente de [!DNL Experience Manager] Não é possível enviar instâncias de publicação e um formulário adaptável. O problema aparece em [!DNL Experience Manager] instâncias que usam o Dispatcher. (NPR-38285)
* Quando você usa a opção getFormDataString em uma regra do Adobe Launch para capturar os dados do Formulário adaptável, a opção não retorna dados do Adaptive Forms. (NPR-38283)
* [!DNL Experience Manager] 6.5 A API relacionada ao grupo java.acl.obsoleta do Forms e as seguintes mensagens de erro são exibidas no arquivo error.log:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* O Forms criado em alemão não é traduzido para inglês ou qualquer outro idioma. (NPR-38280)
* Quando você usa uma versão localizada de um formulário adaptável, o Documento de registro (DoR) correspondente não é localizado. (NPR-38235)
* Ao usar a etapa Enviar email para enviar um anexo junto com um email, o anexo não retém o nome especificado na etapa Fluxo de trabalho . (NPR-38216)
* Quando uma nova versão da carta é publicada, os usuários não conseguem abrir as cartas de rascunho para versões anteriores das cartas. (NPR-38215, CQ-4342515)
* Ao chamar um método de serviço de ponto final SOAP do serviço AEM Forms JEE em um clique de botão configurado como uma regra do Formulário adaptável, o serviço SOAP falha com a exceção abaixo:
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* Ao usar com.adobe.fd.pdfutility.services.PDFUUtilityService#conversionPDFtoXDP para converter um PDF para o formato XDP, um arquivo XDP inválido é retornado. (NPR-38140, CQ-4342099)
* Quando vários usuários usam o Gerenciamento de correspondência para gerar cartas diferentes, na visualização, uma carta errada é exibida para alguns usuários. (NPR-38134)
* O componente AEM Forms incorporado na página SITES usa o atributo de largura que tem valor em % e não é válido de acordo com a validação do HTML W3C. Os usuários encontram um erro de análise incorreto durante a validação do HTML. (NPR-38124)
* Os itens de botões de opção e caixas de seleção para a maioria dos temas OOTB em formulários adaptáveis não fazem parte da ordem de tabulação (NPR-38108)
* Quando um usuário adiciona tags HTML à seção de comentário ao executar um fluxo de trabalho, as tags HTML são renderizadas. (NPR-37591)
* Ao importar e publicar uma carta que inclui um novo arquivo XDP, as letras não são visualizadas na instância de publicação. No entanto, se as cartas forem importadas e publicadas uma segunda vez usando o mesmo arquivo CMP, elas serão visualizadas com sucesso. (CQ-4343599)
* Um formulário com o conjunto de propriedades Preparar processo de dados não é renderizado no HTML Workspace. (CQ-4343294)
* Para PDF forms estáticos criados com o Forms 6.5 Designer, a acessibilidade do PDF falha com erro `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Não é possível converter uma imagem no PDF usando o serviço PDFG com OCR, após aplicar o patch AEMForms-6.5.0-0038 (log4jv2.16). (CQ-4342450)
* O valor incorreto é exibido para o código de barras SSCC-18. Os servidores da Forms omitem o valor na parte direita do código de barras. (CQ-4342400)
* Não é possível importar um arquivo do Microsoft® Word para o Forms Designer. Erro do usuário encontrado `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)
* No Forms 6.5 Designer, ao abrir um formulário criado com o Forms 6.1 Designer e editar uma caixa de texto, o espaçamento entre parágrafos excede o espaço especificado. Todas as configurações anteriores ao espaço são removidas e a reformatação manual da caixa de texto é necessária. (CQ-4341899)
* O usuário não pode definir horário personalizado no Agendador de limpeza de trabalhos. (CQ-4339192)
* O usuário não pode atualizar nenhuma configuração na interface do usuário do gerenciamento de ponto de extremidade e encontrar um erro ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* Para tags inválidas, o tratamento correto da mensagem de erro não está funcionando como esperado. (NPR-38106 e CQ-4337173)

>[!NOTE]
>
>* O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.


<!-- **Adaptive Forms**

**Form Data Model**

**Interactive Communication**

**Document Services**

**Document Security**

**Foundation JEE**

**Workflow** -->

## Granite {#granite-6513}

* Omnisearch retorna o resultado para usuários sem direitos de leitura. (NPR-38373)
* Habilitar ES6 para `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## Integrações {#integrations-6513}

* Vazamento de sessões do resolvedor de recursos no serviço Test e Target de UserInfoServlet obsoleto. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak - Indexação e Consultas {#oak-6513}

* A versão Oak para 6.5.13.0 foi atualizada para 1.22.11. (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## Plataforma {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* Atualizar dependência de `org.apache.httpcomponents.httpclient` em [!DNL Experience Manager] 6.5. (NPR-37999)
* Carregamento de alto autor devido a sugestões de campo de caminho. (CQ-4341826)
* O usuário deve atualizar a página quando alterar o projeto da exibição de Cartão para a exibição de Calendário. (CQ-4340368)
* As tags são perdidas devido a restrições de permissões. (CQ-4339543)
* Vários problemas relatados com Pesquisa e Filtro na Seleção de caminho não funcionavam. (CQ-4339402)
* Pare de usar o DTM no 6.5 - alterne para o Launch for Omega Instrumentation e adicione suporte ao Gainsight. (CQ-4337809)
* Restringir a função de pesquisa de componente de campo de caminho com base na propriedade de filtro de campo de caminho que está definida. (CQ-4309556)
* [!DNL Experience Manager] Plataforma 6.5: Correções de nomenclatura local em chinês. (CQ-4308978)
* Alterne para Launch para Omega Instrumentation. (NPR-38377)
* [!DNL Experience Manager] Plataforma 6.5: Correções de nomenclatura da localidade chinesa. (CQ-4308978)

## Replicação {#replication-6513}

* Falha na publicação do nó do usuário do Autor para o Editor. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### Admin {#sites-admin-6513}

* Correção da regressão introduzida com o SP 12 que pode ter causado um problema ao mover páginas. (SITES-5298)

### Interface do usuário clássica {#sites-classicui-6513}

* RTE: A imagem atualizada não fica visível quando uma nova imagem é arrastada sobre uma imagem existente. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### Fragmentos de conteúdo {#sites-contentfragments-6513}

* Suporte à criação de modelos de fragmentos de conteúdo em subconfigurações. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* Melhore o desempenho ao usar a validação de &quot;Campo exclusivo&quot; no Modelo de fragmento de conteúdo. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* Melhore o tempo de resposta ao abrir o Editor do modelo de fragmento de conteúdo. Clientes com vários fragmentos no Assets podem ter visto erros ao abrir o. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* Correção da regressão introduzida ao atualizar de 6.5.11 para 6.5.12 que pode ter causado erros no Editor do modelo de fragmento de conteúdo. (SITES-5088 e SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* Melhore a localização da interface do usuário do Editor do modelo de fragmento de conteúdo . (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* Correção de um problema que fechava o Editor de fragmento de conteúdo pode causar um erro quando o servidor do autor é usado com o Dispatcher. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* Correção de um problema que não era possível salvar um modelo quando a validação era usada em um campo RTE. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* Problema de Fragmento de conteúdo com a propriedade booleana que não mostrava o Texto do campo no &quot;título&quot;, em vez de mostrar o &quot;Nome da propriedade&quot;. (NPR-38244)
* Erro ao executar a consulta persistente com a variável de consulta por meio do Postman. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* Componente do fragmento de conteúdo: Regressão na opção &quot;manipular cabeçalhos como parágrafos&quot; corrigida que era 6.5 SP7. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* Corrigir a regressão introduzida na versão 6.5.11 que pode ter causado erros de pesquisa de ativos. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* Usando **[!UICONTROL Editar]** dos resultados da pesquisa podem resultar em uma `Not Found` erro. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* Os modelos da interface do usuário do hub de contexto não são renderizados corretamente sem uma atualização de página permanente. (NPR-38212)

### Editor de email {#sites-emaileditor-6513}

* Ativar suporte para a próxima versão dos Componentes principais de e-mail [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 e NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### Fragmentos de experiência {#sites-experiencefragments-6513}

* Ao usar a ação Navegar até a página nas Referências de um fragmento de experiência, ela abre a página errada. (NPR-38062)
* As propriedades de layout provenientes do modelo XF não são observadas no lado de uma página. (NPR-38214)
* Melhor desempenho do cálculo de referência XF. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### Editor de página {#sites-pageeditor-6513}

* Melhore a ação de desfazer para componentes que não têm o recurso inlineEditing ou dropTarget em `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* A lista suspensa Sistema de estilos pode ter sido posicionada na parte superior da página em vez de no contexto do componente - para componentes que usam `cq:editConfig` &quot;depois da edição: REFRESH_PAGE&quot;. Esse problema agora foi resolvido. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* O componente de texto é desalinhado quando adicionado aos Contêineres de layout aninhados. (NPR-38193)
* Uma guia de estilo vazia era exibida quando não havia configuração do Sistema de estilos para um componente; a guia agora fica oculta quando nenhuma configuração está presente. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* A propriedade `useLegacyResponsiveBehaviour` O funciona somente quando autenticado. (NPR-37996)
* Atualizar a interface do usuário do jquery para a versão mais recente resultou na quebra do Editor. (SITES-5647)

### Segurança {#sites-security-6513}

* A interface de usuário do Gerenciamento de grupo de usuários às vezes não removia usuários, principalmente em grupos com +20 usuários. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Gerador de mapa do site e Tag canônica adicionam suporte a URLs sem .html. (CIF-2647)
* Adicione suporte para remover idiomas alternativos usando a configuração noindex. (CIF-2496)
* Adicione suporte para fornecer URL personalizado para substituir o URL canônico padrão de páginas com conteúdo quase idêntico. (CIF-2747)

### Editor de SPA e SDK {#sites-spa-sdk-6513}

* A partir da versão 6.5.13, não será mais necessário criar o nó do componente de contêiner no JCR antes de fazer edições por meio do Editor de SPA. A `virtual container` é criada antes de salvá-la por meio do SDK. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### Editor de modelos {#sites-templateeditor-6513}

* Corrigir a regressão de que publicar um modelo alterado não publicava todas as dependências. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* O templateResource valueMap deve permitir leituras profundas de acordo com a API do ValueMap. (NPR-38439)

## Sling {#sling-6513}

* Vazamento de memória `DiscoveryLiteDescriptor`. (NPR-38288)
* Atualizar `sling-javax.activation` pacote com correção do SLING-8777. (NPR-38077)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## Projetos de tradução {#translation-6513}

* Várias inicializações sendo criadas para páginas referenciadas/xf. (NPR-38263)
* Alteração do comportamento de adicionar páginas a projetos de tradução desde o Service Pack 10. O projeto de tradução não contém uma página recém-criada [ex: test-page-women-2] na lista, quando o pai selecionado da página recém-criada [não a página recém-criada diretamente]. (NPR-38256)
* Adicionar `cq:isTranslationLaunch` em Lançamentos criados pelo Projeto de tradução. (NPR-38224)
* O Launch está sendo criado para uma página que tem um XF referenciado que tem um ativo nele. (NPR-38199)
* [!DNL Experience Manager] a atualização da memória de tradução não funciona. (NPR-38196)
* Habilitar ES6 para `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* Pacote 18n mais recente para traduções de [!DNL Experience Manager] 6.5. (CQ-4339505)

## Interface do usuário {#ui-6513}

* Quando estiver na página inicial > Ferramentas e clique no botão [!DNL Experience Manager] ícone , o [!DNL Experience Manager] A tela de navegação deve aparecer. (NPR-38417)
* Habilitar ES6 para `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* Habilitar ES6 para `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* O seletor de datas na interface do usuário de toque é exibido em coreano. (NPR-38079)
* Caixa de diálogo de criação com vários campos, após reordenar os campos que perdem o valor de seleção do botão de opção. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5: Correções de nomenclatura local em chinês. (CQ-4308973)
* ResourceResolver não fechado em com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification (NPR-38286)

## Instalar [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.13.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o [!DNL Experience Manager] Pacote 6.5.13.0.

### Instalar o service pack em [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL Experience Manager] 6.5.13.0

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 não suporta a instalação do Bootstrap.

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience Manager (6.5.13.0)` under [!UICONTROL Produtos instalados].

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.3 ou posterior (Use o Console da Web: `/system/console/bundles`).


### Instalar [!DNL Experience Manager] Pacote do complemento Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorar se não estiver usando [!DNL Experience Manager] Forms. Correções na [!DNL Experience Manager] O Forms é fornecido por meio de um pacote complementar separado uma semana após a [!DNL Experience Manager] Versão do Service Pack.

1. Verifique se você instalou o [!DNL Experience Manager] Service Pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalar [!DNL Experience Manager] Forms no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções na [!DNL Experience Manager] O Forms no JEE é fornecido por meio de um instalador separado.

Para obter informações sobre a instalação do instalador cumulativo para [!DNL Experience Manager] Forms no JEE e configuração pós-implantação, consulte o [notas de versão](jee-patch-installer-65.md).

>[!NOTE]
>
>Depois de instalar o instalador cumulativo para [!DNL Experience Manager] Forms no JEE, instale o pacote complementar mais recente do Forms, exclua o pacote do complemento Forms do `crx-repository\install` e reinicie o servidor.

### UberJar {#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.13.0 está disponível no [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://).

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a variável `dependency` .

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] a integração do é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O]. Ele suporta o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [AEM Fragmento de conteúdo com o Pacote de índice GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* As [!DNL Microsoft® Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] não suporta instalações turnkey para [!DNL AEM Forms 6.5.10.0].

* Se estiver atualizando seu [!DNL Experience Manager] da versão 6.5 para 6.5.10.0, você pode visualizar `RRD4JReporter` exceções na `error.log` arquivo. Para resolver o problema, reinicie a instância.

* Se você instalar [!DNL Experience Manager] 6.5 Service Pack 10 ou service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado dos ativos (criado em `/var/workflow/models/dam`) é excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada em [!DNL Experience Manager] usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de reg não registrada.

* Ao tentar mover/excluir/publicar Fragmentos de conteúdo ou Sites/Páginas, há um problema quando as referências do Fragmento de conteúdo são buscadas, uma vez que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (não é necessário reindexar):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.13.0:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.13.0](/help/release-notes/assets/65130_bundles.txt)

* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.13.0](/help/release-notes/assets/65130_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao Cliente Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

