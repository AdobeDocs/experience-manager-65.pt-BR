---
title: Arquitetura de conteúdo
seo-title: Content Architecture
description: Dicas para arquitetar seu conteúdo (dica - tudo é conteúdo)
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Arquitetura de conteúdo{#content-architecture}

## Siga o modelo de David {#follow-david-s-model}

O Modelo de David foi escrito por David Nuescheler anos atrás, mas as ideias são verdadeiras hoje. Os principais princípios do Modelo de David são os seguintes:

* Os dados vêm primeiro, estruturam-se depois. Talvez.
* Direcione a hierarquia de conteúdo, não deixe que isso aconteça.
* Os espaços de trabalho são para `clone()`, `merge()`e `update()`.
* Cuidado com irmãos de mesmo nome.
* As referências são consideradas prejudiciais.
* Os arquivos são arquivos.
* As IDs são más.

O modelo de David pode ser encontrado no wiki do Jackrabbit em [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tudo é conteúdo {#everything-is-content}

Tudo deve ser armazenado no repositório em vez de depender de fontes de dados de terceiros separadas, como bancos de dados. Isso se aplica ao conteúdo criado, dados binários como imagens, código, configurações etc. Isso nos permite usar um conjunto de APIs para gerenciar todo o conteúdo e gerenciar a promoção desse conteúdo por meio da replicação. Também obtemos uma única fonte de backup, registro etc.

### Usar o princípio de design &quot;modelo de conteúdo primeiro&quot; {#use-the-content-model-first-design-principle}

Ao criar um novo recurso, sempre comece criando a estrutura de conteúdo JCR primeiro e, em seguida, procure ler e gravar seu conteúdo usando os servlets Sling padrão. Isso permitirá garantir que sua implementação funcione bem com mecanismos de controle de acesso prontos para uso e evita gerar servlets desnecessários no estilo CRUD.

### Seja RESTful {#be-restful}

Os servlets devem ser definidos com base em resourceTypes em vez de caminhos. Isso possibilita usar os controles de acesso do JCR, seguir os princípios do REST e usar o resolvedor de recursos e de recursos que são fornecidos a nós na solicitação. Isso também permite alterar os scripts que renderizam URLs no lado do servidor sem precisar alterar quaisquer URLs do lado do cliente, enquanto oculta os detalhes de implementação do lado do servidor do cliente para obter mais segurança.

### Evite definir novos tipos de nó {#avoid-defining-new-node-types}

Os tipos de nó funcionam em um nível baixo na camada de infraestrutura e a maioria dos requisitos pode ser atendida usando um sling:resourceType atribuído a um tipo de nó nt:unstructured, oak:Unstructured, sling:Folder ou cq:Page . Os tipos de nó são iguais ao esquema no repositório e a alteração dos tipos de nó pode ser muito cara na estrada.

### Aceitar as convenções de nomenclatura no JCR {#adhere-to-naming-conventions-in-the-jcr}

Aderir às convenções de nomenclatura adicionará consistência à sua base de código, diminuindo a taxa de incidência de defeitos e aumentando a velocidade dos desenvolvedores que trabalham no sistema. As seguintes convenções são usadas pelo Adobe no desenvolvimento de AEM:

* Nomes de nó

   * Todas as minúsculas
   * Separação de palavras usando hífens

* Nomes de propriedades

   * Camel case, começando com letra minúscula

* Componentes (JSP/HTML)

   * Todas as minúsculas
   * Separação de palavras usando hífens
