---
title: Moderação do contexto interno
description: Saiba como administradores e membros confiáveis da comunidade podem executar ações de moderador nas comunidades do Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Moderação do contexto interno {#in-context-moderation}

Para o AEM Communities, a moderação pode ser executada por administradores e membros confiáveis da comunidade diretamente na página publicada onde o conteúdo da comunidade foi publicado.

Ao usar uma [console de moderação](moderation.md), as informações exibidas para o conteúdo incluem um link para a página publicada para permitir acesso a ações de moderação adicionais disponíveis ao moderar no contexto.

## Ações de moderação {#moderation-actions}

Acesse a visão geral de moderação para obter uma descrição de [ações de moderação](moderate-ugc.md#moderation-actions).

## Moderação da interface do usuário {#moderation-ui}

A interface apresentada ao moderador na instância de publicação está contida na caixa de diálogo para postagem e gerenciamento de conteúdo gerado pelo usuário (UGC). Os elementos da interface são determinados pelo status do visitante do site, sejam eles...

1. O membro que publicou o conteúdo.
1. Um moderador de membro confiável.
1. Um administrador.
1. Conectado, mas não é um administrador, moderador nem autor do conteúdo.
1. Não conectado.

## Exemplo {#example}

Usar o [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) site criado quando [Introdução ao AEM Communities](getting-started.md), é possível configurar um thread em um fórum no qual experimentar várias atividades de moderação no ambiente de Publicação. Veja abaixo.

Aaron McDonald (`aaron.mcdonald@mailinator.com`) foi identificado como um membro confiável da comunidade, adicionando-o ao grupo community-engage-moderators ao criar o site.

Rebekah Larsen (`rebekah.larsen@trashymail.com`) pode ser adicionado como membro do grupo de membros de envolvimento da comunidade usando o [Console de membros](members.md).

Para obter mais informações sobre grupos de usuários da comunidade, visite [Gerenciar usuários e grupos de usuários](users.md).

### Criar as publicações do fórum {#create-the-forum-posts}

* Fazer logon como Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Selecionar fórum
   * Selecionar nova publicação
   * Insira o assunto

     Quando trocar o néctar no Humming Bird Feeder

   * Insira o texto do corpo

     Não tenho tido muito sucesso quando penduro um alimentador de beija-flor todo ano. Parece que eles chegam um ou dois dias, então é isso. Eu troco uma vez por semana é muito tempo? Preciso mudá-la antes?

   * Selecionar publicação
   * Selecione Fazer logoff

* Efetue logon como Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Selecionar fórum
   * Para o Tópico Hummingbird, selecione Ler mais
   * Inserir o comentário para Publicar resposta

     Eu troco as minhas uma vez por semana e as recebo de maio a outubro.

   * Selecionar resposta
   * Selecione Fazer logoff

* Faça logon como Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Selecionar fórum
   * Para o Tópico Hummingbird, selecione Ler mais
   * Inserir o comentário para Publicar resposta

     Eu vendo néctar e alimentadores - visite https://my.viral.url/

   * Selecionar resposta
   * Selecione Fazer logoff

### Visitante anônimo do site (#5) {#anonymous-site-visitor}

A seguir está uma visualização do fórum visualizada por um visitante do site que não está conectado (5).

Um visitante anônimo do site só pode ver o fórum, mas não pode publicar conteúdo nem executar ações de moderação.

![comunidade-fórum-visitante](assets/community-forum-visitor.png)

### Novo membro (#4) {#new-member}

Na criação, faça logon como administrador e adicione Boyd Larsen (boyd.larsen@dodgit.com) como um novo membro do grupo de membros envolvidos pela comunidade usando o [Console de membros](members.md)e, em seguida, Fazer logoff.

Ao publicar, faça logon como Boyd Larsen e acesse o thread selecionando `Forum`e depois `Read more` para o poste de beija-flor.

Aviso:

* Boyd não participou do fórum.
* O Boyd não pode excluir nada.
* O Boyd está conectado e pode Responder ou Sinalizar conteúdo.

Peça a Boyd que selecione Flag para sinalizar o conteúdo publicado por Andrew.

Fazer logoff

![comunidade-fórum-membro](assets/community-forum-member.png)

### Administrador (#3) {#administrator}

Faça logon como Administrador (admin) e acesse o thread selecionando Fórum e, em seguida, Leia mais para uma publicação.

Aviso:

* O administrador pode sinalizar, excluir, editar, negar, recortar, fechar, fixar, recurso.
* O administrador pode selecionar Administração para acessar o console de moderação.

![community-admin-forum](assets/community-admin-forum.png)

Selecione o item de menu Administração para poder acessar o [console de moderação](moderation.md) do Ambiente de publicação.

Observe que, para um administrador, todo o conteúdo moderável está visível, não apenas o conteúdo do site da comunidade do Geometrixx Engage.

O filtro de pesquisa é um painel lateral que alterna entre aberto e fechado.

Fazer logoff.

![moderation-console-publish](assets/moderation-console-publish.png)

### Moderador da comunidade (#2) {#community-moderator}

Efetue logon como Aaron McDonald (`aaron.mcdonal@mailinator.com`), um moderador da comunidade, e acesse o tópico selecionando Fórum e, em seguida, Leia mais na publicação do beija-flor.

Aviso:

* Aaron pode Responder, Excluir, Editar ou Negar sua própria publicação.
* Aaron também pode Sinalizar/Permitir, Responder, Excluir, Editar, Negar outro conteúdo.
* Aaron pode Cortar o tópico do fórum para movê-lo para outro fórum que ele modera.
* Aaron pode selecionar Administração para acessar o console de moderação.

![comunidade-fórum-moderador](assets/community-forum-moderator.png)

Selecione o item de menu Administração para poder acessar o [console de moderação](moderation.md) do Ambiente de publicação.

Observe que, para um moderador da comunidade, somente o conteúdo moderável do site da comunidade do Geometrixx Engage fica visível.

Observe que o moderador da comunidade tem as mesmas opções que o administrador (a imagem está com a barra lateral de pesquisa alternada para fechada), mas sem acesso a outros consoles AEM.

Fazer logoff.

![moderador-access](assets/moderator-access.png)

### Autor de conteúdo (#1) {#content-author}

Efetue logon como Rebekah Larsen (`rebekah.larsen@mailinator.com`), um membro da comunidade que iniciou o thread e acesse o thread selecionando Fórum e, em seguida, Leia mais na publicação do beija-flor.

Aviso:

* Rebekah pode excluir ou editar seu próprio post.
* Rebekah também pode Responder ou Sinalizar outro conteúdo.
* Rebekah não pode acessar o console de moderação.

![comunidade-fórum-autor](assets/community-forum-author.png)
