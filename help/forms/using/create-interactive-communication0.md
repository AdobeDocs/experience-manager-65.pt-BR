---
title: '"Tutorial: Criar comunicação interativa "'
seo-title: Criar uma comunicação interativa para impressão e Web
description: Criar uma comunicação interativa usando todos os blocos de construção
seo-description: Criar uma comunicação interativa usando todos os blocos de construção
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Comunicação interativa
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# Tutorial: Criar comunicação interativa {#tutorial-create-interactive-communication}

![Estilo 09-o-forma adaptável-pequena](assets/09-style-your-adaptive-form-small.png)

Este tutorial é uma etapa da série [Create your first Interative Communication](/help/forms/using/create-your-first-interactive-communication.md). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Depois de criar todos os blocos de construção, como o modelo de dados de formulário, fragmentos de documento, modelos e temas para a versão da Web, você pode começar a criar uma Comunicação interativa.

As Comunicações interativas podem ser entregues por meio de dois canais: Imprimir e Web. Você também pode criar um canal de Comunicação interativa com impressão como o principal. A opção Imprimir como principal para canal da Web garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal Imprimir. Também garante que as alterações feitas no canal de Impressão sejam sincronizadas no canal da Web. Os autores de Comunicação interativa, no entanto, têm permissão para quebrar a herança de componentes específicos no canal da Web.

Este tutorial o orienta pelas etapas para criar comunicações interativas para canais de Impressão e Web. Ao final deste tutorial, você poderá:

* Criar comunicação interativa para o canal de impressão
* Criar comunicação interativa para o canal da Web
* Crie Comunicações Interativas da Web e Imprimir como Principal

## Criar Comunicações Interativas para Impressão e Web sem sincronização {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Criar comunicação interativa para o canal de impressão {#create-interactive-communication-for-print-channel}

Esta é a lista de recursos que já foram criados neste tutorial e são necessários ao criar a Comunicação interativa para o canal Imprimir:

**Modelo de impressão:** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modelo de dados de formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Fragmentos de layout:** [table_lf](../../forms/using/create-templates-print-web.md)

**Imagens:** PayNow e ValueAddedServices

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque em **Criar** e selecione **Comunicação interativa**. O assistente **Criar comunicação interativa** é exibido.
1. Especifique **create_first_ic** no campo **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e toque em **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o modelo Imprimir e toque em **Selecionar**. Certifique-se de que a caixa de seleção **Use Print as Principal for Web Channel** não esteja marcada.

   1. Especifique **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo Web e toque em **Selecionar**.

   1. Toque em **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Toque em **Editar** para abrir a Comunicação interativa no painel direito.
1. Vá para a guia **Assets** e aplique o filtro para exibir apenas os fragmentos de documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento em suas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Lista |
   | customer_details_first_ic | Detalhes do cliente |
   | bill_summary_first_ic | Resumo da Lista |
   | summary_charge_first_interative_communication | Encargos |

   ![Fragmentos de documento para Comunicações interativas](assets/create_first_ic_doc_fragments_new.png)

1. Toque em **Charts** área de destino e toque em **+** para adicionar um componente **Chart**.
1. Toque no componente Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecione **Pizza** na lista suspensa **Tipo de Gráfico**.
   1. Selecione a propriedade **calltype** do tipo de objeto **calls** do modelo de dados na seção **X-axis**. Toque em ![done_icon](assets/done_icon.png).
   1. Selecione **Frequency** na lista suspensa **Function**.
   1. Selecione a propriedade **calltype** do tipo de objeto **calls** do modelo de dados na seção **Y-axis**. Toque em ![done_icon](assets/done_icon.png).
   1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Vá para a guia **Assets** e aplique o filtro para exibir apenas os fragmentos de layout no painel esquerdo. Arraste e solte o fragmento de layout **table_lf** na área de destino **Chamadas discriminadas**.
1. Selecione o Campo de texto na coluna **Date** e toque em ![configure_icon](assets/configure_icon.png) (Configurar).
1. Selecione **Objeto do Modelo de Dados** na lista suspensa **Tipo de Vínculo** e selecione **chamadas** > **calldate**. Toque em ![done_icon](assets/done_icon.png) duas vezes para salvar as propriedades.

   Da mesma forma, crie a vinculação com **calltime**, **callnumber**, **callduration** e **callcharge** para campos de texto no **Time**, **Number**, &lt;a1 2/>Colunas Duration **e** Charges **, respectivamente.**

1. Toque na área de destino **PayNow** e toque em **+** para adicionar um componente **Image**.
1. Toque no componente Imagem e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especifique **PayNow** como o nome da imagem no campo **Nome**.
   1. Toque em **Fazer upload**, selecione a imagem salva no sistema de arquivos local e toque em **Abrir**.
   1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Repita as etapas 13 e 14 para adicionar a imagem **ValueAddedServices** à área de destino **ValueAddedServices**.

