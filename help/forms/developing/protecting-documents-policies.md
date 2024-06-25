---
title: Protegendo documentos com políticas
description: Use o serviço de Segurança de documentos para aplicar dinamicamente configurações de confidencialidade a documentos do Adobe PDF e manter o controle sobre os documentos. O serviço de Segurança de documentos também permite que os usuários mantenham controle sobre como os recipients usam o documento PDF protegido por política.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '15394'
ht-degree: 0%

---

# Protegendo documentos com políticas {#protecting-documents-with-policies}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o serviço de segurança de documentos**

O serviço de Segurança de documentos permite que os usuários apliquem configurações de confidencialidade de maneira dinâmica a documentos do Adobe PDF e mantenham o controle sobre os documentos, independentemente da abrangência da sua distribuição.

O serviço de Segurança de documentos impede que as informações se espalhem além do alcance do usuário, permitindo que os usuários mantenham o controle sobre como os recipients usam o documento PDF protegido por política. Um usuário pode especificar quem pode abrir um documento, limitar como usá-lo e monitorar o documento após sua distribuição. Um usuário também pode controlar dinamicamente o acesso a um documento protegido por política e até mesmo revogar dinamicamente o acesso ao documento.

O serviço de Segurança de documentos também protege outros tipos de arquivos, como arquivos do Microsoft Word (arquivos DOC). Você pode usar a API do cliente de segurança de documentos para trabalhar com esses tipos de arquivos. As seguintes versões são compatíveis:

* Arquivos do Microsoft Office 2003 (DOC, XLS, PPT)
* Arquivos do Microsoft Office 2007 (arquivos DOCX, XLSX, PPTX)
* Arquivos PTC Pro/E

Para maior clareza, as duas seções a seguir discutem como trabalhar com documentos do Word:

