---
title: Configure o RTE para vários editores no local.
description: Crie vários editores no local no Adobe Experience Manager configurando o Editor de Rich Text.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Configurar vários editores no local {#configure-multiple-in-place-editors}

Você pode configurar o Editor de Rich Text no Adobe Experience Manager para que ele tenha vários editores no local. Quando configurado, é possível selecionar o conteúdo apropriado e abrir o editor apropriado.

![Um editor local específico](assets/rte-inplace-editor.png)

## Configurar vários editores {#configure-multiple-editors}

Para ativar vários editores no local, a estrutura de um `cq:InplaceEditingConfig` o tipo de nó foi aprimorado com a definição de `cq:ChildEditorConfig` tipo de nó.

Por exemplo:

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Para configurar vários editores, siga estas etapas:

1. No nó `cq:inplaceEditing` de tipo `cq:InplaceEditingConfig`) defina as seguintes propriedades:

   * Nome:`editorType`
   * Tipo: `String`
   * Valor: `hybrid`

1. Nesse nó, crie um nó:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. Em `cq:childEditors` , crie um nó para cada editor local:

   * Nome: O nome de cada nó é o nome da propriedade que ele representa, como ocorre com os destinos de soltar. Por exemplo, `image` e `text`.
   * Tipo: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Há uma correlação entre os destinos de soltar definidos e os editores filhos. O nome do `cq:ChildEditorConfig` é considerado como a ID de destino de soltar, para uso como parâmetro para o editor secundário selecionado. Se a subárea editável não tiver um destino de soltar, por exemplo, em um componente de texto, o nome do editor secundário ainda será considerado uma ID para identificar a área editável correspondente.

1. Em cada um desses nós (`cq:ChildEditorConfig`) defina as propriedades:

   * Nome: `type`.
   * Valor: O nome do editor no local registrado; por exemplo, `image` e `text`.

   * Nome: `title`.
   * Valor: O título exibido na lista de seleção de componentes dos editores disponíveis. Por exemplo, `Image` e `Text`.

### Configuração adicional para editores de Rich Text {#additional-configuration-for-rich-text-editors}

A configuração de vários editores de rich text é um pouco diferente, pois é possível configurar cada instância do RTE individual separadamente. Para obter detalhes, consulte [configurar o Editor de Rich Text](/help/sites-administering/rich-text-editor.md). Para ter vários RTEs, crie uma configuração para cada RTE no local. O Adobe recomenda criar o novo nó de configuração em `cq:InplaceEditingConfig` como cada RTE individual pode ter uma configuração diferente. No novo nó , crie cada configuração de RTE individual.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>No entanto, para o RTE, a variável `configPath` é suportada quando há apenas uma instância do editor de texto (sub-área editável) no componente. Esse uso de `configPath` é fornecido para oferecer suporte à compatibilidade com versões anteriores das caixas de diálogo da interface do usuário do componente.

>[!CAUTION]
>
>Não nomeie o nó de configuração do RTE como `config`. Caso contrário, as configurações do RTE estarão disponíveis apenas para os administradores e não para os usuários do grupo `content-author`.

## Exemplos de código {#code-samples}

Você pode encontrar o código desta página em [projeto aem-authoring-hybrideditors no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Você pode baixar o projeto completo como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Adicionar um editor no local {#add-an-in-place-editor}

Para obter informações gerais sobre como adicionar um editor no local, consulte o documento [personalizar criação de página](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configurar o editor de rich text no Experience Manager](/help/sites-administering/rich-text-editor.md).

