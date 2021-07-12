---
title: Console de emblemas
seo-title: Console de emblemas
description: O console Símbolos de Comunidades permite que você adicione emblemas personalizados que podem ser exibidos para membros quando ganhados (atribuídos) ou quando assumem uma função específica na comunidade (atribuídos)
seo-description: O console Símbolos de Comunidades permite que você adicione emblemas personalizados que podem ser exibidos para membros quando ganhados (atribuídos) ou quando assumem uma função específica na comunidade (atribuídos)
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
source-wordcount: '319'
ht-degree: 4%

---

# Console de emblemas {#badges-console}

## Sobre os emblemas {#about-badges}

O console Símbolos de Comunidades oferece a capacidade de adicionar emblemas personalizados que podem ser exibidos para um membro quando ganhados (atribuídos) ou quando assumem uma função específica na comunidade (atribuídos).

### Visibilidade do emblema {#badge-visibility}

Atualmente, os emblemas que um membro da comunidade recebe ou é atribuído serão exibidos junto com seu nome e avatar nos seguintes locais:

* Perfis
* [Fóruns](/help/communities/forum.md)
* [Perguntas e respostas](/help/communities/working-with-qna.md)
* [Painéis de líderes](/help/communities/enabling-leaderboard.md)
* [Ideação](/help/communities/ideation-feature.md)

No ambiente de criação, navegue até o console Badges :

* Na navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Símbolos]**

Esse console exibe os emblemas disponíveis no momento e a partir dos quais novos emblemas podem ser adicionados.

![badges-homepage](assets/badges-homepage.png)

## Criar selo {#create-badge}

Um selo é criado fazendo o upload de uma imagem suficientemente pequena (72dpi com uma altura entre 26 e 32 pixels) e fornecendo um nome. A imagem do selo é armazenada no repositório em `/libs/settings/community/badging/images` e é replicada automaticamente no ambiente de publicação.

Se o ambiente de publicação for um farm de editores, é necessário configurar [user sync](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Carregar imagem**

   (*Obrigatório*) Uma imagem de selo com um tamanho recomendado de 32 x 32 pixels a 72dpi no formato JPEG ou PNG.

* **Nome**

   (*Obrigatório*) O nome do símbolo. É o `Display Name` padrão, bem como o nome do nó do repositório. Se `Name` não for um nome de nó de repositório válido, ele será modificado.

* **Nome para exibição**

   (*Opcional*) O nome a ser exibido para o símbolo na interface do usuário. O padrão é o texto inalterado inserido para `Name`.

* **Descrição**

   (*Opcional*) Uma descrição para o símbolo.

## Informações adicionais {#additional-information}

Para obter detalhes sobre como configurar as regras de pontuação e marcação, consulte [Pontuação e Aviso no ícone](/help/communities/implementing-scoring.md).

Para gerenciar emblemas para membros, consulte [Console Membros](/help/communities/members.md).
