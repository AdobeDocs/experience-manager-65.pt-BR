---
title: Criação
seo-title: Authoring
description: Conceitos de criação no AEM
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 25%

---

# Criação  {#authoring}

## Conceito de criação (e publicação) {#concept-of-authoring-and-publishing}

O AEM fornece dois ambientes:

* Autor
* Publicação

Eles interagem para permitir que você disponibilize conteúdo no seu site, para que os visitantes possam lê-lo.

O ambiente de criação fornece os mecanismos para criar, atualizar e revisar esse conteúdo antes de realmente publicá-lo:

* Um autor cria e revisa o conteúdo (que pode ser de vários tipos; por exemplo, páginas, ativos, publicações etc.)
* que será, em algum momento, publicado no seu site.

![chlimage_1-132](assets/chlimage_1-132.png)

No ambiente de criação, a funcionalidade do AEM é disponibilizada por meio de duas interfaces do usuário. Para o ambiente de publicação, você projeta toda a aparência e comportamento da interface disponível para os usuários.

### Ambiente de criação {#author-environment}

O autor trabalha no que é conhecido como **ambiente do autor**. Isso oferece uma interface fácil de usar (interface gráfica do usuário (GUI ou UI)) para criar o conteúdo. Normalmente, ela está localizada atrás do firewall de uma empresa que fornece proteção total e requer que o autor faça logon, usando uma conta que recebeu os direitos de acesso apropriados.

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados para criar, editar ou publicar conteúdo.

Dependendo de como sua instância e seus direitos de acesso pessoal estão configurados, você pode executar muitas tarefas no conteúdo, incluindo (entre outras):

* gerar novo conteúdo ou editar conteúdo existente em uma página
* usar modelos predefinidos para criar novas páginas de conteúdo
* criar, editar e gerenciar ativos e coleções
* criar, editar e gerenciar suas publicações
* desenvolver suas campanhas e os recursos relacionados
* desenvolver e gerenciar sites da comunidade
* mover, copiar ou excluir páginas de conteúdo, ativos etc
* publicar (ou desfazer a publicação) páginas, ativos, etc

Além disso, há tarefas administrativas que o ajudam a gerenciar seu conteúdo:

* fluxos de trabalho que controlam como as alterações são gerenciadas; por exemplo. imposição de uma revisão antes da publicação
* projetos que coordenam tarefas individuais

>[!NOTE]
>
>O AEM também é [administrado](/help/sites-administering/home.md) (para a maioria das tarefas) do ambiente de criação.

#### Ambiente de publicação {#publish-environment}

Quando pronto, o conteúdo do site do AEM é publicado no **ambiente de publicação**. Aqui, as páginas do site são disponibilizadas para o público desejado de acordo com a aparência da interface projetada.

Normalmente, o ambiente de publicação está localizado dentro da zona desmilitarizada; em outras palavras, disponível para a Internet, mas não mais sob a proteção total da rede interna.

Quando o site AEM é um [site da comunidade](/help/communities/overview.md), ou inclui [Componentes das comunidades](/help/communities/author-communities.md), os visitantes (membros) do site conectados podem interagir com os recursos das Comunidades. Por exemplo, eles podem postar em um fórum, postar um comentário ou seguir outros membros. Os membros podem receber permissão para realizar atividades normalmente limitadas ao ambiente de criação, como criar novas páginas (grupos da comunidade), artigos de blog e moderar as publicações de outros membros.

>[!NOTE]
>
>Infelizmente, às vezes há uma sobreposição na terminologia usada. Isso pode acontecer com:
>
>* **Publicar/Desfazer a publicação**
   >  Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
>
>* **Ativar / Desativar**
   >  Estes termos são sinônimos de publicar/desfazer a publicação.
>
>* **Replicar / Replicação**
   >  Esses são os termos técnicos usados para indicar a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro; ou seja, ao publicar ou reverter a replicação de comentários do usuário.
>


#### Dispatcher {#dispatcher}

Para otimizar o desempenho para os visitantes do seu site, o **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) implementa o balanceamento de carga e o cache.**
