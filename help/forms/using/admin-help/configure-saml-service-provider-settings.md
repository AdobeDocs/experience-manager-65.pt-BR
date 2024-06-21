---
title: Definir configurações do provedor de serviços SAML
description: Você pode definir as configurações do provedor de serviços SAML para permitir que os usuários façam logon e se autentiquem em formulários AEM por meio de um provedor de identidade de terceiros (IDP) especificado.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Definir configurações do provedor de serviços SAML{#configure-saml-service-provider-settings}

A SAML (Security Assertion Markup Language) é uma das opções que você pode selecionar ao configurar a autorização para um domínio corporativo ou híbrido. O SAML é usado principalmente para oferecer suporte a SSO em vários domínios. Quando o SAML é configurado como seu provedor de autenticação, os usuários fazem logon e se autenticam em formulários AEM por meio de um provedor de identidade de terceiros (IDP) especificado.

Para obter uma explicação sobre SAML, consulte [Visão geral técnica da Security Assertion Markup Language (SAML) V2.0](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurações do Provedor de serviço SAML.
1. Na caixa ID de entidade do provedor de serviços, digite um ID exclusivo para usar como um identificador para a implementação do provedor de serviços dos formulários AEM. Você também especifica esse identificador exclusivo ao configurar seu IDP (por exemplo, `um.lc.com`.) Você também pode usar o URL usado para acessar formulários AEM (por exemplo, `https://AEMformsserver`).
1. Na caixa URL de base do provedor de serviços, digite o URL de base do seu servidor Forms (por exemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que os formulários AEM enviem solicitações de autenticação assinadas ao IDP, execute as seguintes tarefas:

   * Use o Gerenciador de Confiança para importar uma credencial no formato PKCS #12 com a Credencial de assinatura de documento selecionada como o Tipo de armazenamento de confiança. (Consulte [Gerenciar credenciais locais](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Na lista Alias da chave de credencial do provedor de serviços, selecione o alias atribuído à credencial no armazenamento de confiança.
   * Clique em Exportar para salvar o conteúdo do URL em um arquivo e, em seguida, importar esse arquivo para o IDP.

1. (Opcional) Na lista Política de ID de nome do provedor de serviços, selecione o formato de nome que o IDP usa para identificar o usuário em uma asserção SAML. As opções são Não especificado, Email e Nome qualificado de domínio do Windows.

   >[!NOTE]
   >
   >Os formatos de nome não diferenciam maiúsculas de minúsculas.

1. (Opcional) Selecione Habilitar Prompt De Autenticação Para Usuários Locais. Quando essa opção é selecionada, os usuários veem dois links:

   * um link para a página de logon do provedor de identidade SAML de terceiros, em que os usuários que pertencem a um domínio Enterprise podem se autenticar.
   * um link para a página de logon dos formulários AEM, onde os usuários que pertencem a um domínio Local podem se autenticar.

   Quando essa opção não está selecionada, os usuários são direcionados diretamente para a página de logon do provedor de identidade SAML de terceiros, onde os usuários que pertencem a um domínio Enterprise podem se autenticar.

1. (Opcional) Selecione Ativar vinculação de artefato para ativar o suporte à vinculação de artefato. Por padrão, a vinculação de POST é usada com SAML. Mas se você tiver configurado a Associação de Artefato, selecione essa opção. Quando essa opção é selecionada, a asserção do usuário real não é passada pela solicitação do navegador. Em vez disso, um ponteiro para a asserção é transmitido e a asserção é recuperada usando uma chamada de serviço da Web de back-end.
1. (Opcional) Selecione Ativar Vinculação Redirecionada para suportar vinculações SAML que usam redirecionamentos.
1. (Opcional) Em Propriedades personalizadas, especifique propriedades adicionais. As propriedades adicionais são pares nome=valor separados por novas linhas.

   * Você pode configurar formulários AEM para emitir uma asserção SAML para um período de validade que corresponda ao período de validade de uma asserção de terceiros. Para respeitar o tempo limite de asserção SAML de terceiros, adicione a seguinte linha em Propriedades personalizadas:

     `saml.sp.honour.idp.assertion.expiry=true`

   * Adicione a seguinte propriedade personalizada para usar RelayState para determinar a URL para a qual o usuário será redirecionado após a autenticação bem-sucedida.

     `saml.sp.use.relaystate=true`

   * Adicione a seguinte propriedade personalizada para que você possa configurar o URL para as Java™ Server Pages (JSP) personalizadas, que são usadas para renderizar a lista registrada de provedores de identidade. Se você não tiver implantado uma aplicação web personalizada, ela usará a página padrão Gerenciamento de usuários para renderizar a lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Clique em Salvar.
