---
title: Novidades do  [!DNL Experience Manager] 6.5 Service Pack 8
description: Novidades do  [!DNL Experience Manager] 6.5 Service Pack 8
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 2c6d11f63420040a500bbb75f1146c29f64bdcc5
workflow-type: tm+mt
source-wordcount: '2883'
ht-degree: 1%

---


# Novidades do [!DNL Adobe Experience Manager] 6.5 Service Pack 8 {#aem-whats-new-service-pack}

![Novidades](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Os Service Packs oferecem novos recursos, melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança em intervalos trimestrais. A disponibilidade trimestral facilita o acesso e a adoção de novos recursos e inovações.

Este artigo destaca os recursos incluídos no Service Pack mais recente, [principais recursos incluídos nos 6.5 Service Packs anteriores](#key-features-previous-service-packs), e as [versões de chave desde a última versão do Service Pack](#key-releases-since-last-sp).

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### Classifique as páginas da Live Copy disponíveis para implantação {#sort-livecopy-pages}

Agora é possível classificar as páginas da Live Copy disponíveis para implantação usando as propriedades [!UICONTROL Name], [!UICONTROL Last modified date] e [!UICONTROL Last rollout date]. A [!UICONTROL Data da última implementação] de uma página é uma nova propriedade introduzida nesta versão.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* Ao usar [a funcionalidade Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md), agora é possível visualizar uma lista de todas as páginas [!DNL Sites] que usam o ativo. Essas referências a um ativo estão disponíveis na página [!UICONTROL Propriedades] de um ativo. Isso permite que administradores, profissionais de marketing e bibliotecas tenham uma visão completa do uso dos ativos, permitindo um melhor rastreamento, gerenciamento e consistência da marca.

* Ao excluir um ativo referenciado em uma página da Web, [!DNL Experience Manager] exibe um aviso. É possível forçar a exclusão de um ativo referenciado ou verificar e modificar as referências exibidas na página [!DNL Properties] do ativo. Clicar nas referências abre as páginas [!DNL Sites] locais e remotas.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>O pacote complementar de [!DNL Experience Manager Forms] é disponibilizado uma semana após a versão agendada do [!DNL Experience Manager] Service Pack.

## Principais recursos dos [!DNL Experience Manager] 6.5 Service Packs {#key-features-previous-service-packs} anteriores

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Disponibilidade de movimentações de página e implantações de MSM como operações assíncronas (6.5.7.0) {#page-moves-msm-asynchronous}

Agora é possível executar movimentações de página e implantações de MSM como operações assíncronas para reduzir seu impacto no desempenho do tempo de execução. Você pode programar as operações para execução imediata ou posterior. O status das tarefas associadas e das etapas do processo é exibido em um console, que é útil para monitorar implantações de MSM em grande escala.

#### Disponibilidade da operação de movimentação de página no modo assíncrono (6.5.6.0) {#page-move-asynchronous}

A operação Mover página agora está disponível no modo assíncrono. Além da execução imediata, você também pode agendar a operação Mover página para execução posterior.

#### Melhorias de acessibilidade (6.5.5.0) {#accessibility-sites}

* Aprimoramento do relatório de erros ao adicionar informações de texto.

* Foco aprimorado na interface do usuário durante a navegação pelo teclado.

* Taxa de contraste aprimorada para vários elementos da interface do usuário.

* Consistência aprimorada de atributos alt para imagens de página.

* Consistência aprimorada de rótulos ARIA (Accessible Rich Internet Applications).

* Melhorias nos recursos de Acesso não visual a desktop (NVDA).

* Aprimoramento do suporte ao leitor de tela.

#### Outras melhorias importantes (6.5.5.0) {#other-enhancements-sites}

* O acesso anônimo ao CRXDE Lite não tem permissão para melhorar a segurança. Em vez disso, os usuários são direcionados para a tela de logon. Consulte [Desenvolvimento com CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Ao copiar ou colar uma árvore de página, agora há a opção de colar a página raiz ou colar a página raiz com as subpáginas da árvore.

* [!DNL Adobe Experience Manager Experience Fragments] exportados para  [!DNL Adobe Target] espaços de trabalho agora aparecem como tipos de oferta exclusivos e fontes de oferta no  [!DNL Target].

* Gerenciador de vários sites - o acionador Publicar agora exclui um componente da página publicada se um componente for excluído da página de origem.

* Gerenciador de vários sites - Quando o nome de um componente local em uma [!UICONTROL Live Copy] é idêntico ao nome de um componente no blueprint e o componente é implementado no blueprint, o termo `_msm_moved` agora é adicionado ao nome do componente local.

#### Aprimoramentos do sistema de estilos (6.5.4.0) {#style-system-enhancements}

Agora é possível selecionar estilos na caixa de diálogo do componente usando o Sistema de estilos aprimorado.

#### Melhorias de desempenho em várias áreas (6.5.4.0) {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (`contexthub.kernel.js`). Isso resulta em carregamentos de página mais rápidos durante uma visita ao site.

* Redução do tempo para atualizar uma página depois de arrastar [!DNL Experience Fragments] para [!DNL Sites] Editor de página.

* Tempo de carregamento reduzido para entradas em uma página [!DNL Sites] com mais de 200 cópias ativas em **[!UICONTROL Visão geral da Live Copy]**.

* Manuseio aprimorado de URLs incompletas ou inválidas. Esses URLs podem atrasar o Editor de modelo.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* [!DNL Assets] e  [!DNL Dynamic Media] oferecem várias melhorias de acessibilidade. Os aprimoramentos estão relacionados à navegação do teclado, ao uso de leitores de tela e a melhorias semelhantes para permitir o uso de tecnologias de assistência (AT). Consulte [[!DNL Assets] aprimoramentos](/help/release-notes/sp-release-notes.md#assets-6570) e [[!DNL Dynamic Media] aprimoramentos](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Os usuários podem classificar ativos digitais nas exibições de Cartão e Coluna (6.5.7.0).

#### Aprimoramentos de acessibilidade (6.5.6.0) {#accessibility-assets-6560}

* **Foco aprimorado na interface do usuário durante a navegação** do teclado, por exemplo, foco em:

   * `x` ícone na caixa de diálogo  [!UICONTROL Visualização de ] versão de um ativo na  [!UICONTROL Linha do tempo].

   * Opções acionáveis da interface do usuário.

   * Campo de email na caixa de diálogo [!UICONTROL Compartilhar link] e campo para adicionar grupo de usuários fechado na guia [!UICONTROL Permissão] da pasta [!UICONTROL Propriedades].

* **Funcionalidade aprimorada com teclas do teclado**

   Os usuários podem usar teclas de teclado para arrastar controles no editor de Formulário de esquema de metadados no modo de navegação do leitor de tela.

* **Maior usabilidade para usuários** de leitores de tela devido ao seguinte:

   * Leitores de tela anunciam a finalidade dos players de vídeo e áudio.

   * Os leitores de tela anunciam a finalidade das opções da interface do usuário para remover as tags selecionadas usando a caixa de diálogo [!UICONTROL Tags selection] no ativo [!UICONTROL Properties].

   * Os leitores de tela anunciam os cabeçalhos de linha e os itens de linha das tabelas, para que os usuários saibam quais entradas pertencem à mesma linha.

   * Título descritivo e significativo da página de pesquisa.

   * Os leitores de tela anunciam as opções no painel do filtro de pesquisa como opções expansíveis.

#### Outras melhorias em [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Os grupos de usuários associados a pastas (privadas e não privadas) agora são removidos do repositório em [exclusão dessas pastas](/help/assets/private-folder.md#delete-private-folder). No entanto, os grupos de usuários redundantes, órfãos, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o JMX.

#### Aprimoramentos de acessibilidade em [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] O agora está mais acessível, em conformidade com as Web Content Accessibility Guidelines (WCAG). A acessibilidade melhorou devido aos seguintes aprimoramentos:

* Muitos elementos, controles, páginas e caixas de diálogo da interface do usuário são amigáveis para leitores de tela.

* Muitos elementos da interface do usuário, controles e campos de formulário de entrada podem ser acessados pelo teclado.

* A cor e o contraste de alguns elementos da interface do usuário são atualizados para que os usuários com visão limitada ou usuários sem percepção de cor possam distinguir esses elementos da interface do usuário. Por exemplo, a cor dos ícones de classificação de estrelas (como na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] no ativo [!UICONTROL Propriedades] ou na exibição de cartão) é alterada para obter o contraste apropriado.

   ![Ícones de classificação com melhor contraste](assets/star-rating-icons.png)

#### Tratamento de exceções aprimorado (6.5.5.0) {#exception-handling}

[!DNL Assets] o fluxo da interface do usuário tem melhor tratamento de exceções. Se um ativo não tiver um tipo para sua dimensão, a exceção observada será registrada nos arquivos de log.

#### Suporte para ativos 3D em [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

O suporte para imagens 3D em [!DNL Dynamic Media] permite que os clientes publiquem e adicionem conteúdo 3D em páginas e aplicativos da Web. O suporte inclui:

* Publique formatos comuns de ativos 3D e gere um URL de ativo que possa ser usado em páginas da Web e outros aplicativos.

* Um Visualizador da Web 3D, desenvolvido por [!DNL Adobe Dimension], para visualizar interativamente os ativos 3D publicados.

* Publique e visualize ativos 3D comuns em [!DNL Experience Manager Sites] páginas usando o componente [!DNL Sites] WCM.

#### Configure [!DNL Experience Manager Assets] com [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

O canal de autorização entre [!DNL Experience Manager Assets] e [!DNL Brand Portal] é alterado. Anteriormente, [!DNL Brand Portal] era configurado na interface clássica por meio do Gateway OAuth herdado, que usa a troca de token JWT para obter um token de Acesso IMS para autorização. [!DNL Experience Manager Assets] O agora é configurado com o  [!DNL Brand Portal] por meio do  [!DNL Adobe I/O], que obtém um token IMS para autorização do  [!DNL Brand Portal] locatário.

As etapas para configurar [!DNL Experience Manager Assets] com [!DNL Brand Portal] são diferentes dependendo da sua versão [!DNL Experience Manager] e se você está configurando pela primeira vez ou atualizando as configurações existentes. Consulte [Configurar ativos do Experience Manager com o Brand Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) para obter detalhes.

#### Aprimoramentos de acessibilidade (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] O inclui os seguintes aprimoramentos de acessibilidade:

* Teclas de seta no teclado podem ser usadas para mover e deslocar áreas dentro de imagens com zoom. Para obter mais informações, consulte [visualizar ativos usando apenas teclas do teclado](../assets/manage-assets.md#previewing-assets).

* As caixas de seleção de estado misto (nas quais, a menos que você selecione todos os predicados aninhados, as caixas de seleção de primeiro nível não são selecionadas e passam por elas) no painel Filtros são legíveis por leitores de tela.

* As restrições de formato de data e hora são fornecidas nos rótulos de campo dos campos de data, para permitir que os usuários insiram a data no formato correto usando o teclado.
Por exemplo, `On Time (MM-DD-YYYY HH:mm)`. Aqui MM é mês em formato de dois dígitos, AAAA é ano, DD é dia em formato de dois dígitos, HH é hora em formato militar de 24 horas e mm é minuto.

* Os leitores de tela anunciam a opção de remover as tags selecionadas (símbolo`X`) e o número das tags selecionadas.

#### Coluna classificável para a Data de criação dos ativos na exibição de lista (6.5.3.0) {#sortable-date-created-column}

Uma nova coluna classificável para a data de criação dos ativos é adicionada na exibição de lista do DAM e nos resultados da pesquisa de ativos na exibição de lista.

![Coluna classificável para data de criação](assets/asset-created-date.png)

#### Pesquisa visual por [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets]Os usuários do podem pesquisar imagens visualmente semelhantes. O Experience Manager exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [Pesquisa visual](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalidar o conteúdo em cache do CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Agora você pode usar a interface do usuário [!DNL Dynamic Media] para invalidar o conteúdo em cache da Rede de entrega de conteúdo (CDN). Como resultado, os ativos atualizados estão disponíveis instantaneamente em vez de esperar que o cache expire. Você pode invalidar o CDN ao:

* Criando um modelo de invalidação de CDN: Seleção de ativos e URLs com base em modelo associados ao formulário

* Seleção de ativos e predefinições associadas por meio do seletor de ativos

* Adicionar URLs completos do ativo

#### Publicação seletiva de ativos em [!DNL Experience Manager] e [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Agora é possível optar por publicar ou cancelar a publicação seletiva de ativos em [!DNL Experience Manager] ou [!DNL Dynamic Media] usando o assistente [!UICONTROL Publicação rápida] ou [!UICONTROL Gerenciar publicação]. Você também pode definir o modo `Publish` ou `Unpublish` no nível da pasta.

#### Imagem inteligente para Dynamic Media {#smart-imaging}

A geração de imagens inteligentes usa as características de visualização exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagens inteligentes](../assets/imaging-faq.md).

#### Recorte inteligente em perfis de vídeo para Dynamic Media (6.5.3.0) {#smart-crop-video}

Recorte inteligente para vídeo - um recurso opcional disponível em Perfis de vídeo - é uma ferramenta que usa o poder da inteligência artificial no Adobe Sensei para detectar e recortar automaticamente o ponto focal em qualquer vídeo adaptável ou vídeo progressivo que você tenha carregado, independentemente do tamanho. Consulte [Sobre como usar o recorte inteligente em perfis de vídeo](../assets/video-profiles.md).

### Formulários do Experience Manager {#aem-forms-previous-service-packs}

#### Melhorias de desempenho (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 O Service Pack 7 do Forms melhora o desempenho para:

* Validação dos valores de campo no servidor ao enviar um formulário adaptável.

* Converter um formulário PDF em um formulário adaptável usando o [!DNL Automated Forms Conversion service].

#### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com serviços da Web RESTful como fonte de dados agora inclui configurações de cliente HTTP para otimização de desempenho. Consulte [Configurar fontes de dados](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilidade da opção de redefinição para cada componente no modo Layout (6.5.7.0) {#reset-option-layout-mode}

Agora é possível usar a opção de redefinição para cada componente no modo Layout de um formulário adaptável. Ao definir um layout de várias colunas para um painel, você pode usar esse recurso para redefinir componentes individuais dentro do painel. Consulte [Usar o modo de layout para redimensionar componentes](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Preencha previamente um formulário adaptável no cliente (6.5.6.0) {#prefill-merge-data-at-client}

Ao preencher previamente um formulário adaptável, o servidor [!DNL Experience Manager Forms] une os dados a um formulário adaptável e entrega o formulário preenchido a você. Por padrão, a ação de mesclagem de dados ocorre no servidor.
Agora você pode configurar o servidor [!DNL Experience Manager Forms] para [executar a ação de mesclagem de dados no cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md) em vez do servidor. Reduz significativamente o tempo necessário para preencher e renderizar formulários adaptáveis.

#### Integração do modelo de dados de formulário com APIs RESTful em um servidor com implementação SSL bidirecional (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] O modelo de dados de formulário agora pode ser  [integrado com RESTful APIs em um servidor que tem um SSL bidirecional implementado nele](../../help/forms/using/configure-data-sources.md).

#### Adição de suporte para [!DNL Adobe Sign] Tags de texto no Automated forms conversion Service (6.5.6.0) {#sign-integration-acroform-afcs}

Se um AcroForm incluir [!DNL Adobe Sign] Tags de texto, esses campos agora serão reconhecidos e representados como campos [!DNL Adobe Sign] no formulário adaptável convertido usando [!DNL Automated Forms Conversion service]. Um assinante pode preencher esses campos ao assinar o formulário adaptável.

#### Suporte para converter PDF forms coloridos em formulários adaptáveis (6.5.6.0) {#colored-PDF-forms}

Você pode usar [!DNL Automated Forms Conversion service] para converter PDF forms coloridos em formulários adaptáveis.

#### Suporte para protocolos SMB 2 e SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] agora suporta protocolos SMB 2 e SMB 3.

#### Armazenamento em cache aprimorado para páginas de formulário adaptável traduzidas (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Agora é possível especificar [locale como um seletor no URL do formulário adaptável, em vez de um argumento no URL do formulário adaptável](../../help/forms/using/supporting-new-language-localization.md). Ajuda a colocar formulários adaptáveis em cache em [!DNL Experience Manager Dispatcher]. O armazenamento em cache de formulários adaptáveis traduzidos não era possível em versões anteriores. Para obter informações detalhadas sobre como configurar o armazenamento em cache para usar o local como seletor no URL do formulário adaptável, consulte [Configurar o cache do formulário adaptável no dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Salve a saída do serviço de modelo de dados de formulário em uma variável (6.5.6.0) {#save-fdm-service-to-variable}

O modelo de dados de formulário permite salvar a saída de um serviço de modelo de dados de formulário em uma variável. [!DNL Experience Manager Forms] agora mapeia automaticamente o tipo de serviço de modelo de dados de formulário para o tipo de variável.

#### Anexar vários arquivos para o componente Anexo de arquivo (6.5.6.0) {#attach-multiple-files}

Agora é possível [anexar vários arquivos](../../help/forms/using/introduction-forms-authoring.md) ao componente [!UICONTROL Anexo de arquivo] de formulários adaptáveis.

#### Personalizar as colunas da Caixa de entrada do Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Você pode personalizar uma [!DNL Experience Manager] Caixa de entrada para alterar o título padrão de uma coluna, reorganizar a posição de uma coluna e exibir colunas adicionais com base nos dados de um fluxo de trabalho. Os membros do grupo `administrators` ou `workflow-administrators` podem personalizar as colunas. Para obter mais informações, consulte [Admin Control](../sites-authoring/inbox.md#inbox-admin-control).

![Personalizar colunas da Caixa de entrada do Experience Manager](assets/customize-columns.gif)

#### Salvar comunicações interativas como rascunho (6.5.5.0) {#save-as-draft}

Você pode usar a interface do usuário do agente para salvar um ou mais rascunhos de cada Comunicação interativa e recuperar o rascunho posteriormente para continuar trabalhando nela. Você pode especificar um nome diferente para cada rascunho para identificá-lo. Para obter mais informações, consulte [Salvar comunicações interativas como rascunho](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Salvar como rascunho](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] suporte ao servidor de aplicativos (6.5.5.0)  {#weblogic-support}

A Adobe Experience Manager Forms adicionou suporte para [!DNL Oracle WebLogic 12] para Adobe Experience Manager Forms no JEE. Você pode atualizar de uma versão anterior ou configurar um novo Experience Manager 6.5 Forms no servidor JEE em [!DNL Oracle WebLogic] 12.2.1.4 e posterior. Mais tarde corresponde às alterações de versão secundária, onde x em 12.2.1.x é substituído por um número de versão.

#### Melhorias de acessibilidade (6.5.5.0) {#accessibility-improvements}

O Adobe Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Quando um usuário visualiza um formulário adaptável como um formulário HTML, o campo [!UICONTROL Assinatura do rabisco] retém o foco da guia.

* As mensagens de erro exibidas ao enviar um formulário adaptável agora contêm o atributo `aria-describedBy`. O atributo é anexado aos campos mencionados na mensagem de erro. O atributo `aria-describedby` indica as IDs dos elementos que descrevem o objeto. Ajuda a estabelecer uma relação entre widgets ou grupos e texto que os descreveu.

* Se um formulário adaptável tiver alguns campos obrigatórios, o atributo obrigatório será definido como `True` para esses campos no schema de acessibilidade ARIA.

#### Autenticação com certificado X-509 para serviços da Web baseados em SOAP no modelo de dados de formulário (6.5.5.0) {#x509-based-authentication-soap}

O modelo de dados de formulário agora oferece suporte à autenticação baseada em certificado X-509 ao usar serviços da Web SOAP como a fonte de dados. Para obter mais informações, consulte [Configurar serviços Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Outras melhorias importantes (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms na Segurança de documentos JEE agora é baseado em [!DNL Apache Struts 2].

* Adição de suporte para [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Gerar saída para impressão em workflows do Experience Manager Forms (6.5.4.0) {#generate-printable-output}

A etapa de fluxo de trabalho Gerar saída para impressão permite integrar um arquivo de modelo de origem a um arquivo de dados. Essa integração permite que você imprima ou salve cópias diferentes do arquivo de modelo. A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL. Para obter mais informações sobre esse recurso, consulte [Fluxo de trabalho centrado no Forms em OSGi - Referência da etapa](../forms/using/aem-forms-workflow-step-reference.md).

![Gerar saída para impressão](assets/generate-print-output-step.gif)

#### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout (6.5.4.0) {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas. Alterne para o modo de layout para usar a nova opção de várias colunas. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

![Layout de várias colunas](assets/multi-column-layout.gif)

#### Personalizações da Caixa de entrada do Experience Manager (6.5.4.0) {#aem-inbox}

A nova opção Controle de administrador permite que os administradores:

* Personalize o texto e o logotipo do cabeçalho.

* Controlar a exibição de links de navegação disponíveis no cabeçalho.

A opção Controle de administrador é visível somente para os membros do grupo `administrators` ou `workflow-administrators`. Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

#### Suporte a rich text em formulários HTML5 (6.5.4.0) {#rich-text-support}

Converta um campo de texto em um formulário XFA em um campo de rich text em um formulário HTML5. Para obter mais informações, consulte [Criação de modelos de formulário para formulários HTML5](../forms/using/designing-form-template.md).

#### Aprimoramentos de acessibilidade (6.5.4.0) {#forms-accessibility-enhancements-6540}

O Experience Manager Forms inclui os seguintes aprimoramentos de acessibilidade:

* Os leitores de tela anunciam as caixas de seleção, os links, o Seletor de data e os campos de Entrada de data corretamente em um formulário adaptável.

* Cada página de um formulário adaptável agora inclui um título e um rótulo principal de marca.

#### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Assim que outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá reivindicar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso aos itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

#### Defina as configurações de ausência do escritório para os itens da Caixa de entrada de um usuário do Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Se você planeja estar fora do escritório, você pode especificar o que acontece com os itens que são atribuídos a você para esse período.
Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que as configurações de ausência do escritório entrem em vigor. Você pode definir uma pessoa padrão para a qual todos os itens são enviados. Consulte [Definir configurações de ausência do escritório](../forms/using/configure-out-of-office-settings.md).

#### Gere várias comunicações interativas usando a API em lote para o Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Você pode usar a API em lote para produzir várias comunicações interativas de um modelo. O modelo é uma comunicação interativa sem dados. A API em lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API em lote](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versões de chave desde [!DNL Adobe Experience Manager] 6.5 SP7 {#key-releases-since-last-sp}

Entre 26 de novembro de 2020 e 25 de fevereiro de 2021, a Adobe lançou o seguinte, além dos Service Packs e dos Cumulative Fix Packs:

* [!DNL Adobe Experience Manager] como Cloud Service  [2020.11.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-11-0.html),  [2020.12.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-12-0.html) e  [2021.1.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date).

* [[!DNL Experience Manager] aplicativo de desktop 2.1 (2.1.0.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Feature Pack 202011](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202011.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] Documentação 6.5](../user-guide/home.md)
>* [Notas de versão gerais do [!DNL Adobe Experience Manager] 6.5](release-notes.md)
>* [Notas de versão do Service Pack para [!DNL Adobe Experience Manager] 6.5](sp-release-notes.md)

