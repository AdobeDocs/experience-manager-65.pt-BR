---
title: Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless
description: Saiba como usar a API REST do Assets do AEM para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 41%

---

# Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless {#accessing-delivering-content-fragments}

Saiba como usar a API REST do AEM Assets para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.

## O que são as APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que criou alguns fragmentos de conteúdo,](create-content-fragment.md) você pode usar as APIs do AEM para entregá-los de forma headless.

* [A API do GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) permite criar solicitações para acessar e entregar Fragmentos de conteúdo.
   * Para usar isso, [endpoints devem ser definidos e habilitados no AEM](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint) e, se necessário, a [Interface GraphiQL deve ser instalada](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [A API REST do Assets](/help/assets/assets-api-content-fragments.md) permite criar e modificar Fragmentos de conteúdo (e outros ativos).

O restante deste guia terá como foco o acesso ao GraphQL e a entrega de Fragmentos de conteúdo.

## Como fornecer um fragmento de conteúdo usando o GraphQL {#how-to-deliver-a-content-fragment}

Os arquitetos da informação devem projetar consultas para seus endpoints de canal para fornecer conteúdo. Considere essas consultas apenas uma vez por endpoint, por modelo. Para este guia de introdução, crie apenas um.

1. Faça logon no AEM e acesse a [Interface GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * Por exemplo: `http://<host>:<port>/aem/graphiql.html`.

1. O GraphiQL é um editor de consultas no navegador para o GraphQL. Você pode usá-lo para criar consultas para recuperar Fragmentos de conteúdo e entregá-los de forma headless como JSON.
   * O painel esquerdo permite criar a consulta.
   * O painel direito exibe os resultados.
   * O Editor de consultas tem recursos de autocompletar código e teclas de atalho para executar a consulta com facilidade.
     ![Editor do GraphiQL](assets/graphiql.png)

1. Supondo que o modelo criado era chamado `person` com os campos `firstName`, `lastName` e `position`, podemos criar uma consulta simples para recuperar o conteúdo do Fragmento de conteúdo.

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

1. Clique no ícone **Executar Consulta** (seta para a direita) ou use a tecla de atalho `Ctrl-Enter` e os resultados serão exibidos como JSON no painel direito.
   ![Resultados do GraphiQL](assets/graphiql-results.png)

1. Clique em:
   * **Documentação** na parte superior direita da página para mostrar a documentação contextual para ajudá-lo a criar suas consultas que se adaptam aos seus próprios modelos.
   * **Histórico** na barra de ferramentas superior para mostrar consultas anteriores.
   * **Salvar como** e **Salvar** para salvar suas consultas. Depois disso, você poderá listá-las e recuperá-las do painel **Consultas Persistentes** e **Publicar**.
     ![Documentação do GraphiQL](assets/graphiql-documentation.png)

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas e entrega excessiva. Em vez disso, permite a entrega em massa exatamente do que é necessário para a renderização, como resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo headless no AEM. Existem muitos outros recursos onde é possível se aprofundar para obter um entendimento abrangente dos recursos disponíveis.

* **[Navegador de Configuração](create-configuration.md)** - Para obter detalhes sobre o Navegador de Configuração do AEM
* **[Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)** - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** para obter mais detalhes sobre o uso do GraphiQL IDE
* **[Consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md)** para obter mais detalhes sobre consultas persistentes
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/assets-api-content-fragments.md)** - Para obter detalhes sobre como acessar conteúdo do AEM diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - Para obter detalhes sobre como fornecer Fragmentos de conteúdo de forma headless
