---
title: Preencher previamente campos de formulário adaptável
description: Use dados existentes para preencher previamente os campos de um formulário adaptável.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
exl-id: 29cbc330-7b3d-457e-ba4a-7ce6091f3836
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 0%

---

# Preencher previamente campos de formulário adaptável{#prefill-adaptive-form-fields}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/prepopulate-adaptive-form-fields.html) |
| AEM 6.5 | Este artigo |

## Introdução {#introduction}

É possível preencher previamente os campos de um formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para preencher previamente os dados em um formulário adaptável, disponibilize os dados do usuário como um XML/JSON de preenchimento prévio no formato que segue a estrutura de dados de formulários adaptáveis de preenchimento prévio.

## Estrutura dos dados de preenchimento prévio {#the-prefill-structure}

Um formulário adaptável pode ter uma combinação de campos vinculados e não vinculados. Os campos associados são campos que são arrastados da guia Localizador de conteúdo e contêm o valor da propriedade `bindRef` não vazio na caixa de diálogo de edição de campo. Os campos não vinculados são arrastados diretamente do navegador de componentes do Sidekick e têm um valor `bindRef` vazio.

É possível preencher previamente os campos vinculados e não vinculados de um formulário adaptável. Os dados de pré-preenchimento contêm as seções afBoundData e afUnBoundData para preencher previamente os campos ligados e não vinculados de um formulário adaptável. A seção `afBoundData` contém os dados de preenchimento prévio para campos e painéis associados. Esses dados devem ser compatíveis com o schema do modelo de formulário associado:

