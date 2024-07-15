---
title: Arquitetura de conteúdo
description: Dicas para projetar seu conteúdo (dica - tudo é conteúdo)
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Arquitetura de conteúdo{#content-architecture}

## Siga o modelo de David {#follow-david-s-model}

O modelo de David foi escrito por David Nuescheler anos atrás, mas as ideias se mantêm verdadeiras hoje. Os principais princípios do Modelo de David são os seguintes:

* Os dados vêm primeiro, estruturados depois. Talvez.
* Direcione a hierarquia de conteúdo, não deixe que isso aconteça.
* Os espaços de trabalho são para `clone()`, `merge()` e `update()`.
* Cuidado com os irmãos de mesmo nome.
* As referências são consideradas prejudiciais.
* Arquivos são arquivos.
* As identidades são más.

O modelo de David pode ser encontrado no wiki do Jackrabbit em [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tudo é conteúdo {#everything-is-content}

Tudo deve ser armazenado no repositório, em vez de depender de fontes de dados separadas de terceiros, como bancos de dados. Isso se aplica ao conteúdo criado, aos dados binários como imagens, código e configurações. Isso nos permite usar um conjunto de APIs para gerenciar todo o conteúdo e gerenciar a promoção desse conteúdo por meio de replicação. Você também obtém uma única fonte de backup, registro e assim por diante.

### Usar o princípio de design de &quot;modelo de conteúdo primeiro&quot; {#use-the-content-model-first-design-principle}

Ao criar um novo recurso, sempre comece criando a estrutura de conteúdo JCR primeiro e, em seguida, examine a leitura e a gravação de conteúdo usando os servlets Sling padrão. Isso permite garantir que sua implementação funcione bem com mecanismos de controle de acesso prontos para uso e evitar a geração de servlets de estilo CRUD desnecessários.

### Ser RESTful {#be-restful}

Os servlets devem ser definidos com base em resourceTypes em vez de caminhos. Isso permite usar controles de acesso JCR, seguir princípios REST e usar o resolvedor de recursos e recursos fornecidos a nós na solicitação. Isso também permite alterar os scripts que renderizam URLs no lado do servidor sem precisar alterar URLs do lado do cliente, enquanto oculta os detalhes de implementação do lado do servidor do cliente para maior segurança.

### Evitar a definição de novos tipos de nó {#avoid-defining-new-node-types}

Os tipos de nó funcionam em um nível baixo na camada de infraestrutura e a maioria dos requisitos pode ser atendida usando um sling:resourceType atribuído a um tipo de nó nt:unstructured, oak:Unstructured, sling:Folder ou cq:Page. Os tipos de nó equivalem ao esquema no repositório e alterar os tipos de nó pode custar caro.

### Seguir as convenções de nomenclatura no JCR {#adhere-to-naming-conventions-in-the-jcr}

Seguir convenções de nomenclatura adiciona consistência à base de código, reduzindo a taxa de incidência de defeitos e aumentando a velocidade dos desenvolvedores que trabalham no sistema. As seguintes convenções são usadas pelo Adobe no desenvolvimento do AEM:

* Nomes de nós

   * Todas em minúsculas
   * Separação de palavras usando hifens

* Nomes de propriedades

   * Camel case, começando com uma letra minúscula

* Componentes (JSP/HTML)

   * Todas em minúsculas
   * Separação de palavras usando hifens