### Criar comunicação interativa para o canal Web {#create-interactive-communication-for-web-channel}

Esta é a lista de recursos que já foram criados neste tutorial e são necessários ao criar a Comunicação interativa para o canal da Web:

**Modelo da Web:** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modelo de dados de formulário:** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragmentos do documento:** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charge_first_ic](../../forms/using/create-document-fragments.md)

**Imagens:** PayNowWeb e ValueAddedServicesWeb

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque em **Criar** e selecione **Comunicação interativa**. O assistente **Criar comunicação interativa** é exibido.
1. Especifique **create_first_ic** no campo **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e toque em **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o modelo Imprimir e toque em **Selecionar**. Certifique-se de que a caixa de seleção **Use Print as Principal for Web Channel** não esteja marcada.

   1. Especifique **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo Web e toque em **Selecionar**.

   1. Toque em **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Toque em **Editar** para abrir a Comunicação interativa no painel direito.
1. Toque na guia **Channels** no painel esquerdo e toque em **Web**.
1. Vá para a guia **Assets** e aplique o filtro para exibir apenas os fragmentos de documento no painel esquerdo.
1. Arraste e solte os seguintes fragmentos de documento em suas áreas de destino na Comunicação interativa:

   | Fragmento do documento | Área de destino |
   |---|---|
   | bill_details_first_ic | Detalhes da Lista |
   | customer_details_first_ic | Detalhes do cliente |
   | bill_summary_first_ic | Resumo da Lista |
   | summary_charge_first_interative_communication | Encargos |

1. Toque em **Resumo das Encargos** na área de destino e toque em **+** para adicionar um componente **Gráfico**.
1. Toque no componente Gráfico e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades do gráfico são exibidas no painel esquerdo:

   1. Especifique um nome para o gráfico.
   1. Selecione **Pizza** na lista suspensa **Tipo de Gráfico**.

   1. Selecione a propriedade **calltype** do tipo de objeto **calls** do modelo de dados na seção **X-axis**. Toque em ![done_icon](assets/done_icon.png).

   1. Selecione **Frequency** na lista suspensa **Function**.

   1. Selecione a propriedade **calltype** do tipo de objeto **calls** do modelo de dados na seção **Y-axis**. Toque em ![done_icon](assets/done_icon.png).

   1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

1. Selecione a guia **Fontes de Dados** no painel esquerdo e arraste e solte o objeto de modelo de dados **chamadas** para a área de destino **Chamadas Discriminadas**. Todas as propriedades no objeto de modelo de dados **calls** são exibidas como colunas de tabela na área de destino **Chamadas Discriminadas** no painel direito.

   Com base no caso de uso, você precisa das colunas Data da chamada, Hora da chamada, Número da chamada, Duração da chamada e Encargos de chamada na tabela.

   ![Tabela para comunicação interativa](assets/table_ic_web_new.png)

1. Selecione o cabeçalho da coluna da tabela **Mobilenum** e selecione **Mais opções** > **Excluir coluna**. Da mesma forma, exclua a coluna **Calltype**.
1. Selecione o cabeçalho da coluna da tabela **Calldate** e toque em ![editar](assets/edit.png) (Editar) para renomear o texto para **Data da Chamada**. Da mesma forma, renomeie outros cabeçalhos de coluna na tabela.
1. Com base no caso de uso, insira um botão **Pagar Agora** na Comunicação Interativa que fornece ao usuário uma opção para fazer o pagamento clicando no botão . Execute as seguintes etapas para inserir o botão:

   1. Toque na área de destino **Pagar Agora** e toque em **+** para adicionar um componente **Texto**.

   1. Toque no componente de texto e toque em ![editar](assets/edit.png) (Editar).
   1. Renomeie o texto para **Pagar Agora**.
   1. Selecione o texto e toque no ícone Hiperlink.
   1. Especifique o URL do pagamento no campo **Path**.
   1. Selecione **New Tab** na lista suspensa **Target**.

   1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades de hiperlink.

1. Selecione **Style** na lista suspensa ao lado da opção **Preview**.

   ![Selecionar modo Estilo para Comunicação Interativa](assets/select_style_ic_web_new.png)

1. Estilo do texto do hiperlink para exibi-lo como um botão na Comunicação interativa usando as seguintes etapas:

   1. Toque no componente de texto e selecione ![edit](assets/edit.png) (Editar).
   1. Na seção **Border**, especifique **1.5px** como **Largura da Borda**, selecione **Sólido** como **Estilo da Borda** e especifique **46px** como 12/>Raio da borda **.**

   1. Selecione Vermelho como a cor de plano de fundo do botão na seção **Plano de fundo**.
   1. No campo **Margin** para a seção **Dimension &amp; Position**, toque no ícone **Editar simultaneamente** e defina a margem **Direita** como **450px**. Os campos Superior, Inferior e Esquerdo são definidos como em branco.

   ![Inserir hiperlink na Comunicação Interativa](assets/ic_web_hyperlink_new.png)

