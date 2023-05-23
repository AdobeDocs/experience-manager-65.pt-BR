---
title: Console de selos
seo-title: Badges Console
description: O console Selos das comunidades permite adicionar selos personalizados que podem ser exibidos para membros quando obtidos (premiados) ou quando assumem uma função específica na comunidade (atribuídos)
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# Console de selos {#badges-console}

## Sobre selos {#about-badges}

O console Selos de comunidades oferece a capacidade de adicionar selos personalizados que podem ser exibidos para um membro quando ganho (premiado) ou quando ele assume uma função específica na comunidade (atribuído).

### Visibilidade do selo {#badge-visibility}

Atualmente, as medalhas que um membro da comunidade ganha ou é atribuído aparecerão junto com seu nome e avatar nos seguintes locais:

* Perfis
* [Fóruns](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Placar de líderes](/help/communities/enabling-leaderboard.md)
* [Ideação](/help/communities/ideation-feature.md)

No ambiente de criação, navegue até o console Emblemas:

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]** > **[!UICONTROL Medalhas]**

Esse console exibe os emblemas disponíveis no momento e a partir dos quais novos emblemas podem ser adicionados.

![badges-homepage](assets/badges-homepage.png)

## Criar selo {#create-badge}

Um selo é criado fazendo upload de uma imagem adequadamente pequena (72 dpi com uma altura variando de 26 a 32 pixels) e fornecendo um nome. A imagem do selo é armazenada no repositório em `/libs/settings/community/badging/images` e é replicado automaticamente para o ambiente de publicação.

Se o ambiente de publicação for um farm de editores, será necessário configurar [sincronização de usuário](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Fazer upload de imagem**

   (*Obrigatório*) Uma imagem de selo com tamanho recomendado de 32 x 32 pixels a 72 dpi no formato JPEG ou PNG.

* **Nome**

   (*Obrigatório*) O nome do selo. É o padrão `Display Name` e o nome do nó de repositório. Se a variável `Name` não é um nome de nó de repositório válido, ele será modificado.

* **Nome de exibição**

   (*Opcional*) O nome a ser exibido para o selo na interface do usuário. O padrão é o texto inalterado inserido para o `Name`.

* **Descrição**

   (*Opcional*) Uma descrição para o selo.

## Informações adicionais {#additional-information}

Para obter detalhes sobre como configurar regras de pontuação e medalha, consulte [Pontuação e medalhas](/help/communities/implementing-scoring.md).

Para gerenciar selos para membros, consulte [Console de membros](/help/communities/members.md).
