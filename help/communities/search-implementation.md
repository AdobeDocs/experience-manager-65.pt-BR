---
title: Fundamentos da pesquisa
seo-title: Search Essentials
description: Pesquisar em comunidades
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 5%

---

# Fundamentos da pesquisa {#search-essentials}

## Visão geral {#overview}

O recurso de pesquisa é um recurso essencial do AEM Communities. Além do [Pesquisa na plataforma AEM](../../help/sites-deploying/queries-and-indexing.md) , a AEM Communities fornece a variável [API de pesquisa UGC](#ugc-search-api) para fins de pesquisa de conteúdo gerado pelo usuário (UGC). O UGC tem propriedades exclusivas, pois é inserido e armazenado separadamente de outro conteúdo AEM e dados do usuário.

Para Comunidades, as duas coisas geralmente pesquisadas são:

* Conteúdo publicado por membros da comunidade

   * Usa a API de pesquisa UGC do AEM Communities.

* Usuários e grupos de usuários (dados do usuário)

   * Usa os recursos de pesquisa da plataforma AEM.

Esta seção da documentação é de interesse para desenvolvedores que estão criando componentes personalizados que criam ou gerenciam o UGC.

## Nós de Segurança e Sombra {#security-and-shadow-nodes}

Para um componente personalizado, é necessário usar o [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) métodos. Os métodos de utilitário que criam e pesquisam o UGC estabelecerão o [nós sombra](srp.md#about-shadow-nodes-in-jcr) e verifique se o membro tem as permissões corretas para a solicitação.

O que não é gerenciado por meio dos utilitários SRP são propriedades relacionadas à moderação.

Consulte [Princípios básicos de SRP e UGC](srp-and-ugc.md) para obter informações sobre métodos de utilitários usados para acessar nós de sombra UGC e ACL.

## API de pesquisa UGC {#ugc-search-api}

O [repositório comum UGC](working-with-srp.md) é fornecido por um dos vários provedores de recursos de armazenamento (SRPs), cada um com possivelmente uma linguagem de consulta nativa diferente. Portanto, independentemente do SRP escolhido, o código personalizado deve usar métodos do [Pacote da API UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) que chamará a linguagem de consulta apropriada para o SRP escolhido.

### Pesquisas ASRP {#asrp-searches}

Para [ASRP](asrp.md), o UGC é armazenado na nuvem do Adobe. Embora o UGC não esteja visível no CRX, [moderação](moderate-ugc.md) O está disponível nos ambientes do autor e de publicação. O uso da variável [API de pesquisa UGC](#ugc-search-api) funciona para ASRP da mesma forma que para outros SRPs.

Atualmente, não existem ferramentas para gerenciar pesquisas ASRP.

Ao criar propriedades personalizadas que podem ser pesquisadas, é necessário seguir as [requisitos de nomenclatura](#naming-of-custom-properties).

### Pesquisas do MSRP {#msrp-searches}

Para [MSRP](msrp.md), o UGC é armazenado no MongoDB configurado para usar o Solr para pesquisa. O UGC não estará visível no CRX, mas [moderação](moderate-ugc.md) O está disponível nos ambientes do autor e de publicação.

Relativamente ao MSRP e ao Solr:

* A Solr incorporada para a plataforma de AEM não é usada para MSRP.
* Se estiver usando um Solr remoto para a plataforma de AEM, ele poderá ser compartilhado com o MSRP, mas deverá usar coleções diferentes.
* O Solr pode ser configurado para pesquisa padrão ou para pesquisa multilíngue (MLS).
* Para obter detalhes de configuração, consulte [Configuração Solr](msrp.md#solr-configuration) para MSRP.

Os recursos de pesquisa personalizados devem usar o [API de pesquisa UGC](#ugc-search-api).

Ao criar propriedades personalizadas que podem ser pesquisadas, é necessário seguir as [requisitos de nomenclatura](#naming-of-custom-properties).

### Pesquisas JSRP {#jsrp-searches}

Para [JSRP](jsrp.md), o UGC é armazenado em [Oak](../../help/sites-deploying/platform.md) e é visível somente no repositório do autor ou da instância de publicação do AEM em que foi inserido.

Como o UGC normalmente é inserido no ambiente de publicação, para sistemas de produção de vários editores, é necessário configurar um [cluster de publicação](topologies.md), não um farm de publicação, para que o conteúdo inserido fique visível de todos os editores.

Para JSRP, o UGC inserido no ambiente de publicação nunca estará visível no ambiente do autor. Assim todos [moderação](moderate-ugc.md) As tarefas ocorrem no ambiente de publicação.

Os recursos de pesquisa personalizados devem usar o [API de pesquisa UGC](#ugc-search-api).

#### Indexação do Oak {#oak-indexing}

Embora os índices Oak não sejam criados automaticamente para a pesquisa da plataforma AEM, a partir AEM 6.2, eles foram adicionados ao AEM Communities para melhorar o desempenho e fornecer suporte para paginação ao apresentar resultados de pesquisa UGC.

Se as propriedades personalizadas estiverem em uso e as pesquisas estiverem lentas, será necessário criar índices adicionais para que as propriedades personalizadas sejam mais eficazes. Para manter a portabilidade, siga as [requisitos de nomenclatura](#naming-of-custom-properties) ao criar propriedades personalizadas que podem ser pesquisadas.

Para modificar índices existentes ou criar índices personalizados, consulte [Consultas e indexação do Oak](../../help/sites-deploying/queries-and-indexing.md).

O [Gerenciador de Índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) está disponível em ACS AEM Commons. Ele fornece:

* Uma exibição de índices existentes.
* A capacidade de iniciar a reindexação.

Para exibir os índices existentes do Oak em [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), o local é:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Propriedades de Pesquisa Indexada {#indexed-search-properties}

### Propriedades de pesquisa padrão {#default-search-properties}

Veja a seguir algumas das propriedades pesquisáveis usadas para vários recursos das Comunidades:

| **Propriedade** | **Tipo de dados** |
|---|---|
| isFlagged | *Booleano* |
| isSpam | *Booleano* |
| leitura | *Booleano* |
| influência | *Booleano* |
| anexos | *Booleano* |
| sentimento | *Longo* |
| sinalizado | *Booleano* |
| adicionado | *Data* |
| modifiedDate | *Data* |
| estado | *Sequência de caracteres* |
| userIdentifier | *Sequência de caracteres* |
| respostas | *Longo* |
| jcr:title | *Sequência de caracteres* |
| jcr:description | *Sequência de caracteres* |
| sling:resourceType | *Sequência de caracteres* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Data* |
| publishJobId | *Sequência de caracteres* |
| respondido | *Booleano* |
| chosenanswers | *Booleano* |
| tag | *Sequência de caracteres* |
| cq:Tag | *Sequência de caracteres* |
| author_display_name | *Sequência de caracteres* |
| location_t | *Sequência de caracteres* |
| parentPath | *Sequência de caracteres* |
| parentTitle | *Sequência de caracteres* |

### Nomenclatura de propriedades personalizadas {#naming-of-custom-properties}

Ao adicionar propriedades personalizadas, para que essas propriedades fiquem visíveis, as classificações e pesquisas criadas com o [API de pesquisa UGC](#ugc-search-api), é *obrigatório* para adicionar um sufixo ao nome da propriedade.

O sufixo é para idiomas de consulta que usam um schema:

* Ela identifica a propriedade como pesquisável.
* Ela identifica o tipo de dados.

Solr é um exemplo de linguagem de consulta que usa um schema .

| **Sufixo** | **Tipo de dados** |
|---|---|
| _b | *Booleano* |
| _dt | *Calendário* |
| _d | *Duplo* |
| _tl | *Longo* |
| _s | *Sequência de caracteres* |
| _t | *Texto* |

**Notas:**

* *Texto* é uma string com tokens, *String* não é. Use *Texto* para pesquisas difusas (mais parecidas com esta).

* Para tipos de valores múltiplos, adicione &quot;s&quot; ao sufixo, por exemplo:

   * `viewDate_dt`: propriedade de data única
   * `viewDates_dts`: propriedade list of dates

## Filtros {#filters}

Componentes que incluem o [sistema de comentários](essentials-comments.md) suporta a adição do parâmetro de filtro aos endpoints.

A sintaxe do filtro para a lógica E e OU é expressa da seguinte maneira (mostrada antes de ser codificada no URL):

* Para especificar OU use um parâmetro de filtro com valores separados por vírgula:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Para especificar E usar vários parâmetros de filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

A implementação padrão do [Componente de pesquisa](search.md) O usa essa sintaxe como pode ser visto no URL que abre a página Resultados da pesquisa no [Guia de componentes da comunidade](components-guide.md). Para experimentar, procure por [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Os operadores de filtro são:

| EQ | igual |
|---|---|
| NE | não é igual |
| LT | menor que |
| LTE | menor que ou igual a |
| GE | maior que |
| GTE | maior que ou igual a |
| LIKE | correspondência difusa |

É importante que o URL faça referência ao componente Comunidades (recurso) e não à página na qual o componente é colocado:

* Correto: componente do fórum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorreto: página do fórum
   * `/content/community-components/en/forum.social.json`

## Ferramentas SRP {#srp-tools}

Há um projeto do Adobe Marketing Cloud GitHub que contém:

[Ferramentas SRP da AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Esse repositório contém ferramentas para gerenciar dados no SRP.

Atualmente, há um servlet que fornece a capacidade de excluir todo o UGC de qualquer SRP.

Por exemplo, para excluir todos os UGC no ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Resolução de problemas {#troubleshooting}

### Consulta Solr {#solr-query}

Para ajudar a solucionar problemas com uma consulta Solr, habilite o log DEBUG para

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

A consulta Solr real será exibida com o URL codificado no log de depuração:

A consulta para solr é: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

O valor da variável `q` é a consulta. Depois que a codificação do URL é decodificada, o query pode ser transmitido à ferramenta Solr Admin Query para depuração adicional.

## Recursos relacionados {#related-resources}

* [Armazenamento de conteúdo da comunidade](working-with-srp.md) - Discute as opções de SRP disponíveis para uma loja comum UGC.
* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Métodos de utilitário para SRP que substituem o SocialUtils.
* [Componentes de Pesquisa e Resultados de Pesquisa](search.md) - Adicionar recurso de pesquisa UGC a um modelo.
