---
title: Protegendo documentos com políticas
seo-title: Protegendo documentos com políticas
description: Use o serviço de segurança de documentos para aplicar dinamicamente configurações de confidencialidade a documentos do Adobe PDF e manter o controle sobre os documentos. O serviço de segurança de documentos também permite que os usuários mantenham o controle sobre como os recipients usam o documento PDF protegido por políticas.
seo-description: Use o serviço de segurança de documentos para aplicar dinamicamente configurações de confidencialidade a documentos do Adobe PDF e manter o controle sobre os documentos. O serviço de segurança de documentos também permite que os usuários mantenham o controle sobre como os recipients usam o documento PDF protegido por políticas.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '15559'
ht-degree: 0%

---


# Protegendo documentos com políticas {#protecting-documents-with-policies}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço de segurança de documentos**

O serviço de segurança de documentos permite que os usuários apliquem dinamicamente configurações de confidencialidade a documentos da Adobe PDF e mantenham o controle sobre os documentos, independentemente da extensão de distribuição.

O serviço de segurança de documentos impede que as informações se espalhem além do alcance do usuário, permitindo que os usuários mantenham o controle sobre como os recipients usam o documento PDF protegido por políticas. Um usuário pode especificar quem pode abrir um documento, limitar como ele pode usá-lo e monitorar o documento após a distribuição. Um usuário também pode controlar dinamicamente o acesso a um documento protegido por políticas e pode até mesmo revogar dinamicamente o acesso ao documento.

O serviço Segurança de documentos também protege outros tipos de arquivos, como arquivos do Microsoft Word (arquivos DOC). Você pode usar a API do cliente de segurança de documentos para trabalhar com esses tipos de arquivos. As seguintes versões são compatíveis:

* Arquivos do Microsoft Office 2003 (arquivos DOC, XLS, PPT)
* Arquivos do Microsoft Office 2007 (arquivos DOCX, XLSX, PPTX)
* Arquivos PTC Pro/E

Para maior clareza, as duas seções a seguir discutem como trabalhar com documentos do Word:

