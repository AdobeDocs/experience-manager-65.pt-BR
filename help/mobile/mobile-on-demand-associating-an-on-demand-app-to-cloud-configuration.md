---
title: Configuração de nuvem
description: Associar um aplicativo sob demanda a uma configuração na nuvem permite que o Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado no Mobile On-Demand estabelecendo um link bidirecional. Siga esta página para saber mais.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# Configuração de nuvem{#cloud-configuration}

{{ue-over-mobile}}

Associar um aplicativo sob demanda a uma configuração na nuvem permite que o Adobe Experience Manager (AEM) se comunique diretamente com um projeto hospedado no Mobile On-Demand estabelecendo um link bidirecional. Ao vincular seu aplicativo a um projeto do Mobile On-Demand, você poderá criar conteúdo, como artigos, banners e coleções no AEM, mas também fornecerá esse conteúdo ao Mobile On-Demand.

A partir daí, a publicação, a pré-visualização e o gerenciamento de conteúdo se tornam possíveis. Você também pode importar conteúdo Mobile On-Demand existente para o AEM e fazer edição de conteúdo.

## Definição da configuração de nuvem {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Antes de começar a definir a configuração de nuvem para o aplicativo On-Demand, você deve se familiarizar com o Provisionamento e a Configuração do cliente AEM Mobile On-demand Services do AEM Mobile.
>
>Para obter detalhes, consulte [Configuração do AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) na seção Administração.

Para configurar os Cloud Service do Mobile On-Demand, clique na engrenagem superior no canto superior direito do bloco **Gerenciar conexão** do painel do aplicativo.

Você deve estar familiarizado com o painel do aplicativo e os blocos disponíveis. Consulte [Painel de Aplicativos do AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) para obter mais detalhes.

### Definição da configuração de link para nuvem {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Verifique se você tem uma configuração de cliente On-Demand e de nuvem existente.
>
>Para obter detalhes, consulte [Configuração do AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) na seção Administração.

As etapas a seguir descrevem a definição do link para a configuração na nuvem:

1. No **Mobile**, escolha **Apps** e seu aplicativo Mobile On-Demand no catálogo.
1. Clique no ícone de engrenagem no bloco **Gerenciar Conexão**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Insira a configuração já existente ou crie uma inserindo o **Título da Configuração**, o **ID do Dispositivo** e o **Token do Dispositivo**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Depois que a sua **ID do dispositivo** e o **Token do dispositivo** forem verificados, escolha o seu projeto sob demanda na lista.

   Clique em **Enviar**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   O bloco **Gerenciar Conexão** mostra sua Configuração na Nuvem.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Se você tentar alterar a qual projeto este aplicativo está associado ao alternar o projeto no painel, você receberá um aviso sobre problemas de integridade de conteúdo, como mostrado na figura abaixo:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Próximas etapas {#the-next-steps}

Após definir a configuração de nuvem do seu aplicativo, consulte os seguintes recursos para gerenciar conteúdo:

* [Gerenciamento de artigos](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gerenciamento de banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gerenciar coleções](/help/mobile/mobile-on-demand-managing-collections.md)
* [Upload de recursos compartilhados](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicar/desfazer publicação do conteúdo](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Visualização com simulação](/help/mobile/aem-mobile-manage-ondemand-services.md)
