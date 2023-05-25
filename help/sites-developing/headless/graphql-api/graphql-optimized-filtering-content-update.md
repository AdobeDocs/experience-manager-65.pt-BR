---
title: Atualizar fragmentos de conteúdo para a filtragem otimizada de GraphQL
description: Saiba como atualizar os fragmentos de conteúdo para uma filtragem otimizada de GraphQL no Adobe Experience Manager para entrega de conteúdo headless.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 42%

---


# Atualizar fragmentos de conteúdo para a filtragem otimizada de GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para otimizar o desempenho dos filtros do GraphQL, execute um procedimento para atualizar os Fragmentos de conteúdo.

>[!NOTE]
>
>Depois de atualizar os fragmentos de conteúdo, você pode seguir as recomendações para [Otimização de consultas do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Pré-requisitos {#prerequisites}

Certifique-se de que você tenha um mínimo da versão 6.5.17.0 do AEM.

## Atualização dos fragmentos de conteúdo {#updating-content-fragments}

Para executar o procedimento, siga as etapas abaixo:

1. [Definir as configurações do OSGi](/help/sites-deploying/configuring-osgi.md) para o **Configuração da tarefa de migração do fragmento de conteúdo**:

   ![Configuração do trabalho de migração do fragmento de conteúdo OSGi](assets/cfm-graphql-update-01.png "Configuração do trabalho de migração do fragmento de conteúdo OSGi")

1. Na caixa de diálogo do, defina esses dois parâmetros da seguinte maneira:

   * **ContentFragmentMigration:Habilitado** : `1`
   * **MigraçãoDeFragmentoDeConteúdo:Aplicar** : `1`

1. **Salvar** as especificações - o procedimento de atualização é iniciado.

1. Aguarde até que o procedimento seja concluído. O procedimento é concluído quando a propriedade `cfGlobalVersion` aparece em `/content/dam` e está definido como `1`.

1. Retorne à configuração do OSGi para desativar o procedimento.

   Na caixa de diálogo do **Configuração da tarefa de migração do fragmento de conteúdo** defina esses dois parâmetros da seguinte maneira:

   * **ContentFragmentMigration:Habilitado** : `0`
   * **MigraçãoDeFragmentoDeConteúdo:Aplicar** : `0`

## Limitações {#limitations}

Esteja ciente das seguintes limitações:

* A otimização do desempenho dos filtros de GraphQL só será possível após uma atualização completa de todos os fragmentos de conteúdo (indicada pela presença da propriedade `cfGlobalVersion` no nó `/content/dam` do JCR)

* Se os fragmentos de conteúdo forem importados de um pacote de conteúdo (usando `crx/de`) depois que o procedimento de atualização for executado, esses fragmentos de conteúdo não serão considerados nos resultados da consulta de GraphQL até que o procedimento de atualização seja executado novamente.