---
title: Configuração na nuvem
seo-title: Cloud Configuration
description: Associar um aplicativo sob demanda a uma configuração da nuvem permite que a Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado no Mobile On-Demand, estabelecendo um link bidirecional. Siga esta página para saber mais.
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# Configuração na nuvem{#cloud-configuration}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Associar um aplicativo sob demanda a uma configuração da nuvem permite que a Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado no Mobile On-Demand, estabelecendo um link bidirecional. Ao vincular seu aplicativo a um projeto Mobile On-Demand, você poderá realizar a criação de conteúdo, como artigos, banners e coleções no AEM, mas também veicular esse conteúdo no Mobile On-Demand.

A partir daí, a publicação, a visualização e o gerenciamento de conteúdo se tornam possíveis. Também é possível importar conteúdo móvel sob demanda existente para o AEM e realizar a edição de conteúdo.

## Configuração da nuvem {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Antes de começar a configurar a configuração de nuvem para seu aplicativo sob demanda, você deve estar familiarizado com o AEM Mobile Provisioning e a configuração do cliente AEM Mobile On-demand Services.
>
>Para obter detalhes, consulte [Configuração do AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) na seção Administração.

Para configurar o Mobile On-Demand Cloud Services, clique na engrenagem superior no canto superior direito do **Gerenciar conexão** bloco do painel do aplicativo.

Familiarize-se com o painel do aplicativo e os blocos disponíveis. Consulte [Painel de aplicativos do AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter mais detalhes.

### Configuração do link para a configuração do Cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Certifique-se de ter uma configuração de nuvem e cliente sob demanda existente.
>
>Para obter detalhes, consulte [Configuração do AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) na seção Administração.

As etapas a seguir descrevem a configuração do link para a configuração da nuvem:

1. De **Celular**, escolha **Aplicativos** e depois seu aplicativo Mobile On-Demand do catálogo.
1. Clique no ícone de engrenagem na **Gerenciar conexão** mosaico.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Insira a configuração já existente ou crie uma nova inserindo o **Título da configuração**, **ID do dispositivo** e **Token do dispositivo**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Uma vez que o **ID do dispositivo** e **Token do dispositivo** forem verificados, escolha o projeto sob demanda na lista.

   Clique em **Enviar**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   O **Gerenciar conexão** O bloco mostra a Configuração da nuvem.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Se tentar alterar o projeto ao qual este aplicativo está associado, ao alternar um projeto no painel, você receberá um aviso sobre problemas de integridade de conteúdo, conforme mostrado na figura abaixo:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Próximas etapas {#the-next-steps}

Após configurar a configuração da nuvem para seu aplicativo, consulte os seguintes recursos para gerenciar o conteúdo:

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciando Coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer a publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com comprovação](/help/mobile/aem-mobile-manage-ondemand-services.md)
