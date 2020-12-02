---
title: Arquitetura de conteúdo
seo-title: Arquitetura de conteúdo
description: 'Dicas para arquitetar seu conteúdo (dica: tudo é conteúdo)'
seo-description: Dicas para arquitetar seu conteúdo no Adobe Experience Manager (AEM). (dica - tudo é conteúdo)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Arquitetura de conteúdo{#content-architecture}

## Siga o modelo de David {#follow-david-s-model}

O Modelo de David foi escrito por David Nuescheler anos atrás, mas as ideias são verdadeiras hoje. Os principais princípios do modelo de David são os seguintes:

* Os dados vêm primeiro, depois a estrutura. Talvez.
* Direcione a hierarquia de conteúdo, não deixe que isso aconteça.
* Os espaços de trabalho são para `clone()`, `merge()` e `update()`.
* Cuidado com o mesmo nome de irmãos.
* As referências são consideradas prejudiciais.
* Arquivos são arquivos.
* As IDs são más.

O modelo de David pode ser encontrado no wiki do Jackrabbit em [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tudo é conteúdo {#everything-is-content}

Tudo deve ser armazenado no repositório em vez de depender de fontes de dados de terceiros separadas, como bancos de dados. Isso se aplica ao conteúdo criado, aos dados binários, como imagens, código, configurações etc. Isso nos permite usar um conjunto de APIs para gerenciar todo o conteúdo e gerenciar a promoção desse conteúdo por meio da replicação. Também ganhamos uma única fonte de backup, registro, etc.

### Use o princípio de design &quot;content model first&quot; {#use-the-content-model-first-design-principle}

Ao criar um novo recurso, sempre faça start ao projetar a estrutura de conteúdo JCR primeiro e, em seguida, procure ler e gravar seu conteúdo usando os servlets Sling padrão. Isso permitirá garantir que sua implementação funcione bem com mecanismos de controle de acesso prontos para uso e permitirá evitar a geração de servlets desnecessários ao estilo CRUD.

### Seja RESTful {#be-restful}

Servlets devem ser definidos com base em resourceTypes em vez de caminhos. Isso possibilita usar controles de acesso JCR, seguir os princípios REST e usar o resolvedor de recursos e recursos que nos são fornecidos na solicitação. Isso também permite alterar os scripts que renderizam URLs no lado do servidor sem precisar alterar quaisquer URLs do lado do cliente, enquanto oculta detalhes de implementação do lado do servidor do cliente para maior segurança.

### Evite definir novos tipos de nó {#avoid-defining-new-node-types}

Os tipos de nó funcionam em um nível baixo na camada de infraestrutura e a maioria dos requisitos pode ser atendida usando um sling:resourceType atribuído a um tipo de nó nt:unstructed, oak:Unstructed, sling:Folder ou cq:Page. Os tipos de nó correspondem ao schema no repositório e a alteração dos tipos de nó pode ser muito cara na estrada.

### Aceitar convenções de nomenclatura no JCR {#adhere-to-naming-conventions-in-the-jcr}

O cumprimento das convenções de nomenclatura adicionará consistência à sua base de códigos, diminuindo a taxa de incidência de defeitos e aumentando a velocidade de trabalho dos desenvolvedores no sistema. As seguintes convenções são usadas pela Adobe no desenvolvimento de AEM:

* Nomes de nó

   * Todas as minúsculas
   * Separação de palavras usando hífens

* Nomes de propriedade

   * Caso de Camel, começando com uma letra minúscula

* Componentes (JSP/HTML)

   * Todas as minúsculas
   * Separação de palavras usando hífens

