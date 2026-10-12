---
title: Execução de formulários do AEM no modo de manutenção
description: O modo de manutenção é útil ao executar tarefas como corrigir um DSC, atualizar formulários do AEM ou aplicar um service pack. Saiba mais sobre como executar formulários do AEM no modo de manutenção.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%
---
# Execução de formulários do AEM no modo de manutenção {#running-aem-forms-in-maintenance-mode}

O modo de manutenção é útil ao executar tarefas como corrigir um DSC, atualizar formulários do AEM ou aplicar um service pack.

Evite chamar processos enquanto o servidor estiver no modo de manutenção. Isso é o que acontece se um processo é chamado enquanto o servidor está no modo de manutenção:

* Se o processo for de longa duração, ele será adicionado ao banco de dados de jobs, mas não será iniciado. Ao sair do modo de manutenção, o AEM Forms processa as tarefas de longa duração em sua fila, mesmo que o servidor tenha sido reiniciado enquanto estava no modo de manutenção.
* Se o processo tiver vida curta, ele será processado imediatamente.

**Colocar formulários do AEM no modo de manutenção**

1. Em um navegador da Web, digite:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Uma mensagem &quot;now paused&quot; é exibida na janela do navegador.

   >[!NOTE]
   >
   >Se você desligar o servidor enquanto ele estiver no modo de manutenção, ele ainda estará no modo de manutenção quando for reiniciado. Desative o modo de manutenção quando terminar suas tarefas de manutenção.

**Verifique se o AEM Forms está em execução no modo de manutenção**

1. Em um navegador da Web, digite:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   O status é exibido na janela do navegador. Um status &quot;true&quot; indica que o servidor está sendo executado no modo de manutenção e &quot;false&quot; indica que o servidor não está no modo de manutenção.

**Desativar modo de manutenção**

1. Em um navegador da Web, digite:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Uma mensagem &quot;now running&quot; é exibida na janela do navegador.
