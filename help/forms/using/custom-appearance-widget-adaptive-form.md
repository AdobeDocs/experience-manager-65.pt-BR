---
title: Criar aparências personalizadas para campos de formulário adaptáveis
seo-title: Create custom appearances for adaptive form fields
description: Personalize a aparência dos componentes prontos para uso no Adaptive Forms.
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 8a24ca02762e7902b7d0033b36560629ee711de1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# Criar aparências personalizadas para campos de formulário adaptáveis{#create-custom-appearances-for-adaptive-form-fields}

## Introdução {#introduction}

Os formulários adaptáveis usam o [estrutura de aparência](/help/forms/using/introduction-widgets.md) para ajudá-lo a criar aparências personalizadas para campos de formulário adaptáveis e fornecer uma experiência de usuário diferente. Por exemplo, substitua botões de opção e caixas de seleção por botões de alternância ou use plug-ins jQuery personalizados para restringir as entradas de usuários em campos como números de telefone ou ID de email.

Este documento explica como usar um plug-in jQuery para criar essas experiências alternativas para campos de formulário adaptáveis. Além disso, mostra um exemplo para criar uma aparência personalizada para que o componente de campo numérico apareça como um passo ou controle deslizante numérico.

Vamos primeiro analisar os termos e conceitos principais usados neste artigo.

**Aparência** Refere-se ao estilo, aparência e comportamento e à organização de vários elementos de um campo de formulário adaptável. Geralmente inclui um rótulo, uma área interativa para fornecer entradas, um ícone de ajuda e descrições curtas e longas do campo. A personalização da aparência discutida neste artigo é aplicável para a aparência da área de entrada do campo.

**Plug-in do jQuery** Fornece um mecanismo padrão, baseado na estrutura do widget jQuery, para implementar uma aparência alternativa.

**ClientLib** Um sistema de bibliotecas do lado do cliente em AEM processamento no lado do cliente, orientado por códigos complexos de JavaScript e CSS. Para obter mais informações, consulte Usar bibliotecas do lado do cliente.

**Arquétipo** Um kit de ferramentas de modelo de projeto Maven definido como um padrão ou modelo original para projetos Maven. Para obter mais informações, consulte Introdução aos arquétipos.

**Controle do usuário** Refere-se ao elemento principal em um widget que contém o valor do campo e é usado pela estrutura de aparência para vincular a interface do usuário de widget personalizada ao modelo de formulário adaptável.

## Etapas para criar uma aparência personalizada {#steps-to-create-a-custom-appearance}

As etapas, em um alto nível, para criar uma aparência personalizada são as seguintes:

1. **Criar um projeto**: Crie um projeto Maven que gera um pacote de conteúdo para implantar no AEM.
1. **Estender uma classe de widget existente**: Estender uma classe de widget existente e substituir as classes necessárias.
1. **Criar uma biblioteca do cliente**: Crie um `clientLib: af.customwidget` e adicione os arquivos JavaScript e CSS necessários.

1. **Criar e instalar o projeto**: Crie o projeto Maven e instale o pacote de conteúdo gerado no AEM.
1. **Atualizar o formulário adaptável**: Atualize as propriedades dos campos de formulário adaptáveis para usar a aparência personalizada.

### Criar um projeto {#create-a-project}

Um arquétipo maven é um ponto de partida para a criação de uma aparência personalizada. Os detalhes do arquétipo a ser usado são os seguintes:

* **Repositório**: https://repo1.maven.org/maven2/com/adobe/
* **Id Do Artefato**: custom-appearance-archetype
* **ID do Grupo**: com.adobe.aemforms
* **Versão**: 1.0.4

Execute o seguinte comando para criar um projeto local com base no arquétipo:

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

O comando baixa os plug-ins e as informações do arquétipo do Maven do repositório e gera um projeto com base nas seguintes informações:

* **groupId**: ID de grupo usada pelo projeto Maven gerado
* **artifactId**: ID de artefato usada pelo projeto Maven gerado.
* **version**: Versão do projeto Maven gerado.
* **pacote**: Pacote usado para a estrutura do arquivo.
* **artifactName**: Nome do artefato do pacote de AEM gerado.
* **packageGroup**: Grupo de pacotes do pacote de AEM gerado.
* **widgetName**: Nome de aparência usado para referência.

O projeto gerado tem a seguinte estrutura:

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### Estender uma classe de widget existente {#extend-an-existing-widget-class}

