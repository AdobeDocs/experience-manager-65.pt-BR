---
title: Marcação do conteúdo gerado pelo usuário
seo-title: Tagging User Generated Content
description: A marcação do conteúdo gerado pelo usuário (UGC) mostra como os membros da comunidade podem ajudar outros membros a pesquisar conteúdo
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# Marcação do conteúdo gerado pelo usuário {#tagging-user-generated-content}

## Visão geral {#overview}

A marcação de conteúdo gerado pelo usuário (UGC) é o meio pelo qual os membros da comunidade podem ajudar outros membros a pesquisar conteúdo.

Normalmente, as tags são aplicadas por autores e administradores no ambiente de criação. A marcação de UGC é única, pois as tags UGC são aplicadas pelos membros da comunidade no ambiente de publicação.

Os namespaces e as taxonomias de tags são os mesmos para ambos os aplicativos.

## Recursos das comunidades {#communities-features}

Os recursos do AEM Communities que podem ser configurados para permitir a marcação são:

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Biblioteca de arquivo](file-library.md)
* [Fórum](forum.md#configuretheaddedforum)
* [Perguntas e respostas](working-with-qna.md)

## Administração de tags {#administering-tags}

Consulte [Administração de tags](../../help/sites-administering/tags.md#tagging-console) para criar e gerenciar namespaces de tags e taxonomias.

Consulte [Fundamentos de tags](tag.md) para obter informações do desenvolvedor.

Consulte [Uso da Social Tag Cloud](tagcloud.md) para adicionar um componente do Social Tag Cloud a uma página e facilitar a pesquisa de UGC publicado usando as tags aplicadas.

### Permissões de tag {#tag-permissions}

As permissões padrão são definidas para não permitir que os namespaces de tag sejam lidos por todos no ambiente de publicação.

Como as tags são aplicadas a UGC no ambiente de publicação, a permissão de leitura precisa ser ativada para os membros da comunidade para que eles possam selecionar as tags a serem aplicadas.

Consulte [Definição de permissões de tag](../../help/sites-administering/tags.md#setting-tag-permissions).

Veja a seguir como ele aparece no CRXDE quando um administrador aplica permissões de leitura a `/etc/tag/discussions` para o grupo `Community Engage Members`.

![permissões de tag](assets/tag-permissions.png)
