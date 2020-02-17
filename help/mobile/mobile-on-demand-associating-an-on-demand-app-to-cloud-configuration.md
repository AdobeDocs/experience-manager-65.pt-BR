---
title: Configuração na nuvem
seo-title: Configuração na nuvem
description: Associar um aplicativo sob demanda a uma configuração na nuvem permite que o Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado sob demanda móvel estabelecendo um link bidirecional. Siga esta página para saber mais.
seo-description: Associar um aplicativo sob demanda a uma configuração na nuvem permite que o Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado sob demanda móvel estabelecendo um link bidirecional. Siga esta página para saber mais.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração na nuvem{#cloud-configuration}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Associar um aplicativo sob demanda a uma configuração na nuvem permite que o Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado sob demanda móvel estabelecendo um link bidirecional. Ao vincular seu aplicativo a um projeto Mobile On-Demand, você poderá realizar a criação de conteúdo, como artigos, banners e coleções no AEM, mas também fornecer esse conteúdo para Mobile On-Demand.

Daí, a publicação, visualização e gerenciamento de conteúdo se torna possível. Também é possível importar conteúdo Mobile On-Demand existente para o AEM e realizar a edição de conteúdo.

## Configuração da Cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Antes de começar a configurar a configuração em nuvem para seu aplicativo sob demanda, você deve estar familiarizado com o AEM Mobile Provisioning e a configurar o cliente de serviços sob demanda do AEM Mobile.
>
>Para obter detalhes, consulte [Configuração dos serviços](/help/mobile/aem-mobile-setup.md) sob demanda do AEM Mobile na seção Administração.

Para configurar Mobile On-Demand Cloud Services, clique na engrenagem superior no canto superior direito do bloco **Gerenciar conexão** no painel do aplicativo.

Familiarize-se com o painel do aplicativo e os blocos disponíveis. Consulte Painel [de aplicativos do](/help/mobile/mobile-apps-ondemand-application-dashboard.md) AEM Mobile para obter mais detalhes.

### Configuração do link para a configuração na nuvem {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Verifique se você tem uma configuração de cliente e nuvem sob demanda existente.
>
>Para obter detalhes, consulte [Configuração dos serviços](/help/mobile/aem-mobile-setup.md) sob demanda do AEM Mobile na seção Administração.

As etapas a seguir descrevem como configurar o link para a configuração da nuvem:

1. No **Mobile**, escolha **Aplicativos** e depois seu aplicativo Mobile On-Demand do catálogo.
1. Clique no ícone de engrenagem no bloco **Gerenciar conexão** .

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Insira a configuração já existente ou crie uma nova inserindo o Título **** de configuração, a Id **do** dispositivo e o Token **do** dispositivo.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Depois que a ID **do** dispositivo e o token **do** dispositivo forem verificados, escolha o projeto sob demanda na lista.

   Clique em **Enviar**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   O bloco **Gerenciar conexão** mostra a configuração da nuvem.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Se tentar alterar o projeto ao qual este aplicativo está associado, ao mudar de projeto no painel, você receberá um aviso sobre problemas de integridade de conteúdo, como mostrado na figura abaixo:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Próximas etapas {#the-next-steps}

Depois de configurar a configuração em nuvem para o aplicativo, consulte os seguintes recursos para gerenciar conteúdo:

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciamento de coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com o Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
