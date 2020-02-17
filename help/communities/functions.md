---
title: Funções da comunidade
seo-title: Funções da comunidade
description: Saiba como acessar o console Funções da comunidade
seo-description: Saiba como acessar o console Funções da comunidade
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funções da comunidade{#community-functions}

O tipo de recursos esperados de uma experiência da comunidade são bem conhecidos. Os recursos da comunidade estão disponíveis como funções da comunidade. Basicamente, elas são uma ou mais páginas pré-conectadas para implementar um recurso da comunidade que requer mais do que simplesmente adicionar um componente a uma página no modo de autor. Eles são os elementos básicos usados para definir a estrutura de um modelo [de site da](/help/communities/sites.md) comunidade a partir do qual os sites da comunidade são [criados](/help/communities/sites-console.md).

Depois que um site da comunidade é criado, o conteúdo pode ser adicionado às páginas resultantes usando o modo [de criação padrão do](/help/sites-authoring/editing-content.md)AEM. Várias funções da comunidade estão disponíveis, como visto no console de funções da comunidade.

>[!NOTE]
>
>Os consoles para a criação de sites [da](/help/communities/sites-console.md)comunidade, modelos [de site da](/help/communities/sites.md)comunidade, modelos [de grupos da](/help/communities/tools-groups.md)comunidade e funções [da](/help/communities/functions.md) comunidade são para uso somente no ambiente do autor.

## Console de funções da comunidade {#community-functions-console}

No ambiente do autor, para acessar o console de funções da comunidade

* da navegação global: **Ferramentas, Comunidades, Funções da comunidade**

![chlimage_1-106](assets/chlimage_1-106.png)

## Funções pré-criadas {#pre-built-functions}

Veja a seguir uma breve descrição das funções fornecidas com o AEM Communities. Cada função inclui uma ou mais páginas AEM que contêm componentes Comunidades conectados em conjunto em um recurso que é facilmente incorporado a um modelo [de site da](/help/communities/sites.md)comunidade.

Um modelo de site da comunidade fornece a estrutura para um site da comunidade, incluindo logon, perfis de usuário, notificações, mensagens, menu do site, pesquisa, tema e recursos de marca.

### Configurações de título e URL {#title-and-url-settings}

**Título **e **URL **são propriedades comuns a todas as funções da comunidade.

Quando uma função da comunidade é adicionada a um modelo de site da comunidade ou adicionada ao [modificar](/help/communities/sites-console.md#modifying-site-properties) a estrutura de um site da comunidade, a caixa de diálogo da função é aberta para que o Título e o URL possam ser configurados.

#### Detalhes da função de configuração {#configuration-function-details}

![chlimage_1-107](assets/chlimage_1-107.png)

* **Título**(*obrigatório*) O texto que aparece no menu de recursos do site

* **URL**(*obrigatório*) O nome usado para gerar o URI. O nome deve estar em conformidade com as convenções [de](/help/sites-developing/naming-conventions.md) nomenclatura impostas pelo AEM e JCR.

Por exemplo, usar o site criado a partir do acompanhamento do tutorial [Introdução](/help/communities/getting-started.md) , se

* Título = Página da Web
* URL = página

em seguida, o URL da página é https://localhost:4503/content/sites/engage/en/**page**.html

e o link de menu da página é exibido como:

![chlimage_1-108](assets/chlimage_1-108.png)

### Função de fluxo de atividades {#activity-stream-function}

A função de fluxo de atividade é uma página com um componente [de Fluxos de](/help/communities/activities.md) atividade com todas as exibições selecionadas (todas as atividades, atividades do usuário e seguintes). Consulte também [Activity Stream Essentials](/help/communities/essentials-activities.md) para desenvolvedores.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

#### Detalhes da função de configuração {#configuration-function-details-1}

![chlimage_1-109](assets/chlimage_1-109.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Mostrar exibição**&quot;Minhas atividades&quot; Se selecionada, a página Atividades inclui uma guia que filtra as atividades com base nas geradas na comunidade pelo membro atual. O padrão está selecionado.

* **Mostrar exibição**&quot;Todas as atividades&quot; Se selecionada, a página Atividades inclui uma guia que inclui todas as atividades geradas na comunidade às quais o membro atual tem acesso. O padrão está selecionado.

* **Mostrar exibição** do &quot;Feed de notícias&quot; Se selecionado, as páginas de Atividades incluem uma guia que filtra as atividades com base nas atividades que o membro atual está seguindo. O padrão está selecionado.

### Função das atribuições {#assignments-function}

A função de atribuições é o recurso básico que define um site da [comunidade para a ativação](/help/communities/overview.md#enablement-community). Permite a atribuição de recursos de ativação para membros da comunidade. Consulte também [Atribuições essenciais](/help/communities/essentials-assignments.md) para desenvolvedores.

Essa função está disponível como um recurso do complemento de [ativação](/help/communities/enablement.md). O complemento de ativação requer licenciamento adicional para uso em um ambiente de produção.

Quando adicionada a um modelo, a única configuração é para as Configurações [de](#title-and-url-settings)Título e URL.

### Função do blog {#blog-function}

A função de blog é uma página com um componente [de](/help/communities/blog-feature.md) Blog configurado para marcação, uploads de arquivos, a seguir, membros para autoeditar, votar e moderar. Consulte também [Blog Essentials](/help/communities/blog-developer-basics.md) for developers.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![chlimage_1-110](assets/chlimage_1-110.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Permitir membros** privilegiadosSe selecionado, o blog permite somente que membros privilegiados criem artigos permitindo a seleção de um grupo [de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão criar. O padrão está desmarcado.

* **Permitir uploads** de arquivosSe selecionado, o blog inclui a capacidade de os membros carregarem arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas** Se não estiver selecionado, o blog permitirá respostas (comentários) a um artigo, mas as respostas aos comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo** em destaque Se selecionado, o blog é identificado como conteúdo [em](/help/communities/featured.md)destaque. O padrão está selecionado.

### Função do calendário {#calendar-function}

A função de calendário é uma página com um componente [de](/help/communities/calendar.md) Calendário configurado para permitir marcação. Consulte também [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) for developers.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![chlimage_1-111](assets/chlimage_1-111.png)

* consulte Configurações de [título e URL](#title-and-url-settings)
* **Permitir fixação** Se selecionado, o fórum permite que as respostas aos tópicos sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros** privilegiadosSe selecionado, o blog permite somente que membros privilegiados criem artigos permitindo a seleção de um grupo [de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão criar. O padrão está desmarcado.

* **Permitir uploads** de arquivosSe selecionado, o blog inclui a capacidade de os membros carregarem arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas** Se não estiver selecionado, o blog permitirá respostas (comentários) a um artigo, mas as respostas aos comentários não serão permitidas. O padrão está selecionado.

* **Permitir conteúdo** em destaque Se selecionado, seu conteúdo é identificado como conteúdo [em](/help/communities/featured.md)destaque. O padrão está selecionado.

### Função do catálogo {#catalog-function}

A função de catálogo fornece a capacidade de [ativar membros da comunidade](/help/communities/overview.md#enablement-community) para navegar pelos recursos de ativação que não estão atribuídos a eles. Consulte [Marcação de recursos](/help/communities/tag-resources.md) de ativação e [catálogo essenciais](/help/communities/catalog-developer-essentials.md) para desenvolvedores.

Todos os recursos de ativação e caminhos de aprendizado do site da comunidade são exibidos em todos os catálogos se sua propriedade ` [Show in Catalog](/help/communities/resources.md)`, estiver definida como true. Para incluir explicitamente recursos e caminhos de aprendizado, é necessário aplicar um [pré-filtro](/help/communities/catalog-developer-essentials.md#pre-filters) ao catálogo.

Quando adicionada a um modelo, a configuração permite especificar os namespaces de tags usados para configurar o filtro de tags apresentado aos visitantes do site:

![Função de catálogo](assets/catalog-function.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Selecionar todos os namespaces**Os namespaces de tags selecionados definem quais tags podem ser selecionadas pelos visitantes para filtrar a lista de recursos de ativação listados no catálogo.
Se selecionado, todos os namespaces de tags permitidos para o site da comunidade estarão disponíveis.
Se desmarcada, é possível selecionar um ou mais namespaces permitidos para o site da comunidade.
O padrão está selecionado.

### Função de conteúdo em destaque {#featured-content-function}

A função de conteúdo em destaque é uma página com um componente [Conteúdo em](/help/communities/featured.md) destaque configurado para permitir que os comentários sejam adicionados e excluídos.

A capacidade de incluir conteúdo pode ser permitida ou não permitida por componente (consulte Função [do](#blog-function)blog, Função [do](#calendar-function)calendário, Função [do](#forum-function)fórum, Função [de](#ideation-function)ideia e Função [](#qna-function)QnA).

Quando adicionada a um modelo, a única configuração é para as Configurações [de](#title-and-url-settings)Título e URL.

### Função da biblioteca de arquivo {#file-library-function}

A função de biblioteca de arquivos é uma página com um componente [Biblioteca de](/help/communities/file-library.md) arquivos configurado para permitir que os comentários sejam adicionados e excluídos.

Quando adicionada a um modelo, a única configuração é para as Configurações [de](#title-and-url-settings)Título e URL.

### Função do fórum {#forum-function}

A função do fórum é uma página com um componente [do](/help/communities/forum.md) Fórum configurado para marcação, uploads de arquivos, a seguir, membros para autoeditar, votar e moderar.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

#### Detalhes da função de configuração {#configuration-function-details-2}

![chlimage_1-112](assets/chlimage_1-112.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Permitir fixação** Se selecionado, o fórum permite que as respostas aos tópicos sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros** privilegiadosSe selecionado, o fórum só permite que membros privilegiados postem tópicos permitindo a seleção de um grupo [de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir uploads** de arquivosSe selecionado, o fórum inclui a capacidade de os membros carregarem arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas** Se não estiver selecionado, o fórum permite comentários sobre um tópico, mas as respostas a esses comentários não são permitidas. O padrão está selecionado.

* **Permitir conteúdo** em destaque Se selecionado, o conteúdo do componente é identificado como conteúdo [em](/help/communities/featured.md)destaque. O padrão está selecionado.

### Função Grupos {#groups-function}

>[!CAUTION]
>
>A função groups não deve *ser a *primeira nem a única* função na estrutura de um site ou em um modelo de site da comunidade.
>
>Qualquer outra função, como a função [de](#page-function)página, deve ser incluída e listada primeiro.

A função de grupos fornece a capacidade de membros da comunidade criarem subcomunidades dentro do site da comunidade no ambiente de publicação.

Dependendo das [configurações](/help/communities/sites-console.md#groupmanagement) quando a função Grupos é incluída em um modelo [de site da](/help/communities/sites.md)comunidade, os grupos podem ser públicos ou privados e um ou mais modelos de grupo da comunidade podem ser configurados para fornecer uma escolha de modelos quando o grupo da comunidade é realmente criado (como a partir do ambiente de publicação). Um modelo [de grupo da](/help/communities/tools-groups.md) comunidade especifica quais recursos das Comunidades são criados para as páginas de grupo, como fóruns e calendários.

Quando um grupo da comunidade é criado, um grupo de membros é criado dinamicamente para o novo grupo, ao qual os membros podem ser atribuídos ou associados. Para obter mais informações, consulte [Gerenciamento de usuários e grupos](/help/communities/users.md)de usuários.

No pacote de [recursos Comunidades 1](/help/communities/deploy-communities.md#latestfeaturepack), os grupos da comunidade são criados no ambiente do autor usando o console [Grupos do Sites](/help/communities/groups.md)das Comunidades e podem ser criados no ambiente de publicação quando ativados.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta:

![chlimage_1-113](assets/chlimage_1-113.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Selecionar modelos** de grupoUma lista suspensa que permite a seleção de um ou mais modelos de grupo ativados a partir dos quais o futuro criador de um novo grupo de comunidade (no ambiente de publicação) pode escolher.

* **Permitir membros** privilegiadosSe selecionado, o fórum só permite que membros privilegiados postem tópicos permitindo a seleção de um grupo [de segurança de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir criação de publicação**Se selecionada, os membros autorizados da comunidade podem criar um grupo no ambiente de publicação. Se desmarcada, novos grupos (subcomunidades) só poderão ser criados no ambiente do autor a partir do console Grupos do Sites das Comunidades.
O padrão está selecionado.

### Função de ideação {#ideation-function}

A função de ideação é uma página com um componente [de](/help/communities/ideation-feature.md)Ideação.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta, que especifica os nomes padrão de Título e URL, bem como as configurações de exibição padrão do modelo:

![chlimage_1-114](assets/chlimage_1-114.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Permitir membros** privilegiadosSe selecionado, o fórum só permite que membros privilegiados postem tópicos permitindo a seleção de um grupo [de segurança de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir uploads** de arquivosSe selecionada, a ideia inclui a capacidade de os membros carregarem arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas** Se não estiver selecionada, a ideia permite respostas (comentários) a um tópico, mas as respostas aos comentários não são permitidas. O padrão está selecionado.

* **Permitir conteúdo** em destaque Se selecionado, seu conteúdo é identificado como conteúdo [em](/help/communities/featured.md)destaque. O padrão está selecionado.

### Função do Placar de líderes {#leaderboard-function}

A função de quadro de líderes é uma página com um componente [de](/help/communities/enabling-leaderboard.md)Quadro de líderes.

**NOTA**: O componente do Quadro de líderes precisa de mais configuração *depois* que um site da comunidade é criado a partir de um modelo da comunidade que inclui a função do Quadro de líderes. Especifique as [regras](/help/communities/enabling-leaderboard.md#rules-tab)do componente de Quadro de líderes, que dependem da configuração de [pontuação e símbolos](/help/communities/implementing-scoring.md) para o site da comunidade.

Quando adicionada a um modelo, a seguinte caixa de diálogo é aberta, que especifica os nomes padrão de Título e URL, bem como as configurações de exibição padrão do modelo:

![chlimage_1-115](assets/chlimage_1-115.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Exibir emblema**Se selecionado, uma coluna para ícones de emblema é incluída no quadro de líderes.
O padrão está desmarcado.

* **Nome**do selo de exibição Se selecionado, uma coluna para o nome do selo será incluída no quadro de líderes.
O padrão está desmarcado.

* **Exibir avatar**Se selecionada, a imagem de avatar do membro é incluída no quadro de líderes, ao lado do link de nome para o perfil do membro.
O padrão está desmarcado.

### Função da página {#page-function}

A função de página adiciona uma página em branco ao site da comunidade que é conectada aos recursos do site da comunidade: login, menu, notificações, mensagens, temas e marcas. O conteúdo é adicionado à página usando o modo [de criação AEM](/help/sites-authoring/editing-content.md)padrão.

Quando adicionada a um modelo, a única configuração é para as Configurações [de](#title-and-url-settings)Título e URL.

### Função QnA {#qna-function}

A função QnA é uma página com um componente [](/help/communities/working-with-qna.md) QnA configurado para marcação, uploads de arquivos, a seguir, membros para autoeditar, votar e moderação.

Quando adicionada a um modelo, a configuração permite a restrição para membros privilegiados:

![chlimage_1-116](assets/chlimage_1-116.png)

* [Configurações de título e URL](#title-and-url-settings)
* **Permitir fixação** Se selecionado, o fórum permite que as respostas aos tópicos sejam fixadas no início da lista de comentários. O padrão está selecionado.

* **Permitir membros** privilegiados Se selecionado, o fórum QnA só permite que membros privilegiados postem perguntas permitindo a seleção de um grupo [de membros](/help/communities/users.md#privileged-members-group)privilegiados. Se não estiver selecionado, todos os membros da comunidade poderão publicar. O padrão está desmarcado.

* **Permitir uploads** de arquivosSe selecionado, o fórum QnA inclui a capacidade de os membros carregarem arquivos. O padrão está selecionado.

* **Permitir respostas encadeadas** Se não estiver selecionado, o fórum QnA permite comentários (respostas) a uma pergunta publicada, mas as respostas às respostas não são permitidas. O padrão está selecionado.

* **Permitir conteúdo** em destaque Se selecionado, seu conteúdo é identificado como conteúdo [em](/help/communities/featured.md)destaque. O padrão está selecionado.

## Criar função da comunidade {#create-community-function}

A capacidade de criar uma função da comunidade é alcançada selecionando o `Create Community Function` ícone localizado na parte superior do console Funções da comunidade. Várias funções baseadas no mesmo Blueprint do AEM podem ser criadas e personalizadas exclusivamente ao abrir no modo de edição do autor.

![chlimage_1-117](assets/chlimage_1-117.png)

### Nome da função da comunidade {#community-function-name}

![chlimage_1-118](assets/chlimage_1-118.png)

No painel Nome da função da comunidade, um nome, uma descrição e se a função está ativada ou desativada são configurados:

* **Nome** da função da comunidade o nome da função usada para exibição e armazenamento

* **Função da comunidade Descrição** da função para exibição

* **Desativado/Ativado** um interruptor que controla se a função é referenciável

### Blueprint AEM {#aem-blueprint}

![chlimage_1-119](assets/chlimage_1-119.png)

No `AEM Blueprint` painel, é possível selecionar o modelo que é a implementação subjacente da função da comunidade.

A função da comunidade é um mini site que inclui uma ou mais páginas, pré-conectadas para inclusão em um site da comunidade, incluindo logon, perfis de usuário, notificações, mensagens, menu do site, pesquisa, temas e recursos de marca. Depois que a função é criada, é possível [abrir a função](#open-community-function) no modo de edição do autor e personalizar as configurações da página ou do componente.

Como a função da comunidade é implementada como uma cópia [](/help/sites-administering/msm.md#live-copies) ativa de um [blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint), é possível implementar alterações feitas em uma função que afeta todas as páginas do site da comunidade criadas a partir do modelo [de site da](/help/communities/sites.md) comunidade ou do modelo [de grupo da](/help/communities/tools-groups.md) comunidade que incluiu a função. Também é possível desassociar uma página do seu blueprint pai para fazer modificações no nível da página.

Consulte também [Gerenciador](/help/sites-administering/msm.md)de vários sites.

### Miniatura {#thumbnail}

![chlimage_1-120](assets/chlimage_1-120.png)

No painel Miniaturas, uma imagem pode ser carregada para ser exibida no console [Funções da](#community-functions-console)comunidade.

## Abrir função da comunidade {#open-community-function}

![chlimage_1-121](assets/chlimage_1-121.png)

Selecione o `Open Community Function` ícone para entrar no modo de edição do autor para criar o conteúdo da página e modificar a configuração dos componentes do recurso.

### Configuração de componentes {#configuring-components}

Uma função da comunidade é implementada como uma Live Copy de um Blueprint do AEM, cujos detalhes são documentados em [Multi Site Manager](/help/sites-administering/msm.md).

É possível não apenas criar conteúdo de página, mas também configurar componentes.

Se configurar um componente em uma página de um site da comunidade criado, talvez seja necessário cancelar a [herança](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para configurar o componente. A herança deve ser restabelecida quando a configuração for concluída.

Para obter detalhes sobre a configuração, visite Componentes [de](/help/communities/author-communities.md) comunidades para autores.

## Editar função da comunidade {#edit-community-function}

![chlimage_1-122](assets/chlimage_1-122.png)

Selecione o `Edit Community Function` ícone para editar as propriedades da função usando os mesmos painéis que [criar uma função](#create-community-function)da comunidade, incluindo ativar ou desativar a função.
