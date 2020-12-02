---
title: Renderizando Forms como HTML
seo-title: Renderizando Forms como HTML
description: 'null'
seo-description: nulo
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '4108'
ht-degree: 1%

---


# Renderizando o Forms como HTML {#rendering-forms-as-html}

O serviço Forms renderiza formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Uma vantagem de renderizar um formulário como HTML é que o computador no qual o navegador da Web do cliente está localizado não requer Adobe Reader, Acrobat ou Flash Player (para guias de formulário (obsoleto)).

Para renderizar um formulário como HTML, o design de formulário deve ser salvo como um arquivo XDP. Um design de formulário salvo como um arquivo PDF não pode ser renderizado como HTML. Ao desenvolver um design de formulário no Designer que será renderizado como HTML, considere os seguintes critérios:

* Não use as propriedades de borda de um objeto para desenhar linhas, caixas ou grades no seu formulário. Talvez alguns navegadores não alinhem bordas exatamente como elas aparecem em uma visualização do Objetos podem aparecer em camadas ou empurrar outros objetos para fora das posições desejadas.
* É possível usar linhas, retângulos e círculos para definir o plano de fundo.
* Desenhe um texto ligeiramente maior do que o que parece ser necessário para acomodar o texto. Alguns navegadores da Web não exibem o texto de forma legível.

>[!NOTE]
>
>Ao renderizar um formulário que contém imagens TIFF usando os métodos `FormServiceClient` e `renderHTMLForm2` do objeto `(Deprecated) renderHTMLForm`, as imagens TIFF não são visíveis no formulário HTML renderizado exibido nos navegadores Internet Explorer ou Mozilla Firefox. Esses navegadores não fornecem suporte nativo para imagens TIFF.

## Páginas HTML {#html-pages}

Quando um design de formulário é renderizado como um formulário HTML, cada subformulário de segundo nível é renderizado como uma página HTML (painel). É possível visualização uma hierarquia de subformulário no Designer. Os subformulários filho que pertencem ao subformulário raiz (o nome padrão de um subformulário raiz é form1) são os subformulários do painel. O exemplo a seguir mostra os subformulários de um design de formulário.

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

Quando designs de formulário são renderizados como formulários HTML, os painéis não são restritos a qualquer tamanho de página específico. Se houver subformulários dinâmicos, eles devem ser aninhados dentro do subformulário do painel. Os subformulários dinâmicos podem se expandir para um número infinito de páginas HTML.

Quando um formulário é renderizado como um formulário HTML, os tamanhos de página (necessários para paginar formulários renderizados como PDF) não têm significado. Como um formulário com layout flutuante pode se expandir para um número infinito de páginas HTML, é importante evitar rodapés na página principal. Um rodapé abaixo da área de conteúdo em uma página principal pode substituir o conteúdo HTML que continua além de um limite de página.

Você deve mover-se explicitamente de um painel para outro usando os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Você altera páginas enviando um formulário para o serviço Forms e fazendo com que o serviço Forms renderize o formulário de volta para o dispositivo cliente, geralmente um navegador da Web.

>[!NOTE]
>
>O processo de envio de um formulário para o serviço Forms e, em seguida, a renderização do formulário pelo serviço Forms para o dispositivo cliente é chamado de arredondar os dados para o servidor.

