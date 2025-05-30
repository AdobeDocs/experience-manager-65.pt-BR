---
title: Renderização do Forms como HTML
description: Use o serviço Forms para renderizar formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Você pode usar a API do Java&trade; e a API de serviço da Web para renderizar formulários como HTML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '4099'
ht-degree: 0%

---

# Renderização do Forms como HTML {#rendering-forms-as-html}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

O serviço Forms renderiza formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Um benefício de renderizar um formulário como HTML é que o computador no qual o navegador da Web do cliente está localizado não requer Adobe Reader, Acrobat ou Flash Player (para Guias de formulário (desaprovado)).

Para renderizar um formulário como HTML, o design do formulário deve ser salvo como um arquivo XDP. Um design de formulário salvo como um arquivo PDF não pode ser renderizado como HTML. Ao desenvolver um design de formulário no Designer que será renderizado como HTML, considere os seguintes critérios:

* Não use as propriedades de borda de um objeto para desenhar linhas, caixas ou grades no formulário. Alguns navegadores podem não alinhar bordas exatamente como aparecem em uma visualização. Objetos podem aparecer em camadas ou podem empurrar outros objetos para fora de sua posição esperada.
* Você pode usar linhas, retângulos e círculos para definir o plano de fundo.
* O texto do Draw é um pouco maior do que o necessário para acomodar o texto. Alguns navegadores da Web não exibem o texto de forma legível.

>[!NOTE]
>
>Ao renderizar um formulário que contém imagens TIFF usando os métodos `(Deprecated) renderHTMLForm` e `renderHTMLForm2` do objeto `FormServiceClient`, as imagens TIFF não ficam visíveis no formulário HTML renderizado que é exibido nos navegadores Internet Explorer ou Mozilla Firefox. Esses navegadores não fornecem suporte nativo para imagens TIFF.

## páginas HTML {#html-pages}

Quando um design de formulário é renderizado como um formulário HTML, cada subformulário de segundo nível é renderizado como uma página de HTML (painel). Você pode visualizar a hierarquia de um subformulário no Designer. Os subformulários secundários que pertencem ao subformulário raiz (o nome padrão de um subformulário raiz é form1) são os subformulários do painel. O exemplo a seguir mostra os subformulários de um design de formulário.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

Quando os designs de formulário são renderizados como formulários de HTML, os painéis não são restritos a nenhum tamanho de página específico. Se você tiver subformulários dinâmicos, eles devem ser aninhados dentro do subformulário do painel. Os subformulários dinâmicos podem se expandir para um número infinito de páginas de HTML.

Quando um formulário é renderizado como um formulário HTML, os tamanhos de página (necessários para paginar formulários renderizados como PDF) não têm significado. Como um formulário com layout fluível pode se expandir para um número infinito de páginas de HTML, é importante evitar rodapés na página principal. Um rodapé abaixo da área de conteúdo em uma página-mestre pode substituir o conteúdo de HTML que flui além de um limite de página.

Você deve mover explicitamente de um painel para outro usando os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Você altera páginas enviando um formulário para o serviço Forms e fazendo com que o serviço Forms renderize o formulário de volta para o dispositivo cliente, normalmente um navegador da Web.

>[!NOTE]
>
>O processo de enviar um formulário para o serviço Forms e, em seguida, fazer com que o serviço Forms renderize o formulário para o dispositivo cliente é chamado de dados de viagem de ida e volta para o servidor.

>[!NOTE]
>
>Se você quiser personalizar a aparência do botão HTML Digital Signature em um formulário HTML, altere as seguintes propriedades no arquivo fscdigsig.css (no arquivo adobe-forms-ds.ear > adobe-forms-ds.war):

**`.fsc-ds-ssb`**: esta folha de estilos é aplicável se houver um campo de sinal em branco.

**`.fsc-ds-ssv`**: esta folha de estilos é aplicável se houver um campo de sinal Válido.

**`.fsc-ds-ssc`**: esta folha de estilos será aplicável se houver um campo Sinal válido, mas os dados forem alterados.

