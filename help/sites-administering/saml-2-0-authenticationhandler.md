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
source-git-commit: ffabf5a9e3b08f60394cecfe540692b161437362
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# Manipulador de autenticação SAML 2.0{#saml-authentication-handler}

AEM navios com uma [SAML](https://saml.xml.org/saml-specifications) manipulador de autenticação. Esse manipulador fornece suporte para o [SAML](https://saml.xml.org/saml-specifications) Protocolo de solicitação de autenticação 2.0 (perfil Web-SSO) usando o `HTTP POST` vinculação.

Ele suporta:

* assinatura e criptografia de mensagens
* criação automática de usuários
* sincronização de grupos com os existentes no AEM
* Autenticação iniciada pelo Provedor de serviços e Provedor de identidade

Esse manipulador armazena a mensagem de resposta SAML criptografada no nó do usuário ( `usernode/samlResponse`) para facilitar a comunicação com um provedor de serviços terceirizado.

>[!NOTE]
>
>Para ler um artigo completo da comunidade, clique em: [Integração do SAML com o Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configurar o manipulador de autenticação do SAML 2.0 {#configuring-the-saml-authentication-handler}

O [Console da Web](/help/sites-deploying/configuring-osgi.md) fornece acesso ao [SAML](https://saml.xml.org/saml-specifications) Configuração do Manipulador de Autenticação 2.0 chamada **Manipulador de autenticação do Adobe Granite SAML 2.0**. As seguintes propriedades podem ser definidas.

>[!NOTE]
>
>O SAML 2.0 Authentication Handler está desativado por padrão. Você deve definir pelo menos uma das seguintes propriedades para habilitar o manipulador:
>
>* O URL do POST do Provedor de identidade.
>* A ID da Entidade do Provedor de Serviços.
>


>[!NOTE]
>
>As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, você deve fornecer pelo menos o certificado público do Provedor de identidade no TrustStore. Consulte [Adicionar o certificado IdP ao TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obter mais informações.

**Caminho** Caminho do repositório para o qual esse manipulador de autenticação deve ser usado pelo Sling. Se estiver vazio, o manipulador de autenticação será desativado.

**Classificação do serviço** Valor de Classificação do Serviço de Estrutura OSGi para indicar a ordem na qual chamar esse serviço. Esse é um valor inteiro em que valores mais altos designam precedência mais alta.

**Alias de certificado IDP** O alias do certificado do IdP no truststore global. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado. Consulte o capítulo &quot;Adicionar o certificado IdP ao AEM TrustStore&quot; abaixo sobre como configurá-lo.

**URL do provedor de identidade** URL do IDP para o qual a Solicitação de autenticação SAML deve ser enviada. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado.

>[!CAUTION]
>
>O nome de host do Provedor de identidade deve ser adicionado ao **Filtro de referenciador do Apache Sling** Configuração do OSGi. Consulte a [Console da Web](/help/sites-deploying/configuring-osgi.md) para obter mais informações.

**ID da Entidade do Provedor de Serviços** ID que identifica exclusivamente este provedor de serviços com o provedor de identidade. Se esta propriedade estiver vazia, o manipulador de autenticação será desativado.

**Redirecionamento padrão** O local padrão para o qual redirecionar após a autenticação bem-sucedida.

>[!NOTE]
>
>Esse local só será usado se a variável `request-path` cookie não está definido. Se você solicitar qualquer página abaixo do caminho configurado sem um token de login válido, o caminho solicitado será armazenado em um cookie
>e o navegador será redirecionado para esse local novamente após a autenticação bem-sucedida.

**Atributo de ID de usuário** O nome do atributo que contém a ID de usuário usada para autenticar e criar o usuário no repositório CRX.

>[!NOTE]
>
>A ID de usuário não será retirada do `saml:Subject` nó da asserção SAML, mas desta `saml:Attribute`.

**Usar criptografia** Se esse manipulador de autenticação espera ou não asserções de SAML criptografadas.

**Criar automaticamente usuários do CRX** Criar ou não automaticamente usuários não existentes no repositório após a autenticação bem-sucedida.

>[!CAUTION]
>
>Se a criação automática de usuários do CRX estiver desativada, os usuários precisarão ser criados manualmente.

**Adicionar a grupos** Se um usuário deve ou não ser adicionado automaticamente a grupos CRX após uma autenticação bem-sucedida.

**Associação de Grupo** O nome do saml:Attribute contendo uma lista de grupos CRX ao qual esse usuário deve ser adicionado.

## Adicionar o Certificado IdP ao AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

As asserções SAML são assinadas e podem, opcionalmente, ser criptografadas. Para que isso funcione, é necessário fornecer pelo menos o certificado público do IdP no repositório. Para fazer isso, você precisa:

1. Ir para *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pressione a tecla **[!UICONTROL Criar link TrustStore]**
1. Digite a senha do TrustStore e pressione **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL Gerenciar TrustStore]**.
1. Faça upload do certificado IdP.
1. Anote o certificado Alias. O alias é **[!UICONTROL admin#1436172864930]** no exemplo abaixo.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Adicionar a chave do Provedor de serviços e a cadeia de certificados ao repositório de chaves AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>As etapas abaixo são obrigatórias, caso contrário, a seguinte exceção será lançada: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vá para: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite o `authentication-service` usuário.
1. Criar um KeyStore clicando em **Criar KeyStore** under **Configurações da conta**.

>[!NOTE]
>
>As etapas abaixo são necessárias somente se o manipulador for capaz de assinar ou descriptografar mensagens.

1. Carregue o arquivo de chave privada clicando em **Selecionar arquivo de chave privada**. A chave precisa estar no formato PKCS#8 com codificação DER.
1. Faça upload do arquivo de certificado clicando em **Selecionar arquivos da cadeia de certificados**.
1. Atribua um Alias, conforme mostrado abaixo:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar um logger para SAML {#configure-a-logger-for-saml}

Você pode configurar um Logger para depurar todos os problemas que possam surgir da configuração incorreta do SAML. Você pode fazer isso ao:

1. Ir para o Console da Web, em *http://localhost:4502/system/console/configMgr*
1. Procure e clique na entrada chamada **Configuração do Apache Sling Logging Logger**
1. Crie um logger com a seguinte configuração:

   * **Nível de registro:** Depurar
   * **Arquivo de log:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml
