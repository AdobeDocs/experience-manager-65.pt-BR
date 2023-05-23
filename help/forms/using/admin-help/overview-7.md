---
title: Noções básicas para configuração de formulários
seo-title: Basics of configuring forms
description: Saiba mais sobre os vários serviços de formulários que ajudam você a criar aplicativos interativos de captura de dados.
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Noções básicas para configuração de formulários {#basics-of-configuring-forms}

O serviço Forms permite criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e fornecem formulários normalmente criados no Designer. Os autores de formulários desenvolvem um único design de formulário que o serviço Forms renderiza em vários formatos:

* como PDF no Adobe Reader ou em um navegador
* como HTML em vários ambientes do navegador, incluindo uma renderização XHTML 1.0 compatível
* como Guias de formulário em vários ambientes de navegador compatíveis com o Flash Player Adobe.

Para obter informações adicionais sobre o serviço Forms, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

Usando a página Forms no console de administração, você pode configurar o comportamento do serviço Forms. Essas configurações se aplicam a todas as invocações do serviço. Quaisquer parâmetros enviados por meio do SDK de formulários AEM substituem as configurações definidas no console de administração; no entanto, eles afetam apenas essa invocação específica.

Depois de alterar as configurações do Forms no console de administração, clique em Salvar. Não é necessário reiniciar o servidor para que as alterações entrem em vigor. No entanto, talvez seja necessário interromper e reiniciar o serviço do Forms ao definir as configurações do modo de cache. (Consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
