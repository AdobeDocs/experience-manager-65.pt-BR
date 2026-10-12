---
title: Gerenciar endpoints de GraphQL no AEM
description: Saiba como gerenciar endpoints do GraphQL no Adobe Experience Manager para entrega de conteúdo headless.
exl-id: a59a5e50-0787-4c1c-a83d-bb3eac1479a8
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
source-wordcount: '510'
ht-degree: 91%
---
# Gerenciar endpoints de GraphQL no AEM {#graphql-aem-endpoint}

O endpoint é o caminho usado para acessar o GraphQL no AEM. Usando esse caminho, você (ou seu aplicativo) pode:

* acessar o esquema de GraphQL,
* enviar suas consultas de GraphQL,
* receber as respostas (para suas consultas de GraphQL).

Há dois tipos de endpoints no AEM:

* Global
  * Disponível para uso por todos os sites.
  * Esse endpoint pode usar todos os modelos de fragmento de conteúdo de todas as configurações do Sites (definidas no [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
  * Se houver modelos de fragmento de conteúdo que devem ser compartilhados entre as configurações do Sites, eles devem ser criados nas configurações globais do Sites.
* Configurações do Sites:
  * Corresponde a uma configuração do Sites, conforme definido no [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
  * Específico de um site/projeto especificado.
  * Um endpoint específico de uma configuração do Sites usará os modelos de fragmento de conteúdo dessa configuração, junto com aqueles da configuração global do Sites.

>[!CAUTION]
>
>O Editor de fragmento de conteúdo pode permitir que um fragmento de conteúdo de uma configuração do Sites faça referência a um fragmento de conteúdo de outra configuração do Sites (por meio de políticas).
>
>Nesse caso, nem todo o conteúdo poderá ser recuperado usando um endpoint específico de uma configuração do Sites.
>
>O autor de conteúdo deve controlar esse cenário; por exemplo, pode ser útil considerar colocar modelos de fragmento de conteúdo compartilhados na configuração global do Sites.

O caminho do repositório do GraphQL para o endpoint global do AEM é:

`/content/cq:graphql/global/endpoint`

Para o qual seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar um endpoint para GraphQL no AEM, é necessário:

* [Habilitar seu endpoint de GraphQL](#enabling-graphql-endpoint)
* [Publicar seu endpoint de GraphQL](#publishing-graphql-endpoint)

## Habilitação do seu endpoint de GraphQL {#enabling-graphql-endpoint}

Para habilitar um endpoint de GraphQL, primeiro é necessário ter uma configuração apropriada. Consulte [Fragmentos de conteúdo - Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se o [uso de modelos de fragmento de conteúdo não foi habilitado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

Para habilitar o endpoint correspondente:

1. Navegue até **Ferramentas**, **Ativos** e, em seguida, selecione **GraphQL**.
1. Selecione **Criar**.
1. A caixa de diálogo **Criar novo ponto de acesso de GraphQL** será aberta. Aqui, é possível especificar:
   * **Nome**: nome do endpoint; é possível inserir qualquer texto.
   * **Usar o esquema de GraphQL fornecido por**: use a lista suspensa para selecionar o site/projeto necessário.

   >[!NOTE]
   >
   >O seguinte aviso é mostrado na caixa de diálogo:
   >
   >* *Os endpoints do GraphQL podem apresentar problemas de desempenho e de segurança de dados se não forem gerenciados com cuidado. Defina as permissões apropriadas após criar um ponto de extremidade.*

1. Confirme com **Criar**.
1. A caixa de diálogo **Próximas etapas** fornecerá um link direto até o console de Segurança, para que você possa garantir que o endpoint recém-criado tenha as permissões adequadas.

   >[!CAUTION]
   >
   >O endpoint é acessível a todos. Isso pode causar uma preocupação de segurança, especialmente em instâncias de publicação, já que as consultas de GraphQL podem colocar uma carga pesada sobre o servidor.
   >
   >É possível configurar ACLs apropriadas ao seu caso de uso no endpoint.

## Publicar seu endpoint de GraphQL {#publishing-graphql-endpoint}

Selecione o novo endpoint e escolha **Publicar** para disponibilizá-lo completamente, em todos os ambientes.

>[!CAUTION]
>
>O endpoint é acessível a todos.
>
>Isso pode causar uma preocupação de segurança em instâncias de publicação, já que as consultas de GraphQL podem colocar uma carga pesada sobre o servidor.
>
>Configure ACLs apropriadas ao seu caso de uso no endpoint.
