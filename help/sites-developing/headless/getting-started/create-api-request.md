---
title: Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless
description: Saiba como usar a API REST do Assets do AEM para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 43%
---
# Acesso e entrega de Fragmentos de conteúdo - Guia de início rápido do Headless {#accessing-delivering-content-fragments}

Saiba como usar a API REST do AEM Assets para gerenciar fragmentos de conteúdo e a API do GraphQL para entrega headless do conteúdo do fragmento de conteúdo.

## O que são as APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que criou alguns fragmentos de conteúdo,](create-content-fragment.md) você pode usar as APIs do AEM para entregá-los de forma headless.

* A [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) permite criar solicitações para acessar e fornecer Fragmentos de conteúdo.
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
