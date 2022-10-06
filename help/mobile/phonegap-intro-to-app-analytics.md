---
title: Rastrear o desempenho do aplicativo com o Adobe Mobile Analytics
seo-title: Track App Performance with Adobe Mobile Analytics
description: Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, as falhas do aplicativo, os detalhes do dispositivo e tantas outras métricas críticas para seus aplicativos móveis. Siga esta página para saber mais.
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# Rastrear o desempenho do aplicativo com o Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Você deseja aumentar as conversões e a fidelidade do cliente.

Você deseja fornecer experiências relevantes e envolventes aos seus clientes.

O que seu aplicativo AEM Mobile está fazendo para suas campanhas de marketing?

Como você pode ajustar os aplicativos móveis para proporcionar a melhor experiência aos usuários?

Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, as falhas do aplicativo, os detalhes do dispositivo e tantas outras métricas críticas para seus aplicativos móveis.

O Adobe Experience Manager Mobile fornece uma visão geral dos detalhes de sua análise móvel diretamente do Painel de aplicativos do AEM Mobile. O **Bloco de métricas móveis** no painel, o fornece análises em tempo real para seu aplicativo móvel, permitindo que desenvolvedores, autores e administradores tenham uma ideia rápida da integridade do seu aplicativo móvel. Sob a capa que alimenta a análise, a variável [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. O SDK do Adobe Mobile Analytics pode ser conectado a seus aplicativos nativamente ou por meio de um plug-in PhoneGap bridge para visualizações da Web. As métricas são coletadas e armazenadas em cache no dispositivo até que o dispositivo esteja conectado, no qual os dados são enviados para a Adobe Mobile Services Cloud para relatórios e análises.

O SDK do Adobe Mobile Analytics oferece o seguinte:

1. **Coleta de dados para canais móveis** - Colete dados abrangentes para seus sites e aplicativos móveis em todos os principais sistemas operacionais.
1. **Análise de engajamento móvel** - Entenda o engajamento do usuário em seu aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores inicializam o canal, independentemente de fazerem compras com ele e muito mais.
1. **Painéis e relatórios do aplicativo móvel** - Obtenha relatórios de uso que incluem medições de ciclo de vida para seus aplicativos e métricas da loja de aplicativos — consulte tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise de campanha móvel** - Quantificar a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa para dispositivos móveis, anúncios para exibição para dispositivos móveis e códigos QR.
1. **Análise de geolocalização** - Descubra onde seus usuários do aplicativo são iniciados e interagem com suas experiências móveis por localização do GPS ou pontos de interesse.
1. **Análise de definição de caminho** - Veja como os usuários navegam pelo seu aplicativo para determinar quais telas e elementos da interface do usuário estão envolvendo usuários e quais fazem com que os usuários saiam.

Esta seção descreve como [Desenvolvedores de AEM](#developers) Você pode aprender a preparar aplicativos AEM Mobile com o rastreamento analítico.

Por último, [Administradores de AEM](#administrators) aprenda a:

* criar um serviço em nuvem para o Adobe Mobile Services
* criar uma configuração de serviço móvel e associar um conjunto de relatórios
* associar a configuração do serviço móvel a um aplicativo móvel
* exibir métricas através do Centro de comando AEM Apps
* atribuir a configuração do SDK do AMS ao aplicativo móvel

## Para desenvolvedores - Integre o Analytics ao seu aplicativo {#for-developers-integrate-analytics-into-your-app}

**Pré-requisito:** AEM administradores precisam configurar a configuração de nuvem do Adobe Mobile Services, [conforme discutido abaixo](#amscloudserviceconfig).

Os desenvolvedores são responsáveis por [adição do analytics a um aplicativo AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) conforme necessário para rastrear, relatar e entender como os usuários interagem com o conteúdo do seu aplicativo móvel e medir medições de ciclo de vida importantes, como inicializações, tempo no aplicativo e taxa de falha.

## Para administradores - Configure o Cloud Service do Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aproveitar os benefícios do Adobe Mobile Services, você precisa configurar o Cloud Service do Adobe Mobile Services AEM com suas informações de conta da Adobe Analytics. O Centro de comando de aplicativos fornece um **Analisar métricas** bloco em que você pode criar e associar o serviço de nuvem ao aplicativo móvel.

Configure o serviço de nuvem para o seu aplicativo móvel começa clicando no ícone de engrenagem localizado no bloco Analisar métricas .

![chlimage_1-125](assets/chlimage_1-125.png)

Clicar no ícone de engrenagem no bloco Analisar métricas abrirá a caixa de diálogo modal &quot;Configurar análise do Mobile Services&quot;. Selecione a configuração no menu suspenso &quot;Selecionar uma configuração do Mobile Service&quot;. Se precisar criar uma nova configuração, clique na chave inglesa .

Para criar um serviço em nuvem do Adobe Mobile Service, há duas etapas envolvidas: a conexão com o serviço e a seleção de qual conjunto de relatórios atribuir à configuração.

Para começar, clique no botão &#39;+&#39; no bloco Gerenciar Cloud Services no painel.

![chlimage_1-126](assets/chlimage_1-126.png)

Ao clicar no botão **+** botão &#39;, o **Adicionar Cloud Service** será exibido.

![chlimage_1-127](assets/chlimage_1-127.png)

Selecione ou crie uma nova configuração de serviço móvel preenchendo os campos obrigatórios, conforme mostrado abaixo. O administrador do AEM precisará dessas informações para criar com êxito a conexão com o Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Após concluir as Configurações da conta do Mobile Services, você será solicitado a selecionar um aplicativo. Isso conecta os relatórios de análise do Adobe Mobile Service a esse aplicativo.

Selecione o serviço móvel desejado e clique em &#39;Atualizar&#39; para atribuir a configuração do serviço móvel e fechar a caixa de diálogo.

Agora que você associou a configuração do serviço móvel ao aplicativo AEM Mobile, o bloco começará a buscar os dados da métrica e começará a gerar relatórios.

![chlimage_1-129](assets/chlimage_1-129.png)

### Arquivo de configuração do SDK do Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

Neste ponto, seu aplicativo móvel está associado a um serviço em nuvem, no entanto, o aplicativo móvel ainda não sabe como comunicar as métricas móveis coletadas de volta ao Adobe Analytics. Para conectar o aplicativo móvel ao Adobe Analytics, o arquivo de configuração de SDK do Adobe Mobile Services precisa ser adicionado ao Adobe Experience Manager.

No bloco Analisar métricas , clique no ícone de seta para expor as entradas do menu Baixar/carregar a configuração do SDK do AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

A primeira etapa é obter a configuração do SDK do Adobe Mobile Services, clicar em &quot;Baixar configuração do SDK do AMS&quot; redirecionará você para o site do Adobe Mobile Services, onde é possível baixar o arquivo de configuração. Depois de obter o arquivo ADBMobileConfig.json, clique em &quot;Fazer upload da configuração do SDK do AMS&quot; para fazer upload do arquivo de configuração no AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Clique no botão &quot;Fazer upload do Adobe Mobile Services Application Config&quot; e procure pelo arquivo ADBMobileConfig.json e clique em &quot;Fazer upload&quot;.

Agora que o aplicativo móvel tem acesso ao arquivo ADBMobileConfig.json, ele tem o conhecimento sobre como se comunicar de volta ao Adobe Analytics e começar a relatar o valor dessas métricas importantes que ajudarão a aumentar o sucesso dos aplicativos.

## O que vem a seguir? {#what-s-next}

1. [Iniciar minha experiência com o aplicativo AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gerenciar o conteúdo do meu aplicativo](/help/mobile/phonegap-manage-app-content.md)
1. [Criar meu aplicativo](/help/mobile/building-app-mobile-phonegap.md)
1. [Acompanhe o desempenho do meu aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Fornecer uma experiência personalizada com o aplicativo Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensagens importantes para meus usuários](/help/mobile/phonegap-push-notifications.md)
