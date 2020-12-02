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
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 20%

---


# Propriedades e nós do conteúdo {#content-properties-and-nodes}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Artigos, banners e coleções são representados como cq:Pages em AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer cq:Page, além de várias outras mostradas abaixo que representam os metadados dos serviços sob demanda do Adobe Experience Manager (AEM) Mobile e as propriedades de suporte da integração.

As tabelas a seguir descrevem as propriedades e os nós do conteúdo.

## Propriedades de integração comuns {#common-integration-properties}

| **Nome da Propriedade** | **Tipo** | **Valores padrão ou valores esperados** | **Descrição** |
|---|---|---|---|
| dps-id | Sequência de caracteres |  | atribuído pela AEM Mobile e armazenado por AEM uma vez carregado no AEM Mobile ou importado da AEM Mobile |
| dps-resourceType | Sequência de caracteres | dps:Article | dps:Banner | dps:Collection | propriedade de tipo de entidade |
| dps-version | Sequência de caracteres |  | versão da entidade AEM Mobile (também contida em aemm-id completo) |
| dps-lastSynced | Data |  | data da última sincronização/importação da AEM Mobile para AEM |
| dps-lastUploaded | Data |  | data do último upload do AEM para o AEM Mobile |
| dps-lastUploadedBy | String:userid |  | usuário de ID que executou a última solicitação de upload do AEM para a AEM Mobile |

## Propriedades de metadados principais {#core-metadata-properties}

| Nome da Propriedade | Tipo | Valores padrão ou valores esperados |
|--- |--- |--- |
| dps-title | Sequência de caracteres |  |
| dps-shortTitle | Sequência de caracteres |  |
| dps-abstract | Sequência de caracteres |  |
| dps-shortAbstract | Sequência de caracteres |  |
| departamento de dps | Sequência de caracteres |  |
| dps-categoria | Sequência de caracteres |  |
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
|--- |--- |--- |--- |
| imagem | jcr:PrimaryType=nt:sling <br> não estruturado:resourceType=base/components/image |  |  |

### Entidades {#entities}

#### Artigos {#articles-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| social-share-image |  | jcr:PrimaryType=nt:sling <br> não estruturado:resourceType=base/components/image |  |

#### Banners {#banners-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|---|---|---|---|
| ND |  |  |  |

#### Coleções {#collections-1}

| Nome do nó | Tipo | Padrões de valores esperados | Descrição |
|--- |--- |--- |--- |
| background-image | jcr:PrimaryType=nt:sling <br> não estruturado:resourceType=base/components/image |  |  |
