---
title: Execução de formulários AEM no modo de manutenção
seo-title: Running AEM forms in maintenance mode
description: O modo de manutenção é útil ao executar tarefas como corrigir um DSC, atualizar formulários AEM ou aplicar um service pack. Saiba mais sobre como executar formulários AEM no modo de manutenção.
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Execução de formulários AEM no modo de manutenção {#running-aem-forms-in-maintenance-mode}

O modo de manutenção é útil ao executar tarefas como corrigir um DSC, atualizar formulários AEM ou aplicar um service pack.

Evite chamar processos enquanto o servidor estiver no modo de manutenção. Isso é o que acontece se um processo é chamado enquanto o servidor está no modo de manutenção:

* Se o processo for de longa duração, ele será adicionado ao banco de dados de jobs, mas não será iniciado. Ao sair do modo de manutenção, o AEM processa os trabalhos de longa duração em sua fila, mesmo que o servidor tenha sido reiniciado enquanto estava no modo de manutenção.
* Se o processo tiver vida curta, ele será processado imediatamente.

**Colocar formulários AEM no modo de manutenção**

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