* Para formulários adaptáveis usando o [modelo de formulário XFA](../../forms/using/prepopulate-adaptive-form-fields.md), use o XML de preenchimento prévio compatível com o esquema de dados do modelo XFA.
* Para formulários adaptáveis usando o [esquema XML](#xml-schema-af), use o XML de preenchimento prévio compatível com a estrutura do esquema XML.
* Para formulários adaptáveis que usam o [esquema JSON](#json-schema-based-adaptive-forms), use o JSON de preenchimento prévio compatível com o esquema JSON.
* Para formulários adaptáveis que usam o esquema do FDM, use o preenchimento prévio de JSON compatível com o esquema do FDM.
* Para formulários adaptáveis com [nenhum modelo de formulário](#adaptive-form-with-no-form-model), não há dados associados. Cada campo é um campo não vinculado e é pré-preenchido usando o XML não vinculado.

### Exemplo de estrutura XML de preenchimento prévio {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### Exemplo de estrutura JSON de preenchimento prévio {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Para campos vinculados com o mesmo vínculo ou campos não vinculados com o mesmo nome, os dados especificados na tag XML ou no objeto JSON são preenchidos em todos os campos. Por exemplo, dois campos em um formulário são mapeados para o nome `textbox` nos dados de preenchimento prévio. Durante o tempo de execução, se o primeiro campo da caixa de texto contiver &quot;A&quot;, então &quot;A&quot; será automaticamente preenchido na segunda caixa de texto. Esse vínculo é chamado de vínculo ao vivo de campos de formulário adaptáveis.

### Formulário adaptável usando modelo de formulário XFA {#xfa-based-af}

A estrutura do XML pré-preenchido e do XML enviado para formulários adaptáveis baseados em XFA é a seguinte:

* **Estrutura XML de Preenchimento Prévio**: o XML de preenchimento prévio para o formulário adaptável baseado em XFA deve ser compatível com o esquema de dados do modelo de formulário XFA. Para preencher previamente campos não associados, envolva a estrutura XML de preenchimento prévio na marca `/afData/afBoundData`.

* **Estrutura XML Enviada**: quando nenhum XML de preenchimento prévio é usado, o XML enviado contém dados para campos associados e não associados na marca wrapper `afData`. Se um XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura que o XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a marca raiz `afData`, o XML de saída também terá o mesmo formato. Se o XML de preenchimento prévio não tiver `afData/afBoundData`wrapper e, em vez disso, iniciar diretamente da marca raiz do esquema como `employeeData`, o XML enviado também iniciará com a marca `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Obter arquivo](assets/prefill-submit-data-contentpackage.zip)
Amostra contendo dados de preenchimento prévio e dados enviados

### Formulários adaptáveis baseados em esquema XML  {#xml-schema-af}

A estrutura do XML pré-preenchido e do XML enviado para formulários adaptáveis com base no esquema XML é a seguinte:

* **Estrutura XML de preenchimento prévio**: o XML de preenchimento prévio deve ser compatível com o Esquema XML associado. Para preencher previamente os campos não vinculados, coloque a estrutura XML de preenchimento previamente na tag /afData/afBoundData.
* **Estrutura XML enviada**: se nenhum XML de preenchimento prévio for usado, o XML enviado conterá dados para campos associados e não associados na marca wrapper `afData`. Se o XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura do XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a marca raiz `afData`, o XML de saída terá o mesmo formato. Se o XML de preenchimento prévio não tiver o invólucro `afData/afBoundData` e, em vez disso, iniciar diretamente da marca raiz do esquema como `employeeData`, o XML enviado também iniciará com a marca `employeeData`.

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Para campos cujo modelo é um esquema XML, os dados são pré-preenchidos na marca `afBoundData`, como mostrado na amostra XML abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>É recomendável não usar campos não vinculados em painéis vinculados (painéis com o `bindRef` não vazio que foi criado ao arrastar componentes da guia Sidekick ou Fontes de dados). Isso pode causar perda de dados desses campos não vinculados. Além disso, é recomendável que os nomes dos campos sejam exclusivos em todo o formulário, especialmente para campos não vinculados.

#### Um exemplo sem afData e afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Formulários adaptáveis baseados em esquema JSON {#json-schema-based-adaptive-forms}

Para formulários adaptáveis com base no esquema JSON, a estrutura do JSON de preenchimento prévio e do JSON enviado é descrita abaixo. Para obter mais informações, consulte [Criação de formulários adaptáveis usando o esquema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Preencher previamente a estrutura JSON**: o JSON de preenchimento prévio deve ser compatível com o Esquema JSON associado. Opcionalmente, ele pode ser encapsulado no objeto /afData/afBoundData se você também quiser preencher previamente os campos não vinculados.
* **Estrutura JSON enviada**: se nenhum JSON de preenchimento prévio for usado, o JSON enviado conterá dados para campos ligados e não ligados na marca afData wrapper. Se o JSON de preenchimento prévio for usado, o JSON enviado terá a mesma estrutura que o JSON de preenchimento prévio. Se o JSON de preenchimento prévio começar com o objeto raiz afData, o JSON de saída terá o mesmo formato. Se o JSON de preenchimento prévio não tiver o invólucro afData/afBoundData e, em vez disso, iniciar diretamente a partir do objeto raiz do esquema, como o usuário, o JSON enviado também começará com o objeto do usuário.

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

Para campos que usam o modelo de esquema JSON, os dados são pré-preenchidos no objeto afBoundData, como mostrado na amostra JSON abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados. Veja abaixo um exemplo de dados com o wrapper `afData/afBoundData`:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Veja abaixo um exemplo sem o `afData/afBoundData` wrapper:

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>O uso de campos não vinculados em painéis vinculados (painéis com bindRef não vazios que foram criados ao arrastar componentes da guia Sidekick ou Fontes de dados) é **não** recomendado, pois pode causar perda de dados dos campos não vinculados. É recomendável ter nomes de campo exclusivos em todo o formulário, especialmente para campos não vinculados.

### Formulário adaptável sem modelo de formulário {#adaptive-form-with-no-form-model}

Para formulários adaptáveis sem modelo de formulário, os dados de todos os campos estão sob a marca `<data>` de `<afUnboundData> tag`.

Além disso, tome nota do seguinte:

As tags XML para os dados do usuário enviados para vários campos são geradas usando o nome dos campos. Portanto, os nomes dos campos devem ser exclusivos.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuração do serviço de preenchimento prévio usando o Gerenciador de configurações {#configuring-prefill-service-using-configuration-manager}

Para ativar o serviço de preenchimento prévio, especifique a Configuração do serviço de preenchimento prévio padrão na Configuração do console da Web AEM. Use as seguintes etapas para configurar o serviço de Preenchimento prévio:

>[!NOTE]
>
>A Configuração do serviço de preenchimento prévio é aplicável para formulários adaptáveis, formulários de HTML5 e conjuntos de formulários de HTML5.

1. Abra a **[!UICONTROL Configuração do Console da Web do Adobe Experience Manager]** usando a URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. Pesquise e abra **[!UICONTROL Configuração do Serviço de Preenchimento Prévio Padrão]**.

   ![Configuração de preenchimento prévio](assets/prefill_config_new.png)

1. Insira o local dos dados ou um regex (expressão regular) para os **locais dos arquivos de dados**. Exemplos de locais válidos de arquivos de dados são:

   * file:///C:/Users/public/Document/Prefill/.&#42;
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >Por padrão, o preenchimento prévio é permitido por meio de arquivos crx para todos os tipos de Forms adaptável (XSD, XDP, JSON, FDM e sem modelo de formulário baseado). O preenchimento prévio é permitido somente com arquivos JSON e XML.

1. O serviço de preenchimento prévio agora está configurado para o formulário.

   >[!NOTE]
   >
   >O protocolo crx cuida da segurança de dados pré-preenchida e, portanto, é permitido por padrão. O preenchimento prévio por meio de outros protocolos usando regex genérico pode causar vulnerabilidade. Na configuração do, especifique uma configuração de URL segura para proteger seus dados.

## O caso curioso de painéis repetíveis {#the-curious-case-of-repeatable-panels}

Geralmente, os campos vinculados (esquema de formulário) e não vinculados são criados no mesmo formulário adaptável, mas as exceções a seguir são algumas caso os campos vinculados sejam repetíveis:

* Os painéis repetíveis não vinculados não são compatíveis com formulários adaptáveis usando o modelo de formulário XFA, XSD, esquema JSON ou esquema FDM.
* Não use campos não vinculados em painéis repetíveis vinculados.

>[!NOTE]
>
>Como regra geral, não misture campos vinculados e não vinculados se eles forem cruzados em dados preenchidos pelo usuário final em campos desvinculados. Se possível, você deve modificar o esquema ou o modelo de formulário XFA e adicionar uma entrada para campos não vinculados, para que também se torne vinculado e seus dados estejam disponíveis como outros campos nos dados enviados.

## Protocolos compatíveis com o preenchimento prévio de dados do usuário {#supported-protocols-for-prefilling-user-data}

Os formulários adaptáveis podem ser pré-preenchidos com dados do usuário no formato de dados de preenchimento prévio por meio dos seguintes protocolos quando configurados com regex válido:

### O protocolo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

O nó especificado deve ter uma propriedade chamada `jcr:data` e conter os dados.

### O protocolo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

O arquivo referenciado deve estar no mesmo servidor.

### O protocolo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### O protocolo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME refere-se ao nome do serviço de preenchimento prévio OSGI. Consulte [Criar e executar um serviço de preenchimento prévio](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER refere-se a quaisquer metadados necessários pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador para o usuário conectado é um exemplo de metadados que podem ser usados.

>[!NOTE]
>
>Não há suporte para a transmissão de parâmetros de autenticação.

### Definição do atributo de dados em slingRequest {#setting-data-attribute-in-slingrequest}

Você também pode definir o atributo `data` em `slingRequest`, onde o atributo `data` é uma cadeia de caracteres que contém XML ou JSON, conforme mostrado no código de exemplo abaixo (O exemplo é para XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Você pode gravar uma sequência XML ou JSON simples contendo todos os seus dados e defini-la em slingRequest. Isso pode ser feito facilmente no JSP do renderizador para qualquer componente, que você deseja incluir na página, onde é possível definir o atributo de dados slingRequest.

Por exemplo, quando você deseja um design específico para a página com um tipo específico de cabeçalho. Para isso, você pode escrever seu próprio `header.jsp`, que pode ser incluído no componente de página e definir o atributo `data`.

Outro bom exemplo é um caso de uso em que você deseja preencher previamente os dados ao fazer logon por meio de contas sociais como Facebook, Twitter ou LinkedIn. Nesse caso, você pode incluir um JSP simples em `header.jsp`, que busca dados da conta de usuário e define o parâmetro de dados.

prefill-page component.zip

[Obter arquivo](assets/prefill-page-component.zip)
Amostra de prefill.jsp no componente Página

## Serviço de preenchimento prévio personalizado do AEM Forms {#aem-forms-custom-prefill-service}

Você pode usar o serviço de preenchimento prévio personalizado para os cenários, em que lê constantemente os dados de uma fonte predefinida. O serviço de preenchimento prévio lê os dados de fontes de dados definidas e preenche os campos do formulário adaptável com o conteúdo do arquivo de dados de preenchimento prévio. Também ajuda a associar permanentemente os dados pré-preenchidos a um formulário adaptável.

### Criar e executar um serviço de preenchimento prévio {#create-and-run-a-prefill-service}

O serviço de pré-preenchimento é um serviço OSGi e é empacotado por meio do pacote OSGi. Crie o pacote OSGi, faça upload e instale-o nos pacotes do AEM Forms. Antes de começar a criar o pacote:

* [Baixar o AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
* Baixar o pacote padrão

* Coloque o arquivo de dados (dados de preenchimento prévio) no repositório crx. Você pode colocar o arquivo em qualquer local na pasta \contents do repositório crx.

[Obter arquivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Criar um serviço de preenchimento {#create-a-prefill-service}

O pacote padrão (pacote de serviço de preenchimento de amostra) contém uma implementação de amostra do serviço de preenchimento prévio do AEM Forms. Abra o pacote padrão em um editor de código. Por exemplo, abra o projeto padronizado no Eclipse para edição. Depois de abrir o pacote padrão em um editor de código, execute as etapas a seguir para criar o serviço.

1. Abra o arquivo src\main\java\com\adobe\test\Prefill.java para edição.
1. No código, defina o valor de:

   * `nodePath:` A variável de caminho de nó que aponta para o local do repositório crx contém o caminho do arquivo de dados (preenchimento prévio). Por exemplo, /content/prefilldata.xml
   * `label:` O parâmetro de rótulo especifica o nome de exibição do serviço. Por exemplo, Serviço de preenchimento prévio padrão

1. Salvar e fechar o arquivo `Prefill.java`.
1. Adicione o pacote `AEM Forms Client SDK` ao caminho de compilação do projeto padrão.
1. Compile o projeto e crie o .jar para o pacote.

#### Iniciar e usar o serviço de preenchimento prévio {#start-and-use-the-prefill-service}

Para iniciar o serviço de preenchimento prévio, faça upload do arquivo JAR para o Console da Web do AEM Forms e ative o serviço. Agora, o serviço começa a aparecer no editor de formulários adaptáveis. Para associar um serviço de preenchimento prévio a um formulário adaptável:

1. Abra o formulário adaptável no Editor de Forms e abra o painel Propriedades do Contêiner de formulário.
1. No console Propriedades, navegue até Contêiner do AEM Forms > Básico > Serviço de preenchimento prévio.
1. Selecione o Serviço de preenchimento prévio padrão e clique em **[!UICONTROL Salvar]**. O serviço está associado ao formulário.

## Preencher dados previamente no cliente {#prefill-at-client}

Ao preencher previamente um formulário adaptável, o servidor do AEM Forms mescla os dados com um formulário adaptável e entrega o formulário preenchido a você. Por padrão, a ação de mesclagem de dados ocorre no servidor.

Você pode configurar o servidor do AEM Forms para executar a ação de mesclagem de dados no cliente em vez do servidor. Ele reduz bastante o tempo necessário para preencher previamente e renderizar formulários adaptáveis. Por padrão, o recurso está desativado. Você pode habilitá-lo no Gerenciador de configurações ou na linha de comando.

* Para ativar ou desativar o no gerenciador de configurações:
   1. Abra o Gerenciador de configuração do AEM.
   1. Localize e abra o formulário adaptável e a configuração do canal da Web de comunicação interativa
   1. Habilitar a opção Configuration.af.clientside.datamerge.enabled.name
* Para ativar ou desativar o na linha de comando:
   * Para habilitar, execute o seguinte comando cURL:
     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Para desativar, execute o seguinte comando cURL:
     `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  Para aproveitar ao máximo os dados pré-preenchidos na opção do cliente, atualize o serviço de preenchimento para retornar [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) e [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)
