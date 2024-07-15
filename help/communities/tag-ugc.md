---
title: Marcação do conteúdo gerado pelo usuário
description: A marcação do conteúdo gerado pelo usuário (UGC) mostra como os membros da comunidade podem ajudar outros membros a pesquisar conteúdo
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
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

Consulte [Administrando tags](../../help/sites-administering/tags.md#tagging-console) para criar e gerenciar namespaces de tags e taxonomias.

Consulte o [Tag Essentials](tag.md) para obter informações sobre desenvolvedores.

Consulte [Usando a Nuvem de Tags Sociais](tagcloud.md) para adicionar um componente da Nuvem de Tags Sociais a uma página para facilitar a pesquisa de UGC publicado usando as tags aplicadas.

### Permissões de tag {#tag-permissions}

As permissões padrão são definidas para não permitir que os namespaces de tag sejam lidos por todos no ambiente de publicação.

Como as tags são aplicadas a UGC no ambiente de publicação, a permissão de leitura precisa ser ativada para os membros da comunidade para que eles possam selecionar as tags a serem aplicadas.

Consulte [Definindo Permissões de Marca](../../help/sites-administering/tags.md#setting-tag-permissions).

Veja a seguir como ele aparece no CRXDE quando um administrador aplica permissões de leitura a `/etc/tag/discussions` para o grupo `Community Engage Members`.

![permissões de tag](assets/tag-permissions.png)
