---
title: Configuração do conector para o Microsoft SharePoint
description: Configure o Connector para Microsoft SharePoint para permitir a comunicação entre o AEM Forms e o Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
source-wordcount: '223'
ht-degree: 0%
---

# Configuração do conector para o Microsoft SharePoint

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

O conector para Microsoft SharePoint permite a comunicação entre o AEM Forms e o Microsoft SharePoint. Para obter informações adicionais em segundo plano, consulte &quot;Conectores para ECM&quot; na [Referência de Serviços](https://www.adobe.com/go/learn_aemforms_services_63).

1. No console de administração, clique em Serviços > Conector para Microsoft SharePoint.
2. Especifique as seguintes configurações para o SharePoint Server:

   **Nome do Host do SharePoint Server:** O número da porta do nome do host do aplicativo Web no servidor SharePoint, no formato `[hostname]:'port'`.

   **Nome do Usuário:** a conta de usuário usada para se conectar ao servidor do SharePoint.

   **Senha:** Senha da conta de usuário usada para conexão com o servidor do SharePoint

   **Nome do Domínio:** Domínio onde o servidor SharePoint está localizado.

3. Clique em Salvar.

## Serviço de configuração do Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

O serviço de configuração do Microsoft SharePoint `(MSSharePointConfigService)` permite especificar credenciais para o usuário do AEM Forms que tem permissões de representação. Para obter informações sobre permissões de representação, consulte [Configurando o Conector para o Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estas etapas para especificar configurações para `MSSharePointConfigService`:

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Navegue pela lista de serviços e clique em `MSSharePointConfigService`.
1. Especifique as seguintes configurações na página Configuração:

   * Nome De Usuário Para Um Usuário Com Permissões De Representação
   * Senha Do Usuário Acima

1. Clique em Salvar.
