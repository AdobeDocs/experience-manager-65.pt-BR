---
title: Criação e organização de páginas com o AEM
description: Saiba como criar e gerenciar páginas com o Adobe Experience Manager.
exl-id: 74576e51-4b4e-464e-a0b8-0fae748a505d
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 383192083ec84176f67882a869550374f6074eef
workflow-type: tm+mt
source-wordcount: '2476'
ht-degree: 62%

---

# Criar e organizar páginas {#creating-and-organizing-pages}

Esta seção descreve como criar e gerenciar páginas com o Adobe Experience Manager (AEM) para depois [criar conteúdo](/help/sites-authoring/editing-content.md) nessas páginas.

>[!NOTE]
>
>Sua conta precisa de [direitos de acesso apropriados](/help/sites-administering/security.md) e [permissões](/help/sites-administering/security.md#permissions) para executar ações nas páginas, como criar, copiar, mover, editar e excluir.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

>[!NOTE]
>
>Há vários [atalhos de teclado](/help/sites-authoring/keyboard-shortcuts.md) que você pode usar no console Sites que tornam a organização das suas páginas mais eficiente.

## Organizar seu site {#organizing-your-website}

Como autor, organize seu site no AEM. Isso envolve criar e nomear suas páginas de conteúdo de modo que:

* Você pode encontrá-las facilmente no ambiente de criação
* Os visitantes do seu site possam navegar facilmente por elas no ambiente de publicação

Você também pode usar [pastas](#creating-a-new-folder) para ajudar a organizar o seu conteúdo.

A estrutura de um site pode ser considerada como uma estrutura em árvore que armazena suas páginas de conteúdo. Os nomes dessas páginas de conteúdo são usadas para formar os URLs, enquanto o título é exibido quando o conteúdo da página é visualizado.

O exemplo a seguir mostra o site We.Retail, onde uma página de shorts de caminhada ( `desert-sky-shorts`) é acessada:

* Ambiente de autor
  `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* Ambiente de publicação
  `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

Dependendo da configuração da sua instância, o uso de `/content` pode ser opcional no ambiente de publicação.

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

Esta estrutura pode ser visualizada do console **Sites**, onde é possível [navegar através das páginas do seu site](/help/sites-authoring/basic-handling.md#navigating) e executar ações nas páginas. Você também pode criar novos sites e [páginas](#creating-a-new-page).

De qualquer ponto, você pode visualizar a ramificação ascendente da navegação estrutural na barra do cabeçalho:

![caop-01](assets/caop-01.png)

### Convenções de nomenclatura da página {#page-naming-conventions}

Ao criar uma página, há dois campos principais:

* **[Título](#title)**:

   * O título é exibido ao usuário no console, na parte superior do conteúdo da página ao editar.
   * Esse campo é obrigatório.

* **[Nome](#name)**:

   * Usado para gerar o URI.
   * A entrada do usuário para este campo é opcional. Se não especificado, o nome é derivado do título. Consulte a seguinte seção [Restrições de nome de página e práticas recomendadas](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices) para obter detalhes.

#### Restrições de nome de página e práticas recomendadas {#page-name-restrictions-and-best-practices}

O **Título** da página e o **Nome** podem ser criados separadamente, mas estão relacionados:

* Ao criar uma página, somente o campo **Título** é obrigatório. Se nenhum **Nome** for fornecido na criação da página, o AEM gerará um nome a partir dos primeiros 64 caracteres do título (observando o conjunto definido abaixo). Somente os primeiros 64 caracteres são usados para seguir a prática recomendada de nomes de página curtos.

* Se um nome de página for especificado manualmente pelo autor, o limite de 64 caracteres não se aplicará. Contudo, outras limitações técnicas no comprimento de nome de página poderão ser aplicadas.

>[!NOTE]
>
>Ao definir um nome de página, um princípio básico é manter o nome da página curto, mas tão expressivo e memorável quanto possível para facilitar a compreensão do leitor. Consulte o [guia de estilo W3C](https://www.w3.org/Provider/Style/TITLE.html) no elemento `title`para obter mais informações.
>
>Lembre-se também de que alguns navegadores (por exemplo, versões mais antigas do IE) só podem aceitar URLs com um limite de comprimento, por isso também há um motivo técnico para manter os nomes de página curtos.

Ao criar uma página, o AEM [valida o nome da página de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR.

Os caracteres mínimos permitidos são:

* &#39;a&#39; até &#39;z&#39;
* &#39;A&#39; até &#39;Z&#39;
* &#39;0&#39; até &#39;9&#39;
* `_` (sublinhado)
* `-` (hífen/sinal de menos)

Detalhes completos sobre todos os caracteres permitidos podem ser encontrados nas [convenções de nomenclatura](/help/sites-developing/naming-conventions.md).

>[!NOTE]
>
>Se o AEM estiver em execução em uma [implantação do gerenciador de persistência MongoMK](/help/sites-deploying/recommended-deploys.md), os nomes de página serão limitados a 150 caracteres.

#### Título {#title}

Se você fornecer apenas uma página **Título** ao criar uma página, a AEM derivará a página **Nome** desta cadeia de caracteres e [validará o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR. Um campo de **Título** que contém caracteres inválidos será aceito, mas o nome derivado terá os caracteres inválidos substituídos. Por exemplo:

| Título | Nome derivado |
|---|---|
| Schön | schoen.html |
| SC%&amp;&#42;ç+ | sc---c-.html |

#### Nome {#name}

Quando você fornece uma página **Nome** ao criar uma página, o AEM [valida o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR. Não é possível inserir caracteres inválidos no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é realçado com uma mensagem explicativa.

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>Evite usar um código de duas letras, conforme definido por ISO-639-1 como um nome de página, a menos que seja uma raiz de idioma.
>
>Consulte [Preparação de conteúdo para tradução](/help/sites-administering/tc-prep.md) para obter mais informações.

### Modelos {#templates}

No AEM, um modelo especifica um tipo especializado de página. Um modelo é usado como a base para qualquer nova página que está sendo criada.

O modelo define a estrutura de uma página, incluindo uma imagem em miniatura e outras propriedades. Por exemplo, você pode ter modelos separados para páginas de produtos, mapas de site e informações de contato. Os modelos são compostos de [componentes](#components).

O AEM vem com vários modelos prontos para uso. Os modelos disponíveis dependem do site individual. Os campos principais são:

* **Título** O título exibido na página da Web resultante.

* **Nome** Usado ao nomear a página.

* **Modelo** Uma lista de modelos disponíveis para uso ao gerar a nova página.

>[!NOTE]
>
>Se configurado na instância,[ os autores de modelo poderão criá-los com o Editor de modelo](/help/sites-authoring/templates.md).

### Componentes {#components}

Os componentes são os elementos fornecidos pelo AEM, desse modo, é possível adicionar tipos específicos de conteúdo. O AEM vem com uma variedade de [componentes prontos para uso](/help/sites-authoring/default-components-console.md) que fornecem funcionalidade abrangente. Isso inclui:

* Texto
* Imagem
* Slideshow
* Vídeo
* E muito mais

Depois de criar e abrir uma página, é possível [adicionar conteúdo usando os componentes](/help/sites-authoring/editing-content.md#insertinganewparagraph), que estão disponíveis no [navegador de componentes](/help/sites-authoring/author-environment-tools.md#componentbrowser).

>[!NOTE]
>
>O console [Componentes](/help/sites-authoring/default-components-console.md) fornece uma visão geral dos componentes na instância.

## Gerenciamento de páginas {#managing-pages}

### Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, antes de começar a criar conteúdo, você deve criar uma página:

1. Abra o console Sites (por exemplo, [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)).
1. Navegue até o local onde deseja criar a nova página.
1. Abra o seletor suspenso usando **Criar** na barra de ferramentas e selecione **Página** na lista:

   ![caop-03](assets/caop-03.png)

1. A partir do primeiro estágio do assistente, você pode:

   * Selecione o modelo que deseja usar para criar a nova página e clique em **Avançar** para continuar.

   * **Cancelar** para suspender o processo.

   ![caop-04](assets/caop-04.png)

1. A partir do último estágio do assistente, você pode:

   * Use as três guias para inserir as [propriedades de página](/help/sites-authoring/editing-page-properties.md) que você deseja atribuir à nova página, em seguida, clique em **Criar** para realmente criar a página.

   * Use **Voltar** para retornar à seleção do modelo.

   Os campos principais são:

   * **Título**:

      * Ele é exibido ao usuário e é obrigatório.

   * **Nome**:

      * Usado para gerar o URI. Se não especificado, o nome é derivado do título.
      * Se você fornecer uma página **Nome** ao criar uma página, o AEM [validará o nome de acordo com as convenções](/help/sites-developing/naming-conventions.md) impostas pelo AEM e JCR.

      * **Não é possível inserir caracteres inválidos** no campo **Nome**. Quando o AEM detectar caracteres inválidos, o campo será realçado e uma mensagem explicativa será exibida para indicar os caracteres que precisam ser removidos/substituídos.

   >[!NOTE]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   As informações mínimas necessárias para criar uma página são o **Título**.

   ![caop-05](assets/caop-05.png)

1. Use **Criar** para concluir o processo e criar a sua nova página. A caixa de diálogo de confirmação perguntará se você deseja **Abrir** a página imediatamente ou voltar para o console (**concluído**):

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >Caso crie uma página usando um nome que já existe no local, o sistema vai gerar automaticamente uma variação do nome, ao anexar um número. Por exemplo, se `winter` já existir, uma nova página se tornará `winter0`.

1. Caso volte ao console, você verá em sua nova página:

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>Assim que uma página tiver sido criada, seu modelo não poderá ser alterado, a menos que você [crie uma inicialização com um novo modelo](/help/sites-authoring/launches-creating.md#create-launch-with-new-template), embora isso perderá todo o conteúdo já existente.

### Abrir uma página para edição {#opening-a-page-for-editing}

Depois de criar uma página ou navegar para uma página existente (no console), você pode abri-la para edição:

1. Abra o console do **Sites**.
1. Navegue até encontrar a página que deseja editar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) e a barra de ferramentas

   E, em seguida, selecione o ícone **Editar**:

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. A página será aberta e aqui é possível [editar a página](/help/sites-authoring/editing-content.md#touchoptimizedui) conforme necessário.

>[!NOTE]
>
>Navegar para outras páginas do editor de páginas só é possível no modo de visualização, pois os links não estão ativos no modo de Edição...

### Copiar e colar uma página      {#copying-and-pasting-a-page}

Você pode copiar uma página e todas as suas subpáginas para um novo local:

1. No console do **Sites**, navegue até encontrar a página que deseja copiar.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) e a barra de ferramentas

   E, em seguida, o ícone da página **Copiar**:

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >Se você estiver no modo de seleção, isso será encerrado automaticamente assim que a página for copiada.

1. Navegue até o local para a nova cópia da página.
1. O ícone **Colar** está disponível com uma seta suspensa à direita:

   ![Colar](assets/paste-without-children.png)

   Você pode:
   * Selecionar o próprio ícone **Colar**: uma cópia da página original e qualquer página filha serão criadas neste local.
   * Selecione a seta suspensa para revelar a opção **Colar sem filhos**. Será criada uma cópia da página original neste local; páginas filhas não serão copiadas.

   >[!NOTE]
   >
   >Se você copiar a página para um local onde uma página com o mesmo nome que a original já existir, o sistema gerará automaticamente uma variação do nome anexando um número. Por exemplo, se `winter` já existir, `winter` se tornará `winter1`.

### Mover ou renomear uma página {#moving-or-renaming-a-page}

>[!NOTE]
>
>A renomeação de uma página também está sujeita às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar o nome da nova página.

>[!NOTE]
>
>Uma página só pode ser movida para um local que permita o uso do modelo no qual a página se baseia. Consulte [Disponibilidade de modelo](/help/sites-developing/templates.md#template-availability) para obter mais informações.

O procedimento para mover ou renomear uma página é basicamente o mesmo e é realizado pelo mesmo assistente. Com este assistente você pode:

* Renomear uma página sem movê-la.
* Mover a página sem renomeá-la.
* Mover e renomear ao mesmo tempo.

O AEM oferece a funcionalidade de atualizar todos os links internos que se referem à página que está sendo renomeada/movida. Isso pode ser feito página por página para proporcionar total flexibilidade.

1. Navegue até encontrar a página que deseja mover.
1. Selecione sua página usando:

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) e a barra de ferramentas

   Em seguida, selecione o ícone de página **Mover**:

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   Isso abre o assistente para mover página.

1. A etapa **Renomear** do assistente fornece **Informações** sobre a página, incluindo a data de criação, o caminho e o número de referências diretas. Aqui, é possível:

   * Especifique o nome que deseja para a página após movê-la, em seguida, clique em **Avançar** para prosseguir.
   * **Cancelar** para suspender o processo.

   ![caop-07](assets/caop-07.png)

   O nome da página pode permanecer o mesmo se você estiver apenas movendo a página.

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `winter` já existir, `winter` se tornará `winter1`.

1. No estágio **Selecionar destino** do assistente, é possível:

   * Use a [exibição de coluna](/help/sites-authoring/basic-handling.md#column-view) para navegar até o novo local da página:

      * Para selecionar o destino, clique em sua miniatura.
      * Clique em **Avançar** para continuar.

   * Use **Voltar** para retornar à especificação do nome da página.

   >[!NOTE]
   >
   >Por padrão, a página principal da página que você está movendo/renomeando será selecionada como destino.

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >Se você mover uma página para um local onde uma página com o mesmo nome já existe, o sistema gera automaticamente uma variação do nome ao anexar um número. Por exemplo, se `winter` já existir, `winter` se tornará `winter1`.

1. Se a página estiver vinculada ou referenciada, ou tiver sido publicada, os detalhes serão listados na etapa **Ajustar/Republicar**.

   Você pode indicar o que deve ser ajustado e/ou republicado, conforme necessário.

   >[!NOTE]
   >
   >* Se a página não estiver vinculada nem referenciada, essa etapa não estará disponível.
   >* Esta etapa lista referências diretas e indiretas. Isso pode ser diferente do valor relatado na etapa **Renomear** do assistente, bem como das referências relatadas pelo painel de referências, que relatam apenas referências diretas por motivos de desempenho.

   ![caop-09](assets/caop-09.png)

1. Selecionar **Mover** concluirá o processo e moverá/renomeará a página conforme apropriado.

>[!NOTE]
>
>Se a página já tiver sido publicada, movê-la automaticamente desfará a publicação. Por padrão, ela será republicada quando a mudança for concluída, mas isso pode ser alterado ao desmarcar o campo **Republicar** na etapa **Ajustar/Republicar**.

>[!NOTE]
>
>Caso a página não seja mencionada de alguma maneira, então a etapa **Ajustar/republicar** será ignorada.

#### Ações assíncronas {#asynchronous-actions}

As ações de movimentação de página são sempre processadas de forma assíncrona, permitindo que o usuário continue a criação na interface do usuário desimpedida.

* O usuário deve definir quando a operação assíncrona deve ser executada
   * **Agora** a execução do trabalho assíncrono começa imediatamente.
   * **Mais tarde** permite que o usuário defina quando o trabalho assíncrono será iniciado.

  ![Mover página assíncrona](assets/asynchronous-page-move.png)

O status de trabalhos assíncronos pode ser verificado no painel [**Status de Trabalhos Assíncronos**](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação Global** > **Ferramentas** > **Operações** > **Trabalhos**

>[!NOTE]
>
>Para obter mais informações sobre o processamento assíncrono de trabalhos e como configurar o limite para ações de movimentação/renomeação de páginas, consulte o documento [Trabalhos assíncronos](/help/sites-administering/asynchronous-jobs.md) no guia do usuário de Administração.

>[!NOTE]
>
>O processamento assíncrono de movimentação de página requer o AEM 6.5.3.0 ou superior.

### Excluir uma página {#deleting-a-page}

1. Navegue até que você possa visualizar a página que deseja excluir.
1. Use o [modo de seleção](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) para selecionar a página pretendida, em seguida, use **Excluir** na barra de ferramentas:

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >Como uma precaução de segurança, o ícone de **Excluir página** não está disponível como uma ação rápida.

1. Uma caixa de diálogo solicitará uma confirmação. Use:

   * Use a opção **Cancelar** para suspender a ação
   * Clique em **Excluir** para confirmar a ação:

      * Se a página não tiver referências, ela será excluída.
      * Se a página tiver referências, uma caixa de mensagem informará que **Uma ou mais páginas são mencionadas.** Você pode selecionar **Forçar Exclusão** ou **Cancelar**.

>[!NOTE]
>
>Se uma página já estiver publicada, sua publicação será automaticamente desfeita antes da exclusão.

### Bloquear uma página   {#locking-a-page}

É possível [bloquear/desbloquear uma página](/help/sites-authoring/editing-content.md#locking-a-page) a partir de um console ou ao editar uma página individual. As informações sobre páginas bloqueadas também são mostradas em ambos os locais.

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### Criação de uma nova pasta {#creating-a-new-folder}

Você pode criar pastas para ajudar a organizar seus arquivos e páginas.

>[!NOTE]
>
>As pastas também estão sujeitas às [convenções de nomenclatura de página](#page-naming-conventions) ao especificar um novo nome de pasta.

>[!CAUTION]
>
>* Pastas só podem ser criadas diretamente em **Sites** ou em outras pastas. Elas não podem ser criadas em uma página.
>* As ações padrão de mover, copiar, colar, excluir, publicar, cancelar a publicação e exibir/editar propriedades podem ser executadas em uma pasta.
>* As pastas não estão disponíveis para seleção em uma live copy.
>

1. Abra o console **Sites** e navegue até o local necessário.
1. Para abrir a lista de opções, selecione **Criar** na barra de ferramentas
1. Selecione **Pasta** para abrir a caixa de diálogo. Aqui você pode inserir o **Nome** e o **Título**:

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Selecione **Criar** para criar a pasta.
