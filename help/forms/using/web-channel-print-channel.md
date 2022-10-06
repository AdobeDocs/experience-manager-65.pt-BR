---
title: Canal de impressão e canal da Web
seo-title: Print channel and web channel
description: Importação de modelos de canal de impressão e criação e habilitação de modelos de canal da Web
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Canal de impressão e canal da Web{#print-channel-and-web-channel}

As Comunicações interativas podem ser entregues por meio de dois canais: impressão e web. O canal de impressão é usado para criar PDF e comunicações em papel, como uma carta impressa como lembrete do pagamento do prêmio de seguro, enquanto o canal da Web é usado para fornecer experiências online, como uma declaração de cartão de crédito em um site.

Os autores da Comunicação interativa podem reutilizar ativos, como fragmentos de documento e imagens para criar versões impressas e da Web da Comunicação interativa.

Um dos pré-requisitos para [Criação de uma comunicação interativa](../../forms/using/create-interactive-communication.md) O deve ter os modelos para impressão e/ou canal da Web disponíveis no servidor. Enquanto os autores de modelo criam o modelo de canal da Web em si, o modelo de canal de impressão XDP é criado no Adobe Forms Designer e carregado no servidor.

## Canal de impressão {#printchannel}

Canal de impressão de uma Comunicação interativa usa o modelo de formulário XFA, XDP. Um XDP foi projetado no Adobe Forms Designer. Para obter mais informações sobre como criar modelos de canal de impressão, consulte [Design de layout](../../forms/using/layout-design-details.md). Para usar um modelo de canal de impressão em sua Comunicação interativa, é necessário fazer upload do modelo para o servidor do AEM Forms.

### Fazer upload do modelo de canal de impressão de Comunicação interativa {#upload-interactive-communication-print-channel-template}

Para carregar o modelo, você precisa ser um membro do grupo de usuários de formulários. Use as seguintes etapas para fazer upload do modelo de canal de impressão (XDP) no AEM Forms:

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. Toque **[!UICONTROL Criar]** > **[!UICONTROL Upload de arquivo]**.

   Navegue e selecione o modelo de canal de impressão apropriado (XDP) e toque em **[!UICONTROL Abrir]**.

## Canal da Web {#web-channel}

Autores e administradores de modelos podem criar, editar e ativar modelos da Web. Para permitir que outros usuários criem modelos da Web, você precisa conceder direitos a eles. Para obter mais informações, consulte [Administração de usuários, grupos e direitos de acesso](/help/sites-administering/user-group-ac-admin.md).

### Criação de modelo de canal web {#authoring-web-channel-template}

Para criar um template de canal da Web, primeiro crie uma pasta Template . Depois de criar um modelo da Web dentro de uma pasta de modelo, é necessário habilitar o modelo para permitir que os usuários do formulário criem um canal da Web de uma Comunicação interativa com base no modelo.

Para criar um template de canal da Web Complete as etapas a seguir:

1. Crie uma pasta Template para manter seus templates da Web de Comunicação interativa, se você ainda não tiver um. Para obter mais informações, consulte Pastas de modelo em [Modelos de página - Editável](/help/sites-developing/page-templates-editable.md).

   1. Toque **[!UICONTROL Ferramentas]** ![ferramentas](assets/tools.png) > **[!UICONTROL Navegador de configuração]**.
      * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.
   1. Na página Navegador de configuração, toque em **[!UICONTROL Criar]**.
   1. Na caixa de diálogo Criar configuração , especifique um título para a pasta e marque **[!UICONTROL Modelos editáveis]** e toque em **[!UICONTROL Criar]**.

      A Pasta é criada e listada na página Navegador de configuração.

1. Navegue até a pasta de modelo apropriada e crie um modelo da Web.

   1. Navegue até a pasta de modelo apropriada selecionando **[!UICONTROL Ferramentas]** > **[!UICONTROL Modelos]** > **`[Folder]`**.
   1. Toque **[!UICONTROL Criar]**.
   1. Selecionar **[!UICONTROL Comunicação interativa - Canal da Web]** e tocar **[!UICONTROL Próximo]**.
   1. Insira um título e uma descrição do Modelo e toque em **[!UICONTROL Criar]**.

      O modelo é criado e uma caixa de diálogo é exibida.

   1. Toque **[!UICONTROL Abrir]** para abrir o modelo criado no editor de modelo.

      O Editor de modelo é exibido.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Ao criar ou editar um modelo, há vários aspectos que um Autor do modelo pode definir. Criar ou editar um modelo é semelhante à criação de página. Para obter mais informações, consulte Editar modelos - Autores do modelo em [Criação de modelos de página](/help/sites-authoring/templates.md).

1. Para permitir o uso desse modelo para a criação da Comunicação interativa, ative o modelo .

   1. Toque **[!UICONTROL Ferramentas]** ![ferramentas](assets/tools.png) > **[!UICONTROL Modelos]**.
   1. Navegue até o modelo apropriado, selecione-o e toque em **[!UICONTROL Habilitar]** e na mensagem de alerta, toque em **[!UICONTROL Habilitar]**.

      O modelo é ativado e seu status é exibido como Ativado. Agora você pode continuar criando uma Comunicação interativa, onde pode usar o modelo de canal da Web recém-criado.

### Imprimir canal como principal para canal da Web {#print-channel-as-master-for-web-channel}

Ao criar uma comunicação interativa, os autores podem selecionar essa opção para criar o canal da Web em sincronia com o canal de impressão. Usar o canal de impressão como principal para o canal da Web garante que o conteúdo, a herança e o vínculo de dados do canal da Web sejam derivados do canal de impressão e as alterações feitas no canal de impressão possam ser refletidas no canal da Web. No entanto, os autores de Comunicação interativa podem quebrar a herança de componentes específicos no canal da Web, conforme necessário.

![Imprimir canal como principal](assets/create_ic_print_master_new.png) ![Canal da Web com canal de impressão principal](assets/create_ic_print_master_web_new.png)
