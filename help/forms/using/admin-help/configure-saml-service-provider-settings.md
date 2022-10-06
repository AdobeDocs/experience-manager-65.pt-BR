---
title: Definir configurações do provedor de serviços SAML
seo-title: Configure SAML service provider settings
description: É possível definir as configurações do provedor de serviços SAML para permitir que os usuários façam logon e se autenticem AEM formulários por meio de um provedor de identidade de terceiros (IDP) especificado.
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Definir configurações do provedor de serviços SAML{#configure-saml-service-provider-settings}

O SAML (Security Assertion Markup Language) é uma das opções que você pode selecionar ao configurar a autorização para um domínio enterprise ou híbrido. O SAML é usado principalmente para oferecer suporte ao SSO em vários domínios. Quando o SAML é configurado como seu provedor de autenticação, os usuários fazem logon e se autenticam para AEM formulários por meio de um provedor de identidade de terceiros (IDP) especificado.

Para obter uma explicação sobre SAML, consulte [Linguagem de marcação de asserção de segurança (SAML) V2.0 Visão geral técnica](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurações do provedor de serviços SAML.
1. Na caixa ID da entidade do provedor de serviços, digite uma ID exclusiva para usar como um identificador para a implementação do provedor de serviços de formulários AEM. Você também especifica essa ID exclusiva ao configurar sua IDP (por exemplo, `um.lc.com`.) Também é possível usar o URL usado para acessar formulários AEM (por exemplo, `https://AEMformsserver`).
1. Na caixa URL base do provedor de serviços , digite o URL básico do servidor de formulários (por exemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que formulários AEM enviem solicitações de autenticação assinadas para o IDP, execute as seguintes tarefas:

   * Use o Gerenciador de Confiança para importar uma credencial no formato PKCS #12 com Credencial de Assinatura de Documento selecionada como o Tipo de Armazenamento de Confiança. (Consulte [Gerenciamento de credenciais locais](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Na lista Alias da Chave de Credencial do Provedor de Serviços, selecione o alias atribuído à credencial no Armazenamento de Confiança.
   * Clique em Exportar para salvar o conteúdo do URL em um arquivo e, em seguida, importe esse arquivo para o IDP.

1. (Opcional) Na lista Política de ID do nome do provedor de serviços, selecione o formato do nome que o IDP usa para identificar o usuário em uma asserção SAML. As opções são Não especificado, Email e Nome Qualificado de Domínio do Windows.

   >[!NOTE]
   >
   >Os formatos de nome não fazem distinção entre maiúsculas e minúsculas.

1. (Opcional) Selecione Ativar Prompt De Autenticação Para Usuários Locais. Quando essa opção for selecionada, os usuários verão dois links:

   * um link para a página de logon do provedor de identidade SAML de terceiros, onde os usuários que pertencem a um domínio Enterprise podem ser autenticados.
   * um link para a página de logon dos formulários AEM, onde os usuários que pertencem a um domínio Local podem se autenticar.

   Quando essa opção não estiver selecionada, os usuários serão direcionados para a página de logon do provedor de identidade SAML de terceiros, onde os usuários que pertencem a um domínio Enterprise poderão ser autenticados.

1. (Opcional) Selecione Ativar vínculo de artefato para ativar o suporte de vínculo de artefato. Por padrão, a vinculação de POST é usada com SAML. Mas, se tiver configurado o Vínculo de artefato, selecione esta opção. Quando essa opção é selecionada, a asserção de usuário real não é passada pela solicitação do Navegador. Em vez disso, um ponteiro para a asserção é passado e a asserção é recuperada usando uma chamada de serviço da Web de backend.
1. (Opcional) Selecione Ativar Vínculo Redirecionado para oferecer suporte a vínculos SAML que usam redirecionamentos.
1. (Opcional) Em Propriedades personalizadas, especifique propriedades adicionais. As propriedades adicionais são pares name=value separados por novas linhas.

   * Você pode configurar AEM formulários para emitir uma asserção SAML para um período de validade que corresponda ao período de validade de uma asserção de terceiros. Para honrar o tempo limite da asserção SAML de terceiros, adicione a seguinte linha em Propriedades personalizadas:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Adicione a seguinte propriedade personalizada para usar RelayState para determinar o URL onde o usuário será redirecionado após a autenticação bem-sucedida.

      `saml.sp.use.relaystate=true`

   * Adicione a seguinte propriedade personalizada para configurar o URL para as páginas personalizadas do servidor Java (JSP), que será usada para renderizar a lista registrada de provedores de identidade. Se você não tiver implantado uma aplicação Web personalizada, ela usará a página Gerenciamento de usuários padrão para renderizar a lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Clique em Salvar.
