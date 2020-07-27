---
title: Protegendo Documentos com políticas
seo-title: Protegendo Documentos com políticas
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '15466'
ht-degree: 0%

---


# Protegendo Documentos com políticas {#protecting-documents-with-policies}

**Sobre o Serviço de Segurança do Documento**

O serviço de Segurança do Documento permite que os usuários apliquem dinamicamente configurações de confidencialidade a documentos Adobe PDF e mantenham o controle dos documentos, independentemente da sua distribuição.

O serviço de Segurança do Documento impede que as informações se espalhem além do alcance do usuário, permitindo que os usuários mantenham o controle sobre como os recipient usam o documento PDF protegido por política. Um usuário pode especificar quem pode abrir um documento, limitar como ele pode usá-lo e monitorar o documento depois que ele é distribuído. Um usuário também pode controlar dinamicamente o acesso a um documento protegido por política e pode até mesmo revogar dinamicamente o acesso ao documento.

O serviço de Segurança do Documento também protege outros tipos de arquivos, como arquivos do Microsoft Word (arquivos DOC). Você pode usar a API do cliente de segurança do Documento para trabalhar com esses tipos de arquivos. As seguintes versões são suportadas:

* Arquivos do Microsoft Office 2003 (DOC, XLS, arquivos PPT)
* Arquivos do Microsoft Office 2007 (arquivos DOCX, XLSX, PPTX)
* Arquivos PTC Pro/E

Para maior clareza, as duas seções a seguir discutem como trabalhar com documentos do Word:

