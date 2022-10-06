---
title: Propriedades e nós do conteúdo
seo-title: Content Properties and Nodes
description: Siga esta página para saber mais sobre propriedades e nós de conteúdo.
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 21%

---

# Propriedades e nós do conteúdo {#content-properties-and-nodes}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Artigos, banners e coleções são representados como cq:Pages em AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer cq:Page, além de várias outras mostradas abaixo que representam os metadados do Adobe Experience Manager (AEM) Mobile On-Demand Services e as propriedades de suporte da integração.

As tabelas a seguir descrevem as propriedades e os nós do conteúdo.

## Propriedades comuns da integração {#common-integration-properties}

| **Nome da Propriedade** | **Tipo** | **Padrões ou valores esperados** | **Descrição** |
|---|---|---|---|
| dps-id | Sequência de caracteres |  | atribuído pelo AEM Mobile e armazenado pelo AEM uma vez carregado no AEM Mobile ou importado do AEM Mobile |
| dps-resourceType | Sequência de caracteres | dps:Article | dps:Banner | dps:Collection | propriedade de tipo de entidade |
| dps-version | Sequência de caracteres |  | versão da entidade do AEM Mobile (também contida no aemm-id completo) |
| dps-lastSynced | Data |  | data da última sincronização/importação do AEM Mobile para o AEM |
| dps-lastUploaded | Data |  | data do último upload do AEM para o AEM Mobile |
| dps-lastUploadedBy | String:userid |  | usuário de id que executou a última solicitação de upload do AEM para o AEM Mobile |

## Propriedades dos metadados principais {#core-metadata-properties}

| Nome da Propriedade | Tipo | Padrões ou valores esperados |
|--- |--- |--- |
| dps-title | Sequência de caracteres |  |
| dps-shortTitle | Sequência de caracteres |  |
| dps-abstract | Sequência de caracteres |  |
| dps-shortAbstract | Sequência de caracteres |  |
| dps-departamental | Sequência de caracteres |  |
| dps-category | Sequência de caracteres |  |
| dps-keywords | Sequência de caracteres[] |  |
| dps-internalKeywords | Sequência de caracteres[] |  |
| dps-importance | Sequência de caracteres[] | Importância de {&quot;baixo&quot;, &quot;normal&quot;, &quot;alto&quot;} |

### Artigos {#articles}

| **Nome da Propriedade** | **Tipo** | **Padrões ou valores esperados** |
|---|---|---|
| dps-author | Sequência de caracteres |  |
| dps-authorURL | Sequência de caracteres |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | Sequência de caracteres | ProtectedAccess de {&quot;protegido&quot;, &quot;medido&quot;, &quot;livre&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Sequência de caracteres |  |
| dps-articleText | Sequência de caracteres |  |
| dps-url | Sequência de caracteres |  |

### Banners {#banners}

| **Nome da Propriedade** | **Tipo** | **Padrões ou valores esperados** |
|---|---|---|
| dps-tapAction |  | ToqueAction de {webLink} |
| dps-tapActionUrl |  |  |

### Coleções {#collections}

| Nome da Propriedade | Tipo | Padrões ou valores esperados |
|--- |--- |--- |
| dps-productId | Sequência de caracteres |  |
| dps-readingPosition | Sequência de caracteres | de {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Sequência de caracteres | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Sequência de caracteres |  |

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
| imagem de fundo | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