* [Aplicando Políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Removendo Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

É possível realizar essas tarefas usando o serviço Segurança de documentos:

* Criar políticas. Para obter informações, consulte [Criação de políticas](protecting-documents-policies.md#creating-policies).
* Modificar políticas. Para obter informações, consulte [Modificação de Políticas](protecting-documents-policies.md#modifying-policies).
* Excluir políticas. Para obter informações, consulte [Exclusão de Políticas](protecting-documents-policies.md#deleting-policies).
* Aplique políticas a documentos do PDF. Para obter informações, consulte [Aplicação de políticas a documentos do PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Remova as políticas dos documentos do PDF. Para obter informações, consulte [Remoção de políticas de documentos do PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documentos protegidos por política do Inspect. Para obter informações, consulte [Inspeção de Documentos PDF Protegidos por Política](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revogar o acesso a documentos do PDF. Para obter informações, consulte [Revogação do acesso a documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Restaure o acesso aos documentos revogados. Para obter informações, consulte [Restauração do Acesso a Documentos Revogados](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Criar marcas d&#39;água. Para obter informações, consulte [Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks).
* Pesquisar eventos. Para obter informações, consulte [Pesquisando Eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criação de políticas {#creating-policies}

Você pode criar políticas programaticamente usando a API Java de segurança de documentos ou a API de serviço da Web. A *política* O é uma coleção de informações que inclui configurações de segurança de documentos, usuários autorizados e direitos de uso. Você pode criar e salvar qualquer número de políticas, usando configurações de segurança apropriadas para diferentes situações e usuários.

As políticas permitem executar estas tarefas:

* Especifique os indivíduos que podem abrir o documento. Os destinatários podem pertencer à sua organização ou ser externos a ela.
* Especifique como os destinatários podem usar o documento. Você pode restringir o acesso a diferentes recursos do Acrobat e do Adobe Reader. Esses recursos incluem a capacidade de imprimir e copiar texto, adicionar assinaturas e adicionar comentários a um documento.
* Altere as configurações de acesso e segurança a qualquer momento, mesmo depois de distribuir o documento protegido por política.
* Monitore o uso do documento depois de distribuí-lo. Você pode ver como o documento está sendo usado e quem está usando-o. Por exemplo, você pode descobrir quando alguém abriu o documento.

### Criação de uma política usando serviços da Web {#creating-a-policy-using-web-services}

Ao criar uma política usando a API do serviço Web, faça referência a um arquivo XML de linguagem PDRL (Portable Document Rights Language) existente que descreva a política. As permissões de política e o principal são definidos no documento PDRL. O documento XML a seguir é um exemplo de um documento PDRL.

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar uma política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Defina os atributos da política.
1. Criar uma entrada de política.
1. Registre a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se o AEM Forms for implantado no JBoss)
* jaxb-api.jar (se o AEM Forms for implantado no JBoss)
* jaxb-impl.jar (se o AEM Forms for implantado no JBoss)
* jaxb-libs.jar (se o AEM Forms for implantado no JBoss)
* jaxb-xjc.jar (se o AEM Forms for implantado no JBoss)
* relaxngDatatype.jar (se o AEM Forms for implantado no JBoss)
* xsdlib.jar (se o AEM Forms for implantado no JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (use um arquivo JAR diferente se o AEM Forms não for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação do serviço de Segurança de documentos, crie um objeto de cliente desse serviço.

**Definir os atributos da política**

Para criar uma política, defina atributos de política. Um atributo obrigatório é o nome da política. Os nomes das políticas devem ser exclusivos para cada conjunto de políticas. Um conjunto de políticas é simplesmente uma coleção de políticas. Pode haver duas políticas com o mesmo nome se elas pertencerem a conjuntos de políticas separados. Entretanto, duas políticas em um único conjunto de políticas não podem ter o mesmo nome de política.

Outro atributo útil a ser definido é o período de validade. Um período de validade é o período durante o qual um documento protegido por política está acessível aos recipients autorizados. Se você não definir esse atributo, a política será sempre válida.

Um período de validade pode ser definido como uma destas opções:

* Um número definido de dias em que o documento estará acessível a partir do momento em que for publicado
* Uma data final após a qual o documento não estará acessível
* Um intervalo de datas específico para o qual o documento está acessível
* Sempre válido

Você pode especificar apenas uma data de início, o que resulta na validade da política após a data de início. Se você especificar apenas uma data final, a política será válida até a data final. No entanto, uma exceção será lançada se uma data de início e uma data de término não estiverem definidas.

Ao definir atributos que pertencem a uma política, você também pode definir configurações de criptografia. Essas configurações de criptografia são aplicadas quando a política é aplicada a um documento. Você pode especificar os seguintes valores de criptografia:

* **AES256**: representa o algoritmo de criptografia AES com uma chave de 256 bits.
* **AES128**: representa o algoritmo de criptografia AES com uma chave de 128 bits.
* **Sem criptografia:** Representa nenhuma criptografia.

Ao especificar a variável `NoEncryption` , não será possível definir a `PlaintextMetadata` opção para `false`. Se você tentar fazer isso, uma exceção será lançada.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte `Policy` descrição da interface no [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Criar uma entrada de política**

Uma entrada de política anexa principais, que são grupos e usuários, e permissões a uma política. Uma política deve ter pelo menos uma entrada de política. Suponha, por exemplo, que você execute estas tarefas:

* Crie e registre uma entrada de política que permita a um grupo exibir apenas um documento enquanto estiver online e proíba os recipients de copiá-lo.
* Anexe a entrada de política à política.
* Proteger um documento com a política usando o Acrobat.

Essas ações fazem com que os recipients possam exibir somente o documento online e não possam copiá-lo. O documento permanece seguro até que a segurança seja removida dele.

**Registrar a política**

Uma nova política deve ser registrada antes de ser usada. Depois de registrar uma política, você pode usá-la para proteger documentos.

### Criar uma política usando a API Java {#create-a-policy-using-the-java-api}

Crie uma política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina os atributos da política.

   * Criar um `Policy` ao invocar o `InfomodelObjectFactory` estática do objeto `createPolicy` método. Este método retorna um valor de `Policy` objeto.
   * Defina o atributo de nome da política chamando o `Policy` do objeto `setName` e transmitindo um valor de string que especifica o nome da política.
   * Defina a descrição da política chamando o `Policy` do objeto `setDescription` e transmitindo um valor de string que especifica a descrição da política.
   * Especifique o conjunto de políticas ao qual a nova política pertence, chamando o `Policy` do objeto `setPolicySetName` e transmitindo um valor de string que especifica o nome do conjunto de políticas. (Você pode especificar `null` para esse valor de parâmetro que resulta na adição da política ao *Minhas Políticas* definição de políticas.)
   * Crie o período de validade da política chamando o `InfomodelObjectFactory` estática do objeto `createValidityPeriod` método. Este método retorna um valor de `ValidityPeriod` objeto.
   * Defina o número de dias durante os quais um documento protegido por política estará acessível chamando o `ValidityPeriod` do objeto `setRelativeExpirationDays` e transmitindo um valor inteiro que especifica o número de dias.
   * Defina o período de validade da política invocando o `Policy` do objeto `setValidityPeriod` e transmitindo o `ValidityPeriod` objeto.

1. Criar uma entrada de política.

   * Criar uma entrada de política chamando o `InfomodelObjectFactory` estática do objeto `createPolicyEntry` método. Este método retorna um valor de `PolicyEntry` objeto.
   * Especifique as permissões da política invocando o `InfomodelObjectFactory` estática do objeto `createPermission` método. Transmita um membro de dados estático que pertença a `Permission` que representa a permissão. Este método retorna um valor de `Permission` objeto. Por exemplo, para adicionar a permissão que permite aos usuários copiar dados de um documento PDF protegido por política, passe `Permission.COPY`. (Repita essa etapa para cada permissão a ser adicionada).
   * Adicione a permissão à entrada de política chamando o `PolicyEntry` do objeto `addPermission` e transmitindo o `Permission` objeto. (Repita essa etapa para cada `Permission` objeto que você criou).
   * Crie a entidade de segurança da política chamando o `InfomodelObjectFactory` estática do objeto `createSpecialPrincipal` método. Transmita um membro de dados que pertença a `InfomodelObjectFactory` objeto que representa o principal. Este método retorna um valor de `Principal` objeto. Por exemplo, para adicionar o editor do documento como principal, passe `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Adicione o principal à entrada de política chamando o `PolicyEntry` do objeto `setPrincipal`e transmitindo o `Principal` objeto.
   * Adicione a entrada da política à política chamando o `Policy` do objeto `addPolicyEntry` e transmitindo o `PolicyEntry` objeto.

1. Registre a política.

   * Criar um `PolicyManager` ao invocar o `DocumentSecurityClient` do objeto `getPolicyManager` método.
   * Registre a política invocando o `PolicyManager` do objeto `registerPolicy` e transmitindo os seguintes valores:

      * A variável `Policy` objeto que representa a política a ser registrada.

   * Um valor de string que representa o conjunto de políticas ao qual a política pertence.

   Se você usar uma conta de administrador de formulários AEM nas configurações de conexão para criar a variável `DocumentSecurityClient` e, em seguida, especifique o nome do conjunto de políticas quando chamar o `registerPolicy` método. Se você passar um `null` para o conjunto de políticas, a política é criada nos administradores *Minhas Políticas* conjunto de políticas.

   Se você usar um usuário de Segurança de documentos nas configurações de conexão, poderá invocar a sobrecarga `registerPolicy` método que aceita somente a política. Ou seja, não é necessário especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas Políticas*. Se você não quiser adicionar a nova política a este conjunto de políticas, especifique um nome para o conjunto de políticas ao chamar o `registerPolicy` método.

   >[!NOTE]
   >
   >Ao criar uma política, faça referência a um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, será lançada uma exceção.

Para obter exemplos de código usando o serviço de Segurança de documentos, consulte o seguinte:

* &quot;Início rápido (modo SOAP): criação de uma política usando a API Java&quot;

### Criar uma política usando a API do serviço Web {#create-a-policy-using-the-web-service-api}

Crie uma política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina os atributos da política.

   * Criar um `PolicySpec` usando seu construtor.
   * Defina o nome da política atribuindo um valor de string ao `PolicySpec` do objeto `name` membro de dados.
   * Defina a descrição da política atribuindo um valor de string ao `PolicySpec` do objeto `description` membro de dados.
   * Especifique o conjunto de políticas ao qual a política pertence, atribuindo um valor de string ao `PolicySpec` do objeto `policySetName` membro de dados. Especifique um nome de conjunto de políticas existente. (Você pode especificar `null` para este valor de parâmetro que resulta na política sendo adicionada a *Minhas Políticas*.)
   * Defina o período de concessão offline da política atribuindo um valor inteiro ao `PolicySpec` do objeto `offlineLeasePeriod` membro de dados.
   * Defina o `PolicySpec` do objeto `policyXml` membro de dados com um valor de string que representa dados XML PDRL. Para executar esta tarefa, crie um .NET `StreamReader` usando seu construtor. Transmita o local de um arquivo XML PDRL que representa a política para o `StreamReader` construtor. Em seguida, chame o `StreamReader` do objeto `ReadLine` e atribua o valor de retorno a uma variável de string. Repita através do `StreamReader` até que o `ReadLine` o método retorna nulo. Atribua a variável de string ao `PolicySpec` do objeto `policyXml` membro de dados.

1. Criar uma entrada de política.

   Não é necessário criar uma entrada de política ao criar uma política usando a API do serviço Web de Segurança de documentos. A entrada de política é definida no documento PDRL.

1. Registre a política.

   Registre a política invocando o `DocumentSecurityServiceClient` do objeto `registerPolicy` e transmitindo os seguintes valores:

   * A variável `PolicySpec` objeto que representa a política a ser registrada.
   * Um valor de string que representa o conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na adição da política ao *Minhas Políticas* conjunto de políticas.

   Se você usar uma conta de administrador de formulários AEM nas configurações de conexão para criar a variável `DocumentSecurityClient` objeto, especifique o nome do conjunto de políticas quando chamar o `registerPolicy` método.

   Se você usar um usuário de Segurança de documentos nas configurações de conexão, poderá invocar a sobrecarga `registerPolicy` método que aceita somente a política. Ou seja, não é necessário especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas Políticas*. Se você não quiser adicionar a nova política a este conjunto de políticas, especifique um nome para o conjunto de políticas ao chamar o `registerPolicy` método.

   >[!NOTE]
   >
   >Ao criar uma política e especificar um conjunto de políticas, certifique-se de especificar um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, será lançada uma exceção.

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): criação de uma política usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): criação de uma política usando a API de serviço Web&quot;

## Modificação de Políticas {#modifying-policies}

Você pode modificar uma política existente usando a API Java de Segurança de documentos ou a API de serviço da Web. Para alterar uma política existente, você a recupera, modifica e atualiza a política no servidor. Por exemplo, suponha que você recupere uma política existente e estenda seu período de validade. Antes da alteração entrar em vigor, você deve atualizar a política.

É possível modificar uma política quando os requisitos de negócios mudam e a política não reflete mais esses requisitos. Em vez de criar uma política, você pode simplesmente atualizar uma política existente.

Para modificar atributos de política usando um serviço Web (por exemplo, usando classes de proxy Java que foram criadas com JAX-WS), você deve garantir que a política esteja registrada no serviço de Segurança de documentos. É possível fazer referência à política existente usando o `PolicySpec.getPolicyXml` e modificar os atributos da política usando os métodos aplicáveis. Por exemplo, você pode modificar o período de concessão offline chamando a opção `PolicySpec.setOfflineLeasePeriod` método.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para modificar uma política existente, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recuperar uma política existente.
1. Alterar atributos de políticas.
1. Atualize a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos. Se estiver usando a API Java, crie uma `RightsManagementClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `RightsManagementServiceService` objeto.

**Recuperar uma política existente**

Recupere uma política existente para modificá-la. Para recuperar uma política, especifique o nome da política e o conjunto de políticas ao qual a política pertence. Se você especificar um `null` para o nome do conjunto de políticas, a política é recuperada da variável *Minhas Políticas* conjunto de políticas.

**Definir os atributos da política**

Para modificar uma política, você modifica o valor dos atributos da política. O único atributo de política que não pode ser alterado é o atributo de nome. Por exemplo, para alterar o período de concessão offline da política, você pode modificar o valor do atributo de período de concessão offline da política.

Ao modificar o período de concessão off-line de uma política usando um serviço Web, a variável `offlineLeasePeriod` no campo `PolicySpec` A interface do é ignorada. Para atualizar o período de concessão offline, modifique o `OfflineLeasePeriod` elemento no documento XML PDRL. Em seguida, faça referência ao documento XML PDRL atualizado usando o `PolicySpec` da interface `policyXML` membro de dados.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte `Policy` descrição da interface no [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Atualizar a política**

Antes que as alterações feitas em uma política entrem em vigor, é necessário atualizar a política com o serviço de Segurança de documentos. As alterações nas políticas que estão protegendo documentos são atualizadas na próxima vez que o documento protegido por política for sincronizado com o serviço de Segurança de documentos.

### Modificar políticas existentes usando a API Java {#modify-existing-policies-using-the-java-api}

Modifique uma política existente usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar uma política existente.

   * Criar um `PolicyManager` ao invocar o `RightsManagementClient` do objeto `getPolicyManager` método.
   * Criar um `Policy` objeto que representa a política a ser atualizada chamando o `PolicyManager` do objeto `getPolicy` e transmitindo os seguintes valores&quot;

      * Um valor de string que representa o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
      * Um valor de string que representa o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às necessidades dos negócios. Por exemplo, para alterar o período de concessão offline da política, chame o `Policy` do objeto `setOfflineLeasePeriod` método.

1. Atualize a política.

   Atualizar a política chamando `PolicyManager` do objeto `updatePolicy` método. Passe o `Policy` objeto que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte Início rápido (modo SOAP): modificação de uma política usando a seção API do Java.

### Modificar políticas existentes usando a API do serviço Web {#modify-existing-policies-using-the-web-service-api}

Modifique uma política existente usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar uma política existente.

   Criar um `PolicySpec` objeto que representa a política a ser modificada chamando o `RightsManagementServiceClient` do objeto `getPolicy` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às necessidades dos negócios.

1. Atualize a política.

   Atualize a política chamando o `RightsManagementServiceClient` do objeto `updatePolicyFromSDK` e transmitindo o `PolicySpec` objeto que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): modificação de uma política usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): modificação de uma política usando a API do serviço Web&quot;

## Exclusão de Políticas {#deleting-policies}

Você pode excluir uma política existente usando a API Java de segurança de documentos ou a API de serviço da Web. Depois que uma política é excluída, ela não pode mais ser usada para proteger documentos. No entanto, os documentos protegidos por política que estão usando a política ainda estão protegidos. É possível excluir uma política quando uma mais recente estiver disponível.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para deletar uma política existente, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Exclua a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos. Se estiver usando a API Java, crie uma `RightsManagementClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `RightsManagementServiceService` objeto.

**Excluir a política**

Para excluir uma política, especifique a política a ser excluída e o conjunto de políticas ao qual a política pertence. O usuário cujas configurações são usadas para chamar o AEM Forms deve ter permissão para excluir a política; caso contrário, ocorre uma exceção. Da mesma forma, se você tentar excluir uma política que não existe, ocorre uma exceção.

### Excluir políticas usando a API do Java {#delete-policies-using-the-java-api}

Exclua uma política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Exclua a política.

   * Criar um `PolicyManager` ao invocar o `RightsManagementClient` do objeto `getPolicyManager` método.
   * Exclua a política invocando o `PolicyManager` do objeto `deletePolicy` e transmitindo os seguintes valores:

      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
      * Um valor de string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): exclusão de uma política usando a API Java&quot;

### Excluir políticas usando a API do serviço Web {#delete-policies-using-the-web-service-api}

Exclua uma política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Exclua a política.

   Exclua uma política invocando o `RightsManagementServiceClient` do objeto `deletePolicy` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
   * Um valor de string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): exclusão de uma política usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): exclusão de uma política usando a API de serviço Web&quot;

## Aplicação de políticas a documentos do PDF {#applying-policies-to-pdf-documents}

Você pode aplicar uma política a um documento PDF para proteger o documento. Ao aplicar uma política a um documento PDF, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se ele já estiver protegido por uma política.

Enquanto o documento estiver aberto, você também poderá restringir o acesso aos recursos do Acrobat e do Adobe Reader, incluindo a capacidade de imprimir e copiar texto, fazer alterações e adicionar assinaturas e comentários a um documento. Além disso, você pode revogar um documento PDF protegido por política quando não quiser mais que os usuários acessem o documento.

Você pode monitorar o uso de um documento protegido por política após distribuí-lo. Ou seja, você pode ver como o documento está sendo usado e quem está usando-o. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para aplicar uma política a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento PDF ao qual uma política seja aplicada.
1. Aplique uma política existente ao documento PDF.
1. Salve o documento PDF protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação do serviço de Segurança de documentos, crie um objeto de cliente desse serviço. Se estiver usando a API Java, crie uma `DocumentSecurityClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `DocumentSecurityServiceService` objeto.

**Recuperar um documento PDF**

Você pode recuperar um documento PDF para aplicar uma política. Depois de aplicar uma política ao documento PDF, os usuários ficam restritos ao usar o documento. Por exemplo, se a política não permitir que o documento seja aberto offline, os usuários deverão estar online para abrir o documento.

**Aplicar uma política existente ao documento PDF**

Para aplicar uma política a um documento PDF, faça referência a uma política existente e especifique a qual política a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salve o documento PDF**

Depois que o serviço de Segurança de documentos aplicar uma política a um documento PDF, você poderá salvar o documento PDF protegido por política como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogação do acesso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicação de uma política a um documento PDF usando a API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplique uma política a um documento PDF usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Aplique uma política existente ao documento PDF.

   * Criar um `DocumentManager` ao invocar o `RightsManagementClient` do objeto `getDocumentManager` método.
   * Aplique uma política ao documento PDF invocando o `DocumentManager` do objeto `protectDocument` e transmitindo os seguintes valores:

      * A variável `com.adobe.idp.Document` objeto que contém o documento PDF ao qual a política é aplicada.
      * Um valor de cadeia de caracteres que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o publicador do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser nulo).
      * Um valor de string que representa o nome canônico do usuário gerente do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se este parâmetro for nulo, o valor do parâmetro anterior deverá ser `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e não é usado para documentos PDF. Para proteger um documento PDF, especifique `null`.

     A variável `protectDocument` o método retorna um `RMSecureDocumentResult` objeto que contém o documento PDF protegido por política.

1. Salve o documento PDF.

   * Chame o `RMSecureDocumentResult` do objeto `getProtectedDoc` para obter o documento PDF protegido por política. Este método retorna um valor de `com.adobe.idp.Document` objeto.
   * Criar um `java.io.File` e verifique se a extensão do arquivo é PDF.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `getProtectedDoc` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo EJB): aplicando uma política a um documento PDF usando a API Java&quot;
* &quot;Início rápido (modo SOAP): aplicação de uma política a um documento PDF usando a API Java&quot;

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicação de uma política a um documento PDF usando a API de serviço Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplique uma política a um documento PDF usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF ao qual uma política é aplicada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Aplique uma política existente ao documento PDF.

   Aplique uma política ao documento PDF invocando o `RightsManagementServiceClient` do objeto `protectDocument` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento PDF ao qual a política é aplicada.
   * Um valor de cadeia de caracteres que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o publicador do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser `null`).
   * Um valor de string que representa o nome canônico do usuário gerente do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor do parâmetro anterior deverá ser `null`).
   * A `RMLocale` valor que especifica o valor do local (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída da string usado para armazenar o valor do identificador da política.
   * Um parâmetro de saída da string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída da string que é usado para armazenar o tipo MIME (por exemplo, `application/pdf`).

   A variável `protectDocument` o método retorna um `BLOB` objeto que contém o documento PDF protegido por política.

1. Salve o documento PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `protectDocument` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): aplicação de uma política a um documento PDF usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): aplicação de uma política a um documento PDF usando a API de serviço Web &quot;

## Remoção de políticas de documentos do PDF {#removing-policies-from-pdf-documents}

Você pode remover uma política de um documento protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se você quiser atualizar um documento protegido por política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, será mais eficiente alternar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para remover uma política de um documento de PDF protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento PDF protegido por política.
1. Remova a política do documento PDF.
1. Salve o documento PDF não seguro.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação do serviço de Segurança de documentos, crie um objeto de cliente desse serviço.

**Recuperar um documento PDF protegido por política**

Você pode recuperar um documento de PDF protegido por política para remover uma política. Se você tentar remover uma política de um documento PDF que não está protegido por uma política, causará uma exceção.

**Remover a política do documento PDF**

Você pode remover uma política de um documento PDF protegido por política desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deve conter a `SWITCH_POLICY` permissão para remover uma política de um documento PDF. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salve o documento PDF não seguro**

Depois que o serviço de Segurança de documentos remover uma política de um documento PDF, você poderá salvar o documento PDF não seguro como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos do PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Remover uma política de um documento PDF usando a API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Remova uma política de um documento PDF protegido por política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF protegido por política.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova a política do documento PDF.

   * Criar um `DocumentManager` ao invocar o `DocumentSecurityClient` do objeto `getDocumentManager` método.
   * Remova uma política do documento PDF invocando o `DocumentManager` do objeto `removeSecurity` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF protegido por política. Este método retorna um valor de `com.adobe.idp.Document` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF não seguro.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é PDF.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `removeSecurity` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): remoção de uma política de um documento PDF usando a API Java&quot;

### Remover uma política usando a API do serviço Web {#remove-a-policy-using-the-web-service-api}

Remova uma política de um documento PDF protegido por política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF protegido por política.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF protegido por política do qual a política é removida.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova a política do documento PDF.

   Remova a política do documento PDF chamando o `DocumentSecurityServiceClient` do objeto `removePolicySecurity` e transmitindo o `BLOB` objeto que contém o documento PDF protegido por política. Este método retorna um valor de `BLOB` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF não seguro.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `removePolicySecurity` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): remoção de uma política de um documento PDF usando a API de serviço Web &quot;
* &quot;Início rápido (SwaRef): remoção de uma política de um documento PDF usando a API de serviço Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revogação do acesso a documentos {#revoking-access-to-documents}

É possível revogar o acesso a um documento de PDF protegido por política, resultando na inacessibilidade de todas as cópias do documento para os usuários. Quando um usuário tenta abrir um documento de PDF revogado, ele é redirecionado para um URL especificado, no qual um documento revisado pode ser visualizado. A URL para onde o usuário é redirecionado deve ser especificada de forma programática. Quando você revoga o acesso a um documento, a alteração entra em vigor na próxima vez que o usuário sincronizar com o serviço de Segurança de documentos, abrindo o documento protegido por política online.

A capacidade de revogar o acesso a um documento oferece segurança adicional. Por exemplo, suponha que uma versão mais recente de um documento esteja disponível e você não deseja mais que ninguém visualize a versão desatualizada. Nessa situação, o acesso ao documento mais antigo pode ser revogado, e ninguém poderá ver o documento, a menos que o acesso seja restabelecido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para revogar um documento protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento PDF protegido por política.
1. Revogue o documento protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos.

**Recuperar um documento PDF protegido por política**

Recupere um documento PDF protegido por política para revogá-lo. Não é possível revogar um documento que já tenha sido revogado ou que não seja um documento protegido por política.

Se você souber o valor do identificador de licença do documento protegido por política, não será necessário recuperar o documento PDF protegido por política. No entanto, na maioria dos casos, você deve recuperar o documento PDF para obter o valor do identificador de licença.

**Revogar o documento protegido por política**

Para revogar um documento protegido por política, especifique o identificador de licença do documento protegido por política. Além disso, você pode especificar o URL de um documento que o usuário pode visualizar quando tentar abrir o documento revogado. Ou seja, suponha que um documento desatualizado seja revogado. Quando um usuário tenta abrir o documento revogado, ele verá um documento atualizado em vez do documento revogado.

>[!NOTE]
>
>Se você tentar revogar um documento já revogado, uma exceção será lançada.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos do PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Restauração do Acesso a Documentos Revogados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revogar acesso a documentos usando a API Java {#revoke-access-to-documents-using-the-java-api}

Revogue o acesso a um documento de PDF protegido por política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente de segurança de documentos

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento PDF protegido por política

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Revogar o documento protegido por política

   * Criar um `DocumentManager` ao invocar o `DocumentSecurityClient` do objeto `getDocumentManager` método.
   * Recupere o valor do identificador de licença do documento protegido por política chamando o `DocumentManager` do objeto `getLicenseId` método. Passe o `com.adobe.idp.Document` objeto que representa o documento protegido por política. Este método retorna um valor de string que representa o valor do identificador da licença.
   * Criar um `LicenseManager` ao invocar o `DocumentSecurityClient` do objeto `getLicenseManager` método.
   * Revogue o documento protegido por política chamando o `LicenseManager` do objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do `DocumentManager` do objeto `getLicenseId` método).
      * Um membro de dados estático do `License` interface que especifica o motivo para revogar o documento. Por exemplo, você pode especificar `License.DOCUMENT_REVISED`.
      * A `java.net.URL` valor que especifica a localização onde um documento revisado está localizado. Se não quiser redirecionar um usuário para outro URL, você poderá enviar `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): Revogação de um documento usando a API Java&quot;

### Revogar acesso a documentos usando a API do serviço Web {#revoke-access-to-documents-using-the-web-service-api}

Revogue o acesso a um documento de PDF protegido por política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de segurança de documentos

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar um documento PDF protegido por política

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF protegido por política que é revogado.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido por política a ser revogado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Revogar o documento protegido por política

   * Recupere o valor do identificador de licença do documento protegido por política chamando o `DocumentSecurityServiceClient` do objeto `getLicenseID` e transmitindo o `BLOB` objeto que representa o documento protegido por política. Este método retorna um valor de string que representa o identificador da licença.
   * Revogue o documento protegido por política chamando o `DocumentSecurityServiceClient` do objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do `DocumentSecurityServiceService` do objeto `getLicenseId` método).
      * Um membro de dados estático do `Reason` enum que especifica o motivo para revogar o documento. Por exemplo, você pode especificar `Reason.DOCUMENT_REVISED`.
      * A `string` valor que especifica a localização do URL onde um documento revisado está localizado. Se não quiser redirecionar um usuário para outro URL, você poderá enviar `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): Revogação de um documento usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): Revogação de um documento usando a API de serviço Web&quot;

**Consulte também**

[Removendo Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Restauração do Acesso a Documentos Revogados {#reinstating-access-to-revoked-documents}

Você pode restabelecer o acesso a um documento de PDF revogado, fazendo com que todas as cópias do documento revogado fiquem acessíveis aos usuários. Quando um usuário abre um documento restabelecido que foi revogado, ele pode exibir o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para restabelecer o acesso a um documento de PDF revogado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere o identificador de licença do documento de PDF revogado.
1. Restaure o acesso ao documento de PDF revogado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos. Se estiver usando a API Java, crie uma `DocumentSecurityClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `DocumentSecurityServiceService` objeto.

**Recuperar o identificador de licença do documento PDF revogado**

Recupere o identificador de licença do documento de PDF revogado para restaurar um documento de PDF revogado. Após obter o valor do identificador de licença, é possível restaurar um documento revogado. Se você tentar restabelecer um documento que não foi revogado, causará uma exceção.

**Restaurar o acesso ao documento de PDF revogado**

Para restabelecer o acesso a um documento de PDF revogado, você deve especificar o identificador de licença do documento revogado. Se você tentar restabelecer o acesso a um documento PDF que não foi revogado, você causará uma exceção.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos do PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revogação do acesso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Restaurar o acesso a documentos revogados usando a API do Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Restaure o acesso a um documento revogado usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o identificador de licença do documento de PDF revogado.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF revogado usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.
   * Criar um `DocumentManager` ao invocar o `DocumentSecurityClient` do objeto `getDocumentManager` método.
   * Recupere o valor do identificador de licença do documento revogado chamando o `DocumentManager` do objeto `getLicenseId` e transmitindo o `com.adobe.idp.Document` objeto que representa o documento revogado. Este método retorna um valor de string que representa o identificador da licença.

1. Restaure o acesso ao documento de PDF revogado.

   * Criar um `LicenseManager` ao invocar o `DocumentSecurityClient` do objeto `getLicenseManager` método.
   * Restaure o acesso ao documento de PDF revogado invocando o `LicenseManager` do objeto `unrevokeLicense` e transmitindo o valor do identificador de licença do documento revogado.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): restabelecendo o acesso a um documento revogado usando a API de serviço da Web&quot;

### Restaurar o acesso a documentos revogados usando a API do serviço da Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Restaure o acesso a um documento revogado usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o identificador de licença do documento de PDF revogado.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento de PDF revogado ao qual o acesso é restabelecido.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF revogado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Restaure o acesso ao documento de PDF revogado.

   * Recupere o valor do identificador de licença do documento revogado chamando o `DocumentSecurityServiceClient` do objeto `getLicenseID` e transmitindo o `BLOB` objeto que representa o documento revogado. Este método retorna um valor de string que representa o identificador da licença.
   * Restaure o acesso ao documento de PDF revogado invocando o `DocumentSecurityServiceClient` do objeto `unrevokeLicense` e transmitindo um valor de string que especifica o valor do identificador de licença do documento de PDF revogado (transmita o valor de retorno do `DocumentSecurityServiceClient` do objeto `getLicenseId` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): restabelecendo o acesso a um documento revogado usando a API de serviço Web&quot;
* &quot;Início Rápido (SwaRef): restabelecimento do acesso a um documento revogado usando a API de serviço Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Inspeção de Documentos PDF Protegidos por Política {#inspecting-policy-protected-pdf-documents}

Você pode usar a API do serviço de segurança de documentos (Java e serviço da Web) para inspecionar documentos de PDF protegidos por política. A inspeção de documentos PDF protegidos por política retorna informações sobre o documento PDF protegido por política. Você pode, por exemplo, determinar a política usada para proteger o documento e a data em que o documento foi protegido.

Não é possível executar essa tarefa se a sua versão do LiveCycle for 8.x ou anterior. O suporte para inspecionar documentos protegidos por política foi adicionado no AEM Forms. Se você tentar inspecionar um documento protegido por política usando o LiveCycle 8.x (ou anterior), ocorrerá uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para inspecionar um documento de PDF protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento protegido por política para inspecionar.
1. Obter informações sobre o documento protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação do serviço de Segurança de documentos, crie um objeto de cliente desse serviço. Se estiver usando a API Java, crie uma `RightsManagementClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `RightsManagementServiceService` objeto.

**Recuperar um documento protegido por política para inspecionar**

Para inspecionar um documento protegido por política, recupere-o. Se você tentar inspecionar um documento que não é seguro com uma política ou que foi revogado, uma exceção será lançada.

**Inspect o documento**

Após recuperar um documento protegido por política, você pode inspecioná-lo.

**Obter informações sobre o documento protegido por política**

Depois de inspecionar um documento de PDF protegido por política, você pode obter informações sobre ele. Por exemplo, você pode determinar a política usada para proteger o documento.

Se você proteger um documento com uma política que pertença a Minhas políticas e chamar `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, null é retornado.

Se o documento estiver protegido usando uma política contida em um conjunto de políticas (diferente de Minhas Políticas), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` retornar strings válidas.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documentos do Inspect Policy Protected PDF usando a API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

O Inspect é um documento PDF protegido por política usando a API do serviço de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento protegido por política para inspecionar.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF protegido por política usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Inspect o documento.

   * Criar um `DocumentManager` ao invocar o `RightsManagementClient` do objeto `getDocumentManager` método.
   * Inspect o documento protegido por política invocando o `LicenseManager` do objeto `inspectDocument` método. Passe o `com.adobe.idp.Document` objeto que contém o documento PDF protegido por política. Este método retorna um valor de `RMInspectResult` objeto que contém informações sobre o documento protegido por política.

1. Obter informações sobre o documento protegido por política.

   Para obter informações sobre o documento protegido por política, chame o método apropriado que pertence a `RMInspectResult` objeto. Por exemplo, para recuperar o nome da política, chame o `RMInspectResult` do objeto `getPolicyName` método.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): inspeção de documentos PDF protegidos por política usando a API Java&quot;

### Documentos do Inspect Policy Protected PDF usando a API de serviço Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

O Inspect é um documento PDF protegido por política usando a API do serviço de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento protegido por política para inspecionar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF para inspeção.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Inspect o documento.

   Inspect o documento protegido por política invocando o `RightsManagementServiceClient` do objeto `inspectDocument` método. Passe o `BLOB` objeto que contém o documento PDF protegido por política. Este método retorna um valor de `RMInspectResult` objeto que contém informações sobre o documento protegido por política.

1. Obter informações sobre o documento protegido por política.

   Para obter informações sobre o documento protegido por política, obtenha o valor do campo apropriado que pertence à `RMInspectResult` objeto. Por exemplo, para recuperar o nome da política, obtenha o valor do `RMInspectResult` do objeto `policyName` campo.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): inspecionando documentos de PDF protegidos por política usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): inspecionando documentos de PDF protegidos por política usando a API de serviço Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de marcas d&#39;água {#creating-watermarks}

As marcas d&#39;água ajudam a garantir a segurança de um documento, identificando exclusivamente o documento e controlando a violação de direitos autorais. Por exemplo, você pode criar e colocar uma marca d&#39;água que digite Confidencial em todas as páginas de um documento. Depois que uma marca d&#39;água é criada, você pode incluí-la como parte de uma política. Ou seja, você pode definir o atributo de marca d&#39;água da política com a marca d&#39;água recém-criada. Depois que uma política que contém uma marca d&#39;água é aplicada a um documento, a marca d&#39;água é exibida no documento protegido por política.

>[!NOTE]
>
>Somente usuários com privilégios administrativos de Segurança de documentos podem criar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança de documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para criar uma marca d&#39;água, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Defina os atributos de marca d&#39;água.
1. Registre a marca d&#39;água no serviço de Segurança de documentos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos. Se estiver usando a API Java, crie uma `RightsManagementClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `RightsManagementServiceService` objeto.

**Definir os atributos de marca d&#39;água**

Para criar uma marca d&#39;água, você deve definir atributos de marca d&#39;água. O atributo name deve ser sempre definido. Além do atributo name, você deve definir pelo menos um dos seguintes atributos:

* Texto personalizado
* DateIncluded
* UserIdIncluded
* NomeUsuárioIncluído

A tabela a seguir lista os pares de chaves e valores necessários ao criar uma marca d&#39;água usando serviços da Web.

<table>
 <thead>
  <tr>
   <th><p>Nome da chave</p></th>
   <th><p>Descrição</p></th>
   <th><p>Valor</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>Especifica se o nome de usuário do usuário que abre o documento faz parte da marca d'água.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Especifica se a identificação do usuário que abre o documento faz parte da marca d'água.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Especifica se a data atual faz parte da marca d'água.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Se esse valor for true, o valor do texto personalizado deverá ser especificado usando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Especifica a opacidade da marca d'água. O valor padrão é 0,5 se não for especificado.</p></td>
   <td><p>Um valor entre 0,0 e 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Especifica a rotação da marca d'água. O valor padrão é 0 graus.</p></td>
   <td><p>Um valor entre 0-359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Se esse valor for especificado, então <code>WaterBackCmd:IS_SIZE_ENABLED</code> deve estar presente e o valor deve ser true. Se esse atributo não for especificado, o comportamento padrão será ajustar à página.</p></td>
   <td><p>Um valor maior que 0,0 e menor ou igual a 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Especifica o alinhamento horizontal da marca d'água. O valor padrão é center.</p></td>
   <td><p>esquerda, centro ou direita</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Especifica o alinhamento vertical da marca d'água. O valor padrão é center.</p></td>
   <td><p>superior, centro ou inferior</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Especifica se a marca d'água é um plano de fundo. O valor padrão é false.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>Verdadeiro se uma escala personalizada for especificada. Se esse valor for true, SCALE também deverá ser especificado. Se esse valor for falso, o padrão será Ajustar à página.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica o texto personalizado de uma marca d'água. Se esse valor estiver presente, então <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> também deve estar presente e definido como true.</p></td>
   <td><p>Verdadeiro ou falso</p></td>
  </tr>
 </tbody>
</table>

Todas as marcas d&#39;água devem ter um dos seguintes atributos definidos:

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

Todos os outros atributos são opcionais.

**Registrar a marca d&#39;água**

Uma nova marca d&#39;água deve ser registrada no serviço de Segurança de documentos antes de ser usada. Depois de registrar uma marca d&#39;água, você pode usá-la em políticas.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos do PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Criar marcas d&#39;água usando a API Java {#create-watermarks-using-the-java-api}

Crie uma marca d&#39;água usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Incluir arquivos JAR do cliente, como o `adobe-rightsmanagement-client.jar`, no caminho de classe do projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir os atributos da marca d&#39;água

   * Criar um `Watermark` ao invocar o `InfomodelObjectFactory` estática do objeto `createWatermark` método. Este método retorna um valor de `Watermark` objeto.
   * Defina o atributo de nome da marca d&#39;água chamando o `Watermark` do objeto `setName` e transmitindo um valor de string que especifica o nome da política.
   * Defina o atributo de plano de fundo da marca d&#39;água chamando o `Watermark` do objeto `setBackground` método e transmissão `true`. Ao configurar esse atributo, a marca d&#39;água aparece no plano de fundo do documento.
   * Defina o atributo de texto personalizado da marca d&#39;água chamando o `Watermark` do objeto `setCustomText` e transmitindo um valor de string que representa o texto da marca d&#39;água.
   * Defina o atributo de opacidade da marca d&#39;água chamando o `Watermark` do objeto `setOpacity` e transmitindo um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

1. Registre a marca d&#39;água.

   * Criar um `WatermarkManager` ao invocar o `RightsManagementClient` do objeto `getWatermarkManager` método. Este método retorna um valor de `WatermarkManager` objeto.
   * Registre a marca d&#39;água invocando o `WatermarkManager` do objeto `registerWatermark` e transmitindo o `Watermark` objeto que representa a marca d&#39;água a ser registrada. Esse método retorna um valor de string que representa o valor de identificação da marca d&#39;água.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (modo SOAP): criação de uma marca d&#39;água usando a API Java&quot;

### Criar marcas d&#39;água usando a API do serviço Web {#create-watermarks-using-the-web-service-api}

Crie uma marca d&#39;água usando a API de segurança de documentos (serviço da Web):

1. Crie um objeto de API do cliente de Segurança de documentos.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Defina os atributos da marca d&#39;água.

   * Criar um `WatermarkSpec` ao invocar o `WatermarkSpec` construtor.
   * Defina o nome da marca d&#39;água atribuindo um valor de string ao `WatermarkSpec` do objeto `name` membro de dados.
   * Definir a marca d&#39;água `id` atribuindo um valor de string à variável `WatermarkSpec` do objeto `id` membro de dados.
   * Para cada propriedade de marca d&#39;água a ser definida, crie uma `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Defina o valor da chave atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` membro de dados (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` membro de dados (por exemplo, `.25`).
   * Criar um `MyArrayOf_xsd_anyType` objeto. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, chame o `MyArrayOf_xsd_anyType` do objeto `Add` método. Passe o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua a `MyArrayOf_xsd_anyType` objeto para o `WatermarkSpec` do objeto `values` membro de dados.

1. Registre a marca d&#39;água.

   Registre a marca d&#39;água invocando o `RightsManagementServiceClient` do objeto `registerWatermark` e transmitindo o `WatermarkSpec` objeto que representa a marca d&#39;água a ser registrada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): criação de uma marca d&#39;água usando a API de serviço Web&quot;
* &quot;Início rápido (SwaRef): criação de uma marca d&#39;água usando a API do serviço Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificação de Marcas D&#39;Água {#modifying-watermarks}

Você pode modificar uma marca d&#39;água existente usando a API Java de Segurança de documentos ou a API de serviço da Web. Para alterar uma marca d&#39;água existente, você a recupera, modifica seus atributos e a atualiza no servidor. Por exemplo, suponha que você recupere uma marca d&#39;água e modifique seu atributo de opacidade. Antes da alteração entrar em vigor, você deve atualizar a marca d&#39;água.

Quando você modifica uma marca d&#39;água, a alteração afeta documentos futuros que têm a marca d&#39;água aplicada a eles. Ou seja, os documentos PDF existentes que contêm a marca d&#39;água não são afetados.

>[!NOTE]
>
>Somente usuários com privilégios administrativos de Segurança de documentos podem modificar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança de documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-9}

Para modificar uma marca d&#39;água, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere a marca d&#39;água a ser modificada.
1. Defina os atributos de marca d&#39;água.
1. Atualize a marca d&#39;água.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos. Se estiver usando a API Java, crie uma `DocumentSecurityClient` objeto. Se estiver usando a API do serviço Web de Segurança de documentos, crie uma `DocumentSecurityServiceService` objeto.

**Recuperar a marca d&#39;água para modificar**

Para modificar uma marca d&#39;água, você deve recuperar uma marca d&#39;água existente. Você pode recuperar uma marca d&#39;água especificando seu nome ou seu valor de identificador.

**Definir os atributos de marca d&#39;água**

Para modificar uma marca d&#39;água existente, altere o valor de um ou mais atributos de marca d&#39;água. Ao atualizar programaticamente uma marca d&#39;água usando um serviço da Web, você deve definir todos os atributos que foram originalmente definidos, mesmo que o valor não seja alterado. Por exemplo, suponha que os seguintes atributos de marca d&#39;água estejam definidos: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`, e `WaterBackCmd:SRCTEXT`. Embora o único atributo que você deseja modificar seja `WaterBackCmd:OPACITY`, você deve definir os outros valores como well.

>[!NOTE]
>
>Ao usar a API Java para modificar uma marca d&#39;água, não é necessário especificar todos os atributos. Defina o atributo de marca d&#39;água que você deseja modificar.

>[!NOTE]
>
>Para obter informações sobre os nomes dos atributos de marca d&#39;água, consulte [Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks).

**Atualizar a marca d&#39;água**

Depois de modificar os atributos de uma marca d&#39;água, você deve atualizar a marca d&#39;água.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks)

### Modificar marcas d&#39;água usando a API Java {#modify-watermarks-using-the-java-api}

Modifique uma marca d&#39;água usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere a marca d&#39;água a ser modificada.

   Criar um `WatermarkManager` ao invocar o `DocumentSecurityClient` do objeto `getWatermarkManager` e transmitem um valor de string que especifica o nome da marca d&#39;água. Este método retorna um valor de `Watermark` objeto que representa a marca d&#39;água a ser modificada.

1. Defina os atributos da marca d&#39;água.

   Defina o atributo de opacidade da marca d&#39;água chamando o `Watermark` do objeto `setOpacity` e transmitindo um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

   >[!NOTE]
   >
   >Esse exemplo modifica somente o atributo de opacidade.

1. Atualize a marca d&#39;água.

   * Atualize a marca d&#39;água chamando o `WatermarkManager` do objeto `updateWatermark` e transmita o `Watermark` objeto cujo atributo foi modificado.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte Início rápido (modo SOAP): modificação de uma marca d&#39;água usando a seção API Java.

### Modificar marcas d&#39;água usando a API do serviço Web {#modify-watermarks-using-the-web-service-api}

Modifique uma marca d&#39;água usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere a marca d&#39;água a ser modificada.

   Recupere a marca d&#39;água a ser modificada chamando o `DocumentSecurityServiceClient` do objeto `getWatermarkByName` método. Transmita um valor de string que especifique o nome da marca d&#39;água. Este método retorna um valor de `WatermarkSpec` objeto que representa a marca d&#39;água a ser modificada.

1. Defina os atributos da marca d&#39;água.

   * Para cada propriedade de marca d&#39;água a ser atualizada, crie uma `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Defina o valor da chave atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` membro de dados (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` membro de dados (por exemplo, `.50`).
   * Criar um `MyArrayOf_xsd_anyType` objeto. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, chame o `MyArrayOf_xsd_anyType` do objeto `Add` método. Passe o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua a `MyArrayOf_xsd_anyType` objeto para o `WatermarkSpec` do objeto `values` membro de dados.

1. Atualize a marca d&#39;água.

   Atualize a marca d&#39;água chamando o `DocumentSecurityServiceClient` do objeto `updateWatermark` e transmitindo o `WatermarkSpec` objeto que representa a marca d&#39;água a ser modificada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): modificação de uma marca d&#39;água usando a API do serviço Web&quot;

## Pesquisando Eventos {#searching-for-events}

O serviço Rights Management rastreia ações específicas à medida que ocorrem, como aplicar uma política a um documento, abrir um documento protegido por política e revogar o acesso a documentos. A auditoria de eventos deve ser habilitada para o serviço Rights Management ou os eventos não são rastreados.

Os eventos se enquadram em uma das seguintes categorias:

* Eventos de administrador são ações relacionadas a um administrador, como a criação de uma conta de administrador.
* Eventos de documento são ações relacionadas a um documento, como fechar um documento protegido por política.
* Eventos de política são ações relacionadas a uma política, como a criação de uma política.
* Eventos de serviço são ações relacionadas ao serviço Rights Management, como sincronização com o diretório de usuário.

Você pode pesquisar eventos específicos usando a API Java do Rights Management ou a API de serviço da Web. Ao pesquisar eventos, você pode executar tarefas, como criar um arquivo de log de determinados eventos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Rights Management, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-10}

Para procurar um evento Rights Management, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Rights Management Client API.
1. Especifique o evento que deseja pesquisar.
1. Procure o evento.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Rights Management**

Antes de executar programaticamente uma operação de serviço de Rights Management, você deve criar um objeto cliente de serviço de Rights Management. Se estiver usando a API Java, crie uma `DocumentSecurityClient` objeto. Se estiver usando a API de serviço Web do Rights Management, crie uma `DocumentSecurityServiceService` objeto.

**Especifique os eventos a serem pesquisados**

Especifique o evento a ser pesquisado. Por exemplo, você pode pesquisar pelo evento de criação de política, que ocorre quando uma nova política é criada.

**Pesquisar o evento**

Depois de especificar o evento a ser pesquisado, você pode usar a API Java do Rights Management ou a API de serviço Web do Rights Management para pesquisar o evento.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Pesquisar eventos usando a API Java {#search-for-events-using-the-java-api}

Procure eventos usando a API de Rights Management (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente do Rights Management

   Criar um `DocumentSecurityClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Especifique os eventos a serem pesquisados

   * Criar um `EventManager` ao invocar o `DocumentSecurityClient` do objeto `getEventManager` método. Este método retorna um valor de `EventManager` objeto.
   * Criar um `EventSearchFilter` invocando seu construtor.
   * Especifique o evento para o qual pesquisar chamando o `EventSearchFilter` do objeto `setEventCode` e transmitir um membro de dados estático que pertença ao `EventManager` classe que representa o evento que deve ser pesquisado. Por exemplo, para pesquisar o evento de criação de política, passe `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Você pode definir critérios de pesquisa adicionais chamando `EventSearchFilter` métodos de objeto. Por exemplo, chame o `setUserName` para especificar um usuário associado ao evento.

1. Pesquisar o evento

   Procure o evento chamando o `EventManager` do objeto `searchForEvents` e transmitindo o `EventSearchFilter` objeto que define os critérios de pesquisa do evento. Este método retorna uma matriz de `Event` objetos.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Quick Starts:

* &quot;Início rápido (SOAP): procurando eventos usando a API Java&quot;

### Pesquisar eventos usando a API de serviço Web {#search-for-events-using-the-web-service-api}

Procure eventos usando a API do Rights Management (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto da API do cliente do Rights Management

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Especifique os eventos a serem pesquisados

   * Criar um `EventSpec` usando seu construtor.
   * Especifique o início do período durante o qual o evento ocorreu definindo o `EventSpec` do objeto `firstTime.date` membro de dados com `DataTime` instância que representa o início do intervalo de datas quando o evento ocorreu.
   * Atribuir o valor `true` para o `EventSpec` do objeto `firstTime.dateSpecified` membro de dados.
   * Especifique o fim do período durante o qual o evento ocorreu definindo o `EventSpec` do objeto `lastTime.date` membro de dados com `DataTime` instância que representa o fim do intervalo de datas em que o evento ocorreu.
   * Atribuir o valor `true` para o `EventSpec` do objeto `lastTime.dateSpecified` membro de dados.
   * Defina o evento a ser pesquisado atribuindo um valor de string ao `EventSpec` do objeto `eventCode` membro de dados. A tabela a seguir lista os valores numéricos que você pode atribuir a essa propriedade:

   <table>
    <thead>
    <tr>
    <th><p>Tipo de evento</p></th>
    <th><p>Valor</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. Pesquisar o evento

   Procure o evento chamando o `DocumentSecurityServiceClient` do objeto `searchForEvents` e transmitindo o `EventSpec` objeto que representa o evento que deve ser pesquisado e o número máximo de resultados. Este método retorna um valor de `MyArrayOf_xsd_anyType` coleção em que cada elemento é um `AuditSpec` instância. Uso de um `AuditSpec` instância, você pode obter informações sobre o evento, como a hora em que ele ocorreu. A variável `AuditSpec` a instância contém um `timestamp` membro de dados que especifica essas informações.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Quick Starts:

* &quot;Início rápido (MTOM): procurando eventos usando a API de serviço da Web&quot;
* &quot;Início rápido (SwaRef): procurando eventos usando a API de serviço da Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicando Políticas a Documentos do Word {#applying-policies-to-word-documents}

Além de documentos PDF, o serviço Rights Management suporta formatos de documento adicionais, como um documento do Microsoft Word (arquivo DOC) e outros formatos de arquivo do Microsoft Office. Por exemplo, você pode aplicar uma política a um documento do Word para protegê-lo. Ao aplicar uma política a um documento do Word, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se ele já estiver protegido por uma política.

Você pode monitorar o uso de um documento do Word protegido por política após distribuí-lo. Ou seja, você pode ver como o documento está sendo usado e quem está usando-o. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-11}

Para aplicar uma política a um documento do Word, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento do Word ao qual uma política é aplicada.
1. Aplicar uma política existente ao documento do Word.
1. Salve o documento do Word protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documentos, você deve criar um objeto cliente de serviço de Segurança de documentos.

**Recuperar um documento do Word**

Recupere um documento do Word para aplicar uma política. Depois de aplicar uma política ao documento do Word, os usuários ficam restritos ao usar o documento. Por exemplo, se a política não permitir que o documento seja aberto offline, os usuários deverão estar online para abrir o documento.

**Aplicar uma política existente ao documento do Word**

Para aplicar uma política a um documento do Word, você deve fazer referência a uma política existente e especificar a qual política a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salve o documento do Word**

Depois que o serviço de Segurança de documentos aplicar uma política a um documento do Word, você poderá salvar o documento do Word protegido por política como um arquivo DOC.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogação do acesso a documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar uma política a um documento do Word usando a API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplique uma política a um documento do Word usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocumentSecurityClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento do Word.

   * Criar um `java.io.FileInputStream` objeto que representa o documento do Word usando seu construtor e transmitindo um valor de string que especifica o local do documento do Word.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Aplicar uma política existente ao documento do Word.

   * Criar um `DocumentManager` ao invocar o `DocumentSecurityClient` do objeto `getDocumentManager` método.
   * Aplique uma política ao documento do Word chamando o `DocumentManager` do objeto `protectDocument` e transmitindo os seguintes valores:

      * A variável `com.adobe.idp.Document` objeto que contém o documento do Word ao qual a política é aplicada.
      * Um valor de cadeia de caracteres que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o publicador do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser nulo).
      * Um valor de string que representa o nome canônico do usuário gerente do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se este parâmetro for `null`, o valor do parâmetro anterior deverá ser `null`).
      * A `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e você pode especificar `null`.

     A variável `protectDocument` o método retorna um `RMSecureDocumentResult` objeto que contém o documento do Word protegido por política.

1. Salve o documento do Word.

   * Chame o `RMSecureDocumentResult` do objeto `getProtectedDoc` para obter o documento do Word protegido por política. Este método retorna um valor de `com.adobe.idp.Document` objeto.
   * Criar um `java.io.File` e verifique se a extensão do arquivo é DOC.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `getProtectedDoc` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte o seguinte Início rápido:

* &quot;Início rápido (modo SOAP): aplicação de uma política a um documento do Word usando a API Java&quot;

### Aplicar uma política a um documento do Word usando a API de serviço Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplique uma política a um documento do Word usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de API do cliente de Segurança de documentos.

   * Criar um `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Criar um `DocumentSecurityServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento do Word.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento do Word ao qual uma política é aplicada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Aplicar uma política existente ao documento do Word.

   Aplique uma política ao documento do Word chamando o `DocumentSecurityServiceClient` do objeto `protectDocument` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento do Word ao qual a política é aplicada.
   * Um valor de cadeia de caracteres que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na `MyPolicies` conjunto de políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o publicador do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser `null`).
   * Um valor de string que representa o nome canônico do usuário gerente do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor do parâmetro anterior deverá ser `null`).
   * A `RMLocale` valor que especifica o valor do local (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída da string usado para armazenar o valor do identificador da política.
   * Um parâmetro de saída da string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída da string que é usado para armazenar o tipo MIME (por exemplo, `application/doc`).

   A variável `protectDocument` o método retorna um `BLOB` objeto que contém o documento do Word protegido por política.

1. Salve o documento do Word.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `protectDocument` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo do Word chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): aplicação de uma política a um documento do Word usando a API de serviço Web &quot;

## Removendo Políticas de Documentos do Word {#removing-policies-from-word-documents}

Você pode remover uma política de um documento do Word protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se você quiser atualizar um documento do Word protegido por política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, será mais eficiente alternar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-12}

Para remover uma política de um documento do Word protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto de API do cliente de Segurança de documentos.
1. Recupere um documento do Word protegido por política.
1. Remova a política do documento do Word.
1. Salve o documento do Word não protegido

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação do serviço de Segurança de documentos, crie um objeto de cliente desse serviço.

**Recuperar um documento do Word protegido por política**

Recupere um documento do Word protegido por política para remover uma política. Se você tentar remover uma política de um documento do Word que não esteja protegido por uma política, causará uma exceção.

**Remover a política do documento do Word**

Você pode remover uma política de um documento do Word protegido por política desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deve conter a `SWITCH_POLICY` permissão para remover uma política de um documento do Word. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salvar o documento do Word não protegido**

Depois que o serviço de Segurança de documentos remover uma política de um documento do Word, você poderá salvar o documento do Word não protegido como um arquivo DOC.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicando Políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Remover uma política de um documento do Word usando a API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente de segurança de documentos

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `RightsManagementClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento do Word protegido por política

   * Criar um `java.io.FileInputStream` objeto que representa o documento do Word protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento do Word.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remover a política do documento do Word

   * Criar um `DocumentManager` ao invocar o `RightsManagementClient` do objeto `getDocumentManager` método.
   * Remova uma política do documento do Word chamando o `DocumentManager` do objeto `removeSecurity` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento do Word protegido por política. Este método retorna um valor de `com.adobe.idp.Document` objeto que contém um documento do Word não seguro.

1. Salvar o documento do Word não protegido

   * Criar um `java.io.File` e verifique se a extensão do arquivo é DOC.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `removeSecurity` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte o seguinte Início rápido:

* &quot;Início rápido (modo SOAP): remoção de uma política de um documento do Word usando a API Java &quot;

### Remover uma política de um documento do Word usando a API do serviço Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de segurança de documentos

   * Criar um `RightsManagementServiceClient` usando seu construtor padrão.
   * Criar um `RightsManagementServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperar um documento do Word protegido por política

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento do Word protegido por política do qual a política é removida.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Remover a política do documento do Word

   Remova a política do documento do Word chamando o `RightsManagementServiceClient` do objeto `removePolicySecurity` e transmitindo o `BLOB` objeto que contém o documento do Word protegido por política. Este método retorna um valor de `BLOB` objeto que contém um documento do Word não seguro.

1. Salvar o documento do Word não protegido

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento do Word não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `removePolicySecurity` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documentos, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): remoção de uma política de um documento do Word usando a API de serviço Web&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
