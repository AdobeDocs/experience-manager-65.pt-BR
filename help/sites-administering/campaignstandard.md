---
title: Integração com o Adobe Campaign Standard
seo-title: Integrating with Adobe Campaign Standard
description: Saiba como integrar o AEM com o Adobe Campaign Standard.
seo-description: Learn how to integrate AEM with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: a0062ffbdd6477eca494fea4142d271f3015599a
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 18%

---


# Integração com o Adobe Campaign Standard {#integrating-with-adobe-campaign-standard}

Ao integrar AEM com o Adobe Campaign, você pode gerenciar a entrega de e-mails, conteúdo e formulários diretamente no AEM. As etapas de configuração no Adobe Campaign Standard e no AEM são necessárias para permitir a comunicação bidirecional entre as soluções.

Essa integração permite que o AEM e o Adobe Campaign Standard sejam usados de forma independente. Os profissionais de marketing podem criar campanhas e usar o direcionamento no Adobe Campaign, enquanto os criadores de conteúdo podem trabalhar em paralelo no design de conteúdo no AEM. Com a integração, o conteúdo e o design da campanha criada no AEM podem ser direcionados e entregues pelo Adobe Campaign.

## Etapas de integração {#integration-steps}

A configuração da integração entre o AEM e o Adobe Campaign Standard requer várias etapas em ambas as soluções.

