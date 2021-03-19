---
title: Console de relatórios
seo-title: Console de relatórios
description: Saiba como acessar relatórios
seo-description: Saiba como acessar relatórios
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 7%

---


# Console de relatórios {#reports-console}

## Visão geral {#overview}

Para o AEM Communities, há vários relatórios que podem ser acessados de várias maneiras do ambiente de criação.

Em geral, os diversos relatórios são:

* [Relatório de atribuições](#assignments-report)

   Para uma [comunidade de ativação](/help/communities/overview.md#enablement-community), fornece uma visão geral do progresso dos alunos em suas atribuições, incluindo uma pontuação associada se estiver implementando o padrão SCORM.

* [Relatório de exibições](#views-report)

   Fornece um gráfico de visualizações de conteúdo por membros da comunidade e visitantes do site para qualquer site da comunidade.

* [Relatório de publicações](#posts-report)

   Fornece um gráfico de vários tipos de postagens por membros da comunidade para qualquer site da comunidade.

Quando [Adobe Analytics estiver ativado](/help/communities/sites-console.md#analytics), os relatórios incluirão o número de exibições, reproduções, comentários e classificações para cada recurso de ativação ao longo do tempo.

Os relatórios tabulares podem ser exportados no formato .csv para processamento subsequente.

## Consoles de relatórios {#reporting-consoles}

### Relatórios para sites da comunidade {#reports-for-community-sites}

* Na navegação global: **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Relatórios]**

* Escolha entre:

   * **[!UICONTROL Relatório de atribuições]**

      * Gere um relatório para o Site da Comunidade, Usuário ou Grupo e Atribuição selecionados.
   * **[!UICONTROL Relatório de publicações]**

      * Gere um relatório para o Site da comunidade, Tipo de conteúdo e Período selecionado.
   * **[!UICONTROL Relatório de exibições]**

      * gerar um relatório para o Site da comunidade, Tipo de conteúdo e Período.



![relatórios](assets/reports1.png)

### Relatórios para recursos de ativação e caminhos de aprendizado {#reports-for-enablement-resources-and-learning-paths}

* Na navegação global: **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

* Selecione um site da comunidade de ativação existente:

   * Selecione o ícone **Report** para gerar relatórios que cubram todos os recursos de ativação.
   * Selecione um caminho de aprendizagem de ativação.
   * Selecione o ícone **Relatório** para gerar relatórios para:

      * Os recursos de ativação incluídos.
      * Os alunos atribuídos ao caminho de aprendizado.

* Esses relatórios fornecem:

   * Dados da tabela, baixáveis como CSV:

      * Identificando o aluno
      * Seu status
      * Se atribuído ou acessado pelo catálogo
      * Número de comentários feitos
      * Classificação de estrelas fornecida

Para obter mais detalhes, consulte a [seção Relatórios](/help/communities/resources.md#report) do console Recursos.

## Relatório de atribuições {#assignments-report}

O console Atribuições permite que os relatórios sejam filtrados por ativação do site da comunidade, usuários ou grupos e atribuição.

O relatório fornece informações sobre o seu progresso, bem como quaisquer comentários ou notações fornecidas.

![relatório de atribuição](assets/assignment-report.png)

Selecione os critérios do relatório :

* **Site**

   Selecione um site da comunidade de ativação.

* **Usuário ou grupo**
   * Selecione Usuário para gerar um relatório para um aluno.
   * Selecione Grupo para gerar um relatório para um grupo de alunos.

   O serviço de túnel acessará membros e grupos de membros do ambiente de publicação.

* **Atribuição**

   Escolha entre os recursos de ativação atribuídos ao(s) aluno(s) selecionado(s).

Selecione **Generate** para criar o relatório:

![gerar relatório](assets/generate-assignment-report.png)

## Relatório de exibições {#views-report}

O console Exibições permite que os relatórios sejam gerados nas exibições de página por recursos da comunidade por um determinado período.

![exibir relatório](assets/view-report.png)

Selecione os critérios do relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todos os conteúdos ou selecionar um dos recursos existentes no site.

* **[!UICONTROL Intervalo de tempo]**

   Selecione um dos seguintes:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **[!UICONTROL Generate]** para criar o relatório.

![generate-views](assets/generate-views.png)

## Relatório de publicações {#posts-report}

O console Publicações permite que os relatórios sejam gerados no número de publicações para recursos da comunidade por um determinado período.

![relatório de postagens](assets/posts-report.png)

Selecione os critérios do relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todos os conteúdos ou selecionar um dos recursos existentes no site.

* **[!UICONTROL Intervalo de tempo]**

   Selecione um dos seguintes:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **[!UICONTROL Generate]** para criar o relatório.

![gerar relatório](assets/generate-posts-report.png)

## Resolução de problemas {#troubleshooting}

### Nenhum site da comunidade listado {#no-community-sites-listed}

Se nenhum site da comunidade estiver listado, verifique se o Adobe Analytics foi ativado para um site. Se você escolher relatórios em atribuições, verifique se a função de atribuições está na estrutura do site da comunidade.

### Os relatórios não são exibidos na instância do autor do AEM {#reports-do-not-show-in-aem-author-instance}

Se os relatórios não forem exibidos na instância do autor do AEM, verifique as personalizações, como o mapeamento de URL na instância de publicação. Se o mapeamento de URL for feito somente na instância de publicação do AEM do site de comunidades, verifique se o mesmo foi configurado na instância do autor do AEM na configuração **Site Trend Report Social Component Fatory**.

![Mapeamento de URL no autor do AEM](assets/sitetrend.png)