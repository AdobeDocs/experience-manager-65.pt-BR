---
title: Search Essentials
description: Saiba mais sobre o recurso de pesquisa que é um recurso essencial do AEM Communities. As comunidades também fornecem a API de pesquisa para conteúdo gerado pelo usuário.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 3%

---

# Search Essentials {#search-essentials}

## Visão geral {#overview}

O recurso de pesquisa é um recurso essencial das comunidades Adobe Experience Manager (AEM). Além dos recursos de [pesquisa de plataforma AEM](../../help/sites-deploying/queries-and-indexing.md), a AEM Communities fornece a [API de pesquisa UGC](#ugc-search-api) para pesquisar conteúdo gerado pelo usuário (UGC). O UGC tem propriedades exclusivas, pois é inserido e armazenado separadamente de outro conteúdo AEM e dados do usuário.

Para as Comunidades, as duas coisas geralmente pesquisadas são:

* Conteúdo publicado por membros da comunidade

   * Ele usa a API de pesquisa UGC do AEM Communities.

* Usuários e grupos de usuários (dados do usuário)

   * Ele usa os recursos de pesquisa da plataforma AEM.

Esta seção da documentação é de interesse para desenvolvedores que estão criando componentes personalizados que criam ou gerenciam o UGC.

## Nós de segurança e sombra {#security-and-shadow-nodes}

Para um componente personalizado, é necessário usar os métodos [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). Os métodos de utilitário que criam e pesquisam por UGC estabelecem os [nós sombra](srp.md#about-shadow-nodes-in-jcr) necessários e garantem que o membro tenha as permissões corretas para a solicitação.

O que não é gerenciado pelos utilitários SRP são propriedades relacionadas à moderação.

Consulte [SRP and UGC Essentials](srp-and-ugc.md) para obter informações sobre os métodos de utilitário usados para acessar nós de sombra UGC e ACL.

## API de pesquisa UGC {#ugc-search-api}

O [repositório comum de UGC](working-with-srp.md) é fornecido por um dos vários provedores de recursos de armazenamento (SRPs), cada um possivelmente com um idioma de consulta nativo diferente. Portanto, independentemente do SRP escolhido, o código personalizado deve usar métodos do [pacote de API de UGC](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) que invoca o idioma de consulta apropriado para o SRP escolhido.

### Pesquisas ASRP {#asrp-searches}

Para [ASRP](asrp.md), o UGC está armazenado na nuvem Adobe. Embora o UGC não esteja visível no CRX, a [moderação](moderate-ugc.md) está disponível nos ambientes do autor e do Publish. O uso da [API de pesquisa UGC](#ugc-search-api) funciona para ASRP da mesma forma que para outros SRPs.

No momento, não existem ferramentas para gerenciar pesquisas ASRP.

Ao criar propriedades personalizadas pesquisáveis, é necessário atender aos [requisitos de nomenclatura](#naming-of-custom-properties).

### Pesquisas MSRP {#msrp-searches}

Para [MSRP](msrp.md), o UGC é armazenado no MongoDB configurado para usar Solr para pesquisa. O UGC não está visível no CRX, mas a [moderação](moderate-ugc.md) está disponível nos ambientes do autor e do Publish.

Quanto ao MSRP e ao Solr:

* O Solr incorporado para a plataforma AEM não é usado para MSRP.
* Se estiver usando um Solr remoto para a plataforma AEM, ele poderá ser compartilhado com o MSRP, mas eles deverão usar coleções diferentes.
* O Solr pode ser configurado para pesquisa padrão ou para pesquisa multilíngue (MLS).
* Para obter detalhes sobre a configuração, consulte [Configuração Solr](msrp.md#solr-configuration) para MSRP.

Os recursos de pesquisa personalizados devem usar a [API de pesquisa UGC](#ugc-search-api).

Ao criar propriedades personalizadas pesquisáveis, é necessário atender aos [requisitos de nomenclatura](#naming-of-custom-properties).

### Pesquisas JSRP {#jsrp-searches}

Para [JSRP](jsrp.md), o UGC está armazenado no [Oak](../../help/sites-deploying/platform.md) e é visível somente no repositório do Autor de AEM ou da instância do Publish em que foi inserido.

Como o UGC é normalmente inserido no ambiente Publish, para sistemas de produção com vários editores, é necessário configurar um [cluster de publicação](topologies.md), não um farm de publicação, para que o conteúdo inserido fique visível de todos os editores.

Para JSRP, o UGC inserido no ambiente do Publish nunca é visível no ambiente do autor. Portanto, todas as tarefas de [moderação](moderate-ugc.md) ocorrem no ambiente do Publish.

Os recursos de pesquisa personalizados devem usar a [API de pesquisa UGC](#ugc-search-api).

#### Indexação do Oak {#oak-indexing}

Embora os índices Oak não sejam criados automaticamente para a pesquisa na plataforma AEM, a partir do AEM 6.2, eles foram adicionados para o AEM Communities para melhorar o desempenho e dar suporte para paginação ao apresentar resultados de pesquisa UGC.

Se as propriedades personalizadas estiverem em uso e as pesquisas estiverem lentas, índices adicionais deverão ser criados para que as propriedades personalizadas tenham melhor desempenho. Para manter a portabilidade, siga os [requisitos de nomenclatura](#naming-of-custom-properties) ao criar propriedades personalizadas que possam ser pesquisadas.

Para modificar índices existentes ou criar índices personalizados, consulte [Consultas e Indexação do Oak](../../help/sites-deploying/queries-and-indexing.md).

O [Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) está disponível no ACS AEM Commons. Ele fornece:

* Uma exibição de índices existentes.
* A capacidade de iniciar a reindexação.

Para exibir os índices Oak existentes em [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), o local é:

* `/oak:index/socialLucene`

![lucene_social](assets/social-lucene.png)

## Propriedades de Pesquisa Indexada {#indexed-search-properties}

### Propriedades de pesquisa padrão {#default-search-properties}

Estas são algumas das propriedades pesquisáveis usadas para vários recursos do Communities:

| **Propriedade** | **Tipo de dados** |
|---|---|
| isFlagged | *Booleano* |
| isSpam | *Booleano* |
| ler | *Booleano* |
| influência | *Booleano* |
| anexos | *Booleano* |
| sentimento | *Longo* |
| sinalizado | *Booleano* |
| adicionado | *Data* |
| modifiedDate | *Data* |
| estado | *String* |
| userIdentifier | *String* |
| respostas | *Longo* |
| jcr:title | *String* |
| jcr:description | *String* |
| sling:resourceType | *String* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Data* |
| publishJobId | *String* |
| respondido | *Booleano* |
| escolhido respondido | *Booleano* |
| tag | *String* |
| cq:Tag | *String* |
| author_display_name | *String* |
| location_t | *String* |
| parentPath | *String* |
| parentTitle | *String* |

### Nomeação de propriedades personalizadas {#naming-of-custom-properties}

Ao adicionar propriedades personalizadas, para que essas propriedades fiquem visíveis para classificações e pesquisas criadas com a [API de pesquisa de UGC](#ugc-search-api), é *necessário* adicionar um sufixo ao nome da propriedade.

O sufixo é para linguagens de consulta que usam um schema:

* Ela identifica a propriedade como pesquisável.
* Identifica o tipo de dados.

Solr é um exemplo de uma linguagem de consulta que usa um schema.

| **Sufixo** | **Tipo de dados** |
|---|---|
| _b | *Booleano* |
| _dt | *Calendário* |
| _d | *Duplo* |
| _tl | *Longo* |
| _s | *String* |
| _t | *Texto* |

**Notas:**

* *Text* é uma cadeia de caracteres tokenizada, *String* não é. Use *Texto* para pesquisas difusas (mais ou menos como esta).

* Para tipos com vários valores, adicione &#39;s&#39; ao sufixo, por exemplo:

   * `viewDate_dt`: propriedade de data única
   * `viewDates_dts`: lista da propriedade de datas

## Filtros {#filters}

Os componentes, que incluem o [sistema de comentários](essentials-comments.md), oferecem suporte ao parâmetro de filtro além de seus pontos de extremidade.

A sintaxe de filtro para as lógicas AND e OR é expressa da seguinte maneira (mostrada antes de ser codificada por URL):

* Para especificar OU usar um parâmetro de filtro com valores separados por vírgulas:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Para especificar E usar vários parâmetros de filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

A implementação padrão do [componente de Pesquisa](search.md) usa essa sintaxe como pode ser vista na URL que abre a página Resultados da Pesquisa no [guia Componentes da Comunidade](components-guide.md). Para experimentar, navegue até [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Os operadores de filtro são:

| EQ | igual |
|---|---|
| NE | não é igual |
| LT | menor que |
| LTE | menor que ou igual a |
| GE | maior que |
| GTE | maior que ou igual a |
| LIKE | correspondência difusa |

É importante que o URL faça referência ao componente Comunidades (recurso) e não à página em que o componente é colocado:

* Correto: componente do fórum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorreto: página do fórum
   * `/content/community-components/en/forum.social.json`

## Ferramentas SRP {#srp-tools}

Há um projeto GitHub da Adobe Experience Cloud que contém:

[Ferramentas SRP do AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Este repositório contém ferramentas para gerenciar dados no SRP.

Atualmente, há um servlet que pode excluir todo o UGC de qualquer SRP.

Por exemplo, para excluir todo o UGC no ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Resolução de problemas {#troubleshooting}

### Consulta Solr {#solr-query}

Para ajudar a solucionar problemas com uma consulta Solr, ative o log DEBUG para

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

A consulta Solr real é exibida com o URL codificado no log de depuração:

A consulta a solr é: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

O valor do parâmetro `q` é a consulta. Depois que a codificação do URL é decodificada, a consulta pode ser passada para a ferramenta Solr Admin Query para depuração adicional.

## Recursos relacionados {#related-resources}

* [Armazenamento do Conteúdo da Comunidade](working-with-srp.md) - Discute as opções de SRP disponíveis para um armazenamento comum de UGC.
* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Métodos de utilitário para SRP que substituem SocialUtils.
* [Componentes de Resultados de Pesquisa e Pesquisa](search.md) - Adicionando o recurso de pesquisa UGC a um modelo.
