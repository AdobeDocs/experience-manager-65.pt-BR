---
title: Trabalhando com credenciais
seo-title: Trabalhando com credenciais
description: Importe credenciais no AEM Forms usando a API do Gerenciador de Confiança e a API do Java. Além disso, saiba como excluir credenciais usando a API do Trust Manager e a API do Java.
seo-description: Importe credenciais no AEM Forms usando a API do Gerenciador de Confiança e a API do Java. Além disso, saiba como excluir credenciais usando a API do Trust Manager e a API do Java.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# Trabalhando com credenciais {#working-with-credentials}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o Serviço de Credenciais**

Uma credencial contém suas informações de chave privada necessárias para assinar ou identificar documentos. Um certificado são informações de chave pública configuradas para confiança. A AEM Forms usa certificados e credenciais para várias finalidades:

* O Acrobat Reader DC Extensions usa uma credencial para habilitar os direitos de uso do Adobe Reader em documentos PDF. (Consulte [Aplicar direitos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* O serviço de assinatura acessa certificados e credenciais ao executar operações como assinar digitalmente documentos PDF. (Consulte [Assinando documentos PDF digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Você pode interagir programaticamente com o serviço de Credencial usando a API Java do Gerenciador de Confiança. Você pode executar as seguintes tarefas:

* [Importando credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Também é possível importar e excluir certificados usando o console de administração. (Consulte [ajuda de administração.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importando credenciais usando a API do Gerenciador de Confiança {#importing-credentials-by-using-the-trust-manager-api}

Você pode importar uma credencial para o AEM Forms por programação usando a API do Gerenciador de Confiança. Por exemplo, você pode importar uma credencial usada para assinar um documento PDF. (Consulte [Assinando documentos PDF digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Ao importar uma credencial, especifique um alias para a credencial. O alias é usado para executar uma operação do Forms que requer uma credencial. Depois de importada, uma credencial pode ser visualizada no console de administração, conforme mostrado na ilustração a seguir. Observe que o alias da credencial é *Seguro*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Não é possível importar uma credencial para o AEM Forms usando os serviços da Web.

### Resumo das etapas {#summary-of-steps}

Para importar uma credencial para o AEM Forms, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente do serviço de credenciais.
1. Referencie a credencial.
1. Execute a operação de importação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credencial**

Antes de poder importar uma credencial programaticamente para o AEM Forms, crie um cliente de serviço de credenciais. Para obter informações, consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência da credencial**

Faça referência a uma credencial que você deseja importar para o AEM Forms. O início rápido associado a esta seção faz referência a um arquivo P12 localizado no sistema de arquivos.

**Executar a operação de importação**

Depois de fazer referência à credencial, importe a credencial para o AEM Forms. Se a credencial não for importada com êxito, uma exceção será lançada. Ao importar uma credencial, especifique um alias para a credencial.

**Consulte também:**

[Importar credenciais usando a API do Java](credentials.md#import-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Credenciais](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciais usando a API do Java {#import-credentials-using-the-java-api}

Importe uma credencial para o AEM Forms usando a API do Gerenciador de Confiança (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente de serviço de credencial

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `CredentialServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência da credencial

   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local da credencial.
   * Crie um objeto `com.adobe.idp.Document` que armazene a credencial usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém a credencial para o construtor.

1. Executar a operação de importação

   * Crie uma matriz de sequência de caracteres que contenha um elemento. Atribua o valor `truststore.usage.type.sign` ao elemento.
   * Chame o método `CredentialServiceClient` do objeto `importCredential` e passe os seguintes valores:

      * Um valor de string que especifica o valor do alias para a credencial.
      * A instância `com.adobe.idp.Document` que armazena a credencial.
      * Um valor da string que especifica a senha associada à credencial.
      * A matriz da string que contém o valor de uso. Por exemplo, você pode especificar esse valor `truststore.usage.type.sign`. Para importar uma credencial de Extensão do Reader, especifique `truststore.usage.type.lcre`.

**Consulte também:**

[Importando credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Início rápido (modo SOAP): Como importar credenciais usando a API do Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Excluindo Credenciais usando a API do Gerenciador de Confiança {#deleting-credentials-by-using-the-trust-manager-api}

Você pode excluir uma credencial por programação usando a API do Gerenciador de Confiança. Ao excluir uma credencial, especifique um alias que corresponda à credencial. Depois de excluída, uma credencial não pode ser usada para executar uma operação.

>[!NOTE]
>
>Não é possível excluir uma credencial no AEM Forms usando serviços da Web.

### Resumo das etapas {#summary_of_steps-1}

Para excluir uma credencial, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente do serviço de credenciais.
1. Execute a operação de exclusão.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credencial**

Antes de excluir uma credencial por programação, crie um cliente do serviço de Integração de dados . Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Executar a operação de exclusão**

Para excluir uma credencial, especifique o alias que corresponde à credencial. Se você especificar um alias que não existe, uma exceção é lançada.

**Consulte também:**

[Importar credenciais usando a API do Java](credentials.md#import-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciais usando a API do Java](credentials.md#import-credentials-using-the-java-api)

### Excluindo credenciais usando a API do Java {#deleting-credentials-using-the-java-api}

Exclua uma credencial do AEM Forms usando a API do Gerenciador de confiança (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente de serviço de credencial

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `CredentialServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Executar a operação de exclusão

   Chame o método `CredentialServiceClient` do objeto e transmita um valor de string que especifica o valor do alias.`deleteCredential`

**Consulte também:**

[Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Início rápido (modo SOAP): Exclusão de credenciais usando a API do Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