1. [Configure o ](#aemserver-user)
1. [Verifique o ](#resource-type-filter)
1. [Criar um modelo de delivery de email específico do AEM no Campaign](#aem-email-delivery-template)
1. [Configurar a integração do Campaign no AEM](#campaign-integration)
1. [Configurar replicação para a instância de publicação do AEM](#replication)
1. [Configurar o externalizador do AEM](#externalizer)
1. [Configure o ](#campaign-remote-user)
1. [Configurar a conta externa do AEM no Campaign](#acc-external-user)

Este documento aborda detalhadamente cada uma dessas etapas.

## Pré-requisitos {#prerequisites}

* Acesso de administrador ao Adobe Campaign Standard
   * Se você precisar de detalhes adicionais sobre como configurar e configurar o Adobe Campaign Standard, consulte o [Documentação do Adobe Campaign Standard.](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* Acesso do administrador ao AEM

## Configurar o usuário do aemserver no Campaign {#aemserver-user}

Por padrão, o Adobe Campaign Standard vem com uma `aemserver` usuário que AEM usa para se conectar ao Adobe Campaign. Você deve atribuir um grupo de segurança apropriado para este usuário e definir sua senha.

1. Faça logon no Adobe Campaign como administrador.

1. Toque ou clique no logotipo Adobe Campaign no canto superior esquerdo da barra de menus para abrir a navegação global e, em seguida, selecione **Administração** > **Usuários e segurança** > **Usuários** no menu de navegação.

1. Toque ou clique no botão `aemserver` no console de usuários.

1. Certifique-se de que `aemserver` O usuário é atribuído, no mínimo, a um grupo de segurança que tenha a função `deliveryPrepare` atribuído a ele. Por padrão, o grupo `Standard Users` tem esse papel.

   ![usuário do aemserver no Adobe Campaign](assets/acs-aemserver-user.png)

1. Toque ou clique **Salvar** para salvar as alterações.

Seu `aemserver` O usuário agora tem os direitos necessários para que o AEM possa usá-lo para se comunicar com o Adobe Campaign.

No entanto, antes que AEM possa usar a variável `aemserver` usuário, sua senha deve ser definida. Isso não pode ser feito por meio da Adobe Campaign. Deve ser realizado por um engenheiro de apoio Adobe. [Gere um tíquete junto ao Atendimento ao cliente do Adobe](https://experienceleague.adobe.com/?support-tab=home&amp;lang=pt-BR#support) para solicitar a redefinição do `aemserver` senha. Depois de obter a senha do Atendimento ao cliente do Adobe, mantenha-a em um local seguro.

## Verificar o AEMResourceTypeFilter no Campaign {#resource-type-filter}

O `AEMResourceTypeFilter` é uma opção no Adobe Campaign usada para filtrar AEM recursos que podem ser usados no Adobe Campaign. Como AEM contém muito conteúdo, essa opção atua como um filtro que permite ao Adobe Campaign recuperar apenas o conteúdo AEM de tipos especificamente projetados para serem usados no Adobe Campaign.

Essa opção vem pré-configurada. No entanto, pode ser necessário atualizá-lo se tiver personalizado os componentes do Campaign do AEM. Para verificar se a variável `AEMResourceTypeFilter` estiver configurada, siga estas etapas.

1. Faça logon no Adobe Campaign como administrador.

1. Toque ou clique no logotipo Adobe Campaign no canto superior esquerdo da barra de menus para abrir a navegação global e, em seguida, selecione **Administração** > **Configurações do aplicativo** > **Opções** no menu de navegação.

1. Toque ou clique no botão `AEMResourceTypeFilter` no console opções.

1. Confirme a configuração da variável `AEMResourceTypeFilter`. Os caminhos são delimitados por vírgulas e, por padrão, contêm:

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. Toque ou clique **Salvar** para salvar as alterações.

Seu `AEMResourceTypeFilter` O agora está configurado para recuperar o conteúdo correto do AEM.

## Criar um modelo de delivery de email específico do AEM no Campaign {#aem-email-delivery-template}

Por padrão, AEM não está ativado nos modelos de email do Adobe Campaign. Você deve configurar um novo template do delivery de email que possa ser usado para criar emails usando AEM conteúdo. Para criar um template do delivery de email específico do AEM, siga estas etapas.

1. Faça logon no Adobe Campaign como administrador.

1. Toque ou clique no logotipo Adobe Campaign no canto superior esquerdo da barra de menus para abrir a navegação global e, em seguida, selecione **Recursos** > **Modelos** > **Templates de delivery** no menu de navegação.

1. No console templates do delivery, localize o template de email padrão **Enviar por email (email)** e passe o mouse sobre o cartão (ou linha) que o representa para revelar as opções. Clique em **Elemento duplicado**.

   ![Elemento duplicado](assets/acs-copy-template.png)

1. No **Confirmação** , clique em **Confirmar** para duplicar o template.

   ![Caixa de diálogo de confirmação](assets/acs-confirmation.png)

1. O editor de modelos é aberto com a cópia do **Enviar por email (email)** modelo . Clique no botão **Editar propriedades** ícone na parte superior direita da janela.

   ![Editor de modelo](assets/acs-template-editor.png)

1. Na janela de propriedades, altere a **Rótulo** campo para ser descritivo do novo modelo de AEM.

1. Clique no botão **Conteúdo** para expandi-lo e selecionar **Adobe Experience Manager** no **Fonte de conteúdo** lista suspensa.

1. Isso revela o **Conta Adobe Experience Manager** campo. Use o menu suspenso para selecionar **Instância do Adobe Experience Manager (aemInstance)** usuário. Esse é o usuário externo padrão para a integração de AEM.

![Configurar propriedades do modelo](assets/acs-template-properties.png)

1. Clique em **Confirmar** para salvar as alterações nas propriedades.

1. No editor de modelos, clique em **Salvar** para salvar a cópia modificada do template de email para uso com o AEM.

Agora você tem um template de email que pode usar AEM conteúdo.

## Configurar a integração do Campaign no AEM {#campaign-integration}

AEM se comunica com o Adobe Campaign usando uma integração integrada e a `aemserver` usuário que você configurou no Adobe Campaign. Siga estas etapas para configurar essa integração.

1. Faça logon na instância de criação do AEM como administrador.

1. No painel lateral da navegação global, selecione **Ferramentas** > **Cloud Services** > **Cloud Services herdado** > **Adobe Campaign** e, depois, clique em **Configurar agora**.

   ![Configurar o Adobe Campaign](assets/configure-campaign-service.png)

1. Na caixa de diálogo, crie uma configuração do serviço do Campaign inserindo um **Título** e clique em **Criar**.

   ![Caixa de diálogo Configurar o Campaign](assets/configure-campaign-dialog.png)

1. Uma nova janela e uma nova caixa de diálogo são abertas para editar a configuração. Forneça as informações necessárias.

   * **Nome do usuário** - Isso é [o `aemserver` no Adobe Campaign que você configurou em uma etapa anterior.](#aemserver-user) Por padrão, é `aemserver`.
   * **Senha** - Esta é a senha para [o `aemserver` no Adobe Campaign que você solicitou ao Atendimento ao cliente do Adobe em uma etapa anterior.](#aemserver-user)
   * **Endpoint da API** - este é o URL da instância do Adobe Campaign.

   ![Configurar o Adobe Campaign no AEM](assets/configure-campaign.png)

1. Selecione **Conectar ao Adobe Campaign** para verificar a conexão e clique em **OK**.

Agora, o AEM pode se comunicar com o Adobe Campaign.

>[!NOTE]
>
>Certifique-se de que o servidor do Adobe Campaign possa ser acessado pela Internet. AEM não pode acessar redes privadas.

## Configurar replicação para a instância de publicação do AEM {#replication}

O conteúdo da campanha é criado pelos autores de conteúdo na instância de criação do AEM. Normalmente, essa instância só está disponível internamente em sua organização. Para que conteúdo como imagens e ativos sejam acessíveis aos recipients da sua campanha, é necessário publicar esse conteúdo.

O agente de replicação é responsável pela publicação do conteúdo da instância do autor de AEM para a instância de publicação e deve ser configurado para que a integração funcione corretamente. Essa etapa também é necessária para replicar determinadas configurações de instância de criação na instância de publicação.

Para configurar a replicação da instância do autor do AEM para a instância de publicação:

1. Faça logon na instância de criação do AEM como administrador.

1. No painel lateral de navegação global, selecione **Ferramentas** > **Implantação** > **Replicação** > **Agentes do autor**, em seguida, toque ou clique em **Agente padrão (publicar)**.

   ![Configurar agente de replicação](assets/acc-replication-config.png)

1. Toque ou clique **Editar** em seguida, selecione o **Transportes** guia .

1. Configure o **URI** substituindo o campo padrão `localhost` com o endereço IP da instância de publicação AEM.

   ![Guia Transporte](assets/acc-transport-tab.png)

1. Toque ou clique **OK** para salvar as alterações nas configurações do agente.

Você configurou a replicação para a instância de publicação do AEM para que os recipients da campanha possam acessar o conteúdo.

>[!NOTE]
>
>Se você não quiser usar o URL de replicação, mas usar o URL voltado para o público, poderá definir o URL público na seguinte configuração por meio do OSGi
>
>No painel lateral de navegação global, selecione **Ferramentas** > **Operações** > **Console da Web** > **Configuração do OSGi** e procurar **Integração do AEM Campaign - Configuração**. Edite a configuração e altere o campo **URL público** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Configurar o externalizador do AEM {#externalizer}

[O Externalizador é um serviço OSGi no AEM que transforma um caminho de recurso em um URL externo e absoluto, que é necessário para o AEM fornecer conteúdo que o Campaign possa usar. ](/help/sites-developing/externalizer.md) Você deve configurá-lo para que a integração do Campaign funcione.

1. Faça logon na instância de criação do AEM como administrador.
1. No painel lateral de navegação global, selecione **Ferramentas** > **Operações** > **Console da Web** > **Configuração do OSGi** e procurar **Externalizador de link CQ do dia**.
1. Por padrão, a última entrada no **Domínios** O campo destina-se à instância de publicação. Alterar o URL do padrão `http://localhost:4503` para sua instância de publicação disponível publicamente.

   ![Configurar o Externalizador](assets/acc-externalizer-config.png)

1. Toque ou clique em **Salvar**.

Você configurou o Externalizador e o Adobe Campaign agora pode acessar o conteúdo.

>[!NOTE]
A instância de publicação deve ser acessível através do servidor do Adobe Campaign. Se ela apontar para `localhost:4503` Para outro servidor que o Adobe Campaign não pode acessar, as imagens do AEM não serão exibidas no console do Adobe Campaign.

## Configure o usuário remoto de campanha no AEM {#campaign-remote-user}

Assim como você precisa de um usuário no Adobe Campaign que AEM possa usar para se comunicar com o Adobe Campaign, o Adobe Campaign também precisa de um usuário no AEM para comunicação com o AEM. Por padrão, a integração do Campaign cria a variável `campaign-remote` usuário no AEM. Siga estas etapas para configurar este usuário.

1. Faça logon no AEM como administrador.
1. No console de navegação principal, clique em **Ferramentas** no painel esquerdo.
1. Em seguida, clique em **Segurança** > **Usuários** para abrir o console de administração do usuário.
1. Localize o usuário `campaign-remote`.
1. Selecione o usuário `campaign-remote` e clique em **Propriedades** para editá-lo.
1. Na janela **Editar configurações de usuário**, clique em **Alterar senha**.
1. Forneça uma nova senha para o usuário e anote-a em um local seguro para uso futuro.
1. Clique em **Salvar** para salvar a alteração da senha.
1. Clique em **Salvar e fechar** para salvar as alterações no usuário `campaign-remote`.

## Configurar a conta externa do AEM no Campaign {#acc-external-user}

Quando você [criou um template de delivery de email específico de AEM,](#aem-email-delivery-template) você especificou que o modelo deve usar a variável `aemInstance` conta externa para se comunicar com o AEM. Para habilitar a comunicação bidirecional entre ambas as soluções, é necessário configurar essa conta no Adobe Campaign.

1. Faça logon no Adobe Campaign como administrador.

1. Toque ou clique no logotipo Adobe Campaign no canto superior esquerdo da barra de menus para abrir a navegação global e, em seguida, selecione **Administração** > **Configurações do aplicativo** > **Contas externas** no menu de navegação.

1. Toque ou clique no botão **Instância do Adobe Experience Manager (aemInstance)** no console de usuários.

1. Certifique-se de que o usuário tenha **Adobe Experience Manager** como **Tipo**.

1. No **Conexão** , defina os seguintes campos:

   1. Servidor: Esse é o URL do seu servidor de criação de AEM. Isso não deve terminar com uma barra.
   1. Conta: Este é o `campaign-remote` usuário [configurado anteriormente no AEM.](#campaign-remote-user)
   1. Senha: Esta é a senha da `campaign-remote`usuário [configurado anteriormente no AEM.](#campaign-remote-user)

   ![Editar o usuário aemInstance](assets/acs-external-acount-editor.png)

1. Certifique-se de que **Ativado** estiver marcada e, em seguida, clicar em **Salvar** para salvar as alterações.

Parabéns. Você concluiu a integração entre o AEM e o Adobe Campaign Standard!

## Próximas etapas {#next-steps}

Com o Adobe Campaign Classic e o AEM configurados, a integração agora é concluída.

Agora você pode aprender a criar um informativo no Adobe Experience Manager seguindo para [este documento.](/help/sites-authoring/campaign.md)
