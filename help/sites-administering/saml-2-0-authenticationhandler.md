---
title: Manipulador de autenticação SAML 2.0
description: Saiba mais sobre o Manipulador de autenticação SAML 2.0 no AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Manipulador de autenticação SAML 2.0{#saml-authentication-handler}

O AEM vem com um manipulador de autenticação [SAML](https://saml.xml.org/saml-specifications). Este manipulador dá suporte ao Protocolo de Solicitação de Autenticação [SAML](https://saml.xml.org/saml-specifications) 2.0 (perfil Web-SSO) usando a associação `HTTP POST`.

Ele oferece suporte a:

* assinatura e criptografia de mensagens
* criação automática de usuários
* sincronização de grupos com grupos existentes no AEM
* O provedor de serviços e o provedor de identidade iniciaram a autenticação

Este manipulador armazena a mensagem de resposta SAML criptografada no nó do usuário ( `usernode/samlResponse`) para facilitar a comunicação com um Provedor de Serviços de terceiros.

>[!NOTE]
>
>Consulte [uma demonstração de integração de AEM e SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=pt-BR).

## Configurando o Manipulador de Autenticação SAML 2.0 {#configuring-the-saml-authentication-handler}

O [console da Web](/help/sites-deploying/configuring-osgi.md) fornece acesso à configuração do Manipulador de Autenticação [SAML](https://saml.xml.org/saml-specifications) 2.0 chamada **Manipulador de Autenticação SAML 2.0 do Adobe Granite**. As seguintes propriedades podem ser definidas.

>[!NOTE]
>
>O Manipulador de autenticação SAML 2.0 é desativado por padrão. Defina pelo menos uma das seguintes propriedades para ativar o manipulador:
>
>* O URL POST do provedor de identidade ou URL do IDP.
>* A ID da entidade do provedor de serviços.
>

>[!NOTE]
>
>As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do Provedor de Identidade no TrustStore. Consulte [Adicionando o certificado IdP à seção TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obter mais informações.

**Caminho** Caminho do repositório para o qual este manipulador de autenticação deve ser usado pelo Sling. Se estiver vazio, o manipulador de autenticação será desativado.

**Classificação do Serviço** Valor de Classificação do Serviço OSGi Framework para indicar a ordem na qual chamar este serviço. É um valor inteiro em que valores mais altos designam maior precedência.

**Alias do Certificado IDP** O alias do certificado IdP no truststore global. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado. Consulte o capítulo &quot;Adicionar o certificado IdP ao AEM TrustStore&quot; abaixo sobre como configurá-lo.

**URL do IDP** URL do IDP para o qual a Solicitação de Autenticação SAML deve ser enviada. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

>[!CAUTION]
>
>O nome de host do Provedor de Identidade deve ser adicionado à configuração OSGi **Filtro do Referenciador Apache Sling**. Consulte a seção [Console da Web](/help/sites-deploying/configuring-osgi.md) para obter mais informações.

**ID da Entidade do Provedor de Serviços** que identifica exclusivamente este provedor de serviços com o provedor de identidade. Se essa propriedade estiver vazia, o manipulador de autenticação será desativado.

**Redirecionamento padrão** O local padrão para o qual redirecionar após a autenticação bem-sucedida.

>[!NOTE]
>
>Este local só será usado se o cookie `request-path` não estiver definido. Se você solicitar qualquer página abaixo do caminho configurado sem um token de logon válido, o caminho solicitado será armazenado em um cookie
>e o navegador será redirecionado para este local novamente após a autenticação bem-sucedida.

**Atributo de ID de usuário** O nome do atributo que contém a ID de usuário usada para autenticar e criar o usuário no repositório do CRX.

>[!NOTE]
>
>A ID de usuário não será retirada do nó `saml:Subject` da asserção SAML, mas desse `saml:Attribute`.

**Usar Criptografia** Se este manipulador de autenticação espera ou não declarações SAML criptografadas.

**Criar Usuários do CRX Automaticamente** Determina se os usuários não existentes no repositório devem ou não ser criados automaticamente após a autenticação bem-sucedida.

>[!CAUTION]
>
>Se a criação automática de usuários do CRX estiver desativada, os usuários terão que ser criados manualmente.

**Adicionar aos grupos** Se um usuário deve ou não ser adicionado automaticamente aos grupos do CRX após a autenticação bem-sucedida.

**Associação de Grupo** O nome do saml:Attribute contendo uma lista de grupos CRX aos quais esse usuário deve ser adicionado.

## Adicionar o certificado IdP ao AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do IdP no repositório. Para fazer isso, é necessário:

1. Ir para *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pressione o **[!UICONTROL link Criar TrustStore]**
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
1. Editar o usuário `authentication-service`.
1. Crie um KeyStore clicando em **Criar KeyStore** em **Configurações de Conta**.

>[!NOTE]
>
>As etapas abaixo são necessárias somente se o manipulador puder assinar ou descriptografar mensagens.

1. Crie o certificado/par de chaves para AEM. O comando para gerá-lo via openssl deve se parecer com o exemplo abaixo:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Converta a chave para o formato PKCS#8 com codificação DER. Esse é o formato exigido pelo armazenamento de chaves do AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Carregue o arquivo de chave privada clicando em **Selecionar arquivo de chave privada**.
1. Carregue o arquivo de certificado clicando em **Selecionar Arquivos da Cadeia de Certificados**.
1. Atribua um Alias, conforme mostrado abaixo:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar um agente de log para SAML {#configure-a-logger-for-saml}

Você pode configurar um Logger para depurar quaisquer problemas que possam surgir ao configurar incorretamente o SAML. Você pode fazer isso ao:

1. Acessando o Console da Web, em *http://localhost:4502/system/console/configMgr*
1. Procure e clique na entrada denominada **Configuração do logger de log do Apache Sling**
1. Crie um agente de log com a seguinte configuração:

   * **Nível de Log:** Depuração
   * **Arquivo de Log:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
