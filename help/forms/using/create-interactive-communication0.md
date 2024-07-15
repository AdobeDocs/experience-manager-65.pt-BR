---
title: "Tutorial: Criar a comunicação interativa"
description: Criar uma comunicação interativa usando todos os elementos
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Tutorial: Criar a comunicação interativa {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Este tutorial é uma etapa da série [Criar sua primeira Comunicação Interativa](/help/forms/using/create-your-first-interactive-communication.md). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

Depois de criar todos os blocos de construção, como modelo de dados de formulário, fragmentos de documento, modelos e temas para a versão da Web, você pode começar a criar uma comunicação interativa.

As Comunicações interativas podem ser fornecidas por meio de dois canais: Impressão e Web. Você também pode criar uma Comunicação interativa com o canal de impressão como mestre. A opção Print as master para o canal da Web garante que o conteúdo, a herança e a associação de dados do canal da Web sejam derivados do canal de impressão. Também garante que as alterações feitas no canal Print sejam sincronizadas no canal Web. Os autores da Comunicação interativa podem, no entanto, interromper a herança de componentes específicos no canal da Web.

Este tutorial percorre as etapas para criar comunicações interativas para canais impressos e da Web. Ao final deste tutorial, você será capaz de:

* Criar comunicação interativa para o canal de impressão
* Criar comunicação interativa para o canal da Web
* Criar comunicações interativas da Web e de impressão com Imprimir como mestre

## Criar comunicações interativas para impressão e Web sem sincronização {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Criar comunicação interativa para o canal de impressão {#create-interactive-communication-for-print-channel}

Esta é a lista de recursos que já foram criados neste tutorial e que são necessários ao criar a Comunicação interativa para o canal de impressão:

**Modelo de impressão:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modelo de Dados de Formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_charges_first_ic](../../forms/using/create-document-fragments.md)

**Fragmentos de layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Imagens:** PayNow e ValueAddedServices

1. Faça logon na instância de autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **Criar** e selecione **Comunicação interativa**. O assistente **Criar Comunicação Interativa** é exibido.
1. Especifique **create_first_ic** no **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e selecione **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**. Certifique-se de que a caixa de seleção **Usar impressão como principal para canal da Web** não esteja marcada.

   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Select**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecione **Editar** para abrir a Comunicação Interativa no painel direito.
1. Vá para a guia **Assets** e aplique o filtro para exibir somente os fragmentos de documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento nas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Fatura |
   | customer_details_first_ic | DetalhesDoCliente |
   | bill_summary_first_ic | Resumo da fatura |
   | summary_charge_first_interative_communication | Encargos |

   ![Fragmentos de documentos para Comunicações Interativas](assets/create_first_ic_doc_fragments_new.png)

1. Selecione a área de destino **Gráficos** e **+** para adicionar um componente **Gráfico**.
1. Selecione o componente Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecione **Pizza** na lista suspensa **Tipo de Gráfico**.
   1. Selecione a propriedade **calltype** do tipo de objeto de modelo de dados **calls** na seção **eixo X**. Selecione ![done_icon](assets/done_icon.png).
   1. Selecione **Frequência** na lista suspensa **Função**.
   1. Selecione a propriedade **calltype** do tipo de objeto de modelo de dados **calls** na seção **eixo Y**. Selecione ![done_icon](assets/done_icon.png).
   1. Selecione ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Vá para a guia **Assets** e aplique o filtro para exibir somente os fragmentos de layout no painel esquerdo. Arraste e solte o fragmento de layout **table_lf** na área de destino **Chamadas Discriminadas**.
1. Selecione o Campo de texto na coluna **Data** e selecione ![configure_icon](assets/configure_icon.png) (Configurar).
1. Selecione **Objeto de Modelo de Dados** na lista suspensa **Tipo de Associação** e selecione **chamadas** > **calldate**. Selecione ![done_icon](assets/done_icon.png) duas vezes para salvar as propriedades.

   Da mesma forma, crie uma associação com **calltime**, **callnumber**, **callduration** e **callcharge** para campos de texto nas colunas **Time**, **Number**, **Duration** e **Charges**, respectivamente.

