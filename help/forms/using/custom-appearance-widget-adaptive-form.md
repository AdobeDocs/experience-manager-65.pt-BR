---
title: Criar aparências personalizadas para campos de formulário adaptáveis
description: Personalize a aparência dos componentes prontos para uso no Adaptive Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# Criar aparências personalizadas para campos de formulário adaptáveis{#create-custom-appearances-for-adaptive-form-fields}

## Introdução {#introduction}

Os formulários adaptáveis usam a [estrutura de aparência](/help/forms/using/introduction-widgets.md) para ajudar você a criar aparências personalizadas para campos de formulários adaptáveis e fornecer uma experiência de usuário diferente. Por exemplo, substitua botões de opção e caixas de seleção por botões de alternância ou use plug-ins personalizados do jQuery para restringir as entradas dos usuários em campos como números de telefone ou ID de email.

Este documento explica como usar um plug-in jQuery para criar essas experiências alternativas para campos de formulário adaptáveis. Além disso, mostra um exemplo para criar uma aparência personalizada para que o componente de campo numérico apareça como um seletor ou passo numérico.

Primeiro, vamos analisar os termos e conceitos principais usados neste artigo.

**Aparência** refere-se ao estilo, aparência e comportamento e organização de vários elementos de um campo de formulário adaptável. Geralmente inclui um rótulo, uma área interativa para fornecer entradas, um ícone de ajuda e descrições curtas e longas do campo. A personalização da aparência discutida neste artigo é aplicável à aparência da área de entrada do campo.

O **plug-in jQuery** fornece um mecanismo padrão, baseado na estrutura de widget jQuery, para implementar uma aparência alternativa.

**ClientLib** Um sistema de bibliotecas do lado do cliente no processamento AEM do lado do cliente orientado por código JavaScript e CSS complexo. Para obter mais informações, consulte Uso de bibliotecas do lado do cliente.

**Arquétipo** Um kit de ferramentas de modelos de projeto Maven definido como um padrão ou modelo original para projetos Maven. Para obter mais informações, consulte Introdução aos arquétipos.

**Controle de Usuário** Refere-se ao elemento principal em um widget que contém o valor do campo e é usado pela estrutura de aparência para associar a interface de widget personalizada ao modelo de formulário adaptável.

## Etapas para criar uma aparência personalizada {#steps-to-create-a-custom-appearance}

As etapas, em um alto nível, para criar uma aparência personalizada são as seguintes:

1. **Criar um projeto**: crie um projeto Maven que gere um pacote de conteúdo para implantar no AEM.
1. **Estender uma classe de widget existente**: estender uma classe de widget existente e substituir as classes necessárias.
1. **Criar uma biblioteca do cliente**: criar uma biblioteca `clientLib: af.customwidget` e adicionar os arquivos JavaScript e CSS necessários.

1. **Criar e instalar o projeto**: criar o projeto Maven e instalar o pacote de conteúdo gerado no AEM.
1. **Atualizar o formulário adaptável**: atualize as propriedades do campo de formulário adaptável para usar a aparência personalizada.

### Criar um projeto {#create-a-project}

Um arquétipo maven é um ponto de partida para criar uma aparência personalizada. Os detalhes do arquétipo a ser usado são os seguintes:

* **Repositório**: https://repo1.maven.org/maven2/com/adobe/
* **Id do artefato**: custom-appearance-archetype
* **Id do Grupo**: com.adobe.aemforms
* **Versão**: 1.0.4

Execute o seguinte comando para criar um projeto local com base no arquétipo:

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

O comando baixa as informações dos plug-ins Maven e do arquétipo no repositório e gera um projeto com base nas seguintes informações:

* **groupId**: ID de grupo usada pelo projeto Maven gerado
* **artifactId**: ID de artefato usada pelo projeto Maven gerado.
* **versão**: versão para o projeto Maven gerado.
* **pacote**: pacote usado para a estrutura de arquivo.
* **artifactName**: nome do artefato do pacote AEM gerado.
* **packageGroup**: grupo do pacote do AEM gerado.
* **widgetName**: nome da aparência usado para referência.

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

   1. Coloque os plug-ins de terceiros ou personalizados do jQuery na pasta `jqueryplugin/javascript` e nos arquivos CSS relacionados na pasta `jqueryplugin/css`. Para obter mais detalhes, consulte os arquivos JS e CSS na pasta `jqueryplugin/javascript and jqueryplugin/css`.

   1. Modifique os arquivos `js.txt` e `css.txt` para incluir qualquer arquivo JavaScript e CSS adicional do plug-in jQuery.

