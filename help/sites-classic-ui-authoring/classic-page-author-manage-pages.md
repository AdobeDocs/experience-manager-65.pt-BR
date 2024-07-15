---
title: Criação e organização de páginas
description: Esta seção descreve como criar e gerenciar páginas com AEM para depois criar o conteúdo nessas páginas.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 16%

---

# Criar e organizar páginas{#creating-and-organizing-pages}

Esta seção descreve como criar e gerenciar páginas com o Adobe Experience Manager (AEM) para depois [criar conteúdo](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) nessas páginas.

>[!NOTE]
>
>Sua conta precisa de [direitos de acesso apropriados](/help/sites-administering/security.md) e [permissões](/help/sites-administering/security.md#permissions) para realizar ações nas páginas, por exemplo, criar, copiar, mover, editar, excluir.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

## Organizar seu site {#organizing-your-website}

Como autor, você deve organizar seu site dentro do AEM. Isso envolve criar e nomear suas páginas de conteúdo de modo que:

* você pode encontrá-los facilmente no ambiente de criação
* os visitantes do seu site podem navegá-los facilmente no ambiente de publicação

Você também pode usar [pastas](#creating-a-new-folder) para ajudar a organizar o seu conteúdo.

A estrutura de um site pode ser considerada como uma *estrutura em árvore* que armazena suas páginas de conteúdo. Os nomes dessas páginas de conteúdo são usadas para formar os URLs, enquanto o título é exibido quando o conteúdo da página é visualizado.

A seguir, uma extração do site do Geometrixx; onde, por exemplo, a página `Triangle` será acessada:

* Ambiente de autor

  `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* Ambiente do Publish

  `http://localhost:4503/content/geometrixx/en/products/triangle.html`

  Dependendo da configuração da sua instância, o uso de `/content` pode ser opcional no ambiente de publicação.

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

Esta estrutura pode ser visualizada do console Sites, que você pode usar para [navegar pela estrutura de árvore](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### Convenções de nomenclatura da página {#page-naming-conventions}

Ao criar uma página, há dois campos principais:

* **[Título](#title)**:

   * O título é exibido ao usuário no console, na parte superior do conteúdo da página ao editar.
   * Esse campo é obrigatório.

* **[Nome](#name)**:

   * Usado para gerar o URI.
   * A entrada do usuário para este campo é opcional. Se não especificado, o nome é derivado do título.

Ao criar uma página, AEM [valida o nome da página de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR.

A implementação e a lista de caracteres permitidos diferem ligeiramente de acordo com a interface do usuário (é mais extensa para a interface habilitada para toque), mas o mínimo permitido é:

* &#39;a&#39; até &#39;z&#39;
* &#39;A&#39; até &#39;Z&#39;
* &#39;0&#39; até &#39;9&#39;
* _ (sublinhado)
* `-` (hífen/sinal de menos)

Use apenas estes caracteres se quiser ter certeza de que eles serão aceitos/usados (se precisar de detalhes completos sobre todos os caracteres permitidos, consulte [as convenções de nomenclatura](/help/sites-developing/naming-conventions.md)).

#### Título {#title}

Se você fornecer apenas uma página **Título** ao criar uma página, o AEM derivará a página **Nome** desta cadeia de caracteres e [validará o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR. Em ambas as interfaces, um campo **Título** contendo caracteres inválidos será aceito, mas o nome derivado terá os caracteres inválidos substituídos. Por exemplo:

| Título | Nome derivado |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### Nome {#name}

Se você fornecer uma página **Nome** ao criar uma página, o AEM [validará o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR.

Na interface clássica, você **não pode inserir caracteres inválidos** no campo **Nome**.

>[!NOTE]
>Na interface habilitada para toque, você **não pode enviar caracteres inválidos** no campo **Nome**. Quando o AEM detectar caracteres inválidos, o campo será realçado e uma mensagem explicativa será exibida para indicar os caracteres que precisam ser removidos/substituídos.

>[!NOTE]
>
>Evite usar um código de duas letras, conforme definido pela ISO-639-1, a menos que seja uma raiz de idioma.
>
>Consulte [Preparação de conteúdo para tradução](/help/sites-administering/tc-prep.md) para obter mais informações.

### Modelos {#templates}

No AEM, um modelo especifica um tipo especializado de página. Um modelo é usado como a base para qualquer nova página que está sendo criada.

O modelo define a estrutura de uma página, incluindo uma imagem em miniatura e outras propriedades. Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de site e informações de contato. Os modelos são compostos de [componentes](#components).

O AEM vem com vários modelos prontos para uso. Os modelos oferecidos dependem do site individual e as informações que precisam ser fornecidas (ao criar a nova página) dependem da interface do usuário que está sendo usada. Os campos principais são:

* **Título** O título exibido na página da Web resultante.

* **Nome** Usado ao nomear a página.

* **Modelo** Uma lista de modelos disponíveis para uso ao gerar a nova página.

### Componentes {#components}

Os componentes são os elementos fornecidos pelo AEM, desse modo, é possível adicionar tipos específicos de conteúdo. O AEM vem com vários componentes prontos para uso que fornecem funcionalidade abrangente; eles incluem:

* Texto
* Imagem
* Slideshow
* Vídeo
* muito mais

Depois de criar e abrir uma página, você pode [adicionar conteúdo usando os componentes](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponíveis no [sidekick](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Gerenciamento de páginas {#managing-pages}

### Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, antes de começar a criar conteúdo, você deve criar uma página:

1. No console **Sites**, selecione o nível no qual deseja criar uma página.

   No exemplo a seguir, você está criando uma página no nível **Produtos** - mostrado no painel esquerdo; o painel direito mostra páginas que já existem no nível em **Produtos**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. No menu **Nova...** (clique na seta ao lado de **Nova...**), selecione **Nova página...**. A janela **Criar página** é aberta.

   Clicar em **Nova...** também atua como atalho para a opção **Nova página...**.

1. A caixa de diálogo **Criar Página** permite:

   * Forneça um **Título**; isto é exibido ao usuário.
   * Forneça um **Nome**; ele é usado para gerar o URI. Se não especificado, o nome será derivado do título.

      * Se você fornecer uma página **Nome** ao criar uma página, o AEM [validará o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR.
      * Na interface clássica, você **não pode inserir caracteres inválidos** no campo **Nome**.

   * Clique no template que deseja usar para criar a nova página.

     O modelo é usado como a base para a nova página; por exemplo, para determinar o layout básico de uma página de conteúdo.

   >[!NOTE]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   As informações mínimas necessárias para criar uma página são o **Título** e o modelo necessário.

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Se você quiser usar caracteres unicode nas URLs, defina a propriedade Alias ( `sling:alias`) ([propriedades da página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Clique em **Criar** para criar a página. Você retorna ao console **Sites**, no qual pode ver uma entrada para a nova página.

   O console fornece informações sobre a página (por exemplo, quando ela foi editada pela última vez e por quem) que é atualizada conforme necessário.

   >[!NOTE]
   >
   >Você também pode criar uma página ao editar uma página existente. Usar a **Criar página secundária** da guia **Página** do sidekick cria uma página diretamente abaixo da página que está sendo editada.

### Abrir uma página para edição {#opening-a-page-for-editing}

Você pode abrir a página para ser [editada](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) por um dos vários métodos:

* No console **Sites**, você pode **clicar duas vezes** na entrada da página para abri-la para edição.

* No console **Sites**, você pode **clicar com o botão direito do mouse** (menu de contexto) no item de página e selecionar **Abrir** no menu.

* Depois de abrir uma página, você pode navegar para outras páginas do site (para editá-las) clicando em hiperlinks.

### Copiar e colar uma página      {#copying-and-pasting-a-page}

Ao copiar, é possível copiar:

* uma página única
* uma página junto com todas as subpáginas

1. No console **Sites**, selecione a página que deseja copiar.

   >[!NOTE]
   >
   >Nesse estágio, é irrelevante se você deseja copiar uma única página ou as subpáginas subjacentes.

1. Clique em **Copiar**.

1. Navegue até o novo local e clique em:

   * **Colar** - para colar a página junto com todas as subpáginas
   * **Shift + Colar** - para colar somente a página selecionada

   As páginas são coladas no novo local.

   >[!NOTE]
   >
   >O nome da página pode ser ajustado automaticamente se uma página existente já tiver o mesmo nome.

   >[!NOTE]
   >
   >Você também pode usar **Copiar página** da guia **Página** do sidekick. Isso abre uma caixa de diálogo onde você pode especificar o destino e assim por diante.

### Mover ou renomear página {#moving-or-renaming-page}

>[!NOTE]
>
>A renomeação de uma página também está sujeita às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar o nome da nova página.

O procedimento para mover ou renomear uma página é o mesmo. Com a mesma ação, é possível:

* mover uma página para um novo local
* renomear uma página no mesmo local
* mover uma página para um novo local e renomeá-la ao mesmo tempo

O AEM oferece a funcionalidade de atualizar links internos para a página que está sendo renomeada ou movida. Isso pode ser feito página por página para proporcionar total flexibilidade.

Para mover ou renomear uma página:

1. Há vários métodos para acionar uma movimentação:

   * No console **Sites**, clique para selecionar a página e selecione **Mover...**
   * No console **Sites**, você também pode selecionar o item de página, clicar com o **botão direito do mouse** e selecionar **Mover...**
   * Ao editar uma página, você pode selecionar **Mover página** na guia **Página** do sidekick.

1. A janela **Mover** é aberta; aqui você pode especificar um novo local, um novo nome para a página ou ambos.

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   A página também lista todas as páginas que fazem referência à página que está sendo movida. Dependendo do status da página de referência, talvez seja possível ajustar esses links e/ou republicar as páginas.

1. Preencha os seguintes campos, conforme apropriado:

   * **Destino**

     Use o mapa de site (disponível por meio do seletor suspenso) para selecionar o local para onde a página deve ser movida.

     Se você estiver apenas renomeando a página, ignore este campo.

   * **Mover**

     Especifique a página a ser movida - geralmente, ela é preenchida por padrão, dependendo de como e onde você iniciou a ação de movimentação.

   * **Renomear para**

     O rótulo da página atual é exibido por padrão. Especifique o rótulo da nova página, se necessário.

   * **Ajustar**

     Atualize os links na página listada que apontam para a página movida: por exemplo, se a página A tiver links para a página B, o AEM ajustará os links na página A, caso você mova a página B.

     Isso pode ser selecionado/desmarcado para cada página de referência individual.

   * **Republicar**

     Republicar a página de referência; novamente, isso pode ser selecionado para cada página individual.

   >[!NOTE]
   >
   >Se a página já tiver sido ativada, movê-la automaticamente a desativará. Por padrão, ele será reativado quando a movimentação for concluída, mas isso pode ser alterado ao desmarcar o campo **Republicar** para a página na janela **Mover**.

1. Clique em **Mover**. A confirmação será necessária. Clique em **OK** para confirmar.

   >[!NOTE]
   >
   >O título da página não será atualizado.

### Excluir uma página {#deleting-a-page}

1. Você pode excluir uma página de vários locais:

   * No console **Sites**, clique para selecionar a página, clique com o botão direito do mouse e selecione **Excluir** do menu resultante.
   * No console **Sites**, clique para selecionar a página e selecione **Excluir** no menu da barra de ferramentas.
   * No sidekick, use a guia **Página** para selecionar **Excluir página**. Isso exclui a página aberta no momento.

1. Depois de selecionar a exclusão de uma página, você deve confirmar a solicitação, pois a ação não pode ser desfeita.

   >[!NOTE]
   >
   >Após a exclusão, se a página tiver sido publicada, é possível restaurar a versão mais recente (ou uma específica), mas ela pode não ter exatamente o mesmo conteúdo da última versão caso tenham sido feitas outras modificações. Consulte [Como Restaurar Páginas](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) para obter mais detalhes.

>[!NOTE]
>
>Se uma página já estiver ativada, ela será automaticamente desativada antes da exclusão.

### Bloquear uma página   {#locking-a-page}

É possível [bloquear/desbloquear uma página](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) a partir de um console ou ao editar uma página individual. As informações sobre páginas bloqueadas também são mostradas em ambos os locais.

### Criação de uma nova pasta {#creating-a-new-folder}

>[!NOTE]
>
>As pastas também estão sujeitas às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar um novo nome de pasta.

1. Abra o console **Sites** e navegue até o local necessário.
1. No menu **Nova...** (clique na seta ao lado de **Nova...**), selecione **Nova Pasta...**.
1. A caixa de diálogo **Criar Pasta** é aberta. Aqui você pode inserir o **Nome** e o **Título**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Selecione **Criar** para criar a pasta.
