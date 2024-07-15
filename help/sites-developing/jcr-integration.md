---
title: Integração JCR
description: Saiba mais sobre algumas dicas para quando você precisa integrar com o Adobe Experience Manager no nível do JCR.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Integração JCR{#jcr-integration}

## Prefira a API de recursos do Sling à API JCR {#prefer-the-sling-resource-api-to-jcr-api}

A API do Sling funciona em um nível mais alto e mais abstrato do que a API JCR. Isso permite que o código seja mais reutilizável e independente do armazenamento subjacente. Isso facilita a inclusão de dados virtuais externos por meio do mecanismo ResourceProvider, se necessário.

## Evitar consultas sempre que possível {#avoid-queries-wherever-possible}

É sempre mais rápido navegar pelo repositório para recuperar dados do que executar uma consulta. Há casos em que as consultas serão necessárias, como uma consulta de usuário final ou a necessidade de encontrar conteúdo estruturado em todo o repositório, mas, para todos os outros casos, é preferível navegar até os nós necessários. As consultas sempre devem ser evitadas na lógica de renderização, como componentes de navegação, uma &quot;lista de itens recentes&quot;, contagens de itens e assim por diante. Nesses casos, é melhor percorrer a hierarquia ou pré-armazenar o resultado em cache para que ele possa ser usado diretamente quando renderizado.

## Restringir o escopo de observação do JCR {#restrict-the-scope-of-jcr-observation}

Ao acompanhar eventos no repositório, é importante restringir o escopo o máximo possível. Por exemplo, é muito melhor ouvir um evento em `/etc/mycompany` do que ouvir em `/etc`. Nunca escute eventos na raiz do repositório. Além disso, certifique-se de que os métodos de retorno de chamada sejam executados o mais rápido possível quando não houver nada para eles fazerem.

## Eliminar o uso do acesso do administrador de JCR {#eliminate-use-of-jcr-admin-access}

A partir do AEM 6, o logon Administrativo foi descontinuado, pois o obteve uma sessão administrativa do ResourceResolverFactory. Em vez disso, contas de serviço devem ser criadas para as operações de back-office que exigiriam esse tipo de acesso, e o ResourceResolverFactory pode ser usado para obter um ResourceResolver para essa conta.
