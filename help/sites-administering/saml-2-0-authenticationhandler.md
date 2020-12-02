---
title: Manipulador de autenticação SAML 2.0
seo-title: Manipulador de autenticação SAML 2.0
description: Saiba mais sobre o SAML 2.0 Authentication Handler no AEM.
seo-description: Saiba mais sobre o SAML 2.0 Authentication Handler no AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: d559a15e3c1c65c39e38935691835146f54a356e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# Manipulador de autenticação SAML 2.0{#saml-authentication-handler}

AEM é fornecido com um manipulador de autenticação [SAML](http://saml.xml.org/saml-specifications). Este manipulador fornece suporte para o [SAML](http://saml.xml.org/saml-specifications) 2.0 Authentication Request Protocol (perfil Web-SSO) usando o vínculo `HTTP POST`.

Ele suporta:

* assinatura e criptografia de mensagens
* criação automática de usuários
* sincronização de grupos com os existentes no AEM
* Autenticação iniciada pelo provedor de serviço e provedor de identidade

Este manipulador armazena a mensagem de resposta SAML criptografada no nó do usuário ( `usernode/samlResponse`) para facilitar a comunicação com um Provedor de serviço de terceiros.

>[!NOTE]
>
>Consulte [uma demonstração da integração AEM e SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Para ler um artigo da comunidade de fim a fim, clique em: [Integração do SAML com o Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configurando o manipulador de autenticação SAML 2.0 {#configuring-the-saml-authentication-handler}

O [console Web](/help/sites-deploying/configuring-osgi.md) fornece acesso à configuração do [SAML](http://saml.xml.org/saml-specifications) 2.0 Authentication Handler chamada **Adobe Granite SAML 2.0 Authentication Handler**. As seguintes propriedades podem ser definidas.

>[!NOTE]
>
>O SAML 2.0 Authentication Handler está desativado por padrão. É necessário definir pelo menos uma das seguintes propriedades para habilitar o manipulador:
>
>* O URL POST do provedor de identidade.
>* A ID de entidade do Provedor de serviço.

>



>[!NOTE]
>
>As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do Provedor de Identidade no TrustStore. Consulte [Adicionar o certificado IdP à seção TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obter mais informações.

**Caminho** PathRepository para o qual esse manipulador de autenticação deve ser usado pelo Sling. Se estiver vazio, o manipulador de autenticação será desativado.

**Valor de classificação do serviço de** classificação OSGi Framework para indicar a ordem na qual chamar esse serviço. Esse é um valor inteiro em que valores mais altos designam precedência mais alta.

**Certificado IDP** AliasO alias do certificado do IdP no Truststore global. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado. Consulte o capítulo &quot;Adicionar o certificado IdP ao AEM TrustStore&quot; abaixo sobre como configurá-lo.

**URL do provedor de identidade** do IDP para o qual a Solicitação de autenticação SAML deve ser enviada. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

>[!CAUTION]
>
>O nome do host do provedor de identidade deve ser adicionado à configuração **Filtro de Quem indicou Sling do Apache** OSGi. Consulte a seção [Web console](/help/sites-deploying/configuring-osgi.md) para obter mais informações.

**provedor de serviço Entity** IDID que identifica exclusivamente esse provedor de serviço com o provedor de identidade. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

**Redirecionamento padrãoO local padrão para redirecionar após a autenticação bem-sucedida.** 

>[!NOTE]
>
>Este local só é usado se o cookie `request-path` não estiver definido. Se você solicitar qualquer página abaixo do caminho configurado sem um token de login válido, o caminho solicitado será armazenado em um cookie
>e o navegador será redirecionado para esse local novamente após a autenticação bem-sucedida.

**Atributo da ID do usuário** O nome do atributo que contém a ID do usuário usada para autenticar e criar o usuário no repositório CRX.

>[!NOTE]
>
>A ID de usuário não será retirada do nó `saml:Subject` da asserção SAML, mas desse `saml:Attribute`.

**Usar** criptografiaIndependentemente deste manipulador de autenticação esperar ou não asserções SAML criptografadas.

**Criação automática de** usuários CRXede criar ou não automaticamente usuários não existentes no repositório após a autenticação bem-sucedida.

>[!CAUTION]
>
>Se a criação automática de usuários CRX estiver desativada, os usuários terão que ser criados manualmente.

**Adicionar a** gruposSe um usuário deve ser adicionado automaticamente a grupos CRX após uma autenticação bem-sucedida.

**Associação de grupoO nome do mesmo** atributo:que contém uma lista de grupos CRX aos quais este usuário deve ser adicionado.

## Adicione o certificado IdP ao AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do IdP no repositório. Para fazer isso, é necessário:

1. Vá para *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pressione o link **[!UICONTROL Create TrustStore]**
1. Digite a senha do TrustStore e pressione **[!UICONTROL Save]**.
1. Clique em **[!UICONTROL Gerenciar TrustStore]**.
1. Carregue o certificado IdP.
1. Anote o certificado Alias. O alias é **[!UICONTROL admin#1436172864930]** no exemplo abaixo.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Adicione a chave do Provedor de serviço e a cadeia de certificados ao armazenamento de chaves AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>As etapas abaixo são obrigatórias, caso contrário, a seguinte exceção será lançada: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir para: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite o usuário `authentication-service`.
1. Crie um KeyStore clicando em **Create KeyStore** em **Configurações da conta**.

>[!NOTE]
>
>As etapas abaixo são necessárias somente se o manipulador puder assinar ou descriptografar mensagens.

1. Carregue o arquivo de chave privada clicando em **Selecionar arquivo de chave privada**. A chave precisa estar no formato PKCS#8 com codificação DER.
1. Carregue o arquivo de certificado clicando em **Selecionar arquivos da cadeia de certificados**.
1. Atribua um Alias, como mostrado abaixo:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar um Logger para SAML {#configure-a-logger-for-saml}

Você pode configurar um Logger para depurar quaisquer problemas que possam surgir de uma configuração incorreta do SAML. Você pode fazer isso:

1. Ir para o Web Console, em *http://localhost:4502/system/console/configMgr*
1. Procure e clique na entrada **Configuração do Apache Sling Logging Logger**
1. Crie um agente de log com a seguinte configuração:

   * **Nível de log:** Depuração
   * **Arquivo de registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml

