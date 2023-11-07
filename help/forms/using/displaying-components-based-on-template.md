---
title: Exibição de componentes com base no modelo usado
seo-title: Displaying components based on the template used
description: Ao criar um formulário, saiba como habilitar componentes na barra lateral com base no modelo selecionado.
seo-description: When you create a form, learn how you can enable components in the sidebar based on the template selected.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Exibição de componentes com base no modelo usado{#displaying-components-based-on-the-template-used}

Quando um autor de formulário cria um formulário adaptável usando uma [modelo](../../forms/using/template-editor.md), o autor do formulário pode ver e usar componentes específicos com base na política do modelo. Você pode especificar uma política de conteúdo de modelo que permita escolher um grupo de componentes que o autor do formulário vê no momento da criação do formulário.

## Alteração da política de conteúdo de um modelo {#changing-the-content-policy-of-a-template}

Ao criar um modelo, ele é criado em `/conf` no repositório de conteúdo. Com base nas pastas criadas no `/conf` diretório, o caminho para o modelo é: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Execute as seguintes etapas para mostrar os componentes na barra lateral com base na política de conteúdo de um modelo:

1. Abra o CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. No CRXDE, navegue até a pasta em que o modelo é criado.

   Por exemplo: `/conf/<your-folder>/`

1. No CRXDE, acesse: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Para selecionar um grupo de componentes, é necessária uma nova política de conteúdo. Para criar uma política, copie e cole a política padrão e renomeie-a.

   O caminho para a política de conteúdo padrão é: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   No `gridFluidLayout` , copie e cole a política padrão e renomeie-a. Por exemplo, `myPolicy`.

   ![Copiando políticas padrão](assets/crx-default1.png)

1. Selecione a nova política que você criar e selecione o **componentes** propriedade no painel direito com tipo `string[]`.

   Ao selecionar e abrir a propriedade componentes, você verá a caixa de diálogo Editar componentes. A caixa de diálogo Editar componentes permite adicionar ou remover grupos de componentes usando o **+** e **-** botões. Você pode adicionar grupos de componentes que incluem componentes que o formulário deseja que os autores usem.

   ![Adicionar ou remover componentes na política](assets/add-components-list1.png)

   Depois de adicionar um grupo de componentes, clique em **OK** para atualizar a lista e clique em **Salvar tudo** acima da barra de endereços CRXDE e atualize.

1. No modelo, altere a política de conteúdo padrão para a nova política criada. ( `myPolicy` neste exemplo.)

   Para alterar a política, no CRXDE, acesse `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   No `cq:policy` propriedade, alterar `default` ao novo nome da política ( `myPolicy`).

   ![Política de conteúdo do modelo atualizada](assets/updated-policy.png)

   Ao criar um formulário usando o modelo, você pode ver os componentes adicionados na barra lateral.
