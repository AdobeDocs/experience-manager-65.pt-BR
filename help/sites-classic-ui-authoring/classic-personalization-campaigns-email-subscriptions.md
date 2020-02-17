---
title: Gerenciamento de assinaturas
seo-title: Gerenciamento de assinaturas
description: Os usuários podem ser solicitados a se inscrever em listas de distribuição do Provedor de serviços de email com a ajuda do componente Formulário usado em uma página da web do AEM. Para preparar uma página do AEM com um formulário de inscrição para assinatura de listas de distribuição do seu serviço de email, você deve aplicar a configuração de serviço correspondente à página do AEM que o possível assinante visitará.
seo-description: Os usuários podem ser solicitados a se inscrever em listas de distribuição do Provedor de serviços de email com a ajuda do componente Formulário usado em uma página da web do AEM. Para preparar uma página do AEM com um formulário de inscrição para assinatura de listas de distribuição do seu serviço de email, você deve aplicar a configuração de serviço correspondente à página do AEM que o possível assinante visitará.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gerenciamento de assinaturas{#managing-subscriptions}

>[!NOTE]
>
>A Adobe não pretende aprimorar ainda mais esse recurso (Gerenciando Clientes Potenciais e Listas).
>A recomendação é aproveitar o [Adobe Campaign e sua integração](/help/sites-administering/campaign.md)com o AEM.

Users can be asked to subscribe to **Email Service Provider&#39;s** mailing lists with the help of the **Form** component used on an AEM web page. Para preparar uma página do AEM com um formulário de inscrição para assinatura de listas de distribuição do seu serviço de email, você deve aplicar a configuração de serviço correspondente à página do AEM que o possível assinante visitará.

## Aplicação da configuração do serviço de email a uma página {#applying-email-service-configuration-to-a-page}

Para configurar uma página do AEM:

1. Navegue até a guia **Sites**.
1. Selecione a página que precisa ser configurada para o serviço. Right-click the page and select **Properties**.

1. Select **Cloud Services** then **Add Service**. Selecione uma configuração na lista de configurações disponíveis.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Clique em **OK**.

## Criação de um formulário de inscrição em uma página do AEM para assinar/cancelar a assinatura de listas {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Para criar um formulário de inscrição e configurá-lo para assinaturas de listas de distribuição do Provedor de serviços de email:

1. Abra a página do AEM que o usuário visitará.
1. Aplique a configuração do Provedor de serviços de email à página.

1. Adicione um componente **Formulário** à página arrastando esse componente do sidekick. Se o componente não estiver disponível, alterne para o modo de design e ative o grupo **Formulário**.
1. Click **Edit** in the **Start of Form** bar and navigate to the **Advanced** tab.
1. In the **Form** drop-down menu, select **E-mail Service: Create Subscriber** and add to list.
1. At the bottom of the dialog box, open the **Action Configuration** drop-down, which allows you to select one or more subscription lists.
1. Na lista **Selecionar,** selecione a lista na qual você deseja que os usuários se inscrevam. Você pode adicionar várias listas usando o botão de adição (**Adicionar item**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >Sua caixa de diálogo pode ser diferente, dependendo do provedor de serviços de email.

1. Na guia **Formulário**, selecione a página de agradecimento que você deseja que os usuários acessem depois de enviarem o formulário (se ficar em branco, o formulário será exibido novamente após o envio). Clique em **OK**. Um componente de **ID de email** aparece no Formulário, permitindo criar um formulário em que os usuários podem enviar seus endereços de email para assinar ou cancelar a assinatura de uma lista de emails.
1. Adicione o componente de botão **Enviar** da seção **Formulário** no sidekick.

   O formulário está pronto. Publique a página configurada nas etapas acima junto com a página de **agradecimento** na instância de publicação. Qualquer assinante em potencial que visitar a página poderá preencher o formulário e assinar a lista fornecida na configuração.

   >[!NOTE]
   >
   >Para que a assinatura do formulário funcione corretamente, [as chaves de criptografia do autor precisam ser exportadas e importadas na instância de publicação](#exporting-keys-from-author-and-importing-on-publish).

## Exportação de chaves do autor e importação na publicação {#exporting-keys-from-author-and-importing-on-publish}

Para que o processo de assinatura ou cancelamento de assinatura do serviço de email funcione com o uso do formulário de inscrição na instância de publicação, é necessário seguir estas etapas:

1. Na instância de autor, navegue até o Gerenciador de pacotes.
1. Crie um novo pacote. Set the filter as `/etc/key`.
1. Construa e faça o download do pacote.
1. Navegue até o Gerenciador de pacotes na instância de publicação e faça upload desse pacote.
1. Navegue até o console do osgi de Publicação e reinicie o pacote chamado **Adobe Granite Crypto Support**.

## Cancelamento da assinatura de usuários em listas {#unsubscribing-users-from-lists}

Para cancelar a assinatura de usuários em listas:

1. Abra as propriedades da página do AEM que tem o formulário de inscrição para cancelar a assinatura de um lead.
1. Aplique a configuração de serviço à página.
1. Crie um formulário de inscrição na página.
1. While configuring the component, select the action **E-mail Service**: **Unsubscribe user from list.**
1. No menu suspenso, selecione a lista apropriada da qual o usuário será removido ao cancelar a assinatura.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exportar as chaves do autor para publicar.

## Configurando emails de resposta automática para o serviço de email {#configuring-auto-responder-emails-for-email-service}

Para configurar um email de resposta automática para um assinante:

1. Abra as propriedades da página AEM que têm o formulário de inscrição para configurar o respondedor automático para um cliente potencial.
1. Aplique a configuração do ExactTarget à página.

1. Adicione um componente **Formulário** à página arrastando esse componente do sidekick. Se o componente não estiver disponível, alterne para o modo de design e ative o grupo **Formulário**.
1. Click **Edit** in the **Start of Form** bar and navigate to the **Advanced** tab.
1. In the **Form** drop-down menu, select **E-mail Service: Send auto responder email.**
1. **Selecione um email** (este é o email enviado como um email de resposta automática).

1. **Selecione Classificação** (esta classificação é usada para enviar o email).
1. Select the **Thank you** page (the page where users are directed to once they submit the form).

   In the **Form** tab, select the thank you page you want users to go to after they submit the form. (If left blank, the form redisplays upon submission.) Clique em **OK**.

1. Exportar as chaves do autor para publicar.
1. Adicione o componente de botão **Enviar** da seção **Formulário** no sidekick.

   O formulário de inscrição está pronto. Publique a página configurada nas etapas acima junto com a página de **agradecimento** na instância de publicação. Qualquer assinante em potencial que visitar a página poderá preencher o formulário e, ao enviá-lo, o visitante receberá um email de resposta automática na ID de email preenchida nesse formulário.

   >[!NOTE]
   >
   >Para que a assinatura do formulário de inscrição funcione corretamente, [as chaves de criptografia do autor precisam ser exportadas e importadas na instância de publicação](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)

