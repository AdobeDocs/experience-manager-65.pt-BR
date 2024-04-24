---
title: Funções da comunidade
description: Saiba como acessar o console de Funções da comunidade
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# Funções da comunidade{#community-functions}

O tipo de recursos esperados de uma experiência da comunidade são bem conhecidos. Os recursos da comunidade estão disponíveis como funções da comunidade. Basicamente, elas são uma ou mais páginas pré-conectadas para implementar um recurso da comunidade que requer mais do que simplesmente adicionar um componente a uma página no modo de criação. São os blocos de construção usados para definir a estrutura de um [modelo do site da comunidade](/help/communities/sites.md) de onde os sites da comunidade são [criado](/help/communities/sites-console.md).

Após criar um site da comunidade, o conteúdo pode ser adicionado às páginas resultantes usando o padrão [Modo de criação do AEM](/help/sites-authoring/editing-content.md). Várias funções da comunidade estão disponíveis, conforme visto no console de funções da comunidade.

>[!NOTE]
>
>Os consoles para a criação de [sites da comunidade](/help/communities/sites-console.md), [modelos de site da comunidade](/help/communities/sites.md), [modelos de grupo da comunidade](/help/communities/tools-groups.md), e [funções da comunidade](/help/communities/functions.md) são para uso somente no ambiente de criação.

## Console de funções da comunidade {#community-functions-console}

Para acessar o console de funções de comunidade no ambiente de criação:

* Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]** > **[!UICONTROL Funções da comunidade]**.

![funções da comunidade](assets/community-functions.png)

## Funções pré-criadas {#pre-built-functions}

Veja a seguir uma breve descrição das funções fornecidas com o AEM Communities. Cada função inclui uma ou mais páginas AEM contendo componentes Communities conectados em um recurso que é facilmente incorporado a um [modelo do site da comunidade](/help/communities/sites.md).

Um modelo de site da comunidade fornece a estrutura de um site da comunidade, incluindo logon, perfis de usuário, notificações, mensagens, menu do site, pesquisa, temas e recursos de marca.

### Configurações de título e URL {#title-and-url-settings}

**Título** e **URL** são propriedades comuns a todas as funções da comunidade.

