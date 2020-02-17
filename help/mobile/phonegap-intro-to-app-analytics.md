---
title: Acompanhar o desempenho do aplicativo com o Adobe Mobile Analytics
seo-title: Acompanhar o desempenho do aplicativo com o Adobe Mobile Analytics
description: Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, falhas de aplicativos, detalhes de dispositivos e tantas outras métricas críticas para seus aplicativos móveis. Siga esta página para saber mais.
seo-description: Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, falhas de aplicativos, detalhes de dispositivos e tantas outras métricas críticas para seus aplicativos móveis. Siga esta página para saber mais.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Acompanhar o desempenho do aplicativo com o Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Você deseja aumentar as conversões e a fidelidade do cliente.

Você deseja fornecer experiências relevantes e envolventes aos seus clientes.

O que seu aplicativo AEM Mobile está fazendo para suas campanhas de marketing?

Como você pode ajustar seus aplicativos móveis para proporcionar a melhor experiência para seus usuários?

Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, falhas de aplicativos, detalhes de dispositivos e tantas outras métricas críticas para seus aplicativos móveis.

O Adobe Experience Manager Mobile oferece uma visão geral dos detalhes de sua análise móvel diretamente do painel de aplicativos do AEM Mobile. O título **Métricas** móveis no painel fornece análises em tempo real para seu aplicativo móvel, permitindo que desenvolvedores, autores e administradores obtenham uma rápida visão da integridade do aplicativo móvel. Nas capas que alimentam a análise está o SDK do [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) . O SDK do Adobe Mobile Analytics pode ser conectado aos seus aplicativos nativamente ou por meio de um plug-in PhoneGap bridge para visualizações da Web. As métricas são coletadas e armazenadas em cache no dispositivo até que o dispositivo esteja conectado, no qual os dados são enviados para a Adobe Mobile Services Cloud para relatórios e análises.

O SDK do Adobe Mobile Analytics oferece o seguinte:

1. **Coleta de dados para canais** móveis - Colete dados abrangentes para seus sites e aplicativos móveis em todos os principais sistemas operacionais.
1. **Análise** de envolvimento móvel - Entenda o envolvimento do usuário em seu aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores iniciam o canal, se fazem compras dele e muito mais.
1. **Painéis e relatórios** de aplicativos móveis - Obtenha relatórios de uso que incluem medições de ciclo de vida para seus aplicativos e métricas da app store. consulte as tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise** de campanha móvel - quantificar a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa móvel, anúncios de exibição móvel e códigos QR.
1. **Análise** de localização geográfica - Descubra onde os usuários do aplicativo iniciam e interagem com suas experiências móveis por localização GPS ou pontos de interesse.
1. **Análise** de definição de caminho - Veja como os usuários navegam pelo aplicativo para determinar quais telas e elementos da interface estão envolvendo os usuários e quais fazem com que os usuários sejam excluídos.

