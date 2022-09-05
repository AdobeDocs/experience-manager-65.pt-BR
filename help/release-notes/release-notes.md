---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista detalhada de alterações para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 381ab110ccf5605b17382b9c77693c819e31e3b6
workflow-type: tm+mt
source-wordcount: '3224'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Notas de versão mais recentes do Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | 25 de agosto de 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] O 6.5.14.0 inclui novos recursos, principais melhorias solicitadas pelo cliente, correções de bugs e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este service pack](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* Não é possível adicionar ou exibir tags para arquivos PDF. (NPR-38452)
* Quando você configura o Connected Assets, salva a configuração, reabre a página de configuração e testa a configuração já salva, a conexão de teste falha. (NPR-38507)
* Não é possível adicionar usuários com ID numérica de usuário às coleções. (NPR-38538)
* Experience Manager falha ao processar o FFmpeg instalado na instância do autor. (NPR-38568)
* O processamento de PDF falha com um `NoClassDefFoundError` mensagem de erro. (NPR-38741)
* O botão Adicionar em Colunas personalizadas não é exibido corretamente ao criar um relatório de ativos para `de_DE` localidade. (ATIVO-10641)
* Quando você carrega um ativo duplicado no repositório do Gerenciamento de ativos digitais e detecta e fornece uma opção para excluir o ativo duplicado, o ativo original também é excluído do repositório. (ATIVO-10826)
* O Experience Manager não salva os metadados da pasta corretamente ao especificar caracteres especiais em vários campos. (ATIVO-10721)
* Não é possível salvar as propriedades do ativo até você clicar em **[!UICONTROL Salvar e fechar]** duas vezes. (ATIVO-12040)
* O leitor de tela só anuncia o `Relate` botão. No entanto, a variável `Relate` também contém um submenu e pode ser expandido e recolhido. (ATIVO-6938)
* Atributos ARIA (Accessible Rich Internet Applications) obrigatórios `aria-expanded` para `role="combo box"` está ausente. (ATIVO-6928)
* Na exibição de Cartão, na área de navegação do arquivo principal, o conteúdo do texto **[!UICONTROL Classificar por]** não tem pelo menos uma relação de contraste de 4,5:1 em relação à cor de plano de fundo. (ATIVO-6926)
* Experience Manager não identifica **[!UICONTROL Selecione um modelo de Fluxo de trabalho]** lista suspensa como um campo obrigatório ao criar um modelo de fluxo de trabalho. (ATIVO-6871)

>[!NOTE]
>
>Os Serviços de conteúdo inteligente não estarão disponíveis para novos clientes no local da Experience Manager Assets a partir de 1º de setembro de 2022. Nenhum impacto nos clientes no local e do Adobe Managed Services que já têm esse recurso ativado.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Adicione suporte para redefinição de senha para o usuário do Dynamic Media Classic no Experience Manager. (ATIVO-10298)
* Os Recortes inteligentes gerados para as imagens com fundo transparente têm fundo branco. (ATIVO-13148)
* O Dynamic Media não gera miniaturas para arquivos EPS. (ATIVO-10959)
* Os ativos não são carregados na conta do Dynamic Media devido à falta de parâmetro de upload. (ATIVO-13165)
* Permitir que ativos com nomes maiores que 127 caracteres sejam carregados no Dynamic Media. (ATIVO-9991)
* Ativação do JavaScript ES6 (ECMAScript 6) para visualizadores Dynamic Media no Experience Manager 6.5.14.0. (NPR-38393)
* Configuração das opções no Dynamic Media **[!UICONTROL Configurações gerais]** e **[!UICONTROL Configuração de publicação]** não deve ser acessível a usuários que não sejam administradores. (ASSETS-8628)
* Dynamic Media **[!UICONTROL Configurações gerais]** não mostra os parâmetros de upload já configurados corretamente. (ATIVO-10245)
* A interface do usuário do Experience Manager não mostra nenhuma mensagem de falha em caso de falha de criação/atualização do conjunto de relatórios. (ATIVO-10264)
* Não é possível aplicar uma política salva a um dos contêineres de um modelo editável para permitir que você adicione componentes do Dynamic Media. (ATIVO-11044)
* Os ativos não são carregados na conta do Dynamic Media após a execução do fluxo de trabalho Ativos de reprocessamento do Dynamic Media em ativos com identificador de trabalho incorreto. (ASSETS-12084, ASSETS-9877)
* Os usuários de leitores de tela são afetados pela variável `title` não sendo fornecido `<frame>` e `<iframe>` no **[!UICONTROL Digite para pesquisar]** caixa de diálogo. (ATIVO-5483)
* Em leitores de tela, relacionados e significativos `alt=` deve ser fornecido para várias imagens que estão presentes em **[!UICONTROL Ativos]** no painel esquerdo. (ATIVO-5644)
* O leitor de tela não lê **[!UICONTROL Mudo]** e **[!UICONTROL Sem som]** botão no vídeo usando o componente Dynamic Media. (ATIVO-10169)

## Commerce {#commerce-6514}

* Os produtos de comércio não estão sendo classificados usando o cabeçalho da coluna e está usando _remoto_ modo de classificação; em vez disso, os produtos do Commerce devem ser classificados usando cabeçalhos de coluna com _local_ modo de classificação. (CQ-4343750, NPR-38498)



## [!DNL Forms] {#forms-6514}

<!--

>[!NOTE]
>
> Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

>[!NOTE]
>
>* [!DNL Experience Manager Forms] releases the add-on packages one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages will release Thursday, September 1, 2022. In addition, a list of Forms fixes and enhancements will also be added to this section.

-->

* Quando um arquivo é anexado a um formulário adaptável de vários painéis e um rascunho do formulário adaptável é salvo, ocorre um erro. (NPR-38978)
* Quando um usuário converte o perfil do RGB em perfil CMYK usando a API Java createPDF2 com as configurações AdobePDF, a opção não funciona com a API Java. A opção funciona bem com o aplicativo DistillerClient independente. (NPR-38858, CQ-4346181)
* Depois de instalar o AEM 6.5 Forms service pack 12 (6.5.12.0), todas as opções, exceto fechar a tarefa, se tornarão indisponíveis na etapa Atribuir tarefa dos fluxos de trabalho AEM. (NPR-38743)
* Em um Documento de registro (DoR), alguns valores em uma tabela são truncados. (NPR-38657)
* Ao visualizar o FormSet com Data XML, quando o XDP contém um campo flutuante, ao visualizar um FormSet, nenhum dado é exibido, mas os dados são exibidos quando a opção Visualizar PDF é usada.
* No Adaptive Forms, o botão de opção e a caixa de seleção não estão na ordem das guias. (NPR-38645)
* Quando você usar a variável `Summary Step` para gerar Documento de registro (DoR) para um Formulário adaptável traduzido após o formulário de envio, não é traduzido para o idioma localizado. (NPR-38567)
* A opção desativar nova tentativa em AEM etapas do fluxo de trabalho não está funcionando como esperado. O problema aparece intermitentemente. (NPR-38547)
* Quando o formulário adaptável é enviado com o campo Rich Text, a variável `an Internal Error while Submitting a Form` ocorre. Quando o usuário focaliza no campo rich text, antes do envio do formulário, o erro não ocorre. (NPR-38542)
* Um erro `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` está registrado. (NPR-38541)
* Quando um usuário carrega um PDF para um Formulário adaptável, o servidor do AEM Forms fica sem resposta. (NPR-38398)
* Em um AEM Forms em um servidor OSGi, ao usar a API do Serviço de documento para certificar o PDF, ele falha com o erro: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311. (CQ-4346252)
* Ao enviar o rascunho de cartas, a `Could not upload asset from xml input` ocorre. Ele não afeta a funcionalidade. Ao abrir um rascunho, a letra é renderizada corretamente. (CQ-4345979, CQ-4344418)
* Quando uma data é inserida no formato alemão e a variável `Preview with Data` for usada para uma carta, o campo Date não será renderizado. (CQ-4345783)
* Quando você cria um portal da Web e gera os códigos de barras com base em dados, alguns códigos de barras não são decodificados corretamente. (CQ-4345743)
* A conversão de postscript para o PDF não renderiza o documento de saída com as cores esperadas. (CQ-4345074)
* O resolvedor de recursos faz com que falhas intermitentes de envio e resulta no mesmo rastreamento de pilha apareçam várias vezes para um único envio. (CQ-4344764)
* Os usuários não podem abrir as letras de rascunho modificadas que usam o `cmDataUrl` parâmetro. Os rascunhos são abertos pela primeira vez. Os problemas começam a aparecer em tentativas subsequentes. (CQ-4344418)
* Quando o usuário entra no `&` símbolo numa comunicação interativa (IC), o rascunho do IC correspondente não é carregado. (CQ-4343969)
* Quando você usa opções de estilo no AEM Forms Designer para gerar arquivos PCL, o estilo especificado não é aplicado aos arquivos gerados. (CQ-4339573)
* Quando a contagem de páginas é superior a 15, a conversão automática de formulários XDP dinâmicos para o Formulário adaptável falha. Isso funciona bem quando a contagem de página é inferior a 15. (NPR-35337)
* Quando a opção Adicionar aos favoritos é usada, ela não indica o status da alternância para o leitor de tela. (NPR-37137)
* No Modelo de Dados de Formulário, os valores após decimais no Modelo de Dados de Formulário com banco de dados são truncados para dados monetários e de moeda pequena. . (CQDOC-19509)
* Ao selecionar um link de navegação para fluxo de trabalho no HTML Workspace, ele não é indicado para a seleção do link de navegação. (NPR-37138)
* O recurso Assinatura de rabisco não é compatível com as diretrizes de acessibilidade. (NPR-37596)
* O AEM Forms usa o log4j 1.x. O suporte para log4j 1.x chegou ao fim da vida útil. (NPR-38273)
* Ao usar o banco de dados MSSQL como fonte de dados em um Modelo de dados de formulário e recuperar valores, os números após o decimal nos valores de recuperação são ativados. (CQ-4346190)
* No Forms 6.5 Designer, ao abrir um formulário criado com o Forms 6.1 Designer e editar uma caixa de texto, o espaçamento entre parágrafos excede o espaço especificado. Todas as configurações anteriores ao espaço são removidas e a reformatação manual da caixa de texto é necessária. (CQ-4341899)
* O valor incorreto é exibido para o código de barras SSCC-18. Os servidores da Forms omitem o valor na parte direita do código de barras. (CQ-4342400)
* Para PDF forms estáticos criados com o Forms 6.5 Designer, a acessibilidade do PDF falha com erro `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Adição da capacidade de especificar o texto de Reader de tela para hiperlinks no Forms Designer.(NPR-36221)

## Integrações {#integrations-6514}

* Ativar o suporte de compilação do JavaScript ES6 (modo ECMAScript6 ou melhor) para minificação da variável `/libs/cq/analytics/widgets.js` biblioteca. (NPR-38433)
* Ativar o suporte de compilação do JavaScript ES6 (modo ESMAScript6 ou melhor) para minificação da variável `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` biblioteca. (NPR-38435)
* Quanto mais conteúdo há em `/content/campaigns`, quanto mais longa a chamada para `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) é necessária quando você abre o Editor de páginas. (NPR-38663)

