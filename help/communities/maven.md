---
title: Uso do Maven para comunidades
seo-title: Uso do Maven para comunidades
description: jar de API da AEM Communities e jar de API Uber AEM
seo-description: jar de API da AEM Communities e jar de API Uber AEM
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Uso do Maven para comunidades {#using-maven-for-communities}

## Visão geral {#overview}

Esta seção da documentação da AEM Communities é complementar a:

* [Construção AEM projetos usando o Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Agora existem dois artefatos &quot;uber&quot; que substituem artefatos individuais:

* AEM API [Communities](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Artefato de molar da API das Comunidades {#communities-api-jar-artifact}

Veja a seguir um exemplo de um GAV para o jar de API do AEM Communities:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

Verifique se a versão especificada corresponde à versão do pacote Communities instalada para AEM Communities. Para verificar o número da versão instalada:

1. Faça logon com privilégios administrativos.
1. Navegue até [Package Manager](../../help/sites-administering/package-manager.md). Por exemplo, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Localize o pacote: `cq-socialcommunities-pkg-1.x.xxx`
1. Extraia a versão do nome do pacote:
   * A primeira versão do AEM 6.3 é a versão 1.11.170.
   * Os pacotes de recursos serão as versões 1.12.xxx.

>[!NOTE]
>
>É recomendável manter-se atualizado com a versão mais recente das Comunidades.
>
>Visite a seção Versões [mais recentes](deploy-communities.md#latest-releases) para identificar a versão mais recente.

## Exemplo de Dependência Maven {#maven-dependency-example}

O jar da API Communities deve ser especificado antes do jar da API Uber.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
