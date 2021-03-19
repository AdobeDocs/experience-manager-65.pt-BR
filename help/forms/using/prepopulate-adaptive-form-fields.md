---
title: Preencher previamente campos de formulário adaptáveis
seo-title: Preencher previamente campos de formulário adaptáveis
description: Use dados existentes para preencher previamente campos de um formulário adaptável.
seo-description: Com formulários adaptáveis, os usuários podem preencher previamente as informações básicas em um formulário, fazendo logon com os perfis sociais. Este artigo descreve como você pode fazer isso.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 0%

---


# Preencher previamente campos de formulário adaptáveis{#prefill-adaptive-form-fields}

## Introdução {#introduction}

É possível preencher previamente os campos de um formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para preencher previamente os dados em um formulário adaptável, disponibilize os dados do usuário como um XML / JSON de preenchimento prévio no formato que adere à estrutura de dados de preenchimento prévio de formulários adaptáveis.

## Estrutura dos dados de preenchimento prévio {#the-prefill-structure}

Um formulário adaptável pode ter vários campos vinculados e não vinculados. Campos vinculados são campos que são arrastados a partir da guia Localizador de conteúdo e contêm valor de propriedade `bindRef` não vazio na caixa de diálogo de edição de campo. Campos não vinculados são arrastados diretamente do navegador de componentes do Sidekick e têm um valor `bindRef` vazio.

É possível preencher previamente os campos vinculados e não vinculados de um formulário adaptável. Os dados de preenchimento prévio contêm as seções afBoundData e afBoundData para preencher previamente os campos vinculados e não vinculados de um formulário adaptável. A seção `afBoundData` contém os dados de preenchimento prévio de campos e painéis vinculados. Esses dados devem ser compatíveis com o schema do modelo de formulário associado:

