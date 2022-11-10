---
title: Integração com o Adobe Target
seo-title: Integrating with Adobe Target
description: Saiba mais sobre a integração de AEM com o Adobe Target.
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 66%

---

# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) permite aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais. O Adobe Target é usado pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público instantaneamente (com base no comportamento) e automatizar o direcionamento de conteúdo e experiências online. AEM adotou o workflow para construção do target usado no Adobe Target Standard. Se você usar o Target, estará familiarizado com o ambiente de edição de direcionamento no AEM.

Integre o AEM Sites com o Adobe Target para personalizar o conteúdo em suas páginas:

* Implemente o direcionamento de conteúdo.
* Use os públicos do Target para criar experiências personalizadas.
* Envie dados de contexto para o Target quando os visitantes interagirem com suas páginas.
* Rastreie as taxas de conversão.

Para integrar com o Target, execute as seguintes tarefas:

1. [Execute as tarefas de pré-requisito](/help/sites-administering/target-requirements.md): registre-se no Adobe Target e configure determinados aspectos da instância de autor do AEM. Sua conta do Adobe Target deve ter no mínimo permissões **de nível de aprovador **. Além disso, você deve proteger as configurações de atividade no nó de publicação para que elas fiquem inacessíveis aos usuários.

1. Ou:

   1. [Optar pela Adobe Target](/help/sites-administering/opt-in.md): O assistente de aceitação pega as informações da conta do Target e cria uma configuração de nuvem do Adobe Target e uma Estrutura do Target. O assistente também associa seus sites à Estrutura do Target. Se o assistente não conseguir se conectar ao target, consulte o [solução de problemas de conexão](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) seção. Você pode [Modificar as configurações padrão da nuvem](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Se necessário, modifique a configuração e a estrutura da nuvem criadas pelo assistente de aceitação. Por exemplo, modifique a estrutura para enviar dados de contexto adicionais para o Target. Se quiser usar o Adobe Analytics como fonte de relatórios para o Adobe Target, será necessário modificar a configuração da nuvem para apontar para a configuração A4T.
   1. [Integração manual com o Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurar atividades](/help/sites-authoring/activitylib.md): associe suas atividades à configuração de nuvem do Target.

>[!NOTE]
>
>Consulte também [Integração de AEM com o Adobe Target e o Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se você estiver usando o Target com uma configuração de proxy personalizada, precisará configurar ambas as configurações de proxy do cliente HTTP, pois algumas funcionalidades do AEM usam as APIs 3.x e outras usam as APIs 4.x:
>
>* A 3.x está configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* A 4.x está configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>Você deve proteger o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) para obter informações detalhadas.

Quando a integração for concluída, você poderá [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md) que envia dados do visitante para o Adobe Target. Observe que os componentes da página exigem um código específico para ativar o direcionamento de conteúdo. (Consulte [Desenvolvimento de conteúdo direcionado](/help/sites-developing/target.md).)

>[!NOTE]
>
>Ao direcionar um componente no autor do AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita do ambiente de publicação do AEM para o Adobe Target.

## Fontes de informações de segundo plano {#background-information-sources}

A integração do AEM com o Adobe Target requer conhecimento do Adobe Target, gerenciamento de atividades AEM e gerenciamento de AEM públicos-alvo. Familiarize-se com as seguintes informações:

* Adobe Target (consulte a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR)).
* Console de Atividades do AEM (consulte [Gerenciamento de atividades](/help/sites-authoring/activitylib.md)).
* Públicos do AEM (consulte [Gerenciamento de públicos](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Ao trabalhar com o Adobe Target, o número máximo de artefatos permitidos em uma campanha é o seguinte:
>
>* 50 locais
>* 2.000 experiências
>* 50 métricas
>* 50 segmentos de relatórios
>