* [Aplicando Políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Remover Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

Você pode realizar essas tarefas usando o serviço Segurança de documentos:

* Criar políticas. Para obter informações, consulte [Criando Políticas](protecting-documents-policies.md#creating-policies).
* Modificar políticas. Para obter informações, consulte [Modificando Políticas](protecting-documents-policies.md#modifying-policies).
* Excluir políticas. Para obter informações, consulte [Excluindo Políticas](protecting-documents-policies.md#deleting-policies).
* Aplicar políticas a documentos PDF. Para obter informações, consulte [Aplicando Políticas a Documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* Remova políticas de documentos PDF. Para obter informações, consulte [Removendo Políticas de Documentos PDF](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Documentos protegidos por políticas da Inspect. Para obter informações, consulte [Inspecionando documentos PDF protegidos por política](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* Revogar o acesso a documentos PDF. Para obter informações, consulte [Revogando acesso a documentos](protecting-documents-policies.md#revoking-access-to-documents).
* Retomar o acesso aos documentos revogados. Para obter informações, consulte [Reinstalando o Acesso a Documentos Revogados](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* Criar marcas d&#39;água. Para obter informações, consulte [Criando Marcas D&#39;Água](protecting-documents-policies.md#creating-watermarks).
* Procure por eventos. Para obter informações, consulte [Procurando Eventos](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criando Políticas {#creating-policies}

Você pode criar políticas programaticamente usando a API do Java de segurança de documentos ou a API do serviço da Web. Uma *policy* é uma coleção de informações que inclui configurações de segurança de documentos, usuários autorizados e direitos de uso. Você pode criar e salvar qualquer número de políticas, usando configurações de segurança apropriadas para diferentes situações e usuários.

As políticas permitem que você execute estas tarefas:

* Especifique os indivíduos que podem abrir o documento. Os recipients podem pertencer à organização ou ser externos a ela.
* Especifique como os destinatários podem usar o documento. Você pode restringir o acesso a diferentes recursos do Acrobat e Adobe Reader. Esses recursos incluem a capacidade de imprimir e copiar texto, adicionar assinaturas e adicionar comentários a um documento.
* Altere as configurações de acesso e segurança a qualquer momento, mesmo depois de distribuir o documento protegido por política.
* Monitore o uso do documento após distribuí-lo. Você pode ver como o documento está sendo usado e quem o está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

### Criação de uma política usando serviços da Web {#creating-a-policy-using-web-services}

Ao criar uma política usando a API do serviço da Web, consulte um arquivo XML da Linguagem de direitos de documento portátil (PDRL) existente que descreve a política. As permissões de política e o principal são definidos no documento PDRL. O documento XML a seguir é um exemplo de um documento PDRL.

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
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar uma política, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Defina os atributos da política.
1. Crie uma entrada de política.
1. Registre a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-rightsmanagement-client.jar
* namespace.jar (se o AEM Forms estiver implantado no JBoss)
* jaxb-api.jar (se o AEM Forms estiver implantado no JBoss)
* jaxb-impl.jar (se o AEM Forms estiver implantado no JBoss)
* jaxb-libs.jar (se o AEM Forms estiver implantado no JBoss)
* jaxb-xjc.jar (se o AEM Forms for implantado no JBoss)
* relaxngDatatype.jar (se o AEM Forms for implantado no JBoss)
* xsdlib.jar (se o AEM Forms estiver implantado no JBoss)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar (use um arquivo JAR diferente se o AEM Forms não estiver implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documento, crie um objeto cliente de serviço de Segurança de documento.

**Definir os atributos da política**

Para criar uma política, defina os atributos da política. Um atributo obrigatório é o nome da política. Os nomes de políticas devem ser exclusivos para cada conjunto de políticas. Um conjunto de políticas é simplesmente uma coleção de políticas. Pode haver duas políticas com o mesmo nome se as políticas pertencerem a conjuntos de políticas separados. No entanto, duas políticas em um único conjunto de políticas não podem ter o mesmo nome de política.

Outro atributo útil a ser definido é o período de validade. Um período de validade é o período durante o qual um documento protegido por uma política é acessível aos destinatários autorizados. Se você não definir esse atributo, a política sempre será válida.

Um período de validade pode ser definido como uma destas opções:

* Um número definido de dias em que o documento é acessível a partir do momento em que o documento é publicado
* Uma data final após a qual o documento não está acessível
* Um intervalo de datas específico para o qual o documento está acessível
* Sempre válido

Você pode especificar apenas uma data de início, o que resulta na validade da política após a data de início. Se você especificar apenas uma data de término, a política será válida até a data de término. No entanto, uma exceção é lançada se uma data inicial e uma data final não estiverem definidas.

Ao definir atributos que pertencem a uma política, também é possível definir configurações de criptografia. Essas configurações de criptografia ocorrem quando a política é aplicada a um documento. Você pode especificar os seguintes valores de criptografia:

* **AES256**: Representa o algoritmo de criptografia AES com uma chave de 256 bits.
* **AES128**: Representa o algoritmo de criptografia AES com uma chave de 128 bits.
* **NoEncryption:** não representa criptografia.

Ao especificar a opção `NoEncryption`, não é possível definir a opção `PlaintextMetadata` como `false`. Se você tentar fazer isso, uma exceção será lançada.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte a descrição da interface `Policy` no [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Criar uma entrada de política**

Uma entrada de política anexa entidades principais, que são grupos e usuários, e permissões a uma política. Uma política deve ter pelo menos uma entrada política. Considere, por exemplo, que você executa essas tarefas:

* Crie e registre uma entrada de política que permita que um grupo exiba apenas um documento enquanto estiver online e proíba os destinatários de copiá-lo.
* Anexe a entrada de política à política.
* Proteja um documento com a política usando o Acrobat.

Essas ações resultam em recipients serem capazes apenas de exibir o documento online e não poderem copiá-lo. O documento permanece seguro até que a segurança seja removida dele.

**Registrar a política**

Uma nova política deve ser registrada antes de poder ser usada. Depois de registrar uma política, você pode usá-la para proteger documentos.

### Crie uma política usando a API Java {#create-a-policy-using-the-java-api}

Crie uma política usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Defina os atributos da política.

   * Crie um objeto `Policy` chamando o método `InfomodelObjectFactory` estático `createPolicy` do objeto. Este método retorna um objeto `Policy`.
   * Defina o atributo de nome da política chamando o método `Policy` do objeto `setName` e passando um valor de string que especifica o nome da política.
   * Defina a descrição da política chamando o método `Policy` do objeto `setDescription` e passando um valor de string que especifica a descrição da política.
   * Defina o conjunto de políticas ao qual a nova política pertence, chamando o método `Policy` do objeto e passando um valor de string que especifica o nome do conjunto de políticas. `setPolicySetName` (Você pode especificar `null` para esse valor de parâmetro que resulta na política sendo adicionada ao conjunto de políticas *Minhas políticas*.)
   * Crie o período de validade da política chamando o método `InfomodelObjectFactory` estático `createValidityPeriod` do objeto. Este método retorna um objeto `ValidityPeriod`.
   * Defina o número de dias para os quais um documento protegido por política é acessível, chamando o método `ValidityPeriod` do objeto `setRelativeExpirationDays` e passando um valor inteiro que especifica o número de dias.
   * Defina o período de validade da política chamando o método `Policy` do objeto e transmitindo o objeto `ValidityPeriod`.`setValidityPeriod`

1. Crie uma entrada de política.

   * Crie uma entrada de política chamando o método `InfomodelObjectFactory` estático `createPolicyEntry` do objeto. Este método retorna um objeto `PolicyEntry`.
   * Especifique as permissões da política chamando o método `InfomodelObjectFactory` estático `createPermission` do objeto. Passe um membro de dados estáticos que pertence à interface `Permission` que representa a permissão. Este método retorna um objeto `Permission`. Por exemplo, para adicionar a permissão que permite aos usuários copiar dados de um documento PDF protegido por política, passe `Permission.COPY`. (Repita essa etapa para cada permissão para adicionar).
   * Adicione a permissão à entrada da política chamando o método `PolicyEntry` do objeto `addPermission` e transmitindo o objeto `Permission`. (Repita essa etapa para cada objeto `Permission` que você criou).
   * Crie o principal da política chamando o método `InfomodelObjectFactory` estático `createSpecialPrincipal` do objeto. Passe um membro de dados que pertence ao objeto `InfomodelObjectFactory` que representa o principal. Este método retorna um objeto `Principal`. Por exemplo, para adicionar o editor do documento como principal, passe `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * Adicione o principal à entrada da política, chamando o método `PolicyEntry` do objeto e passando o objeto `Principal`.`setPrincipal`
   * Adicione a entrada da política à política chamando o método `Policy` do objeto `addPolicyEntry` e transmitindo o objeto `PolicyEntry`.

1. Registre a política.

   * Crie um objeto `PolicyManager` chamando o método `DocumentSecurityClient` `getPolicyManager` do objeto.
   * Registre a política chamando o método `PolicyManager` do objeto `registerPolicy` e transmitindo os seguintes valores:

      * O objeto `Policy` que representa a política a ser registrada.
   * Um valor de string que representa o conjunto de políticas ao qual a política pertence.

   Se você usar uma conta de administrador do AEM forms nas configurações de conexão para criar o objeto `DocumentSecurityClient`, especifique o nome do conjunto de políticas ao chamar o método `registerPolicy`. Se você passar um valor `null` para o conjunto de políticas, a política será criada no conjunto de políticas de administradores *Minhas Políticas*.

   Se você usar um usuário de Segurança de documento nas configurações de conexão, poderá invocar o método sobrecarregado `registerPolicy` que aceita apenas a política. Ou seja, você não precisa especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas Políticas*. Se não quiser adicionar a nova política a esse conjunto de políticas, especifique um nome de conjunto de políticas ao chamar o método `registerPolicy`.

   >[!NOTE]
   >
   >Ao criar uma política, faça referência a um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, uma exceção será lançada.

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte:

* &quot;Início rápido (modo SOAP): Criar uma política usando a API do Java&quot;

### Criar uma política usando a API do serviço da Web {#create-a-policy-using-the-web-service-api}

Crie uma política usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina os atributos da política.

   * Crie um objeto `PolicySpec` usando seu construtor.
   * Defina o nome da política atribuindo um valor de string ao membro de dados `PolicySpec` do objeto `name`.
   * Defina a descrição da política atribuindo um valor de string ao membro de dados `PolicySpec` do objeto `description`.
   * Defina o conjunto de políticas ao qual a política pertencerá, atribuindo um valor de string ao `PolicySpec` membro de dados `policySetName` do objeto. Você deve especificar um nome de conjunto de políticas existente. (Você pode especificar `null` para esse valor de parâmetro que resulta na política sendo adicionada a *Minhas Políticas*.)
   * Defina o período de concessão offline da política atribuindo um valor inteiro ao membro de dados `PolicySpec` do objeto `offlineLeasePeriod`.
   * Defina o membro de dados `PolicySpec` do objeto `policyXml` com um valor de string que represente dados XML de PDRL. Para executar essa tarefa, crie um objeto .NET `StreamReader` usando seu construtor. Passe o local de um arquivo XML PDRL que representa a política para o construtor `StreamReader`. Em seguida, chame o método `StreamReader` do objeto e atribua o valor de retorno a uma variável de string. `ReadLine` Itere pelo objeto `StreamReader` até que o método `ReadLine` retorne nulo. Atribua a variável da string ao membro de dados `PolicySpec` do objeto.`policyXml`

1. Crie uma entrada de política.

   Não é necessário criar uma entrada de política ao criar uma política usando a API do serviço da Web Document Security. A entrada de política é definida no documento PDRL.

1. Registre a política.

   Registre a política chamando o método `DocumentSecurityServiceClient` do objeto `registerPolicy` e transmitindo os seguintes valores:

   * O objeto `PolicySpec` que representa a política a ser registrada.
   * Um valor de string que representa o conjunto de políticas ao qual a política pertence. Você pode especificar um valor `null` que resulta na adição da política ao conjunto de políticas *MyPolices*.

   Se você usar uma conta de administrador do AEM forms nas configurações de conexão para criar o objeto `DocumentSecurityClient` , especifique o nome do conjunto de políticas ao chamar o método `registerPolicy`.

   Se você usar um usuário de Segurança de documento nas configurações de conexão, poderá invocar o método sobrecarregado `registerPolicy` que aceita somente a política. Ou seja, você não precisa especificar o nome do conjunto de políticas. No entanto, a política é adicionada ao conjunto de políticas chamado *Minhas Políticas*. Se não quiser adicionar a nova política a esse conjunto de políticas, especifique um nome de conjunto de políticas ao chamar o método `registerPolicy`.

   >[!NOTE]
   >
   >Ao criar uma política e especificar um conjunto de políticas, especifique um conjunto de políticas existente. Se você especificar um conjunto de políticas que não existe, uma exceção será lançada.

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Criação de uma política usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Criação de uma política usando a API do serviço da Web&quot;

## Modificando Políticas {#modifying-policies}

Você pode modificar uma política existente usando a API do Java de segurança de documentos ou a API do serviço da Web. Para fazer alterações em uma política existente, você a recupera, a modifica e então atualiza a política no servidor. Por exemplo, suponha que você recupere uma política existente e estenda seu período de validade. Antes que a alteração entre em vigor, você deve atualizar a política.

Você pode modificar uma política quando os requisitos da empresa mudarem e a política não refletir mais esses requisitos. Em vez de criar uma nova política, você pode simplesmente atualizar uma política existente.

Para modificar atributos de política usando um serviço da Web (por exemplo, usando classes proxy Java criadas com JAX-WS), é necessário garantir que a política seja registrada no serviço de Segurança de documento. Você pode fazer referência à política existente usando o método `PolicySpec.getPolicyXml` e modificar os atributos da política usando os métodos aplicáveis. Por exemplo, você pode modificar o período de concessão offline chamando o método `PolicySpec.setOfflineLeasePeriod`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para modificar uma política existente, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere uma política existente.
1. Alterar atributos de políticas.
1. Atualize a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento. Se estiver usando a API do Java, crie um objeto `RightsManagementClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `RightsManagementServiceService`.

**Recuperar uma política existente**

Você deve recuperar uma política existente para modificá-la. Para recuperar uma política, especifique o nome da política e o conjunto de políticas ao qual a política pertence. Se você especificar um valor `null` para o nome do conjunto de políticas, a política será recuperada do conjunto de políticas *Minhas Políticas*.

**Definir os atributos da política**

Para modificar uma política, você modifica o valor dos atributos de política. O único atributo de política que não pode ser alterado é o atributo name. Por exemplo, para alterar o período de concessão offline da política, você pode modificar o valor do atributo de período de concessão offline da política.

Ao modificar o período de concessão offline de uma política usando um serviço da Web, o campo `offlineLeasePeriod` na interface `PolicySpec` é ignorado. Para atualizar o período de concessão offline, modifique o elemento `OfflineLeasePeriod` no documento XML PDRL. Em seguida, faça referência ao documento XML PDRL atualizado usando o `PolicySpec` membro de dados `policyXML` da interface.

>[!NOTE]
>
>Para obter informações sobre outros atributos que podem ser definidos, consulte a descrição da interface `Policy` no [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Atualizar a política**

Antes que as alterações feitas em uma política sejam aplicadas, é necessário atualizar a política com o serviço de Segurança de documentos. As alterações nas políticas que protegem documentos são atualizadas na próxima vez que o documento protegido por política for sincronizado com o serviço de Segurança de documentos.

### Modifique as políticas existentes usando a API Java {#modify-existing-policies-using-the-java-api}

Modifique uma política existente usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere uma política existente.

   * Crie um objeto `PolicyManager` chamando o método `RightsManagementClient` `getPolicyManager` do objeto.
   * Crie um objeto `Policy` que represente a política a ser atualizada chamando o método `PolicyManager` do objeto `getPolicy` e transmitindo os seguintes valores&quot;

      * Um valor de string que representa o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
      * Um valor de string que representa o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às suas necessidades de negócios. Por exemplo, para alterar o período de concessão offline da política, chame o método `Policy` do objeto `setOfflineLeasePeriod`.

1. Atualize a política.

   Atualize a política chamando o método `PolicyManager` do objeto `updatePolicy`. Passe o objeto `Policy` que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o Início rápido (modo SOAP): Modificação de uma política usando a seção API do Java .

### Modifique as políticas existentes usando a API do serviço da Web {#modify-existing-policies-using-the-web-service-api}

Modifique uma política existente usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere uma política existente.

   Crie um objeto `PolicySpec` que represente a política a ser modificada chamando o método `RightsManagementServiceClient` do objeto `getPolicy` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
   * Um valor da string que especifica o nome da política.

1. Defina os atributos da política.

   Altere os atributos da política para atender às suas necessidades de negócios.

1. Atualize a política.

   Atualize a política chamando o método `RightsManagementServiceClient` do objeto `updatePolicyFromSDK` e transmitindo o objeto `PolicySpec` que representa a política a ser atualizada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Modificação de uma política usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Modificação de uma política usando a API do serviço da Web&quot;

## Excluindo Políticas {#deleting-policies}

É possível excluir uma política existente usando a API do Java de segurança de documento ou a API do serviço da Web. Depois que uma política é excluída, ela não pode mais ser usada para proteger documentos. No entanto, os documentos protegidos por políticas que estão usando a política ainda estão protegidos. É possível excluir uma política quando uma nova estiver disponível.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para excluir uma política existente, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Cliente de segurança de documento.
1. Exclua a política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento. Se estiver usando a API do Java, crie um objeto `RightsManagementClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `RightsManagementServiceService`.

**Excluir a política**

Para excluir uma política, especifique a política a ser excluída e o conjunto de políticas ao qual a política pertence. O usuário cujas configurações são usadas para chamar o AEM Forms deve ter permissão para excluir a política; caso contrário, ocorrerá uma exceção. Da mesma forma, se você tentar excluir uma política que não existe, ocorrerá uma exceção.

### Excluir políticas usando a API Java {#delete-policies-using-the-java-api}

Exclua uma política usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Exclua a política.

   * Crie um objeto `PolicyManager` chamando o método `RightsManagementClient` `getPolicyManager` do objeto.
   * Exclua a política chamando o método `PolicyManager` do objeto `deletePolicy` e passando os seguintes valores:

      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
      * Um valor da string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Excluir uma política usando a API do Java&quot;

### Excluir políticas usando a API do serviço da Web {#delete-policies-using-the-web-service-api}

Exclua uma política usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Exclua a política.

   Exclua uma política chamando o método `RightsManagementServiceClient` do objeto `deletePolicy` e passando os seguintes valores:

   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
   * Um valor da string que especifica o nome da política a ser excluída.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Exclusão de uma política usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Exclusão de uma política usando a API do serviço da Web&quot;

## Aplicação de políticas a documentos PDF {#applying-policies-to-pdf-documents}

É possível aplicar uma política a um documento PDF para proteger o documento. Ao aplicar uma política a um documento PDF, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se ele já estiver protegido por uma política.

Enquanto o documento estiver aberto, você também poderá restringir o acesso aos recursos do Acrobat e Adobe Reader, incluindo a capacidade de imprimir e copiar texto, fazer alterações e adicionar assinaturas e comentários a um documento. Além disso, você pode revogar um documento PDF protegido por políticas quando não quiser mais que os usuários acessem o documento.

Você pode monitorar o uso de um documento protegido por políticas depois de distribuí-lo. Ou seja, você pode ver como o documento está sendo usado e quem o está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para aplicar uma política a um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere um documento PDF ao qual uma política é aplicada.
1. Aplique uma política existente ao documento PDF.
1. Salve o documento PDF protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documento, crie um objeto cliente de serviço de Segurança de documento. Se estiver usando a API do Java, crie um objeto `DocumentSecurityClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `DocumentSecurityServiceService`.

**Recuperar um documento PDF**

Você pode recuperar um documento PDF para aplicar uma política. Depois de aplicar uma política ao documento PDF, os usuários são restritos ao usar o documento. Por exemplo, se a política não habilitar a abertura do documento offline, os usuários deverão estar online para abrir o documento.

**Aplicar uma política existente ao documento PDF**

Para aplicar uma política a um documento PDF, consulte uma política existente e especifique a que conjunto de políticas a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salvar o documento PDF**

Depois que o serviço de segurança de documento aplicar uma política a um documento PDF, você poderá salvar o documento PDF protegido por política como um arquivo PDF.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogando o acesso aos documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar uma política a um documento PDF usando a API Java {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Aplique uma política a um documento PDF usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere um documento PDF.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Aplique uma política existente ao documento PDF.

   * Crie um objeto `DocumentManager` chamando o método `RightsManagementClient` `getDocumentManager` do objeto.
   * Aplique uma política ao documento PDF chamando o método `DocumentManager` do objeto `protectDocument` e transmitindo os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém o documento PDF ao qual a política é aplicada.
      * Um valor de string que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um valor `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor do parâmetro deve ser nulo).
      * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se esse parâmetro for nulo, o valor do parâmetro anterior deverá ser `null`).
      * Um `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e não é usado para documentos PDF. Para proteger um documento PDF, especifique `null`.

      O método `protectDocument` retorna um objeto `RMSecureDocumentResult` que contém o documento PDF protegido por política.


1. Salve o documento PDF.

   * Chame o método `RMSecureDocumentResult` do objeto `getProtectedDoc` para obter o documento PDF protegido por política. Este método retorna um objeto `com.adobe.idp.Document`.
   * Crie um objeto `java.io.File` e verifique se a extensão de arquivo é PDF.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `getProtectedDoc`).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo EJB): Aplicar uma política a um documento PDF usando a API do Java&quot;
* &quot;Início rápido (modo SOAP): Aplicar uma política a um documento PDF usando a API do Java&quot;

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplicar uma política a um documento PDF usando a API do serviço da Web {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Aplique uma política a um documento PDF usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento PDF.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF ao qual uma política é aplicada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Determine o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Aplique uma política existente ao documento PDF.

   Aplique uma política ao documento PDF chamando o método `RightsManagementServiceClient` do objeto `protectDocument` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF ao qual a política é aplicada.
   * Um valor de string que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um valor `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor do parâmetro deve ser `null`).
   * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor do parâmetro anterior deve ser `null`).
   * Um valor `RMLocale` que especifica o valor do local (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída da string usado para armazenar o valor do identificador de política.
   * Um parâmetro de saída de string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída de string usado para armazenar o tipo MIME (por exemplo, `application/pdf`).

   O método `protectDocument` retorna um objeto `BLOB` que contém o documento PDF protegido por política.

1. Salve o documento PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `protectDocument`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Aplicar uma política a um documento PDF usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Aplicar uma política a um documento PDF usando a API do serviço da Web&quot;

## Removendo políticas de documentos PDF {#removing-policies-from-pdf-documents}

Você pode remover uma política de um documento protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se quiser atualizar um documento protegido por uma política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, é mais eficiente mudar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para remover uma política de um documento PDF protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere um documento PDF protegido por política.
1. Remova a política do documento PDF.
1. Salve o documento PDF inseguro.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documento, crie um objeto cliente de serviço de Segurança de documento.

**Recuperar um documento PDF protegido por política**

Você pode recuperar um documento PDF protegido por uma política para remover uma política. Se você tentar remover uma política de um documento PDF que não está protegido por uma política, ocorrerá uma exceção.

**Remover a política do documento PDF**

É possível remover uma política de um documento PDF protegido por políticas, desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deverá conter a permissão `SWITCH_POLICY` para remover uma política de um documento PDF. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salvar o documento PDF não seguro**

Depois que o serviço de segurança de documentos remove uma política de um documento PDF, é possível salvar o documento PDF não seguro como um arquivo PDF.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Remova uma política de um documento PDF usando a API Java {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Remova uma política de um documento PDF protegido por políticas usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere um documento PDF protegido por política.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF protegido por política usando seu construtor e transmitindo um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remova a política do documento PDF.

   * Crie um objeto `DocumentManager` chamando o método `DocumentSecurityClient` `getDocumentManager` do objeto.
   * Remova uma política do documento PDF chamando o método `DocumentManager` do objeto e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF protegido por política. `removeSecurity` Esse método retorna um objeto `com.adobe.idp.Document` que contém um documento PDF inseguro.

1. Salve o documento PDF inseguro.

   * Crie um objeto `java.io.File` e verifique se a extensão de arquivo é PDF.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `removeSecurity`).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Remover uma política de um documento PDF usando a API Java&quot;

### Remova uma política usando a API do serviço da Web {#remove-a-policy-using-the-web-service-api}

Remova uma política de um documento PDF protegido por política usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento PDF protegido por política.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF protegido por política do qual a política é removida.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Remova a política do documento PDF.

   Remova a política do documento PDF chamando o método `DocumentSecurityServiceClient` do objeto `removePolicySecurity` e transmitindo o objeto `BLOB` que contém o documento PDF protegido por política. Esse método retorna um objeto `BLOB` que contém um documento PDF inseguro.

1. Salve o documento PDF inseguro.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `removePolicySecurity`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Remover uma política de um documento PDF usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Remover uma política de um documento PDF usando a API do serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Revogando o acesso aos documentos {#revoking-access-to-documents}

Você pode revogar o acesso a um documento PDF protegido por políticas, resultando em todas as cópias do documento serem inacessíveis aos usuários. Quando um usuário tenta abrir um documento PDF revogado, ele é redirecionado para um URL especificado, onde um documento revisado pode ser visualizado. O URL para onde o usuário é redirecionado deve ser especificado de forma programática. Quando você revoga o acesso a um documento, a alteração entrará em vigor na próxima vez que o usuário sincronizar com o serviço de Segurança de documentos, abrindo o documento protegido por política online.

A capacidade de revogar o acesso a um documento fornece segurança adicional. Por exemplo, suponha que uma versão mais recente de um documento esteja disponível e você não quer mais que ninguém visualize a versão desatualizada. Nessa situação, o acesso ao documento mais antigo pode ser revogado e ninguém pode exibi-lo a menos que o acesso seja recriado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para revogar um documento protegido por política, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere um documento PDF protegido por política.
1. Revogar o documento protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento.

**Recuperar um documento PDF protegido por política**

Você deve recuperar um documento PDF protegido por política para revogá-lo. Não é possível revogar um documento que já foi revogado ou que não é um documento protegido por uma política.

Se você souber o valor do identificador de licença do documento protegido por política, não será necessário recuperar o documento PDF protegido por política. No entanto, na maioria dos casos, será necessário recuperar o documento PDF para obter o valor do identificador de licença.

**Revogar o documento protegido por política**

Para revogar um documento protegido por política, especifique o identificador de licença do documento protegido por política. Além disso, você pode especificar o URL de um documento que o usuário pode visualizar ao tentar abrir o documento revogado. Ou seja, suponha que um documento desatualizado seja revogado. Quando um usuário tenta abrir o documento revogado, ele verá um documento atualizado em vez do documento revogado.

>[!NOTE]
>
>Se você tentar revogar um documento que já foi revogado, uma exceção será lançada.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Reposição do acesso a documentos revisados](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Revogar o acesso a documentos usando a API Java {#revoke-access-to-documents-using-the-java-api}

Revogar o acesso a um documento PDF protegido por políticas usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Cliente de segurança de documentos

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar um documento PDF protegido por política

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF protegido por política usando seu construtor e transmitindo um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Revogar o documento protegido por política

   * Crie um objeto `DocumentManager` chamando o método `DocumentSecurityClient` `getDocumentManager` do objeto.
   * Recupere o valor do identificador da licença do documento protegido por política, chamando o método `DocumentManager` do objeto `getLicenseId`. Passe o objeto `com.adobe.idp.Document` que representa o documento protegido por política. Esse método retorna um valor de string que representa o valor do identificador de licença.
   * Crie um objeto `LicenseManager` chamando o método `DocumentSecurityClient` `getLicenseManager` do objeto.
   * Revoge o documento protegido por política, chamando o método `LicenseManager` do objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do método `DocumentManager` do objeto `getLicenseId`).
      * Um membro de dados estáticos da interface `License` que especifica o motivo para revogar o documento. Por exemplo, você pode especificar `License.DOCUMENT_REVISED`.
      * Um valor `java.net.URL` que especifica o local onde um documento revisado está localizado. Se você não deseja redirecionar um usuário para outro URL, é possível enviar `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Revogar um documento usando a API do Java&quot;

### Revogar o acesso a documentos usando a API do serviço da Web {#revoke-access-to-documents-using-the-web-service-api}

Revogar o acesso a um documento PDF protegido por políticas usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do Cliente de segurança de documentos

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento PDF protegido por política

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF protegido por política que é revogado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF protegido por política a ser revogado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Revogar o documento protegido por política

   * Recupere o valor do identificador da licença do documento protegido por política, chamando o método `DocumentSecurityServiceClient` do objeto `getLicenseID` e transmitindo o objeto `BLOB` que representa o documento protegido por política. Esse método retorna um valor de string que representa o identificador de licença.
   * Revoge o documento protegido por política, chamando o método `DocumentSecurityServiceClient` do objeto `revokeLicense` e transmitindo os seguintes valores:

      * Um valor de string que especifica o valor do identificador de licença do documento protegido por política (especifique o valor de retorno do método `DocumentSecurityServiceService` do objeto `getLicenseId`).
      * Um membro de dados estáticos do enum `Reason` que especifica o motivo para revogar o documento. Por exemplo, você pode especificar `Reason.DOCUMENT_REVISED`.
      * Um valor `string` que especifica o local do URL para onde um documento revisado está localizado. Se você não deseja redirecionar um usuário para outro URL, é possível enviar `null`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Revogar um documento usando a API de serviço da Web&quot;
* &quot;Início rápido (SwaRef): Revogar um documento usando a API de serviço da Web&quot;

**Consulte também:**

[Remover Políticas de Documentos do Word](protecting-documents-policies.md#removing-policies-from-word-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Reinstalando o acesso aos documentos revogados {#reinstating-access-to-revoked-documents}

Você pode restabelecer o acesso a um documento PDF revogado, resultando em todas as cópias do documento revogado serem acessíveis aos usuários. Quando um usuário abre um documento recriado que foi revogado, ele pode visualizar o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para restabelecer o acesso a um documento PDF revogado, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere o identificador da licença do documento PDF revogado.
1. Retomar o acesso ao documento PDF revogado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento. Se estiver usando a API do Java, crie um objeto `DocumentSecurityClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `DocumentSecurityServiceService`.

**Recuperar o identificador de licença do documento PDF revogado**

Você deve recuperar o identificador de licença do documento PDF revogado para restabelecer um documento PDF revogado. Após obter o valor do identificador de licença, é possível reinstalar um documento revogado. Se tentar reinstalar um documento que não foi revogado, ocorrerá uma exceção.

**Retomar o acesso ao documento PDF revogado**

Para restabelecer o acesso a um documento PDF revogado, você deve especificar o identificador de licença do documento revogado. Se você tentar restabelecer o acesso a um documento PDF que não foi revogado, ocorrerá uma exceção.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[Revogando o acesso aos documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Retomar o acesso a documentos revogados usando a API Java {#reinstate-access-to-revoked-documents-using-the-java-api}

Instale novamente o acesso a um documento revogado usando a API de segurança de documento (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o identificador da licença do documento PDF revogado.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF revogado usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.
   * Crie um objeto `DocumentManager` chamando o método `DocumentSecurityClient` `getDocumentManager` do objeto.
   * Recupere o valor do identificador da licença do documento revogado, chamando o método `DocumentManager` do objeto `getLicenseId` e transmitindo o objeto `com.adobe.idp.Document` que representa o documento revogado. Esse método retorna um valor de string que representa o identificador de licença.

1. Retomar o acesso ao documento PDF revogado.

   * Crie um objeto `LicenseManager` chamando o método `DocumentSecurityClient` `getLicenseManager` do objeto.
   * Reinstale o acesso ao documento PDF revogado chamando o método `LicenseManager` do objeto `unrevokeLicense` e transmitindo o valor do identificador de licença do documento revogado.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Reposição do acesso a um documento revogado usando a API do serviço da Web&quot;

### Retomar o acesso a documentos revogados usando a API do serviço da Web {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Instale novamente o acesso a um documento revogado usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere o identificador da licença do documento PDF revogado.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF revogado para o qual o acesso é restabelecido.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF revogado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Retomar o acesso ao documento PDF revogado.

   * Recupere o valor do identificador da licença do documento revogado, chamando o método `DocumentSecurityServiceClient` do objeto `getLicenseID` e transmitindo o objeto `BLOB` que representa o documento revogado. Esse método retorna um valor de string que representa o identificador de licença.
   * Reinstale o acesso ao documento PDF revogado chamando o método `DocumentSecurityServiceClient` do objeto e passando um valor de string que especifica o valor do identificador de licença do documento PDF revogado (passe o valor de retorno do método `DocumentSecurityServiceClient` do objeto `getLicenseId`).`unrevokeLicense`

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Reposição do acesso a um documento revogado usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Reposição do acesso a um documento revogado usando a API do serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Como inspecionar Documentos PDF Protegidos pela Política {#inspecting-policy-protected-pdf-documents}

Você pode usar a API do Serviço de segurança de documentos (Java e serviço da Web) para inspecionar documentos PDF protegidos por políticas. Inspecionar documentos PDF protegidos por política retorna informações sobre o documento PDF protegido por política. Você pode, por exemplo, determinar a política usada para proteger o documento e a data em que o documento foi protegido.

Não é possível executar essa tarefa se a versão do LiveCycle for 8.x ou anterior. O suporte para inspecionar documentos protegidos por políticas é adicionado no AEM Forms. Se você tentar inspecionar um documento protegido por uma política usando o LiveCycle 8.x (ou anterior), uma exceção será lançada.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para inspecionar um documento PDF protegido por uma política, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere um documento protegido por política para inspecionar.
1. Obtenha informações sobre o documento protegido por políticas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documento, crie um objeto cliente de serviço de Segurança de documento. Se estiver usando a API do Java, crie um objeto `RightsManagementClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `RightsManagementServiceService`.

**Recuperar um documento protegido por política para inspecionar**

Para inspecionar um documento protegido por política, recupere-o. Se você tentar inspecionar um documento que não está protegido com uma política ou que foi revogado, uma exceção será lançada.

**Inspect o documento**

Depois de recuperar um documento protegido por políticas, você pode inspecioná-lo.

**Obter informações sobre o documento protegido por políticas**

Após inspecionar um documento PDF protegido por políticas, você pode obter informações sobre ele. Por exemplo, você pode determinar a política usada para proteger o documento.

Se você proteger um documento com uma política que pertence a Minhas Políticas e, em seguida, chamar `RMInspectResult.getPolicysetName` ou `RMInspectResult.getPolicysetId`, null será retornado.

Se o documento estiver protegido usando uma política contida em um conjunto de políticas (diferente de Minhas Políticas), `RMInspectResult.getPolicysetName` e `RMInspectResult.getPolicysetId` retornará sequências de caracteres válidas.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Documentos PDF protegidos pela política Inspect usando a API Java {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect um documento PDF protegido por políticas usando a API do Serviço de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como o adobe-rights-management-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere um documento protegido por política para inspecionar.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF protegido por política usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Inspect o documento.

   * Crie um objeto `DocumentManager` chamando o método `RightsManagementClient` `getDocumentManager` do objeto.
   * Inspect o documento protegido por política, chamando o método `LicenseManager` do objeto `inspectDocument`. Passe o objeto `com.adobe.idp.Document` que contém o documento PDF protegido por política. Este método retorna um objeto `RMInspectResult` que contém informações sobre o documento protegido por política.

1. Obtenha informações sobre o documento protegido por políticas.

   Para obter informações sobre o documento protegido por política, chame o método apropriado que pertence ao objeto `RMInspectResult`. Por exemplo, para recuperar o nome da política, chame o método `RMInspectResult` do objeto `getPolicyName`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Como inspecionar documentos PDF protegidos por política usando a API Java&quot;

### Documentos PDF protegidos pela política do Inspect usando a API de serviço da Web {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect um documento PDF protegido por políticas usando a API do Serviço de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere um documento protegido por política para inspecionar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF a ser inspecionado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Inspect o documento.

   Inspect o documento protegido por política, chamando o método `RightsManagementServiceClient` do objeto `inspectDocument`. Passe o objeto `BLOB` que contém o documento PDF protegido por política. Este método retorna um objeto `RMInspectResult` que contém informações sobre o documento protegido por política.

1. Obtenha informações sobre o documento protegido por políticas.

   Para obter informações sobre o documento protegido por política, obtenha o valor do campo apropriado que pertence ao objeto `RMInspectResult`. Por exemplo, para recuperar o nome da política, obtenha o valor do campo `RMInspectResult` do objeto `policyName`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Como inspecionar documentos PDF protegidos por política usando a API de serviço da Web&quot;
* &quot;Início rápido (SwaRef): Como inspecionar documentos PDF protegidos por política usando a API de serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de marcas d&#39;água {#creating-watermarks}

As marcas d&#39;água ajudam a garantir a segurança de um documento, identificando-o exclusivamente e controlando a violação de direitos autorais. Por exemplo, você pode criar e colocar uma marca d&#39;água que declare Confidencial em todas as páginas de um documento. Depois que uma marca d&#39;água é criada, é possível incluí-la como parte de uma política. Ou seja, você pode definir o atributo de marca d&#39;água da política com a marca d&#39;água recém-criada. Depois que uma política que contém uma marca d&#39;água é aplicada a um documento, a marca d&#39;água aparece no documento protegido por política.

>[!NOTE]
>
>Somente usuários com privilégios administrativos de Segurança de documento podem criar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança de documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para criar uma marca d&#39;água, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Defina os atributos de marca d&#39;água.
1. Registre a marca d&#39;água no serviço de segurança de documentos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento. Se estiver usando a API do Java, crie um objeto `RightsManagementClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `RightsManagementServiceService`.

**Definir os atributos de marcas d&#39;água**

Para criar uma nova marca d&#39;água, você deve definir atributos de marca d&#39;água. O atributo name deve ser sempre definido. Além do atributo name, você deve definir pelo menos um dos seguintes atributos:

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
   <td><p>Se esse valor for true, o valor do texto personalizado deverá ser especificado usando <code>WaterBackCmd:SRCTEXT</code>.</p></td>
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
   <td><p>Se esse valor for especificado, <code>WaterBackCmd:IS_SIZE_ENABLED</code> deverá estar presente e o valor deverá ser verdadeiro. Se esse atributo não for especificado, o comportamento padrão se ajustará à página.</p></td>
   <td><p>Um valor superior a 0.0 e inferior ou igual a 1.0.</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>Especifica o alinhamento horizontal da marca d'água. O valor padrão é central.</p></td>
   <td><p>esquerda, central ou direita</p></td>
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
   <td><p>True se uma escala personalizada for especificada. Se este valor for verdadeiro, SCALE também deverá ser especificado. Se esse valor for falso, o padrão se ajusta à página.</p></td>
   <td><p>Verdadeiro ou Falso</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>Especifica o texto personalizado de uma marca d'água. Se esse valor estiver presente, <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> também deverá estar presente e definido como true.</p></td>
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

Uma nova marca d&#39;água deve ser registrada no serviço de segurança de documentos antes de poder ser usada. Depois de registrar uma marca d&#39;água, você pode usá-la nas políticas.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicação de políticas a documentos PDF](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Criar marcas d&#39;água usando a API Java {#create-watermarks-using-the-java-api}

Crie uma marca d&#39;água usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como `adobe-rightsmanagement-client.jar`, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir os atributos de marca d&#39;água

   * Crie um objeto `Watermark` chamando o método `InfomodelObjectFactory` estático `createWatermark` do objeto. Este método retorna um objeto `Watermark`.
   * Defina o atributo name da marca d&#39;água chamando o método `Watermark` do objeto `setName` e passando um valor de string que especifica o nome da política.
   * Defina o atributo de plano de fundo da marca d&#39;água chamando o método `Watermark` do objeto `setBackground` e transmitindo `true`. Ao definir esse atributo, a marca d&#39;água aparece no plano de fundo do documento.
   * Defina o atributo de texto personalizado da marca d&#39;água chamando o método `Watermark` do objeto `setCustomText` e passando um valor de string que representa o texto da marca d&#39;água.
   * Defina o atributo de opacidade da marca d&#39;água chamando o método `Watermark` do objeto `setOpacity` e passando um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

1. Registre a marca d&#39;água.

   * Crie um objeto `WatermarkManager` chamando o método `RightsManagementClient` `getWatermarkManager` do objeto. Este método retorna um objeto `WatermarkManager`.
   * Registre a marca d&#39;água chamando o método `WatermarkManager` do objeto `registerWatermark` e transmitindo o objeto `Watermark` que representa a marca d&#39;água a ser registrada. Esse método retorna um valor de string que representa o valor de identificação da marca d&#39;água.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (modo SOAP): Criar uma marca d&#39;água usando a API do Java&quot;

### Criar marcas d&#39;água usando a API do serviço da Web {#create-watermarks-using-the-web-service-api}

Crie uma marca d&#39;água usando a API de segurança de documentos (serviço da Web):

1. Crie um objeto da API do Cliente de segurança de documento.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Defina os atributos de marca d&#39;água.

   * Crie um objeto `WatermarkSpec` chamando o construtor `WatermarkSpec`.
   * Defina o nome da marca d&#39;água atribuindo um valor de string ao `WatermarkSpec` membro de dados `name` do objeto.
   * Defina o atributo `id` da marca d&#39;água atribuindo um valor de string ao `WatermarkSpec` membro de dados `id` do objeto.
   * Para cada propriedade de marca d&#39;água a ser definida, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` separado.
   * Defina o valor da chave atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` membro de dados `key` do objeto (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` membro de dados `value` do objeto (por exemplo, `.25`).
   * Crie um objeto `MyArrayOf_xsd_anyType`. Para cada objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`, chame o método `MyArrayOf_xsd_anyType` do objeto `Add`. Passe o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua o objeto `MyArrayOf_xsd_anyType` ao membro de dados `WatermarkSpec` do objeto `values`.

1. Registre a marca d&#39;água.

   Registre a marca d&#39;água chamando o método `RightsManagementServiceClient` do objeto `registerWatermark` e transmitindo o objeto `WatermarkSpec` que representa a marca d&#39;água a ser registrada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Criação de uma marca d&#39;água usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Criação de uma marca d&#39;água usando a API do serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificação de Marcas D&#39;Água {#modifying-watermarks}

Você pode modificar uma marca d&#39;água existente usando a API do Java de segurança de documento ou a API do serviço da Web. Para fazer alterações em uma marca d&#39;água existente, você a recupera, modifica seus atributos e a atualiza no servidor. Por exemplo, suponha que você recupere uma marca d&#39;água e modifique seu atributo de opacidade. Antes que a alteração entre em vigor, você deve atualizar a marca d&#39;água.

Quando você modifica uma marca d&#39;água, a alteração afeta documentos futuros que tenham a marca d&#39;água aplicada a eles. Ou seja, os documentos PDF existentes que contêm a marca d&#39;água não são afetados.

>[!NOTE]
>
>Somente usuários com privilégios administrativos de Segurança de documento podem modificar marcas d&#39;água. Ou seja, você deve especificar esse usuário ao definir as configurações de conexão necessárias para criar um objeto cliente do serviço de Segurança de documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-9}

Para modificar uma marca d&#39;água, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupere a marca d&#39;água para modificar.
1. Defina os atributos de marca d&#39;água.
1. Atualize a marca d&#39;água.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento. Se estiver usando a API do Java, crie um objeto `DocumentSecurityClient` . Se estiver usando a API do serviço da Web de Segurança de documento, crie um objeto `DocumentSecurityServiceService`.

**Recuperar a marca d&#39;água para modificar**

Para modificar uma marca d&#39;água, você deve recuperar uma marca d&#39;água existente. Você pode recuperar uma marca d&#39;água especificando seu nome ou especificando seu valor de identificador.

**Definir os atributos de marcas d&#39;água**

Para modificar uma marca d&#39;água existente, altere o valor de um ou mais atributos de marca d&#39;água. Ao atualizar programaticamente uma marca d&#39;água usando um serviço da Web, você deve definir todos os atributos que foram originalmente definidos, mesmo que o valor não seja alterado. Por exemplo, suponha que os seguintes atributos de marca d&#39;água estejam definidos: `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY` e `WaterBackCmd:SRCTEXT`. Embora o único atributo que você deseja modificar seja `WaterBackCmd:OPACITY`, você deve definir os outros valores corretamente.

>[!NOTE]
>
>Ao usar a API Java para modificar uma marca d&#39;água, não é necessário especificar todos os atributos. Defina o atributo de marca d&#39;água que deseja modificar.

>[!NOTE]
>
>Para obter informações sobre os nomes dos atributos de marca d&#39;água, consulte [Criação de Marcas d&#39;água](protecting-documents-policies.md#creating-watermarks).

**Atualizar a marca d&#39;água**

Depois de modificar os atributos de uma marca d&#39;água, atualize a marca d&#39;água.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Criação de marcas d&#39;água](protecting-documents-policies.md#creating-watermarks)

### Modifique marcas d&#39;água usando a API Java {#modify-watermarks-using-the-java-api}

Modifique uma marca d&#39;água usando a API de segurança de documentos (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como o adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere a marca d&#39;água para modificar.

   Crie um objeto `WatermarkManager` chamando o método `DocumentSecurityClient` do objeto e transmita um valor de string que especifica o nome da marca d&#39;água. `getWatermarkManager` Esse método retorna um objeto `Watermark` que representa a marca d&#39;água a ser modificada.

1. Defina os atributos de marca d&#39;água.

   Defina o atributo de opacidade da marca d&#39;água chamando o método `Watermark` do objeto `setOpacity` e passando um valor inteiro que especifica o nível de opacidade. Um valor de 100 indica que a marca d&#39;água é completamente opaca e um valor de 0 indica que a marca d&#39;água é completamente transparente.

   >[!NOTE]
   >
   >Este exemplo modifica somente o atributo de opacidade.

1. Atualize a marca d&#39;água.

   * Atualize a marca d&#39;água chamando o método `WatermarkManager` do objeto `updateWatermark` e passe o objeto `Watermark` cujo atributo foi modificado.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o Início rápido (modo SOAP): Modificação de uma marca d&#39;água usando a seção API do Java .

### Modifique marcas d&#39;água usando a API do serviço da Web {#modify-watermarks-using-the-web-service-api}

Modifique uma marca d&#39;água usando a API de segurança de documentos (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recupere a marca d&#39;água para modificar.

   Recupere a marca d&#39;água para modificar, chamando o método `DocumentSecurityServiceClient` do objeto `getWatermarkByName`. Passe um valor de string que especifica o nome da marca d&#39;água. Esse método retorna um objeto `WatermarkSpec` que representa a marca d&#39;água a ser modificada.

1. Defina os atributos de marca d&#39;água.

   * Para cada propriedade de marca d&#39;água a ser atualizada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` separado.
   * Defina o valor da chave atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` membro de dados `key` do objeto (por exemplo, `WaterBackCmd:OPACITY)`.
   * Defina o valor atribuindo um valor ao `MyMapOf_xsd_string_To_xsd_anyType_Item` membro de dados `value` do objeto (por exemplo, `.50`).
   * Crie um objeto `MyArrayOf_xsd_anyType`. Para cada objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`, chame o método `MyArrayOf_xsd_anyType` do objeto `Add`. Passe o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua o objeto `MyArrayOf_xsd_anyType` ao membro de dados `WatermarkSpec` do objeto `values`.

1. Atualize a marca d&#39;água.

   Atualize a marca d&#39;água chamando o método `DocumentSecurityServiceClient` do objeto `updateWatermark` e transmitindo o objeto `WatermarkSpec` que representa a marca d&#39;água a ser modificada.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): Modificação de uma marca d&#39;água usando a API do serviço da Web&quot;

## Pesquisar eventos {#searching-for-events}

O serviço Rights Management rastreia ações específicas à medida que ocorrem, como aplicar uma política a um documento, abrir um documento protegido por política e revogar o acesso a documentos. A auditoria de eventos deve ser ativada para o serviço Rights Management ou os eventos não são rastreados.

Os eventos são incluídos em uma das seguintes categorias:

* Os eventos de administrador são ações relacionadas a um administrador, como a criação de uma nova conta de administrador.
* Eventos de documento são ações relacionadas a um documento, como fechar um documento protegido por política.
* Eventos de política são ações relacionadas a uma política, como a criação de uma nova política.
* Os eventos de serviço são ações relacionadas ao serviço do Rights Management, como a sincronização com o diretório do usuário.

Você pode pesquisar por eventos específicos usando a API do Java do Rights Management ou a API do serviço da Web. Ao procurar por eventos, você pode executar tarefas, como criar um arquivo de log de determinados eventos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Rights Management, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-10}

Para procurar um evento Rights Management, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de API do cliente do Rights Management.
1. Especifique o evento para o qual pesquisar.
1. Procure o evento .

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Rights Management**

Antes de executar programaticamente uma operação de serviço Rights Management, é necessário criar um objeto de cliente de serviço Rights Management. Se estiver usando a API do Java, crie um objeto `DocumentSecurityClient` . Se estiver usando a API do serviço da Web do Rights Management , crie um objeto `DocumentSecurityServiceService` .

**Especifique os eventos que serão pesquisados**

Você deve especificar o evento a ser procurado. Por exemplo, você pode pesquisar o evento de criação de política, que ocorre quando uma nova política é criada.

**Pesquisar pelo evento**

Depois de especificar o evento que será pesquisado, você pode usar a API do Java do Rights Management ou a API do serviço da Web do Rights Management para pesquisar o evento.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Procure eventos usando a API do Java {#search-for-events-using-the-java-api}

Procure eventos usando a API do Rights Management (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Rights Management

   Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Especifique os eventos que serão pesquisados

   * Crie um objeto `EventManager` chamando o método `DocumentSecurityClient` `getEventManager` do objeto. Este método retorna um objeto `EventManager`.
   * Crie um objeto `EventSearchFilter` chamando seu construtor.
   * Especifique o evento para o qual pesquisar, chamando o método `EventSearchFilter` do objeto `setEventCode` e passando um membro de dados estáticos que pertence à classe `EventManager` que representa o evento para o qual pesquisar. Por exemplo, para procurar pelo evento de criação de política, passe `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >Você pode definir critérios de pesquisa adicionais chamando métodos de objeto `EventSearchFilter`. Por exemplo, chame o método `setUserName` para especificar um usuário associado ao evento.

1. Pesquisar pelo evento

   Procure o evento chamando o método `EventManager` do objeto `searchForEvents` e transmitindo o objeto `EventSearchFilter` que define os critérios de pesquisa do evento. Esse método retorna uma matriz de objetos `Event`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (SOAP): Pesquisar eventos usando a API do Java&quot;

### Procure eventos usando a API de serviço da Web {#search-for-events-using-the-web-service-api}

Procure eventos usando a API do Rights Management (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente do Rights Management

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Especifique os eventos que serão pesquisados

   * Crie um objeto `EventSpec` usando seu construtor.
   * Especifique o início do período de tempo durante o qual o evento ocorreu, definindo o membro de dados `EventSpec` do objeto `firstTime.date` com a instância `DataTime` que representa o início do intervalo de datas quando o evento ocorreu.
   * Atribua o valor `true` ao membro de dados `EventSpec` do objeto `firstTime.dateSpecified`.
   * Especifique o fim do período de tempo durante o qual o evento ocorreu, definindo o membro de dados `EventSpec` do objeto `lastTime.date` com a instância `DataTime` que representa o fim do intervalo de datas quando o evento ocorreu.
   * Atribua o valor `true` ao membro de dados `EventSpec` do objeto `lastTime.dateSpecified`.
   * Defina o evento para pesquisar atribuindo um valor de string ao `EventSpec` membro de dados `eventCode` do objeto. A tabela a seguir lista os valores numéricos que você pode atribuir a essa propriedade:

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

1. Pesquisar pelo evento

   Procure o evento chamando o método `DocumentSecurityServiceClient` do objeto `searchForEvents` e passando o objeto `EventSpec` que representa o evento para o qual pesquisar e o número máximo de resultados. Esse método retorna uma coleção `MyArrayOf_xsd_anyType` em que cada elemento é uma instância `AuditSpec`. Usando uma instância `AuditSpec`, você pode obter informações sobre o evento, como a hora em que ele ocorreu. A instância `AuditSpec` contém um membro de dados `timestamp` que especifica essas informações.

**Exemplos de código**

Para obter exemplos de código usando o serviço Rights Management, consulte os seguintes Inícios rápidos:

* &quot;Início rápido (MTOM): Procurar eventos usando a API do serviço da Web&quot;
* &quot;Início rápido (SwaRef): Procurar eventos usando a API do serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplicando Políticas a Documentos do Word {#applying-policies-to-word-documents}

Além de documentos PDF, o serviço Gerenciamento de Direitos oferece suporte a formatos de documento adicionais, como um documento do Microsoft Word (arquivo DOC) e outros formatos de arquivo do Microsoft Office. Por exemplo, você pode aplicar uma política a um documento do Word para protegê-lo. Ao aplicar uma política a um documento do Word, você restringe o acesso ao documento. Não é possível aplicar uma política a um documento se ele já estiver protegido por uma política.

Você pode monitorar o uso de um documento do Word protegido por política depois de distribuí-lo. Ou seja, você pode ver como o documento está sendo usado e quem o está usando. Por exemplo, você pode descobrir quando alguém abriu o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-11}

Para aplicar uma política a um documento do Word, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recupera um documento do Word ao qual uma política é aplicada.
1. Aplique uma política existente ao documento do Word.
1. Salve o documento do Word protegido por política.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente de segurança de documentos**

Antes de poder executar programaticamente uma operação de serviço de Segurança de Documento, é necessário criar um objeto de cliente do serviço de Segurança de Documento.

**Recuperar um documento do Word**

Você deve recuperar um documento do Word para aplicar uma política. Depois de aplicar uma política ao documento do Word, os usuários são restritos ao usar o documento. Por exemplo, se a política não habilitar a abertura do documento offline, os usuários deverão estar online para abrir o documento.

**Aplicar uma política existente ao documento do Word**

Para aplicar uma política a um documento do Word, é necessário referenciar uma política existente e especificar a qual conjunto de políticas a política pertence. O usuário que está definindo as propriedades de conexão deve ter acesso à política especificada. Caso contrário, ocorrerá uma exceção.

**Salvar o documento do Word**

Depois que o serviço de segurança de documento aplicar uma política a um documento do Word, você poderá salvar o documento do Word protegido por política como um arquivo DOC.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Revogando o acesso aos documentos](protecting-documents-policies.md#revoking-access-to-documents)

### Aplicar uma política a um documento do Word usando a API Java {#apply-a-policy-to-a-word-document-using-the-java-api}

Aplique uma política a um documento do Word usando a API de segurança de documento (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocumentSecurityClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar um documento do Word.

   * Crie um objeto `java.io.FileInputStream` que represente o documento do Word usando seu construtor e passando um valor de string que especifica o local do documento do Word.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Aplique uma política existente ao documento do Word.

   * Crie um objeto `DocumentManager` chamando o método `DocumentSecurityClient` `getDocumentManager` do objeto.
   * Aplique uma política ao documento do Word chamando o método `DocumentManager` do objeto e transmitindo os seguintes valores:`protectDocument`

      * O objeto `com.adobe.idp.Document` que contém o documento do Word ao qual a política é aplicada.
      * Um valor de string que especifica o nome do documento.
      * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um valor `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
      * Um valor de string que especifica o nome da política.
      * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor do parâmetro deve ser nulo).
      * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser `null` (se esse parâmetro for `null`, o valor de parâmetro anterior deverá ser `null`).
      * Um `com.adobe.livecycle.rightsmanagement.Locale` que representa a localidade usada para selecionar o modelo do MS Office. Esse valor de parâmetro é opcional e você pode especificar `null`.

      O método `protectDocument` retorna um objeto `RMSecureDocumentResult` que contém o documento do Word protegido por política.


1. Salve o documento do Word.

   * Chame o método `RMSecureDocumentResult` do objeto `getProtectedDoc` para obter o documento do Word protegido por política. Este método retorna um objeto `com.adobe.idp.Document`.
   * Crie um objeto `java.io.File` e verifique se a extensão de arquivo é DOC.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `getProtectedDoc`).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte Início rápido:

* &quot;Início rápido (modo SOAP): Aplicar uma política a um documento do Word usando a API do Java&quot;

### Aplicar uma política a um documento do Word usando a API do serviço da Web {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Aplique uma política a um documento do Word usando a API de segurança de documento (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto da API do Cliente de segurança de documento.

   * Crie um objeto `DocumentSecurityServiceClient` usando seu construtor padrão.
   * Crie um objeto `DocumentSecurityServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DocumentSecurityServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento do Word.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento do Word ao qual uma política é aplicada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Determine o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Aplique uma política existente ao documento do Word.

   Aplique uma política ao documento do Word chamando o método `DocumentSecurityServiceClient` do objeto e transmitindo os seguintes valores:`protectDocument`

   * O objeto `BLOB` que contém o documento do Word ao qual a política é aplicada.
   * Um valor de string que especifica o nome do documento.
   * Um valor de string que especifica o nome do conjunto de políticas ao qual a política pertence. Você pode especificar um valor `null` que resulta no conjunto de políticas `MyPolicies` sendo usado.
   * Um valor de string que especifica o nome da política.
   * Um valor de string que representa o nome do domínio do gerenciador de usuários do usuário que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o próximo valor do parâmetro deve ser `null`).
   * Um valor de string que representa o nome canônico do usuário do gerenciador de usuários que é o editor do documento. Esse valor de parâmetro é opcional e pode ser nulo (se esse parâmetro for nulo, o valor do parâmetro anterior deve ser `null`).
   * Um valor `RMLocale` que especifica o valor do local (por exemplo, `RMLocale.en`).
   * Um parâmetro de saída da string usado para armazenar o valor do identificador de política.
   * Um parâmetro de saída de string usado para armazenar o valor do identificador protegido por política.
   * Um parâmetro de saída de string usado para armazenar o tipo MIME (por exemplo, `application/doc`).

   O método `protectDocument` retorna um objeto `BLOB` que contém o documento do Word protegido por política.

1. Salve o documento do Word.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do Word protegido por política.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `protectDocument`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo do Word chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): Aplicar uma política a um documento do Word usando a API do serviço da Web&quot;

## Removendo Políticas de Documentos do Word {#removing-policies-from-word-documents}

Você pode remover uma política de um documento do Word protegido por política para remover a segurança do documento. Ou seja, se você não quiser mais que o documento seja protegido por uma política. Se você quiser atualizar um documento do Word protegido por política com uma política mais recente, em vez de remover a política e adicionar a política atualizada, é mais eficiente mudar a política.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de segurança de documentos, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-12}

Para remover uma política de um documento do Word protegido por política, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um objeto da API do Cliente de segurança de documento.
1. Recuperar um documento do Word protegido por política.
1. Remova a política do documento do Word.
1. Salve o documento do Word não seguro.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Cliente de segurança de documentos**

Antes de executar programaticamente uma operação de serviço de Segurança de documento, crie um objeto cliente de serviço de Segurança de documento.

**Recuperar um documento do Word protegido por política**

Você deve recuperar um documento do Word protegido por política para remover uma política. Se tentar remover uma política de um documento do Word que não está protegido por uma política, ocorrerá uma exceção.

**Remover a política do documento do Word**

Você pode remover uma política de um documento do Word protegido por política, desde que um administrador seja especificado nas configurações de conexão. Caso contrário, a política usada para proteger um documento deverá conter a permissão `SWITCH_POLICY` para remover uma política de um documento do Word. Além disso, o usuário especificado nas configurações de conexão do AEM Forms também deve ter essa permissão. Caso contrário, uma exceção será lançada.

**Salvar o documento do Word não seguro**

Depois que o serviço de segurança de documentos remove uma política de um documento do Word, você pode salvar o documento do Word não seguro como um arquivo DOC.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aplicando Políticas a Documentos do Word](protecting-documents-policies.md#applying-policies-to-word-documents)

### Remova uma política de um documento do Word usando a API Java {#remove-a-policy-from-a-word-document-using-the-java-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança de documentos (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-rights-management-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Cliente de segurança de documentos

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `RightsManagementClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar um documento do Word protegido por política

   * Crie um objeto `java.io.FileInputStream` que represente o documento do Word protegido por política usando seu construtor e transmitindo um valor de string que especifique o local do documento do Word.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remover a política do documento do Word

   * Crie um objeto `DocumentManager` chamando o método `RightsManagementClient` `getDocumentManager` do objeto.
   * Remova uma política do documento do Word chamando o método `DocumentManager` do objeto `removeSecurity` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento do Word protegido por política. Este método retorna um objeto `com.adobe.idp.Document` que contém um documento do Word não seguro.

1. Salvar o documento do Word não seguro

   * Crie um objeto `java.io.File` e verifique se a extensão de arquivo é DOC.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `removeSecurity`).

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte Início rápido:

* &quot;Início rápido (modo SOAP): Remover uma política de um documento do Word usando a API do Java&quot;

### Remover uma política de um documento do Word usando a API do serviço da Web {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Remova uma política de um documento do Word protegido por política usando a API de segurança de documentos (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do Cliente de segurança de documentos

   * Crie um objeto `RightsManagementServiceClient` usando seu construtor padrão.
   * Crie um objeto `RightsManagementServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `RightsManagementServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.


1. Recuperar um documento do Word protegido por política

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento do Word protegido por política do qual a política é removida.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do Word e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Remover a política do documento do Word

   Remova a política do documento do Word chamando o método `RightsManagementServiceClient` do objeto `removePolicySecurity` e transmitindo o objeto `BLOB` que contém o documento do Word protegido por política. Este método retorna um objeto `BLOB` que contém um documento do Word não seguro.

1. Salvar o documento do Word não seguro

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do Word não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `removePolicySecurity`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.

**Exemplos de código**

Para obter exemplos de código usando o serviço Segurança de documento, consulte o seguinte Início rápido:

* &quot;Início rápido (MTOM): Remover uma política de um documento do Word usando a API do serviço da Web&quot;

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
