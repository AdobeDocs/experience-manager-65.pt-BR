---
title: Integração com o Adobe Sign | Manipulação de dados do usuário
description: Saiba mais sobre a integração do AEM Forms com o Adobe Sign para obter assinaturas eletrônicas em formulários adaptáveis. Ele oferece suporte a várias opções de assinatura para vários workflows.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: a16aea24-4e85-528d-9377-cd80bb039c1d
    internal-label: Acrobat Sign
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%
---
# Integração com o Adobe Sign | Manipulação de dados do usuário {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integra-se com [!DNL  Adobe Sign] para habilitar fluxos de trabalho de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para fluxos de trabalho jurídicos, de vendas, de folha de pagamento e de gerenciamento de recursos humanos. Ele permite assinar formulários com um único usuário e vários usuários, fluxos de trabalho de assinatura sequenciais e simultâneas, assinar formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um signatário ou vários signatários assinam e enviam um formulário adaptável, é gerado um contrato [!DNL Adobe Sign] que inclui informações sobre os signatários.

Para obter mais informações sobre a integração do [!DNL AEM Forms] com o [!DNL Adobe Sign], consulte [Usando o Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

## Dados do usuário e armazenamentos de dados {#data}

O formulário adaptável habilitado para [!DNL Adobe Sign] inclui informações sobre os signatários e pode incluir outros dados de usuário coletados pelo formulário adaptável. O serviço [!DNL Adobe Sign] salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo em um servidor [!DNL Adobe Sign] configurado nos serviços de nuvem [!DNL AEM Forms]. Além disso, se o formulário adaptável estiver configurado para usar a ação enviar do Forms Portal, os dados do contrato serão salvos no armazenamento de dados do Forms Portal junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados no contrato, mas não são salvos em nenhuma tabela de serviço. O [!DNL Adobe Sign] permite que os administradores façam suas próprias escolhas no gerenciamento dos dados que controlam no serviço. Os administradores de privacidade no serviço [!DNL Adobe Sign] podem listar ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] oferece um aplicativo Web que permite a pesquisa de contratos pelos participantes e, se necessário, a exclusão deles. Para obter mais informações, consulte [Adobe Sign - Recurso: excluir informações do usuário](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Forms Portal também são salvos no armazenamento de dados do Forms Portal. Para acessar e excluir dados do armazenamento de dados do Forms Portal, consulte [Forms Portal | Manipulando dados do usuário](/help/forms/using/forms-portal-handling-user-data.md).