>[!NOTE]
>
>Se você quiser personalizar a aparência do botão Assinatura digital HTML em um formulário HTML, é necessário alterar as seguintes propriedades no arquivo fscdigsig.css (no arquivo adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Esta folha de estilos é aplicável no caso de um campo de sinal em branco.

**.fsc-ds-ssv**: Esta folha de estilos é aplicável no caso de um campo de sinal válido.

**.fsc-ds-ssc**: Esta folha de estilos é aplicável no caso de um campo de sinal válido, mas os dados foram alterados.

**.fsc-ds-ssi**: Esta folha de estilos é aplicável no caso de um campo de sinal inválido.

**.fsc-ds-popup-bg**: Esta propriedade da folha de estilos não está sendo usada.

**.fsc-ds-popup-btn**: Esta propriedade da folha de estilos não está sendo usada.

## Execução de scripts {#running-scripts}

Um autor de formulário especifica se um script é executado no servidor ou no cliente. O serviço Forms cria um ambiente de processamento distribuído e de evento para execução de inteligência de formulário que pode ser distribuído entre o cliente e o servidor usando o atributo `runAt`. Para obter informações sobre esse atributo ou como criar scripts em designs de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

O serviço Forms pode executar scripts enquanto o formulário está sendo renderizado. Como resultado, você pode pré-preencher um formulário com dados ao se conectar a um banco de dados ou a serviços da Web que podem não estar disponíveis no cliente. Você também pode definir o evento `Click` de um botão para ser executado no servidor, de modo que o cliente troque os dados para o servidor. Isso permite que o cliente execute scripts que possam exigir recursos do servidor, como um banco de dados corporativo, enquanto um usuário interage com um formulário. Para formulários HTML, scripts formcalc podem ser executados somente no servidor. Como resultado, você deve marcar esses scripts para serem executados em `server` ou `both`.

Você pode projetar formulários que se movem entre páginas (painéis) chamando os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Esse script é colocado no evento `Click` de um botão e o atributo `runAt` é definido como `Both`. O motivo pelo qual você escolhe `Both` é para que o Adobe Reader ou o Acrobat (para formulários renderizados como PDF) possa alterar páginas sem ir para o servidor e os formulários HTML podem alterar páginas ao arredondar os dados para o servidor. Ou seja, um formulário é enviado para o serviço Forms e um formulário é renderizado novamente como HTML com a nova página exibida.

É recomendável que você não atribua variáveis de script e campos de formulário aos mesmos nomes, como item. Alguns navegadores da Web, como o Internet Explorer, podem não inicializar uma variável com o mesmo nome de um campo de formulário que resulta em um erro de script. É uma boa prática fornecer nomes diferentes para campos de formulário e variáveis de script.

Ao renderizar formulários HTML que contêm a funcionalidade de navegação de página e scripts de formulário (por exemplo, suponha que um script recupere dados de campo de um banco de dados toda vez que o formulário for renderizado), verifique se o script de formulário está localizado no evento form:calculate em vez de form:readyevent.

Os scripts de formulário localizados no evento form:ready são executados apenas uma vez durante a renderização inicial do formulário e não são executados para recuperações de página subsequentes. Por outro lado, o evento form:calculate é executado para cada navegação de página em que o formulário é renderizado.

>[!NOTE]
Em um formulário de várias páginas, as alterações feitas pelo JavaScript em uma página não são retidas se você mover para uma página diferente.

É possível invocar scripts personalizados antes de enviar um formulário. Este recurso funciona em todos os navegadores disponíveis. No entanto, ele pode ser usado somente quando os usuários renderizam o formulário HTML que tem a propriedade `Output Type` definida como `Form Body`. Não funcionará quando `Output Type` for `Full HTML`. Consulte Configurar formulários na ajuda administrativa para obter as etapas de configuração desse recurso.

Primeiro, é necessário definir uma função de retorno de chamada que é chamada antes de enviar o formulário, onde o nome da função é `_user_onsubmit`. Pressupõe-se que a função não gerará nenhuma exceção, ou se isso ocorrer, a exceção será ignorada. É recomendável colocar a função JavaScript na seção head do html; no entanto, você pode declará-lo em qualquer lugar antes do final das tags de script que incluem `xfasubset.js`.

Quando o formserver renderiza um XDP que contém uma lista suspensa, além de criar a lista suspensa, ele também cria dois campos de texto ocultos. Esses campos de texto armazenam os dados da lista suspensa (um armazena o nome de exibição das opções e outro armazena o valor das opções). Portanto, toda vez que um usuário envia o formulário, todos os dados da lista suspensa são enviados. Supondo que você não queira enviar tantos dados toda vez, você pode escrever um script personalizado para desativá-lo. Por exemplo: O nome da lista suspensa é `drpOrderedByStateProv` e está vinculado sob o cabeçalho do subformulário. O nome do elemento de entrada HTML será `header[0].drpOrderedByStateProv[0]`. O nome dos campos ocultos que armazenam e enviam os dados da lista suspensa têm os seguintes nomes: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

Ao criar designs de formulário para renderizar como HTML, você deve restringir seus scripts ao subconjunto XFA para scripts na linguagem JavaScript.

Os scripts executados no cliente ou executados no cliente e no servidor devem ser gravados no subconjunto XFA. Os scripts executados no servidor podem usar o modelo de script XFA completo e também usar FormCalc. Para obter informações sobre como usar o JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Ao executar scripts no cliente, somente o painel atual que está sendo exibido pode usar scripts; por exemplo, não é possível executar script em relação aos campos localizados no painel A quando o painel B é exibido. Ao executar scripts no servidor, todos os painéis podem ser acessados.

Você também deve tomar cuidado ao usar expressões SOM (Modelo de objeto de script) em scripts que são executados no cliente. Somente um subconjunto simplificado de expressões SOM é suportado por scripts executados no cliente.

## Tempo de evento {#event-timing}

O subconjunto XFA define os eventos XFA que são mapeados para eventos HTML. Há uma pequena diferença de comportamento no tempo dos eventos calculate e validate. Em um navegador da Web, um evento calculate completo é executado quando você sai de um campo. Os eventos de cálculo não são executados automaticamente quando você altera para um valor de campo. Você pode forçar um evento calculate chamando o método `xfa.form.execCalculate`.

Em um navegador da Web, eventos de validação só são executados ao sair de um campo ou enviar um formulário. Você pode forçar um evento validate usando o método `xfa.form.execValidate`.

A Forms exibida em um navegador da Web (em oposição ao Adobe Reader ou Acrobat) está em conformidade com o teste nulo XFA (erros ou avisos) para campos obrigatórios.

* Se o teste nulo gerar um erro e você sair de um campo sem especificar um valor, uma caixa de mensagem será exibida e você será reposicionado no campo depois de clicar em OK.
* Se um teste nulo produzir um aviso e você sair de um campo sem especificar um valor, será solicitado que clique em OK ou Cancelar, dando-lhe a opção de continuar sem especificar um valor ou retornar ao campo para inserir um valor.

Para obter mais informações sobre um teste nulo, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botões de formulário {#form-buttons}

Clicar em um botão Enviar envia dados de formulário para o serviço Forms e representa o fim do processamento de formulários. O evento `preSubmit` pode ser definido para ser executado no cliente ou servidor. O evento `preSubmit` é executado antes do envio do formulário se estiver configurado para execução no cliente. Caso contrário, o evento `preSubmit` será executado no servidor durante o envio do formulário. Para obter mais informações sobre o evento `preSubmit`, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se um botão não tiver um script do lado do cliente associado a ele, os dados serão enviados ao servidor, os cálculos serão executados no servidor e o formulário HTML será gerado novamente. Se um botão contiver um script do lado do cliente, os dados não serão enviados para o servidor e o script do lado do cliente será executado no navegador da Web.

## Navegador da Web HTML 4.0 {#html-4-0-web-browser}

Um navegador da Web que suporta apenas HTML 4.0 não pode suportar o modelo de script do lado do cliente do subconjunto XFA. Ao criar um design de formulário para funcionar em HTML 4.0 e MSDHTML ou CSS2HTML, um script marcado para execução no cliente será executado no servidor. Por exemplo, suponha que um usuário clique em um botão localizado em um formulário exibido em um navegador da Web HTML 4.0. Nessa situação, os dados do formulário são enviados para o servidor onde o script do cliente é executado.

É recomendável colocar a lógica do formulário em eventos calculate, que são executados no servidor em HTML 4.0 e no cliente para MSDHTML ou CSS2HTML.

## Manutenção das alterações de apresentação {#maintaining-presentation-changes}

Conforme você se move entre páginas HTML (painéis), somente o estado dos dados é mantido. Configurações como cor de plano de fundo ou configurações de campo obrigatório não são mantidas (se diferentes das configurações iniciais). Para manter o estado da apresentação, é necessário criar campos (geralmente ocultos) que representem o estado da apresentação dos campos. Se você adicionar um script ao evento `Calculate` de um campo que altera a apresentação com base em valores de campo ocultos, poderá preservar o estado da apresentação conforme você se move para frente e para trás entre páginas HTML (painéis).

O script a seguir mantém `fillColor` de um campo com base no valor de `hiddenField`. Suponha que esse script esteja localizado no evento `Calculate` de um campo.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Objetos estáticos não são exibidos em um formulário HTML renderizado quando aninhados dentro de uma célula de tabela. Por exemplo, um círculo e retângulo aninhados dentro de uma célula de tabela não são exibidos em um formulário HTML de renderização. No entanto, esses mesmos objetos estáticos são exibidos corretamente quando localizados fora da tabela.

## Assinatura digital de formulários HTML {#digitally-signing-html-forms}

Não é possível assinar um formulário HTML que contenha um campo de assinatura digital se o formulário for renderizado como uma das seguintes transformações HTML:

* AHTML
* HTML 4
* StaticHTML
* NoScriptXHTML

Para obter informações sobre como assinar digitalmente um documento, consulte [Assinando e certificando Documentos digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md)

## Renderização de um formulário XHTML compatível com diretrizes de acessibilidade {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

É possível renderizar um formulário HTML completo compatível com as diretrizes de acessibilidade. Ou seja, o formulário é renderizado em tags HTML completas, em vez de o formulário HTML ser renderizado em tags body (não em uma página HTML completa).

## Validação de dados de formulário {#validating-form-data}

É recomendável limitar o uso de regras de validação para campos de formulário ao renderizar o formulário como um formulário HTML. Algumas regras de validação podem não ser suportadas em formulários HTML. Por exemplo, quando um padrão de validação de MM-DD-AAAA é aplicado a um campo `Date/Time` localizado em um design de formulário renderizado como um formulário HTML, ele não funciona corretamente, mesmo se a data for digitada corretamente. No entanto, esse padrão de validação funciona corretamente para formulários renderizados como PDF.

>[!NOTE]
Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Defina as opções de tempo de execução HTML.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de poder importar dados de forma programática para uma API FormClient do PDF, é necessário criar um cliente de serviço de Integração de Dados de Formulário. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Definir opções de tempo de execução HTML**

As opções de tempo de execução HTML são definidas ao renderizar um formulário HTML. Por exemplo, é possível adicionar uma barra de ferramentas a um formulário HTML para permitir que os usuários selecionem anexos de arquivo localizados no computador cliente ou recuperem anexos de arquivo renderizados com o formulário HTML. Por padrão, uma barra de ferramentas HTML é desativada. Para adicionar uma barra de ferramentas a um formulário HTML, é necessário definir programaticamente as opções de tempo de execução. Por padrão, uma barra de ferramentas HTML consiste nos seguintes botões:

* `Home`: Fornece um link para a raiz da Web do aplicativo.
* `Upload`: Fornece uma interface de usuário para selecionar arquivos a serem anexados ao formulário atual.
* `Download`: Fornece uma interface de usuário para exibir os arquivos anexados.

Quando uma barra de ferramentas HTML é exibida em um formulário HTML, o usuário pode selecionar no máximo dez arquivos para enviar juntamente com os dados do formulário. Depois que os arquivos forem submetidos, o serviço Forms poderá recuperá-los.

Ao renderizar um formulário como HTML, você pode especificar um valor agente-usuário. Um valor agente-usuário fornece informações do navegador e do sistema. Esse é um valor opcional e você pode passar um valor de string vazio. O start rápido Renderizar um formulário HTML usando a API Java mostra como obter um valor de agente do usuário e usá-lo para renderizar um formulário como HTML.

URLs HTTP para onde os dados do formulário são postados podem ser especificados ao configurar o URL do público alvo usando a API do Forms Service Client ou podem ser especificados no botão Enviar contido no design de formulário XDP. Se o URL do público alvo for especificado no design de formulário, não defina um valor usando a API do Forms Service Client.

>[!NOTE]
A renderização de um formulário HTML com uma barra de ferramentas é opcional.

>[!NOTE]
Se você renderizar um formulário AHTML, é recomendável não adicionar uma barra de ferramentas ao formulário.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário HTML fica visível para o usuário.

**Consulte também:**

[Renderizar um formulário como HTML usando a API Java](#render-a-form-as-html-using-the-java-api)

[Renderizar um formulário como HTML usando a API de serviço da Web](#render-a-form-as-html-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização de HTML Forms com barras de ferramentas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário como HTML usando a API Java {#render-a-form-as-html-using-the-java-api}

Renderize um formulário HTML usando a API Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e transmita um valor de enumeração `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o método `HTMLRenderSpec` do objeto `setLocale` e transmita um valor de string que especifica o valor de localidade. (Esta é uma configuração opcional.)
   * Para renderizar o formulário HTML em tags HTML completas, chame o método `HTMLRenderSpec` do objeto e passe `OutputType.FullHTMLTags`. `setOutputType` (Esta é uma configuração opcional.)

   >[!NOTE]
   O Forms não é renderizado com êxito em HTML quando a opção `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` passado para o método `FormsServiceClient` do objeto). `(Deprecated) renderHTMLForm` Quando `ApplicationWebRoot` for outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve suas configurações.

1. Renderizar um formulário HTML

   Chame o método `FormsServiceClient` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `(Deprecated) renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderizando Forms como HTML](#rendering-forms-as-html)

[Start rápido (modo SOAP): Como renderizar um formulário HTML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário como HTML usando a API de serviço da Web {#render-a-form-as-html-using-the-web-service-api}

Renderize um formulário HTML usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e transmita um valor de enumeração `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o método `HTMLRenderSpec` do objeto `setLocale` e transmita um valor de string que especifica o valor de localidade. Para obter mais informações, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para renderizar o formulário HTML em tags HTML completas, chame o método `HTMLRenderSpec` do objeto e passe `OutputType.FullHTMLTags`.`setOutputType`

   >[!NOTE]
   O Forms não é renderizado com êxito em HTML quando a opção `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` passado para o método `FormsServiceClient` do objeto). `(Deprecated) renderHTMLForm` Quando `ApplicationWebRoot` for outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve suas configurações.

1. Renderizar um formulário HTML

   Chame o método `FormsService` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe `null`. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário. (Consulte [Anexar arquivos ao formulário](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método. Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método. Esse parâmetro armazenará os dados XML de saída.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método. Esse argumento armazenará o número de páginas no formulário.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método. Esse argumento armazenará o valor de localidade.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método. Esse argumento armazenará o valor de renderização HTML usado.
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `(Deprecated) renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderizando Forms como HTML](#rendering-forms-as-html)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

