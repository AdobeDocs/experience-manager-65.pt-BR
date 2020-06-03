---
title: Novidades do Adobe Experience Manager 6.5 Service Pack 5
description: Novidades do Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 4%

---


# Novidades do AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Os service packs do Adobe Experience Manager 6.5 fornecem novos recursos, melhorias de desempenho, estabilidade relacionadas a solicitações do cliente em intervalos trimestrais. O modelo de delivery trimestral facilita o acesso e a adoção de novos recursos e inovações.

Este artigo destaca os recursos incluídos no Service Pack 6.5 mais recente, os recursos [principais incluídos nos Service Packs](#key-features-previous-service-packs)6.5 anteriores e algumas das versões [principais desde a versão 6.5.4.0](#key-features-sice-sp3) do Experience Manager.

## AEM Sites {#aem-sites}

### Aprimoramentos de acessibilidade {#accessibility-sites}

* relatórios de erro aprimorado ao adicionar informações de texto

* Foco aprimorado na interface do usuário durante a navegação do teclado

* Contraste do texto aprimorado (proporção de luminosidade)

* Consistência aprimorada de atributos alternativo para imagens de página

* Consistência aprimorada de rótulos de aplicativos acessíveis de Internet avançada (ARIA - Accessible Rich Internet Applications)

* Capacidades NVDA (Non-Visual Desktop Access) aprimoradas

* Suporte aprimorado ao leitor de tela

### Outras melhorias importantes {#other-enhancements-sites}

* Ao copiar ou colar uma árvore de página, agora você tem a opção de colar a página raiz ou colar a página raiz com as subpáginas da árvore.

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* Gerenciador de vários sites - o acionador Publicar agora exclui com êxito um componente da página publicada se um componente for excluído da página de origem.

* Gerenciador de vários sites - quando o nome de um componente local em um LiveCopy é idêntico ao nome de um componente no blueprint e o componente é lançado do blueprint, o termo _msm_move agora é adicionado com êxito ao nome do componente local.

## Ativos AEM {#aem-assets}

### Aprimoramentos de acessibilidade em ativos {#assets-accessibility}

[!DNL Adobe Experience Manager] As funcionalidades de ativos agora estão mais acessíveis em conformidade com as Diretrizes de acessibilidade de conteúdo da Web (WCAG). A acessibilidade melhorou nas seguintes áreas:

* Os elementos, controles, páginas e caixas de diálogo da interface do usuário são compatíveis com o leitor de tela.

* Elementos da interface do usuário, controles e campos de formulário de entrada podem ser acessados usando o teclado.

* Alteração na cor e no contraste de alguns gráficos para serem distinguidos por usuários com visão limitada e sem percepção de cor. Por exemplo, a cor dos ícones de classificação de estrelas (como na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] em [!UICONTROL Propriedades] do ativo ou na visualização do cartão) é alterada para contraste adequado.

![cor dos ícones de classificação de estrelas alterada para melhorar o contraste](assets/star-rating-icons.png)

### Manuseio de Exceção aprimorado {#exception-handling}

O fluxo da interface do usuário do Assets tem melhor tratamento de exceções. Anteriormente, se um ativo não tivesse o tipo adequado para sua dimensão, era observada uma exceção que era capturada silenciosamente sem rastreamento nos registros. Esse comportamento mudou e todas as exceções são capturadas nos registros.

## [!DNL Dynamic Media] {#dynamic-media}

### Suporte 3D em [!DNL Dynamic Media] {#support-for-3d}

O suporte 3D em [!DNL Dynamic Media] agora permite que os clientes publiquem e adicionem conteúdo 3D a páginas da Web e aplicativos. Inclui:

* Publicação de formatos comuns de ativos 3D para gerar um URL de ativo.

* Visualização interativa de ativos 3D publicados usando um novo Visualizador da Web 3D disponível na biblioteca do [!DNL Dynamic Media] visualizador, com o Adobe Dimension.

* Publicação e visualização em 3D na [!DNL Experience Manager Sites] página usando o componente [!DNL Sites] WCM.

## Formulários AEM {#aem-forms}

### Personalizar as colunas da Caixa de entrada do AEM {#customize-aem-inbox-columns}

Você pode personalizar uma Caixa de entrada do AEM para alterar o título padrão de uma coluna, reordenar a posição de uma coluna e exibir colunas adicionais com base nos dados de um fluxo de trabalho. Você deve ser um membro `administrators` ou um `workflow-administrators` grupo para personalizar as colunas.

