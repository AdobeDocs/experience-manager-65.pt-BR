---
title: Criação
seo-title: Criação
description: Conceitos de criação no AEM
seo-description: Conceitos de criação no AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Criação{#authoring}

## Conceito de criação (e publicação) {#concept-of-authoring-and-publishing}

O AEM oferece dois ambientes:

* Autor
* Publicação

Eles interagem para permitir a você tornar conteúdo disponível no website, para que os visitantes possam lê-lo.

O ambiente de criação oferece os mecanismos para criação, atualização e análise desse conteúdo, antes de realmente publicá-lo:

* Um autor cria e analisa o conteúdo (que pode ser de vários tipos; por exemplo, páginas, ativos, publicações etc)
* que será, em algum ponto, publicado no website.

![chlimage_1-132](assets/chlimage_1-132.png)

No ambiente de criação, a funcionalidade do AEM é disponibilizada por meio de duas interfaces de usuário. Para o ambiente de publicação, você projeta toda a aparência e comportamento da interface disponível para os usuários.

>[!NOTE]
>
>O próprio AEM é usado para criar a documentação do AEM.
>
>Junto com o Dispatcher, ele também é usado para publicação.

### Ambiente de criação {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados para criar, editar ou publicar conteúdos.

Dependendo do modo como sua instância e seus direitos de acesso pessoais estão configurados, você pode executar muitas tarefas no seu conteúdo, incluindo (dentre outras):

* gerar conteúdo novo ou editar no conteúdo existente em uma página
* usar modelos predefinidos para criar novas páginas de conteúdo
* criar, editar e gerenciar seus ativos e coleções
* criar, editar e gerenciar seus aplicativos
* desenvolver suas campanhas e os recursos relacionados
* desenvolver e administrar sites da comunidade
* mover, copiar ou excluir páginas de conteúdo, ativos etc
* publicar (ou desfazer a publicação de) páginas, ativos etc

Além disso, há tarefas administrativas que o ajudam a gerenciar seu conteúdo:

* fluxos de trabalho que controlam como as alterações são gerenciadas; por exemplo, impor uma análise antes da publicação
* projetos que coordenam tarefas individuais

>[!NOTE]
>
>O AEM também é [administrado](/help/sites-administering/home.md) (para uma grande parte das tarefas) no ambiente do autor.

#### Ambiente de publicação {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. Aqui, as páginas do site são disponibilizadas ao público-alvo pretendido de acordo com a aparência da interface projetada.

Normalmente, o ambiente de publicação está localizado dentro da zona desmilitarizada; em outras palavras, disponível para a Internet, mas não mais sob a proteção total da rede interna.

Quando o site do AEM é um [site da comunidade](/help/communities/overview.md), ou inclui [ componentes do Communities](/help/communities/author-communities.md), visitantes do site que fizeram logon (membros) podem interagir com recursos do Communities. Por exemplo, eles podem postar em um fórum, postar um comentário ou seguir outros membros. Os membros podem receber permissão para executar atividades normalmente limitadas para o ambiente de criação, como criar novas páginas (grupos da comunidade), artigos de blog e moderar publicações de outros membros.

>[!NOTE]
>
>Infelizmente, há uma sobreposição na terminologia usada. Isso pode acontecer ao:
>
>* **Publicar / Não publicar**
   >  Esses são os termos principais das ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
   >
   >
* **Ativar / Desativar**
   >  Esses termos são sinônimos de publicar/desfazer a publicação.
   >
   >
* **Replicar / Replicação**
   >  Estes são os termos técnicos usados para indicar a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro; Ou seja, ao publicar ou reverter a replicação de comentários do usuário.
>



#### Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
