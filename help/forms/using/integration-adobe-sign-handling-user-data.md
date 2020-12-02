---
title: Integração com a Adobe Sign | Tratamento de dados de utilizadores
seo-title: Integração com a Adobe Sign | Tratamento de dados de utilizadores
description: Integração com a Adobe Sign | Tratamento de dados de utilizadores
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Integração com a Adobe Sign | Tratamento de dados do usuário {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integra [!DNL  Adobe Sign] sem ativar workflows de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para workflows legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos. Ele permite a assinatura de um único usuário e de vários usuários, workflows de assinatura sequenciais e simultâneos, a assinatura de formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um assinante ou vários signatários assinam e enviam um formulário adaptável, um [!DNL Adobe Sign] contrato é gerado que inclui informações sobre os signatários.

Para obter mais informações sobre a integração [!DNL AEM Forms] com [!DNL Adobe Sign], consulte [Usar o Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

## Os dados do usuário e os armazenamentos de dados {#data}

[!DNL Adobe Sign] o formulário adaptativo habilitado inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptativo. O serviço [!DNL Adobe Sign] salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo no servidor [!DNL Adobe Sign] configurado nos serviços em nuvem [!DNL AEM Forms]. Além disso, se o formulário adaptativo estiver configurado para usar a ação de envio do Forms Portal, os dados do contrato serão salvos no armazenamento de dados do portal de formulários junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados dentro do contrato, mas não são salvos em nenhuma das tabelas de serviço. [!DNL Adobe Sign] permite que os administradores façam suas próprias escolhas no gerenciamento de dados que controlam no serviço. Os administradores de privacidade no serviço [!DNL Adobe Sign] podem lista ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] oferta um aplicativo da Web que permite a pesquisa de contratos por participantes e, se necessário, a exclusão deles. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações do usuário](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Forms Portal também são salvos no armazenamento de dados do portal de formulários. Para acessar e excluir dados do repositório de dados do portal de formulários, consulte [Portal da Forms | Tratamento de dados do usuário](/help/forms/using/forms-portal-handling-user-data.md).