1. Selecione a área de destino **PayNow** e **+** para adicionar um componente **Image**.
1. Selecione o componente de Imagem e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especifique **PayNow** como o nome da imagem no campo **Name**.
   1. Selecione **Carregar**, a imagem salva no sistema de arquivos local e **Abrir**.
   1. Selecione ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Repita as etapas 13 e 14 para adicionar a imagem **ValueAddedServices** à área de destino **ValueAddedServices**.

### Criar comunicação interativa para o canal da Web {#create-interactive-communication-for-web-channel}

Esta é a lista de recursos que já foram criados neste tutorial e são necessários ao criar a Comunicação interativa para o canal da Web:

**Modelo da Web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modelo de Dados de Formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_charges_first_ic](../../forms/using/create-document-fragments.md)

**Imagens:** PayNowWeb e ValueAddedServicesWeb

1. Faça logon na instância de autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **Criar** e selecione **Comunicação interativa**. O assistente **Criar Comunicação Interativa** é exibido.
1. Especifique **create_first_ic** no **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e selecione **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**. Certifique-se de que a caixa de seleção **Usar impressão como principal para canal da Web** não esteja marcada.

   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Select**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecione **Editar** para abrir a Comunicação Interativa no painel direito.
1. Selecione a guia **Canais** no painel esquerdo e selecione **Web**.
1. Vá para a guia **Assets** e aplique o filtro para exibir somente os fragmentos de documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento nas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Fatura |
   | customer_details_first_ic | DetalhesDoCliente |
   | bill_summary_first_ic | Resumo da fatura |
   | summary_charge_first_interative_communication | Encargos |

1. Selecione a área de destino **Resumo de Encargos** e **+** para adicionar um componente **Gráfico**.
1. Selecione o componente Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecione **Pizza** na lista suspensa **Tipo de Gráfico**.

   1. Selecione a propriedade **calltype** do tipo de objeto de modelo de dados **calls** na seção **eixo X**. Selecione ![done_icon](assets/done_icon.png).

   1. Selecione **Frequência** na lista suspensa **Função**.

   1. Selecione a propriedade **calltype** do tipo de objeto de modelo de dados **calls** na seção **eixo Y**. Selecione ![done_icon](assets/done_icon.png).

   1. Selecione ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Selecione a guia **Fontes de Dados** no painel esquerdo e arraste e solte o objeto de modelo de dados **chamadas** na área de destino **Chamadas detalhadas**. Todas as propriedades no objeto de modelo de dados **calls** são exibidas como colunas de tabela na área de destino **Chamadas Discriminadas** no painel direito.

   Com base no caso de uso, você exige as colunas Data da chamada, Hora da chamada, Número da chamada, Duração da chamada e Encargos da chamada na tabela.

   ![Tabela para comunicação interativa](assets/table_ic_web_new.png)

1. Selecione o cabeçalho de coluna da tabela **Mobilenum** e selecione **Mais opções** > **Excluir coluna**. Da mesma forma, exclua a coluna **Calltype**.
1. Selecione o cabeçalho de coluna da tabela **Calldate** e selecione ![edit](assets/edit.png) (Editar) para renomear o texto como **Call Date**. Da mesma forma, renomeie outros cabeçalhos de coluna na tabela.
1. Com base no caso de uso, insira um botão **Pagar agora** na Comunicação interativa que forneça ao usuário uma opção para fazer o pagamento clicando no botão. Execute as seguintes etapas para inserir o botão:

   1. Selecione a área de destino **Pagar Agora** e **+** para adicionar um componente **Texto**.

   1. Selecione o componente de texto e selecione ![editar](assets/edit.png) (Editar).
   1. Renomeie o texto para **Pagar Agora**.
   1. Selecione o texto e o ícone de Hiperlink.
   1. Especifique a URL de pagamento no campo **Caminho**.
   1. Selecione **Nova guia** na lista suspensa **Destino**.

   1. Selecione ![done_icon](assets/done_icon.png) para salvar as propriedades do hiperlink.

1. Selecione **Style** na lista suspensa ao lado da opção **Preview**.

   ![Selecionar modo de Estilo para Comunicação Interativa](assets/select_style_ic_web_new.png)

