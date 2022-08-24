---
title: Integração JCR
seo-title: JCR Integration
description: Dicas para quando você deve integrar no nível do JCR
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Integração JCR{#jcr-integration}

## Preferir a API do recurso Sling para a API JCR {#prefer-the-sling-resource-api-to-jcr-api}

A API do Sling funciona em um nível mais alto e mais abstrato que a API do JCR. Isso permite que seu código seja mais reutilizável e independente do armazenamento subjacente. Isso facilita a inclusão de dados virtuais externos por meio do mecanismo ResourceProvider, se necessário.

## Evite consultas sempre que possível {#avoid-queries-wherever-possible}

É sempre mais rápido navegar no repositório para recuperar dados do que executar um query. Há casos em que as consultas serão necessárias, como uma consulta de usuário final ou a necessidade de localizar conteúdo estruturado em todo o repositório, mas para todos os outros casos, é preferível navegar até os nós necessários. As consultas devem ser sempre evitadas na lógica de renderização, como componentes de navegação, uma &quot;lista de itens recentes&quot;, contagens de itens e assim por diante. Nesses casos, é melhor percorrer a hierarquia ou pré-armazenar o resultado em cache para que ele possa ser usado diretamente quando renderizado.

## Restringir o escopo da observação do JCR {#restrict-the-scope-of-jcr-observation}

Ao acompanhar eventos no repositório, é importante restringir o escopo o máximo possível. Por exemplo, é muito melhor ouvir um evento em `/etc/mycompany` do que ouvir `/etc`. Nunca acompanhe eventos na raiz do repositório. Além disso, certifique-se de que os métodos de retorno de chamada sejam executados o mais rápido possível quando não houver nada para eles fazerem.

## Eliminar o uso do acesso do administrador do JCR {#eliminate-use-of-jcr-admin-access}

A partir do AEM 6, o login administrativo foi descontinuado, pois recebeu uma sessão administrativa do ResourceResolverFactory. Em vez disso, devem ser criadas contas de serviço para as operações de back office que exigiriam esse tipo de acesso e o ResourceResolverFactory pode ser usado para obter um ResourceResolver para esta conta.
