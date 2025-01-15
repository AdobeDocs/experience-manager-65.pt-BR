---
title: Configurar o Cloud Service do Adobe Mobile Services
description: Siga esta página para configurar o Cloud Service do Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Configurar o Cloud Service do Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

{{ue-over-mobile}}

O **Bloco de Métricas do Mobile** no centro de comando fornece análises em tempo real para o seu aplicativo móvel.

O SDK do [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) é disponibilizado por meio de um plug-in PhoneGap. As métricas são coletadas e armazenadas em cache no dispositivo até que o dispositivo seja conectado, momento em que os dados são enviados para a nuvem do Adobe Mobile Services para relatórios e análise.

O Adobe Mobile Analytics SDK oferece o seguinte:

1. **Coleta de dados para canais móveis** - Colete dados abrangentes para seus sites e aplicativos móveis em todos os principais sistemas operacionais.
1. **Análise de engajamento móvel** - Entenda o engajamento do usuário no aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores iniciam o canal, se fazem compras dele e muito mais.
1. **Painéis e relatórios de aplicativos móveis** - Obtenha relatórios de uso que incluem métricas de ciclo de vida dos seus aplicativos e métricas da loja de aplicativos — veja as tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise de campanha móvel** - Quantifique a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa móveis, anúncios de exibição para dispositivos móveis e códigos QR.
1. **Análise de geolocalização** - Descubra onde os usuários do aplicativo inicializam e interagem com suas experiências móveis por localização no GPS ou pontos de interesse.
1. **Análise de definição de caminho** - Veja como os usuários navegam pelo seu aplicativo para determinar quais telas e elementos da interface do usuário estão envolvendo os usuários e quais fazem com que eles abandonem.

>[!CAUTION]
>
>O bloco **Analisar métricas** será exibido no painel somente se você tiver configurado os serviços em nuvem.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaico de métricas do centro de comando do AEM

## Configuração do Cloud Service {#configuring-the-cloud-service}

Para aproveitar as vantagens do Adobe Mobile Services Analytics, é necessário configurar o AEM Mobile Analytics Cloud Service com as informações de sua conta do Adobe Analytics.

1. Clique no ícone superior direito para adicionar ou editar os Cloud Service do bloco **Gerenciar Cloud Service** no painel de aplicativos.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. A tela **Adicionar ou Editar Cloud Service** é exibida. Selecione **Adobe Mobile Services** e clique em **Avançar**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Escolha uma configuração existente do **Mobile Services** ou escolha **Criar configuração** para criar uma.

   Para nova configuração, insira as **Propriedades do Mobile Services** e clique em **Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Se as credenciais forem verificadas, o botão **Verificar** será alterado para **Verificado**. Você pode escolher um aplicativo de serviço para dispositivo móvel em **Selecione um Serviço de Aplicativo para Dispositivo Móvel**.

   Clique em **Enviar** para definir sua configuração.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Depois de definir uma configuração de nuvem, você pode visualizar a mesma no painel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Depois de definir a configuração de nuvem, você pode exibir o bloco **Analisar métricas** no painel do aplicativo.

   ![chlimage_1-28](assets/chlimage_1-28.png)
