---
title: Integração com o Adobe Sign| Tratamento de dados de utilizadores
seo-title: Integração com o Adobe Sign| Tratamento de dados de utilizadores
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integração com o Adobe Sign| Tratamento de dados de utilizadores {#integration-with-adobe-sign-handling-user-data}

O AEM Forms integra-se ao Adobe Sign para permitir fluxos de trabalho de assinatura eletrônica em formulários adaptáveis para processar formulários ou contratos para fluxos de trabalho legais, de vendas, de folha de pagamento e de gerenciamento de recursos humanos. Ele permite a assinatura de usuário único e multiusuário, fluxos de trabalho de assinatura sequenciais e simultâneos, a assinatura de formulários como um usuário anônimo ou conectado e várias maneiras de autenticar usuários.

Quando um assinante ou vários signatários assinam e enviam um formulário adaptável, um contrato do Adobe Sign é gerado e inclui informações sobre os signatários.

Para obter mais informações sobre a integração do AEM Forms com o Adobe Sign, consulte [Usar o Adobe Sign em um formulário](/help/forms/using/working-with-adobe-sign.md)adaptável.

## Armazenamento de dados e dados do usuário {#data}

O formulário adaptativo habilitado para o Adobe Sign inclui informações sobre os signatários e pode incluir outros dados do usuário coletados pelo formulário adaptativo. O serviço Adobe Sign salva os dados do usuário com a assinatura dentro do contrato. O contrato é salvo no servidor Adobe Sign configurado nos serviços em nuvem do AEM Forms. Além disso, se o formulário adaptativo estiver configurado para usar a ação de envio do Portal do Forms , os dados do contrato serão salvos no armazenamento de dados do portal de formulários junto com os dados do formulário.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Os dados do usuário são coletados dentro do contrato, mas não são salvos em nenhuma das tabelas de serviço. O Adobe Sign permite que os administradores façam suas próprias escolhas no gerenciamento de dados que controlam no serviço. Os administradores de privacidade do serviço Adobe Sign podem listar ou remover contratos com base no endereço de email de um solicitante.

O Adobe Sign oferece um aplicativo da Web que permite a pesquisa de contratos por participantes e, se necessário, a exclusão deles. Para obter mais informações, consulte [Adobe Sign - Recurso: Excluir informações](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)do usuário.

Os dados de contratos para formulários adaptáveis configurados para usar a ação de envio do Portal de Formulários também são salvos no armazenamento de dados do portal de formulários. Para acessar e excluir dados do repositório de dados do portal de formulários, consulte Portal do [Forms| Tratamento de dados](/help/forms/using/forms-portal-handling-user-data.md)do utilizador.
