---
title: Console de grupos da comunidade
description: Saiba mais sobre o console Grupos da comunidade que permite criar grupos da comunidade quando a estrutura de modelo de um site da comunidade inclui a função de grupos.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Console de grupos da comunidade {#community-groups-console}

O console Grupos fornece acesso à criação de grupos da comunidade quando a [estrutura de modelo](/help/communities/sites-console.md#step1) de um site da comunidade inclui a [função de grupos](/help/communities/functions.md#groups-function).

* O AEM Communities suporta o aninhamento de grupos dentro de outros grupos. O aninhamento de grupos é possível quando a [estrutura do novo grupo](/help/communities/tools-groups.md) contém a função de grupos.
* Somente para o ambiente de criação, há um assistente de criação de grupo semelhante ao assistente de criação de site.
* Se os membros podem (ou não) criar grupos no ambiente de publicação, é configurável ao adicionar uma função Grupos a uma estrutura de site da comunidade ou de grupo da comunidade.

Dos três modelos de grupo incluídos, somente o modelo `Reference Group` inclui uma função de grupos em sua estrutura.

As diferentes facetas dos grupos da comunidade são:

* **Criação**: o novo grupo pode ser criado no autor e, opcionalmente, na instância de publicação.
* **Controle**: o grupo pode ser aberto ou secreto.
* **Aninhamento**: o grupo pode conter zero ou mais grupos.

<!-- This is a 404 on helpx. Update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), is not listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Este console Grupos, acessível apenas pelo console Sites de Comunidades, não deve ser confundido com o [console Grupos](/help/communities/members.md) do membro para gerenciar grupos de membros.
>
>Os grupos de membros são grupos de usuários registrados no ambiente de publicação e acessados do ambiente de criação usando o [serviço de túnel](/help/communities/deploy-communities.md#tunnel-service-on-author).

## Criação do grupo {#group-creation}

Para acessar o console Grupos:

* Em Autor, faça logon com privilégios de administrador.
* Da navegação global: **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.
* Selecione uma pasta existente do site da comunidade para que você possa abri-la.
* Selecione uma instância de um site da comunidade dentro da pasta.

   * A estrutura do site da comunidade deve incluir uma função de grupos.
   * Estas capturas de tela são do tutorial de Introdução após [criar grupos na publicação](/help/communities/published-site.md).

  ![criar-grupo](assets/create-group.png)

* Selecione a **pasta Grupos** para abri-la.

  Quando abertos, todos os grupos existentes, sejam eles criados em Autor ou Publish, são exibidos.

  Nesse console Grupos, é possível criar novos grupos.

  ![criar-novo-grupo](assets/create-new-group.png)

* Selecione o botão **Criar Grupo**.

### Etapa 1: modelo do grupo da comunidade {#step-community-group-template}

![Grupos de comunidades multilíngues](assets/multi-lingual-group.png)

* **Título do Grupo da Comunidade**

  Um título de exibição para o grupo.
O título é exibido no site publicado do grupo.

* **Descrição do grupo da comunidade**

  Uma descrição do grupo.

* **Raiz do grupo da comunidade**

  O caminho raiz para o grupo.
A raiz padrão é o site pai, mas a raiz pode ser movida para qualquer local no site. Não é recomendável alterá-lo.

* **Idiomas adicionais disponíveis do grupo da comunidade** menu

  Use o menu suspenso para selecionar os idiomas disponíveis do grupo da comunidade. O menu exibe todos os idiomas nos quais o site pai da comunidade é criado. Os usuários podem selecionar entre esses idiomas para criar grupos em vários locais nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites de comunidade.

* **Nome do Grupo da Comunidade**

  O nome da página raiz do grupo que aparece no URL. Evite usar caracteres de sublinhado (_) e palavras-chave, como recursos e configuração no nome do grupo.

   * Verifique novamente o nome, pois ele não pode ser facilmente alterado após a criação do grupo.
   * A URL base é exibida abaixo de `Community Group Name`.
   * Para um URL válido, anexe &quot;.html&quot;

     *por exemplo*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* Menu **Modelo do grupo da comunidade**

  Use o menu suspenso para escolher um [modelo de grupo de comunidades](/help/communities/tools.md) disponível.

### Etapa 2: design {#step-design}

### TEMA DO GRUPO DA COMUNIDADE {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

A estrutura usa o `Twitter Bootstrap` para trazer um design responsivo e flexível para o site. Um dos muitos temas de Bootstrap pré-carregados pode ser selecionado para estilizar o modelo de grupo da comunidade selecionado, ou um tema de Bootstrap pode ser carregado.

Quando selecionado, o tema é sobreposto por uma marca de seleção azul opaca.

É possível selecionar um tema que difere do tema do site principal.

Depois que o site da comunidade for publicado, será possível [editar as propriedades](#modifyinggroupproperties) e selecionar um tema diferente.

### MARCA DE GRUPO DA COMUNIDADE {#community-group-branding}

![marca-grupo-comunidade](assets/community-group-branding.png)

A marca do site da comunidade é uma imagem exibida como um cabeçalho na parte superior de cada página. É possível exibir um banner para o grupo que difere de outras páginas do site.

A imagem deve ser dimensionada para ter a largura esperada da página no navegador e 120 pixels de altura.

Ao criar ou selecionar uma imagem, lembre-se:

* A altura da imagem é cortada para 120 pixels, medidos a partir da borda superior da imagem
* A imagem é fixada na borda esquerda da janela do navegador
* Não há redimensionamento da imagem, de modo que, quando a largura da imagem for:

   * Menor que a largura do navegador, a imagem é repetida horizontalmente.
   * Maior que a largura do navegador, a imagem aparece cortada.

### Etapa 3: Configurações {#step-settings}

**MODERAÇÃO**

![selecionar funções de membro do grupo da comunidade](assets/group-admin.png)

**Moderadores do grupo da comunidade**

Por padrão, a lista de moderadores do site da comunidade principal é herdada.

É possível adicionar moderadores especificamente ao grupo. Procurar por membros (do ambiente de publicação) para adicioná-los como moderadores

**Administradores do grupo**

Por padrão, o administrador pai do site da comunidade também é o administrador dos grupos.

No entanto, é possível atribuir administradores de grupo independentes. Os administradores de grupo podem gerenciar seu grupo (por exemplo, G1) e criar um subgrupo aninhado em G1. Eles podem atribuir administradores diferentes para o subgrupo.

Um usuário U1, portanto, pode ser um administrador em um grupo G1 e um usuário regular em seu grupo aninhado G2.

**ASSOCIAÇÃO**

A configuração de associação permite a seleção de uma das três maneiras de proteger um grupo da comunidade.

![associação-grupo-comunidade](assets/community-group-membership.png)

* **Associação Opcional**

  Se selecionado, o grupo da comunidade será público. Os membros do site podem participar do grupo e publicar sem entrar explicitamente no grupo. O padrão está selecionado.

* **Associação necessária**

  Se selecionado, o grupo da comunidade será aberto. Os membros do site da comunidade podem exibir o conteúdo do grupo, mas devem ingressar no grupo para publicar conteúdo. Os membros ingressam selecionando o botão `Join` no ambiente de publicação. O padrão não está selecionado.

* **Associação restrita**

  Se selecionado, o grupo da comunidade será um grupo secreto. Os membros da comunidade devem ser convidados explicitamente. Os membros convidados são inseridos na caixa de pesquisa. Os membros podem ser adicionados posteriormente usando os [consoles Membros e Grupos](/help/communities/members.md) do ambiente de criação. O padrão não está selecionado.

**MINIATURA**

![miniatura de grupo da comunidade](assets/community-group-thumbnail.png)

A miniatura é uma imagem a ser exibida para o grupo no autor e na publicação.

O tamanho ideal para uma imagem de grupo é de 170 x 90 pixels em um formato de imagem compatível (como JPG ou PNG).

Se nenhuma imagem for adicionada, uma imagem padrão será exibida.

![imagem-miniatura](assets/thumbnail-image.png)

### Etapa 4: Criar grupo {#step-create-group}

![community-create-group](assets/community-create-group.png)

Se forem necessários ajustes, use o botão **Voltar** para fazer os ajustes.

Depois que **Criar** é selecionado e iniciado, o processo de criação do grupo não pode ser interrompido.

Quando o processo for concluído, o cartão do novo site da subcomunidade (grupo) será exibido no console Grupos do Sites de comunidades, no qual os autores podem adicionar conteúdo à página, ou os administradores podem modificar as propriedades do site.

![criar grupo da comunidade](assets/create-community-groups.png)

>[!NOTE]
>
>O grupo é criado em todos os idiomas, conforme especificado em [Etapa 1: Modelo do grupo da comunidade](/help/communities/groups.md#step-community-group-template) em Idiomas adicionais disponíveis do grupo da comunidade, no console Grupos da comunidade dos respectivos sites da comunidade.

## Conteúdo do grupo de autores {#author-group-content}

![open-site](assets/open-site.png)

O conteúdo da página de um grupo pode ser criado com as mesmas ferramentas de qualquer outra página AEM. Para abrir o grupo para criação, selecione o ícone Abrir site que aparece ao passar o mouse sobre o cartão de grupo.

## Modificar propriedades do grupo {#modify-group-properties}

As propriedades de um site da subcomunidade existente, especificadas durante o processo de criação do grupo da comunidade, podem ser modificadas ao selecionar o ícone Editar site que aparece ao passar o mouse sobre o cartão do grupo:

![editar-site](assets/edit-site.png)

Os detalhes das seguintes propriedades correspondem às descrições fornecidas na seção [Criação de Grupo](#group-creation). Qualquer grupo aninhado pode ser modificado, seja criado no ambiente de publicação ou no ambiente de autor.

![grupo-comunidade-básico](assets/community-group-basic.png)

### Modificar Básico {#modify-basic}

O painel BÁSICO permite a modificação de

* Título do grupo da comunidade
* Descrição do grupo da comunidade

O Nome do grupo da comunidade não pode ser modificado.

Escolher um modelo de grupo da comunidade diferente não teria efeito em um site de grupo da comunidade existente, pois nenhuma conexão permanece entre modelos e sites.

Em vez disso, a [ESTRUTURA](#modify-structure) da subcomunidade pode ser modificada.

### Modificar estrutura {#modify-structure}

O painel ESTRUTURA permite a modificação da estrutura criada inicialmente a partir do modelo de grupo da comunidade selecionado ao criar o site da subcomunidade a partir do ambiente do autor ou de publicação. No painel, é possível:

* Arraste e solte [funções adicionais da comunidade](/help/communities/functions.md) na estrutura do site.
* Em uma instância de uma função da comunidade na estrutura do site:

   * **`Gear icon`**
Edite as configurações, incluindo o título de exibição, a URL e os [grupos de membros privilegiados](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Remover (excluir) funções da estrutura do site.

   * **`Grid icon`**
Modifique a ordem das funções conforme exibidas na barra de navegação de nível superior do site.

>[!CAUTION]
>
>Embora o título de exibição possa ser alterado sem efeitos colaterais, não é recomendável editar o nome do URL de uma função da comunidade que pertence a um site da comunidade.
>
>Por exemplo, renomear o URL não move o UGC existente, portanto, tem o efeito de &quot;perder&quot; o UGC.

>[!CAUTION]
>
>A função de grupos deve *não* ser a *primeira nem a única* função na estrutura do site.
>
>Qualquer outra função, como a [função de página](/help/communities/functions.md#page-function), deve ser incluída e listada primeiro.

**Exemplo: Adicionando uma Função de Calendário a uma Estrutura de Subcomunidade (Grupo)**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### Modificar design {#modify-design}

O painel DESIGN permite a modificação do tema:

* [Tema do grupo da comunidade](#community-group-theme)
* [Marca de grupo da comunidade](#community-group-branding)

   * Role até a parte inferior do painel para que você possa alterar a imagem da marca.

### Modificar configurações {#modify-settings}

O painel CONFIGURAÇÕES permite adicionar a comunidade [moderadores](#moderation).

### Modificar Associação {#modify-membership}

O painel [ASSOCIAÇÃO](#membership) é apenas informativo. Não é possível alterar o tipo de associação de grupo estabelecido, seja ele opcional, obrigatório ou restrito.

### Modificar miniatura {#modify-thumbnail}

O painel [MINIATURA](#thumbnail) permite que uma imagem seja carregada para representar o grupo da comunidade para os visitantes do site no ambiente Publish e no console Grupos do Site de Comunidades no ambiente de criação.

## Publish o grupo {#publish-the-group}

![publicar-site](assets/publish-site.png)

Depois que um grupo da comunidade for recém-criado ou modificado, é possível publicar (ativar) o grupo selecionando o ícone `Publish Site`.

Depois que o grupo for publicado com êxito, a seguinte mensagem será exibida:

![grupo-publicado](assets/group-published.png)

>[!CAUTION]
>
>O site da comunidade principal e os grupos principais já devem ter sido publicados.
>
>O site da comunidade e os grupos aninhados devem ser publicados de cima para baixo.

## Excluir o grupo {#delete-the-group}

![ícone excluir](assets/deleteicon.png)

Exclua um grupo do console Grupos da comunidade, selecionando o ícone Excluir grupo, que aparece ao passar o mouse sobre o grupo.

Isso remove todos os itens associados ao grupo, por exemplo, todo o conteúdo do grupo é permanentemente excluído e as associações de usuário são removidas do sistema.
