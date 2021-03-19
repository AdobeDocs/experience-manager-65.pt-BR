---
title: Integração com o Adobe Sign | Tratamento de dados de utilizadores
seo-title: Integração com o Adobe Sign | Tratamento de dados de utilizadores
description: Integração com o Adobe Sign | Tratamento de dados de utilizadores
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Integração com o Adobe Sign | Tratamento de dados do usuário {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] O integra o [!DNL  Adobe Sign] para ativar os fluxos de trabalho de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para fluxos de trabalho legais, de vendas, de folha de pagamento e de gerenciamento de recursos humanos. Ele permite a assinatura única e multiusuário, fluxos de trabalho de assinatura sequenciais e simultâneos, a assinatura de formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um assinante ou vários signatários assinam e enviam um formulário adaptável, um acordo [!DNL Adobe Sign] é gerado, incluindo informações sobre os signatários.

Para obter mais informações sobre a integração [!DNL AEM Forms] com [!DNL Adobe Sign], consulte [Uso do Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

## Os dados e armazenamentos de dados do usuário {#data}

[!DNL Adobe Sign] o formulário adaptável ativado inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptável. O serviço [!DNL Adobe Sign] salva os dados do usuário com a assinatura no contrato. O contrato é salvo no servidor [!DNL Adobe Sign] configurado nos [!DNL AEM Forms] serviços em nuvem. Além disso, se o formulário adaptável estiver configurado para usar a ação de envio do Portal Forms, os dados do contrato serão salvos no armazenamento de dados do portal de formulários junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados dentro do contrato, mas não são salvos em nenhuma das tabelas de serviço. [!DNL Adobe Sign] permite que os administradores façam suas próprias escolhas no gerenciamento de dados que controlam no serviço. Os administradores de privacidade no serviço [!DNL Adobe Sign] podem listar ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] O oferece uma aplicação web que permite pesquisar contratos por participantes e, se necessário, excluí-los. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações do usuário](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Portal Forms também são salvos no armazenamento de dados do portal de formulários. Para acessar e excluir dados do armazenamento de dados do portal de formulários, consulte [Portal do Forms | Manipulação de dados do usuário](/help/forms/using/forms-portal-handling-user-data.md).
