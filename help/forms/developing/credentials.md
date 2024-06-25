---
title: Trabalhar com credenciais
description: Importe credenciais para o AEM Forms usando a API do Gerenciador de Confiança e a API Java. Além disso, saiba como excluir credenciais usando a API do Gerenciador de confiança e a API Java.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---

# Trabalhar com credenciais {#working-with-credentials}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Credenciais**

Uma credencial contém suas informações de chave privada necessárias para assinar ou identificar documentos. Um certificado é uma informação de chave pública que você configura para confiança. O AEM Forms usa certificados e credenciais para várias finalidades:

* As extensões do Acrobat Reader DC usam uma credencial para ativar os direitos de uso do Adobe Reader em documentos do PDF. (Consulte [Aplicação de direitos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* O serviço de assinatura acessa certificados e credenciais ao executar operações, como assinar digitalmente documentos de PDF. (Consulte [Assinatura digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Você pode interagir programaticamente com o serviço de credenciais usando a API Java do Gerenciador de Confiança. Você pode executar as seguintes tarefas:

* [Importando Credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>Também é possível importar e excluir certificados usando o console de administração. (Consulte [ajuda administrativa.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Importando Credenciais usando a API do Gerenciador de Confiança {#importing-credentials-by-using-the-trust-manager-api}

Você pode importar programaticamente uma credencial para o AEM Forms usando a API do Gerenciador de Confiança. Por exemplo, você pode importar uma credencial usada para assinar um documento PDF. (Consulte [Assinatura digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

Ao importar uma credencial, especifique um alias para a credencial. O alias é usado para executar uma operação do Forms que requer uma credencial. Depois de importada, uma credencial pode ser exibida no console de administração, conforme mostrado na ilustração a seguir. Observe que o alias da credencial é *Seguro*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Não é possível importar uma credencial para o AEM Forms usando serviços da Web.

### Resumo das etapas {#summary-of-steps}

Para importar uma credencial para o AEM Forms, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de credencial.
1. Referencie a credencial.
1. Execute a operação de importação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credencial**

Antes de importar programaticamente uma credencial para o AEM Forms, crie um cliente de serviço de credencial. Para obter informações, consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referenciar a credencial**

Referencie uma credencial que você deseja importar para o AEM Forms. O início rápido associado a esta seção faz referência a um arquivo P12 no sistema de arquivos.

**Executar a operação de importação**

Depois de referenciar a credencial, importe-a para o AEM Forms. Se a credencial não for importada com êxito, uma exceção será lançada. Ao importar uma credencial, especifique um alias para a credencial.

**Consulte também**

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Credencial](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Importar credenciais usando a API Java {#import-credentials-using-the-java-api}

Importe uma credencial para o AEM Forms usando a API do Gerenciador de Confiança (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço de credencial

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `CredentialServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referenciar a credencial

   * Criar um `java.io.FileInputStream` usando seu construtor. Transmita um valor de cadeia de caracteres que especifique o local da credencial.
   * Criar um `com.adobe.idp.Document` objeto que armazena a credencial usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém a credencial para o construtor.

1. Executar a operação de importação

   * Crie uma matriz de cadeia de caracteres que contenha um elemento. Atribuir o valor `truststore.usage.type.sign` ao elemento.
   * Chame o `CredentialServiceClient` do objeto `importCredential` e passe os seguintes valores:

      * Um valor de cadeia de caracteres que especifica o valor de alias da credencial.
      * A variável `com.adobe.idp.Document` instância que armazena a credencial.
      * Um valor de cadeia de caracteres que especifica a senha associada à credencial.
      * A matriz de cadeia de caracteres que contém o valor de uso. Por exemplo, você pode especificar esse valor `truststore.usage.type.sign`. Para importar uma credencial de extensão de Reader, especifique `truststore.usage.type.lcre`.

**Consulte também**

[Importando Credenciais usando a API do Gerenciador de Confiança](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[Início rápido (modo SOAP): importação de credenciais usando a API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Excluindo Credenciais usando a API do Gerenciador de Confiança {#deleting-credentials-by-using-the-trust-manager-api}

Você pode excluir programaticamente uma credencial usando a API do Gerenciador de Confiança. Ao excluir uma credencial, especifique um alias que corresponda à credencial. Depois de excluída, uma credencial não pode ser usada para executar uma operação.

>[!NOTE]
>
>Não é possível excluir uma credencial no AEM Forms usando serviços da Web.

### Resumo das etapas {#summary_of_steps-1}

Para excluir uma credencial, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de credencial.
1. Execute a operação de exclusão.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de credencial**

Antes de excluir programaticamente uma credencial, crie um cliente de serviço de Integração de Dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Executar a operação de exclusão**

Para excluir uma credencial, especifique o alias que corresponde à credencial. Se você especificar um alias que não existe, uma exceção será lançada.

**Consulte também**

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Importar credenciais usando a API Java](credentials.md#import-credentials-using-the-java-api)

### Exclusão de credenciais usando a API Java {#deleting-credentials-using-the-java-api}

Exclua uma credencial do AEM Forms usando a API do Gerenciador de Confiança (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-truststore-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço de credencial

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `CredentialServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Executar a operação de exclusão

   Chame o `CredentialServiceClient` do objeto `deleteCredential` e transmitem um valor de string que especifica o valor do alias.

**Consulte também**

[Excluindo Credenciais usando a API do Gerenciador de Confiança](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[Início rápido (modo SOAP): exclusão de credenciais usando a API Java](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
