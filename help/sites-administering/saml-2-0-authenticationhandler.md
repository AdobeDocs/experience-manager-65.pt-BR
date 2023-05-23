---
title: Manipulador de autenticação SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: Saiba mais sobre o Manipulador de autenticação SAML 2.0 no AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6fa3679429527e026313b22d953267503598d1a9
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# Manipulador de autenticação SAML 2.0{#saml-authentication-handler}

O AEM tem uma [SAML](https://saml.xml.org/saml-specifications) manipulador de autenticação. Esse manipulador fornece suporte para o [SAML](https://saml.xml.org/saml-specifications) 2.0 Protocolo de solicitação de autenticação (perfil Web-SSO) usando o `HTTP POST` vinculativo.

Ele oferece suporte a:

* assinatura e criptografia de mensagens
* criação automática de usuários
* sincronização de grupos com grupos existentes no AEM
* O provedor de serviços e o provedor de identidade iniciaram a autenticação

Esse manipulador armazena a mensagem de resposta SAML criptografada no nó do usuário ( `usernode/samlResponse`) para facilitar a comunicação com um provedor de serviços terceirizado.

>[!NOTE]
>
>Consulte [uma demonstração da integração do AEM e SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=pt-BR).

## Configurando o Manipulador de Autenticação SAML 2.0 {#configuring-the-saml-authentication-handler}

A variável [Console da Web](/help/sites-deploying/configuring-osgi.md) fornece acesso à [SAML](https://saml.xml.org/saml-specifications) Configuração do Manipulador de autenticação 2.0 chamada **Manipulador de autenticação Adobe Granite SAML 2.0**. As seguintes propriedades podem ser definidas.

>[!NOTE]
>
>O Manipulador de autenticação SAML 2.0 é desativado por padrão. Você deve definir pelo menos uma das seguintes propriedades para habilitar o manipulador:
>
>* O URL POST do provedor de identidade ou URL do IDP.
>* A ID da entidade do provedor de serviços.
>


>[!NOTE]
>
>As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do Provedor de Identidade no TrustStore. Consulte [Adicionar o certificado IdP ao TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obter mais informações.

**Caminho** Caminho do repositório para o qual esse manipulador de autenticação deve ser usado pelo Sling. Se estiver vazio, o manipulador de autenticação será desativado.

**Classificação do serviço** Valor de Classificação do OSGi Framework Service para indicar a ordem na qual chamar esse serviço. É um valor inteiro em que valores mais altos designam maior precedência.

**Alias do certificado IDP** O alias do certificado do IdP na truststore global. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado. Consulte o capítulo &quot;Adicionar o certificado IdP ao AEM TrustStore&quot; abaixo sobre como configurá-lo.

**URL DO IDP** URL do IDP para o qual a Solicitação de Autenticação SAML deve ser enviada. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

>[!CAUTION]
>
>O nome de host do Provedor de Identidade deve ser adicionado ao **Filtro referenciador do Apache Sling** Configuração do OSGi. Consulte a [Console da Web](/help/sites-deploying/configuring-osgi.md) para obter mais informações.

**ID da entidade do provedor de serviços** ID que identifica exclusivamente este provedor de serviços com o provedor de identidade. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

**Redirecionamento padrão** O local padrão para redirecionar após a autenticação bem-sucedida.

>[!NOTE]
>
>Esse local só será usado se a variável `request-path` cookie não está definido. Se você solicitar qualquer página abaixo do caminho configurado sem um token de logon válido, o caminho solicitado será armazenado em um cookie
>e o navegador será redirecionado para este local novamente após a autenticação bem-sucedida.

**Atributo de ID de usuário** O nome do atributo que contém a ID de usuário usada para autenticar e criar o usuário no repositório CRX.

>[!NOTE]
>
>A ID de usuário não será retirada do `saml:Subject` nó da asserção SAML, mas a partir deste `saml:Attribute`.

**Usar criptografia** Se este manipulador de autenticação espera ou não afirmações SAML criptografadas.

**Criar automaticamente usuários do CRX** Determina se os usuários não existentes no repositório devem ou não ser criados automaticamente após a autenticação bem-sucedida.

>[!CAUTION]
>
>Se a criação automática de usuários do CRX estiver desativada, os usuários terão que ser criados manualmente.

**Adicionar a grupos** Se um usuário deve ou não ser adicionado automaticamente a grupos CRX após a autenticação bem-sucedida.

**Associação de grupo** O nome do saml:Attribute contendo uma lista de grupos CRX aos quais esse usuário deve ser adicionado.

## Adicionar o certificado IdP ao AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do IdP no repositório. Para fazer isso, é necessário:

1. Ir para *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pressione a **[!UICONTROL Criar link TrustStore]**
1. Insira a senha para o TrustStore e pressione **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL Gerenciar TrustStore]**.
1. Carregue o certificado IdP.
1. Anote o alias do certificado. O alias é **[!UICONTROL admin#1436172864930]** no exemplo abaixo.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Adicione a chave do Provedor de serviços e a cadeia de certificados ao keystore do AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>As etapas abaixo são obrigatórias, caso contrário, a seguinte exceção será lançada: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir para: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite o `authentication-service` usuário.
1. Crie um KeyStore clicando em **Criar KeyStore** em **Configurações da conta**.

>[!NOTE]
>
>As etapas abaixo são necessárias somente se o manipulador puder assinar ou descriptografar mensagens.

1. Crie o certificado/par de chaves para AEM. O comando para gerá-lo via openssl deve se parecer com o exemplo abaixo:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Converta a chave para o formato PKCS#8 com codificação DER. Esse é o formato exigido pelo armazenamento de chaves do AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Faça upload do arquivo de chave de privacidade clicando em **Selecione o arquivo da chave de privacidade**.
1. Faça upload do arquivo de certificado clicando em **Selecionar arquivos da cadeia de certificados**.
1. Atribua um Alias, conforme mostrado abaixo:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar um agente de log para SAML {#configure-a-logger-for-saml}

Você pode configurar um Logger para depurar quaisquer problemas que possam surgir da configuração incorreta do SAML. Você pode fazer isso ao:

1. Acessando o console da Web, em *http://localhost:4502/system/console/configMgr*
1. Procure e clique na entrada chamada **Configuração do logger de log do Apache Sling**
1. Crie um agente de log com a seguinte configuração:

   * **Nível de log:** Depurar
   * **Arquivo de log:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
