---
title: Configuração do conector para o Microsoft SharePoint
description: Configure Connector for Microsoft SharePoint para habilitar a comunicação entre formulários AEM e Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configuração do conector para o Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

O conector para Microsoft SharePoint permite a comunicação entre o AEM forms e o Microsoft SharePoint. Para obter informações adicionais em segundo plano, consulte &quot;Conectores para ECM&quot; na [Referência de Serviços](https://www.adobe.com/go/learn_aemforms_services_63).

1. No console de administração, clique em Serviços > Conector para Microsoft SharePoint.
1. Especifique as seguintes configurações para o SharePoint Server:

   **Nome do Host do SharePoint Server:** O número da porta do nome do host do aplicativo Web no servidor SharePoint, no formato `[hostname]:'port'`.

   **Nome do Usuário:** a conta de usuário usada para se conectar ao servidor do SharePoint.

   **Senha:** Senha da conta de usuário usada para conexão com o servidor do SharePoint

   **Nome do Domínio:** Domínio onde o servidor SharePoint está localizado.

1. Clique em Salvar.

## Serviço de configuração do Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

O serviço de configuração do Microsoft SharePoint `(MSSharePointConfigService)` permite especificar credenciais para o usuário de formulários AEM que tem permissões de representação. Para obter informações sobre permissões de representação, consulte [Configurando o Conector para o Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estas etapas para especificar configurações para `MSSharePointConfigService`:

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Navegue pela lista de serviços e clique em `MSSharePointConfigService`.
1. Especifique as seguintes configurações na página Configuração:

   * Nome De Usuário Para Um Usuário Com Permissões De Representação
   * Senha Do Usuário Acima

1. Clique em Salvar.
