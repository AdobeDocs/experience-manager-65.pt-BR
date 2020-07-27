---
title: Criar aparências personalizadas para campos de formulário adaptáveis
seo-title: Criar aparências personalizadas para campos de formulário adaptáveis
description: Personalize a aparência dos componentes prontos para uso nos Formulários adaptativos.
seo-description: Personalize a aparência dos componentes prontos para uso nos Formulários adaptativos.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 0%

---


# Criar aparências personalizadas para campos de formulário adaptáveis{#create-custom-appearances-for-adaptive-form-fields}

## Introdução {#introduction}

Formulários adaptáveis aproveitam a estrutura [de](/help/forms/using/introduction-widgets.md) aparência para ajudá-lo a criar aparências personalizadas para campos de formulário adaptáveis e fornecer uma experiência diferente ao usuário. Por exemplo, substitua botões de opção e caixas de seleção por botões de alternância ou use plug-ins jQuery personalizados para restringir as entradas de usuários em campos como números de telefone ou ID de email.

Este documento explica como usar um plug-in do jQuery para criar essas experiências alternativas para campos de formulário adaptáveis. Além disso, exibe um exemplo para criar uma aparência personalizada para que o componente de campo numérico apareça como um auxiliar numérico ou um controle deslizante.

Vamos primeiro ver os termos e conceitos principais usados neste artigo.

**Aparência** Refere-se ao estilo, aparência e comportamento e organização de vários elementos de um campo de formulário adaptável. Geralmente inclui um rótulo, uma área interativa para fornecer entradas, um ícone de ajuda e descrições curtas e longas do campo. A personalização da aparência discutida neste artigo é aplicável à aparência da área de entrada do campo.

**Plug-in** jQuery Fornece um mecanismo padrão, baseado na estrutura do widget jQuery, para implementar uma aparência alternativa.

**ClientLib** Um sistema de bibliotecas do lado do cliente no processamento do lado do cliente AEM, controlado por complexos códigos JavaScript e CSS. Para obter mais informações, consulte Usar bibliotecas do lado do cliente.

**Archetype** Um kit de ferramentas de modelo de projeto Maven definido como um padrão ou modelo original para projetos Maven. Para obter mais informações, consulte Introdução aos arquétipos.

**Controle** do usuárioRefere-se ao elemento principal em um widget que contém o valor do campo e é usado pela estrutura de aparência para vincular a interface do usuário do widget personalizado ao modelo de formulário adaptável.

## Etapas para criar uma aparência personalizada {#steps-to-create-a-custom-appearance}

As etapas, em alto nível, para criar uma aparência personalizada são as seguintes:

1. **Criar um projeto**: Crie um projeto Maven que gera um pacote de conteúdo para implantar no AEM.
1. **Estende uma classe** de widget existente: Estende uma classe de widget existente e substitui as classes necessárias.
1. **Criar uma biblioteca** de clientes: Crie uma `clientLib: af.customwidget` biblioteca e adicione os arquivos JavaScript e CSS necessários.

1. **Crie e instale o projeto**: Crie o projeto Maven e instale o pacote de conteúdo gerado no AEM.
1. **Atualize o formulário** adaptável: Atualize as propriedades de campos de formulário adaptáveis para usar a aparência personalizada.

### Criar um projeto {#create-a-project}

Um arquétipo maven é um ponto de partida para a criação de uma aparência personalizada. Os detalhes do arquétipo a utilizar são os seguintes:

* **Repositório**: https://repo.adobe.com/nexus/content/groups/public/
* **Id** do artefato: custom-appearance-archetype
* **Id** do grupo: com.adobe.aemforms
* **Versão**: 1.0.4.

Execute o seguinte comando para criar um projeto local com base no arquétipo:

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

O comando baixa os plug-ins Maven e as informações de tipo de arquivo do repositório e gera um projeto com base nas seguintes informações:

* **groupId**: ID do grupo usada pelo projeto Maven gerado
* **artefatoId**: ID de artefato usada pelo projeto Maven gerado.
* **versão**: Versão do projeto Maven gerado.
* **pacote**: Pacote usado para a estrutura do arquivo.
* **artefatoName**: Nome do artefato do pacote AEM gerado.
* **packageGroup**: Grupo de pacotes do pacote AEM gerado.
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

Depois que o modelo de projeto for criado, faça as seguintes alterações, conforme necessário:

