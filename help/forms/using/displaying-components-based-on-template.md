---
title: Exibição de componentes com base no modelo usado
description: Ao criar um formulário, saiba como habilitar componentes na barra lateral com base no modelo selecionado.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Exibição de componentes com base no modelo usado{#displaying-components-based-on-the-template-used}

Quando um autor de formulário cria um formulário adaptável usando um [modelo](../../forms/using/template-editor.md), o autor do formulário pode ver e usar componentes específicos com base na política do modelo. Você pode especificar uma política de conteúdo de modelo que permita escolher um grupo de componentes que o autor do formulário vê no momento da criação do formulário.

## Alteração da política de conteúdo de um modelo {#changing-the-content-policy-of-a-template}

Ao criar um modelo, ele é criado em `/conf` no repositório de conteúdo. Com base nas pastas criadas no diretório `/conf`, o caminho para o modelo é: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Execute as seguintes etapas para mostrar os componentes na barra lateral com base na política de conteúdo de um modelo:

1. Abra o CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. No CRXDE, navegue até a pasta em que o modelo é criado.

   Por exemplo: `/conf/<your-folder>/`

1. No CRXDE, navegue até: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Para selecionar um grupo de componentes, é necessária uma nova política de conteúdo. Para criar uma política, copie e cole a política padrão e renomeie-a.

   O caminho para a política de conteúdo padrão é: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   Na pasta `gridFluidLayout`, copie e cole a política padrão e renomeie-a. Por exemplo, `myPolicy`.

   ![Copiando políticas padrão](assets/crx-default1.png)

1. Selecione a nova política criada e a propriedade **components** no painel direito com o tipo `string[]`.

   Ao selecionar e abrir a propriedade componentes, você verá a caixa de diálogo Editar componentes. A caixa de diálogo Editar componentes permite adicionar ou remover grupos de componentes usando os botões **+** e **-**. Você pode adicionar grupos de componentes que incluem componentes que o formulário deseja que os autores usem.

   ![Adicionar ou remover componentes na política](assets/add-components-list1.png)

   Depois de adicionar um grupo de componentes, clique em **OK** para atualizar a lista e em **Salvar tudo** acima da barra de endereços CRXDE e atualize.

1. No modelo, altere a política de conteúdo padrão para a nova política criada. ( `myPolicy` neste exemplo.)

   Para alterar a política, no CRXDE, navegue até `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   Na propriedade `cq:policy`, altere `default` para o novo nome de política ( `myPolicy`).

   ![Política de conteúdo de modelo atualizada](assets/updated-policy.png)

   Ao criar um formulário usando o modelo, você pode ver os componentes adicionados na barra lateral.
