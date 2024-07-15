---
title: Tendências da atividade
description: Adicionar um componente da Lista de atividades da comunidade a uma página
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Tendências da atividade {#activity-trends}

## Introdução {#introduction}

O componente `Community Activity List` permite adicionar informações de tendência sobre postagens e visualizações por membros e postagens e visualizações de conteúdo.

O documento descreve:

* Adicionando o componente `Community Activity List` a um [site da comunidade](/help/communities/overview.md#community-sites).

* Definições de configuração para o componente `Community Activity List`.

### Requisito {#requirement}

Os dados para o `Community Activity List` só estão disponíveis quando o Adobe Analytics é licenciado e configurado para o site da comunidade.

Consulte [Configuração do Analytics para Recursos de Comunidades](/help/communities/analytics.md).

### Adicionar uma lista de atividades da comunidade a uma página {#adding-a-community-activity-list-to-a-page}

Para adicionar um componente `Community Activity List` a uma página no modo de autor, localize o componente `Communities / Community Activity List` e arraste-o para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![atividade-comunidade](assets/community-activity.png)

### Configuração da lista de atividades da comunidade  {#configuring-community-activity-list}

Selecione o componente `Community Activity List` inserido e o ícone `Configure` para que você possa abrir a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **Comentários**, especifique se e como os comentários dos arquivos carregados serão exibidos:

![propriedades](assets/activity-list-properties.png)

* **Tipo**

  Especifique se deseja exibir dados relativos aos membros da comunidade ou conteúdo gerado pelo usuário (UGC).

  Selecionar de:

   * `Members`
   * `Content`

  O padrão é `Members`.

* **Exibir título**

  Um título descritivo a ser exibido acima dos dados, como `Trending Content`.
O padrão é sem título.

* **Exibir contagem**

  O número de itens a serem listados.
O padrão é 10.

* **Tipo de atividade**

  Selecione um de:

   * `Views`(visitas à página)
   * `Posts`(criando UGC)
   * `Follows`
   * `Likes`

  O padrão é Exibições.

* **Período**

  Selecione um de:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  O padrão é `Total`.

* **Caminho de contexto**

  Isso permite que você atribua o escopo da atividade a um subconjunto do site, como um Blog específico.
O padrão é todo o site da comunidade.

* **Agregação de contagem de membros**

  Quando desmarcados (desativados), somente os posts de nível superior são contados. Por exemplo, se o contexto for a página raiz (o padrão), um `Activity Type` de `Posts` nunca mostrará nenhuma atividade, pois não há capacidade de postar conteúdo na página raiz. Quando marcadas, as contagens em todas as páginas descendentes são incluídas.
O padrão está marcado.

### Exemplo de página com quatro componentes {#example-page-with-components}

Configuração de **Principais Visitantes**: Tipo = Membros, Tipo de atividade = Exibições

Configuração de **Principais Colaboradores**: Tipo = Membros, Tipo de atividade = Publicações

Configuração **Conteúdo Principal**: Tipo = Conteúdo, Tipo de atividade = Exibições,

Configuração de **Conteúdo de Tendências**: Tipo = Conteúdo, Tipo de atividade = Publicações

![componentes](assets/activity-list-components.png)
