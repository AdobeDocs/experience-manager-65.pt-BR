---
title: Novidades do Adobe Experience Manager 6.5 Service Pack 4
description: Novidades do Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d0038181326037ab71f4df9b509d2f0827191c86

---


# Novidades do Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

O Adobe Experience Manager (AEM) 6.5 fornece recursos e melhorias contínuas por meio de Service Packs trimestrais este ano. A nova abordagem beneficia nossos clientes à medida que eles adotam as inovações mais rapidamente.

O AEM Service Pack 4 (6.5.4.0) mais recente foi lançado em 5 **de março de 2020**. Este artigo destaca os recursos que o Service Pack mais recente oferece para tornar sua jornada do AEM mais enriquecedora.

## AEM Sites {#aem-sites}

### Melhorias no desempenho em várias áreas {#performance-improvements}

* Redução do tempo para carregar e inicializar o ContextHub em um site (contexthub.kernel.js). Isso resulta no carregamento de uma página mais rápido durante uma visita ao site.

* Redução do tempo para atualizar uma página após arrastar e soltar Fragmentos de experiência na tela de um editor de página.

* Redução do tempo de carregamento de entradas para uma página Sites com mais de 200 cópias online na Visão geral da Live Copy.

* Aprimorado o tratamento de URLs incompletos ou inválidos que podem fazer com que o Editor de modelos fique lento no Editor de modelos.

Além disso, o AEM 6.5 Service Pack 4 inclui melhorias no Sistema de estilo. Agora você também pode selecionar estilos em uma caixa de diálogo de componente.

## Ativos AEM {#aem-assets}

### Integração com o Brand Portal por meio do Console de E/S da Adobe {#assets-integration-bp}

Agora você pode configurar os ativos AEM com o Portal de marcas por meio do Console de E/S da Adobe. O Console de E/S da Adobe obtém um token IMS para autorização do locatário do Brand Portal. Anteriormente, os ativos AEM eram configurados com o Brand Portal na interface clássica por meio do gateway OAuth herdado. As configurações que usam o Gateway OAuth Herdado serão suportadas até 6 de abril de 2020. Se você não modificar a integração, as configurações existentes continuarão funcionando.

Você pode criar uma nova integração ou atualizar suas configurações de integração para o Console de E/S da Adobe.

### Accessibility enhancements {#accessibility-enhancements}

* As caixas de seleção de estado misto agora têm um atributo marcado com ária com um valor &quot;misto&quot;, para expor seu estado misto aos leitores de tela.

* Os controles baseados em teclado agora são suportados além dos gestos baseados em caminho para mover-se em imagens ampliadas.

* As restrições de formato de data foram fornecidas em rótulos de campo para que usuários somente de teclado digitem manualmente a data.

* O atributo Alt foi adicionado aos ícones decorativos e removeu o atributo role=img, de modo que tais ícones e imagens não sejam expostos aos usuários do leitor de tela.

* O atributo Alt foi adicionado para fechar ícones para indicar aos usuários do leitor de tela quando eles o preparem.

## Formulários AEM {#aem-forms}

### Gerar saída imprimível em fluxos de trabalho do AEM Forms {#generate-printable-output}

Se você quiser que uma solução imprima ou salve várias cópias de um arquivo de modelo de origem e integre-o a um arquivo de dados com vários registros, uma nova etapa do fluxo de trabalho Gerar saída imprimível estará disponível no AEM Forms. Por exemplo, se você quiser imprimir um formulário de origem com um nome diferente toda vez que ele for impresso, poderá ter esses nomes no arquivo de dados e integrá-lo a um arquivo de modelo padrão.

Tire proveito desse recurso usando **Ferramentas** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Criar]** e pesquise a etapa do fluxo de trabalho **[!UICONTROL Gerar saída]** imprimível.

![Gerar saída para impressão](assets/generate-print-output-demo.gif)

Para obter mais informações sobre esse recurso, consulte Fluxo de trabalho centrado no [Forms em OSGi - Referência](../forms/using/aem-forms-workflow-step-reference.md)de etapas.