1. Toque na área de destino **Pagar Agora** e toque em **+** para adicionar um componente **Image**.
1. Toque no componente Imagem e selecione ![configure_icon](assets/configure_icon.png) (Configurar). As propriedades da imagem são exibidas no painel esquerdo:

   1. Especifique **PayNow** como o nome da imagem no campo **Nome**.

   1. Toque em **Upload**, selecione a imagem **PayNowWeb** salva no sistema de arquivos local e toque em **Abrir**.

   1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades da imagem.

1. Com base no caso de uso, insira um botão **Subscribe** na Comunicação interativa que fornece ao usuário uma opção para assinar os serviços de valor agregado clicando no botão .

   Repita as etapas 13 - 17 para adicionar um botão **Subscribe** à área de destino **Value Added Services** e adicionar a imagem **ValueAddedServicesWeb**.

## Criar Comunicações interativas para impressão e Web com sincronização automática {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Você também pode criar uma Comunicação interativa permitindo a sincronização automática entre os canais Imprimir e Web. Para ativar a sincronização automática, selecione a opção Imprimir como principal ao criar a Comunicação interativa. Selecionar a opção Imprimir como principal garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal Imprimir. Também garante que as alterações feitas no canal de Impressão sejam refletidas no canal da Web.

Execute as seguintes etapas para derivar o conteúdo do canal da Web usando o Canal de impressão:

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque em **Criar** e selecione **Comunicação interativa**. O assistente **Criar comunicação interativa** é exibido.
1. Especifique **create_first_ic** no campo **Title** e no campo **Name**. Selecione **FDM_Create_First_IC** como o Modelo de dados de formulário e toque em **Próximo**.
1. No assistente **Canais**:

   1. Especifique **create_first_ic_print_template** como o modelo Imprimir e toque em **Selecionar**.

   1. Marque a caixa de seleção **Use Print as Principal for Web Channel**.
   1. Especifique **Create_First_IC_templates** pasta > **Create_First_IC_Web_Template** como o modelo Web e toque em **Selecionar**.

   1. Toque em **Criar**.

   Uma mensagem de confirmação é exibida informando que a Comunicação interativa foi criada com êxito.

1. Toque em **Editar** para abrir a Comunicação interativa no painel direito.
1. Execute as etapas 6 - 15 da seção [Criar comunicação interativa para o canal de impressão](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Toque na guia **Channels** no painel esquerdo e toque em **Web** para gerar automaticamente o conteúdo para o canal Web a partir do canal de Impressão.
1. Como a caixa de seleção **Use Print as Principal for Web Channel** é selecionada na etapa 4, o conteúdo e os vínculos são gerados automaticamente para o canal da Web do canal de Impressão.

   O conteúdo do canal de impressão é inserido abaixo do conteúdo do modelo de canal da Web. Para modificar o conteúdo do canal da Web que foi gerado automaticamente pelo canal de Impressão, você pode cancelar a herança para qualquer área de destino.

   Passe o mouse sobre a área de destino relevante no canal da Web e selecione ![cancelar herança](assets/cancelinheritance.png) (Cancelar herança) e, na caixa de diálogo **Cancelar herança**, toque em **Sim**.

   ![Cancelar herança](assets/cancel_inheritance_web_channel_new.png)

   Se você cancelou a herança de um componente, é possível reativá-la. Para reativar a herança, passe o mouse sobre o limite da área de destino relevante, que inclui o componente, e toque em ![reabilitar herança](assets/reenableinheritance.png).

1. Selecione a guia **Content** no painel esquerdo.
1. Arraste e solte o conteúdo do canal da Web gerado automaticamente nos painéis existentes no modelo da Web usando a árvore de conteúdo. Esta é a lista de componentes que precisam ser reorganizados:

   * Componente Detalhes da Lista para o painel Detalhes da Lista
   * Componente Detalhes do cliente para o painel Detalhes do cliente
   * Componente Resumo da Lista para o painel Resumo da Lista
   * Resumo do componente Encargos para o painel Resumo de Encargos
   * Fragmento de layout (tabela) para o painel Chamadas discriminadas

   ![Árvore de conteúdo da Web](assets/ic_web_content_tree_new.png)

1. Repita as etapas 13 - 18 de [Criar comunicação interativa para canal Web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) para inserir os hiperlinks **Pagar agora** e **Assinar** no canal Web da Comunicação interativa.

