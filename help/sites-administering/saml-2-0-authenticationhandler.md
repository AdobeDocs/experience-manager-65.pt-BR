---
title: Manipulador de autenticação SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: Saiba mais sobre o SAML 2.0 Authentication Handler no AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6bc60122d2512a6f58c0204cd240a1b99a37ed93
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 1%

---

# Manipulador de autenticação SAML 2.0{#saml-authentication-handler}

AEM vem com um manipulador de autenticação [SAML](http://saml.xml.org/saml-specifications). Este manipulador fornece suporte para o [SAML](http://saml.xml.org/saml-specifications) Protocolo de solicitação de autenticação 2.0 (perfil Web-SSO) usando o vínculo `HTTP POST`.

Ele suporta:

* assinatura e criptografia de mensagens
* criação automática de usuários
* sincronização de grupos com os existentes no AEM
* Autenticação iniciada pelo Provedor de serviços e Provedor de identidade

Esse manipulador armazena a mensagem de resposta SAML criptografada no nó do usuário ( `usernode/samlResponse`) para facilitar a comunicação com um Provedor de serviços de terceiros.

>[!NOTE]
>
>Consulte [uma demonstração da integração de AEM e SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Para ler um artigo completo da comunidade, clique em: [Integração do SAML com o Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configurar o manipulador de autenticação do SAML 2.0 {#configuring-the-saml-authentication-handler}

O [Web console](/help/sites-deploying/configuring-osgi.md) fornece acesso à configuração do [SAML](http://saml.xml.org/saml-specifications) Manipulador de Autenticação 2.0 chamada **Adobe Granite SAML 2.0 Authentication Handler**. As seguintes propriedades podem ser definidas.

>[!NOTE]
>
>O SAML 2.0 Authentication Handler está desativado por padrão. Você deve definir pelo menos uma das seguintes propriedades para habilitar o manipulador:
>
>* O URL do POST do Provedor de identidade.
>* A ID da Entidade do Provedor de Serviços.

>


>[!NOTE]
>
>As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, você deve fornecer pelo menos o certificado público do Provedor de identidade no TrustStore. Consulte [Adicionar o certificado IdP à seção TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obter mais informações.

**** Caminho PathRepository para o qual esse manipulador de autenticação deve ser usado pelo Sling. Se estiver vazio, o manipulador de autenticação será desativado.

**Valor de Classificação do Serviço** RankingOSGi Framework Service para indicar a ordem na qual chamar este serviço. Esse é um valor inteiro em que valores mais altos designam uma precedência mais alta.

**Certificado IDP** AliasO alias do certificado do IdP no truststore global. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado. Consulte o capítulo &quot;Adicionar o certificado IdP ao AEM TrustStore&quot; abaixo sobre como configurá-lo.

**O** URL do provedor de identidade do IDP para o qual a Solicitação de autenticação SAML deve ser enviada. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado.

>[!CAUTION]
>
>O nome de host do Provedor de identidade deve ser adicionado à configuração OSGi **Apache Sling Referrer Filter**. Consulte a seção [Console da Web](/help/sites-deploying/configuring-osgi.md) para obter mais informações.

**IDID da Entidade do Provedor de Serviços que identifica exclusivamente este provedor de serviços com o** provedor de identidade. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado.

**Padrão** Redirecionar O local padrão para o qual redirecionar após a autenticação bem-sucedida.

>[!NOTE]
>
>Este local só será usado se o cookie `request-path` não estiver definido. Se você solicitar qualquer página abaixo do caminho configurado sem um token de login válido, o caminho solicitado será armazenado em um cookie
>e o navegador será redirecionado para esse local novamente após a autenticação bem-sucedida.

**** Atributo da ID do usuário: o nome do atributo que contém a ID do usuário usada para autenticar e criar o usuário no repositório CRX.

>[!NOTE]
>
>A ID de usuário não será retirada do nó `saml:Subject` da asserção de SAML, mas desse `saml:Attribute`.

**Use** EncryptionSe esse manipulador de autenticação espera ou não asserções de SAML criptografadas.

**Criar** usuários do CRX automaticamentePara criar usuários não existentes automaticamente no repositório após a autenticação bem-sucedida.

>[!CAUTION]
>
>Se a criação automática de usuários do CRX estiver desativada, os usuários precisarão ser criados manualmente.

**Adicionar a** gruposSe um usuário deve ou não ser adicionado automaticamente a grupos CRX após uma autenticação bem-sucedida.

**Associação** de GrupoO nome do saml:Attribute contendo uma lista de grupos CRX ao qual esse usuário deve ser adicionado.

## Adicionar o Certificado IdP ao AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do IdP no repositório. Para fazer isso, você precisa:

1. Vá para *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pressione o link **[!UICONTROL Create TrustStore]**
1. Insira a senha do TrustStore e pressione **[!UICONTROL Save]**.
1. Clique em **[!UICONTROL Gerenciar TrustStore]**.
1. Faça upload do certificado IdP.
1. Anote o certificado Alias. O alias é **[!UICONTROL admin#1436172864930]** no exemplo abaixo.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Adicionar a chave do Provedor de serviços e a cadeia de certificados ao repositório de chaves AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>As etapas abaixo são obrigatórias, caso contrário, a seguinte exceção será lançada: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vá para: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite o usuário `authentication-service`.
1. Crie um KeyStore clicando em **Criar KeyStore** em **Configurações de conta**.

>[!NOTE]
>
>As etapas abaixo são necessárias somente se o manipulador for capaz de assinar ou descriptografar mensagens.

1. Faça upload do arquivo de chave privada clicando em **Selecionar arquivo de chave privada**. A chave precisa estar no formato PKCS#8 com codificação DER.
1. Faça upload do arquivo de certificado clicando em **Selecionar arquivos da cadeia de certificados**.
1. Atribua um Alias, conforme mostrado abaixo:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar um logger para SAML {#configure-a-logger-for-saml}

Você pode configurar um Logger para depurar todos os problemas que possam surgir da configuração incorreta do SAML. Você pode fazer isso ao:

1. Ir para o Console da Web, em *http://localhost:4502/system/console/configMgr*
1. Procure e clique na entrada chamada **Apache Sling Logging Logger Configuration**
1. Crie um logger com a seguinte configuração:

   * **Nível de log:** Depuração
   * **Arquivo de log:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