![Personalizar colunas da Caixa de entrada do AEM](assets/customize-columns.gif)

### Salvar comunicações interativas como rascunho {#save-as-draft}

Você pode usar a interface do agente para salvar um ou mais rascunhos para cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nele. Você pode especificar um nome diferente para cada rascunho para facilitar a identificação.

![Salvar como rascunho](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] suporte ao servidor de aplicativos {#weblogic-support}

O AEM Forms adicionou suporte para [!DNL Oracle WebLogic 12] o AEM Forms no JEE. Você pode atualizar de uma versão anterior ou configurar um novo AEM 6.5 Forms no servidor JEE em [!DNL Oracle WebLogic] 12.2.1.4 e posterior. Mais tarde corresponde às alterações de versão secundária, em que x em 12.2.1.x é substituído por um número de versão.

### Aprimoramentos de acessibilidade {#accessibility-improvements}

O AEM Forms inclui os seguintes aprimoramentos de acessibilidade:

* Quando um usuário pré-visualização um formulário adaptável como um formulário HTML, o campo Assinatura [!UICONTROL em] script retém o foco da guia.

* As mensagens de erro exibidas ao enviar um formulário adaptável agora contêm o `aria-describedBy` atributo. O atributo é anexado aos campos mencionados na mensagem de erro. O `aria-describedby` atributo indica IDs dos elementos que descrevem o objeto. Ajuda a estabelecer uma relação entre widgets ou grupos e texto que os descreveu.

* Se um formulário adaptável tiver alguns campos obrigatórios, o atributo obrigatório será definido como `True` para esses campos no schema de acessibilidade ARIA.

### Autenticação baseada em certificado X-509 para serviços Web baseados em SOAP no modelo de dados de formulário {#x509-based-authentication-soap}

O modelo de dados de formulário agora oferece suporte à autenticação baseada em certificado X-509 ao usar serviços Web SOAP como fonte de dados.

### Outras melhorias importantes {#other-improvements}

* O AEM 6.5 Forms no JEE Documento Security agora é baseado em [!DNL Apache Struts 2].

* Adicionado suporte para [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Principais recursos dos Service Packs anteriores do AEM 6.5 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### Aprimoramentos do sistema de estilo (6.5.4.0) {#style-system-enhancements}

Agora é possível selecionar estilos na caixa de diálogo do componente usando o Sistema de estilo aprimorado.

#### Melhorias no desempenho em várias áreas (6.5.4.0) {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (`contexthub.kernel.js`). Isso resulta em cargas de página mais rápidas durante uma visita ao site.

* Redução do tempo para atualizar uma página depois de arrastar Fragmentos de experiência para o Editor de páginas de sites.

* Tempo de carregamento reduzido para entradas em uma página Sites com mais de 200 cópias online na Visão geral **** da Live Copy.

* Funcionamento aprimorado de URLs incompletos ou inválidos. Tais URLs podem retardar o Editor de modelos.

### Ativos AEM {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

O canal de autorização entre os ativos AEM e o Portal de marcas foi alterado. Anteriormente, o Brand Portal estava configurado na interface clássica via Gateway OAuth herdado, que usa a troca de token JWT para obter um Token de acesso IMS para autorização. Os ativos AEM agora estão configurados com o Portal de marcas por meio da E/S da Adobe, que obtém um token IMS para autorização do locatário do Portal de marcas.

As etapas para configurar os ativos AEM com o Brand Portal são diferentes dependendo da versão do AEM e se você está configurando pela primeira vez ou atualizando as configurações existentes. Consulte [Configurar ativos AEM com o Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) da marca para obter detalhes.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Os ativos do Experience Manager incluem os seguintes aprimoramentos de acessibilidade:

* Teclas de seta no teclado podem ser usadas para mover e deslocar áreas em imagens ampliadas. Para obter mais informações, consulte [pré-visualizações usando apenas](../assets/managing-assets-touch-ui.md#previewing-assets)teclas de teclado.

* As caixas de seleção de estado misto (nas quais, a menos que você marque todos os predicados aninhados, as caixas de seleção de primeiro nível não serão selecionadas e passarão por elas) no painel Filtros poderão ser lidas pelos leitores de tela.

* As restrições de formato de data e hora são fornecidas nos rótulos de campo dos campos de data, para permitir que os usuários digitem a data no formato correto usando o teclado.

   Por exemplo, `On Time (MM-DD-YYYY HH:mm)`. Aqui MM é mês em formato de dois dígitos, AAAA é ano, DD é dia em formato de dois dígitos, HH é hora em formato militar de 24 horas e mm é minuto.

* O `X` símbolo no botão para remover as tags atualmente selecionadas agora é anunciado pelos leitores de tela, juntamente com o número de tags selecionadas.

#### Pesquisa visual para AEM Assets (6.5.2.0) {#visual-search}

Os usuários do Assets podem pesquisar imagens visualmente semelhantes. O AEM exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Imagem inteligente para o Dynamic Media {#smart-imaging}

A geração de imagens inteligentes usa as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte Imagem [inteligente](../assets/imaging-faq.md).

#### Recorte inteligente em perfis de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

Recorte inteligente para vídeo e recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial no Adobe Sensei para detectar e recortar automaticamente o ponto focal em qualquer vídeo adaptável ou progressivo que você tenha carregado, independentemente do tamanho. Consulte [Sobre como usar o recorte inteligente em perfis](../assets/video-profiles.md)de vídeo.

### Formulários AEM {#aem-forms-previous-service-packs}

#### Gerar saída imprimível em workflows do AEM Forms (6.5.4.0) {#generate-printable-output}

A etapa de fluxo de trabalho Gerar saída imprimível permite integrar um arquivo de modelo de origem a um arquivo de dados. Essa integração permite que você imprima ou salve cópias diferentes do arquivo de modelo. A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL. Para obter mais informações sobre esse recurso, consulte Fluxo de trabalho centrado no [Forms em OSGi - Referência](../forms/using/aem-forms-workflow-step-reference.md)de etapas.

![Gerar saída para impressão](assets/generate-print-output-step.gif)

#### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout (6.5.4.0) {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas. Alterne para o modo de layout para usar a nova opção de várias colunas. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

![Layout de várias colunas](assets/multi-column-layout.gif)

#### Personalizações da Caixa de entrada do AEM (6.5.4.0) {#aem-inbox}

A nova opção Controle de administrador permite que os administradores:

* Personalizar o texto e o logotipo do cabeçalho

* Controlar a exibição de links de navegação disponíveis no cabeçalho

A opção Controle de administrador está visível somente para os membros do grupo de administradores ou administradores de fluxo de trabalho. Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

#### Suporte a Rich Text em formulários HTML5 (6.5.4.0) {#rich-text-support}

Converta um campo de texto em um formulário XFA em um campo de texto formatado em um formulário HTML5. Para obter mais informações, consulte [Criar modelos de formulário para formulários](../forms/using/designing-form-template.md)HTML5.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

O Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Os leitores de tela anunciam as caixas de seleção, os links, o Seletor de data e os campos de Entrada de data corretamente em um formulário adaptável.

* Cada página de um formulário adaptável agora inclui um título e um rótulo principal.

#### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário do AEM Forms (6.5.3.0) {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Quando outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá solicitar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso a itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

#### Defina as configurações de disponibilidade para itens da Caixa de entrada de um usuário do AEM Forms (6.5.3.0) {#configure-out-of-office}

Se planeja estar fora do escritório, você pode especificar o que acontece com os itens que lhe são atribuídos para esse período.
Você tem a opção de especificar uma data e hora de start e uma data e hora de término para que suas configurações de fora do escritório entrem em vigor. Você pode definir uma pessoa padrão para a qual todos os itens serão enviados. Consulte [Configurar configurações](../forms/using/configure-out-of-office-settings.md)fora do escritório.

#### Gerar várias comunicações interativas usando a API de lote para AEM Forms (6.5.3.0) {#generate-multiple-ic}

Você pode usar a API de lote para produzir várias comunicações interativas a partir de um modelo. O modelo é uma comunicação interativa sem dados. A API de lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, declarações de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)de lote.

## Versões de chave desde o AEM 6.5 SP4 {#key-releases-since-last-sp}

Entre 05 de março de 2020 e 04 de junho de 2020, a Adobe lançou os seguintes recursos que estão fora do principal produto do AEM:

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)e [2020.5.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM Assets: Aplicativo para desktop 2.0.2.0](https://docs.adobe.com/content/help/pt-BR/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: Feature Pack 202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## Recursos úteis

* [Guias do usuário do AEM 6.5](../user-guide/home.md)

* [Notas de versão gerais do Adobe Experience Manager 6.5](release-notes.md)

* [Notas de versão do Service Pack para o Adobe Experience Manager 6.5](sp-release-notes.md)
