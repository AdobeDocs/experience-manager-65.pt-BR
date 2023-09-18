---
title: Tendências da atividade
description: Adicionar um componente da Lista de atividades da comunidade a uma página
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---

# Tendências da atividade {#activity-trends}

## Introdução {#introduction}

A variável `Community Activity List` O componente permite adicionar informações de tendência sobre publicações e visualizações por membros, bem como publicações e visualizações de conteúdo.

O documento descreve:

* Adicionar o `Community Activity List` componente a um [site da comunidade](/help/communities/overview.md#community-sites).

* Definições de configuração para o `Community Activity List` componente.

### Requisito {#requirement}

Dados para o `Community Activity List` O só está disponível quando o Adobe Analytics é licenciado e configurado para o site da comunidade.

Consulte [Configuração do Analytics para recursos das comunidades](/help/communities/analytics.md).

### Adicionar uma lista de atividades da comunidade a uma página {#adding-a-community-activity-list-to-a-page}

Para adicionar um `Community Activity List` para uma página no modo de autor, localize o componente `Communities / Community Activity List` e arraste-o para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![atividade da comunidade](assets/community-activity.png)

### Configuração da lista de atividades da comunidade  {#configuring-community-activity-list}

Selecione o colocado `Community Activity List` e selecione o `Configure` para que você possa abrir a caixa de diálogo editar.

![configurar](assets/configure-new.png)

No **Comentários** especifique se e como os comentários dos arquivos carregados serão exibidos:

![propriedades](assets/activity-list-properties.png)

* **Tipo**

  Especifique se deseja exibir dados relativos aos membros da comunidade ou conteúdo gerado pelo usuário (UGC).

  Selecionar de:

   * `Members`
   * `Content`

  O padrão é `Members`.

* **Título de exibição**

  Um título descritivo a ser exibido acima dos dados, como `Trending Content`.
O padrão é sem título.

* **Contagem de exibições**

  O número de itens a serem listados.
O padrão é 10.

* **Tipo de atividade**

  Selecione um de:

   * `Views`(visitas à página)
   * `Posts`(criando UGC)
   * `Follows`
   * `Likes`

  O padrão é Exibições.

* **Período de tempo**

  Selecione um de:

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

  O padrão é `Total`.

* **Caminho do contexto**

  Isso permite que você atribua o escopo da atividade a um subconjunto do site, como um Blog específico.
O padrão é todo o site da comunidade.

* **Agregação da contagem de membros**

  Quando desmarcados (desativados), somente os posts de nível superior são contados. Por exemplo, se o contexto for a página raiz (o padrão), uma variável `Activity Type` de `Posts` nunca mostra nenhuma atividade, pois não há capacidade de publicar conteúdo na página raiz. Quando marcadas, as contagens em todas as páginas descendentes são incluídas.
O padrão está marcado.

### Exemplo de página com quatro componentes {#example-page-with-components}

**Principais visitantes** config: Tipo = Membros, Tipo de atividade = Exibições

**Colaboradores principais** config: Tipo = Membros, Tipo de atividade = Publicações

**Conteúdo principal** config: Tipo = Conteúdo, Tipo de atividade = Exibições,

**Conteúdo de tendência** config: Tipo = Conteúdo, Tipo de atividade = Publicações

![componentes](assets/activity-list-components.png)
