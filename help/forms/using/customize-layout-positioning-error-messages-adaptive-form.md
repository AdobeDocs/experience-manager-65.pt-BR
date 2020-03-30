---
title: Personalizar o layout e o posicionamento de mensagens de erro de um formulário adaptável
seo-title: Personalizar o layout e o posicionamento de mensagens de erro de um formulário adaptável
description: 'Você pode personalizar o layout e o posicionamento das mensagens de erro de um adaptador para. '
seo-description: 'Você pode personalizar o layout e o posicionamento das mensagens de erro de um adaptador para. '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Personalizar o layout e o posicionamento de mensagens de erro de um formulário adaptável{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

É possível personalizar o layout e o posicionamento das mensagens de erro de um formulário adaptável. Você pode executar as seguintes personalizações:

* Personalizar o local e o layout da legenda de um campo sem fazer qualquer alteração nas propriedades CSS correspondentes
* Personalizar a posição das mensagens de erro em linha
* Personalizar o conteúdo do indicador dinâmico de ajuda
* Personalizar a posição dos componentes de campo (legenda, widget, descrição curta, descrição longa e componentes do indicador de ajuda) sem fazer qualquer alteração nas propriedades de CSS correspondentes

## Personalizar o layout dos campos {#customize-layout-of-fields}

Você pode personalizar o layout de um único campo ou de todos os campos para alterar a posição da legenda e das mensagens de erro. Execute as seguintes etapas para aplicar um layout personalizado a um campo:

### Personalizar o layout de um único campo {#customize-layout-of-a-single-field}

Execute as seguintes etapas para aplicar um layout personalizado a um único campo:

1. Abra o formulário no modo **Estilo** . Para abrir o formulário no modo de estilo, na barra de ferramentas da página, toque em ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.
1. Na barra lateral, em Objetos **de** formulário, selecione o campo e toque no botão Editar, botão ![editar](assets/edit-button.png).
1. Selecione o estado do campo que deseja personalizar e especifique o estilo para esse estado.

   ![Especificação do estilo em linha de um campo](assets/edit-error-state.png)

### Personalizar o layout de todos os campos de um formulário {#customize-layout-of-all-the-fields-of-a-form}

Com o AEM Forms, agora é possível criar um tema e aplicá-lo ao formulário. O editor de temas permite especificar o estilo de componentes de formulário em um local. Ao criar um tema, especifique o estilo em um nível de componente. Para obter mais informações sobre temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

Crie um tema usando o Editor de Temas para personalizar o layout de todos os campos do formulário. Depois de criar um tema, execute as seguintes etapas para aplicá-lo a um formulário:

1. Abra o formulário no modo de edição.
1. No modo de edição, selecione um componente, em seguida, toque em nível ![de](assets/field-level.png) campo > Container **de formulário** adaptável e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, em Tema de formulário adaptável, selecione o tema que você criou usando o Editor de temas.

## Criar um layout de campo personalizado {#create-a-custom-field-layout}

1. Abra o CRXDE lite. O URL padrão é https://&#39;[server]:[port]&#39;/crx/de.
1. Copie um layout de campo do nó /libs/fd/af/layouts/field (Por exemplo, defaultFieldLayout) para o nó /apps (Por exemplo, /apps/af-field-layout).
1. Renomeie o nó copiado e o arquivo defaultFieldLayout.jsp. Por exemplo, errorOnRight.jsp.

1. Altere o valor das propriedades qtip e jcr:description do nó copiado. Por exemplo, altere o valor das propriedades para Erro à direita

1. Para adicionar novos estilos e comportamento, crie uma biblioteca de cliente no nó /etc.

   Por exemplo, no local /etc/af-field-layout-clientlib, crie o nó client-library. Adicione a propriedade categoria com o valor af.field.errorOnRight e o arquivo style.less com o seguinte código:

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. Para aprimorar a aparência e o comportamento, inclua a biblioteca do cliente criada no arquivo de layout (errorOnRight.jsp).
1. Abra a caixa de diálogo de edição do campo e selecione a guia **Estilo** . Na caixa suspensa **Configurar layout** de campo, selecione o layout recém-criado e clique em **OK**.

O pacote ErrorOnRight.zip contém código para mostrar mensagens de erro no lado direito dos campos.

[Obter arquivo](assets/erroronright.zip)
