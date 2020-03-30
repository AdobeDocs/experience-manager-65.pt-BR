---
title: Configurando o Connector para Microsoft SharePoint
seo-title: Configurando o Connector para Microsoft SharePoint
description: Configure o Connector para Microsoft SharePoint para permitir a comunicação entre formulários AEM e Microsoft SharePoint.
seo-description: Configure o Connector para Microsoft SharePoint para permitir a comunicação entre formulários AEM e Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurando o Connector para Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

O Connector for Microsoft SharePoint permite a comunicação entre formulários AEM e Microsoft SharePoint. Para obter informações adicionais de plano de fundo, consulte &quot;Conectores para ECM&quot; na Referência [de](https://www.adobe.com/go/learn_aemforms_services_63)serviços.

1. No console de administração, clique em Serviços > Conector para Microsoft SharePoint.
1. Especifique as seguintes configurações para o SharePoint Server:

   **Nome do Host do SharePoint Server:** O número da porta do nome do host do aplicativo da Web no servidor SharePoint, no formato `[hostname]:'port'`.

   **Nome do usuário:** A conta de usuário usada para se conectar ao servidor SharePoint.

   **Senha:** Senha da conta de usuário usada para conexão com o servidor SharePoint

   **Nome do domínio:** Domínio onde o servidor SharePoint está localizado.

1. Clique em Salvar.

## Serviço de configuração do Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

O serviço de configuração do Microsoft SharePoint `(MSSharePointConfigService)` permite especificar credenciais para o usuário de formulários AEM que tem permissões de representação. Para obter informações sobre permissões de representação, consulte [Configuração do Conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Siga estas etapas para especificar configurações para `MSSharePointConfigService`:

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Navegue na lista de serviços e clique em `MSSharePointConfigService`.
1. Especifique as seguintes configurações na página Configuração:

   * Nome De Usuário Para Um Usuário Com Permissões De Representação
   * Senha Para O Usuário Acima

1. Clique em Salvar.

