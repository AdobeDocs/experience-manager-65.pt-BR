---
title: Configuração de vários editores no local
seo-title: Configuração de vários editores no local
description: É possível configurar seu componente para que ele tenha vários editores no local
seo-description: É possível configurar seu componente para que ele tenha vários editores no local
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Configuração de vários editores no local{#configuring-multiple-in-place-editors}

É possível configurar seu componente para que ele tenha vários editores no local na interface habilitada para toque.

Quando configurado, você pode selecionar o conteúdo apropriado e abrir o editor apropriado. Por exemplo:

![chlimage_1-8](assets/chlimage_1-8a.png)

## Configuração de vários editores {#configuring-multiple-editors}

Para habilitar vários editores no local, a estrutura de um tipo de `cq:InplaceEditingConfig` nó foi aprimorada com a definição do tipo de `cq:ChildEditorConfig` nó.

Por exemplo:

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Para configurar vários editores:

1. No nó `cq:inplaceEditing` (do tipo `cq:InplaceEditingConfig`), defina a propriedade:

   * Nome:`editorType`
   * Tipo: `String`
   * Valor: `hybrid`

1. Neste nó, crie um novo nó:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. No `cq:childEditors` nó, crie um novo nó para cada editor local:

   * Nome: o nome de cada nó deve ser o nome da propriedade que ele representa (assim como os destinos de soltar). Por exemplo, `image`, `text`.
   * Tipo: cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >Há uma correlação entre os destinos de soltar definidos e os editores filhos. O nome do `cq:ChildEditorConfig` nó será considerado como a ID de destino de soltar, para uso como parâmetro para o editor filho selecionado. Se a subárea editável não tiver um destino de soltar (por exemplo, como com um componente de texto), o nome do editor filho ainda será considerado como uma ID para identificar a área editável correspondente.

1. Em cada um desses nós ( `cq:ChildEditorConfig`) define as propriedades:

   * Nome: `type`
   * Valor: Nome do editor no local registrado; por exemplo, `image`, `text`

   * Nome: `title`
   * Valor: o título que você deseja exibir na lista de seleção de componentes (de editores disponíveis); por exemplo, `Image`, `Text`

### Configuração adicional para editores de Rich Text {#additional-configuration-for-rich-text-editors}

A configuração para vários editores de Rich Text é um pouco diferente, pois você pode configurar cada instância individual do RTE separadamente.

>[!NOTE]
>
>Para obter mais detalhes, consulte [Configuração do Editor](/help/sites-administering/rich-text-editor.md)de Rich Text.

Para ter vários RTEs, você precisa de uma configuração para cada RTE no local:

* Em `cq:InplaceEditingConfig` definir um `config` nó.

   * No `config` nó, defina cada configuração individual do RTE.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>A prática recomendada é definir o `config` nó em `cq:InplaceEditingConfig` que cada RTE individual pode ter uma configuração diferente.
>
>No entanto, para o RTE, a `configPath` propriedade é suportada quando há apenas uma instância do editor de texto (subárea editável) no componente. Esse uso do é fornecido para oferecer suporte à compatibilidade com versões anteriores das caixas de diálogo mais antigas do componente. `configPath`

## Amostras de código {#code-samples}

**CÓDIGO NO GITHUB**

Você pode encontrar o código desta página no GitHub

* [Abrir projeto aem-authoring-hybrideditors no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## Adicionar um editor local {#adding-an-in-place-editor}

Para obter informações gerais sobre como adicionar um editor no local, consulte o documento [Personalizando a criação](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)de páginas.
