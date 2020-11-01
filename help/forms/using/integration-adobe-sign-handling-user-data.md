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


# Integração com a Adobe Sign | Tratamento de dados de utilizadores {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integra-se com[!DNL  Adobe Sign] o para permitir que workflows de assinatura eletrônica em formulários adaptáveis processem formulários ou contratos para workflows legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos. Ele permite a assinatura de um único usuário e de vários usuários, workflows de assinatura sequenciais e simultâneos, a assinatura de formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um assinante ou vários assinantes assinam e enviam um formulário adaptável, um [!DNL Adobe Sign] contrato que inclui informações sobre os signatários é gerado.

Para obter mais informações sobre [!DNL AEM Forms] integração com [!DNL Adobe Sign], consulte [Usar o Adobe Sign em um formulário](/help/forms/using/working-with-adobe-sign.md)adaptável.

## Armazenamento de dados e dados do usuário {#data}

[!DNL Adobe Sign] o formulário adaptativo habilitado inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptativo. O [!DNL Adobe Sign] serviço salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo no [!DNL Adobe Sign] servidor configurado nos serviços [!DNL AEM Forms] em nuvem. Além disso, se o formulário adaptativo estiver configurado para usar a ação de envio do Forms Portal, os dados do contrato serão salvos no armazenamento de dados do portal de formulários junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados dentro do contrato, mas não são salvos em nenhuma das tabelas de serviço. [!DNL Adobe Sign] permite que os administradores façam suas próprias escolhas no gerenciamento de dados que controlam no serviço. Os administradores de privacidade no [!DNL Adobe Sign] serviço podem lista ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] oferta um aplicativo da Web que permite a pesquisa de contratos por participantes e, se necessário, a exclusão deles. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)do usuário.

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Forms Portal também são salvos no armazenamento de dados do portal de formulários. Para acessar e excluir dados do repositório de dados do portal de formulários, consulte Portal da [Forms | Tratamento de dados](/help/forms/using/forms-portal-handling-user-data.md)do utilizador.
