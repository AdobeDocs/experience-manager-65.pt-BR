---
title: Gerenciamento de assinaturas
description: Os usuários podem ser solicitados a assinar as listas de correspondência do provedor de serviços de email com a ajuda do componente de Formulário usado em uma página da Web AEM. Para preparar uma página AEM com um formulário de inscrição para inscrição nas listas de endereçamento do seu serviço de email, você deve aplicar a configuração de serviço correspondente à página AEM que o assinante potencial visitará.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: add05d22-3a11-49e9-a554-2315962552d5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# Gerenciamento de assinaturas{#managing-subscriptions}

>[!NOTE]
>
>O Adobe não planeja aprimorar ainda mais esse recurso (Gerenciamento de clientes em potencial e listas).
>A recomendação é usar [Adobe Campaign e sua integração com o AEM](/help/sites-administering/campaign.md).

Os usuários podem ser solicitados a assinar **do provedor de serviços de e-mail** listas de endereçamento com a ajuda do **Formulário** componente usado em uma página da Web AEM. Para preparar uma página AEM com um formulário de inscrição para inscrição nas listas de endereçamento do seu serviço de email, você deve aplicar a configuração de serviço correspondente à página AEM que o assinante potencial visitará.

## Aplicar a configuração do Serviço de email a uma página {#applying-email-service-configuration-to-a-page}

Para configurar uma página AEM:

1. Navegue até a **Sites** guia.
1. Selecione a página que precisa ser configurada para o serviço. Clique com o botão direito do mouse e selecione **Propriedades**.

1. Selecionar **Cloud Service** depois **Adicionar serviço**. Selecione uma configuração na lista de configurações disponíveis.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Clique em **OK**.

## Criação de um formulário de inscrição em uma página de AEM para inscrição/cancelamento de inscrição em listas {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Para criar um formulário de inscrição e configurá-lo para assinaturas das listas de endereçamento do provedor de serviços de email:

1. Abra a página do AEM que o usuário visitará.
1. Aplique a configuração do provedor de serviços de email à página.

1. Adicionar um **Formulário** para a página, arrastando o componente do sidekick. Se o componente não estiver disponível, alterne para o modo de design e ative **Formulário** grupo.
1. Clique em **Editar** no **Início do formulário** e navegue até a **Avançado** guia.
1. No **Formulário** selecione **Serviço de E-mail: Criar Assinante** e adicionar à lista.
1. Na parte inferior da caixa de diálogo, abra **Configuração de ação** , que permite selecionar uma ou mais listas de assinaturas.
1. No **Selecionar lista**, selecione a lista que deseja que os usuários assinem. É possível adicionar várias listas usando o botão de adição (**Adicionar item**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >Sua caixa de diálogo pode ser diferente dependendo do provedor de serviços de email.

1. No **Formulário** , selecione a página de agradecimento que você deseja que os usuários acessem após enviarem o formulário (Se permanecer em branco, o formulário será exibido novamente após o envio). Clique em **OK**. Um **ID do e-mail** aparece no Formulário, que permite criar um formulário em que os usuários podem enviar seus endereços de email para se inscreverem ou cancelar a inscrição de uma lista de endereçamento.
1. Adicione o **Enviar** componente de botão do **Formulário** seção no sidekick.

   O formulário está pronto. Publique a página configurada nas etapas acima, juntamente com o **obrigado** página para a instância de publicação. Qualquer assinante em potencial que visite a página pode preencher o formulário e assinar a lista fornecida na configuração.

   >[!NOTE]
   >
   >Para fazer com que a assinatura do formulário funcione corretamente, [as chaves de criptografia do autor precisam ser exportadas e importadas na instância de publicação](#exporting-keys-from-author-and-importing-on-publish).

## Exportação de chaves do autor e importação na publicação {#exporting-keys-from-author-and-importing-on-publish}

Para que a assinatura e o cancelamento de assinatura do serviço de e-mail funcionem por meio do formulário de inscrição na instância de publicação, é necessário seguir estas etapas:

1. Na instância do autor, navegue até o Gerenciador de pacotes.
1. Criar um pacote. Definir o filtro como `/etc/key`.
1. Crie e baixe o pacote.
1. Navegue até o Gerenciador de pacotes na instância de publicação e faça upload deste pacote.
1. Navegue até o console Publicar osgi e reinicie o pacote chamado **Suporte à criptografia do Adobe Granite**.

## Cancelamento de assinatura de usuários em listas {#unsubscribing-users-from-lists}

Para cancelar a inscrição de usuários nas listas:

1. Abra as propriedades da página AEM que tem o formulário de inscrição para cancelar a inscrição de um cliente potencial.
1. Aplicar a configuração do serviço à página.
1. Crie um formulário de inscrição na página.
1. Ao configurar o componente, selecione a ação **Serviço de e-mail**: **Cancelar inscrição do usuário na lista.**
1. No menu suspenso, selecione a lista apropriada da qual o usuário será removido ao cancelar a inscrição.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exporte as chaves do autor para a publicação.

## Configuração de emails de resposta automática para o Serviço de email {#configuring-auto-responder-emails-for-email-service}

Para configurar um email de resposta automática para um assinante:

1. Abra as propriedades da página AEM que têm o formulário de inscrição para configurar o respondente automático para um cliente potencial.
1. Aplicar a configuração ExactTarget à página.

1. Adicionar um **Formulário** para a página, arrastando o componente do sidekick. Se o componente não estiver disponível, alterne para o modo de design e ative a opção **Formulário** grupo.
1. Clique em **Editar** no **Início do formulário** e navegue até a **Avançado** guia.
1. No **Formulário** selecione **Serviço de e-mail: envia um e-mail de resposta automática.**
1. **Selecione um email** (esse é o email enviado como um email de resposta automática).

1. **Selecionar classificação** (essa classificação é usada para enviar o email).
1. Selecione o **Obrigado** página (a página para a qual os usuários são direcionados depois de enviarem o formulário).

   No **Formulário** selecione a página de agradecimento que os usuários devem acessar depois de enviarem o formulário. (Se deixado em branco, o formulário será exibido novamente após o envio.) Clique em **OK**.

1. Exporte as chaves do autor para a publicação.
1. Adicione o **Enviar** componente de botão do **Formulário** seção no sidekick.

   O formulário de inscrição está pronto. Publique a página configurada nas etapas acima, juntamente com o **obrigado** página para a instância de publicação. Qualquer assinante em potencial que visite a página pode preencher o formulário e, ao enviar o formulário, o visitante receberá um email de resposta automática sobre a ID de email preenchida no formulário.

   >[!NOTE]
   >
   >Para fazer com que o formulário de inscrição funcione corretamente, [as chaves de criptografia do autor precisam ser exportadas e importadas na instância de publicação](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
