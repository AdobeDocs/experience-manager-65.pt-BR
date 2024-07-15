---
title: Renderização do HTML Forms com barras de ferramentas personalizadas
description: Use o serviço Forms para personalizar uma barra de ferramentas que é renderizada com um formulário HTML. Você pode renderizar um Formulário HTML com uma barra de ferramentas personalizada usando a API Java e uma API de Serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2328'
ht-degree: 0%

---

# Renderização do HTML Forms com barras de ferramentas personalizadas {#rendering-html-forms-with-customtoolbars}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

## Renderização do HTML Forms com barras de ferramentas personalizadas {#rendering-html-forms-with-custom-toolbars}

O serviço Forms permite personalizar uma barra de ferramentas que é renderizada com um formulário HTML. Uma barra de ferramentas pode ser personalizada para alterar sua aparência substituindo estilos CSS padrão e para adicionar comportamento dinâmico substituindo scripts Java. Uma barra de ferramentas é personalizada usando um arquivo XML chamado fscmenu.xml. Por padrão, o serviço Forms recupera esse arquivo de um local de URI especificado internamente.

>[!NOTE]
>
>Esse local do URI está no arquivo adobe-forms-core.jar, que está no arquivo adobe-forms-dsc.jar. O arquivo adobe-forms-dsc.jar está na pasta C:\Adobe\Adobe_Experience_Manager_forms\ (C:\ é o diretório de instalação). Você pode usar uma ferramenta de extração de arquivos, como Win RAR, para abrir o Adobe.

Você pode copiar o arquivo fscmenu.xml desse local, modificá-lo para atender aos seus requisitos e, em seguida, colocá-lo em um local URI personalizado. Em seguida, usando a API de serviço do Forms, defina as opções de tempo de execução que fazem com que o serviço do Forms use o arquivo fscmenu.xml do local especificado. Essas ações resultam na renderização, pelo serviço Forms, de um formulário HTML com uma barra de ferramentas personalizada.

Além do arquivo fscmenu.xml, você também precisa obter os seguintes arquivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS é o script Java associado a cada nó. É necessário fornecer um para o nó `div#fscmenu` e, opcionalmente, para os nós `ul#fscmenuItem`. Os arquivos JS implementam a funcionalidade principal da barra de ferramentas e os arquivos padrão funcionam.

fscCSS é uma folha de estilos associada a um nó específico. Os estilos nos arquivos CSS especificam a aparência da barra de ferramentas. *fscVCSS* é uma folha de estilos de uma barra de ferramentas vertical, que é exibida à esquerda do formulário HTML renderizado. *fscICES* é uma folha de estilos usada para formulários HTML que são renderizados no Internet Explorer.

Verifique se todos os arquivos acima estão referenciados no arquivo fscmenu.xml. Ou seja, no arquivo fscmenu.xml, especifique os locais de URI para apontar para esses arquivos para que o serviço Forms possa localizá-los. Por padrão, esses arquivos estão disponíveis em locais URI começando com palavras-chave internas `FSWebRoot` ou `ApplicationWebRoot`.

Para personalizar a barra de ferramentas, substitua as palavras-chave usando a palavra-chave externa `FSToolBarURI`. Essa palavra-chave representa o URI passado para o serviço Forms no tempo de execução (essa abordagem é mostrada posteriormente nesta seção).

Você também pode especificar os locais absolutos desses arquivos JS e CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. Nessa situação, não é necessário usar a palavra-chave `FSToolBarURI`.

>[!NOTE]
>
>Não é recomendável misturar as maneiras pelas quais esses arquivos são referenciados. Ou seja, todos os URIs devem ser referenciados usando a palavra-chave `FSToolBarURI` ou um local absoluto.

Você pode obter os arquivos JS e CSS abrindo o arquivo adobe-forms-&lt;appserver>.ear. Neste arquivo, abra o adobe-forms-res.war. Todos esses arquivos estão no arquivo WAR. O arquivo adobe-forms-&lt;appserver>.ear está na pasta de instalação do AEM forms (C:\ é o diretório de instalação). Você pode abrir o adobe-forms-&lt;appserver>.ear usando uma ferramenta de extração de arquivos, como o WinRAR.

A sintaxe XML a seguir mostra um arquivo fscmenu.xml de exemplo.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>O texto em negrito representa os URIs para os arquivos CSS e JS que devem ser referenciados.

Os itens a seguir descrevem como personalizar uma barra de ferramentas:

* Altere os valores dos atributos `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (no arquivo fscmenu.xml) para refletir os locais personalizados dos arquivos referenciados usando um dos métodos descritos nesta seção (por exemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Todos os arquivos CSS e JS devem ser especificados. Se nenhum dos arquivos for modificado, forneça o padrão no local personalizado. Você pode obter os arquivos padrão abrindo vários arquivos conforme descrito nesta seção.
* É permitido fornecer uma referência absoluta (por exemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para qualquer arquivo.
* Os arquivos JS e CSS exigidos pelo nó `div#fscmenu` são essenciais para a funcionalidade da barra de ferramentas. Os nós `ul#fscmenuItem` individuais podem ou não ter arquivos JS ou CSS compatíveis.

