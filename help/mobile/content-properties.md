---
title: Propriedades e nós do conteúdo
seo-title: Propriedades e nós do conteúdo
description: Siga esta página para saber mais sobre as propriedades e os nós do conteúdo.
seo-description: Siga esta página para saber mais sobre as propriedades e os nós do conteúdo.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Propriedades e nós do conteúdo {#content-properties-and-nodes}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Artigos, banners e coleções são representados como cq:Pages no AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer cq:Page, além de várias outras mostradas abaixo que representam os metadados dos serviços sob demanda do Adobe Experience Manager (AEM) Mobile e as propriedades de suporte da integração.

As tabelas a seguir descrevem as propriedades e os nós do conteúdo.

## Propriedades de integração comuns {#common-integration-properties}

| **Nome da Propriedade** | **Tipo** | **Valores padrão ou valores esperados** | **Descrição** |
|---|---|---|---|
| dps-id | Sequência de caracteres |  | atribuído pelo AEM Mobile e armazenado pelo AEM depois de carregado no AEM Mobile ou importado do AEM Mobile |
| dps-resourceType | Sequência de caracteres | dps:Article | dps:Banner | dps:Collection | propriedade de tipo de entidade |
| dps-version | Sequência de caracteres |  | versão da entidade do AEM Mobile (também contida na aemm-id completa) |
| dps-lastSynced | Data |  | data da última sincronização/importação do AEM Mobile para o AEM |
| dps-lastUploaded | Data |  | data do último upload do AEM para o AEM Mobile |
| dps-lastUploadedBy | String:userid |  | usuário de ID que realizou a última solicitação de upload do AEM para o AEM Mobile |

## Propriedades de metadados principais {#core-metadata-properties}

| Nome da Propriedade | Tipo | Valores padrão ou valores esperados |
|--- |--- |--- |
| dps-title | Sequência de caracteres |  |
| dps-shortTitle | Sequência de caracteres |  |
| dps-abstract | Sequência de caracteres |  |
| dps-shortAbstract | Sequência de caracteres |  |
| departamento de dps | Sequência de caracteres |  |
| dps-category | Sequência de caracteres |  |
| palavras-chave dps | Sequência de caracteres[] |  |
| dps-internalKeywords | Sequência de caracteres[] |  |
| importância de dps | Sequência de caracteres[] | Importância de {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artigos {#articles}

| **Nome da Propriedade** | **Tipo** | **Valores padrão ou valores esperados** |
|---|---|---|
| dps-author | Sequência de caracteres |  |
| dps-authorURL | Sequência de caracteres |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | Sequência de caracteres | ProtectedAccess de {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Sequência de caracteres |  |
| dps-articleText | Sequência de caracteres |  |
| dps-url | Sequência de caracteres |  |

### Banners {#banners}

| **Nome da Propriedade** | **Tipo** | **Valores padrão ou valores esperados** |
|---|---|---|
| dps-tapAction |  | TapAction de {webLink} |
| dps-tapActionUrl |  |  |

### Coleções {#collections}

| Nome da Propriedade | Tipo | Valores padrão ou valores esperados |
|--- |--- |--- |
| dps-productId | Sequência de caracteres |  |
| dps-readingPosition | Sequência de caracteres | de {&quot;reset&quot;,&quot;retém&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Sequência de caracteres | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Sequência de caracteres |  |

## Nós de conteúdo {#content-nodes}

### Nós comuns {#common-nodes}

| Nome do nó | Tipo | Valores padrão ou valores esperados | Descrição |
--- |--- |--- |--- |
| imagem | jcr:PrimaryType=nt: <br> sling não estruturado:resourceType=base/components/image |  |  |

### Entidades {#entities}

#### Artigos {#articles-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| social-share-image |  | jcr:PrimaryType=nt: <br> sling não estruturado:resourceType=base/components/image |  |

#### Banners {#banners-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|---|---|---|---|
| ND |  |  |  |

#### Coleções {#collections-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| background-image | jcr:PrimaryType=nt: <br> sling não estruturado:resourceType=base/components/image |  |  |
