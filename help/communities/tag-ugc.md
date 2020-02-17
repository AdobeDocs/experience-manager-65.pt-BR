---
title: Marcação de conteúdo gerado pelo usuário
seo-title: Marcação de conteúdo gerado pelo usuário
description: A marcação do conteúdo gerado pelo usuário (UGC) é a forma como os membros da comunidade podem ajudar outros membros a pesquisar o conteúdo
seo-description: A marcação do conteúdo gerado pelo usuário (UGC) é a forma como os membros da comunidade podem ajudar outros membros a pesquisar o conteúdo
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Marcação de conteúdo gerado pelo usuário {#tagging-user-generated-content}

## Visão geral {#overview}

A marcação de conteúdo gerado pelo usuário (UGC) é o meio pelo qual os membros da comunidade podem ajudar outros membros a pesquisar conteúdo.

Normalmente, as tags são aplicadas por autores e administradores no ambiente do autor. A marcação UGC é exclusiva porque as tags UGC são aplicadas por membros da comunidade no ambiente de publicação.

Os namespaces de tags e as taxonomias são os mesmos para ambos os aplicativos.

## Recursos das comunidades {#communities-features}

Os recursos do AEM Communities que podem ser configurados para permitir a marcação são

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Biblioteca de arquivos](file-library.md)
* [Fórum](forum.md#configuretheaddedforum)
* [Perguntas e respostas](working-with-qna.md)

## Administração de tags {#administering-tags}

Consulte [Administração de tags](../../help/sites-administering/tags.md#tagging-console) para criar e gerenciar namespaces de tags e taxonomias.

Consulte [Tag Essentials](tag.md) para obter informações sobre desenvolvedores.

Consulte [Usar a Nuvem](tagcloud.md) de tags sociais para adicionar um componente da Nuvem de tags sociais a uma página para facilitar a pesquisa por UGC publicado usando as tags aplicadas.

### Permissões de tag {#tag-permissions}

As permissões padrão estão definidas para não permitir que os namespaces de tags sejam lidos por todos no ambiente de publicação.

Como as tags são aplicadas ao UGC no ambiente de publicação, a permissão de leitura precisa ser ativada para membros da comunidade para que possam selecionar as tags a serem aplicadas.

Consulte [Configuração de permissões](../../help/sites-administering/tags.md#setting-tag-permissions)de tag.

Veja a seguir como ele aparece no CRXDE quando um administrador aplica permissões de leitura `/etc/tag/discussions` para o grupo `*Community Engage Members*`.

![chlimage_1-74](assets/chlimage_1-74.png)

