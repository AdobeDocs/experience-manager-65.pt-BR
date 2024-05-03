---
title: Noções básicas para configuração de formulários
description: Saiba mais sobre os vários serviços de formulários que ajudam você a criar aplicativos interativos de captura de dados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '197'
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
