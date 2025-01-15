---
title: Nós e propriedades de conteúdo
description: Siga esta página para saber mais sobre propriedades de conteúdo e nós.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 21%

---

# Nós e propriedades de conteúdo {#content-properties-and-nodes}

{{ue-over-mobile}}

Artigos, Banners e Coleções são representados como cq:Pages no AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer cq:Page, além de várias outras mostradas abaixo que representam os metadados dos serviços por demanda do Adobe Experience Manager (AEM) Mobile e as propriedades de suporte à integração.

As tabelas a seguir descrevem as propriedades de conteúdo e os nós.

## Propriedades comuns de integração {#common-integration-properties}

| **Nome da Propriedade** | **Tipo** | **Valores Padrões ou Esperados** | **Descrição** |
|---|---|---|---|
| dps-id | String |  | atribuído pelo AEM Mobile e armazenado pelo AEM depois de carregado no AEM Mobile ou importado do AEM Mobile |
| dps-resourceType | String | dps:Article | dps:Banner | dps:Collection | propriedade de tipo de entidade |
| dps-version | String |  | versão da entidade AEM Mobile (também contida na aemm-id completa) |
| dps-lastSynced | Data |  | data da última sincronização/importação do AEM Mobile para o AEM |
| dps-lastUploaded | Data |  | data do último upload do AEM para o AEM Mobile |
| dps-lastUploadedBy | Cadeia de caracteres:ID do usuário |  | usuário da id que executou a última solicitação de upload do AEM para o AEM Mobile |

## Propriedades dos metadados principais {#core-metadata-properties}

| Nome de propriedade | Tipo | Padrões ou valores esperados |
|--- |--- |--- |
| dps-title | String |  |
| dps-shortTitle | String |  |
| dps-abstract | String |  |
| dps-shortAbstract | String |  |
| dps-department | String |  |
| dps-category | String |  |
| dps-keywords | Cadeia de caracteres[] |  |
| dps-internalKeywords | Cadeia de caracteres[] |  |
| dps-importance | Cadeia de caracteres[] | Importância de {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Artigos {#articles}

| **Nome da Propriedade** | **Tipo** | **Valores Padrões ou Esperados** |
|---|---|---|
| dps-author | String |  |
| dps-authorURL | String |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | String | ProtectedAccess de {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | String |  |
| dps-articleText | String |  |
| dps-url | String |  |

### Banners {#banners}

| **Nome da Propriedade** | **Tipo** | **Valores Padrões ou Esperados** |
|---|---|---|
| dps-tapAction |  | TapAction de {webLink} |
| dps-tapActionUrl |  |  |

### Coleções {#collections}

| Nome de propriedade | Tipo | Padrões ou valores esperados |
|--- |--- |--- |
| dps-productId | String |  |
| dps-readingPosition | String | de {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | String | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | String |  |

## Nós de conteúdo {#content-nodes}

### Nós comuns {#common-nodes}

| Nome do nó | Tipo | Padrões ou valores esperados | Descrição |
|--- |--- |--- |--- |
| imagem | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Entidades {#entities}

#### Artigos {#articles-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Banners {#banners-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|---|---|---|---|
| ND |  |  |  |

#### Coleções {#collections-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