Esta seção descreve como os desenvolvedores [do](#developers) AEM podem aprender a instruir aplicativos do AEM Mobile com rastreamento analítico.

Por fim, os administradores [do](#administrators) AEM aprendem a:

* criar um serviço em nuvem para o Adobe Mobile Services
* criar uma configuração de serviço móvel e associar um conjunto de relatórios
* associar a configuração do serviço móvel a um aplicativo móvel
* exibir métricas por meio do AEM Apps Command Center
* atribuir a configuração do SDK do AMS ao seu aplicativo móvel

## Para desenvolvedores - Integrar o Analytics ao seu aplicativo {#for-developers-integrate-analytics-into-your-app}

**** Pré-requisito: Os administradores do AEM precisam configurar a configuração de nuvem do Adobe Mobile Services, [conforme discutido abaixo](#amscloudserviceconfig).

Os desenvolvedores são responsáveis por [adicionar a análise a um aplicativo](/help/mobile/phonegap-add-analytics-to-apps.md) do AEM Mobile conforme necessário para rastrear, relatar e entender como os usuários se envolvem com o conteúdo do aplicativo móvel e medir as principais medições de ciclo de vida, como inicializações, tempo no aplicativo e taxa de falha.

## Para administradores - Configurar o serviço da Adobe Mobile Services Cloud {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aproveitar os Adobe Mobile Services, é necessário configurar o AEM Adobe Mobile Services Cloud Service com as informações de conta do Adobe Analytics. A Central de comandos do aplicativo fornece um bloco de métricas **de** análise onde você pode criar e associar o serviço de nuvem ao aplicativo móvel.

Configure o serviço de nuvem para seu aplicativo móvel e clique no ícone de engrenagem localizado no bloco Analisar métricas.

![chlimage_1-125](assets/chlimage_1-125.png)

Clicar no ícone de engrenagem no bloco Analisar métricas abrirá a caixa de diálogo modal &quot;Configurar análise do Mobile Services&quot;. Selecione sua configuração no menu suspenso &quot;Selecione uma configuração de serviço móvel&quot;. Se precisar criar uma nova configuração, clique no botão chave inglesa.

Para criar um serviço em nuvem do Adobe Mobile Service, há duas etapas envolvidas: a conexão com o serviço e a seleção do conjunto de relatórios a ser atribuído à configuração.

Para começar, clique no botão &#39;+&#39; no bloco Gerenciar serviços da nuvem no painel.

![chlimage_1-126](assets/chlimage_1-126.png)

Ao clicar no botão &quot;**+**&quot;, o assistente para **Adicionar serviço** em nuvem será exibido.

![chlimage_1-127](assets/chlimage_1-127.png)

Selecione ou crie uma nova configuração de serviço móvel preenchendo os campos obrigatórios, conforme mostrado abaixo. O administrador do AEM precisará dessas informações para criar com êxito a conexão com o Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Após concluir as Configurações da conta do Mobile Services, você será solicitado a selecionar um aplicativo. Isso conecta os relatórios de análise do Adobe Mobile Service ao aplicativo.

Selecione o serviço móvel desejado e clique em &#39;Atualizar&#39; para atribuir a configuração do serviço móvel e fechar a caixa de diálogo.

Agora que você associou a configuração do serviço móvel ao aplicativo do AEM Mobile, o bloco começará a buscar os dados da métrica e começará a gerar relatórios.

![chlimage_1-129](assets/chlimage_1-129.png)

### Arquivo de configuração do SDK do Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

Nesse ponto, seu aplicativo móvel está associado a um serviço em nuvem, no entanto, o aplicativo móvel ainda não sabe como comunicar as métricas móveis coletadas de volta ao Adobe Analytics. Para conectar o aplicativo móvel ao Adobe Analytics, o arquivo de configuração do SDK do Adobe Mobile Services precisa ser adicionado ao Adobe Experience Manager.

No bloco Analisar métricas, clique no ícone de seta para expor as entradas do menu Configuração do SDK para Download / Upload do AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

A primeira etapa é obter a configuração do SDK do Adobe Mobile Services, clicar em &quot;Baixar configuração do SDK do AMS&quot; redirecionará você para o site do Adobe Mobile Services no qual você pode baixar o arquivo de configuração. Depois de obter o arquivo ADBMobileConfig.json, clique em &quot;Carregar configuração do SDK do AMS&quot; para carregar o arquivo de configuração no AEM.

![chlimage_1-135](assets/chlimage_1-131.png)

Clique no botão &quot;Carregar configuração do aplicativo Adobe Mobile Services&quot; e procure o arquivo ADBMobileConfig.json e clique em &quot;Carregar&quot;.

Agora que o aplicativo móvel tem acesso ao arquivo ADBMobileConfig.json, ele tem o conhecimento sobre como se comunicar de volta ao Adobe Analytics e começar a relatar o valor dessas métricas importantes que ajudarão a direcionar seus aplicativos com sucesso.

## O que vem depois? {#what-s-next}

1. [Iniciar minha experiência com aplicativos do AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gerenciar o conteúdo do meu aplicativo](/help/mobile/phonegap-manage-app-content.md)
1. [Criar meu aplicativo](/help/mobile/building-app-mobile-phonegap.md)
1. [Acompanhar o desempenho do meu aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Fornecer uma experiência personalizada com o aplicativo Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensagens importantes para meus usuários](/help/mobile/phonegap-push-notifications.md)