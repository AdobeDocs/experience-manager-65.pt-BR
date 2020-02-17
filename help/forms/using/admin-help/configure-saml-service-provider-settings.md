---
title: Definir configurações do provedor de serviços SAML
seo-title: Definir configurações do provedor de serviços SAML
description: Você pode configurar as configurações do provedor de serviços SAML para permitir que os usuários façam logon e se autentiquem em formulários AEM por meio de um provedor de identidade de terceiros (IDP) especificado.
seo-description: Você pode configurar as configurações do provedor de serviços SAML para permitir que os usuários façam logon e se autentiquem em formulários AEM por meio de um provedor de identidade de terceiros (IDP) especificado.
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Definir configurações do provedor de serviços SAML{#configure-saml-service-provider-settings}

O SAML (Security Assertion Markup Language) é uma das opções que você pode selecionar ao configurar a autorização para um domínio corporativo ou híbrido. O SAML é usado principalmente para suportar SSO em vários domínios. Quando o SAML é configurado como seu provedor de autenticação, os usuários fazem logon e se autenticam em formulários AEM por meio de um provedor de identidade de terceiros (IDP) especificado.

Para obter uma explicação do SAML, consulte [Security Assertion Markup Language (SAML) V2.0 Technical Overview](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurações do provedor de serviços SAML.
1. Na caixa ID de entidade do provedor de serviços, digite uma ID exclusiva para usar como identificador para a implementação do provedor de serviços de formulários AEM. Você também especifica essa ID exclusiva ao configurar seu IDP (por exemplo, `um.lc.com`.) Você também pode usar o URL usado para acessar formulários AEM (por exemplo, `https://AEMformsserver`).
1. Na caixa URL base do provedor de serviços, digite o URL básico para o servidor de formulários (por exemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que formulários AEM enviem solicitações de autenticação assinadas ao IDP, execute as seguintes tarefas:

   * Use o Gerenciador de confiança para importar uma credencial no formato PKCS #12 com a Credencial de assinatura do documento selecionada como Tipo de armazenamento de confiança. (Consulte [Gerenciamento de credenciais](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)locais.)
   * Na lista Alias da Chave de Credencial do Provedor de Serviços, selecione o alias atribuído à credencial no Repositório de Confiança.
   * Clique em Exportar para salvar o conteúdo do URL em um arquivo e depois importe esse arquivo para seu IDP.

1. (Opcional) Na lista Diretiva de ID do nome do provedor de serviços, selecione o formato do nome que o IDP usa para identificar o usuário em uma asserção SAML. As opções são Não especificado, Email e Nome qualificado do domínio do Windows.

   >[!NOTE]
   >
   >Os formatos de nome não fazem distinção entre maiúsculas e minúsculas.

1. (Opcional) Selecione Ativar prompt de autenticação para usuários locais. Quando essa opção for selecionada, os usuários verão dois links:

   * um link para a página de logon do provedor de identidade SAML de terceiros, onde os usuários que pertencem a um domínio Enterprise podem autenticar.
   * um link para a página de logon de formulários do AEM, onde os usuários que pertencem a um domínio local podem se autenticar.
   Quando essa opção não estiver selecionada, os usuários serão direcionados diretamente para a página de logon do provedor de identidade SAML de terceiros, onde os usuários que pertencem a um domínio Enterprise podem autenticar.

1. (Opcional) Selecione Ativar vínculo de artefato para ativar o suporte para vínculo de artefato. Por padrão, o vínculo POST é usado com SAML. Mas se você tiver configurado o Vínculo de artefato, selecione esta opção. Quando essa opção é selecionada, a asserção do usuário real não é transmitida pela solicitação do navegador. Em vez disso, um ponteiro para a asserção é transmitido e a asserção é recuperada usando uma chamada de serviço da Web de backend.
1. (Opcional) Selecione Ativar vínculo redirecionado para suportar vínculos SAML que usam redirecionamentos.
1. (Opcional) Em Propriedades personalizadas, especifique propriedades adicionais. As propriedades adicionais são pares name=value separados por novas linhas.

   * Você pode configurar formulários AEM para emitir uma asserção SAML para um período de validade que corresponda ao período de validade de uma asserção de terceiros. Para cumprir o limite de tempo de asserção SAML de terceiros, adicione a seguinte linha em Propriedades personalizadas:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Adicione a seguinte propriedade personalizada para usar RelayState para determinar o URL no qual o usuário será redirecionado após a autenticação bem-sucedida.

      `saml.sp.use.relaystate=true`

   * Adicione a seguinte propriedade personalizada para configurar o URL para o Java Server Pages (JSP) personalizado, que será usado para renderizar a lista registrada de provedores de identidade. Se você não implantou um aplicativo da Web personalizado, ele usará a página Gerenciamento de usuários padrão para renderizar a lista.
   `saml.sp.discovery.url=/custom/custom.jsp`

1. Clique em Salvar.