* [Aplicar políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Remover Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

É possível realizar essas tarefas usando o serviço de Segurança do Documento:

* Criar políticas. Para obter informações, consulte [Criação de políticas](protecting-documents-policies.md#creating-policies).
* Modificar políticas. Para obter informações, consulte [Modificando Políticas](protecting-documents-policies.md#modifying-policies).
* Excluir políticas. Para obter informações, consulte [Excluindo Políticas](protecting-documents-policies.md#deleting-policies).
* Aplicar políticas a documentos PDF. Para obter informações, consulte [Aplicar políticas a Documentos](protecting-documents-policies.md#applying-policies-to-pdf-documents)PDF.
* Remova políticas de documentos PDF. Para obter informações, consulte [Remoção de políticas de Documentos](protecting-documents-policies.md#removing-policies-from-pdf-documents)PDF.
* Inspecione documentos protegidos por política. Para obter informações, consulte [Inspeção de Documentos](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)PDF protegidos por política.
* Revogar o acesso a documentos PDF. Para obter informações, consulte [Revogação do acesso a Documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Reinstale o acesso aos documentos revogados. Para obter informações, consulte [Reposição do acesso a Documentos](protecting-documents-policies.md#reinstating-access-to-revoked-documents)Revogados.
* Criar marcas d&#39;água. Para obter informações, consulte [Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks).
* Procure eventos. Para obter informações, consulte [Procurando Eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criando Políticas {#creating-policies}

Você pode criar políticas programaticamente usando a API Java de segurança do Documento ou a API de serviço da Web. Uma *política* é uma coleção de informações que inclui configurações de segurança do documento, usuários autorizados e direitos de uso. Você pode criar e salvar qualquer número de políticas, usando as configurações de segurança apropriadas para diferentes situações e usuários.

As políticas permitem executar estas tarefas:

* Especifique os indivíduos que podem abrir o documento. Os Recipient podem pertencer ou ser externos à sua organização.
* Especifique como os recipient podem usar o documento. Você pode restringir o acesso a diferentes recursos do Acrobat e do Adobe Reader. Esses recursos incluem a capacidade de imprimir e copiar texto, adicionar assinaturas e adicionar comentários a um documento.
* Altere as configurações de acesso e segurança a qualquer momento, mesmo depois de distribuir o documento protegido por política.
* Monitore o uso do documento depois de distribuí-lo. Você pode ver como o documento está sendo usado e quem o está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

### Criação de uma política usando serviços da Web {#creating-a-policy-using-web-services}

Ao criar uma política usando a API de serviço da Web, consulte um arquivo XML da Linguagem de Direitos do Documento do Portátil (PDRL) que descreve a política. As permissões de política e o principal são definidos no documento PDRL. O documento XML a seguir é um exemplo de um documento PDRL.

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
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar uma política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Defina os atributos da política.
1. Criar uma entrada de política.
1. Registre a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se AEM Forms forem implantados em JBoss)
* jaxb-api.jar (se os AEM Forms forem implantados em JBoss)
* jaxb-impl.jar (se os AEM Forms forem implantados em JBoss)
* jaxb-libs.jar (se os AEM Forms forem implantados em JBoss)
* jaxb-xjc.jar (se os AEM Forms forem implantados em JBoss)
* relaxngDatatype.jar (se os AEM Forms forem implantados em JBoss)
* xsdlib.jar (se os AEM Forms forem implantados em JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (use um arquivo JAR diferente se os AEM Forms não estiverem implantados em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, crie um objeto cliente de serviço de Segurança do Documento.

**Definir os atributos da política**

Para criar uma política, defina os atributos da política. Um atributo obrigatório é o nome da política. Os nomes de políticas devem ser exclusivos para cada conjunto de políticas. Um conjunto de políticas é simplesmente uma coleção de políticas. Pode haver duas políticas com o mesmo nome se as políticas pertencerem a conjuntos de políticas separados. No entanto, duas políticas em um único conjunto de políticas não podem ter o mesmo nome de política.

Outro atributo útil a ser definido é o período de validade. Um período de validade é o período durante o qual um documento protegido por política é acessível aos recipient autorizados. Se você não definir esse atributo, a política sempre será válida.

Um período de validade pode ser definido como uma destas opções:

* Um número definido de dias em que o documento é acessível a partir do momento em que o documento é publicado
* Uma data final após a qual o documento não está acessível
* Um intervalo de datas específico para o qual o documento está acessível
* Sempre válido

Você pode especificar apenas uma data de start, o que resulta na política válida após a data de start. Se você especificar apenas uma data de término, a política será válida até a data de término. No entanto, uma exceção é lançada se uma data de start e uma data de término não estiverem definidas.

Ao definir atributos que pertencem a uma política, também é possível definir configurações de criptografia. Essas configurações de criptografia ocorrem quando a política é aplicada a um documento. Você pode especificar os seguintes valores de criptografia:

* **AES256**: Representa o algoritmo de criptografia AES com uma chave de 256 bits.
* **AES128**: Representa o algoritmo de criptografia AES com uma chave de 128 bits.
* **NoEncryption:** Não representa criptografia.

Ao especificar a `NoEncryption` opção, não é possível definir a `PlaintextMetadata` opção como `false`. Se você tentar fazer isso, uma exceção é lançada.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte a descrição da `Policy` interface na Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Criar uma entrada de política**

Uma entrada de política anexa os principais, que são grupos e usuários, e permissões a uma política. Uma política deve ter pelo menos uma entrada na política. Considere, por exemplo, que você executa estas tarefas:

* Crie e registre uma entrada de política que permita que um grupo apenas visualização um documento enquanto estiver on-line e proíba que recipient o copiem.
* Anexe a entrada de política à política.
* Proteja um documento com a política usando o Acrobat.

Essas ações resultam em recipient que só podem visualização o documento on-line e não podem copiá-lo. O documento permanece protegido até que a segurança seja removida dele.

**Registrar a política**

Uma nova política deve ser registrada antes de poder ser usada. Depois de registrar uma política, você pode usá-la para proteger documentos.

### Criar uma política usando a API Java {#create-a-policy-using-the-java-api}

Crie uma política usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Defina os atributos da política.

   * Crie um `Policy` objeto chamando o `InfomodelObjectFactory` método estático do `createPolicy` objeto. Esse método retorna um `Policy` objeto.
   * Defina o atributo name da política chamando o método do `Policy` `setName` objeto e transmitindo um valor de string que especifica o nome da política.
   * Defina a descrição da política chamando o método do `Policy` `setDescription` objeto e transmitindo um valor de string que especifica a descrição da política.
   * Defina o conjunto de políticas ao qual a nova política pertence chamando o método do `Policy` `setPolicySetName` objeto e transmitindo um valor de string que especifica o nome do conjunto de políticas. (Você pode especificar `null` para esse valor de parâmetro que resulta na adição da política ao conjunto de políticas *Minhas políticas* .)
   * Crie o período de validade da política chamando o `InfomodelObjectFactory` método estático do `createValidityPeriod` objeto. Esse método retorna um `ValidityPeriod` objeto.
   * Defina o número de dias para os quais um documento protegido por política pode ser acessado chamando o método do `ValidityPeriod` `setRelativeExpirationDays` objeto e transmitindo um valor inteiro que especifica o número de dias.
   * Defina o período de validade da política chamando o método do `Policy` objeto `setValidityPeriod` e transmitindo o `ValidityPeriod` objeto.

1. Criar uma entrada de política.

   * Crie uma entrada de política chamando o `InfomodelObjectFactory` método estático do `createPolicyEntry` objeto. Esse método retorna um `PolicyEntry` objeto.
   * Especifique as permissões da política chamando o `InfomodelObjectFactory` método estático do `createPermission` objeto. Passe um membro de dados estáticos que pertence à `Permission` interface que representa a permissão. Esse método retorna um `Permission` objeto. Por exemplo, para adicionar a permissão que permite aos usuários copiar dados de um documento PDF protegido por política, passe `Permission.COPY`. (Repita essa etapa para cada permissão a ser adicionada).
   * Adicione a permissão à entrada de política chamando o método do `PolicyEntry` objeto e transmitindo o `addPermission` `Permission` objeto. (Repita essa etapa para cada `Permission` objeto criado).
   * Crie o principal da política chamando o `InfomodelObjectFactory` método estático do `createSpecialPrincipal` objeto. Passe um membro de dados que pertence ao `InfomodelObjectFactory` objeto que representa o principal. Esse método retorna um `Principal` objeto. Por exemplo, para adicionar o editor do documento como principal, passe `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Adicione o principal à entrada de política chamando o `PolicyEntry` método do objeto e transmitindo o `setPrincipal``Principal` objeto.
   * Adicione a entrada de política à política chamando o método do `Policy` objeto `addPolicyEntry` e transmitindo o `PolicyEntry` objeto.

1. Registre a política.

   * Crie um `PolicyManager` objeto chamando o `DocumentSecurityClient` método do `getPolicyManager` objeto.
   * Registre a política chamando o método do `PolicyManager` objeto `registerPolicy` e transmitindo os seguintes valores:

      * O `Policy` objeto que representa a política a ser registrada.
   * Um valor de string que representa o conjunto de políticas ao qual a política pertence.

   Se você usar uma conta de administrador de formulários AEM nas configurações de conexão para criar o `DocumentSecurityClient` objeto, especifique o nome do conjunto de políticas ao chamar o `registerPolicy` método. Se você passar um `null` valor para o conjunto de políticas, a política será criada no conjunto de políticas de administradores *Minhas políticas* .

   Se você usar um usuário do Documento Security nas configurações de conexão, poderá invocar o `registerPolicy` método sobrecarregado que aceita apenas a política. Ou seja, você não precisa especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas políticas*. Se você não quiser adicionar a nova política a esse conjunto de políticas, especifique um nome para o conjunto de políticas ao chamar o `registerPolicy` método.

   >[!NOTE]
   >
   >Ao criar uma política, consulte um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, uma exceção será lançada.

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte:

* &quot;Start rápido (modo SOAP): Criar uma política usando a API Java&quot;

### Criar uma política usando a API de serviço da Web {#create-a-policy-using-the-web-service-api}

Crie uma política usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina os atributos da política.

   * Crie um `PolicySpec` objeto usando seu construtor.
   * Defina o nome da política atribuindo um valor de string ao membro de `PolicySpec` dados do `name` objeto.
   * Defina a descrição da política atribuindo um valor de string ao membro de `PolicySpec` dados do `description` objeto.
   * Defina o conjunto de políticas ao qual a política pertencerá atribuindo um valor de string ao membro de `PolicySpec` dados do `policySetName` objeto. É necessário especificar um nome de conjunto de políticas existente. (Você pode especificar `null` para esse valor de parâmetro que resulta na adição da política às *Minhas políticas*.)
   * Defina o período de empréstimo offline da política atribuindo um valor inteiro ao membro de `PolicySpec` dados do `offlineLeasePeriod` objeto.
   * Defina o membro de `PolicySpec` dados do `policyXml` objeto com um valor de string que representa dados XML PDF. Para executar essa tarefa, crie um objeto .NET `StreamReader` usando seu construtor. Passe o local de um arquivo XML PDRL que representa a política para o `StreamReader` construtor. Em seguida, chame o método do `StreamReader` objeto `ReadLine` e atribua o valor de retorno a uma variável de string. Iterar pelo `StreamReader` objeto até que o `ReadLine` método retorne nulo. Atribua a variável de string ao membro de `PolicySpec` dados do `policyXml` objeto.

1. Criar uma entrada de política.

   Não é necessário criar uma entrada de política ao criar uma política usando a API de serviço da Web do Documento Security. A entrada de política é definida no documento PDRL.

1. Registre a política.

   Registre a política chamando o método do `DocumentSecurityServiceClient` objeto `registerPolicy` e transmitindo os seguintes valores:

   * O `PolicySpec` objeto que representa a política a ser registrada.
   * Um valor de string que representa o conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta na adição da política ao conjunto de políticas *MyPolicy* .

   Se você usar uma conta de administrador de formulários AEM nas configurações de conexão para criar o `DocumentSecurityClient` objeto, especifique o nome do conjunto de políticas ao chamar o `registerPolicy` método.

   Se você usar um usuário do Documento SecurityDocument Security nas configurações de conexão, poderá invocar o `registerPolicy` método sobrecarregado que aceita somente a política. Ou seja, você não precisa especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas políticas*. Se você não quiser adicionar a nova política a esse conjunto de políticas, especifique um nome para o conjunto de políticas ao chamar o `registerPolicy` método.

   >[!NOTE]
   >
   >Ao criar uma política e especificar um conjunto de políticas, especifique um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, uma exceção será lançada.

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Criar uma política usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Criar uma política usando a API de serviço da Web&quot;

## Modificando Políticas {#modifying-policies}

É possível modificar uma política existente usando a API Java de segurança do Documento ou a API de serviço da Web. Para fazer alterações em uma política existente, recupere-a, modifique-a e atualize a política no servidor. Por exemplo, suponha que você recupere uma política existente e estenda seu período de validade. Antes que a alteração entre em vigor, é necessário atualizar a política.

Você pode modificar uma política quando os requisitos de negócios mudam e a política não reflete mais esses requisitos. Em vez de criar uma nova política, basta atualizar uma política existente.

Para modificar atributos de política usando um serviço da Web (por exemplo, usando classes proxy Java que foram criadas com JAX-WS), é necessário garantir que a política seja registrada com o serviço de Segurança do Documento. Em seguida, é possível fazer referência à política existente usando o `PolicySpec.getPolicyXml` método e modificar os atributos da política usando os métodos aplicáveis. Por exemplo, você pode modificar o período de empréstimo offline chamando o `PolicySpec.setOfflineLeasePeriod` método.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para modificar uma política existente, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recuperar uma política existente.
1. Alterar atributos de políticas.
1. Atualize a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `RightsManagementClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `RightsManagementServiceService` objeto.

**Recuperar uma política existente**

É necessário recuperar uma política existente para modificá-la. Para recuperar uma política, especifique o nome da política e o conjunto de políticas ao qual ela pertence. Se você especificar um `null` valor para o nome do conjunto de políticas, a política será recuperada do conjunto de políticas *Minhas políticas* .

**Definir os atributos da política**

Para modificar uma política, modifique o valor dos atributos de política. O único atributo de política que não pode ser alterado é o atributo name. Por exemplo, para alterar o período de empréstimo offline da política, é possível modificar o valor do atributo do período de empréstimo offline da política.

Ao modificar o período de empréstimo offline de uma política usando um serviço da Web, o `offlineLeasePeriod` campo na `PolicySpec` interface é ignorado. Para atualizar o período de empréstimo offline, modifique o `OfflineLeasePeriod` elemento no documento XML PDRL. Em seguida, consulte o documento XML PDF atualizado usando o membro de `PolicySpec` dados da `policyXML` interface.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte a descrição da `Policy` interface na Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Atualizar a política**

Antes que as alterações feitas em uma política entrem em vigor, é necessário atualizar a política com o serviço de Segurança do Documento. As alterações nas políticas que protegem documentos serão atualizadas na próxima vez que o documento protegido por política for sincronizado com o serviço de Segurança do Documento.

### Modificar políticas existentes usando a API Java {#modify-existing-policies-using-the-java-api}

Modifique uma política existente usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar uma política existente.

   * Crie um `PolicyManager` objeto chamando o `RightsManagementClient` método do `getPolicyManager` objeto.
   * Crie um `Policy` objeto que represente a política a ser atualizada chamando o método do `PolicyManager` objeto `getPolicy` e transmitindo os seguintes valores&quot;

      * Um valor de string que representa o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` esses resultados no conjunto de `MyPolicies` políticas que está sendo usado.
      * Um valor de string que representa o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às suas necessidades de negócios. Por exemplo, para alterar o período de empréstimo offline da política, chame o método do `Policy` objeto `setOfflineLeasePeriod` .

1. Atualize a política.

   Atualize a política chamando o método do `PolicyManager` objeto `updatePolicy` . Passe o `Policy` objeto que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o Start rápido (modo SOAP): Modificação de uma política usando a seção da API Java.

### Modificar políticas existentes usando a API de serviço da Web {#modify-existing-policies-using-the-web-service-api}

Modifique uma política existente usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar uma política existente.

   Crie um `PolicySpec` objeto que represente a política a ser modificada chamando o método do `RightsManagementServiceClient` objeto `getPolicy` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` esses resultados no conjunto de `MyPolicies` políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às suas necessidades de negócios.

1. Atualize a política.

   Atualize a política chamando o método do `RightsManagementServiceClient` objeto `updatePolicyFromSDK` e transmitindo o `PolicySpec` objeto que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Modificando uma política usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Modificando uma política usando a API de serviço da Web&quot;

## Excluindo Políticas {#deleting-policies}

Você pode excluir uma política existente usando a API Java de segurança do Documento ou a API de serviço da Web. Depois que uma política é excluída, ela não pode mais ser usada para proteger documentos. No entanto, documentos protegidos por política que estão usando a política ainda são protegidos. Você pode excluir uma política quando uma nova estiver disponível.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para excluir uma política existente, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Documento Security Client.
1. Exclua a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `RightsManagementClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `RightsManagementServiceService` objeto.

**Excluir a política**

Para excluir uma política, especifique a política a ser excluída e o conjunto de políticas ao qual a política pertence. O usuário cujas configurações são usadas para chamar AEM Forms deve ter permissão para excluir a política; caso contrário, ocorrerá uma exceção. Da mesma forma, se você tentar excluir uma política que não existe, ocorrerá uma exceção.

### Excluir políticas usando a API Java {#delete-policies-using-the-java-api}

Exclua uma política usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Exclua a política.

   * Crie um `PolicyManager` objeto chamando o `RightsManagementClient` método do `getPolicyManager` objeto.
   * Exclua a política chamando o método do `PolicyManager` objeto `deletePolicy` e transmitindo os seguintes valores:

      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` esses resultados no conjunto de `MyPolicies` políticas que está sendo usado.
      * Um valor de string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Excluindo uma política usando a API Java&quot;

### Excluir políticas usando a API de serviço da Web {#delete-policies-using-the-web-service-api}

Exclua uma política usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Exclua a política.

   Exclua uma política chamando o método do `RightsManagementServiceClient` objeto `deletePolicy` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` esses resultados no conjunto de `MyPolicies` políticas que está sendo usado.
   * Um valor de string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Excluindo uma política usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Excluindo uma política usando a API de serviço da Web&quot;

## Aplicar políticas a Documentos PDF {#applying-policies-to-pdf-documents}

É possível aplicar uma política a um documento PDF para proteger o documento. Ao aplicar uma política a um documento PDF, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se o documento já estiver protegido por uma política.

Enquanto o documento estiver aberto, você também pode restringir o acesso aos recursos do Acrobat e do Adobe Reader, incluindo a capacidade de imprimir e copiar texto, fazer alterações e adicionar assinaturas e comentários a um documento. Além disso, você pode revogar um documento PDF protegido por política quando não quiser mais que os usuários acessem o documento.

Você pode monitorar o uso de um documento protegido por política depois de distribuí-lo. Ou seja, vocês podem ver como o documento está sendo usado e quem está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para aplicar uma política a um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recupere um documento PDF ao qual uma política é aplicada.
1. Aplique uma política existente ao documento PDF.
1. Salve o documento PDF protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do Cliente do Documento Security**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, crie um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `DocumentSecurityClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `DocumentSecurityServiceService` objeto.

**Recuperar um documento PDF**

É possível recuperar um documento PDF para aplicar uma política. Depois de aplicar uma política ao documento PDF, os usuários são restringidos ao usar o documento. Por exemplo, se a política não permitir que o documento seja aberto offline, os usuários devem estar online para abrir o documento.

**Aplicar uma política existente ao documento PDF**

Para aplicar uma política a um documento PDF, consulte uma política existente e especifique a que conjunto de políticas a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salvar o documento PDF**

Depois que o serviço de Segurança do Documento aplicar uma política a um documento PDF, é possível salvar o documento PDF protegido por política como um arquivo PDF.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogação do acesso a Documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar uma política a um documento PDF usando a API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplique uma política a um documento PDF usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Aplique uma política existente ao documento PDF.

   * Crie um `DocumentManager` objeto chamando o `RightsManagementClient` método do `getDocumentManager` objeto.
   * Aplique uma política ao documento PDF chamando o método do `DocumentManager` objeto `protectDocument` e transmitindo os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém o documento PDF ao qual a política é aplicada.
      * Um valor de string que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta no conjunto de `MyPolicies` políticas que está sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser nulo).
      * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se esse parâmetro for nulo, o valor de parâmetro anterior deve ser `null`).
      * Uma `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e não é usado para documentos PDF. Para proteger um documento PDF, especifique `null`.

      O `protectDocument` método retorna um `RMSecureDocumentResult` objeto que contém o documento PDF protegido por política.


1. Salve o documento PDF.

   * Chame o `RMSecureDocumentResult` `getProtectedDoc` método do objeto para obter o documento PDF protegido por política. Esse método retorna um `com.adobe.idp.Document` objeto.
   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é PDF.
   * Chame o `com.adobe.idp.Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `getProtectedDoc` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo EJB): Aplicar uma política a um documento PDF usando a API Java&quot;
* &quot;Start rápido (modo SOAP): Aplicar uma política a um documento PDF usando a API Java&quot;

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar uma política a um documento PDF usando a API de serviço da Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplique uma política a um documento PDF usando a Documento Security API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço de Formulários (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento PDF.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF ao qual uma política é aplicada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do `Length` objeto.
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Aplique uma política existente ao documento PDF.

   Aplique uma política ao documento PDF chamando o método do `RightsManagementServiceClient` objeto `protectDocument` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF ao qual a política é aplicada.
   * Um valor de string que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta no conjunto de `MyPolicies` políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser `null`).
   * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor de parâmetro anterior deve ser `null`).
   * Um `RMLocale` valor que especifica o valor de localidade (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída de string usado para armazenar o valor do identificador de política.
   * Um parâmetro de saída de string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída de string usado para armazenar o tipo mime (por exemplo, `application/pdf`).

   O `protectDocument` método retorna um `BLOB` objeto que contém o documento PDF protegido por política.

1. Salve o documento PDF.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `protectDocument` método. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Aplicar uma política a um documento PDF usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Aplicar uma política a um documento PDF usando a API de serviço da Web&quot;

## Remoção de políticas de Documentos PDF {#removing-policies-from-pdf-documents}

Você pode remover uma política de um documento protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se quiser atualizar um documento protegido por política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, é mais eficiente trocar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para remover uma política de um documento PDF protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Documento Security Client.
1. Recupere um documento PDF protegido por política.
1. Remova a política do documento PDF.
1. Salve o documento PDF não protegido.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, crie um objeto cliente de serviço de Segurança do Documento.

**Recuperar um documento PDF protegido por política**

É possível recuperar um documento PDF protegido por política para remover uma política. Se você tentar remover uma política de um documento PDF que não esteja protegido por uma política, causará uma exceção.

**Remover a política do documento PDF**

É possível remover uma política de um documento PDF protegido por política, desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deverá conter a `SWITCH_POLICY` permissão para remover uma política de um documento PDF. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salvar o documento PDF não protegido**

Depois que o serviço de Segurança do Documento remover uma política de um documento PDF, é possível salvar o documento PDF não protegido como um arquivo PDF.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar políticas a Documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Remover uma política de um documento PDF usando a API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Remova uma política de um documento PDF protegido por política usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF protegido por política.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova a política do documento PDF.

   * Crie um `DocumentManager` objeto chamando o `DocumentSecurityClient` método do `getDocumentManager` objeto.
   * Remova uma política do documento PDF chamando o método do `DocumentManager` objeto `removeSecurity` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF protegido por política. Esse método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não protegido.

1. Salve o documento PDF não protegido.

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é PDF.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `removeSecurity` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Remover uma política de um documento PDF usando a API Java&quot;

### Remover uma política usando a API de serviço da Web {#remove-a-policy-using-the-web-service-api}

Remova uma política de um documento PDF protegido por política usando a Documento Security API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento PDF protegido por política.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF protegido por política do qual a política é removida.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Remova a política do documento PDF.

   Remova a política do documento PDF chamando o método do `DocumentSecurityServiceClient` objeto `removePolicySecurity` e transmitindo o `BLOB` objeto que contém o documento PDF protegido por política. Esse método retorna um `BLOB` objeto que contém um documento PDF não protegido.

1. Salve o documento PDF não protegido.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `removePolicySecurity` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Remover uma política de um documento PDF usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Remover uma política de um documento PDF usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revogação do acesso a Documentos {#revoking-access-to-documents}

É possível revogar o acesso a um documento PDF protegido por política, resultando em todas as cópias do documento inacessíveis aos usuários. Quando um usuário tenta abrir um documento PDF revogado, ele é redirecionado para um URL especificado onde um documento revisado pode ser visualizado. O URL para o qual o usuário é redirecionado deve ser especificado de forma programática. Quando você revoga o acesso a um documento, a alteração entrará em vigor na próxima vez que o usuário sincronizar com o serviço de Segurança do Documento, abrindo o documento protegido por política on-line.

A capacidade de revogar o acesso a um documento oferece segurança adicional. Por exemplo, suponha que uma versão mais recente de um documento esteja disponível e você não quer mais que ninguém visualize a versão desatualizada. Nessa situação, o acesso ao documento mais antigo pode ser revogado, e ninguém pode visualização o documento a menos que o acesso seja restabelecido.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para revogar um documento protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recupere um documento PDF protegido por política.
1. Revogar o documento protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento.

**Recuperar um documento PDF protegido por política**

É necessário recuperar um documento PDF protegido por política para revogá-lo. Não é possível revogar um documento que já tenha sido revogado ou que não seja um documento protegido por política.

Se você souber o valor do identificador de licença do documento protegido por política, não será necessário recuperar o documento PDF protegido por política. No entanto, na maioria dos casos, será necessário recuperar o documento PDF para obter o valor do identificador de licença.

**Revogar o documento protegido por política**

Para revogar um documento protegido por política, especifique o identificador de licença do documento protegido por política. Além disso, você pode especificar o URL de um documento que o usuário pode visualização ao tentar abrir o documento revogado. Ou seja, suponha que um documento desatualizado seja revogado. Quando um usuário tentar abrir o documento revogado, ele verá um documento atualizado em vez do documento revogado.

>[!NOTE]
>
>Se você tentar revogar um documento que já foi revogado, uma exceção será lançada.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar políticas a Documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Reinstalando o acesso a Documentos Revogados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revogar o acesso a documentos usando a API Java {#revoke-access-to-documents-using-the-java-api}

Revogar o acesso a um documento PDF protegido por política usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Documento Security Client

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento PDF protegido por política

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Revogar o documento protegido por política

   * Crie um `DocumentManager` objeto chamando o `DocumentSecurityClient` método do `getDocumentManager` objeto.
   * Recupere o valor do identificador de licença do documento protegido por política chamando o método do `DocumentManager` objeto `getLicenseId` . Passe o `com.adobe.idp.Document` objeto que representa o documento protegido por política. Esse método retorna um valor de string que representa o valor do identificador de licença.
   * Crie um `LicenseManager` objeto chamando o `DocumentSecurityClient` método do `getLicenseManager` objeto.
   * Revogue o documento protegido por política chamando o método do `LicenseManager` objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do método do `DocumentManager` `getLicenseId` objeto).
      * Um membro de dados estáticos da `License` interface que especifica o motivo para revogar o documento. For example, you can specify `License.DOCUMENT_REVISED`.
      * Um `java.net.URL` valor que especifica o local onde um documento revisado está localizado. Se você não quiser redirecionar um usuário para outro URL, é possível passá-lo `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Revogar um documento usando a API Java&quot;

### Revogar o acesso a documentos usando a API de serviço da Web {#revoke-access-to-documents-using-the-web-service-api}

Revogar o acesso a um documento PDF protegido por política usando a Documento Security API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Criar um objeto de API do Documento Security Client

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento PDF protegido por política

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF protegido por política que é revogado.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido por política a ser revogado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Revogar o documento protegido por política

   * Recupere o valor do identificador de licença do documento protegido por política chamando o método do `DocumentSecurityServiceClient` objeto `getLicenseID` e transmitindo o `BLOB` objeto que representa o documento protegido por política. Esse método retorna um valor de string que representa o identificador de licença.
   * Revogue o documento protegido por política chamando o método do `DocumentSecurityServiceClient` objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do método do `DocumentSecurityServiceService` `getLicenseId` objeto).
      * Um membro de dados estáticos da `Reason` enumeração que especifica o motivo para revogar o documento. For example, you can specify `Reason.DOCUMENT_REVISED`.
      * Um `string` valor que especifica o local do URL para onde um documento revisado está localizado. Se você não quiser redirecionar um usuário para outro URL, é possível passá-lo `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Revogar um documento usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Revogar um documento usando a API de serviço da Web&quot;

**Consulte também:**

[Remover Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Reinstalando o acesso a Documentos Revogados {#reinstating-access-to-revoked-documents}

Você pode reinstalar o acesso a um documento PDF revogado, resultando em todas as cópias do documento revogado serem acessíveis aos usuários. Quando um usuário abre um documento reinstalado que foi revogado, ele pode visualização o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para reinstalar o acesso a um documento PDF revogado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recupere o identificador de licença do documento PDF revogado.
1. Reinstale o acesso ao documento PDF revogado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `DocumentSecurityClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `DocumentSecurityServiceService` objeto.

**Recuperar o identificador de licença do documento PDF revogado**

É necessário recuperar o identificador de licença do documento PDF revogado para reinstalar um documento PDF revogado. Depois de obter o valor do identificador de licença, você pode reinstalar um documento revogado. Se tentar reinstalar um documento que não seja revogado, ocorrerá uma exceção.

**Reinstale o acesso ao documento PDF revogado**

Para restabelecer o acesso a um documento PDF revogado, você deve especificar o identificador de licença do documento revogado. Se você tentar restabelecer o acesso a um documento PDF que não seja revogado, causará uma exceção.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar políticas a Documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revogação do acesso a Documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Reinstale o acesso a documentos revogados usando a API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Instale novamente o acesso a um documento revogado usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o identificador de licença do documento PDF revogado.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF revogado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.
   * Crie um `DocumentManager` objeto chamando o `DocumentSecurityClient` método do `getDocumentManager` objeto.
   * Recupere o valor do identificador de licença do documento revogado chamando o método do `DocumentManager` objeto `getLicenseId` e transmitindo o `com.adobe.idp.Document` objeto que representa o documento revogado. Esse método retorna um valor de string que representa o identificador de licença.

1. Reinstale o acesso ao documento PDF revogado.

   * Crie um `LicenseManager` objeto chamando o `DocumentSecurityClient` método do `getLicenseManager` objeto.
   * Reinstale o acesso ao documento PDF revogado chamando o método do `LicenseManager` objeto `unrevokeLicense` e transmitindo o valor do identificador de licença do documento revogado.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Reinstalando o acesso a um documento revogado usando a API de serviço da Web&quot;

### Reinstale o acesso a documentos revogados usando a API de serviço da Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Instale novamente o acesso a um documento revogado usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere o identificador de licença do documento PDF revogado.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF revogado para o qual o acesso é restabelecido.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF revogado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Reinstale o acesso ao documento PDF revogado.

   * Recupere o valor do identificador de licença do documento revogado chamando o método do `DocumentSecurityServiceClient` objeto `getLicenseID` e transmitindo o `BLOB` objeto que representa o documento revogado. Esse método retorna um valor de string que representa o identificador de licença.
   * Reinstale o acesso ao documento PDF revogado chamando o método do `DocumentSecurityServiceClient` objeto `unrevokeLicense` e transmitindo um valor de string que especifica o valor do identificador de licença do documento PDF revogado (passe o valor de retorno do método do `DocumentSecurityServiceClient` objeto `getLicenseId` ).

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Reinstalando o acesso a um documento revogado usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Reinstalando o acesso a um documento revogado usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Como inspecionar Documentos PDF protegidos por política {#inspecting-policy-protected-pdf-documents}

Você pode usar a API do serviço de segurança do Documento (Java e serviço da Web) para inspecionar documentos PDF protegidos por política. Inspecionar documentos PDF protegidos por política retorna informações sobre o documento PDF protegido por política. Você pode, por exemplo, determinar a política usada para proteger o documento e a data em que o documento foi protegido.

Não é possível executar essa tarefa se sua versão do LiveCycle for 8.x ou uma versão anterior. O suporte para inspecionar documentos protegidos por política é adicionado em AEM Forms. Se você tentar inspecionar um documento protegido por política usando o LiveCycle 8.x (ou anterior), uma exceção será lançada.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para inspecionar um documento PDF protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recupere um documento protegido por política para inspecionar.
1. Obtenha informações sobre o documento protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, crie um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `RightsManagementClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `RightsManagementServiceService` objeto.

**Recuperar um documento protegido por política para inspecionar**

Para inspecionar um documento protegido por política, recupere-o. Se você tentar inspecionar um documento que não esteja protegido por uma política ou que seja revogado, uma exceção será lançada.

**Inspecione o documento**

Depois de recuperar um documento protegido por política, você pode inspecioná-lo.

**Obter informações sobre o documento protegido por política**

Depois de inspecionar um documento PDF protegido por política, você pode obter informações sobre ele. Por exemplo, você pode determinar a política usada para proteger o documento.

Se você proteger um documento com uma política que pertence a Minhas políticas e, em seguida, chamar `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, nulo será retornado.

Se o documento estiver protegido usando uma política contida em um conjunto de políticas (diferente de Minhas políticas), `RMInspectResult.getPolicysetName` `RMInspectResult.getPolicysetId` retorne strings válidas.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspecione Documentos PDF protegidos por política usando a API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspecione um documento PDF protegido por política usando a API do Documento Security Service (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como o adobe-rights management-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento protegido por política para inspecionar.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF protegido por política usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Inspecione o documento.

   * Crie um `DocumentManager` objeto chamando o `RightsManagementClient` método do `getDocumentManager` objeto.
   * Inspecione o documento protegido por política chamando o método do `LicenseManager` objeto `inspectDocument` . Passe o `com.adobe.idp.Document` objeto que contém o documento PDF protegido por política. Esse método retorna um `RMInspectResult` objeto que contém informações sobre o documento protegido por política.

1. Obtenha informações sobre o documento protegido por política.

   Para obter informações sobre o documento protegido por política, chame o método apropriado que pertence ao `RMInspectResult` objeto. Por exemplo, para recuperar o nome da política, chame o método do `RMInspectResult` objeto `getPolicyName` .

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Inspecionar documentos PDF protegidos por política usando a API Java&quot;

### Inspecione Documentos PDF protegidos por política usando a API de serviço da Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspecione um documento PDF protegido por política usando a Documento Security Service API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento protegido por política para inspecionar.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF a ser inspecionado.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Inspecione o documento.

   Inspecione o documento protegido por política chamando o método do `RightsManagementServiceClient` objeto `inspectDocument` . Passe o `BLOB` objeto que contém o documento PDF protegido por política. Esse método retorna um `RMInspectResult` objeto que contém informações sobre o documento protegido por política.

1. Obtenha informações sobre o documento protegido por política.

   Para obter informações sobre o documento protegido por política, obtenha o valor do campo apropriado que pertence ao `RMInspectResult` objeto. Por exemplo, para recuperar o nome da política, obtenha o valor do campo do `RMInspectResult` objeto `policyName` .

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Inspecionar documentos PDF protegidos por política usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Inspecionar documentos PDF protegidos por política usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de marcas d&#39;água {#creating-watermarks}

As marcas d&#39;água ajudam a garantir a segurança de um documento, identificando exclusivamente o documento e controlando a violação dos direitos autorais. Por exemplo, você pode criar e colocar uma marca d&#39;água que informe Confidencial em todas as páginas de um documento. Após a criação de uma marca d&#39;água, é possível incluí-la como parte de uma política. Ou seja, você pode definir o atributo de marca d&#39;água da política com a marca d&#39;água recém-criada. Depois que uma política que contém uma marca d&#39;água é aplicada a um documento, a marca d&#39;água aparece no documento protegido por política.

>[!NOTE]
>
>Somente os usuários com privilégios administrativos do Documento Security podem criar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança do Documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para criar uma marca d&#39;água, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Defina os atributos de marcas d&#39;água.
1. Registre a marca d&#39;água no serviço de Segurança do Documento.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `RightsManagementClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `RightsManagementServiceService` objeto.

**Definir os atributos de marcas d&#39;água**

Para criar uma nova marca d&#39;água, é necessário definir atributos de marca d&#39;água. O atributo name deve ser sempre definido. Além do atributo name, você deve definir pelo menos um dos seguintes atributos:

* Texto personalizado
* DateIncluded
* UserIdIncluded
* UserNameIncluded

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
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>Especifica se a identificação do usuário que abre o documento faz parte da marca d'água.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>Especifica se a data atual faz parte da marca d'água.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>Se esse valor for verdadeiro, o valor do texto personalizado deverá ser especificado usando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>Especifica a opacidade da marca d'água. O valor padrão é 0,5 se não for especificado.</p></td>
   <td><p>Um valor entre 0,0 e 1,0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>Especifica a rotação da marca d'água. O valor padrão é 0 graus.</p></td>
   <td><p>Um valor entre 0 e 359.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>Se esse valor for especificado, então <code>WaterBackCmd:IS_SIZE_ENABLED</code> deverá estar presente e o valor deverá ser verdadeiro. Se esse atributo não for especificado, o comportamento padrão se ajusta à página.</p></td>
   <td><p>Um valor superior a 0.0 e inferior ou igual a 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Especifica o alinhamento horizontal da marca d'água. O valor padrão é central.</p></td>
   <td><p>esquerda, centro ou direita</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>Especifica o alinhamento vertical da marca d'água. O valor padrão é central.</p></td>
   <td><p>superior, central ou inferior</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>Especifica se a marca d'água é um plano de fundo. O valor padrão é false.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>True se uma escala personalizada for especificada. Se esse valor for verdadeiro, a SCALE também deverá ser especificada. Se esse valor for falso, o padrão se ajusta à página.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica o texto personalizado para uma marca d'água. Se esse valor estiver presente, então também <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> deverá estar presente e definido como true.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
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

Uma nova marca d&#39;água deve ser registrada no serviço de segurança do Documento antes de poder ser usada. Depois de registrar uma marca d&#39;água, você pode usá-la nas políticas.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar políticas a Documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Criar marcas d&#39;água usando a API Java {#create-watermarks-using-the-java-api}

Crie uma marca d&#39;água usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como o `adobe-rightsmanagement-client.jar`, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir os atributos de marca d&#39;água

   * Crie um `Watermark` objeto chamando o `InfomodelObjectFactory` método estático do `createWatermark` objeto. Esse método retorna um `Watermark` objeto.
   * Defina o atributo name da marca d&#39;água chamando o método do `Watermark` `setName` objeto e transmitindo um valor de string que especifica o nome da política.
   * Defina o atributo de plano de fundo da marca d&#39;água chamando o `Watermark` método do `setBackground` objeto e transmitindo `true`. Ao definir esse atributo, a marca d&#39;água aparece no plano de fundo do documento.
   * Defina o atributo de texto personalizado da marca d&#39;água chamando o método do `Watermark` objeto `setCustomText` e transmitindo um valor de string que representa o texto da marca d&#39;água.
   * Defina o atributo de opacidade da marca d&#39;água chamando o método do `Watermark` objeto `setOpacity` e transmitindo um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

1. Registre a marca d&#39;água.

   * Crie um `WatermarkManager` objeto chamando o `RightsManagementClient` método do `getWatermarkManager` objeto. Esse método retorna um `WatermarkManager` objeto.
   * Registre a marca d&#39;água invocando o `WatermarkManager` método do `registerWatermark` objeto e transmitindo o `Watermark` objeto que representa a marca d&#39;água para registro. Esse método retorna um valor de string que representa o valor de identificação da marca d&#39;água.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (modo SOAP): Criação de uma marca d&#39;água usando a API Java&quot;

### Criar marcas d&#39;água usando a API de serviço da Web {#create-watermarks-using-the-web-service-api}

Crie uma marca d&#39;água usando a API de segurança do Documento (serviço da Web):

1. Crie um objeto da API do Documento Security Client.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina os atributos de marca d&#39;água.

   * Crie um `WatermarkSpec` objeto chamando o `WatermarkSpec` construtor.
   * Defina o nome da marca d&#39;água atribuindo um valor de string ao membro de `WatermarkSpec` dados do `name` objeto.
   * Defina o `id` atributo da marca d&#39;água atribuindo um valor de string ao membro de `WatermarkSpec` dados do `id` objeto.
   * Para que cada propriedade de marca d&#39;água seja definida, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto separado.
   * Defina o valor-chave atribuindo um valor ao membro de `MyMapOf_xsd_string_To_xsd_anyType_Item` dados do `key` objeto (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao membro de `MyMapOf_xsd_string_To_xsd_anyType_Item` dados do `value` objeto (por exemplo, `.25`).
   * Create a `MyArrayOf_xsd_anyType` object. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, chame o `MyArrayOf_xsd_anyType` método do `Add` objeto. Passe o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua o `MyArrayOf_xsd_anyType` objeto ao membro de `WatermarkSpec` dados do `values` objeto.

1. Registre a marca d&#39;água.

   Registre a marca d&#39;água invocando o `RightsManagementServiceClient` método do `registerWatermark` objeto e transmitindo o `WatermarkSpec` objeto que representa a marca d&#39;água para registro.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Criar uma marca d&#39;água usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Criar uma marca d&#39;água usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificação de Marcas D&#39;Água {#modifying-watermarks}

É possível modificar uma marca d&#39;água existente usando a API Java de segurança do Documento ou a API de serviço da Web. Para fazer alterações em uma marca d&#39;água existente, você a recupera, modifica seus atributos e a atualiza no servidor. Por exemplo, suponha que você recupere uma marca d&#39;água e modifique seu atributo de opacidade. Antes que a alteração entre em vigor, é necessário atualizar a marca d&#39;água.

Quando você modifica uma marca d&#39;água, a alteração afeta documentos futuros que têm a marca d&#39;água aplicada a eles. Ou seja, documentos PDF existentes que contêm a marca d&#39;água não são afetados.

>[!NOTE]
>
>Somente os usuários com privilégios administrativos do Documento Security podem modificar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança do Documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-9}

Para modificar uma marca d&#39;água, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recupere a marca d&#39;água para modificá-la.
1. Defina os atributos de marcas d&#39;água.
1. Atualize a marca d&#39;água.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento. Se você estiver usando a API Java, crie um `DocumentSecurityClient` objeto. Se você estiver usando a API de serviço da Web do Documento Security, crie um `DocumentSecurityServiceService` objeto.

**Recuperar a marca d&#39;água para modificar**

Para modificar uma marca d&#39;água, é necessário recuperar uma marca d&#39;água existente. É possível recuperar uma marca d&#39;água especificando seu nome ou seu valor de identificador.

**Definir os atributos de marcas d&#39;água**

Para modificar uma marca d&#39;água existente, altere o valor de um ou mais atributos de marca d&#39;água. Ao atualizar programaticamente uma marca d&#39;água usando um serviço da Web, você deve definir todos os atributos que foram originalmente definidos, mesmo que o valor não seja alterado. Por exemplo, suponha que os seguintes atributos de marca d&#39;água estejam definidos: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`e `WaterBackCmd:SRCTEXT`. Embora o único atributo que você deseja modificar seja `WaterBackCmd:OPACITY`, é necessário definir os outros valores.

>[!NOTE]
>
>Ao usar a API Java para modificar uma marca d&#39;água, não é necessário especificar todos os atributos. Defina o atributo de marca d&#39;água que deseja modificar.

>[!NOTE]
>
>Para obter informações sobre os nomes de atributos de marca d&#39;água, consulte [Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks).

**Atualizar a marca d&#39;água**

Depois de modificar os atributos de uma marca d&#39;água, é necessário atualizar a marca d&#39;água.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks)

### Modificar marcas d&#39;água usando a API Java {#modify-watermarks-using-the-java-api}

Modifique uma marca d&#39;água usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como o adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere a marca d&#39;água para modificá-la.

   Crie um `WatermarkManager` objeto chamando o `DocumentSecurityClient` método do `getWatermarkManager` objeto e transmita um valor de string que especifica o nome da marca d&#39;água. Esse método retorna um `Watermark` objeto que representa a marca d&#39;água a ser modificada.

1. Defina os atributos de marca d&#39;água.

   Defina o atributo de opacidade da marca d&#39;água chamando o método do `Watermark` objeto `setOpacity` e transmitindo um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

   >[!NOTE]
   >
   >Este exemplo modifica somente o atributo opacity.

1. Atualize a marca d&#39;água.

   * Atualize a marca d&#39;água chamando o `WatermarkManager` método do `updateWatermark` objeto e transmita o `Watermark` objeto cujo atributo foi modificado.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o Start rápido (modo SOAP): Modificação de uma marca d&#39;água usando a seção da API Java.

### Modificar marcas d&#39;água usando a API de serviço da Web {#modify-watermarks-using-the-web-service-api}

Modifique uma marca d&#39;água usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere a marca d&#39;água para modificá-la.

   Recupere a marca d&#39;água para modificá-la chamando o `DocumentSecurityServiceClient` método do `getWatermarkByName` objeto. Passe um valor de string que especifica o nome da marca d&#39;água. Esse método retorna um `WatermarkSpec` objeto que representa a marca d&#39;água a ser modificada.

1. Defina os atributos de marca d&#39;água.

   * Para que cada propriedade de marca d&#39;água seja atualizada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto separado.
   * Defina o valor-chave atribuindo um valor ao membro de `MyMapOf_xsd_string_To_xsd_anyType_Item` dados do `key` objeto (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao membro de `MyMapOf_xsd_string_To_xsd_anyType_Item` dados do `value` objeto (por exemplo, `.50`).
   * Create a `MyArrayOf_xsd_anyType` object. Para cada `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto, chame o `MyArrayOf_xsd_anyType` método do `Add` objeto. Passe o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua o `MyArrayOf_xsd_anyType` objeto ao membro de `WatermarkSpec` dados do `values` objeto.

1. Atualize a marca d&#39;água.

   Atualize a marca d&#39;água chamando o `DocumentSecurityServiceClient` método do `updateWatermark` objeto e transmitindo o `WatermarkSpec` objeto que representa a marca d&#39;água a ser modificada.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o seguinte Start rápido:

* &quot;Start rápido (MTOM): Modificação de uma marca d&#39;água usando a API de serviço da Web&quot;

## Procurando Eventos {#searching-for-events}

O serviço Rights Management rastreia ações específicas à medida que ocorrem, como aplicar uma política a um documento, abrir um documento protegido por política e revogar o acesso a documentos. A auditoria de Eventos deve estar ativada para o serviço Rights Management ou os eventos não são rastreados.

Os Eventos se encaixam em uma das seguintes categorias:

* eventos de administrador são ações relacionadas a um administrador, como a criação de uma nova conta de administrador.
* eventos de Documento são ações relacionadas a um documento, como fechar um documento protegido por política.
* eventos de política são ações relacionadas a uma política, como a criação de uma nova política.
* Os eventos de serviço são ações relacionadas ao serviço Rights Management, como sincronizar com o diretório do usuário.

Você pode procurar eventos específicos usando a API Java do Rights Management ou a API de serviço da Web. Ao procurar eventos, você pode executar tarefas, como criar um arquivo de log de determinados eventos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Rights Management, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-10}

Para procurar um evento do Rights Management, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente Rights Management.
1. Especifique o evento para o qual pesquisar.
1. Procure o evento.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente Rights Management**

Antes de executar programaticamente uma operação de serviço de Gerenciamento de Direitos, é necessário criar um objeto cliente de serviço de Gerenciamento de Direitos. Se você estiver usando a API Java, crie um `DocumentSecurityClient` objeto. Se você estiver usando a API de serviço da Web do Rights Management, crie um `DocumentSecurityServiceService` objeto.

**Especificar os eventos a serem pesquisados**

Você deve especificar o evento a ser pesquisado. Por exemplo, você pode procurar o evento de criação de política, que ocorre quando uma nova política é criada.

**Procurar o evento**

Depois de especificar o evento a ser pesquisado, você pode usar a API Java do Rights Management ou a API do serviço da Web do Rights Management para pesquisar o evento.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Procurar eventos usando a API Java {#search-for-events-using-the-java-api}

Procure eventos usando a API de gerenciamento de direitos (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente Rights Management

   Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Especificar os eventos a serem pesquisados

   * Crie um `EventManager` objeto chamando o `DocumentSecurityClient` método do `getEventManager` objeto. Esse método retorna um `EventManager` objeto.
   * Crie um `EventSearchFilter` objeto chamando seu construtor.
   * Especifique o evento para o qual pesquisar chamando o método do `EventSearchFilter` objeto `setEventCode` e passando um membro de dados estáticos que pertence à `EventManager` classe que representa o evento para o qual pesquisar. Por exemplo, para pesquisar o evento de criação de política, passe `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Você pode definir critérios de pesquisa adicionais chamando métodos de `EventSearchFilter` objeto. Por exemplo, chame o `setUserName` método para especificar um usuário associado ao evento.

1. Procurar o evento

   Procure o evento chamando o `EventManager` método do `searchForEvents` objeto e transmitindo o `EventSearchFilter` objeto que define os critérios de pesquisa do evento. Esse método retorna uma matriz de `Event` objetos.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Start rápidos:

* &quot;Start rápido (SOAP): Procurando eventos usando a API Java&quot;

### Procurar eventos usando a API de serviço da Web {#search-for-events-using-the-web-service-api}

Procure eventos usando a API de Gerenciamento de Direitos (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Criar um objeto de API do cliente Rights Management

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Especificar os eventos a serem pesquisados

   * Crie um `EventSpec` objeto usando seu construtor.
   * Especifique o start do período de tempo durante o qual o evento ocorreu definindo o membro de `EventSpec` dados do `firstTime.date` objeto com a `DataTime` instância que representa o start do intervalo de datas quando o evento ocorreu.
   * Atribua o valor `true` ao membro `EventSpec` `firstTime.dateSpecified` de dados do objeto.
   * Especifique o fim do período de tempo durante o qual o evento ocorreu definindo o membro de `EventSpec` dados do `lastTime.date` objeto com a `DataTime` instância que representa o fim do intervalo de datas quando o evento ocorreu.
   * Atribua o valor `true` ao membro `EventSpec` `lastTime.dateSpecified` de dados do objeto.
   * Defina o evento a ser pesquisado atribuindo um valor de string ao membro de `EventSpec` dados do `eventCode` objeto. A tabela a seguir lista os valores numéricos que você pode atribuir a essa propriedade:

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

1. Procurar o evento

   Procure o evento chamando o `DocumentSecurityServiceClient` método do `searchForEvents` objeto e transmitindo o `EventSpec` objeto que representa o evento para o qual pesquisar e o número máximo de resultados. Esse método retorna uma `MyArrayOf_xsd_anyType` coleção em que cada elemento é uma `AuditSpec` instância. Usando uma `AuditSpec` instância, você pode obter informações sobre o evento, como a hora em que ele ocorreu. A `AuditSpec` instância contém um membro `timestamp` de dados que especifica essas informações.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Start rápidos:

* &quot;Start rápido (MTOM): Procurando eventos usando a API de serviço da Web&quot;
* &quot;Start rápido (SwaRef): Procurando eventos usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicar políticas a Documentos do Word {#applying-policies-to-word-documents}

Além de documentos PDF, o serviço Rights Management suporta formatos de documento adicionais, como um documento do Microsoft Word (arquivo DOC) e outros formatos de arquivo do Microsoft Office. Por exemplo, você pode aplicar uma política a um documento do Word para protegê-lo. Ao aplicar uma política a um documento do Word, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se o documento já estiver protegido por uma política.

Você pode monitorar o uso de um documento do Word protegido por política depois de distribuí-lo. Ou seja, vocês podem ver como o documento está sendo usado e quem está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-11}

Para aplicar uma política a um documento do Word, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Documento Security Client.
1. Recuperar um documento do Word ao qual uma política é aplicada.
1. Aplicar uma política existente ao documento do Word.
1. Salve o documento do Word protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do Cliente do Documento Security**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, você deve criar um objeto cliente de serviço de Segurança do Documento.

**Recuperar um documento do Word**

Você deve recuperar um documento do Word para aplicar uma política. Depois de aplicar uma política ao documento do Word, os usuários são restritos ao usar o documento. Por exemplo, se a política não permitir que o documento seja aberto offline, os usuários devem estar online para abrir o documento.

**Aplicar uma política existente ao documento do Word**

Para aplicar uma política a um documento do Word, é necessário referenciar uma política existente e especificar a qual conjunto de políticas a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salvar o documento do Word**

Depois que o serviço de Segurança do Documento aplicar uma política a um documento do Word, é possível salvar o documento do Word protegido por política como um arquivo DOC.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogação do acesso a Documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar uma política a um documento do Word usando a API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplique uma política a um documento do Word usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto.

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocumentSecurityClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento do Word.

   * Crie um `java.io.FileInputStream` objeto que represente o documento do Word usando seu construtor e transmitindo um valor de string que especifica o local do documento do Word.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Aplicar uma política existente ao documento do Word.

   * Crie um `DocumentManager` objeto chamando o `DocumentSecurityClient` método do `getDocumentManager` objeto.
   * Aplique uma política ao documento do Word chamando o método do `DocumentManager` objeto `protectDocument` e transmitindo os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém o documento do Word ao qual a política é aplicada.
      * Um valor de string que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta no conjunto de `MyPolicies` políticas que está sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser nulo).
      * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se esse parâmetro for `null`, o valor de parâmetro anterior deve ser `null`).
      * Uma `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e você pode especificar `null`.

      O `protectDocument` método retorna um `RMSecureDocumentResult` objeto que contém o documento do Word protegido por política.


1. Salve o documento do Word.

   * Chame o `RMSecureDocumentResult` `getProtectedDoc` método do objeto para obter o documento do Word protegido por política. Esse método retorna um `com.adobe.idp.Document` objeto.
   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é DOC.
   * Chame o `com.adobe.idp.Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `getProtectedDoc` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o seguinte Start rápido:

* &quot;Start rápido (modo SOAP): Aplicar uma política a um documento do Word usando a API do Java&quot;

### Aplicar uma política a um documento do Word usando a API de serviço da Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplique uma política a um documento do Word usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um objeto da API do Documento Security Client.

   * Crie um `DocumentSecurityServiceClient` objeto usando seu construtor padrão.
   * Crie um `DocumentSecurityServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DocumentSecurityServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento do Word.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento do Word ao qual uma política é aplicada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do `Length` objeto.
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Aplicar uma política existente ao documento do Word.

   Aplique uma política ao documento do Word chamando o método do `DocumentSecurityServiceClient` objeto `protectDocument` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento do Word ao qual a política é aplicada.
   * Um valor de string que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um `null` valor que resulta no conjunto de `MyPolicies` políticas que está sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor de parâmetro deverá ser `null`).
   * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor de parâmetro anterior deve ser `null`).
   * Um `RMLocale` valor que especifica o valor de localidade (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída de string usado para armazenar o valor do identificador de política.
   * Um parâmetro de saída de string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída de string usado para armazenar o tipo mime (por exemplo, `application/doc`).

   O `protectDocument` método retorna um `BLOB` objeto que contém o documento do Word protegido por política.

1. Salve o documento do Word.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `protectDocument` método. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo do Word chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o seguinte Start rápido:

* &quot;Start rápido (MTOM): Aplicar uma política a um documento do Word usando a API de serviço da Web&quot;

## Remover Políticas de Documentos do Word {#removing-policies-from-word-documents}

Você pode remover uma política de um documento do Word protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se quiser atualizar um documento do Word protegido por política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, é mais eficiente trocar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Segurança do Documento, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-12}

Para remover uma política de um documento do Word protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Documento Security Client.
1. Recuperar um documento do Word protegido por política.
1. Remova a política do documento do Word.
1. Salve o documento do Word não protegido.s

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Documento Security Client**

Antes de executar programaticamente uma operação de serviço de Segurança do Documento, crie um objeto cliente de serviço de Segurança do Documento.

**Recuperar um documento do Word protegido por política**

Você deve recuperar um documento do Word protegido por política para remover uma política. Se você tentar remover uma política de um documento do Word que não está protegido por uma política, causará uma exceção.

**Remover a política do documento do Word**

Você pode remover uma política de um documento do Word protegido por política, desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deverá conter a `SWITCH_POLICY` permissão para remover uma política de um documento do Word. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salvar o documento do Word não protegido**

Depois que o serviço de Segurança do Documento remover uma política de um documento do Word, é possível salvar o documento do Word não protegido como um arquivo DOC.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicar políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Remover uma política de um documento do Word usando a API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança do Documento (Java):

1. Incluir arquivos de projeto

   Inclua os arquivos JAR do cliente, como adobe-rights management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Documento Security Client

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `RightsManagementClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar um documento do Word protegido por política

   * Crie um `java.io.FileInputStream` objeto que represente o documento do Word protegido por política usando seu construtor e transmitindo um valor de string que especifica o local do documento do Word.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remover a política do documento do Word

   * Crie um `DocumentManager` objeto chamando o `RightsManagementClient` método do `getDocumentManager` objeto.
   * Remova uma política do documento do Word invocando o `DocumentManager` método do `removeSecurity` objeto e transmitindo o `com.adobe.idp.Document` objeto que contém o documento do Word protegido por política. Esse método retorna um `com.adobe.idp.Document` objeto que contém um documento do Word não protegido.

1. Salvar o documento do Word não protegido

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é DOC.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `removeSecurity` método).

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o seguinte Start rápido:

* &quot;Start rápido (modo SOAP): Remover uma política de um documento do Word usando a API Java&quot;

### Remover uma política de um documento do Word usando a API de serviço da Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança do Documento (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Criar um objeto de API do Documento Security Client

   * Crie um `RightsManagementServiceClient` objeto usando seu construtor padrão.
   * Crie um `RightsManagementServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `RightsManagementServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento do Word protegido por política

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento do Word protegido por política do qual a política é removida.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Remover a política do documento do Word

   Remova a política do documento do Word invocando o `RightsManagementServiceClient` método do `removePolicySecurity` objeto e transmitindo o `BLOB` objeto que contém o documento do Word protegido por política. Esse método retorna um `BLOB` objeto que contém um documento do Word não protegido.

1. Salvar o documento do Word não protegido

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento do Word não protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `removePolicySecurity` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.

**Exemplos de código**

Para obter exemplos de código usando o serviço de Segurança do Documento, consulte o seguinte Start rápido:

* &quot;Start rápido (MTOM): Remover uma política de um documento do Word usando a API de serviço da Web&quot;

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
