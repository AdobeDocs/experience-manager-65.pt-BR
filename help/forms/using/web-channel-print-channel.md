---
title: Imprimir canal e canal da Web
seo-title: Imprimir canal e canal da Web
description: Importação de modelos de canais de impressão e criação e habilitação de modelos de canais da Web
seo-description: Importação de modelos de canais de impressão e criação e habilitação de modelos de canais da Web
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Imprimir canal e canal da Web{#print-channel-and-web-channel}

As Comunicações interativas podem ser fornecidas por meio de dois canais: impressão e Web. O canal impresso é usado para criar PDFs e comunicações em papel, como uma carta impressa como lembrete do pagamento de prêmio de seguro, enquanto o canal da Web é usado para fornecer experiências online, como uma declaração de cartão de crédito em um site.

Os autores do Interative Communication podem reutilizar ativos como fragmentos de documento e imagens para criar versões impressas e da Web do Interative Communication.

Um dos pré-requisitos para [Criar uma comunicação](../../forms/using/create-interactive-communication.md) interativa é ter os modelos para impressão e/ou canal da Web disponíveis no servidor. Enquanto os autores de modelo criam o modelo de canal da Web no próprio AEM, o modelo de canal de impressão XDP é criado no Adobe Forms Designer e carregado no servidor.

## Print channel {#printchannel}

O canal de impressão de uma comunicação interativa usa o modelo de formulário XFA, XDP. Um XDP foi projetado no Adobe Forms Designer. Para obter mais informações sobre como criar modelos de canais de impressão, consulte Design [de](../../forms/using/layout-design-details.md)layout. Para usar um modelo de canal de impressão em sua Comunicação interativa, é necessário carregar o modelo no servidor AEM Forms.

### Carregar modelo de canal de impressão do Interative Communication {#upload-interactive-communication-print-channel-template}

Para carregar o modelo, é necessário ser um membro do grupo de usuários de formulários. Use as seguintes etapas para fazer upload do modelo de canal de impressão (XDP) para a AEM Forms:

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Toque em **[!UICONTROL Criar]** > Upload **[!UICONTROL de arquivo]**.

   Navegue e selecione o modelo de canal de impressão apropriado (XDP) e toque em **[!UICONTROL Abrir]**.

## Web channel {#web-channel}

Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Para permitir que outros usuários criem modelos da Web, é necessário conceder direitos a eles. Para obter mais informações, consulte Administração [de direitos de acesso, grupo e](/help/sites-administering/user-group-ac-admin.md)usuário.

### Criação de modelo de Canal da Web {#authoring-web-channel-template}

Para criar um modelo de canal da Web, é necessário primeiro criar uma pasta Modelo. Depois de criar um modelo da Web dentro de uma pasta de modelo, é necessário ativar o modelo para permitir que os usuários criem um canal da Web de uma Comunicação Interativa com base no modelo.

Para criar um modelo de canal da Web Complete as etapas a seguir:

1. Crie uma pasta de modelo para manter seus modelos da Web de comunicação interativa, se você ainda não tiver um. Para obter mais informações, consulte Pastas de modelo em Modelos de [página - Editável](/help/sites-developing/page-templates-editable.md).

   1. Toque em **[!UICONTROL Ferramentas]** ![ferramentas](assets/tools.png) > Navegador **[!UICONTROL de configuração]**.
      * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
   1. Na página Navegador de configuração, toque em **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração, especifique um título para a pasta, marque Modelos **** editáveis e toque em **[!UICONTROL Criar]**.

      A pasta é criada e listada na página Navegador de configuração.

1. Navegue até a pasta de modelo apropriada e crie um modelo da Web.

   1. Navegue até a pasta de modelo apropriada selecionando **[!UICONTROL Ferramentas]** > **[!UICONTROL Modelos]** > **`[Folder]`**.
   1. Toque em **[!UICONTROL Criar]**.
   1. Selecione Comunicação **[!UICONTROL interativa - Canal]** da Web e toque em **[!UICONTROL Próximo]**.
   1. Insira um título e uma descrição do Modelo e toque em **[!UICONTROL Criar]**.

      O modelo é criado e uma caixa de diálogo é exibida.

   1. Toque em **[!UICONTROL Abrir]** para abrir o modelo criado no Editor de modelos.

      O Editor de modelos é exibido.

      ![webcaneltemplate](assets/webchanneltemplate.png)

      Ao criar ou editar um modelo, há vários aspectos que um autor de modelo pode definir. Criar ou editar um modelo é semelhante à criação de página. Para obter mais informações, consulte Edição de modelos - autores de modelos em [Criação de modelos](/help/sites-authoring/templates.md)de página.

1. Para permitir o uso deste modelo para a criação da Comunicação Interativa, ative o modelo.

   1. Toque em **[!UICONTROL Ferramentas]** ![ferramentas](assets/tools.png) > **[!UICONTROL Modelos]**.
   1. Navegue até o modelo apropriado, selecione-o e toque em **[!UICONTROL Ativar]** e, na mensagem de alerta, toque em **[!UICONTROL Ativar]**.

      O modelo está ativado e seu status é exibido como Ativado. Agora, você pode continuar criando uma Comunicação interativa onde você pode usar o modelo de canal da Web recém-criado.

### Imprimir canal como principal para canal da Web {#print-channel-as-master-for-web-channel}

Ao criar uma comunicação interativa, os autores podem selecionar essa opção para criar o canal da Web em sincronia com o canal de impressão. O uso do canal de impressão como principal para o canal da Web garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal de impressão e as alterações feitas no canal de impressão possam ser refletidas no canal da Web. No entanto, os autores de Comunicações interativas podem interromper a herança de componentes específicos no canal da Web, conforme necessário.

![Imprimir canal como canal principal](assets/create_ic_print_master_new.png) ![da Web com canal impresso principal](assets/create_ic_print_master_web_new.png)