### Suporte a várias colunas para formulários adaptáveis e comunicações interativas no modo Layout {#multi-column-adaptive-forms}

Agora é possível definir o número de colunas para um painel em formulários adaptáveis e comunicações interativas.

Você pode encontrar a nova opção alternando para o modo Layout. Toque no painel que deseja converter em um formato de várias colunas, selecione seu pai e toque no ícone de várias colunas para definir o número de colunas para o painel.

![Layout de várias colunas](assets/multi-column-layout.gif)

Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../forms/using/resize-using-layout-mode.md).

### Personalizações da Caixa de entrada do AEM {#aem-inbox}

Você já sentiu a necessidade de personalizar as opções disponíveis no cabeçalho AEM? Agora é possível com a nova versão do Service Pack com a introdução de uma opção de controle **[!UICONTROL de]** administrador.

**Personalize o texto do cabeçalho**

Os administradores de fluxo de trabalho agora podem especificar o texto do cabeçalho de sua própria escolha.

Você pode encontrar a nova opção **[!UICONTROL Personalizar o texto]** do cabeçalho sob o seletor de exibição (disponível na parte superior direita da barra de ferramentas) > Controle **[!UICONTROL de]** administração.

**Personalizar logotipo**

Semelhante à personalização do texto do cabeçalho, os administradores do fluxo de trabalho agora podem especificar o logotipo do cabeçalho de sua própria escolha.

Você pode encontrar a nova opção **[!UICONTROL Personalizar logotipo]** no seletor de exibição > Controle **[!UICONTROL de]** administração.

Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

### Controle de navegação do usuário {#user-navigation-control}

Os administradores de fluxo de trabalho agora têm a opção de fazer com que os usuários trabalhem no AEM em um modo restrito com base em sua função. Os administradores podem controlar a exibição de opções de navegação disponíveis no cabeçalho para restringir os usuários a alternarem para o modo de criação do fluxo de trabalho ou outros links da solução.

Confira as novas opções **[!UICONTROL de navegação]** Ocultar no seletor de exibição > Controle **** administrativo.

Para obter mais informações sobre esse recurso, consulte [Sua Caixa de entrada](../sites-authoring/inbox.md).

### Suporte a Rich Text em formulários HTML5 {#rich-text-support}

O campo de texto agora pode exibir uma lista de opções de formatação no formulário HTML5 renderizado. É necessário definir um formato para o campo de texto no Forms Designer para aplicar as configurações apropriadas ao campo.

Para usar esse recurso, toque no campo de texto na Exibição **[!UICONTROL de]** design no Designer de formulários. Na guia **[!UICONTROL Campo]** , selecione **[!UICONTROL Rich Text]** na lista suspensa Formato **[!UICONTROL de]** campo para aplicar as configurações.

Para obter mais informações, consulte [Criar modelos de formulário para formulários](../forms/using/designing-form-template.md)HTML5.

## Principais destaques

Além dos novos recursos, o AEM 6.5 Service Pack 4 inclui os seguintes destaques principais:

* Agora você pode sincronizar subárvores de conteúdo seletivo para o *Dynamic Media - modo* Scene7 em vez de todos os disponíveis em `content/dam`.

* A integração do modelo de dados de formulário com o serviço da Web SOAP agora oferece suporte a grupos de escolha ou atributos em elementos.

* A entrada ou saída SOAP e estruturas de dados complexas agora suportam Substituição de Grupo Dinâmico.

## Principais recursos dos Service Packs anteriores do AEM 6.5

### Imagem inteligente para o Dynamic Media {#smart-imaging}

A geração de imagens inteligentes aproveita as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo de entrega para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte Imagem [inteligente](../assets/imaging-faq.md).

### Pesquisa visual para ativos AEM {#visual-search}

Os usuários do Assets podem pesquisar imagens visualmente semelhantes. O AEM exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. See [Visual search](../assets/search-assets.md).

### Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário {#share-request-access}

