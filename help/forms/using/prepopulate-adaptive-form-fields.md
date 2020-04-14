---
title: Preencher previamente campos de formulário adaptáveis
seo-title: Preencher previamente campos de formulário adaptáveis
description: Use dados existentes para preencher previamente campos de um formulário adaptável.
seo-description: Com formulários adaptáveis, os usuários podem preencher previamente as informações básicas em um formulário fazendo logon com seus perfis sociais. Este artigo descreve como você pode fazer isso.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Preencher previamente campos de formulário adaptáveis{#prefill-adaptive-form-fields}

## Introdução {#introduction}

É possível pré-preencher os campos de um formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. Para preencher previamente os dados em um formulário adaptável, disponibilize os dados do usuário como um XML / JSON de preenchimento prévio no formato que adere à estrutura de dados de preenchimento prévio de formulários adaptáveis.

## Estrutura dos dados de preenchimento prévio {#the-prefill-structure}

Um formulário adaptável pode ter vários campos vinculados e não vinculados. Campos vinculados são campos que são arrastados da guia Localizador de conteúdo e contêm valor de `bindRef` propriedade não vazio na caixa de diálogo de edição de campo. Campos não vinculados são arrastados diretamente do navegador de componentes do Sidekick e têm um `bindRef` valor vazio.

É possível pré-preencher os campos vinculados e não vinculados de um formulário adaptável. Os dados de preenchimento prévio contêm as seções afBoundData e afUnBoundData para preencher previamente os campos vinculados e não vinculados de um formulário adaptável. A `afBoundData` seção contém os dados de preenchimento prévio para campos e painéis vinculados. Esses dados devem ser compatíveis com o schema de modelo de formulário associado:

* Para formulários adaptáveis que usam o modelo [de formulário](../../forms/using/prepopulate-adaptive-form-fields.md)XFA, use o XML de preenchimento prévio compatível com o schema de dados do modelo XFA.
* Para formulários adaptáveis usando o schema [](#xml-schema-af)XML, use o XML de preenchimento prévio compatível com a estrutura do schema XML.
* Para formulários adaptáveis usando o schema [](#json-schema-based-adaptive-forms)JSON, use o JSON pré-preenchido compatível com o schema JSON.
* Para formulários adaptáveis que usam o schema FDM, use o schema JSON pré-preenchido com o  FDM.
* Para formulários adaptáveis [sem modelo](#adaptive-form-with-no-form-model)de formulário, não há dados vinculados. Cada campo é um campo não vinculado e é pré-preenchido usando o XML não vinculado.

### Exemplo de estrutura XML de pré-preenchimento {#sample-prefill-xml-structure}

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

```
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

Para campos vinculados com o mesmo código de barras ou campos não vinculados com o mesmo nome, os dados especificados na tag XML ou no objeto JSON são preenchidos em todos os campos. Por exemplo, dois campos em um formulário são mapeados para o nome `textbox` nos dados de preenchimento prévio. Durante o tempo de execução, se o primeiro campo da caixa de texto contiver &quot;A&quot;, &quot;A&quot; será automaticamente preenchido na segunda caixa de texto. Essa vinculação é chamada de vinculação ao vivo de campos de formulário adaptáveis.

### Formulário adaptável usando modelo de formulário XFA {#xfa-based-af}

A estrutura do XML de pré-preenchimento e do XML enviado para formulários adaptativos baseados em XFA é a seguinte:

* **Preencher estrutura** XML: O formulário adaptativo com base em XFA deve ser compatível com o schema de dados do modelo de formulário XFA. Para preencher previamente campos não vinculados, vincule a estrutura XML de preenchimento anterior à `/afData/afBoundData` tag .

* **Estrutura** XML enviada: Quando nenhum XML de preenchimento prévio é usado, o XML enviado contém dados para os campos vinculados e não vinculados na tag `afData` wrapper. Se um XML de pré-preenchimento for usado, o XML submetido terá a mesma estrutura do XML de pré-preenchimento. Se o XML de pré-preenchimento for start com a tag `afData` raiz, o XML de saída também terá o mesmo formato. Se o XML de pré-preenchimento não tiver `afData/afBoundData`invólucro e, em vez disso, for start diretamente da tag raiz do schema como `employeeData`, o XML enviado também será start com a `employeeData` tag .

Prefill-Submit-Data-ContentPackage.zip

[Obter](assets/prefill-submit-data-contentpackage.zip)amostra de arquivo contendo dados de preenchimento prévio e dados enviados

### Formulários adaptativos baseados em schemas XML {#xml-schema-af}

A estrutura do XML de preenchimento prévio e do XML enviado para formulários adaptáveis com base no schema XML é a seguinte:

* **Preencher estrutura** XML: O XML de preenchimento prévio deve ser compatível com o Schema XML associado. Para preencher previamente campos não vinculados, vincule a estrutura XML de preenchimento prévio à tag /afData/afBoundData.
* **Estrutura** XML enviada: se nenhum XML de preenchimento prévio for usado, o XML enviado conterá dados para os campos vinculados e não vinculados na tag `afData` wrapper. Se o XML de pré-preenchimento for usado, o XML submetido terá a mesma estrutura do XML de pré-preenchimento. Se o prefill XML for start com a tag `afData` raiz, o XML de saída terá o mesmo formato. Se o XML de pré-preenchimento não tiver `afData/afBoundData` invólucro e, em vez disso, start diretamente da tag raiz do schema como `employeeData`, o XML enviado também será start com a `employeeData` tag .

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

Para campos cujo modelo é schema XML, os dados são preenchidos previamente na `afBoundData` tag, como mostrado na amostra XML abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados.

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
>É recomendável não usar campos não vinculados em painéis vinculados (painéis sem vazio `bindRef` que foram criados arrastando componentes da guia Sidekick ou Fontes de dados). Pode causar perda de dados desses campos não vinculados. Além disso, recomenda-se que os nomes dos campos sejam exclusivos no formulário, especialmente para campos não vinculados.

#### Um exemplo sem o invólucro afData e afBoundData {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Formulários adaptáveis baseados no schema JSON {#json-schema-based-adaptive-forms}

Para formulários adaptáveis baseados no schema JSON, a estrutura de JSON pré-preenchido e JSON enviado é descrita abaixo. Para obter mais informações, consulte [Criação de formulários adaptáveis usando o schema](../../forms/using/adaptive-form-json-schema-form-model.md)JSON.

* **Preencher estrutura** JSON: O JSON de preenchimento prévio deve ser compatível com o Schema JSON associado. Como opção, ele pode ser vinculado ao objeto /afData/afBoundData se você também quiser preencher previamente campos não vinculados.
* **Estrutura** JSON enviada: se nenhum JSON de preenchimento prévio for usado, o JSON enviado conterá dados para os campos vinculados e não vinculados na tag afData wrapper. Se o JSON de pré-preenchimento for usado, o JSON enviado terá a mesma estrutura do JSON de pré-preenchimento. Se o start JSON de pré-preenchimento com o objeto raiz afData, o JSON de saída terá o mesmo formato. Se o JSON de pré-preenchimento não tiver o invólucro afData/afBoundData e, em vez disso, start diretamente do objeto raiz do schema, como usuário, o JSON enviado também será start com o objeto do usuário.

```
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

Para campos que usam o modelo de schema JSON, os dados são preenchidos previamente no objeto afBoundData, como mostrado na amostra JSON abaixo. Ele pode ser usado para preencher previamente um formulário adaptável com um ou mais campos de texto não vinculados. Abaixo está um exemplo de dados com `afData/afBoundData` invólucro:

```
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

Abaixo está um exemplo sem `afData/afBoundData` invólucro:

```
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>O uso de campos não vinculados em painéis vinculados (painéis com bindRef não vazios que foram criados ao arrastar componentes da guia Sidekick ou Fontes de Dados) **não** é recomendado, pois pode causar perda de dados dos campos não vinculados. É recomendável que haja nomes de campos exclusivos no formulário, especialmente para campos não vinculados.

### Formulário adaptável sem modelo de formulário {#adaptive-form-with-no-form-model}

Para formulários adaptáveis sem modelo de formulário, os dados de todos os campos estão sob a `<data>` tag de `<afUnboundData> tag`.

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

## Configuração do serviço de preenchimento prévio usando o Configuration Manager {#configuring-prefill-service-using-configuration-manager}

Para ativar o serviço de preenchimento prévio, especifique a Configuração do serviço de preenchimento padrão na Configuração do console da Web do AEM. Use as seguintes etapas para configurar o serviço de Prefill:

>[!NOTE]
>
>A Configuração do serviço de preenchimento prévio é aplicável a formulários adaptáveis, formulários HTML5 e conjuntos de formulários HTML5.

1. Abra a Configuração **[!UICONTROL do console da Web do]** Adobe Experience Manager usando o URL:\
   https://&lt;servidor>:&lt;porta>/system/console/configMgr
1. Pesquise e abra Configuração **** do serviço de preenchimento padrão.

   ![Configuração de preenchimento prévio](assets/prefill_config_new.png)

1. Insira o local dos dados ou um regex (expressão regular) para os locais **dos arquivos** de dados. Exemplos de locais de arquivos de dados válidos são:

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >Por padrão, o preenchimento prévio é permitido por meio de arquivos crx para todos os tipos de Formulários adaptáveis (XSD, XDP, JSON, FDM e sem base em Modelo de formulário). O preenchimento prévio é permitido somente com arquivos JSON e XML.

1. O serviço de preenchimento prévio agora está configurado para seu formulário.

   >[!NOTE]
   >
   >O protocolo crx cuida da segurança de dados pré-preenchidos e, portanto, é permitido por padrão. Preenchimento por meio de outros protocolos usando regex genérico pode causar vulnerabilidade. Na configuração, especifique uma configuração de URL segura para proteger seus dados.

## O caso curioso de painéis repetíveis {#the-curious-case-of-repeatable-panels}

Geralmente, os campos vinculados (schema de formulário) e não vinculados são criados no mesmo formulário adaptável, mas as exceções a seguir são repetíveis caso os limites sejam repetidos:

* Painéis repetíveis não vinculados não são suportados para formulários adaptáveis usando o modelo de formulário XFA, XSD, schema JSON ou schema FDM.
* Não use campos não vinculados em painéis repetitivos vinculados.

>[!NOTE]
>
>Como regra geral, não misture campos vinculados e não vinculados se eles estiverem intersecados em dados preenchidos pelo usuário final em campos não vinculados. Se possível, você deve modificar o schema ou o modelo de formulário XFA e adicionar uma entrada para campos não vinculados, de modo que também se torne vinculado e seus dados estejam disponíveis como outros campos nos dados enviados.

## Protocolos suportados para o preenchimento prévio de dados do usuário {#supported-protocols-for-prefilling-user-data}

Os formulários adaptativos podem ser pré-preenchidos com dados do usuário no formato de dados de pré-preenchimento através dos seguintes protocolos quando configurados com regex válido:

### O protocolo crx:// {#the-crx-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

O nó especificado deve ter uma propriedade chamada `jcr:data` e manter os dados.

### O protocolo file:// {#the-file-protocol-nbsp}

```xml
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

O arquivo referenciado deve estar no mesmo servidor.

### O protocolo https:// {#the-http-protocol}

```xml
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### O protocolo service:// {#the-service-protocol}

```xml
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME refere-se ao nome do serviço de pré-preenchimento OSGI. Consulte [Criar e executar um serviço](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)de preenchimento prévio.
* IDENTIFIER refere-se a quaisquer metadados exigidos pelo serviço de preenchimento prévio OSGI para buscar os dados de preenchimento prévio. Um identificador do usuário conectado é um exemplo de metadados que podem ser usados.

>[!NOTE]
>
>Não há suporte para a transmissão de parâmetros de autenticação.

### Definindo atributo de dados em slingRequest {#setting-data-attribute-in-slingrequest}

Você também pode definir o `data` atributo em `slingRequest`, onde o `data` atributo é uma string contendo XML ou JSON, como mostrado no código de amostra abaixo (Exemplo é para XML):

```java
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

Você pode gravar uma sequência de caracteres XML ou JSON simples que contenha todos os seus dados e configurá-la em slingRequest. Isso pode ser feito facilmente no JSP do renderizador para qualquer componente, que você deseja incluir na página onde é possível definir o atributo de dados slingRequest.

Por exemplo, onde você deseja um design específico para sua página com um tipo específico de cabeçalho. Para conseguir isso, você pode gravar seu próprio `header.jsp`, que pode ser incluído no componente da página e definir o `data` atributo.

Outro bom exemplo é um caso de uso em que você gostaria de preencher previamente os dados de logon por meio de contas sociais como Facebook, Twitter ou LinkedIn. Nesse caso, é possível incluir um JSP simples no `header.jsp`, que obtém dados da conta do usuário e define o parâmetro data.

prefill-page component.zip

[Obter o arquivo](assets/prefill-page-component.zip)Amostra prefill.jsp no componente de página

## Serviço de pré-preenchimento personalizado do AEM Forms {#aem-forms-custom-prefill-service}

Você pode usar o serviço de preenchimento prévio personalizado para os cenários, onde você lê constantemente os dados de uma fonte predefinida. O serviço de preenchimento prévio lê dados de fontes de dados definidas e preenche previamente os campos do formulário adaptável com o conteúdo do arquivo de dados de preenchimento prévio. Também ajuda a associar permanentemente os dados pré-preenchidos a um formulário adaptável.

### Criar e executar um serviço de preenchimento prévio {#create-and-run-a-prefill-service}

O serviço de pré-preenchimento é um serviço OSGi e é empacotado por meio do pacote OSGi. Crie o pacote OSGi, carregue e instale-o em pacotes do AEM Forms. Antes de começar a criar o pacote:

* [Baixar o AEM Forms Client SDK](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)
* [Download do pacote estereotipado](../../forms/using/prepopulate-adaptive-form-fields.md#main-pars-download-section-711716493)

* Coloque o arquivo de dados (dados de preenchimento prévio) no repositório crx. Você pode colocar o arquivo em qualquer local na pasta \content do crx-repository.

[Obter arquivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Criar um serviço de preenchimento prévio {#create-a-prefill-service}

O pacote estereotipado (pacote de serviço de preenchimento prévio de amostra) contém uma implementação de amostra do serviço de preenchimento prévio do AEM Forms. Abra o pacote estereotipado em um editor de código. Por exemplo, abra o projeto estereotipado no Eclipse para edição. Depois de abrir o pacote estereotipado em um editor de código, execute as seguintes etapas para criar o serviço.

1. Abra o arquivo src\main\java\com\adobe\test\Prefill.java para edição.
1. No código, defina o valor de:

   * `nodePath:` A variável de caminho do nó que aponta para o local do repositório crx contém o caminho do arquivo de dados (pré-preenchimento). Por exemplo, /content/prefilldata.xml
   * `label:` O parâmetro label especifica o nome de exibição do serviço. Por exemplo, Serviço de preenchimento padrão

1. Salve e feche o `Prefill.java` arquivo.
1. Adicione o `AEM Forms Client SDK` pacote ao caminho de compilação do projeto estereotipado.
1. Compile o projeto e crie o .jar para o pacote.

#### Start e uso do serviço de preenchimento prévio {#start-and-use-the-prefill-service}

Para start do serviço de preenchimento prévio, carregue o arquivo JAR no console da Web do AEM Forms e ative o serviço. Agora, os start de serviço aparecem no editor de formulários adaptáveis. Para associar um serviço de preenchimento prévio a um formulário adaptável:

1. Abra o formulário adaptável no Editor de formulários e abra o painel Propriedades do Container de formulário.
1. No console Propriedades, navegue até container de formulários AEM > Básico > Serviço de comprovação.
1. Selecione o Serviço de preenchimento padrão e clique em **[!UICONTROL Salvar]**. O serviço está associado ao formulário.