**`.fsc-ds-ssi`**: esta folha de estilos é aplicável se houver um campo de sinal inválido.

**`.fsc-ds-popup-bg`**: Esta propriedade da folha de estilos não está sendo usada.

**.`fsc-ds-popup-btn`**: Esta propriedade da folha de estilos não está sendo usada.

## Execução de scripts {#running-scripts}

Um autor de formulário especifica se um script é executado no servidor ou no cliente. O serviço Forms cria um ambiente de processamento de eventos distribuído para execução de inteligência de formulários que pode ser distribuído entre o cliente e o servidor usando o atributo `runAt`. Para obter informações sobre este atributo ou criar scripts nos designs de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

O serviço Forms pode executar scripts enquanto o formulário está sendo renderizado. Como resultado, você pode preencher previamente um formulário com dados se conectando a um banco de dados ou a serviços da Web que podem não estar disponíveis no cliente. Você também pode definir o evento `Click` de um botão para ser executado no servidor, para que o cliente arredonde os dados da viagem para o servidor. Isso permite que o cliente execute scripts que podem exigir recursos de servidor, como um banco de dados empresarial, enquanto um usuário interage com um formulário. Para formulários HTML, os scripts formcalc podem ser executados somente no servidor. Como resultado, você deve marcar esses scripts para serem executados às `server` ou `both`.

Você pode criar formulários que se movem entre páginas (painéis) chamando os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Este script é colocado no evento `Click` de um botão e o atributo `runAt` está definido como `Both`. O motivo para você escolher `Both` é para que o Adobe Reader ou o Acrobat (para formulários renderizados como PDF) possam alterar páginas sem ir para o servidor e os formulários HTML possam alterar páginas arredondando dados para o servidor. Ou seja, um formulário é enviado para o serviço Forms e um formulário é renderizado como HTML com a nova página exibida.

É recomendável não atribuir às variáveis de script e aos campos de formulário os mesmos nomes, como item. Alguns navegadores da Web, como o Internet Explorer, podem não inicializar uma variável com o mesmo nome de um campo de formulário que resulta na ocorrência de um erro de script. É uma boa prática fornecer nomes diferentes para campos de formulário e variáveis de script.

Ao renderizar formulários de HTML que contêm a funcionalidade de navegação de página e scripts de formulário (por exemplo, suponha que um script recupere dados de campo de um banco de dados sempre que o formulário for renderizado), verifique se o script de formulário está no formato:calcular evento em vez de no formulário:readyevent.

Os scripts de formulário que estão no evento form:ready são executados apenas uma vez durante a renderização inicial do formulário e não são executados para recuperações de páginas subsequentes. Por outro lado, o evento form:calculate é executado para cada navegação de página em que o formulário é renderizado.

>[!NOTE]
>
>Em um formulário multipáginas, as alterações feitas pelo JavaScript em uma página não serão mantidas se você for para uma página diferente.

Você pode chamar scripts personalizados antes de enviar um formulário. Esse recurso funciona em todos os navegadores disponíveis. No entanto, ele pode ser usado somente quando os usuários renderizam o formulário HTML que tem sua propriedade `Output Type` definida como `Form Body`. Ele não funcionará quando o `Output Type` for `Full HTML`. Consulte Configuração de formulários na ajuda de administração para ver as etapas de configuração desse recurso.

Primeiro, defina uma função de retorno de chamada que seja chamada antes de enviar o formulário, onde o nome da função é `_user_onsubmit`. Pressupõe-se que a função não lançará nenhuma exceção, ou, se o fizer, a exceção será ignorada. É recomendável colocar a função JavaScript na seção head do html; no entanto, você pode declará-la em qualquer lugar antes do fim das tags de script que incluem `xfasubset.js`.