## Plataforma {#platform-6514}

* Não é possível fazer logon no Gerenciador de Pacotes para implantar atualizações. (NPR-38646)
* Na interface do usuário do seletor de tags de ativos, as tags são exibidas na ordem em que foram criadas. No entanto, quando há muitas tags, visualizar e gerenciar as tags é difícil porque elas não podem ser classificadas. (CQ-4344279)
* Crie uma notificação na interface do usuário quando um usuário estiver sendo representado por um administrador ou por qualquer outra pessoa usando o **[!UICONTROL Representar como]** campo. (CQ-4345288)
* Em uma coleção inteligente, todos os ativos eram exibidos ao filtrar usando uma pesquisa salva. (CQ-4345326)
* Uma contagem de ativos selecionada incorreta é mostrada para **[!UICONTROL Adicionar à coleção]** when **[!UICONTROL Selecionar tudo]** está selecionada. (CQ-4345424)
* Ocorreu uma mensagem de exceção ao usar a variável **[!UICONTROL Representar como]** com um grupo ou usuário inexistente. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Ocorreram exclusões inesperadas de caminho ao atualizar o Experience Manager de 6.5.12.0 para 6.5.13.0. (NPR-38532)

### Acessibilidade {#access-6514}

* No Experience Manager Sites, ao expandir o **[!UICONTROL Alterar o formato de exibição e ajustar a configuração de exibição]** e selecione **[!UICONTROL Exibição de lista]**, o **[!UICONTROL Arrastar e soltar]** um nome acessível está ausente. (SITES-2863, NPR-38760)
* O leitor de tela deve anunciar o nome acessível, como `Show description for Archive` ou `Show description for mini shopping cart`. No entanto, o nome acessível atual é anunciado como `Info Circle button show description` para _all_ os botões de informação da dica de ferramenta. (SITES-3104)
* Melhore a ação de desfazer para componentes que não têm o recurso inlineEditing ou dropTarget em `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* A lista suspensa Sistema de estilos pode ter sido posicionada na parte superior da página em vez de no contexto do componente - para componentes que usam `cq:editConfig` &quot;depois da edição: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* O componente de texto é desalinhado quando adicionado aos Contêineres de layout aninhados. (NPR-38193)
* Uma guia de estilo vazia era exibida quando não havia configuração do Sistema de estilos para um componente. A guia agora fica oculta quando nenhuma configuração está presente. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* A propriedade `useLegacyResponsiveBehaviour` O funciona somente quando autenticado. (NPR-37996)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* Problema de validação do campo de enumeração Fragmentos de conteúdo na primeira vez que o fragmento de conteúdo é carregado. (SITES-7140)
* É necessário adicionar campos de personalização do Campaign no Editor de Rich Text do Editor de Fragmentos de conteúdo. (NPR-38526)
* Ao criar ou editar um novo fragmento de conteúdo no editor de Fragmento de conteúdo, por meio do Dispatcher, o modelo de fragmento de conteúdo não é salvo. Além disso, o editor de Fragmento de conteúdo não é fechado e um erro é exibido no log do navegador. (NPR-38691)
* Erro de validação de consulta persistente. (NPR-38523)
* Na caixa de diálogo Fragmento de conteúdo , em **[!UICONTROL Propriedades]**, o **[!UICONTROL Fragmento de conteúdo]** não mantém o caminho salvo no pop-up de seleção. (NPR-38632)
* Ao criar um modelo de fragmento de conteúdo e adicionar um campo de enumeração do tipo suspenso, a validação correta para _`is required`_falha. (NPR-38237)

### Componentes principais  {#sites-corecomponents-6514}

* O novo componente de Email de página não deve forçar você a entrar na interface de usuário clássica ao editar `/etc`. (NPR-38648)

### Editor de página {#sites-pageeditor-6514}

* O usuário não pode redimensionar o componente para o número desejado de colunas. (NPR-38688)

### Editor de modelos {#sites-templateeditor-6514}

* Ausente **[!UICONTROL Excluir]** e **[!UICONTROL Recortar]** botões na barra de Menu em um modelo editável depois de um `cq:actions` foi personalizada. (NPR-38521)
* Se um componente incluir outro componente, não é possível excluir o componente dentro da estrutura do modelo porque a variável **[!UICONTROL Excluir]** está ausente na barra de menus. (NPR-38585)

## Sling {#sling-6514}

* Um aumento no número de arquivos abertos na produção ocorreu devido a um vazamento de memória no módulo `DiscoveryLiteDescriptor` em `org.apache.sling.discovery.commons`, versão 1.0.20. (NPR-38288)
* Em Experience Manager, de **[!UICONTROL Operações]** > **[!UICONTROL Diagnóstico]**, ocorre um erro ao selecionar **[!UICONTROL ZIP de status de download]** > **[!UICONTROL Baixar]**. (NPR-38514)

## Projetos de tradução {#translation-6514}

* O Launch para subpáginas que foram adicionadas como referência em uma página principal não estava sendo promovido quando o `isDeep` propriedade foi definida como `false`. (NPR-38531)

## Interface do usuário {#ui-6514}

* Ao usar **[!UICONTROL Selecionar tudo]** > **[!UICONTROL Publicação rápida]**, o Experience Manager não publicava todos os ativos ou mostrava quantos ativos seriam publicados em **[!UICONTROL Cartão]** exibir ou **[!UICONTROL Lista]** exibir. (NPR-38546)
* A contagem incorreta de ativos selecionados é mostrada para **[!UICONTROL Adicionar à coleção]** em **[!UICONTROL Selecionar tudo]** caso. (NPR-38633)
* Usuários desativados ainda podem ser adicionados a Coleções e Projetos. (NPR-38651)
* Excluir um filtro sem salvar o Formulário de pesquisa cria um erro. (NPR-38698)
* A sessão de um usuário não pode obter um `ModifiableValueMap` para os grupos a fim de estabelecer a associação direta aos grupos. (NPR-38710)

## Fluxo de trabalho {#workflow-6514}

* Ativar o suporte de compilação do JavaScript ES6 (modo ESMAScript6 ou melhor) para minificação da variável `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` biblioteca. (NPR-38304)
* Depois que o workflow é executado e as etapas do processo são concluídas, o mesmo comentário é repetido várias vezes. (NPR-38364)

## Instalar [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.14.0 em uma das instâncias do autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o [!DNL Experience Manager] Pacote 6.5.14.0. <!-- UPDATE FOR EACH NEW RELEASE -->

### Instalar o service pack em [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL Experience Manager] 6.5.14.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.14.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience Manager (6.5.14.0)` under [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é a versão 1.22.12 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- NPR-38747 -->

### Instalar [!DNL Experience Manager] Pacote do complemento Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorar se não estiver usando [!DNL Experience Manager] Forms.

<!-- 

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

-->

1. Verifique se você instalou o [!DNL Experience Manager] Service Pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Se você usar letras no Experience Manager 6.5 Forms, instale o [Pacote de compatibilidade AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Instalar [!DNL Experience Manager] Forms no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções na [!DNL Experience Manager] O Forms no JEE é fornecido por meio de um instalador separado.

Para obter informações sobre a instalação do instalador cumulativo para [!DNL Experience Manager] Forms no JEE e configuração pós-implantação, consulte o [notas de versão](jee-patch-installer-65.md).

>[!NOTE]
>
>Depois de instalar o instalador cumulativo para [!DNL Experience Manager] Forms no JEE, instale o pacote complementar mais recente do Forms, exclua o pacote do complemento Forms do `crx-repository\install` e reinicie o servidor.

### UberJar {#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.13.0 está disponível no [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>No Experience Manager 6.5.14.0, esteja ciente de que a versão UberJar (6.5.13.0) permanece a mesma que a versão anterior.

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] a integração do é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Ele suporta o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O Runtime] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

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
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de registro não registrada.

* Ao tentar mover/excluir/publicar Fragmentos de conteúdo ou Sites/Páginas, há um problema quando as referências do Fragmento de conteúdo são buscadas, uma vez que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (não é necessária reindexação):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.14.0](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.14.0](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao Cliente Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

