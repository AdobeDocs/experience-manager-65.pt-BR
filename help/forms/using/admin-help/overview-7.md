---
title: Noções básicas sobre a configuração de formulários
seo-title: Noções básicas sobre a configuração de formulários
description: Saiba mais sobre os vários serviços de formulários que ajudam a criar aplicativos interativos de captura de dados.
seo-description: Saiba mais sobre os vários serviços de formulários que ajudam a criar aplicativos interativos de captura de dados.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Noções básicas sobre a configuração de formulários {#basics-of-configuring-forms}

O serviço Forms permite que você crie aplicativos clientes de captura de dados interativos que validam, processam, transformam e entregam formulários normalmente criados no Designer. Os autores de formulários desenvolvem um design de formulário único que o serviço Forms renderiza em vários formatos:

* como PDF no Adobe Reader ou em um navegador
* como HTML em vários ambientes de navegador, incluindo uma renderização XHTML 1.0 compatível
* como guias de formulário em vários ambientes do navegador que suportam o Flash Player Adobe.

Para obter informações adicionais sobre o serviço Forms, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

Usando a página do Forms no console de administração, você pode configurar o comportamento do serviço Forms. Essas configurações se aplicam a todas as invocações do serviço. Todos os parâmetros enviados pelo SDK de formulários AEM substituem as configurações definidas no console de administração; no entanto, afetam apenas essa invocação em particular.

Depois de alterar as configurações do Forms no console de administração, clique em Salvar. Não é necessário reiniciar o servidor para que as alterações entrem em vigor. No entanto, talvez seja necessário parar e reiniciar o serviço Forms ao configurar as configurações do modo de cache. (Consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
