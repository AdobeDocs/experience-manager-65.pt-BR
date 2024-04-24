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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Configurar o Cloud Service do Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A variável **Mosaico de métricas móveis** no centro de comando, o fornece análises em tempo real para o aplicativo móvel.

A variável [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) O SDK é disponibilizado por meio de um plug-in PhoneGap. As métricas são coletadas e armazenadas em cache no dispositivo até que o dispositivo seja conectado, momento em que os dados são enviados para a nuvem do Adobe Mobile Services para relatórios e análise.

O SDK do Adobe Mobile Analytics fornece o seguinte:

1. **Coleta de dados para canais móveis** - Colete dados abrangentes para seus sites e aplicativos móveis nos principais sistemas operacionais.
1. **Análise de engajamento móvel** : entenda o engajamento do usuário no aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores iniciam o canal, se fazem compras dele e muito mais.
1. **Painéis e relatórios do aplicativo móvel** : obtenha relatórios de uso que incluem métricas de ciclo de vida para seus aplicativos e métricas da loja de aplicativos — consulte tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise de campanha via celular** - Quantifique a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa móveis, anúncios de exibição para dispositivos móveis e códigos QR.
1. **Análise de geolocalização** - Descubra onde os usuários do aplicativo iniciam e interagem com suas experiências móveis por localização no GPS ou pontos de interesse.
1. **Análise de definição de caminho** - Veja como os usuários navegam pelo seu aplicativo para determinar quais telas e elementos da interface do usuário estão envolvendo os usuários e quais fazem com que eles abandonem.

>[!CAUTION]
>
>A variável **Analisar métricas** O bloco é exibido no painel somente se você tiver configurado os serviços em nuvem.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaico de métricas do centro de comando do AEM

## Configuração do Cloud Service {#configuring-the-cloud-service}

Para aproveitar as vantagens do Adobe Mobile Services Analytics, é necessário configurar o AEM Mobile Analytics Cloud Service com as informações de sua conta do Adobe Analytics.

1. Clique no ícone superior direito para adicionar ou editar os Cloud Service do **Gerenciar Cloud Service** mosaico no painel do aplicativo.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. A variável **Adicionar ou editar Cloud Service** é exibida. Selecionar **Adobe Mobile Services** e clique em **Próxima**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Escolha uma configuração existente na **Mobile Services** ou escolha **Criar configuração** para criar um.

   Para nova configuração, insira o **Propriedades do Mobile Services** e clique em **Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Se as credenciais forem verificadas, a variável **Verificar** botão muda para **Verificado**. Você pode escolher um aplicativo de serviço móvel em **Selecionar um serviço de aplicativo móvel**.

   Clique em **Enviar** para definir sua configuração.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Depois de definir uma configuração de nuvem, você pode visualizar a mesma no painel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Depois de definir a configuração da nuvem, você pode visualizar as **Analisar métricas** Mosaico no painel do aplicativo.

   ![chlimage_1-28](assets/chlimage_1-28.png)