1. Estilize o texto do hiperlink para exibi-lo como um botão na Comunicação interativa usando as seguintes etapas:

   1. Selecione o componente de texto e selecione ![editar](assets/edit.png) (Editar).
   1. Na seção **Borda**, especifique **1.5px** como **Largura da Borda**, selecione **Sólido** como **Estilo da Borda** e especifique **46px** como **Raio da Borda**.

   1. Selecione Vermelho como a cor de fundo do botão na seção **Plano de fundo**.
   1. No campo **Margem** para a seção **Dimension e Posição**, selecione o ícone **Editar simultaneamente** e defina a margem **Direita** como **450px**. Os campos Superior, Inferior e Esquerdo são definidos como em branco.

   ![Inserir hiperlink na comunicação interativa](assets/ic_web_hyperlink_new.png)

1. Selecione a área de destino **Pagar Agora** e **+** para adicionar um componente **Imagem**.
1. Selecione o componente de Imagem e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especifique **PayNow** como o nome da imagem no campo **Name**.

   1. Selecione **Carregar**, selecione a imagem **PayNowWeb** salva no sistema de arquivos local e selecione **Abrir**.

   1. Selecione ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Com base no caso de uso, insira um botão **Assinar** na Comunicação Interativa que forneça ao usuário uma opção para assinar os serviços de valor agregado clicando no botão.

   Repita as etapas 13 - 17 para adicionar um botão **Assinar** à área de destino **Serviços de Valor Agregado** e adicionar a imagem **ValueAddedServicesWeb**.

## Criar comunicações interativas para impressão e Web com sincronização automática {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Você também pode criar uma Comunicação interativa permitindo a sincronização automática entre canais de impressão e da Web. Para habilitar a sincronização automática, selecione a opção Print as master ao criar a comunicação interativa. Selecionar a opção Imprimir como mestre garante que o conteúdo, a herança e a associação de dados do canal da Web sejam derivados do canal de impressão. Também garante que as alterações feitas no canal Print sejam refletidas no canal Web.

Execute as seguintes etapas para derivar o conteúdo do canal da Web usando o Canal de impressão:

1. Faça logon na instância de autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **Criar** e selecione **Comunicação interativa**. O assistente **Criar Comunicação Interativa** é exibido.
1. Especifique **create_first_ic** no **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e selecione **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**.

   1. Marque a caixa de seleção **Usar impressão como principal para canal da Web**.
   1. Especifique **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Select**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecione **Editar** para abrir a Comunicação Interativa no painel direito.
1. Execute as etapas 6 a 15 da seção [Criar comunicação interativa para canal de impressão](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Selecione a guia **Canais** no painel esquerdo e selecione **Web** para gerar automaticamente conteúdo para o canal da Web a partir do canal de impressão.
1. Como a caixa de seleção **Usar impressão como principal para canal da Web** está marcada na etapa 4, o conteúdo e as associações são gerados automaticamente para o canal da Web a partir do canal de impressão.

   O conteúdo do canal de impressão é inserido abaixo do conteúdo do modelo de canal da Web. Para modificar o conteúdo do canal da Web que foi gerado automaticamente no canal de impressão, você pode cancelar a herança de qualquer área de destino.

   Passe o mouse sobre a área de destino relevante no canal da Web e selecione ![cancelar herança](assets/cancelinheritance.png) (Cancelar herança) e, na caixa de diálogo **Cancelar herança**, selecione **Sim**.

   ![Cancelar herança](assets/cancel_inheritance_web_channel_new.png)

   Se você cancelou a herança de um componente, é possível reativá-lo. Para reativar a herança, passe o mouse sobre o limite da área de destino relevante, que inclui o componente, e selecione ![reenableinheritance](assets/reenableinheritance.png).

1. Selecione a guia **Conteúdo** no painel esquerdo.
1. Arraste e solte o conteúdo do canal da Web gerado automaticamente nos painéis existentes no modelo da Web usando a árvore de conteúdo. Esta é a lista de componentes que precisam ser reorganizados:

   * Componente Detalhes da Lista para o painel Detalhes da Lista
   * Componente Detalhes do cliente para o painel Detalhes do cliente
   * Componente Sumário da Lista para o painel Sumário da Lista
   * Componente Sumário de Encargos para o painel Sumário de Encargos
   * Fragmento de layout (tabela) para o painel Chamadas discriminadas

   ![Árvore de conteúdo da Web](assets/ic_web_content_tree_new.png)

1. Repita as etapas 13 a 18 de [Criar comunicação interativa para o canal da Web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) para inserir os hiperlinks **Pagar agora** e **Assinar** no canal da Web da comunicação interativa.