* Para formulários adaptáveis usando o [modelo de formulário XFA](../../forms/using/prepopulate-adaptive-form-fields.md), use o preenchimento prévio XML compatível com o schema de dados do modelo XFA.
* Para formulários adaptáveis usando [XML schema](#xml-schema-af), use o preenchimento prévio XML compatível com a estrutura do esquema XML.
* Para formulários adaptáveis usando [esquema JSON](#json-schema-based-adaptive-forms), use o preenchimento prévio JSON compatível com o esquema JSON.
* Para formulários adaptáveis usando o esquema FDM, use o esquema de preenchimento prévio JSON compatível com o esquema FDM.
* Para formulários adaptáveis com [nenhum modelo de formulário](#adaptive-form-with-no-form-model), não há dados vinculados. Cada campo é um campo não vinculado e é preenchido usando o XML não vinculado.

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

### Exemplo de estrutura JSON de pré-preenchimento {#sample-prefill-json-structure}

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

Para campos vinculados com o mesmo bindref ou campos não vinculados com o mesmo nome, os dados especificados na tag XML ou no objeto JSON são preenchidos em todos os campos. Por exemplo, dois campos em um formulário são mapeados para o nome `textbox` nos dados de preenchimento prévio. Durante o tempo de execução, se o primeiro campo da caixa de texto contiver &quot;A&quot;, o &quot;A&quot; será preenchido automaticamente na segunda caixa de texto. Esse vínculo é chamado de vínculo em tempo real de campos de formulário adaptáveis.

### Formulário adaptável usando o modelo de formulário XFA {#xfa-based-af}

A estrutura do XML de preenchimento prévio e do XML enviado para formulários adaptáveis baseados em XFA é a seguinte:

* **Preencher Estrutura** XML: O XML de preenchimento prévio para formulário adaptável baseado em XFA deve ser compatível com o schema de dados do template de formulário XFA. Para preencher previamente campos não vinculados, vincule a estrutura XML de preenchimento prévio na tag `/afData/afBoundData` .

* **Estrutura** XML enviada: Quando nenhum XML de preenchimento é usado, o XML enviado contém dados para os campos vinculados e não vinculados na tag  `afData` wrapper. Se um XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura do XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a tag raiz `afData`, o XML de saída também terá o mesmo formato. Se o XML de preenchimento prévio não tiver `afData/afBoundData`wrapper e, em vez disso, começar diretamente da tag raiz do esquema como `employeeData`, o XML enviado também começará com a tag `employeeData` .

Prefill-Submit-Data-ContentPackage.zip

[Obter ](assets/prefill-submit-data-contentpackage.zip)
FileSample contendo dados de preenchimento prévio e dados enviados

### Formulários adaptáveis baseados em esquema XML  {#xml-schema-af}

A estrutura do XML de preenchimento prévio e do XML enviado para formulários adaptáveis com base no esquema XML é a seguinte:

* **Preencher estrutura** XML previamente: O XML de preenchimento prévio deve ser compatível com o Esquema XML associado. Para preencher previamente campos não vinculados, vincule a estrutura XML de preenchimento prévio na tag /afData/afBoundData .
* **Estrutura** XML enviada: se nenhum XML de preenchimento prévio for usado, o XML enviado conterá dados para os campos vinculados e não vinculados na tag  `afData` wrapper. Se o XML de preenchimento prévio for usado, o XML enviado terá a mesma estrutura do XML de preenchimento prévio. Se o XML de preenchimento prévio começar com a tag raiz `afData`, o XML de saída terá o mesmo formato. Se o XML de preenchimento prévio não tiver o wrapper `afData/afBoundData` e, em vez disso, começar diretamente da tag raiz do schema, como `employeeData`, o XML enviado também começará com a tag `employeeData`.

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

Para campos cujo modelo é esquema XML, os dados são preenchidos previamente na tag `afBoundData` , como mostrado na amostra de XML abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados.

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
>É recomendável não usar campos não vinculados em painéis vinculados (painéis com `bindRef` não vazio que foi criado ao arrastar componentes do Sidekick ou da guia Fontes de dados). Pode causar perda de dados desses campos não vinculados. Além disso, é recomendável que os nomes dos campos sejam exclusivos no formulário, especialmente para campos não vinculados.

#### Um exemplo sem o wrapper afData e afBoundData {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Formulários adaptáveis baseados em esquema JSON {#json-schema-based-adaptive-forms}

Para formulários adaptáveis com base no esquema JSON, a estrutura do JSON de preenchimento prévio e do JSON enviado é descrita abaixo. Para obter mais informações, consulte [Criação de formulários adaptáveis usando o esquema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Preencher estrutura** JSON previamente: O JSON de preenchimento prévio deve ser compatível com o Esquema JSON associado. Como opção, ele pode ser incluído no objeto /afData/afBoundData se você quiser preencher previamente campos não vinculados também.
* **Estrutura** JSON enviada: se nenhum JSON de preenchimento prévio for usado, o JSON enviado conterá dados para os campos vinculados e não vinculados na tag do wrapper afData. Se o JSON de preenchimento prévio for usado, o JSON enviado terá a mesma estrutura do JSON de preenchimento prévio. Se o JSON de preenchimento prévio começar com o objeto raiz afData, o JSON de saída terá o mesmo formato. Se o JSON de preenchimento prévio não tiver o wrapper afData/afBoundData e, em vez disso, começar diretamente do objeto raiz do esquema, como o usuário, o JSON enviado também inicia com o objeto do usuário.

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

Para campos que usam o modelo de esquema JSON, os dados são pré-preenchidos no objeto afBoundData , como mostrado na amostra JSON abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados. Abaixo está um exemplo de dados com `afData/afBoundData` wrapper:

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

Abaixo está um exemplo sem `afData/afBoundData` wrapper:

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
>Usar campos não vinculados em painéis vinculados (painéis com bindRef não vazio que foram criados ao arrastar componentes do Sidekick ou guia Fontes de dados) é **não** recomendado, pois pode causar perda de dados dos campos não vinculados. É recomendável ter nomes de campo exclusivos no formulário, especialmente para campos não vinculados.

### Formulário adaptável sem modelo de formulário {#adaptive-form-with-no-form-model}

Para formulários adaptáveis sem modelo de formulário, os dados para todos os campos estão sob a tag `<data>` de `<afUnboundData> tag`.

Além disso, tome nota do seguinte:

As tags XML para os dados do usuário enviados para vários campos são geradas usando o nome dos campos. Portanto, os nomes de campo devem ser exclusivos.

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

## Configuração do serviço de preenchimento prévio usando o Gerenciador de configuração {#configuring-prefill-service-using-configuration-manager}

Para ativar o serviço de preenchimento prévio, especifique a Configuração do serviço de preenchimento prévio padrão na Configuração do console da Web AEM. Use as seguintes etapas para configurar o serviço de Preenchimento prévio:

>[!NOTE]
>
>A Configuração do serviço de preenchimento prévio é aplicável a formulários adaptáveis, formulários HTML5 e conjuntos de formulários HTML5.

1. Abra **[!UICONTROL Configuração do Console Web do Adobe Experience Manager]** usando o URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. Pesquise e abra **[!UICONTROL Configuração Padrão do Serviço de Preenchimento]**.

   ![Preencher configuração](assets/prefill_config_new.png)

1. Insira o local dos dados ou um regex (expressão regular) para os **Data files locations**. Exemplos de locais de arquivos de dados válidos são:

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >Por padrão, o preenchimento prévio é permitido por meio de arquivos crx para todos os tipos de Adaptive Forms (XSD, XDP, JSON, FDM e sem base no Modelo de formulário). O preenchimento prévio é permitido somente com arquivos JSON e XML.

1. O serviço de preenchimento prévio agora está configurado para seu formulário.

   >[!NOTE]
   >
   >O protocolo crx cuida da segurança de dados pré-preenchidos e, portanto, é permitido por padrão. Preencher via outros protocolos usando regex genérico pode causar vulnerabilidade. Na configuração, especifique uma configuração de URL segura para proteger seus dados.

## O caso curioso de painéis repetíveis {#the-curious-case-of-repeatable-panels}

Geralmente, campos vinculados (esquema de formulário) e não vinculados são criados no mesmo formulário adaptável, mas as exceções a seguir caso o vínculo seja repetível:

* Painéis repetitivos não vinculados não são compatíveis com formulários adaptáveis usando o modelo de formulário XFA, XSD, esquema JSON ou esquema FDM.
* Não use campos não vinculados em painéis repetitivos vinculados.

>[!NOTE]
>
>Como regra geral, não misture campos vinculados e não vinculados se eles forem cruzados em dados preenchidos pelo usuário final em campos não vinculados. Se possível, você deve modificar o esquema ou o modelo de formulário XFA e adicionar uma entrada para campos não vinculados, de modo que também se torne vinculada e seus dados estejam disponíveis como outros campos em dados enviados.

## Protocolos compatíveis para o preenchimento prévio de dados do usuário {#supported-protocols-for-prefilling-user-data}

Os formulários adaptáveis podem ser preenchidos com dados do usuário no formato de dados de preenchimento prévio por meio dos seguintes protocolos quando configurados com regex válido:

### O protocolo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

O nó especificado deve ter uma propriedade chamada `jcr:data` e manter os dados.

### O protocolo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

O arquivo de referência deve estar no mesmo servidor.

### O protocolo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### O protocolo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME refere-se ao nome do serviço de preenchimento prévio OSGI. Consulte [Criar e executar um serviço de preenchimento prévio](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER refere-se a quaisquer metadados exigidos pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador para o usuário conectado é um exemplo de metadados que podem ser usados.

>[!NOTE]
>
>Não há suporte para transmitir parâmetros de autenticação.

### Configuração do atributo de dados no slingRequest {#setting-data-attribute-in-slingrequest}

Você também pode definir o atributo `data` em `slingRequest`, onde o atributo `data` é uma string contendo XML ou JSON, conforme mostrado no código de amostra abaixo (Exemplo é para XML):

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

Você pode gravar uma string XML ou JSON simples contendo todos os seus dados e configurá-la em slingRequest. Isso pode ser feito facilmente no JSP do renderizador para qualquer componente, que você deseja incluir na página, onde é possível definir o atributo de dados slingRequest .

Por exemplo, onde você deseja um design específico para a página com um tipo específico de cabeçalho. Para fazer isso, você pode escrever seu próprio `header.jsp`, que pode ser incluído no componente da página e definir o atributo `data`.

Outro bom exemplo é um caso de uso em que você gostaria de preencher previamente os dados de logon por meio de contas sociais, como Facebook, Twitter ou LinkedIn. Nesse caso, você pode incluir um JSP simples em `header.jsp`, que obtém dados da conta do usuário e define o parâmetro de dados.

prefill-page component.zip

[Obter ](assets/prefill-page-component.zip)
FileSample prefill.jsp no componente de página

## Serviço de preenchimento prévio personalizado do AEM Forms {#aem-forms-custom-prefill-service}

Você pode usar o serviço de preenchimento prévio personalizado para os cenários, onde os dados de uma fonte predefinida são constantemente lidos. O serviço de preenchimento prévio lê dados de fontes de dados definidas e preenche os campos do formulário adaptável com o conteúdo do arquivo de dados de preenchimento prévio. Também ajuda a associar permanentemente os dados pré-preenchidos a um formulário adaptável.

### Criar e executar um serviço de preenchimento prévio {#create-and-run-a-prefill-service}

O serviço de pré-preenchimento é um serviço OSGi e é empacotado por meio do pacote OSGi. Crie o pacote OSGi, faça upload e instale-o nos pacotes do AEM Forms. Antes de começar a criar o pacote:

* [Baixar o SDK do cliente da AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)
* Baixe o pacote estereotipado

* Coloque o arquivo de dados (dados de preenchimento prévio) no repositório crx. Você pode colocar o arquivo em qualquer local na pasta \content do crx-repository.

[Obter arquivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Criar um serviço de preenchimento prévio {#create-a-prefill-service}

O pacote estereotipado (pacote de serviço de preenchimento prévio de exemplo) contém a implementação de amostra do serviço de preenchimento prévio da AEM Forms. Abra o pacote estereotipado em um editor de código. Por exemplo, abra o projeto estereotipado no Eclipse para edição. Depois de abrir o pacote estereotipado em um editor de código, execute as seguintes etapas para criar o serviço.

1. Abra o arquivo src\main\java\com\adobe\test\Prefill.java para edição.
1. No código, defina o valor de:

   * `nodePath:` A variável do caminho do nó que aponta para o local do repositório crx contém o caminho do arquivo de dados (preenchimento prévio). Por exemplo, /content/prefilldata.xml
   * `label:` O parâmetro label especifica o nome de exibição do serviço. Por exemplo, Serviço de preenchimento prévio padrão

1. Salve e feche o arquivo `Prefill.java`.
1. Adicione o pacote `AEM Forms Client SDK` ao caminho de compilação do projeto estereotipado.
1. Compile o projeto e crie o .jar para o pacote.

#### Iniciar e usar o serviço de preenchimento prévio {#start-and-use-the-prefill-service}

Para iniciar o serviço de pré-preenchimento, carregue o arquivo JAR no Console da Web do AEM Forms e ative o serviço. Agora, o serviço começa a aparecer no editor de formulários adaptáveis. Para associar um serviço de preenchimento prévio a um formulário adaptável:

1. Abra o formulário adaptável no Editor do Forms e abra o painel Propriedades do Contêiner de formulário.
1. No console Propriedades, navegue até AEM Forms container > Básico > Preencher serviço.
1. Selecione o Serviço de preenchimento prévio padrão e clique em **[!UICONTROL Salvar]**. O serviço está associado ao formulário.

## Preencher dados no cliente {#prefill-at-client}

Ao preencher previamente um formulário adaptável, o servidor AEM Forms mescla os dados com um formulário adaptável e fornece o formulário preenchido a você. Por padrão, a ação de mesclagem de dados ocorre no servidor.

Você pode configurar o servidor do AEM Forms para executar a ação de mesclagem de dados no cliente, em vez do servidor. Reduz significativamente o tempo necessário para preencher e renderizar formulários adaptáveis. Por padrão, o recurso está desativado. Você pode habilitá-lo no Configuration Manager ou na linha de comando.

* Para ativar ou desativar do gerenciador de configuração:
   1. Abra AEM Configuration Manager.
   1. Localize e abra a Configuração do canal Web Adaptive Form e Interative Communication
   1. Habilite a opção Configuration.af.clientside.datamerge.enabled.name
* Para ativar ou desativar a partir da linha de comando:
   * Para ativar, execute o seguinte comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Para desativar, execute o seguinte comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   Para aproveitar ao máximo a opção de pré-preenchimento de dados no cliente, atualize o serviço de pré-preenchimento para retornar [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) e [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)