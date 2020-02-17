---
title: Configurar o serviço Adobe Mobile Services Cloud
seo-title: Configurar o serviço Adobe Mobile Services Cloud
description: Siga esta página para configurar o serviço Adobe Mobile Services Cloud.
seo-description: Siga esta página para configurar o serviço Adobe Mobile Services Cloud.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar o serviço Adobe Mobile Services Cloud {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O título **Métricas** móveis no centro de comando fornece análises em tempo real para seu aplicativo móvel.

O [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK é disponibilizado por meio de um plug-in PhoneGap. As métricas são coletadas e armazenadas em cache no dispositivo até que o dispositivo esteja conectado, e então os dados são enviados para a Adobe Mobile Services Cloud para relatórios e análises.

O SDK do Adobe Mobile Analytics oferece o seguinte:

1. **Coleta de dados para canais** móveis - Colete dados abrangentes para seus sites e aplicativos móveis em todos os principais sistemas operacionais.
1. **Análise** de envolvimento móvel - Entenda o envolvimento do usuário em seu aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores iniciam o canal, se fazem compras dele e muito mais.
1. **Painéis e relatórios** de aplicativos móveis - Obtenha relatórios de uso que incluem medições de ciclo de vida para seus aplicativos e métricas da app store. consulte as tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise** de campanha móvel - quantificar a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa móvel, anúncios de exibição móvel e códigos QR.
1. **Análise** de localização geográfica - Descubra onde os usuários do aplicativo iniciam e interagem com suas experiências móveis por localização GPS ou pontos de interesse.
1. **Análise** de definição de caminho - Veja como os usuários navegam pelo aplicativo para determinar quais telas e elementos da interface estão envolvendo os usuários e quais fazem com que os usuários sejam excluídos.

>[!CAUTION]
>
>O título **Analisar métricas** é exibido no painel, somente se você tiver configurado serviços em nuvem.

![chlimage_1-22](assets/chlimage_1-22.png)

Bloco de métricas do Centro de comando do AEM

## Configuração do serviço em nuvem {#configuring-the-cloud-service}

Para aproveitar as vantagens do Adobe Mobile Services Analytics, é necessário configurar o AEM Mobile Analytics Cloud Service com suas informações de conta do Adobe Analytics.

1. Clique no ícone superior direito para adicionar ou editar os Serviços em nuvem no bloco **Gerenciar serviços** em nuvem do painel do aplicativo.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. A tela **Adicionar ou editar serviços** da nuvem é exibida. Selecione **Adobe Mobile Services** e clique em **Avançar**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Escolha uma configuração existente no **Mobile Services** ou escolha **Criar configuração** para criar uma nova.

   Para obter uma nova configuração, digite as Propriedades do **Mobile Services** e clique **em Verificar.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Se as credenciais forem verificadas, o botão **Verificar** será alterado para **Verificado**. Você pode escolher um aplicativo de serviço móvel em **Selecionar um serviço** de aplicativo móvel.

   Clique em **Enviar** para configurar sua configuração.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Depois de configurar uma configuração de nuvem, você pode exibir o mesmo no painel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Depois de configurar sua configuração em nuvem, você pode exibir o título **Analisar métricas** no painel do aplicativo.

   ![chlimage_1-28](assets/chlimage_1-28.png)