Depois que o modelo do projeto for criado, faça as seguintes alterações, conforme necessário:

1. Inclua a dependência de plug-in de terceiros no projeto.

   1. Coloque os plug-ins jQuery de terceiros ou personalizados no `jqueryplugin/javascript` pasta e arquivos CSS relacionados na `jqueryplugin/css` pasta. Para obter mais detalhes, consulte os arquivos JS e CSS na seção `jqueryplugin/javascript and jqueryplugin/css` pasta.

   1. Modifique o `js.txt` e `css.txt` arquivos para incluir qualquer arquivo JavaScript e CSS adicional do plug-in jQuery.

1. Integre o plug-in de terceiros à estrutura para permitir a interação entre a estrutura de aparência personalizada e o plug-in jQuery. O novo widget será funcional somente após estender ou substituir as seguintes funções.

<table>
 <tbody>
  <tr>
   <td><strong>Função</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>A função de renderização retorna o objeto jQuery para o elemento HTML padrão do widget. O elemento HTML padrão deve ser do tipo focalizável. Por exemplo, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>e <code>&lt;li&gt;</code>. O elemento retornado é usado como <code>$userControl</code>. Se a variável <code>$userControl</code> especifica a restrição acima, as funções da variável <code>AbstractWidget</code> funcionam como esperado, caso contrário, algumas das APIs comuns (foco, clique) exigem alterações. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Retorna um mapa para converter eventos HTML em eventos XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Este exemplo mostra que <code>blur</code> é um evento HTML e <code>XFA_EXIT_EVENT</code> é o evento XFA correspondente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Retorna um mapa que fornece detalhes sobre a ação a ser executada na alteração de uma opção. As chaves são as opções fornecidas para o widget e os valores são funções que são chamadas sempre que uma alteração na opção é detectada. O widget fornece manipuladores para todas as opções comuns (exceto <code>value</code> e <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>A estrutura do widget jQuery carrega a função sempre que o valor do widget jQuery é salvo no modelo XFA (por exemplo, no evento exit de um campo de texto). A implementação deve retornar o valor salvo no widget. O manipulador é fornecido com o novo valor para a opção .</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Por padrão, no XFA no evento enter, a variável <code>rawValue</code> do campo é exibido. Essa função é chamada para mostrar a variável <code>rawValue</code> ao usuário. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Por padrão, no evento XFA na saída, a variável <code>formattedValue</code> do campo é exibido. Essa função é chamada para mostrar a variável <code>formattedValue</code> ao usuário. </td>
  </tr>
 </tbody>
</table>

1. Atualize o arquivo JavaScript no `integration/javascript` , conforme necessário.

   * Substituir o texto `__widgetName__` com o nome real do widget.
   * Estenda o widget a partir de uma classe de widget pronta para uso adequada. Na maioria dos casos, é a classe de widget correspondente ao widget existente que está sendo substituído. O nome da classe pai é usado em vários locais, portanto, é recomendável procurar por todas as instâncias da cadeia de caracteres `xfaWidget.textField` no arquivo e substitua-os pela classe pai real usada.
   * Estender o `render` para fornecer uma interface alternativa. É o local de onde o plug-in jQuery será chamado para atualizar a interface do usuário ou o comportamento de interação. O `render` deve retornar um elemento de controle de usuário.

   * Estender o `getOptionsMap` para substituir qualquer configuração de opção afetada devido a uma alteração no widget. A função retorna um mapeamento que fornece detalhes para a ação ser executada na alteração de uma opção. As chaves são as opções fornecidas para o widget e os valores são as funções chamadas sempre que uma alteração na opção é detectada.
   * O `getEventMap` O método mapeia eventos acionados pelo widget, com os eventos exigidos pelo modelo de formulário adaptável. O valor padrão mapeia eventos HTML padrão para o widget padrão e precisa ser atualizado se um evento alternativo for acionado.
   * O `showDisplayValue` e `showValue` aplique a cláusula de exibição e edição de imagem e pode ser substituída para ter um comportamento alternativo.

   * O `getCommitValue` é chamado pela estrutura de formulários adaptáveis quando a variável `commit`ocorre. Geralmente, é o evento exit, exceto para os elementos suspensos, de botão de opção e de caixa de seleção, onde ocorre durante a mudança). Para obter mais informações, consulte [Expressões adaptáveis do Forms](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * O arquivo de modelo fornece a implementação de exemplo para vários métodos. Remova os métodos que não devem ser estendidos.

### Criar uma biblioteca do cliente {#create-a-client-library}

O projeto de amostra gerado pelo arquétipo Maven cria automaticamente as bibliotecas de clientes necessárias e as envolve em uma biblioteca de clientes com uma categoria `af.customwidgets`. Os arquivos JavaScript e CSS disponíveis no `af.customwidgets` são incluídas automaticamente no tempo de execução.

### Criar e instalar {#build-and-install}

Para criar o projeto, execute o seguinte comando no shell para gerar um pacote CRX que precise ser instalado no servidor AEM.

`mvn clean install`

>[!NOTE]
>
>O projeto maven se refere a um repositório remoto dentro do arquivo POM. Isso é somente para fins de referência e, de acordo com os padrões Maven, as informações do repositório são capturadas na variável `settings.xml` arquivo.

### Atualizar o formulário adaptável {#update-the-adaptive-form}

Para aplicar a aparência personalizada a um campo de formulário adaptável:

1. Abra o formulário adaptável no modo de edição.
1. Abra o **Propriedade** para o campo no qual você deseja aplicar a aparência personalizada.
1. No **Estilo** , atualize a guia `CSS class` para adicionar o nome da aparência na `widget_<widgetName>` formato. Por exemplo: **widget_numericstep**

## Exemplo: Criar uma aparência personalizada   {#sample-create-a-custom-appearance-nbsp}

Agora vamos observar um exemplo para criar uma aparência personalizada para que um campo numérico apareça como um passo ou controle deslizante numérico. Execute as seguintes etapas:

1. Execute o seguinte comando para criar um projeto local com base no arquétipo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Ele solicita que você especifique valores para os seguintes parâmetros.
   *Os valores usados nessa amostra são realçados em negrito*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Navegue até o `customWidgets` (valor especificado para a variável `artifactID` e execute o seguinte comando para gerar um projeto Eclipse:

   `mvn eclipse:eclipse`

1. Abra a ferramenta Eclipse e faça o seguinte para importar o projeto Eclipse:

   1. Selecionar **[!UICONTROL Arquivo > Importar > Projetos existentes no Workspace]**.

   1. Procure e selecione a pasta onde você executou o `archetype:generate` comando.

   1. Clique em **[!UICONTROL Concluir]**.

      ![captura de tela do eclipse](assets/eclipse-screenshot.png)

1. Selecione o widget a ser usado para a aparência personalizada. Este exemplo usa o seguinte widget de etapa numérica:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   No projeto do Eclipse, revise o código do plug-in no `plugin.js` para garantir que corresponda aos requisitos para a aparência. Nesta amostra, a aparência cumpre os seguintes requisitos:

   * O passo numérico deve se estender de `- $.xfaWidget.numericInput`.
   * O `set value` O método do widget define o valor após o foco estar no campo. É um requisito obrigatório para um widget de formulário adaptável.
   * O `render` deve ser substituído para chamar o método `bootstrapNumber` método .

   * Não há dependência adicional para o plug-in que não seja o código-fonte principal do plug-in.
   * A amostra não executa nenhum estilo na etapa, portanto, nenhum CSS adicional é necessário.
   * O `$userControl` deve estar disponível para a variável `render` método . É um campo da variável `text` tipo que é clonado com o código do plug-in.

   * O **+** e **-** botões devem ser desativados quando o campo estiver desativado.

1. Substitua o conteúdo da variável `bootstrap-number-input.js` (plugin jQuery) com o conteúdo do `numericStepper-plugin.js` arquivo.
1. No `numericStepper-widget.js` , adicione o seguinte código para substituir o método de renderização para chamar o plug-in e retornar o `$userControl` objeto:

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. No `numericStepper-widget.js` , substitua o `getOptionsMap` para substituir a opção de acesso e ocultar os botões + e - no modo desativado.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. Salve as alterações, navegue até a pasta que contém a variável `pom.xml` e execute o seguinte comando Maven para criar o projeto:

   `mvn clean install`

1. Instale o pacote usando o Gerenciador de pacotes AEM.

1. Abra o formulário adaptável no modo de edição no qual deseja aplicar a aparência personalizada e faça o seguinte:

   1. Clique com o botão direito do mouse no campo no qual deseja aplicar a aparência e clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo Editar componente .

   1. Na guia Estilo , atualize o **[!UICONTROL Classe CSS]** propriedade a ser adicionada `widget_numericStepper`.

A nova aparência que você acabou de criar está disponível para uso.
