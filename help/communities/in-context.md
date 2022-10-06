---
title: Moderação no contexto
seo-title: In-Context Moderation
description: Como executar ações de moderador
seo-description: How to perform moderator actions
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 1%

---

# Moderação no contexto {#in-context-moderation}

Para o AEM Communities, a moderação pode ser executada por administradores e membros confiáveis da comunidade diretamente na página publicada, onde o conteúdo da comunidade foi publicado.

Ao usar um [console de moderação](moderation.md), as informações exibidas para o conteúdo incluem um link para a página publicada para permitir o acesso a ações adicionais de moderação disponíveis ao moderar no contexto.

## Ações de moderação {#moderation-actions}

Visite a visão geral de moderação para obter uma descrição do [ações de moderação](moderate-ugc.md#moderation-actions).

## Interface do usuário de moderação {#moderation-ui}

A interface do usuário apresentada ao moderador na instância de publicação está contida na caixa de diálogo para publicar e gerenciar conteúdo gerado pelo usuário (UGC). Os elementos da interface do usuário são determinados pelo status do visitante do site - sejam eles...

1. O membro que postou o conteúdo.
1. Um moderador de membro confiável.
1. Um administrador.
1. Conectado, mas não é um administrador, moderador ou autor do conteúdo.
1. Não conectado.

## Exemplo {#example}

Usar o [Envolvimento do Geometrixx](http://localhost:4503/content/sites/engage/en.html) site criado ao [Introdução ao AEM Communities](getting-started.md), é possível configurar rapidamente um thread em um fórum no qual você possa realizar várias atividades de moderação no ambiente de publicação, conforme mostrado abaixo.

Aaron McDonald (aaron.mcdonald@mailinator.com) foi identificado como um membro confiável da comunidade ao adicioná-lo ao grupo de moderadores de engajamento da comunidade ao criar o site.

Rebekah Larsen (rebekah.larsen@trashymail.com) pode ser adicionado como membro do grupo de membros do engajamento da comunidade usando o [Console de membros](members.md).

Para obter mais informações sobre grupos de usuários da comunidade, visite [Gerenciar usuários e grupos de usuários](users.md).

### Criar as publicações do fórum {#create-the-forum-posts}

* Faça logon como Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Selecionar Fórum
   * Selecionar Nova Publicação
   * Inserir o Assunto

      Quando mudar o néctar no alimentador de aves de barriga

   * Inserir o texto do corpo

      Não tenho tido muito sucesso quando penduro um alimentador de beija-flor todos os anos. Parece que chegam um ou dois dias depois é isso. Eu mudo uma vez por semana é muito tempo? Preciso mudar isso mais cedo?

   * Selecionar publicação
   * Selecione Fazer logoff

* Faça logon como Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Selecionar Fórum
   * Para o tópico do Hummingbird, selecione Leia mais
   * Inserir o comentário para Resposta da postagem

      Eu troco os meus uma vez por semana e os recebo de maio a outubro.

   * Selecionar resposta
   * Selecione Fazer logoff

* Faça logon como Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Selecionar Fórum
   * Para o tópico do Hummingbird, selecione Leia mais
   * Inserir o comentário para Resposta da postagem

      Eu vendo néctar e alimentadores - visite https://my.viral.url/

   * Selecionar resposta
   * Selecione Fazer logoff

### Visitante Anônimo do Site (#5) {#anonymous-site-visitor}

A seguir, uma exibição do fórum visto por um visitante do site que não está conectado (5).

Um visitante anônimo do site só pode visualizar o fórum, mas não pode publicar nenhum conteúdo nem executar ações de moderação.

![comunidade-fórum-visitor](assets/community-forum-visitor.png)

### Novo Membro (#4) {#new-member}

Na criação, faça logon como administrador e adicione Boyd Larsen (boyd.larsen@dodgit.com) como um novo membro do grupo de membros engajados da comunidade usando a variável [Console de membros](members.md), em seguida, Fazer logoff.

Ao publicar, faça logon como Boyd Larsen e acesse o thread selecionando `Forum`e depois `Read more` para o posto de beija-flor.

Aviso:

* Boyd não participou do fórum.
* Boyd não pode excluir nada.
* O Boyd está conectado e pode responder ou sinalizar conteúdo.

Faça com que Boyd selecione Sinalizar para sinalizar o conteúdo publicado por Andrew.

Fazer logoff

![comunidade-fórum-membro](assets/community-forum-member.png)

### Administrador (#3) {#administrator}

Faça logon como administrador (administrador) e acesse o thread selecionando Fórum e Leia mais para uma publicação.

Aviso:

* O administrador pode Sinalizar, Excluir, Editar, Negar, Recortar, Fechar, Fixar, Recurso.
* O administrador pode selecionar Administração para acessar o console de moderação.

![community-admin-forum](assets/community-admin-forum.png)

Selecione o item de menu Administração para acessar o [console de moderação](moderation.md) do ambiente de publicação.

Observe que, para um administrador, todo o conteúdo moderável é visível, não apenas o conteúdo do site da comunidade Geometrixx Engage.

O filtro de pesquisa é um painel lateral que alterna para aberto ou fechado.

Fazer logoff.

![moderation-console-publish](assets/moderation-console-publish.png)

### Moderador de comunidade (#2) {#community-moderator}

Faça logon como Aaron McDonald (aaron.mcdonal@mailinator.com), um moderador da comunidade e acesse o thread selecionando Forum e, em seguida, Leia mais para a publicação de beija-flor.

Aviso:

* Aaron pode Responder, Excluir, Editar ou Negar sua própria publicação.
* Aaron também pode Sinalizar/Permitir, Responder, Excluir, Editar, Negar outro conteúdo.
* Aaron pode cortar o tópico do fórum para movê-lo para outro fórum para o qual ele modera.
* Aaron pode selecionar Administração para acessar o console de moderação.

![comunidade-fórum-moderator](assets/community-forum-moderator.png)

Selecione o item de menu Administração para acessar o [console de moderação](moderation.md) do ambiente de publicação.

Observe que, para um moderador da comunidade, somente o conteúdo moderável do site da comunidade do Geometrixx Engage está visível.

Observe que o moderador da comunidade tem as mesmas opções que o administrador (a imagem está com a barra lateral de pesquisa alternada fechada), mas não tem acesso a outros consoles de AEM.

Fazer logoff.

![acesso do moderador](assets/moderator-access.png)

### Autor de conteúdo (#1) {#content-author}

Faça logon como Rebekah Larsen (rebekah.larsen@mailinator.com), um membro da comunidade que iniciou o thread, e acesse o thread selecionando Forum e, em seguida, Leia mais para a publicação de beija-flor.

Aviso:

* Rebekah pode excluir ou editar sua própria publicação.
* Rebekah também pode Responder ou Sinalizar outro conteúdo.
* Rebekah não pode acessar o console de moderação.

![community-forum-author](assets/community-forum-author.png)
