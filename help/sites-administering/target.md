---
title: Integração com o Adobe Target
seo-title: Integração com o Adobe Target
description: Saiba mais sobre a integração de AEM com a Adobe Target.
seo-description: Saiba mais sobre a integração de AEM com a Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte do Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e da medição em todos os canais. A Adobe Target é usada pelos comerciantes para projetar e executar testes online, criar segmentos de audiência instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. AEM adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Público alvo, você estará familiarizado com o ambiente de edição de definição de metas no AEM.

Integre seus sites de AEM com o Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use audiências de Públicos alvos para criar experiências personalizadas.
* Envie dados de contexto ao Público alvo quando os visitantes interagirem com suas páginas.
* Rastrear taxas de conversão.

Para integrar ao Público alvo, execute as seguintes tarefas:

1. [Execute tarefas](/help/sites-administering/target-requirements.md) de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor AEM. Sua conta Adobe Target deve ter **aprover **permissões de nível mínimo. Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

1. Ou:

   1. [Optar pelo Adobe Target](/help/sites-administering/opt-in.md): O assistente de aceitação pega as informações da sua conta de Público alvo e cria uma configuração de nuvem da Adobe Target e uma Estrutura de Públicos alvos. O assistente também associa seus sites à Estrutura do Público alvo. Se o assistente não conseguir se conectar ao público alvo, consulte a seção [problemas de conexão](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems). Em seguida, você pode [Modificar as configurações de nuvem padrão](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Se necessário, modifique a configuração e a estrutura da nuvem criadas pelo assistente de aceitação. Por exemplo, modifique a estrutura para enviar dados de contexto adicionais ao Público alvo. Se quiser usar o Adobe Analytics como uma fonte de relatórios para o Adobe Target, você precisará modificar a configuração da nuvem para apontar para a configuração A4T.
   1. [Integrar manualmente ao Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar Atividades](/help/sites-authoring/activitylib.md): Associe suas Atividades à configuração da nuvem do Público alvo.

>[!NOTE]
>
>Consulte também [Integração de AEM com Adobe Target e Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se você estiver usando um Público alvo com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* O 3.x está configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* O 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>É necessário proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração estiver concluída, você poderá [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md) que envia dados do visitante para a Adobe Target. Observe que os componentes da página exigem um código específico para permitir a definição de metas de conteúdo. (Consulte [Desenvolvimento de conteúdo direcionado](/help/sites-developing/target.md).)

>[!NOTE]
>
>Quando você público alvo um componente AEM autor, o componente faz uma série de chamadas do lado do servidor para a Adobe Target para registrar a campanha, configurar o oferta e recuperar segmentos Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita AEM publicação para a Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

Integrar AEM com a Adobe Target requer conhecimento do Adobe Target, gerenciamento AEM Atividade e gerenciamento AEM Audiência. Familiarize-se com as seguintes informações:

* Adobe Target (Consulte a [documentação do Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* AEM console do Atividade (Consulte [Gerenciando Atividade](/help/sites-authoring/activitylib.md)).
* AEM Audiências (Consulte [Gerenciando Audiência](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Ao trabalhar com a Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

>



