---
title: Integração com o Adobe Target
seo-title: Integração com o Adobe Target
description: Saiba mais sobre a integração do AEM com o Adobe Target.
seo-description: Saiba mais sobre a integração do AEM com o Adobe Target.
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

Como parte do Adobe Marketing Cloud, o [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e medição em todos os canais. O Adobe Target é usado pelos comerciantes para projetar e executar testes online, criar segmentos de audiência instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. O AEM adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Target, estará familiarizado com o ambiente de edição de definição de metas no AEM.

Integre seus sites do AEM com a Adobe Target para personalizar conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use audiências de Públicos alvos para criar experiências personalizadas.
* Envie dados de contexto ao Público alvo quando os visitantes interagirem com suas páginas.
* Rastrear taxas de conversão.

Para integrar ao Público alvo, execute as seguintes tarefas:

1. [Execute tarefas](/help/sites-administering/target-requirements.md)de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor de AEM. Sua conta Adobe Target deve ter **aprover **permissões de nível mínimo. Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

1. Ou:

   1. [Optar pela Adobe Target](/help/sites-administering/opt-in.md): O assistente de aceitação pega as informações da sua conta de Público alvo e cria uma configuração de nuvem de Adobe Target e uma Estrutura de Públicos alvos. O assistente também associa seus sites à Estrutura do Público alvo. Se o assistente não conseguir se conectar ao público alvo, consulte a seção Solução de problemas de [conexão](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) . Em seguida, é possível [modificar as configurações](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)padrão da nuvem: Se necessário, modifique a configuração e a estrutura da nuvem criadas pelo assistente de aceitação. Por exemplo, modifique a estrutura para enviar dados de contexto adicionais ao Público alvo. Se você quiser usar o Adobe Analytics como uma fonte de relatórios para o Adobe Target, é necessário modificar a configuração da nuvem para apontar para a configuração A4T.
   1. [Integre manualmente ao Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar Atividades](/help/sites-authoring/activitylib.md): Associe suas Atividades à configuração da nuvem do Público alvo.

>[!NOTE]
>
>Consulte também [Integrar o AEM ao Adobe Target e ao Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se você estiver usando um Público alvo com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
>
>* 3.x é configurado com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x é configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) for detailed information.

Quando a integração estiver concluída, você poderá [criar conteúdo](/help/sites-authoring/content-targeting-touch.md) direcionado que envie dados do visitante para o Adobe Target. Observe que os componentes da página exigem um código específico para permitir a definição de metas de conteúdo. (Consulte [Desenvolvimento de conteúdo](/help/sites-developing/target.md)direcionado.)

>[!NOTE]
>
>Quando você público alvo um componente no autor de AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target para registrar a campanha, configurar o oferta e recuperar segmentos de Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

A integração do AEM com o Adobe Target requer conhecimento sobre Adobe Target, gerenciamento do AEM Atividade e gerenciamento do AEM Audiência. Familiarize-se com as seguintes informações:

* Adobe Target (Consulte a documentação [do](https://docs.adobe.com/content/help/en/target/using/target-home.html)Adobe Target).
* Console do AEM Atividade (consulte [Gerenciamento do Atividade](/help/sites-authoring/activitylib.md)).
* Audiências AEM (Consulte [Gerenciamento de Audiências](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Ao trabalhar com Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios

>



