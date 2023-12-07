---
title: "Tutorial: Criar a comunicação interativa"
description: Criar uma comunicação interativa usando todos os elementos
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Tutorial: Criar a comunicação interativa {#tutorial-create-interactive-communication}

![09-estilo-seu-formulário-adaptável-pequeno](assets/09-style-your-adaptive-form-small.png)

Este tutorial é uma etapa da [Criar a primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

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

**Modelo de dados do formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Fragmentos de layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Imagens:** PayNow e ValueAddedServices

1. Faça logon na instância de autor do AEM e acesse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecionar **Criar** e selecione **Comunicação interativa**. A variável **Criar comunicação interativa** será exibido.
1. Especificar **create_first_ic** no **Título** e a variável **Nome** campo. Selecionar **FDM_Create_First_IC** como o Modelo de dados do formulário e selecione **Próxima**.
1. No **Canais** assistente:

   1. Especificar **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**. Certifique-se de que o **Usar impressão como principal no canal da Web** não está marcada.

   1. Especificar **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Selecionar**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecionar **Editar** para abrir a Comunicação interativa no painel direito.
1. Vá para a **Assets** e aplique o filtro para exibir somente os fragmentos do documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento nas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Fatura |
   | customer_details_first_ic | DetalhesDoCliente |
   | bill_summary_first_ic | Resumo da fatura |
   | summary_charge_first_interative_communication | Encargos |

   ![Fragmentos de documento para Comunicações interativas](assets/create_first_ic_doc_fragments_new.png)

1. Selecionar **Gráficos** área de destino e selecione **+** para adicionar um **Gráfico** componente.
1. Selecione o componente de Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecionar **Pizza** do **Tipo de gráfico** lista suspensa.
   1. Selecione o **calltype** propriedade do **chamadas** tipo de objeto de modelo de dados no **Eixo X** seção. Selecionar ![done_icon](assets/done_icon.png).
   1. Selecionar **Frequência** do **Função** lista suspensa.
   1. Selecione o **calltype** propriedade do **chamadas** tipo de objeto de modelo de dados no **Eixo Y** seção. Selecionar ![done_icon](assets/done_icon.png).
   1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Vá para a **Assets** e aplique o filtro para exibir somente os fragmentos de layout no painel esquerdo. Arraste e solte a variável **table_lf** fragmento de layout à **Chamadas discriminadas** área de destino.
1. Selecione o campo de texto no **Data** e selecione ![configure_icon](assets/configure_icon.png) (Configurar).
1. Selecionar **Objeto de modelo de dados** do **Tipo de vínculo** e selecione **chamadas** > **calldate**. Selecionar ![done_icon](assets/done_icon.png) duas vezes para salvar as propriedades.

   Da mesma forma, crie uma vinculação com **calltime**, **callnumber**, **callduration**, e **encargos de chamada** para campos de texto no **Hora**, **Número**, **Duração**, e **Encargos** respectivamente.

1. Selecionar **PayNow** área de destino e selecione **+** para adicionar um **Imagem** componente.
1. Selecione o componente de Imagem e ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especificar **PayNow** como o nome da imagem na variável **Nome** campo.
   1. Selecionar **Carregar**, selecione a imagem salva no sistema de arquivos local e selecione **Abertura**.
   1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Repita as etapas 13 e 14 para adicionar **ValueAddedServices** imagem para a **ValueAddedServices** área de destino.

### Criar comunicação interativa para o canal da Web {#create-interactive-communication-for-web-channel}

Esta é a lista de recursos que já foram criados neste tutorial e são necessários ao criar a Comunicação interativa para o canal da Web:

**Modelo da Web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modelo de dados do formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Imagens:** PayNowWeb e ValueAddedServicesWeb

1. Faça logon na instância de autor do AEM e acesse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecionar **Criar** e selecione **Comunicação interativa**. A variável **Criar comunicação interativa** será exibido.
1. Especificar **create_first_ic** no **Título** e a variável **Nome** campo. Selecionar **FDM_Create_First_IC** como o Modelo de dados do formulário e selecione **Próxima**.
1. No **Canais** assistente:

   1. Especificar **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**. Certifique-se de que o **Usar impressão como principal no canal da Web** não está marcada.

   1. Especificar **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Selecionar**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecionar **Editar** para abrir a Comunicação interativa no painel direito.
1. Selecione o **Canais** no painel esquerdo e selecione **Web**.
1. Vá para a **Assets** e aplique o filtro para exibir somente os fragmentos do documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento nas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Fatura |
   | customer_details_first_ic | DetalhesDoCliente |
   | bill_summary_first_ic | Resumo da fatura |
   | summary_charge_first_interative_communication | Encargos |

1. Selecionar **Resumo de Encargos** área de destino e selecione **+** para adicionar um **Gráfico** componente.
1. Selecione o componente de Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecionar **Pizza** do **Tipo de gráfico** lista suspensa.

   1. Selecione o **calltype** propriedade do **chamadas** tipo de objeto de modelo de dados no **Eixo X** seção. Selecionar ![done_icon](assets/done_icon.png).

   1. Selecionar **Frequência** do **Função** lista suspensa.

   1. Selecione o **calltype** propriedade do **chamadas** tipo de objeto de modelo de dados no **Eixo Y** seção. Selecionar ![done_icon](assets/done_icon.png).

   1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Selecione o **Fontes de dados** no painel esquerdo e arraste e solte a guia **chamadas** objeto de modelo de dados para o **Chamadas discriminadas** área de destino. Todas as propriedades na **chamadas** objetos do modelo de dados são exibidos como colunas da tabela na **Chamadas discriminadas** área de destino no painel direito.

   Com base no caso de uso, você exige as colunas Data da chamada, Hora da chamada, Número da chamada, Duração da chamada e Encargos da chamada na tabela.

   ![Tabela para comunicação interativa](assets/table_ic_web_new.png)

1. Selecionar **Mobilenum** cabeçalho de coluna da tabela e selecione **Mais opções** > **Excluir coluna**. Da mesma forma, exclua a variável **Calltype** coluna.
1. Selecione o **Calldate** cabeçalho de coluna da tabela e selecione ![editar](assets/edit.png) (Editar) para renomear o texto para **Data da chamada**. Da mesma forma, renomeie outros cabeçalhos de coluna na tabela.
1. Com base no caso de uso, insira uma **Pagar agora** na Comunicação interativa que fornece ao usuário uma opção para fazer o pagamento clicando no botão. Execute as seguintes etapas para inserir o botão:

   1. Selecionar **Pagar agora** área de destino e selecione **+** para adicionar um **Texto** componente.

   1. Selecione o componente de texto e selecione ![editar](assets/edit.png) (Editar).
   1. Renomear o texto para **Pagar agora**.
   1. Selecione o texto e o ícone de Hiperlink.
   1. Especifique o URL de pagamento na **Caminho** campo.
   1. Selecionar **Nova guia** de **Target** lista suspensa.

   1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades do hiperlink.

1. Selecionar **Estilo** na lista suspensa ao lado da guia **Visualizar** opção.

   ![Selecionar modo de Estilo para Comunicação Interativa](assets/select_style_ic_web_new.png)

1. Estilize o texto do hiperlink para exibi-lo como um botão na Comunicação interativa usando as seguintes etapas:

   1. Selecione o componente de texto e selecione ![editar](assets/edit.png) (Editar).
   1. No **Borda** seção, especificar **1,5px** as **Largura da Borda**, selecione **Sólido** as **Estilo da Borda** e especifique **46px** as **Raio da Borda**.

   1. Selecione Vermelho como a cor de fundo do botão **Histórico** seção.
   1. No **Margem** campo para **Dimension e Posição** , selecione a **Editar simultaneamente** e defina o **Direita** margem como **450px**. Os campos Superior, Inferior e Esquerdo são definidos como em branco.

   ![Inserir hiperlink na comunicação interativa](assets/ic_web_hyperlink_new.png)

1. Selecionar **Pagar agora** área de destino e selecione **+** para adicionar um **Imagem** componente.
1. Selecione o componente de Imagem e ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especificar **PayNow** como o nome da imagem na variável **Nome** campo.

   1. Selecionar **Carregar**, selecione o **PayNowWeb** imagem salva no sistema de arquivos local e selecione **Abertura**.

   1. Selecionar ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Com base no caso de uso, insira uma **Assinar** na Comunicação interativa que fornece ao usuário uma opção para assinar os serviços de valor agregado clicando no botão.

   Repita as etapas 13 - 17 para adicionar um **Assinar** botão para a **Serviços de valor agregado** área de destino e adicione a **ValueAddedServicesWeb** imagem.

## Criar comunicações interativas para impressão e Web com sincronização automática {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Você também pode criar uma Comunicação interativa permitindo a sincronização automática entre canais de impressão e da Web. Para habilitar a sincronização automática, selecione a opção Print as master ao criar a comunicação interativa. Selecionar a opção Imprimir como mestre garante que o conteúdo, a herança e a associação de dados do canal da Web sejam derivados do canal de impressão. Também garante que as alterações feitas no canal Print sejam refletidas no canal Web.

Execute as seguintes etapas para derivar o conteúdo do canal da Web usando o Canal de impressão:

1. Faça logon na instância de autor do AEM e acesse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecionar **Criar** e selecione **Comunicação interativa**. A variável **Criar comunicação interativa** será exibido.
1. Especificar **create_first_ic** no **Título** e a variável **Nome** campo. Selecionar **FDM_Create_First_IC** como o Modelo de dados do formulário e selecione **Próxima**.
1. No **Canais** assistente:

   1. Especificar **create_first_ic_print_template** como o Modelo de impressão e selecione **Selecionar**.

   1. Selecione o **Usar impressão como principal no canal da Web** caixa de seleção
   1. Especificar **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo da Web e selecione **Selecionar**.

   1. Selecione **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Selecionar **Editar** para abrir a Comunicação interativa no painel direito.
1. Execute as etapas 6 a 15 de [Criar comunicação interativa para o canal de impressão](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) seção.
1. Selecione o **Canais** no painel esquerdo e selecione **Web** para gerar conteúdo automaticamente para o canal da Web a partir do canal de impressão.
1. Como a variável **Usar impressão como principal no canal da Web** estiver marcada na etapa 4, o conteúdo e as associações serão gerados automaticamente para o canal da Web a partir do canal de impressão.

   O conteúdo do canal de impressão é inserido abaixo do conteúdo do modelo de canal da Web. Para modificar o conteúdo do canal da Web que foi gerado automaticamente no canal de impressão, você pode cancelar a herança de qualquer área de destino.

   Passe o mouse sobre a área de destino relevante no canal da Web e selecione ![cancelinheritance](assets/cancelinheritance.png) (Cancelar herança) e no **Cancelar herança** , selecione **Sim**.

   ![Cancelar herança](assets/cancel_inheritance_web_channel_new.png)

   Se você cancelou a herança de um componente, é possível reativá-lo. Para reativar a herança, passe o mouse sobre o limite da área de destino relevante, que inclui o componente, e selecione ![reenableinheritance](assets/reenableinheritance.png).

1. Selecione o **Conteúdo** no painel esquerdo.
1. Arraste e solte o conteúdo do canal da Web gerado automaticamente nos painéis existentes no modelo da Web usando a árvore de conteúdo. Esta é a lista de componentes que precisam ser reorganizados:

   * Componente Detalhes da Lista para o painel Detalhes da Lista
   * Componente Detalhes do cliente para o painel Detalhes do cliente
   * Componente Sumário da Lista para o painel Sumário da Lista
   * Componente Sumário de Encargos para o painel Sumário de Encargos
   * Fragmento de layout (tabela) para o painel Chamadas discriminadas

   ![Árvore de conteúdo da Web](assets/ic_web_content_tree_new.png)

1. Repita as etapas 13 a 18 de [Criar comunicação interativa para o canal da Web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) para inserir o **Pagar agora** e **Assinar** hiperlinks no canal da Web da Comunicação interativa.