Quando uma função da comunidade é adicionada a um modelo de site da comunidade ou adicionada quando [modificação](/help/communities/sites-console.md#modifying-site-properties) estrutura de um site da comunidade, a caixa de diálogo da função será aberta para que o Título e o URL possam ser configurados.

#### Detalhes da função de configuração {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Título**

  (*Obrigatório*) O texto que aparece no menu de recursos do site

* **URL**

  (*Obrigatório*) O nome usado para gerar o URI. O nome deve estar em conformidade com o [convenções de nomenclatura](/help/sites-developing/naming-conventions.md) impostos pelo AEM e pelo JCR.

Por exemplo, usar o site criado a partir do seguinte [Introdução](/help/communities/getting-started.md) tutorial, se

* Título = Página da Web
* URL = página

Em seguida, o URL para a página é https://localhost:4503/content/sites/engage/en/page.html

e o link de menu da página será exibido como:

![página de envolvimento](assets/engage-page.png)

### Função de fluxo de atividades {#activity-stream-function}

A função de fluxo de atividade é uma página com uma [Componente de Fluxos de atividade](/help/communities/activities.md) com todas as exibições selecionadas (todas as atividades, atividades do usuário e seguintes). Consulte também [Fundamentos do fluxo de atividades](/help/communities/essentials-activities.md) para desenvolvedores.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

#### Detalhes da função de configuração {#configuration-function-details-1}

![detalhes-função](assets/function-details.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Mostrar a exibição &quot;Minhas atividades&quot;**

  Se selecionada, a página Atividades incluirá uma guia que filtra as atividades com base naquelas geradas dentro da comunidade pelo membro atual. O padrão está selecionado.

* **Mostrar a exibição &quot;Todas as atividades&quot;**

  Se selecionada, a página Atividades inclui uma guia que inclui todas as atividades geradas na comunidade à qual o membro atual tem acesso. O padrão está selecionado.

* **Mostrar a exibição &quot;Feed de notícias&quot;**

  Se for selecionada, as páginas Atividades incluirão uma guia que filtra as atividades com base naquelas que o membro atual está seguindo. O padrão está selecionado.

### Função do blog {#blog-function}

A função de blog é uma página com um [Componente do blog](/help/communities/blog-feature.md) configurado para marcação, uploads de arquivo, acompanhamento, membros para autoedição, votação e moderação. Consulte também [Fundamentos do blog](/help/communities/blog-developer-basics.md) para desenvolvedores.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![componente de blog](assets/blog-component.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Permitir membros privilegiados**

  Se selecionado, o blog permitirá que apenas membros privilegiados criem artigos, permitindo a seleção de um [grupo de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão criar. O padrão está desmarcado.

* **Permitir carregamentos de arquivo**

  Se selecionado, o blog incluirá a capacidade de os membros fazerem upload de arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas**

  Se não for selecionada, o blog permitirá respostas (comentários) a um artigo, mas respostas a comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo em destaque**

  Se selecionado, o blog é identificado como [conteúdo em destaque](/help/communities/featured.md). O padrão está selecionado.

### Função do calendário {#calendar-function}

A função de calendário é uma página com um [Componente do calendário](/help/communities/calendar.md) configurado para permitir marcação. Consulte também [Fundamentos do calendário](/help/communities/calendar-basics-for-developers.md) para desenvolvedores.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![calendar-details](assets/calendar-details.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Permitir fixação**

  Se selecionada, o fórum permitirá que as respostas de tópico sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros privilegiados**

  Se selecionado, o blog permitirá que apenas membros privilegiados criem artigos, permitindo a seleção de um [grupo de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão criar. O padrão está desmarcado.

* **Permitir carregamentos de arquivo**

  Se selecionado, o blog incluirá a capacidade de os membros fazerem upload de arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas**

  Se não for selecionada, o blog permitirá respostas (comentários) a um artigo, mas respostas a comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo em destaque**

  Se selecionado, seu conteúdo é identificado como [conteúdo em destaque](/help/communities/featured.md). O padrão está selecionado.

### Função de conteúdo em destaque {#featured-content-function}

A função de conteúdo em destaque é uma página com um [Componente do conteúdo em destaque](/help/communities/featured.md) configurado para permitir que comentários sejam adicionados e excluídos.

A capacidade de apresentar conteúdo pode ser permitida ou não por componente (consulte [Função do blog](#blog-function), [Função do calendário](#calendar-function), [Função do fórum](#forum-function), [Função de ideação](#ideation-function), e [Função QnA](#qna-function)).

Quando adicionado a um modelo, a única configuração é para o [Configurações de título e URL](#title-and-url-settings).

### Função da biblioteca de arquivo {#file-library-function}

A função de biblioteca de arquivos é uma página com um [Componente da biblioteca de arquivos](/help/communities/file-library.md) configurado para permitir que comentários sejam adicionados e excluídos.

Quando adicionado a um modelo, a única configuração é para o [Configurações de título e URL](#title-and-url-settings).

### Função do fórum {#forum-function}

A função de fórum é uma página com um [Componente do fórum](/help/communities/forum.md) configurado para marcação, uploads de arquivo, acompanhamento, membros para autoedição, votação e moderação.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

#### Detalhes da função de configuração {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Permitir fixação**

  Se selecionada, o fórum permitirá que as respostas de tópico sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros privilegiados**

  Se selecionado, o fórum só permitirá que membros privilegiados publiquem tópicos, permitindo a seleção de um [grupo de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir carregamentos de arquivo**

  Se selecionado, o fórum incluirá a capacidade de os membros fazerem upload de arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas**

  Se não for selecionada, o fórum permitirá comentários sobre um tópico, mas as respostas a esses comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo em destaque**

  Se selecionado, o conteúdo do componente é identificado como [conteúdo em destaque](/help/communities/featured.md). O padrão está selecionado.

### Função Grupos {#groups-function}

>[!CAUTION]
>
>A função groups deve *não* ser o *primeiro nem único* função em uma estrutura do site ou em um modelo de site da comunidade.
>
>Qualquer outra função, como a [função de página](#page-function), devem ser incluídos e listados primeiro.

A função de grupos oferece a capacidade de os membros da comunidade criarem subcomunidades dentro do site da comunidade no ambiente de publicação.

Dependendo do(a) [configurações](/help/communities/sites-console.md#groupmanagement) quando a função Grupos é incluída em um [modelo do site da comunidade](/help/communities/sites.md), os grupos podem ser públicos ou privados e um ou mais modelos de grupo da comunidade podem ser configurados para fornecer uma seleção de modelos quando o grupo da comunidade for realmente criado (como no ambiente de publicação). A [modelo de grupo da comunidade](/help/communities/tools-groups.md) especifica quais recursos das Comunidades são criados para as páginas do grupo, como fóruns e calendários.

Quando um grupo da comunidade é criado, um grupo de membros é criado dinamicamente para o novo grupo, ao qual os membros podem ser atribuídos ou associados. Para obter mais informações, consulte [Gerenciar usuários e grupos de usuários](/help/communities/users.md).

A partir das comunidades [pacote de recursos 1](/help/communities/deploy-communities.md#latestfeaturepack), os grupos da comunidade são criados no ambiente de criação usando o [Console de grupos do Sites de comunidades](/help/communities/groups.md), e podem ser criadas no ambiente de publicação quando ativado.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![group-template-config](assets/group-template-config.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Selecionar modelos de grupo**

  Uma lista suspensa que permite a seleção de um ou mais modelos de grupo ativados, a partir dos quais o criador futuro de um novo grupo da comunidade (no ambiente de publicação) poderá escolher.

* **Permitir membros privilegiados**

  Se selecionado, o fórum só permitirá que membros privilegiados publiquem tópicos, permitindo a seleção de um [grupo de segurança de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir publicação da criação**

  Se essa opção for selecionada, os membros autorizados da comunidade poderão criar um grupo no ambiente de publicação. Se desmarcado, novos grupos (subcomunidades) só poderão ser criados no ambiente de criação do console Grupos de sites de comunidades.
O padrão está selecionado.

### Função de ideação {#ideation-function}

A função de ideação é uma página com uma [Componente de ideação](/help/communities/ideation-feature.md).

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta, especificando o Título padrão, os nomes de URL e as configurações de exibição padrão do modelo:

![ideação-função](assets/ideation-function.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Permitir membros privilegiados**

  Se selecionado, o fórum só permitirá que membros privilegiados publiquem tópicos, permitindo a seleção de um [grupo de segurança de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir carregamentos de arquivo**

  Se selecionada, a ideia inclui a capacidade de os membros fazerem upload de arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas**

  Se não for selecionada, a ideia permitirá respostas (comentários) a um tópico, mas respostas a comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo em destaque**

  Se selecionado, seu conteúdo é identificado como [conteúdo em destaque](/help/communities/featured.md). O padrão está selecionado.

### Função do Placar de líderes {#leaderboard-function}

A função de placar de líderes é uma página com uma [Componente do quadro de classificação](/help/communities/enabling-leaderboard.md).

**NOTA**: o componente de Quadro de classificação precisa de mais configuração *após* um site da comunidade é criado a partir de um modelo da comunidade que inclui a função Placar de líderes. Especificar o do componente de Quadro de classificação [regras](/help/communities/enabling-leaderboard.md#rules-tab), que dependem da configuração de [pontuação e medalhas](/help/communities/implementing-scoring.md) para o site da comunidade.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta, especificando o Título padrão, os nomes de URL e as configurações de exibição padrão do modelo:

![quadro de classificação-diálogo](assets/leaderboard-dialog.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Exibir insígnia**

  Se selecionada, uma coluna para ícones de selo será incluída no quadro de classificação.
O padrão está desmarcado.

* **Exibir nome da insígnia**

  Se selecionada, uma coluna para o nome da medalha é incluída no quadro de classificação.
O padrão está desmarcado.

* **Exibir Avatar**

  Se selecionada, a imagem do avatar do membro será incluída no quadro de classificação, ao lado do link de nome para o perfil do membro.
O padrão está desmarcado.

### Função da página {#page-function}

A função de página adiciona uma página em branco ao site da comunidade que está conectada aos recursos do site da comunidade: logon, menu, notificações, mensagens, temas e marca. O conteúdo é adicionado à página usando o [modo de criação padrão do AEM](/help/sites-authoring/editing-content.md).

Quando adicionado a um modelo, a única configuração é para o [Configurações de título e URL](#title-and-url-settings).

### Função QnA {#qna-function}

A função QnA é uma página com um [Componente QnA](/help/communities/working-with-qna.md) configurado para marcação, uploads de arquivo, acompanhamento, membros para autoedição, votação e moderação.

Quando adicionada a um modelo, a configuração permite a restrição a membros privilegiados:

![qna-dialog](assets/qna-dialog.png)

* [Configurações de título e URL](#title-and-url-settings)

* **Permitir fixação**

  Se selecionada, o fórum permitirá que as respostas de tópico sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros privilegiados**

  Se selecionado, o fórum QnA só permitirá que membros privilegiados postem perguntas, permitindo a seleção de um [grupo de membros privilegiados](/help/communities/users.md#privileged-members-group). Se não for selecionada, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir carregamentos de arquivo**

  Se selecionado, o fórum QnA incluirá a capacidade de os membros fazerem upload de arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas**

  Se não for selecionada, o fórum QnA permitirá comentários (respostas) para uma pergunta publicada, mas as respostas às respostas não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo em destaque**

  Se selecionado, seu conteúdo é identificado como [conteúdo em destaque](/help/communities/featured.md). O padrão está selecionado.

## Criar função da comunidade {#create-community-function}

A capacidade de criar uma função da comunidade é alcançada ao selecionar o `Create Community Function` ícone localizado na parte superior do console Funções da comunidade. Várias funções baseadas no mesmo blueprint AEM podem ser criadas e personalizadas de forma exclusiva ao abrir no modo de edição do autor.

![create-community-function](assets/create-community-function.png)

### Nome da função da comunidade {#community-function-name}

![function-name](assets/function-name.png)

No painel Nome da função da comunidade, um nome, uma descrição e se a função está ativada ou desativada são configurados:

* **Nome da função da comunidade**

  O nome da função usada para exibição e armazenamento.

* **Descrição da função da comunidade**

  A descrição da função para exibição.

* **Desativado/Ativado**

  Um switch que controla se a função é referenciável.

### Blueprint AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

No `AEM Blueprint` é possível selecionar o blueprint que é a implementação subjacente da função da comunidade.

A função da comunidade é um mini site que inclui uma ou mais páginas, pré-conectadas para inclusão em um site da comunidade, incluindo logon, perfis de usuário, notificações, mensagens, menu do site, pesquisa, temas e recursos de marca. Depois que a função é criada, é possível [abra a função](#open-community-function) no modo de edição do autor e personalize a página ou as configurações do componente.

Como a função da comunidade é implementada como um [live copy](/help/sites-administering/msm.md#live-copies) de um [blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint), é possível implantar alterações feitas em uma função que afeta todas as páginas de site da comunidade criadas no [modelo do site da comunidade](/help/communities/sites.md) ou [modelo de grupo da comunidade](/help/communities/tools-groups.md) que incluía a função. Também é possível desassociar uma página do blueprint principal para fazer modificações no nível da página.

Consulte também [Gerenciador de vários sites](/help/sites-administering/msm.md).

### Miniatura  {#thumbnail}

![miniatura de função](assets/funtion-thumbnail.png)

No painel Miniatura, uma imagem pode ser carregada para ser exibida no [Console de funções da comunidade](#community-functions-console).

## Abrir função da comunidade {#open-community-function}

![open-function](assets/open-function.png)

Selecione o `Open Community Function` ícone para entrar no modo de edição do autor para criar o conteúdo da página e modificar a configuração do(s) componente(s) de recurso.

### Configurar componentes {#configuring-components}

Uma função da comunidade é implementada como uma Live Copy de um Blueprint do AEM, cujos detalhes estão documentados em [Gerenciador de vários sites](/help/sites-administering/msm.md).

É possível não apenas criar o conteúdo da página, mas configurar os componentes.

Se configurar um componente em uma página de um site da comunidade criado, talvez seja necessário cancelar [herança](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para configurar o componente. A herança deve ser restabelecida quando a configuração for concluída.

Para obter detalhes sobre a configuração, visite [Componentes das comunidades](/help/communities/author-communities.md) para autores.

## Editar função da comunidade {#edit-community-function}

![edit-function](assets/edit-function.png)

Selecione o `Edit Community Function` ícone para editar as propriedades da função usando os mesmos painéis que [criação de uma função da comunidade](#create-community-function), incluindo ativar ou desativar a função.
