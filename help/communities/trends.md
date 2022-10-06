---
title: Tendências da atividade
seo-title: Activity Trends
description: Adicionar um componente de Lista de atividades da comunidade a uma página
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# Tendências da atividade {#activity-trends}

## Introdução {#introduction}

O `Community Activity List` O componente fornece a capacidade de adicionar informações de tendência relacionadas a postagens e visualizações por membros, bem como postagens e visualizações de conteúdo.

O documento descreve:

* Adicionar a `Community Activity List` para um [site da comunidade](/help/communities/overview.md#community-sites).

* Configurações para o `Community Activity List` componente.

### Requisito {#requirement}

Dados para a `Community Activity List` O só está disponível quando o Adobe Analytics está licenciado e configurado para o site da comunidade.

Consulte [Configuração do Analytics para recursos das Comunidades](/help/communities/analytics.md).

### Adicionando uma lista de atividades da comunidade a uma página {#adding-a-community-activity-list-to-a-page}

Para adicionar uma `Community Activity List` para uma página no modo autor, localize o componente

* `Communities / Community Activity List`

e arraste-a para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![atividade da comunidade](assets/community-activity.png)

### Configuração da lista de atividades da comunidade  {#configuring-community-activity-list}

Selecione o `Community Activity List` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Em **Comentários** , especifique se e como os comentários dos arquivos carregados são exibidos:

![propriedades](assets/activity-list-properties.png)

* **Tipo**

   Especifique se deseja exibir dados relativos aos membros da comunidade ou ao conteúdo gerado pelo usuário (UGC).

   Selecione de:

   * `Members`
   * `Content`

   O padrão é `Members`.

* **Título de exibição**

   Um título descritivo a ser exibido acima dos dados, como `Trending Content`.
O padrão não é um título.

* **Contagem de exibições**

   O número de itens a serem listados.
O padrão é 10.

* **Tipo de atividade**

   Selecione um dos seguintes:

   * `Views`(visitas à página)
   * `Posts`(criação de UGC)
   * `Follows`
   * `Likes`

   O padrão é Exibições.

* **Período de tempo**

   Selecione um dos seguintes:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   O padrão é `Total`.

* **Caminho do contexto**

   Fornece a capacidade de escopo da atividade para um subconjunto do site, como um Blog específico.
O padrão é todo o site da comunidade.

* **Agregação da contagem de membros**

   Quando desmarcado (desativado), somente as publicações de nível superior são contadas. Por exemplo, se o contexto for a página raiz (o padrão), então uma `Activity Type` de `Posts` O nunca mostrará nenhuma atividade, pois não há capacidade de postar conteúdo na página raiz. Quando marcado, as contagens em todas as páginas descendentes são incluídas.
O padrão está marcado.

### Exemplo de página com 4 componentes {#example-page-with-components}

**Visitantes principais** configuração: Tipo = Membros, Tipo de atividade = Visualizações

**Principais colaboradores** configuração: Tipo = Membros, Tipo de atividade = Publicações

**Conteúdo principal** configuração: Tipo = Conteúdo, Tipo de atividade = Exibições,

**Conteúdo de tendência** configuração: Tipo = Conteúdo, Tipo de atividade = Publicações

![componentes](assets/activity-list-components.png)
