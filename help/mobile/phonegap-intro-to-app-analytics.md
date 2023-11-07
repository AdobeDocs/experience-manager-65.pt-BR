---
title: Acompanhe o desempenho do aplicativo com o Adobe Mobile Analytics
description: Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, falhas do aplicativo, detalhes do dispositivo e muitas outras métricas críticas para seus aplicativos móveis. Siga esta página para saber mais.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Acompanhe o desempenho do aplicativo com o Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Você deseja impulsionar conversões e fidelidade do cliente mais altas.

Você deseja proporcionar experiências relevantes e envolventes aos seus clientes.

O que seu aplicativo AEM Mobile está fazendo com suas campanhas de marketing?

Como você pode ajustar os aplicativos móveis para fornecer a melhor experiência aos seus usuários?

Com o Adobe Mobile Services, você pode obter informações sobre como seus usuários estão usando seus aplicativos móveis rastreando o uso, falhas do aplicativo, detalhes do dispositivo e muitas outras métricas críticas para seus aplicativos móveis.

O Adobe Experience Manager Mobile fornece uma visão geral dos detalhes da análise móvel diretamente do painel de aplicativos do AEM Mobile. A variável **Mosaico de métricas móveis** no painel do fornece o Real-Time Analytics para seu aplicativo móvel, permitindo que desenvolvedores, autores e administradores tenham uma ideia rápida da integridade do seu aplicativo móvel. Nas capas, o poder da análise é o [Adobe Mobile Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK. O SDK do Adobe Mobile Analytics pode ser conectado aos seus aplicativos nativamente ou por meio de um plug-in PhoneGap Bridge para visualizações da Web. As métricas são coletadas e armazenadas em cache no dispositivo até que ele seja conectado, no qual os dados são enviados para a nuvem do Adobe Mobile Services para relatórios e análise.

O SDK do Adobe Mobile Analytics fornece o seguinte:

1. **Coleta de dados para canais móveis** - Colete dados abrangentes para seus sites e aplicativos móveis nos principais sistemas operacionais.
1. **Análise de engajamento móvel** : entenda o engajamento do usuário no aplicativo móvel, site ou vídeo, incluindo a frequência com que os consumidores iniciam o canal, se fazem compras dele e muito mais.
1. **Painéis e relatórios do aplicativo móvel** : obtenha relatórios de uso que incluem métricas de ciclo de vida para seus aplicativos e métricas da loja de aplicativos — consulte tendências para usuários, inicializações, duração média da sessão, duração da retenção e falhas.
1. **Análise de campanha via celular** - Quantifique a eficácia de campanhas específicas para dispositivos móveis, como SMS, anúncios de pesquisa móveis, anúncios de exibição para dispositivos móveis e códigos QR.
1. **Análise de geolocalização** - Descubra onde os usuários do aplicativo iniciam e interagem com suas experiências móveis por localização no GPS ou pontos de interesse.
1. **Análise de definição de caminho** - Veja como os usuários navegam pelo seu aplicativo para determinar quais telas e elementos da interface do usuário estão envolvendo os usuários e quais fazem com que eles abandonem.

Esta seção descreve como [Desenvolvedores de AEM](#developers) Em seguida, você pode aprender a instrumentar os aplicativos do AEM Mobile com o rastreamento de análise.

Por último, [Administradores de AEM](#administrators) saiba como:

* criar um serviço em nuvem para o Adobe Mobile Services
* criar uma configuração de serviço para dispositivos móveis e associar um conjunto de relatórios
* associar a configuração do mobile service a um aplicativo móvel
* exibir métricas por meio do Centro de comandos dos aplicativos AEM
* atribuir a configuração de SDK AMS ao aplicativo móvel

## Para desenvolvedores - Integre o Analytics ao seu aplicativo {#for-developers-integrate-analytics-into-your-app}

**Pré-requisito:** Os administradores de AEM devem configurar a configuração de nuvem do Adobe Mobile Services, [conforme discutido abaixo](#amscloudserviceconfig).

Os desenvolvedores são responsáveis por [adicionar o analytics a um aplicativo AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) conforme necessário para rastrear, relatar e entender como os usuários se envolvem com o conteúdo do aplicativo móvel e medir as principais métricas de ciclo de vida, como inicializações, tempo no aplicativo e taxa de falha.

## Para administradores - Configurar o Cloud Service do Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Para aproveitar as vantagens do Adobe Mobile Services, você deve configurar o Cloud Service AEM Adobe Mobile Services com as informações de sua conta Adobe Analytics. O Centro de comando dos aplicativos fornece uma **Analisar métricas** bloco, onde é possível criar e associar o serviço em nuvem ao aplicativo móvel.

A configuração do serviço em nuvem para o aplicativo móvel começa clicando no ícone de engrenagem no bloco Analisar métricas.

![chlimage_1-125](assets/chlimage_1-125.png)

Clicar no ícone de engrenagem no bloco Analisar métricas abre a caixa de diálogo modal &quot;Configurar análise do Mobile Services&quot;. Selecione sua configuração na lista suspensa &quot;Selecionar uma configuração do serviço móvel&quot;. Se precisar criar uma configuração, clique na chave inglesa.

Para criar um serviço em nuvem do Adobe Mobile Service, há duas etapas envolvidas: a conexão com o serviço e a seleção do conjunto de relatórios a ser atribuído à configuração.

Para começar, clique no botão &quot;+&quot; no bloco Gerenciar Cloud Service no painel.

![chlimage_1-126](assets/chlimage_1-126.png)

Depois de clicar no ícone &#39;**+** botão &#39;, o botão **Adicionar Cloud Service** será exibido.

![chlimage_1-127](assets/chlimage_1-127.png)

Selecione ou crie uma configuração de serviço para dispositivos móveis preenchendo os campos obrigatórios conforme mostrado abaixo. O administrador do AEM requer essas informações para criar com êxito a conexão com o Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Após concluir as Configurações da conta do Mobile Services, você será solicitado a selecionar um aplicativo. Isso conecta os relatórios analíticos do Adobe Mobile Service a esse aplicativo.

Selecione o serviço para dispositivos móveis desejado e clique em &quot;Atualizar&quot; para atribuir a configuração do serviço para dispositivos móveis e fechar a caixa de diálogo.

Agora que você associou a configuração do serviço para dispositivos móveis ao aplicativo AEM Mobile, o bloco começa a buscar os dados da métrica e começar a criar relatórios.

![chlimage_1-129](assets/chlimage_1-129.png)

### Arquivo de configuração SDK do Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

Neste ponto, o aplicativo móvel está associado a um serviço na nuvem, no entanto, o aplicativo móvel ainda não sabe como comunicar as métricas móveis coletadas de volta ao Adobe Analytics. Para conectar o aplicativo móvel ao Adobe Analytics, o arquivo de configuração SDK do Adobe Mobile Services deve ser adicionado ao Adobe Experience Manager.

No bloco Analisar métricas, clique no ícone de seta para expor as entradas do menu Baixar/Fazer upload da configuração do SDK AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

A primeira etapa é obter a configuração do SDK no Adobe Mobile Services. Clique em &quot;Baixar configuração de SDK AMS&quot; para ser redirecionado para o site do Adobe Mobile Services de onde você pode baixar o arquivo de configuração. Depois de obter o arquivo ADBMobileConfig.json, clique em &quot;Fazer upload da configuração do SDK AMS&quot; para fazer upload do arquivo de configuração no AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Clique no botão &quot;Fazer upload da configuração do aplicativo para Adobe Mobile Services&quot;, procure o arquivo ADBMobileConfig.json e clique em &quot;Fazer upload&quot;.

Agora que o aplicativo móvel tem acesso ao arquivo ADBMobileConfig.json, ele tem o conhecimento sobre como se comunicar com o Adobe Analytics e começar a relatar o valor das métricas importantes que ajudam a impulsionar o sucesso de seus aplicativos.

## O que vem a seguir? {#what-s-next}

1. [Iniciar minha experiência com o aplicativo AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gerenciar o conteúdo do meu aplicativo](/help/mobile/phonegap-manage-app-content.md)
1. [Criar meu aplicativo](/help/mobile/building-app-mobile-phonegap.md)
1. [Acompanhe o desempenho do meu aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofereça uma experiência de aplicativo personalizada com o Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensagens importantes aos meus usuários](/help/mobile/phonegap-push-notifications.md)