1. Inclua a dependência do plug-in de terceiros no projeto.

   1. Coloque os plug-ins jQuery personalizados ou de terceiros na `jqueryplugin/javascript` pasta e os arquivos CSS relacionados na `jqueryplugin/css` pasta. Para obter mais detalhes, consulte os arquivos JS e CSS na `jqueryplugin/javascript and jqueryplugin/css` pasta.

   1. Modifique os arquivos `js.txt` e `css.txt` para incluir qualquer arquivo adicional JavaScript e CSS do plug-in jQuery.

1. Integre o plug-in de terceiros à estrutura para permitir a interação entre a estrutura de aparência personalizada e o plug-in jQuery. O novo widget estará funcional somente depois que você estender ou substituir as seguintes funções.

<table>
 <tbody>
  <tr>
   <td><strong>Função</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>A função de renderização retorna o objeto jQuery para o elemento HTML padrão do widget. O elemento HTML padrão deve ser do tipo focalizável. Por exemplo, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>e <code>&lt;li&gt;</code>. O elemento retornado é usado como <code>$userControl</code>. Se a restrição <code>$userControl</code> especificar acima, as funções da <code>AbstractWidget</code> classe funcionarão conforme esperado, caso contrário, algumas das APIs comuns (foco, clique) exigirão alterações. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Retorna um mapa para converter eventos HTML em eventos XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Este exemplo mostra que <code>blur</code> é um evento HTML e <code>XFA_EXIT_EVENT</code> é o evento XFA correspondente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Retorna um mapa que fornece detalhes sobre a ação a ser executada na alteração de uma opção. As teclas são as opções fornecidas para o widget e os valores são funções que são chamadas sempre que uma alteração na opção é detectada. O widget fornece manipuladores para todas as opções comuns (exceto <code>value</code> e <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>A estrutura do widget jQuery carrega a função sempre que o valor do widget jQuery é salvo no modelo XFA (por exemplo, no evento exit de um campo de texto). A implementação deve retornar o valor salvo no widget. O manipulador é fornecido com o novo valor para a opção.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Por padrão, no XFA ao inserir o evento, o campo <code>rawValue</code> é exibido. Essa função é chamada para mostrar o <code>rawValue</code> ao usuário. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Por padrão, no XFA ao sair do evento, o campo <code>formattedValue</code> é exibido. Essa função é chamada para mostrar o <code>formattedValue</code> ao usuário. </td>
  </tr>
 </tbody>
</table>

1. Atualize o arquivo JavaScript na `integration/javascript` pasta, conforme necessário.

   * Substitua o texto `__widgetName__` pelo nome do widget real.
   * Estenda o widget de uma classe de widget pronta para uso adequada. Na maioria dos casos, é a classe do widget correspondente ao widget existente que está sendo substituído. O nome da classe pai é usado em vários locais, portanto, é recomendável procurar todas as instâncias da string `xfaWidget.textField` no arquivo e substituí-las pela classe pai real usada.
   * Estenda o `render` método para fornecer uma interface alternativa. É o local de onde o plug-in jQuery será chamado para atualizar a interface do usuário ou o comportamento de interação. O `render` método deve retornar um elemento de controle de usuário.

   * Estende o `getOptionsMap` método para substituir qualquer configuração de opção afetada devido a uma alteração no widget. A função retorna um mapeamento que fornece detalhes para a ação ser executada quando uma opção é alterada. As teclas são as opções fornecidas ao widget e os valores são as funções chamadas sempre que uma alteração na opção é detectada.
   * O `getEventMap` método mapeia eventos acionados pelo widget, com os eventos exigidos pelo modelo de formulário adaptável. O valor padrão mapeia eventos HTML padrão para o widget padrão e precisa ser atualizado se um evento alternativo for acionado.
   * A cláusula de exibição `showDisplayValue` e edição de imagem é aplicada `showValue` e pode ser substituída para ter um comportamento alternativo.

   * O `getCommitValue` método é chamado pela estrutura de formulários adaptáveis quando o `commit`evento ocorre. Geralmente, é o evento exit, exceto para os elementos suspensos, botões de opção e caixas de seleção nos quais ocorre ao mudar). Para obter mais informações, consulte Expressões [de formulários](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)adaptáveis.

   * O arquivo de modelo fornece implementação de amostra para vários métodos. Remova os métodos que não devem ser estendidos.

### Criar uma biblioteca de cliente {#create-a-client-library}

