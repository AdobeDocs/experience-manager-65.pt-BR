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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio da definição de metas e medição em todos os canais. O Adobe Target é usado por profissionais de marketing para projetar e executar testes online, criar segmentos de público-alvo instantâneos (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online. O AEM adotou o fluxo de trabalho de definição de metas usado no Adobe Target Standard. Se você usar o Target, estará familiarizado com o ambiente de edição de definição de metas no AEM.

Integre seus sites do AEM ao Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente a definição de metas de conteúdo.
* Use públicos-alvo do Target para criar experiências personalizadas.
* Envie dados de contexto ao Target quando os visitantes interagirem com suas páginas.
* Rastrear as taxas de conversão.

Para integrar-se ao Target, execute as seguintes tarefas:

1. [Execute tarefas](/help/sites-administering/target-requirements.md)de pré-requisito: Registre-se no Adobe Target e configure certos aspectos da instância do autor do AEM. Sua conta do Adobe Target deve ter **aprover **permissões de nível no mínimo. Além disso, você deve proteger as configurações de atividade no nó de publicação para que ele fique inacessível aos usuários.

1. Ou:

   1. [Optar pelo Adobe Target](/help/sites-administering/opt-in.md): O assistente de aceitação coleta as informações de sua conta do Target e cria uma configuração de nuvem do Adobe Target e uma estrutura do Target. O assistente também associa seus sites à estrutura do Target. Se o assistente não conseguir se conectar ao destino, consulte a seção Solução de problemas de [conexão](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) . Em seguida, é possível [modificar as configurações](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)padrão da nuvem: Se necessário, modifique a configuração e a estrutura da nuvem criadas pelo assistente de aceitação. Por exemplo, modifique a estrutura para enviar dados de contexto adicionais ao Target. Se você quiser usar o Adobe Analytics como fonte de geração de relatórios para o Adobe Target, será necessário modificar a configuração da nuvem para apontar para a configuração A4T.
   1. [Integrar-se manualmente ao Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar atividades](/help/sites-authoring/activitylib.md): Associe suas Atividades à configuração da nuvem do Target.

>[!NOTE]
>
>Consulte também [Integração do AEM com o Adobe Target e o Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do Cliente HTTP, já que algumas funcionalidades do AEM estão usando as APIs 3.x e outras as APIs 4.x:
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
>Quando você direciona um componente no autor de AEM, o componente faz uma série de chamadas do servidor para o Adobe Target para registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Target.

## Fontes de informações de plano de fundo {#background-information-sources}

A integração do AEM com o Adobe Target requer conhecimento do Adobe Target, gerenciamento de atividades do AEM e gerenciamento de públicos-alvo do AEM. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a documentação [do](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* Console de atividades do AEM (consulte [Gerenciamento de atividades](/help/sites-authoring/activitylib.md)).
* Públicos-alvo do AEM (consulte [Gerenciamento de públicos-alvo](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatório
>