Quando formserver renderiza um XDP que contém uma lista suspensa, além de criar a lista suspensa, ele também cria dois campos de texto ocultos. Esses campos de texto armazenam os dados da lista suspensa (um armazena o nome de exibição das opções e outro armazena o valor das opções). Portanto, sempre que um usuário enviar o formulário, todos os dados da lista suspensa serão enviados. Supondo que você não deseje enviar tantos dados sempre, você pode gravar um script personalizado para desativá-los. Por exemplo: o nome da lista suspensa é `drpOrderedByStateProv` e está encapsulado sob o cabeçalho do subformulário. O nome do elemento de entrada de HTML será `header[0].drpOrderedByStateProv[0]`. O nome dos campos ocultos que armazenam e enviam os dados da lista suspensa tem os seguintes nomes: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Você pode desativar esses elementos de entrada da seguinte maneira se não quiser publicar os dados. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## Subconjuntos XFA {#xfa-subsets}

Ao criar designs de formulário para renderizar como HTML, você deve restringir seu script ao subconjunto XFA para scripts na linguagem JavaScript.

Os scripts executados no cliente ou no servidor devem ser gravados no subconjunto XFA. Os scripts executados no servidor podem usar o modelo de script XFA completo e também usar FormCalc. Para obter informações sobre como usar o JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Ao executar scripts no cliente, somente o painel atual que está sendo exibido pode usar script; por exemplo, você não pode criar scripts para campos que estão no painel A quando o painel B é exibido. Ao executar scripts no servidor, todos os painéis podem ser acessados.

Tenha cuidado ao usar expressões de modelo de objeto de script (SOM) em scripts executados no cliente. Somente um subconjunto simplificado de expressões SOM é suportado por scripts executados no cliente.

## Tempo do evento {#event-timing}

O subconjunto XFA define os eventos XFA que são mapeados para eventos HTML. Há uma pequena diferença no comportamento em relação ao tempo dos eventos de cálculo e validação. Em um navegador da Web, um evento de cálculo completo é executado ao sair de um campo. Eventos de cálculo não são executados automaticamente quando você faz uma alteração em um valor de campo. Você pode forçar um evento de cálculo chamando o método `xfa.form.execCalculate`.

Em um navegador da Web, a validação de eventos só é executada ao sair de um campo ou enviar um formulário. Você pode forçar um evento de validação usando o método `xfa.form.execValidate`.

A Forms exibida em um navegador da Web (em vez de Adobe Reader ou Acrobat) está em conformidade com o teste nulo XFA (erros ou avisos) para campos obrigatórios.

* Se o teste nulo produzir um erro e você sair de um campo sem especificar um valor, uma caixa de mensagem será exibida e você será reposicionado no campo depois de clicar em OK.
* Se um teste nulo produzir um aviso e você sair de um campo sem especificar um valor, você será solicitado a clicar em OK ou em Cancelar, fornecendo a opção de continuar sem especificar um valor ou retornar ao campo para inserir um valor.

