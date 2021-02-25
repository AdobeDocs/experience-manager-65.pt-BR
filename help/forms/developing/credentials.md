---
title: Trabalhar com credenciais
seo-title: Trabalhar com credenciais
description: Importe credenciais para o AEM Forms usando a API do Trust Manager e a API do Java. Além disso, saiba como excluir credenciais usando a API do Gerenciador de confiança e a API do Java.
seo-description: Importe credenciais para o AEM Forms usando a API do Trust Manager e a API do Java. Além disso, saiba como excluir credenciais usando a API do Gerenciador de confiança e a API do Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---


# Trabalhar com credenciais {#working-with-credentials}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

**Sobre o serviço de credenciais**

Uma credencial contém suas informações de chave privada necessárias para assinar ou identificar documentos. Um certificado é uma informação de chave pública configurada para confiança. A AEM Forms usa certificados e credenciais para vários fins:

* As extensões do Acrobat Reader DC usam uma credencial para ativar os direitos de uso do Adobe Reader em documentos PDF. (Consulte [Aplicar direitos de uso a Documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* O serviço de assinatura acessa certificados e credenciais enquanto executa operações como assinar digitalmente documentos PDF. (Consulte [Assinando Documentos PDF digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Você pode interagir programaticamente com o serviço de Credenciais usando a API Java do Trust Manager. É possível executar as seguintes tarefas:

* [Importando credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Excluindo credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Também é possível importar e excluir certificados usando o console de administração. (Consulte [ajuda administrativa.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importando credenciais usando a API do Trust Manager {#importing-credentials-by-using-the-trust-manager-api}

Você pode importar uma credencial para o AEM Forms de forma programática usando a API do Trust Manager. Por exemplo, é possível importar uma credencial usada para assinar um documento PDF. (Consulte [Assinando Documentos PDF digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Ao importar uma credencial, especifique um alias para a credencial. O alias é usado para executar uma operação do Forms que requer uma credencial. Depois de importada, uma credencial pode ser visualizada no console de administração, como mostrado na ilustração a seguir. Observe que o alias da credencial é *Secure*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Não é possível importar uma credencial para o AEM Forms usando serviços da Web.

### Resumo das etapas {#summary-of-steps}

Para importar uma credencial para o AEM Forms, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço de credenciais.
1. Faça referência à credencial.
1. Execute a operação de importação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credenciais**

Antes de poder importar programaticamente uma credencial para o AEM Forms, crie um cliente de serviço de credenciais. Para obter informações, consulte [Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência à credencial**

Faça referência a uma credencial que você deseja importar para o AEM Forms. O start rápido associado a esta seção faz referência a um arquivo P12 localizado no sistema de arquivos.

**Executar a operação de importação**

Depois de referenciar a credencial, importe-a para o AEM Forms. Se a credencial não for importada com êxito, uma exceção será lançada. Ao importar uma credencial, especifique um alias para a credencial.

**Consulte também:**

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de credenciais](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Excluindo credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciais usando a API Java {#import-credentials-using-the-java-api}

Importe uma credencial para o AEM Forms usando a API do Trust Manager (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de credenciais

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `CredentialServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência à credencial

   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local da credencial.
   * Crie um objeto `com.adobe.idp.Document` que armazene a credencial usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém a credencial para o construtor.

1. Executar a operação de importação

   * Crie uma matriz de string que armazena um elemento. Atribua o valor `truststore.usage.type.sign` ao elemento.
   * Chame o método `CredentialServiceClient` do objeto `importCredential` e passe os seguintes valores:

      * Um valor de string que especifica o valor alias da credencial.
      * A instância `com.adobe.idp.Document` que armazena a credencial.
      * Um valor de string que especifica a senha associada à credencial.
      * A matriz de string que contém o valor de uso. Por exemplo, você pode especificar esse valor `truststore.usage.type.sign`. Para importar uma credencial de extensão de Reader, especifique `truststore.usage.type.lcre`.

**Consulte também:**

[Importando credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Start rápido (modo SOAP): Importando credenciais usando a API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Excluindo credenciais usando a API do Gerenciador de Confiança {#deleting-credentials-by-using-the-trust-manager-api}

Você pode excluir uma credencial por programação usando a API do Gerenciador de confiança. Ao excluir uma credencial, especifique um alias que corresponda à credencial. Depois de excluída, uma credencial não pode ser usada para executar uma operação.

>[!NOTE]
>
>Não é possível excluir uma credencial no AEM Forms usando serviços da Web.

### Resumo das etapas {#summary_of_steps-1}

Para excluir uma credencial, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço de credenciais.
1. Execute a operação de exclusão.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credenciais**

Antes de poder excluir uma credencial programaticamente, crie um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Executar a operação de exclusão**

Para excluir uma credencial, especifique o alias que corresponde à credencial. Se você especificar um alias que não existe, uma exceção será lançada.

**Consulte também:**

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

### Excluindo credenciais usando a API Java {#deleting-credentials-using-the-java-api}

Exclua uma credencial da AEM Forms usando a API do Trust Manager (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de credenciais

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `CredentialServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Executar a operação de exclusão

   Chame o método `CredentialServiceClient` do objeto `deleteCredential` e passe um valor de string que especifique o valor alias.

**Consulte também:**

[Excluindo credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Start rápido (modo SOAP): Excluindo credenciais usando a API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
