---
title: Configurar o RTE para vários editores no local.
description: Crie vários editores no local no Adobe Experience Manager ao configurar o Editor de Rich Text.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Configurar vários editores no local {#configure-multiple-in-place-editors}

Você pode configurar o Editor de Rich Text no Adobe Experience Manager para que ele tenha vários editores no local. Quando configurado, é possível selecionar o conteúdo apropriado e abrir o editor apropriado.

![Um editor específico no local](assets/rte-inplace-editor.png)

## Configurar vários editores {#configure-multiple-editors}

Para habilitar vários editores no local, a estrutura de um tipo de nó `cq:InplaceEditingConfig` foi aprimorada com a definição do tipo de nó `cq:ChildEditorConfig`.

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

1. No nó `cq:inplaceEditing` (do tipo `cq:InplaceEditingConfig`), defina as seguintes propriedades:

   * Nome:`editorType`
   * Tipo: `String`
   * Valor: `hybrid`

1. Neste nó, crie um nó:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. No nó `cq:childEditors`, crie um nó para cada editor local:

   * Nome: O nome de cada nó é o nome da propriedade que ele representa, como ocorre com os destinos de eliminação. Por exemplo, `image` e `text`.
   * Tipo: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Há uma correlação entre os alvos de eliminação definidos e os editores filhos. O nome do nó `cq:ChildEditorConfig` é considerado como a ID de destino de lançamento, para uso como um parâmetro para o editor filho selecionado. Se a subárea editável não tiver um destino de soltar, por exemplo, em um componente de texto, o nome do editor filho ainda será considerado uma ID para identificar a área editável correspondente.

1. Em cada um desses nós (`cq:ChildEditorConfig`), defina as propriedades:

   * Nome: `type`.
   * Valor: o nome do editor registrado no local; por exemplo, `image` e `text`.

   * Nome: `title`.
   * Valor: o título exibido na lista de seleção de componentes dos editores disponíveis. Por exemplo, `Image` e `Text`.

### Configuração adicional para editores de rich text {#additional-configuration-for-rich-text-editors}

A configuração de vários editores de rich text é um pouco diferente, pois é possível configurar cada instância individual do RTE separadamente. Para obter detalhes, consulte [configurar o Editor de Rich Text](/help/sites-administering/rich-text-editor.md). Para ter vários RTEs, crie uma configuração para cada RTE no local. A Adobe recomenda criar o novo nó de configuração em `cq:InplaceEditingConfig`, pois cada RTE individual pode ter uma configuração diferente. No novo nó, crie cada configuração de RTE individual.

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
>No entanto, para o RTE, a propriedade `configPath` tem suporte quando há apenas uma instância do editor de texto (subárea editável) no componente. Este uso do `configPath` é fornecido para dar suporte à compatibilidade com versões anteriores das caixas de diálogo da interface do usuário do componente.

>[!CAUTION]
>
>Não nomeie o nó de configuração de RTE como `config`. Caso contrário, as configurações de RTE estarão disponíveis apenas para os administradores e não para os usuários no grupo `content-author`.

## Amostras de código {#code-samples}

Você pode encontrar o código desta página no [projeto aem-authoring-hybrideditors no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Você pode baixar o projeto completo como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Adicionar um editor no local {#add-an-in-place-editor}

Para obter informações gerais sobre como adicionar um editor no local, consulte o documento [personalizar a criação de página](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configurar Rich Text Editor no Experience Manager](/help/sites-administering/rich-text-editor.md).
