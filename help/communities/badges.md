---
title: Console de selos
description: O console Selos das comunidades permite adicionar selos personalizados que podem ser exibidos para membros quando obtidos (concedidos) ou quando assumem uma função específica na comunidade (atribuídos)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# Console de selos {#badges-console}

## Sobre selos {#about-badges}

O console Selos das comunidades permite adicionar selos personalizados que podem ser exibidos para um membro quando ganho (premiado) ou quando ele assume uma função específica na comunidade (atribuído).

### Visibilidade do selo {#badge-visibility}

Atualmente, as medalhas que um membro da comunidade ganha, ou é atribuído, aparecem junto com seu nome e avatar nos seguintes locais:

* Perfis
* [Fóruns](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Placar de líderes](/help/communities/enabling-leaderboard.md)
* [Ideação](/help/communities/ideation-feature.md)

No ambiente de criação, navegue até o console Emblemas:

* Da navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Medalhas]**

Esse console exibe os emblemas disponíveis no momento e a partir dos quais novos emblemas podem ser adicionados.

![medalhas-página inicial](assets/badges-homepage.png)

## Criar selo {#create-badge}

Um símbolo é criado ao fazer upload de uma imagem adequadamente pequena (72 dpi com uma altura variando de 26 a 32 pixels) e fornecer um nome. A imagem do selo é armazenada no repositório em `/libs/settings/community/badging/images` e é replicada automaticamente para o ambiente de publicação.

Se o ambiente de publicação for um farm de editores, será necessário configurar a [sincronização de usuário](/help/communities/sync.md).

![criar-selo](assets/create-badge.png)

* **Fazer upload de imagem**

  (*Obrigatório*) Uma imagem de selo com tamanho recomendado de 32 x 32 pixels a 72 dpi em formato JPEG ou PNG.

* **Nome**

  (*Obrigatório*) O nome do selo. É o `Display Name` padrão e o nome do nó do repositório. Se `Name` não for um nome de nó de repositório válido, ele será modificado.

* **Nome de exibição**

  (*Opcional*) O nome a ser exibido para o selo na interface do usuário. O padrão é o texto inalterado inserido para `Name`.

* **Descrição**

  (*Opcional*) Uma descrição para a medalha.

## Informações adicionais {#additional-information}

Para obter detalhes sobre a configuração das regras de pontuação e medalha, consulte [Pontuação e medalhas](/help/communities/implementing-scoring.md).

Para gerenciar selos para membros, consulte [Console de Membros](/help/communities/members.md).
