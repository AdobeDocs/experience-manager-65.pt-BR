---
title: Integração com o Adobe Sign | Manipulação de dados do usuário
seo-title: Integration with Adobe Sign | Handling user data
description: Integração com o Adobe Sign | Manipulação de dados do usuário
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Integração com o Adobe Sign | Manipulação de dados do usuário {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integra-se com[!DNL  Adobe Sign] permitir workflows de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para workflows jurídicos, de vendas, de folha de pagamento e de gerenciamento de recursos humanos. Ele permite assinar formulários com um único usuário e vários usuários, fluxos de trabalho de assinatura sequenciais e simultâneas, assinar formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um signatário ou vários signatários assinam e enviam um formulário adaptável, um [!DNL Adobe Sign] é gerado um contrato que inclui informações sobre os signatários.

Para obter mais informações sobre [!DNL AEM Forms] integração com [!DNL Adobe Sign], consulte [Uso do Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

## Dados do usuário e armazenamentos de dados {#data}

[!DNL Adobe Sign] o formulário adaptável ativado inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptável. A variável [!DNL Adobe Sign] serviço salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo em [!DNL Adobe Sign] servidor configurado em [!DNL AEM Forms] serviços em nuvem. Além disso, se o formulário adaptável estiver configurado para usar a ação enviar do Forms Portal, os dados do contrato serão salvos no armazenamento de dados do portal de formulários junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados no contrato, mas não são salvos em nenhuma tabela de serviço. [!DNL Adobe Sign] O permite que os administradores façam suas próprias escolhas no gerenciamento de dados controlados no serviço. Administradores de privacidade na [!DNL Adobe Sign] o serviço pode listar ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] O oferece uma aplicação web que permite pesquisar contratos pelos participantes e, se necessário, excluí-los. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações do usuário](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Forms Portal também são salvos no armazenamento de dados do portal de formulários. Para acessar e excluir dados do armazenamento de dados do portal de formulários, consulte [Portal do Forms | Manipulação de dados do usuário](/help/forms/using/forms-portal-handling-user-data.md).
