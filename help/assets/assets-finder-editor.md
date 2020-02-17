---
title: Criar e configurar páginas do Editor de ativos
description: Saiba como criar páginas personalizadas do Editor de ativos e editar vários ativos simultaneamente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Criar e configurar páginas do Editor de ativos {#creating-and-configuring-asset-editor-pages}

Este documento descreve o seguinte:

* Por que você criaria páginas personalizadas do Editor de ativos.
* Como criar e personalizar páginas do Editor de ativos, que são páginas do WCM que permitem exibir e editar metadados, bem como executar ações no ativo.
* Como editar vários ativos simultaneamente.

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 OOTB samples. -->

>[!NOTE]
>
>O Compartilhamento de ativos está disponível como uma implementação de referência de código aberto. Consulte [Compartilhamento de ativos comuns](https://adobe-marketing-cloud.github.io/asset-share-commons/). Não é oficialmente suportado.

## Por que criar e configurar as páginas do Editor de ativos? {#why-create-and-configure-asset-editor-pages}

O Gerenciamento de ativos digitais está sendo usado em mais e mais cenários. Ao mudar de uma solução em pequena escala para um pequeno grupo de usuários treinados profissionalmente - por exemplo, fotógrafos ou taxonomistas - para grupos de usuários maiores e mais diversos - por exemplo, usuários comerciais, autores de WCM, jornalistas e assim por diante - a poderosa interface de usuário dos ativos Adobe Experience Manager (AEM) para usuários profissionais pode fornecer informações demais e as partes interessadas começam a solicitar interfaces de usuário ou aplicativos específicos para acessar os ativos digitais que são relevantes.

Esses aplicativos centrados em ativos podem ser simples galerias de fotos em uma intranet onde os funcionários podem fazer upload de fotos de visitas comerciais ou de um centro de imprensa em um site público, como o exemplo fornecido com o Geometrixx. Aplicativos centrados em ativos também podem ser estendidos para soluções completas, incluindo carrinhos de compras, processos de checkout e verificação.

A criação de um aplicativo centrado em ativos torna-se, em grande medida, um processo de configuração que não exige codificação, apenas conhecimento dos grupos de usuários e suas necessidades, bem como conhecimento dos metadados usados. Os aplicativos centrados em ativos criados com os ativos AEM são extensíveis: com o esforço de codificação moderado, é possível criar componentes reutilizáveis para pesquisa, visualização e modificação de ativos.

Um aplicativo centrado em ativos no AEM consiste em uma página do Editor de ativos, que pode ser usada para obter uma exibição detalhada de um ativo específico. Uma página do Editor de ativos também permite a edição de metadados, desde que o usuário que acessa o ativo tenha as permissões necessárias.

## Criar e configurar uma página de compartilhamento de ativos {#creating-and-configuring-an-asset-share-page}

Personalize a funcionalidade do DAM Finder e crie páginas com todas as funcionalidades necessárias, chamadas páginas de compartilhamento de ativos. Para criar uma nova página Compartilhamento de ativos, adicione a página usando o modelo Compartilhamento de ativos do Geometrixx e personalize as ações que os usuários podem executar nessa página, determine como os visualizadores podem ver os ativos e decidir como os usuários podem criar suas consultas.

Estes são alguns casos de uso para criar uma página personalizada de compartilhamento de ativos:

* Centro de Imprensa para Jornalistas
* Mecanismo de pesquisa de imagem para usuários empresariais internos
* Banco de dados de imagem para usuários do site
* Interface de marcação de mídia para editores de metadados

### Criar uma página de compartilhamento de ativos {#creating-an-asset-share-page}

Para criar uma nova página Compartilhamento de ativos, você pode criá-la quando estiver trabalhando em sites ou no gerenciador de ativos digitais.

>[!NOTE]
>
>Por padrão, ao criar uma página Compartilhamento de ativos a partir de **Novo** no gerenciador de ativos digitais, um visualizador de ativos e um editor de ativos são criados automaticamente para você.

Para criar uma nova página de compartilhamento de ativos no console **Sites** :

1. Na guia **Sites** , navegue até o local onde deseja criar uma página de compartilhamento de ativos e clique em **Novo**.

1. Selecione a página Compartilhamento **de** ativos e clique em **Criar**. A nova página é criada e a página de compartilhamento de ativos é listada na guia **Sites** .

![dam8](assets/dam8.png)

A página básica criada usando o modelo de Compartilhamento de ativos do Geometrixx DAM é exibida da seguinte maneira:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

Para personalizar a página Compartilhamento de ativos, use elementos do sidekick e edite também as propriedades do construtor de consultas. A página **Geometrixx Press Center** é uma versão personalizada de uma página baseada neste modelo:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

Para criar uma nova página de compartilhamento de ativos por meio do gerenciador de ativos digitais:

1. No gerenciador de ativos digitais, em **Novo**, selecione **Novo compartilhamento** de ativos.
1. No **Título**, informe o nome da página de compartilhamento de ativos. Se desejar, insira um nome para o URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Clique duas vezes na página de compartilhamento de ativos para abri-la e configurar a página.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   Por padrão, ao criar uma página Compartilhamento de ativos em **Novo**, um visualizador de ativos e um editor de ativos são criados automaticamente para você.

#### Personalizar ações {#customizing-actions}

Você pode determinar quais ações os usuários podem executar em ativos digitais selecionados a partir de uma seleção de ações predefinidas.

Para adicionar ações à página Compartilhamento de ativos:

1. Na página Compartilhamento de ativos que você deseja personalizar, clique em **Ações** no sidekick.

As seguintes ações estão disponíveis:

![assetshare2](assets/assetshare2.bmp)

| Ação | Descrição |
|---|---|
| [!UICONTROL Ação de exclusão] | Os usuários podem excluir os ativos selecionados. |
| [!UICONTROL Ação de download] | Permite que os usuários baixem ativos selecionados em seus computadores. |
| [!UICONTROL Ação do Lightbox] | Salva os ativos em um &quot;lightbox&quot; onde você pode executar outras ações. Isso é útil ao trabalhar com ativos em várias páginas. O lightbox também pode ser usado como um carrinho de compras para ativos. |
| [!UICONTROL Ação de mover] | Os usuários podem mover o ativo para outro local |
| [!UICONTROL Ação de tags] | Permite que os usuários adicionem tags aos ativos selecionados |
| [!UICONTROL Exibir ação de ativo] | Abre o ativo no Editor de ativos para manipulação do usuário. |

1. Arraste a ação apropriada para a área **Ações** na página. Isso cria um botão que é usado para executar essa ação.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determinar como os resultados da pesquisa são apresentados {#determining-how-search-results-are-presented}

Você determina como os resultados são exibidos em uma lista predefinida de lentes.

Para alterar como os resultados da pesquisa são exibidos:

1. Na página Compartilhamento de ativos que você deseja personalizar, clique em Pesquisar.

![chlimage_1](assets/assetshare3.png)

1. Arraste a lente apropriada para o centro superior da página. No Press Center, as lentes já estão disponíveis. Os usuários pressionam o ícone de lente apropriado para exibir os resultados da pesquisa conforme desejado.

Estão disponíveis as seguintes lentes:

| Lente | Descrição |
|---|---|
| **[!UICONTROL Listas lentes]** | Apresenta os ativos em uma lista com detalhes. |
| **[!UICONTROL Lentes mosaico]** | Apresenta ativos de forma mosaica. |

#### Lentes mosaico {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### Listas lentes {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Personalizar o Query Builder {#customizing-the-query-builder}

O construtor de consultas permite que você insira termos de pesquisa e crie conteúdo para a página Compartilhamento de ativos. Ao editar o construtor de consultas, você também pode determinar quantos resultados de pesquisa são exibidos por página, qual editor de ativos é aberto quando você clica duas vezes em um ativo, o caminho que a consulta pesquisa e personaliza tipos de nó.

Para personalizar o construtor de consultas:

1. Na página Compartilhamento de ativos que você deseja personalizar, clique em **Editar** no Query Builder. Por padrão, a guia **Geral** é aberta.
1. Selecione o número de resultados por página, o caminho do editor de ativos (se você tiver um editor de ativos personalizado) e o título Ações.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Insira um caminho ou vários caminhos que a pesquisa executará. Esses caminhos serão substituídos se o usuário usar o predicado Caminhos.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Digite outro tipo de nó, se desejar.

1. No campo URL **do Construtor de** consultas, você pode substituir ou vincular o construtor de consultas e inserir os novos URLs de servlet com o componente existente do construtor de consultas. No campo URL **do** feed, também é possível substituir o URL do feed.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. No campo **Texto** , insira o texto que deseja exibir para os resultados e números de página dos resultados. Clique em **OK** ao terminar de fazer as alterações.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Adicionar predicados {#adding-predicates}

Os ativos AEM incluem vários predicados que você pode adicionar à página Compartilhamento de ativos. Isso permite que seus usuários restrinjam ainda mais as pesquisas. Em alguns casos, eles podem substituir um parâmetro do construtor de consultas (por exemplo, o parâmetro Caminho).

Para adicionar predicados:

1. Na página Compartilhamento de ativos que você deseja personalizar, clique em **Pesquisar**.

![assetshare3](assets/assetshare3.png)

1. Arraste os predicados apropriados para a página Compartilhamento de ativos abaixo do construtor de consultas. Isso cria os campos apropriados.

![assetshare4](assets/assetshare4.bmp)

Os seguintes predicados estão disponíveis:

| Predicado | Descrição |
|---|---|
| **[!UICONTROL Predicado de data]** | Permite que os usuários pesquisem ativos que foram modificados antes e depois de determinadas datas. |
| **[!UICONTROL Predicado de opções]** | O proprietário do site pode especificar uma propriedade para pesquisa (como no predicado de propriedade, por exemplo cq:tags) e uma árvore de conteúdo a partir da qual as opções serão preenchidas (por exemplo, a árvore de tags). Isso gera uma lista de opções em que os usuários podem selecionar os valores (tags) que a propriedade selecionada (propriedade tag) deve ter. Esse predicado permite que você crie controles de lista como a lista de tags, tipos de arquivos, orientações de imagem e assim por diante. É ótimo para um conjunto fixo de opções. |
| **[!UICONTROL Predicados de caminho]** | Permite que os usuários definam o caminho e as subpastas, se desejado. |
| **[!UICONTROL Predicado da propriedade]** | O proprietário do site especifica uma propriedade a ser pesquisada, por exemplo, tiff:ImageLength e o usuário pode então inserir um valor, por exemplo, 800. Isso retorna todas as imagens com 800 pixels de altura. Preveja se sua propriedade pode ter valores arbitrários. |

Para obter mais informações, consulte o [predicado Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. Para configurar mais o predicado, clique duas vezes nele. Por exemplo, ao abrir o Predicado de caminho, é necessário atribuir o caminho raiz.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)

## Criar e configurar uma página do Editor de ativos {#creating-and-configuring-an-asset-editor-page}

Personalize o editor de ativos para determinar como os usuários podem visualizar e editar os ativos digitais. Para fazer isso, crie uma nova página do Editor de ativos e personalize as exibições e as ações que os usuários podem executar nessa página.

>[!NOTE]
>
>Se desejar adicionar campos personalizados ao editor de ativos DAM, adicione novos nós cq:Widget a `/apps/dam/content/asseteditors.`

### Criar uma página do Editor de ativos {#creating-the-asset-editor-page}

Ao criar a página Editor de ativos, uma boa prática é criar a página logo abaixo da página Compartilhamento de ativos.

Para criar uma página do Editor de ativos:

1. Na guia **Sites** , navegue até o local onde deseja criar uma página do editor de ativos e clique em **Novo**.
1. Selecione **Editor** de ativos Geometrixx e clique em **Criar**. A nova página é criada e listada na guia **Sites** .

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

A página básica criada usando o modelo do Editor de ativos Geometrixx tem a seguinte aparência:

![assetshare5](assets/assetshare5.bmp)

Para personalizar a página do Editor de ativos, use elementos do sidekick. A página do Editor de ativos que é acessada do **Geometrixx Press Center** é uma versão personalizada de uma página baseada neste modelo:

![assetshare6](assets/assetshare6.bmp)

#### Definir um editor de ativos para abrir a partir de uma página de compartilhamento de ativos {#setting-which-asset-editor-opens-from-an-asset-share-page}

Depois de criar a página personalizada do Editor de ativos, é necessário garantir que, ao clicar duas vezes nos ativos, o Compartilhamento personalizado de ativos que você criou abra os ativos na página personalizada do Editor.

Para definir a página Editor de ativos:

1. Na página Compartilhamento de ativos, clique em **Editar** ao lado do Query Builder.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. Clique na guia **Geral** se ainda não estiver selecionada.

1. No campo **Caminho do Editor** de ativos, digite o caminho para o editor de ativos no qual você deseja que a página Compartilhamento de ativos abra os ativos e clique em **OK**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### Adicionar componentes do Editor de ativos {#adding-asset-editor-components}

Você determina qual funcionalidade um editor de ativos tem adicionando componentes à página.

Para adicionar componentes do editor de ativos:

1. Na página do Editor de ativos que deseja personalizar, selecione o Editor **de** ativos no sidekick. Todos os componentes disponíveis do editor de ativos são exibidos.

>[!NOTE]
>
>O que você pode personalizar depende de quais componentes estão disponíveis. Para ativar os componentes, vá para o Modo de design e selecione os componentes necessários habilitados.

1. Arraste os componentes do sidekick para o editor de ativos e faça quaisquer modificações nas caixas de diálogo do componente. Os componentes são descritos na tabela a seguir e descritos nas instruções detalhadas a seguir.

>[!NOTE]
>
>Ao projetar a página do editor de ativos, você cria componentes que são somente leitura ou editáveis. Os usuários sabem que um campo pode ser editado se uma imagem de um lápis for exibida nesse componente. Por padrão, a maioria dos componentes é configurada como somente leitura.

| Componente | Descrição |
|---|---|
| **[!UICONTROL Campo de texto de formulário]de metadados e[!UICONTROL metadados]** | Permite que você adicione metadados adicionais a um ativo e execute uma ação, como enviar, nesse ativo. |
| **[!UICONTROL Subativos]** | Permite personalizar subativos. |
| **Tags** | Permite que os usuários selecionem e adicionem tags a um ativo. |
| **[!UICONTROL Miniatura]** | Mostra uma miniatura do ativo, seu nome de arquivo e permite que você adicione um texto alternativo. Também é possível adicionar ações do editor de ativos aqui. |
| **[!UICONTROL Título]** | Exibe o título do ativo, que pode ser personalizado. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### Formulário de metadados e campo de texto - Configuração do componente Exibir metadados {#metadata-form-and-text-field-configuring-the-view-metadata-component}

O Formulário de metadados é um formulário que inclui uma ação de início e fim. No meio, você insere campos **de Texto** . Consulte [Formulários](/help/sites-authoring/default-components-foundation.md#form-component) para obter mais informações sobre como trabalhar com formulários.

1. Crie uma ação de início clicando em **Editar** na área Iniciar do formulário. Você pode inserir um título de Caixa, se desejar. Por padrão, o título Caixa é **Metadados**. Marque a caixa de seleção Validação do cliente se desejar que o código do cliente Java-script para validação seja gerado.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. Crie uma ação Encerrar clicando em **Editar** na área Fim do formulário. Por exemplo, você pode criar um botão **Enviar** para permitir que os usuários enviem suas alterações de metadados. Como opção, você pode adicionar um botão **Redefinir** que redefine os metadados para seu estado original.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. Entre o Início **do** formulário e o Fim **do** formulário, arraste os Campos de texto de metadados para o formulário. Os usuários preenchem metadados nesses campos de texto, que podem enviar ou concluir outra ação.

1. Clique duas vezes no nome do campo, por exemplo, **Título** para abrir o campo de metadados e fazer alterações. Na guia **Geral** da janela **Editar componente** , defina o namespace e o rótulo do campo, bem como o tipo, por exemplo, `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

Consulte [Personalização e extensão de ativos](/help/assets/extending-assets.md) AEM para obter informações sobre como modificar os namespaces disponíveis no formulário de metadados.

1. Click the **Constraints** tab. Aqui, você pode selecionar se um campo é obrigatório e, se necessário, adicionar quaisquer restrições.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Click the **Display** tab. Aqui, você pode inserir uma nova largura e número de linhas para o campo de metadados. Marque a caixa de seleção **Campo é somente** leitura para permitir que os usuários editem os metadados.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

A seguir está um exemplo de um formulário Metadados com vários campos:

![chlimage_1-162](assets/chlimage_1-390.png)

Na página Editor de ativos, os usuários podem inserir valores nos campos de metadados (se eles forem editáveis) e executar a ação final (por exemplo, enviar as alterações).

#### Subativos {#sub-assets}

O componente Sub-ativos é onde você pode exibir e selecionar subativos. Você pode determinar quais nomes aparecem no ativo [e subativos](/help/assets/assets.md#what-are-digital-assets) principais.

![screen_shot_2012-04-23at24025pm](assets/screen_shot_2012-04-23at24025pm.png)

Clique duas vezes no componente Sub Assets para abrir a caixa de diálogo Sub-ativos, onde você pode alterar os títulos do ativo principal e de quaisquer subativos. Os valores padrão são exibidos abaixo do campo correspondente.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

A seguir está um exemplo de um componente Sub Assets preenchido:

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

Por exemplo, se você selecionar um subativo, observe como o componente exibe a página apropriada e o título da Caixa muda de Sub-ativos para Irmãos.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### Tags {#tags}

O componente Tags é um componente no qual os usuários podem atribuir tags existentes a um ativo, o que ajuda posteriormente na organização e recuperação. Você pode tornar esse componente somente leitura, de modo que os usuários não possam adicionar tags, mas apenas visualizá-las.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

Clique duas vezes no componente Tags para abrir a caixa de diálogo de tags, onde você pode alterar o título de Tags, se desejar, e onde você pode selecionar os namespaces alocados. Para tornar esse campo editável, desmarque a caixa de seleção **[!UICONTROL Ocultar edição]** . Por padrão, as tags são editáveis.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

Se os usuários puderem editar tags, poderão clicar no lápis para adicionar tags selecionando-as no menu suspenso Tags.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

A seguir está um componente de Tags preenchido:

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### Miniatura {#thumbnail}

O componente Miniatura é o local em que o ativo exibe a miniatura selecionada (para muitos dos formatos, a miniatura é extraída automaticamente). Além disso, o componente exibe o nome do arquivo e [as ações que você pode modificar](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

Clique duas vezes no componente de miniatura para abrir a caixa de diálogo em miniatura, onde é possível alterar o texto alternativo. Por padrão, o texto alternativo em miniatura assume **Click para baixar** o ativo como padrão.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

A seguir está um exemplo de um componente Miniatura preenchido:

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### Título {#title}

O componente Título exibe o título do ativo e uma descrição.

![chlimage_1-163](assets/chlimage_1-391.png)

Por padrão, ele está no modo somente leitura, portanto os usuários não podem editá-lo. Para torná-lo editável, clique duas vezes no componente e desmarque a caixa de seleção **Ocultar botão** de edição. Além disso, insira um título para vários ativos.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

Se o Título puder ser editado, você poderá adicionar um título e uma descrição clicando em Lápis para abrir a janela Propriedades **do** ativo. Além disso, você pode ativar e desativar o ativo selecionando a data e a hora.

Quando os usuários editam o Título clicando no ícone Lápis, eles podem alterar o **Título**, a **Descrição** e digitar os Tempos **Ativado** e **Desativado** para ativar e desativar o ativo.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

A seguir está um exemplo de um componente Título preenchido:

![chlimage_1-164](assets/chlimage_1-392.png)

#### Adicionar ações do Editor de ativos {#adding-asset-editor-actions}

Você pode determinar quais ações os usuários podem executar em ativos digitais selecionados a partir de uma seleção de ações predefinidas.

Para adicionar ações à página Editor de ativos:

1. Na página do Editor de ativos que você deseja personalizar, clique em Editor **de** ativos no sidekick.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

As seguintes ações estão disponíveis:

| Ação | Descrição |
|---|---|
| [!UICONTROL Download] | Permite que os usuários baixem ativos selecionados em seus computadores. |
| [!UICONTROL Editores] | Permite que os usuários editem uma imagem (edição interativa) |
| [!UICONTROL Lightbox] | Salva os ativos em um &quot;lightbox&quot; onde você pode executar outras ações. Isso é útil ao trabalhar com ativos em várias páginas. |
| [!UICONTROL Bloqueio] | Permite que os usuários bloqueiem um ativo. Essa funcionalidade não está ativada por padrão e precisa ser ativada na lista de componentes. |
| [!UICONTROL Referências] | Clique para mostrar em quais páginas o ativo está sendo usado. |
| [!UICONTROL Versões] | Permite criar e restaurar versões de um ativo. |

1. Arraste a ação apropriada para a área **Ações** na página. Isso cria um botão que é usado para executar essa ação.

![chlimage_1-165](assets/chlimage_1-393.png)

## Vários ativos de edição com a página Editor de ativos {#multi-editing-assets-with-the-asset-editor-page}

Com os ativos AEM, é possível fazer alterações em vários ativos ao mesmo tempo. Depois de ter selecionado os ativos, é possível alterar simultaneamente os seguintes itens:

* Tags
* Metadados

Para fazer várias edições de ativos com a página Editor de ativos:

1. Abra a página do Geometrixx **Press Center** :
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. Selecione os ativos:

   * no Windows: `Ctrl + click` cada ativo.
   * no Mac: `Cmd + click` cada ativo.
   Para selecionar uma faixa de ativos: clique no primeiro ativo e depois `Shift + click` no último ativo.

1. Clique em **Editar metadados** no campo **Ações** (parte esquerda da página).
1. A página do Editor **de ativos do Geometrixx** Press Center é aberta em uma nova guia. Os metadados dos ativos são exibidos da seguinte maneira:

   * Uma tag, que não se aplica a todos os ativos, mas apenas a alguns, é exibida em itálico.
   * Uma tag que se aplica a todos os ativos é exibida com uma fonte normal.
   * Metadados diferentes de tags: o valor do campo só será exibido se for o mesmo para todos os ativos selecionados.

1. Clique em **Download** para baixar um arquivo zip que contém as representações originais dos ativos.
1. Clique no ícone de lápis ao lado do campo **Tags** para editar as tags:

   * Uma tag que não se aplica a todos os ativos, mas somente a alguns tem um fundo cinza.
   * Uma tag que se aplica a todos os ativos tem um fundo branco.
   É possível:

   * Clique no ícone **x** para remover a tag de todos os ativos.
   * Clique no ícone **+** para adicionar a tag a todos os ativos.
   * Clique na **seta** e selecione uma tag para adicionar uma nova tag a todos os ativos.
   Clique em **OK** para gravar as alterações no formulário. A caixa ao lado do campo **Tags** é automaticamente marcada.

1. Edite o campo Descrição. Por exemplo, defina como:

   `This is a common description`

   Quando um campo é editado, seu valor substitui os valores existentes dos ativos selecionados quando o formulário é submetido.

   Observação: a caixa ao lado do campo é automaticamente marcada quando o campo é editado.

1. Clique em **Atualizar metadados** para enviar o formulário e salvar as alterações de todos os ativos.

   Observação: somente os metadados marcados são modificados.
