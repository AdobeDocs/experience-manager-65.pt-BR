---
title: Console de símbolos
seo-title: Console de símbolos
description: O console Caracteres das comunidades permite que você adicione emblemas personalizados que podem ser exibidos para membros quando ganhados (premiados) ou quando assumem uma função específica na comunidade (atribuídos)
seo-description: O console Caracteres das comunidades permite que você adicione emblemas personalizados que podem ser exibidos para membros quando ganhados (premiados) ou quando assumem uma função específica na comunidade (atribuídos)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Console de símbolos{#badges-console}

## Sobre emblemas {#about-badges}

O console Distintos de comunidades fornece a capacidade de adicionar emblemas personalizados que podem ser exibidos para um membro quando obtidos (concedidos) ou quando assumem uma função específica na comunidade (atribuídos).

### Visibilidade do selo {#badge-visibility}

Atualmente, os emblemas que um membro da comunidade recebe ou está atribuído serão exibidos junto com seu nome e avatar nos seguintes locais:

* perfis
* [fóruns](/help/communities/forum.md)
* [Perguntas e respostas](/help/communities/working-with-qna.md)
* [quadros](/help/communities/enabling-leaderboard.md)
* [ideação](/help/communities/ideation-feature.md)

No ambiente do autor, para acessar o console Distintos

* da navegação global : **Ferramentas, comunidades, emblemas**

Esse console exibe os emblemas disponíveis no momento e a partir dos quais novos emblemas podem ser adicionados.

![chlimage_1-123](assets/chlimage_1-123.png)

## Criar selo {#create-badge}

Um crachá é criado fazendo upload de uma imagem bem pequena (72 dpi com uma altura entre 26 e 32 pixels) e fornecendo um nome. A imagem do crachá é armazenada no repositório em `/etc/community/badging/images` e é replicada automaticamente para o ambiente de publicação.

Se o ambiente de publicação for um farm de editores, será necessário configurar a sincronização [](/help/communities/sync.md)do usuário.

![chlimage_1-124](assets/chlimage_1-124.png)

* **Carregar imagem**(*obrigatório*) Uma imagem de emblema com um tamanho recomendado de 32 x 32 pixels em 72 dpi no formato JPEG ou PNG.

* **Nome**(*obrigatório*) O nome do crachá. É o nome padrão `Display Name` e o nome do nó do repositório. Se o nome do nó do repositório não `Name` for válido, ele será modificado.

* **Nome** de exibição (*opcional*) O nome a ser exibido para o crachá na interface do usuário. Padrão é o texto inalterado inserido para o `Name`.

* **Descrição**(*opcional*) Uma descrição para o crachá.

## Informações adicionais {#additional-information}

Para obter detalhes sobre como configurar regras de pontuação e marcação, consulte [Pontuação e Distintos](/help/communities/implementing-scoring.md).

Para gerenciar emblemas para membros, consulte Console [](/help/communities/members.md)Membros.
