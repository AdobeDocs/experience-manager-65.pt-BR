---
title: Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo
description: Entenda a autenticação necessária para consultas de GraphQL remotas do AEM, para proteger sua entrega de conteúdo headless.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: 9278ba4fe85edca4ab5741f89c0fc0ef2cf2764d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 61%

---

# Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso principal para A [API GraphQL da Adobe Experience Manager (AEM) para entrega de fragmento de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md) O é aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticada para garantir a entrega de conteúdo headless.

>[!NOTE]
>
>Para testes e desenvolvimento, também é possível acessar a API GraphQL do AEM diretamente, usando a [interface GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Para autenticação, o serviço de terceiros precisa ser autenticado usando o nome de usuário e a senha da conta AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