**Alterando o valor local**

Como parte da personalização de uma barra de ferramentas, você pode alterar o valor do local da barra de ferramentas. Ou seja, você pode exibi-lo em outro idioma. A ilustração a seguir mostra uma barra de ferramentas personalizada que é exibida em francês.

>[!NOTE]
>
>Não é possível criar uma barra de ferramentas personalizada em mais de um idioma. As barras de ferramentas não podem usar arquivos XML diferentes com base nas configurações de local.

Para alterar o valor do local de uma barra de ferramentas, verifique se o arquivo fscmenu.xml contém o idioma que você deseja exibir. A sintaxe XML a seguir mostra o arquivo fscmenu.xml usado para exibir uma barra de ferramentas em francês.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Os Quick Starts associados a esta seção usam este arquivo XML para exibir uma barra de ferramentas personalizada em francês, como mostrado na ilustração anterior.

Além disso, especifique um valor de localidade válido chamando o método `setLocale` do objeto `HTMLRenderSpec` e transmitindo um valor de cadeia de caracteres que especifique o valor de localidade. Por exemplo, passe `fr_FR` para especificar francês. O serviço Forms é fornecido com barras de ferramentas localizadas.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que usa uma barra de ferramentas personalizada, você deve saber como os formulários HTML são renderizados. (Consulte [Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que contenha uma barra de ferramentas personalizada, execute estas tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API Java do Forms.
1. Referencie um arquivo XML fscmenu personalizado.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto da API Java do Forms**

Antes de executar programaticamente uma operação que o serviço Forms suporta, você deve criar um objeto cliente Forms.

**Referenciar um arquivo XML fscmenu personalizado**

Para renderizar um formulário HTML que contém uma barra de ferramentas personalizada, consulte um arquivo XML fscmenu que descreve a barra de ferramentas. (Esta seção fornece dois exemplos de um arquivo XML fscmenu.) Além disso, certifique-se de que o arquivo fscmenu.xml especifique os locais de todos os arquivos referenciados corretamente. Como mencionado anteriormente nesta seção, verifique se todos os arquivos são referenciados pela palavra-chave `FSToolBarURI` ou por seus locais absolutos.

**Renderizar um formulário de HTML**

Para renderizar um formulário HTML, especifique um design de formulário que foi criado no Designer e salvo como um arquivo XDP. Selecione também um tipo de transformação de HTML. Por exemplo, você pode especificar o tipo de transformação de HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores de URI para renderização de outros tipos de formulário.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente para tornar o formulário HTML visível para os usuários.

**Consulte também**

[Renderize um formulário HTML com uma barra de ferramentas personalizada usando a API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API do serviço Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderize um formulário HTML com uma barra de ferramentas personalizada usando a API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Renderize um formulário HTML que contenha uma barra de ferramentas personalizada usando a API de serviço do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto de API Java do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência a um arquivo XML personalizado do fscmenu

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `setHTMLToolbar` do objeto `HTMLRenderSpec` e passe um valor enum `HTMLToolbar`. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu invocando o método `setToolbarURI` do objeto `HTMLRenderSpec` e transmitindo um valor de cadeia de caracteres que especifica o local URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando o método `setLocale` do objeto `HTMLRenderSpec` e transmitindo um valor de cadeia de caracteres que especifica o valor da localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >O Início Rápido associado a esta seção define este valor como `fr_FR`*.*

1. Renderizar um formulário HTML

   Chame o método `renderHTMLForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena opções de tempo de execução de HTML.
   * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` que seja usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Início rápido (modo SOAP): renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API do serviço Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Renderize um formulário HTML que contenha uma barra de ferramentas personalizada usando a API de serviço do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto de API Java do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Referência a um arquivo XML personalizado do fscmenu

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `setHTMLToolbar` do objeto `HTMLRenderSpec` e passe um valor enum `HTMLToolbar`. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu invocando o método `setToolbarURI` do objeto `HTMLRenderSpec` e transmitindo um valor de cadeia de caracteres que especifica o local URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando o método `setLocale` do objeto `HTMLRenderSpec` e transmitindo um valor de cadeia de caracteres que especifica o valor da localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >O Início Rápido associado a esta seção define este valor como `fr_FR`*.*

1. Renderizar um formulário HTML

   Chame o método `renderHTMLForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`.
   * O objeto `HTMLRenderSpec` que armazena opções de tempo de execução de HTML.
   * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT` (como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este parâmetro é opcional, e você pode especificar `null` se não pretende anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método `renderHTMLForm`. Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método `renderHTMLForm`. Esse parâmetro armazena os dados XML de saída.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método `renderHTMLForm`. Esse argumento armazena o número de páginas no formulário.
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método `renderHTMLForm`. Esse argumento armazena o valor do local.
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método `renderHTMLForm`. Esse argumento armazena o valor de renderização do HTML usado.
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` que seja usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