O projeto de amostra gerado pelo arquétipo Maven cria automaticamente as bibliotecas do cliente necessárias e as envolve em uma biblioteca do cliente com uma categoria `af.customwidgets`. Os arquivos JavaScript e CSS disponíveis no `af.customwidgets` são incluídos automaticamente no tempo de execução.

### Criar e instalar {#build-and-install}

Para criar o projeto, execute o seguinte comando no shell para gerar um pacote CRX que precise ser instalado no servidor AEM.

`mvn clean install`

>[!NOTE]
>
>O projeto maven se refere a um repositório remoto dentro do arquivo POM. Isso é feito apenas para fins de referência e, de acordo com os padrões Maven, as informações do repositório são capturadas no `settings.xml` arquivo.

### Atualizar o formulário adaptável {#update-the-adaptive-form}

Para aplicar a aparência personalizada a um campo de formulário adaptável:

1. Abra o formulário adaptável no modo de edição.
1. Abra a caixa de diálogo **Propriedade** do campo no qual você deseja aplicar a aparência personalizada.
1. Na guia **Estilo** , atualize a `CSS class` propriedade para adicionar o nome da aparência no `widget_<widgetName>` formato. Por exemplo: **widget_numericstep**

## Amostra: Criar uma aparência personalizada   {#sample-create-a-custom-appearance-nbsp}

Agora vamos observar um exemplo para criar uma aparência personalizada para que um campo numérico apareça como uma revisão numérica ou um controle deslizante. Execute as seguintes etapas:

1. Execute o seguinte comando para criar um projeto local com base no arquétipo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Ela solicita que você especifique valores para os seguintes parâmetros.
   *Os valores usados nessa amostra são realçados em negrito*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Navegue até o diretório `customWidgets` (valor especificado para a `artifactID` propriedade) e execute o seguinte comando para gerar um projeto Eclipse:

   `mvn eclipse:eclipse`

1. Abra a ferramenta Eclipse e faça o seguinte para importar o projeto Eclipse:

   1. Selecione **[!UICONTROL Arquivo > Importar > Projetos existentes no Workspace]**.

   1. Procure e selecione a pasta na qual você executou o `archetype:generate` comando.

   1. Click **[!UICONTROL Finish]**.

      ![captura de tela do eclipse](assets/eclipse-screenshot.png)

1. Selecione o widget a ser usado para a aparência personalizada. Este exemplo usa o seguinte widget de revisão numérico:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   No projeto do Eclipse, reveja o código do plug-in no `plugin.js` arquivo para garantir que ele corresponda aos requisitos para a aparência. Nessa amostra, a aparência atende aos seguintes requisitos:

   * O passo numérico deve se estender de `- $.xfaWidget.numericInput`.
   * O `set value` método do widget define o valor após o foco estar no campo. É um requisito obrigatório para um widget de formulário adaptável.
   * O `render` método precisa ser substituído para chamar o `bootstrapNumber` método.

   * Não há nenhuma dependência adicional para o plug-in que não seja o código-fonte principal do plug-in.
   * A amostra não executa nenhum estilo na revisão, portanto, nenhum CSS adicional é necessário.
   * O `$userControl` objeto deve estar disponível para o `render` método. É um campo do `text` tipo clonado com o código do plug-in.

   * Os botões **+** e **-** devem ser desativados quando o campo estiver desativado.

1. Substitua o conteúdo do `bootstrap-number-input.js` (plug-in jQuery) pelo conteúdo do `numericStepper-plugin.js` arquivo.
1. No `numericStepper-widget.js` arquivo, adicione o seguinte código para substituir o método de renderização para chamar o plug-in e retornar o `$userControl` objeto:

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

1. No `numericStepper-widget.js` arquivo, substitua a `getOptionsMap` propriedade para substituir a opção de acesso e oculte os botões + e - no modo desativado.

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

1. Salve as alterações, navegue até a pasta que contém o `pom.xml` arquivo e execute o seguinte comando Maven para criar o projeto:

   `mvn clean install`

1. Instale o pacote usando o AEM Package Manager.

1. Abra o formulário adaptável no modo de edição no qual você deseja aplicar a aparência personalizada e faça o seguinte:

   1. Clique com o botão direito do mouse no campo no qual deseja aplicar a aparência e clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo Editar componente.

   1. Na guia Estilo, atualize a propriedade de classe **[!UICONTROL CSS a ser adicionada]** `widget_numericStepper`.

A nova aparência que você acabou de criar está disponível para uso.
