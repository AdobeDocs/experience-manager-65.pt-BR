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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Console de relatórios{#reports-console}

## Visão geral {#overview}

Para o AEM Communities, há vários relatórios que podem ser acessados de várias maneiras a partir do ambiente do autor.

Em geral, os vários relatórios são:

* [Relatório](#assignments-report) de Atribuições - para uma comunidade [de](/help/communities/overview.md#enablement-community)ativação, fornece uma visão geral do progresso dos alunos em suas atribuições, incluindo uma pontuação associada ao implementar o padrão SCORM
* [Relatório](#views-report) de exibições - fornece um gráfico de visualizações do conteúdo por membros da comunidade e visitantes do site para qualquer site da comunidade
* [Relatório](#posts-report) de publicações - fornece um gráfico de vários tipos de publicações por membros da comunidade em qualquer site da comunidade

Quando o [Adobe Analytics estiver ativado](/help/communities/sites-console.md#analytics), os relatórios incluirão o número de exibições, reproduções, comentários e classificações de cada recurso de ativação ao longo do tempo

Os relatórios tabulares podem ser exportados no formato .csv para processamento subsequente.

## Consoles de relatório {#reporting-consoles}

### Relatórios para sites da comunidade {#reports-for-community-sites}

* da navegação global : **Navegação**, **Comunidades, Relatórios**

* escolher de

   * **Relatório de atribuições**

      * gerar um relatório para Site da comunidade, Usuário ou Grupo e Atribuição selecionados

      * **Relatório de publicações**

         * gerar um relatório para o Site da comunidade, o Tipo de conteúdo e o Período de tempo selecionados
      * **Relatório de exibições**

         * gerar um relatório para o Site da comunidade, o Tipo de conteúdo e o Período de tempo selecionados


![chlimage_1-236](assets/chlimage_1-236.png)

### Relatórios para recursos de ativação e caminhos de aprendizado {#reports-for-enablement-resources-and-learning-paths}

* da navegação global: **Navegação**, **Comunidades, Recursos**

* selecionar um site de comunidade de ativação existente

   * selecione **Relatório **ícone para gerar relatórios que abrangem todos os recursos de ativação
   * selecionar um caminho de aprendizado de ativação
   * selecione **Relatório **ícone para gerar relatórios para

      * os recursos de ativação incluídos
      * os alunos atribuídos ao caminho de aprendizado

* esses relatórios fornecem:

   * dados da tabela, disponíveis para download como CSV

      * identificando o aluno
      * o seu estatuto
      * atribuído ou acessado pelo catálogo
      * número de comentários feitos
      * classificação por estrela dada

Para obter mais detalhes, consulte a seção [](/help/communities/resources.md#report) Relatórios do console Recursos.

## Relatório de atribuições {#assignments-report}

O console Atribuições permite que os relatórios sejam filtrados por meio da ativação do site da comunidade, usuários ou grupos e atribuição.

O relatório fornece informações sobre o seu progresso, bem como quaisquer comentários ou notações que lhe sejam fornecidos.

![chlimage_1-237](assets/chlimage_1-237.png)

Selecione os critérios para o relatório:

* **Site**

   selecionar um site de comunidade de ativação

* **Usuário ou grupo**
   * selecione Usuário para gerar um relatório para um aluno
   * selecione Grupo para gerar um relatório para um grupo de alunos
   O serviço de túnel acessará membros e grupos membros do ambiente de publicação

* **Atribuição**

   Escolha entre os recursos de ativação atribuídos aos alunos selecionados

Selecione **Gerar** para criar o relatório:

![chlimage_1-238](assets/chlimage_1-238.png)

## Relatório de exibições {#views-report}

O console Exibições permite que relatórios sejam gerados em exibições de página por recursos da comunidade para um determinado período.

![chlimage_1-239](assets/chlimage_1-239.png)

Selecione os critérios para o relatório:

* **Site**

   selecionar um site da comunidade

* **Tipo de conteúdo**

   pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site

* período

   selecione um de

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **Gerar** para criar o relatório:

![chlimage_1-240](assets/chlimage_1-240.png)

## Relatório de publicações {#posts-report}

O console Publicações permite que os relatórios sejam gerados em número de publicações para recursos da comunidade em um determinado período.

![chlimage_1-241](assets/chlimage_1-241.png)

Selecione os critérios para o relatório:

* **Site**

   selecionar um site da comunidade

* **Tipo de conteúdo**

   pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site

* período

   selecione um de

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **Gerar** para criar o relatório:

![chlimage_1-242](assets/chlimage_1-242.png)

## Resolução de Problemas{#troubleshooting}

### Nenhum site da comunidade listado {#no-community-sites-listed}

Se nenhum site da comunidade estiver listado, verifique se o Adobe Analytics foi habilitado para um site. Se você escolher relatórios em atribuições, verifique se a função de atribuições está na estrutura do site da comunidade.

### Os relatórios não são exibidos na instância do autor de AEM {#reports-do-not-show-in-aem-author-instance}

Se os relatórios não forem exibidos na instância de autor de AEM, verifique se há personalizações, como o mapeamento de URL na instância de publicação. Se o mapeamento de URL for feito somente na instância de publicação de AEM do site de comunidades, verifique se o mesmo foi configurado na instância de autor de AEM na **configuração **Site Trend Report Social Component Fatory **configuration.

![Mapeamento de URL no autor do AEM](assets/sitetrend.png)