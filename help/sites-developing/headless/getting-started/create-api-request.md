---
title: Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless
description: Saiba como usar a API REST do AEM Assets para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 26%

---

# Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless {#accessing-delivering-content-fragments}

Saiba como usar a API REST do AEM Assets para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.

## O que são as APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que criou alguns fragmentos de conteúdo,](create-content-fragment.md) você pode usar as APIs do AEM para entregá-los de forma headless.

* [A API do GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) O permite criar solicitações para acessar e entregar Fragmentos de conteúdo.
   * Para usar isso, [Os endpoints do devem ser definidos e ativados no AEM](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)e, se necessário, [Interface GraphiQL instalada](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [A API REST do Assets](/help/assets/assets-api-content-fragments.md) permite criar e modificar fragmentos de conteúdo (e outros ativos).

O restante deste guia se concentra no acesso ao GraphQL e na entrega de fragmentos de conteúdo.

## Como fornecer um fragmento de conteúdo usando o GraphQL {#how-to-deliver-a-content-fragment}

Os arquitetos da informação devem projetar consultas para seus endpoints de canal para fornecer conteúdo. Essas consultas só devem ser consideradas uma vez por endpoint por modelo. Para os propósitos deste guia de introdução, você só deve criar um.

1. Faça logon no AEM e acesse o [Interface GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * Por exemplo: `http://<host>:<port>/aem/graphiql.html`.

1. O GraphiQL é um editor de consultas no navegador para GraphQL. Você pode usá-lo para criar consultas para recuperar Fragmentos de conteúdo e entregá-los de forma headless como JSON.
   * O painel esquerdo permite criar a consulta.
   * O painel direito exibe os resultados.
   * O Editor de consultas tem recursos de autocompletar código e teclas de atalho para executar a consulta com facilidade.
     ![Editor do GraphiQL](assets/graphiql.png)

1. Supondo que o modelo criado era chamado `person` com campos `firstName`, `lastName`, e `position`, você pode criar uma consulta simples para recuperar o conteúdo do fragmento de conteúdo.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Insira a consulta no painel esquerdo.
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. Clique em **Executar consulta** (seta para a direita) ou use o ícone `Ctrl-Enter` A tecla de atalho e os resultados são exibidos como JSON no painel direito.
   ![Resultados do GraphiQL](assets/graphiql-results.png)

1. Clique em:
   * **Documentação** na parte superior direita da página para mostrar a documentação contextual para ajudá-lo a criar suas consultas que se adaptam aos seus próprios modelos.
   * **Histórico** na barra de ferramentas superior para mostrar consultas anteriores.
   * **Salvar como** e **Salvar** para salvar suas consultas, após o que você pode listá-las e recuperá-las do **Consultas persistentes** painel e **Publish**.
     ![Documentação do GraphiQL](assets/graphiql-documentation.png)

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas e entrega excessiva. Em vez disso, permite a entrega em massa exatamente do que é necessário para a renderização, como resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo headless no AEM. Há muito mais recursos onde você pode se aprofundar para obter uma compreensão abrangente dos recursos disponíveis.

* **[Navegador de configuração](create-configuration.md)** - Para obter detalhes sobre o Navegador de configuração do AEM
* **[Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)** - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[IDE GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** para obter mais detalhes sobre o uso do GraphiQL IDE
* **[Consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md)** para obter mais detalhes sobre consultas persistentes
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/assets-api-content-fragments.md)** - Para obter detalhes sobre como acessar conteúdo do AEM diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - Para obter detalhes sobre como fornecer Fragmentos de conteúdo de forma headless