Para obter mais informações sobre um teste nulo, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botões de formulário {#form-buttons}

Clicar em um botão enviar envia dados de formulário para o serviço Forms e representa o fim do processamento de formulário. O evento `preSubmit` pode ser definido para execução no cliente ou servidor. O evento `preSubmit` será executado antes do envio do formulário se estiver configurado para ser executado no cliente. Caso contrário, o evento `preSubmit` será executado no servidor durante o envio do formulário. Para obter mais informações sobre o evento `preSubmit`, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se um botão não tiver script do lado do cliente associado a ele, os dados serão enviados ao servidor, os cálculos serão executados no servidor e o formulário HTML será gerado novamente. Se um botão contiver um script do lado do cliente, os dados não serão enviados para o servidor e o script do lado do cliente será executado no navegador da Web.

## navegador HTML 4.0 {#html-4-0-web-browser}

Um navegador da Web compatível apenas com o HTML 4.0 não pode oferecer suporte ao modelo de script do lado do cliente do subconjunto XFA. Ao criar um design de formulário para funcionar no HTML 4.0 e MSDHTML ou CSS2HTML, um script que está marcado para execução no cliente será realmente executado no servidor. Por exemplo, suponha que um usuário clique em um botão localizado em um formulário exibido em um navegador HTML 4.0. Nessa situação, os dados de formulário são enviados para o servidor onde o script do lado do cliente é executado.

É recomendável colocar a lógica do formulário em calcular eventos, que são executados no servidor no HTML 4.0 e no cliente para MSDHTML ou CSS2HTML.

## Manutenção das alterações na apresentação {#maintaining-presentation-changes}

À medida que você se move entre páginas HTML (painéis), somente o estado dos dados é mantido. Configurações como cor de fundo ou configurações de campo obrigatório não são mantidas (se forem diferentes das configurações iniciais). Para manter o estado de apresentação, você deve criar campos (geralmente ocultos) que representem o estado de apresentação dos campos. Se você adicionar um script ao evento `Calculate` de um campo que altere a apresentação com base em valores de campo ocultos, será possível preservar o estado da apresentação à medida que você move para frente e para trás entre páginas HTML (painéis).

O script a seguir mantém o `fillColor` de um campo com base no valor de `hiddenField`. Suponha que este script esteja em um evento `Calculate` do campo.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
>
>Os objetos estáticos não são exibidos em um formulário HTML renderizado quando aninhados dentro de uma célula da tabela. Por exemplo, um círculo e um retângulo aninhados dentro de uma célula de tabela não são exibidos em uma forma de HTML de renderização. No entanto, esses mesmos objetos estáticos são exibidos corretamente quando localizados fora da tabela.

## Assinatura digital de formulários de HTML {#digitally-signing-html-forms}

Não é possível assinar um formulário de HTML que contém um campo de assinatura digital se o formulário for renderizado como uma das seguintes transformações de HTML:

* AHTML
* HTML 4
* StaticHTML
* NoScriptXHTML

Para obter informações sobre como assinar digitalmente um documento, consulte [Assinatura Digital e Documentos de Certificação](/help/forms/developing/digitally-signing-certifying-documents.md)

## Renderização de um formulário XHTML compatível com as diretrizes de acessibilidade {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

Você pode renderizar um formulário de HTML completo que esteja em conformidade com as diretrizes de acessibilidade. Ou seja, o formulário é renderizado em tags de HTML completo, em vez de o formulário de HTML ser renderizado em tags de corpo (não uma página de HTML completa).

## Validação de dados do formulário {#validating-form-data}

É recomendável limitar o uso das regras de validação para campos de formulário ao renderizar o formulário como um formulário HTML. Algumas regras de validação podem não ser compatíveis com formulários HTML. Por exemplo, quando um padrão de validação de MM-DD-AAAA é aplicado a um campo `Date/Time` que está em um design de formulário renderizado como um formulário HTML, ele não funciona corretamente, mesmo se a data for digitada corretamente. No entanto, esse padrão de validação funciona corretamente para formulários renderizados como PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Defina as opções de tempo de execução de HTML.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de importar dados programaticamente para uma API formClient do PDF, você deve criar um cliente do serviço de Integração de dados de formulário. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Definir opções de tempo de execução de HTML**

Você define opções de tempo de execução de HTML ao renderizar um formulário de HTML. Por exemplo, você pode adicionar uma barra de ferramentas a um formulário HTML para permitir que os usuários selecionem anexos de arquivo localizados no computador cliente ou para recuperar anexos de arquivo renderizados com o formulário HTML. Por padrão, uma barra de ferramentas HTML está desativada. Para adicionar uma barra de ferramentas a um formulário HTML, você deve definir programaticamente as opções de tempo de execução. Por padrão, uma barra de ferramentas HTML consiste nos seguintes botões:

* `Home`: fornece um link para a raiz da Web do aplicativo.
* `Upload`: Fornece uma interface de usuário para selecionar arquivos para anexar ao formulário atual.
* `Download`: fornece uma interface de usuário para exibir os arquivos anexados.

Quando uma barra de ferramentas HTML é exibida em um formulário HTML, um usuário pode selecionar no máximo dez arquivos para enviar juntamente com os dados de formulário. Depois que os arquivos forem enviados, o serviço Forms poderá recuperá-los.

Ao renderizar um formulário como HTML, você pode especificar um valor user-agent. Um valor agente-usuário fornece informações do navegador e do sistema. Este é um valor opcional, e você pode passar um valor de string vazio. O início rápido da Renderização de um formulário de HTML usando a API Java mostra como obter um valor de agente de usuário e usá-lo para renderizar um formulário como HTML.

Os URLs HTTP para onde os dados de formulário são publicados podem ser especificados definindo o URL de destino usando a API do cliente de serviço do Forms ou podem ser especificados no botão Enviar contido no design do formulário XDP. Se a URL de destino estiver especificada no design do formulário, não defina um valor usando a API do cliente de serviço do Forms.

>[!NOTE]
>
>A renderização de um formulário HTML com uma barra de ferramentas é opcional.

>[!NOTE]
>
>Se você renderizar um formulário AHTML, é recomendável não adicionar uma barra de ferramentas ao formulário.

**Renderizar um formulário de HTML**

Para renderizar um formulário HTML, especifique um design de formulário que foi criado no Designer e salvo como um arquivo XDP. Selecione um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação de HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores de URI, que são necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da web do cliente, o formulário de HTML fica visível para o usuário.

**Consulte também**

[Renderizar um formulário como HTML usando a API Java](#render-a-form-as-html-using-the-java-api)

[Renderizar um formulário como HTML usando a API do serviço Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do HTML Forms com barras de ferramentas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário como HTML usando a API Java {#render-a-form-as-html-using-the-java-api}

Renderize um formulário HTML usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `setHTMLToolbar` do objeto `HTMLRenderSpec` e passe um valor enum `HTMLToolbar`. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o método `setLocale` do objeto `HTMLRenderSpec` e passe um valor de cadeia de caracteres que especifique o valor de localidade. (Esta é uma configuração opcional.)
   * Para renderizar o formulário HTML nas marcas HTML completas, chame o método `setOutputType` do objeto `HTMLRenderSpec` e passe `OutputType.FullHTMLTags`. (Esta é uma configuração opcional.)

   >[!NOTE]
   >
   >Os Forms não são renderizados com êxito no HTML quando a opção `StandAlone` é `true` e o `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` passado para o método `(Deprecated) renderHTMLForm` do objeto `FormsServiceClient`). Quando o `ApplicationWebRoot` é outro servidor de um que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI da raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário HTML

   Invoque o método `(Deprecated) renderHTMLForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena opções de tempo de execução de HTML.
   * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `(Deprecated) renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que pode ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms como HTML](#rendering-forms-as-html)

[Início rápido (modo SOAP): renderização de um formulário HTML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário como HTML usando a API do serviço Web {#render-a-form-as-html-using-the-web-service-api}

Renderize um formulário HTML usando a API (serviço da Web) do Forms:

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Definir opções de tempo de execução de HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `setHTMLToolbar` do objeto `HTMLRenderSpec` e passe um valor enum `HTMLToolbar`. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o método `setLocale` do objeto `HTMLRenderSpec` e passe um valor de cadeia de caracteres que especifique o valor de localidade. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para renderizar o formulário HTML nas marcas HTML completas, chame o método `setOutputType` do objeto `HTMLRenderSpec` e passe `OutputType.FullHTMLTags`.

   >[!NOTE]
   >
   >Os Forms não são renderizados com êxito no HTML quando a opção `StandAlone` é `true` e o `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` passado para o método `(Deprecated) renderHTMLForm` do objeto `FormsServiceClient`). Quando o `ApplicationWebRoot` é outro servidor de um que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI da raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário HTML

   Invoque o método `(Deprecated) renderHTMLForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`. (Consulte [Preenchimento prévio de Forms com Layouts Fluxáveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * O objeto `HTMLRenderSpec` que armazena opções de tempo de execução de HTML.
   * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário. (Consulte [Anexar arquivos ao formulário](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Esse parâmetro armazenará os dados XML de saída.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. Esse argumento armazenará o número de páginas no formulário.
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. Esse argumento armazenará o valor do local.
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. Esse argumento armazenará o valor de renderização do HTML usado.
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `(Deprecated) renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms como HTML](#rendering-forms-as-html)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
