---
title: Integração com o Adobe Sign | Manuseio de dados do usuário
description: Saiba mais sobre a integração do AEM Forms com o Adobe Sign para assinaturas eletrônicas em formulários adaptáveis. Ele oferece suporte a várias opções de assinatura para vários workflows.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Integração com o Adobe Sign | Manuseio de dados do usuário {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] integra-se com[!DNL  Adobe Sign] permitir workflows de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para workflows jurídicos, de vendas, de folha de pagamento e de gerenciamento de recursos humanos. Ele permite assinar formulários com um único usuário e vários usuários, fluxos de trabalho de assinatura sequenciais e simultâneas, assinar formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um signatário ou vários signatários assinam e enviam um formulário adaptável, um [!DNL Adobe Sign] é gerado um contrato que inclui informações sobre os signatários.

Para obter mais informações sobre [!DNL AEM Forms] integração com [!DNL Adobe Sign], consulte [Uso do Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

## Dados do usuário e armazenamentos de dados {#data}

[!DNL Adobe Sign] o formulário adaptável ativado inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptável. A variável [!DNL Adobe Sign] serviço salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo em um [!DNL Adobe Sign] servidor configurado em [!DNL AEM Forms] serviços em nuvem. Além disso, se o formulário adaptável estiver configurado para usar a ação enviar do Forms Portal, os dados do contrato serão salvos no armazenamento de dados do Forms Portal junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados no contrato, mas não são salvos em nenhuma tabela de serviço. [!DNL Adobe Sign] O permite que os administradores façam suas próprias escolhas no gerenciamento dos dados que controlam no serviço. Administradores de privacidade na [!DNL Adobe Sign] o serviço pode listar ou remover contratos com base no endereço de email de um solicitante.

[!DNL Adobe Sign] O oferece uma aplicação web que permite pesquisar contratos pelos participantes e, se necessário, excluí-los. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações do usuário](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Forms Portal também são salvos no armazenamento de dados do Forms Portal. Para acessar e excluir dados do armazenamento de dados do Forms Portal, consulte [Portal Forms | Manuseio de dados do usuário](/help/forms/using/forms-portal-handling-user-data.md).
