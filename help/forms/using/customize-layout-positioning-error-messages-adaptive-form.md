---
title: Personalizar o layout e o posicionamento das mensagens de erro de um formulário adaptável
description: É possível personalizar o layout e o posicionamento das mensagens de erro de um adaptável para.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Personalizar o layout e o posicionamento das mensagens de erro de um formulário adaptável{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

Você pode personalizar o layout e o posicionamento das mensagens de erro de um formulário adaptável. Você pode executar as seguintes personalizações:

* Personalizar a localização e o layout da legenda de um campo sem alterar as propriedades CSS correspondentes
* Personalizar a posição das mensagens de erro em linha
* Personalizar conteúdo do indicador de ajuda dinâmica
* Personalize a posição dos componentes do campo (legenda, widget, descrição curta, descrição longa e indicadores de ajuda) sem alterar as propriedades CSS correspondentes

## Personalizar o layout dos campos {#customize-layout-of-fields}

É possível personalizar o layout de um único campo ou de todos os campos para alterar a posição da legenda e das mensagens de erro.

Para aplicar um layout personalizado a um campo, faça o seguinte:

### Personalizar o layout de um único campo {#customize-layout-of-a-single-field}

1. Abra o formulário no **Estilo** modo. Para abrir o formulário no modo de estilo, selecione na barra de ferramentas da página ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.
1. Na barra lateral, em **Objetos de formulário**, selecione o campo e selecione o botão editar ![botão editar](assets/edit-button.png).
1. Selecione o estado do campo que deseja personalizar e especifique o estilo desse estado.

   ![Especificação do estilo em linha de um campo](assets/edit-error-state.png)

### Personalizar o layout de todos os campos de um formulário {#customize-layout-of-all-the-fields-of-a-form}

Com o AEM Forms, agora é possível criar um tema e aplicá-lo ao formulário. O editor de temas permite especificar o estilo dos componentes de formulário em um local. Ao criar um tema, você especifica o estilo em um nível de componente. Para obter mais informações sobre temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

Crie um tema usando o Editor de temas para personalizar o layout de todos os campos no formulário. Depois de criar um tema, execute as seguintes etapas para aplicá-lo a um formulário:

1. Abra o formulário no modo de edição.
1. No modo de edição, selecione um componente e selecione ![nível de campo](assets/field-level.png) > **Contêiner de formulário adaptável** e selecione ![cmppr](assets/cmppr.png).
1. Na barra lateral, em Tema do formulário adaptável, selecione o tema criado usando o Editor de temas.

## Criar um layout de campo personalizado {#create-a-custom-field-layout}

1. Abra o CRXDE Lite. O URL padrão é https://&#39;[server]:[porta]&quot;/crx/de.
1. Copie um layout de campo do nó /libs/fd/af/layouts/field (Por exemplo, defaultFieldLayout) para o nó /apps (Por exemplo, /apps/af-field-layout).
1. Renomeie o nó copiado e o arquivo defaultFieldLayout.jsp. Por exemplo, errorOnRight.jsp.

1. Altere o valor das propriedades qtip e jcr:description do nó copiado. Por exemplo, altere o valor das propriedades para Error On Right

1. Para adicionar novos estilos e comportamento, crie uma biblioteca do cliente no nó /etc.

   Por exemplo, no local /etc/af-field-layout-clientlib, crie o nó client-library. Adicione a propriedade categories com o valor af.field.errorOnRight e o arquivo style.less com o seguinte código:

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
1. Abra a caixa de diálogo de edição do campo e selecione a **Estilo** guia. No **Configurar layout do campo** selecione o layout recém-criado e clique em **OK**.

O pacote ErrorOnRight.zip contém o código para mostrar mensagens de erro no lado direito dos campos.

[Obter arquivo](assets/erroronright.zip)