Você pode compartilhar seus itens da Caixa de entrada com outro usuário. Quando outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá solicitar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso a itens da Caixa de entrada de outros usuários. Consulte [Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário](../forms/using/configure-shared-queues-osgi.md).

### Configurar configuração fora do escritório para seus itens da Caixa de entrada {#configure-out-of-office}

Se você planeja estar fora do escritório, você pode especificar o que acontece com os itens que lhe são atribuídos para esse período.
Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que suas configurações de encerramento entrem em vigor. É possível definir uma pessoa padrão para a qual todos os itens serão enviados. Consulte [Configurar configurações](../forms/using/configure-out-of-office-settings.md)fora do escritório.

### Gerar várias comunicações interativas usando a API de lote {#generate-multiple-ic}

Você pode usar a API de lote para produzir várias comunicações interativas a partir de um modelo. O modelo é uma comunicação interativa sem dados. A API de lote combina dados com um modelo para produzir uma comunicação interativa. A API é útil na produção em massa de comunicações interativas. Por exemplo, contas telefônicas, declarações de cartão de crédito para vários clientes. Consulte [Gerar várias comunicações interativas usando a API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)de lote.

### Mensagens de erro de validação padrão para formulários adaptáveis {#standard-validation}

Formulários adaptáveis agora podem ser integrados a serviços personalizados para executar validações de dados. Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação retornada pelo servidor estiver no formato de mensagem padrão, as mensagens de erro serão exibidas no nível do campo no formulário. Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação do servidor não estiver no formato de mensagem padrão, os formulários adaptativos fornecerão um mecanismo para transformar as mensagens de erro de validação em um formato padrão, de modo que sejam exibidas no nível do campo no formulário. Consulte Mensagens de erro de validação [padrão para formulários](../forms/using/standard-validation-error-messages-adaptive-forms.md)adaptáveis.

## Versões de chave desde o AEM 6.5 SP3

Entre 12 de dezembro de 2019 e 5 de março de 2020, a Adobe lançou os seguintes recursos que estão fora do principal produto do AEM:

* Aprimoramentos mensais do AEM Cloud Manager 2020.1.0 e 2020.2.0 para o Cloud Manager, as duas últimas versões tiveram como objetivo melhorar o status do pipeline e a capacidade de baixar registros para as várias etapas. Leia as notas de versão completas aqui:
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* Atualizações da CLI do AEM Cloud ManagerAutomatize as tarefas do Cloud Manager usando a ferramenta de linha de comando. Estamos continuamente estendendo a CLI - junte-se ao [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Tipo de arquivo do projeto 23A melhor maneira de iniciar um novo projeto do AEM. Com o Archetype 23, estamos [mesclando o Project Archetype for SPA e os sites regulares em um único](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23), além de fornecer um tema padrão para iniciar seu desenvolvimento de front-end.

* AEM Sites: Site de referência WKNDetodos os [novos projetos](https://www.wknd.site/) de referência com as práticas recomendadas sobre como criar sites com o AEM. Saiba mais ao ler o tutorial [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) WKND completamente atualizado e capturar o código do [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Core Components 0.7.0 e 0.9.0Integrando o AEM Sites e o Magento Commerce. Estamos [estendendo continuamente os Componentes principais dedicados e um Arquivo de projeto com foco no Comércio](https://github.com/adobe/aem-core-cif-components/releases).

* AEM Assets: Aplicativo para desktop 2.0.1.1
   [Obtenha acesso aos ativos para desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens: Feature Pack 202001Sinalização digital diretamente do AEM. Obtenha as melhorias mais recentes com o Feature Pack mais recente, desta vez estamos [habilitando a reprodução síncrona em vários players](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)de mídia.

## Recursos úteis

* [Guias do usuário do AEM 6.5](../user-guide/capabilities.md)

* [Notas de versão gerais do Adobe Experience Manager 6.5](release-notes.md)

* [Notas de versão do Service Pack para o Adobe Experience Manager 6.5](sp-release-notes.md)