1. Integre o plug-in de terceiros à estrutura para permitir a interação entre a estrutura de aparência personalizada e o plug-in jQuery. O novo widget só funcionará depois que você estender ou substituir as funções a seguir.

<table>
 <tbody>
  <tr>
   <td><strong>Função</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>A função de renderização retorna o objeto jQuery para o elemento de HTML padrão do widget. O elemento de HTML padrão deve ser do tipo focalizável. Por exemplo, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code> e <code>&lt;li&gt;</code>. O elemento retornado é usado como <code>$userControl</code>. Se <code>$userControl</code> especificar a restrição acima, as funções da classe <code>AbstractWidget</code> funcionarão como esperado, caso contrário algumas das APIs comuns (foco, clique) exigirão alterações. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Retorna um mapa para converter eventos HTML em eventos XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Este exemplo mostra que <code>blur</code> é um evento HTML e <code>XFA_EXIT_EVENT</code> é o evento XFA correspondente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Retorna um mapa que fornece detalhes sobre a ação a ser executada na alteração de uma opção. As teclas são as opções fornecidas ao widget e os valores são funções chamadas sempre que uma alteração na opção é detectada. O widget fornece manipuladores para todas as opções comuns (exceto <code>value</code> e <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>A estrutura do widget jQuery carrega a função sempre que o valor do widget jQuery é salvo no modelo XFA (por exemplo, no evento de saída de um campo de texto). A implementação deve retornar o valor salvo no widget. O manipulador recebe o novo valor da opção.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Por padrão, no XFA em inserir evento, o <code>rawValue</code> do campo é exibido. Esta função é chamada para mostrar <code>rawValue</code> ao usuário. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Por padrão, no XFA no evento de saída, o <code>formattedValue</code> do campo é exibido. Esta função é chamada para mostrar <code>formattedValue</code> ao usuário. </td>
  </tr>
 </tbody>
</table>

1. Atualize o arquivo JavaScript na pasta `integration/javascript`, conforme necessário.

   * Substituir o texto `__widgetName__` pelo nome real do widget.
   * Estenda o widget de uma classe de widget pronta para uso adequada. Na maioria dos casos, é a classe do widget correspondente ao widget existente que está sendo substituído. O nome da classe pai é usado em vários locais, portanto, é recomendável procurar todas as instâncias da cadeia de caracteres `xfaWidget.textField` no arquivo e substituí-las pela classe pai real usada.
   * Estenda o método `render` para fornecer uma interface alternativa. É o local de onde o plug-in jQuery será chamado para atualizar a interface ou o comportamento de interação. O método `render` deve retornar um elemento de controle de usuário.

   * Estenda o método `getOptionsMap` para substituir qualquer configuração de opção afetada devido a uma alteração no widget. A função retorna um mapeamento que fornece detalhes da ação a ser executada ao alterar uma opção. As teclas são as opções fornecidas ao widget e os valores são as funções chamadas sempre que uma alteração na opção é detectada.
   * O método `getEventMap` mapeia eventos acionados pelo widget, com os eventos exigidos pelo modelo de formulário adaptável. O valor padrão mapeia eventos HTML padrão para o widget padrão e precisa ser atualizado se um evento alternativo for acionado.
   * `showDisplayValue` e `showValue` aplicam a cláusula de exibição e edição de imagem e podem ser substituídas para terem um comportamento alternativo.

   * O método `getCommitValue` é chamado pela estrutura de formulários adaptáveis quando o evento `commit` ocorre. Geralmente, é o evento de saída, exceto os elementos de lista suspensa, botão de opção e caixa de seleção (onde ocorre na alteração). Para obter mais informações, consulte [Expressões Forms adaptáveis](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * O arquivo de modelo fornece uma implementação de amostra para vários métodos. Remova os métodos que não devem ser estendidos.

### Criar uma biblioteca do cliente {#create-a-client-library}

O projeto de amostra gerado pelo arquétipo Maven cria automaticamente as bibliotecas de clientes necessárias e as envolve em uma biblioteca de clientes com uma categoria `af.customwidgets`. Os arquivos JavaScript e CSS disponíveis no `af.customwidgets` são incluídos automaticamente em tempo de execução.

### Criar e instalar {#build-and-install}

Para construir o projeto, execute o seguinte comando no shell para gerar um pacote do CRX que precise ser instalado no servidor AEM.

`mvn clean install`

>[!NOTE]
>
>O projeto maven se refere a um repositório remoto dentro do arquivo POM. Isso é apenas para fins de referência e, de acordo com os padrões Maven, as informações do repositório são capturadas no arquivo `settings.xml`.

### Atualizar o formulário adaptável {#update-the-adaptive-form}

Para aplicar a aparência personalizada a um campo de formulário adaptável:

1. Abra o formulário adaptável no modo de edição.
1. Abra a caixa de diálogo **Propriedade** para o campo no qual você deseja aplicar a aparência personalizada.
1. Na guia **Estilo**, atualize a propriedade `CSS class` para adicionar o nome de aparência no formato `widget_<widgetName>`. Por exemplo: **widget_numericstepper**

## Amostra: Criar uma aparência personalizada   {#sample-create-a-custom-appearance-nbsp}

Agora vamos ver um exemplo para criar uma aparência personalizada para que um campo numérico apareça como um seletor ou passo numérico. Execute as seguintes etapas:

1. Execute o seguinte comando para criar um projeto local com base no arquétipo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Ele solicita que você especifique valores para os parâmetros a seguir.
   *Os valores usados nesta amostra estão realçados em negrito*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Navegue até o diretório `customWidgets` (valor especificado para a propriedade `artifactID`) e execute o seguinte comando para gerar um projeto Eclipse:

   `mvn eclipse:eclipse`

1. Abra a ferramenta Eclipse e faça o seguinte para importar o projeto Eclipse:

   1. Selecione **[!UICONTROL Arquivo > Importar > Projetos existentes no Workspace]**.

   1. Procure e selecione a pasta onde você executou o comando `archetype:generate`.

   1. Clique em **[!UICONTROL Concluir]**.

      ![captura de tela do eclipse](assets/eclipse-screenshot.png)

1. Selecione o widget a ser usado para a aparência personalizada. Este exemplo usa o seguinte widget de passo numérico:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   No projeto Eclipse, revise o código do plug-in no arquivo `plugin.js` para garantir que ele corresponda aos requisitos da aparência. Nesta amostra, o aspecto preenche os seguintes requisitos:

   * O escalonador numérico deve se estender de `- $.xfaWidget.numericInput`.
   * O método `set value` do widget define o valor depois que o foco está no campo. É um requisito obrigatório para um widget de formulário adaptável.
   * O método `render` precisa ser substituído para invocar o método `bootstrapNumber`.

   * Não há dependência adicional para o plug-in além do código-fonte principal do plug-in.
   * A amostra não executa nenhum estilo no depurador, portanto, nenhum CSS adicional é necessário.
   * O objeto `$userControl` deve estar disponível para o método `render`. É um campo do tipo `text` que é clonado com o código do plug-in.

   * Os botões **+** e **-** devem ser desabilitados quando o campo estiver desabilitado.

1. Substitua o conteúdo de `bootstrap-number-input.js` (plug-in jQuery) pelo conteúdo do arquivo `numericStepper-plugin.js`.
1. No arquivo `numericStepper-widget.js`, adicione o seguinte código para substituir o método de renderização para invocar o plug-in e retornar o objeto `$userControl`:

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

1. No arquivo `numericStepper-widget.js`, substitua a propriedade `getOptionsMap` para substituir a opção de acesso e oculte os botões + e - no modo desabilitado.

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

1. Salve as alterações, navegue até a pasta que contém o arquivo `pom.xml` e execute o seguinte comando Maven para criar o projeto:

   `mvn clean install`

1. Instale o pacote usando o Gerenciador de pacotes AEM.

1. Abra o formulário adaptável no modo de edição no qual deseja aplicar a aparência personalizada e faça o seguinte:

   1. Clique com o botão direito do mouse no campo no qual deseja aplicar a aparência e clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo Editar Componente.

   1. Na guia Estilo, atualize a propriedade **[!UICONTROL classe CSS]** para adicionar `widget_numericStepper`.

A nova aparência criada agora está disponível para uso.
