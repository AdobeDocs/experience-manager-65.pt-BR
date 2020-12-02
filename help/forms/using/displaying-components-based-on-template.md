---
title: Exibir componentes com base no modelo usado
seo-title: Exibir componentes com base no modelo usado
description: Ao criar um formulário, saiba como ativar os componentes na barra lateral com base no modelo selecionado.
seo-description: Ao criar um formulário, saiba como ativar os componentes na barra lateral com base no modelo selecionado.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---


# Exibir componentes com base no modelo usado{#displaying-components-based-on-the-template-used}

Quando um autor de formulário cria um formulário adaptável usando um [modelo](../../forms/using/template-editor.md), o autor do formulário pode ver e usar componentes específicos com base na política de modelo. É possível especificar uma política de conteúdo de modelo que permite escolher um grupo de componentes que o autor do formulário vê no momento da criação do formulário.

## Alteração da política de conteúdo de um modelo {#changing-the-content-policy-of-a-template}

Quando você cria um modelo, ele é criado em `/conf` no repositório de conteúdo. Com base nas pastas criadas no diretório `/conf`, o caminho para o modelo é: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Execute as seguintes etapas para mostrar os componentes na barra lateral com base na política de conteúdo de um modelo:

1. Abra o CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. No CRXDE, navegue até a pasta na qual o modelo é criado.

   Por exemplo: `/conf/<your-folder>/`

1. No CRXDE, navegue até: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Para selecionar um grupo de componentes, uma nova política de conteúdo é necessária. Para criar uma nova política, copie e cole a política padrão e renomeie-a.

   O caminho para a política de conteúdo padrão é: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   Na pasta `gridFluidLayout`, copie e cole a política padrão e renomeie-a. Por exemplo, `myPolicy`.

   ![Copiando políticas padrão](assets/crx-default1.png)

1. Selecione a nova política criada e selecione a propriedade **components** no painel direito com o tipo `string[]`.

   Quando você seleciona e abre a propriedade components, é exibida a caixa de diálogo Editar componentes. A caixa de diálogo Editar componentes permite adicionar ou remover grupos de componentes usando os botões **+** e **-**. Você pode adicionar um grupo de componentes que inclui componentes que os autores devem usar.

   ![Adicionar ou remover componentes na política](assets/add-components-list1.png)

   Depois de adicionar um grupo de componentes, clique em **OK** para atualizar a lista e, em seguida, clique em **Salvar tudo** acima da barra de endereços CRXDE e atualize.

1. No modelo, altere a política de conteúdo do padrão para a nova política criada. ( `myPolicy` neste exemplo.)

   Para alterar a política, no CRXDE, navegue até `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   Na propriedade `cq:policy`, altere `default` para o novo nome de política ( `myPolicy`).

   ![Política de conteúdo de modelo atualizada](assets/updated-policy.png)

   Ao criar um formulário usando o modelo, é possível visualizar os componentes adicionados na barra lateral.

