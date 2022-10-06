---
title: Visão geral do provedor de recursos de armazenamento
seo-title: Storage Resource Provider Overview
description: Armazenamento comum para comunidades
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Visão geral do provedor de recursos de armazenamento {#storage-resource-provider-overview}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo da comunidade, comumente chamado de conteúdo gerado pelo usuário (UGC), é armazenado em uma única loja comum fornecida por um [provedor de recursos de armazenamento](working-with-srp.md) (SRP).

Há várias opções de SRP, todas acessando o UGC por meio de uma nova interface do AEM Communities, a [API do SocialResourceProvider](srp-and-ugc.md) (API SRP), que inclui todas as operações de criação, leitura, atualização e exclusão (CRUD).

Todos os componentes do SCF são implementados usando a API do SRP, permitindo que o código seja desenvolvido sem o conhecimento de [topologia subjacente](topologies.md) ou local do UGC.

***A API SocialResourceProvider está disponível somente para clientes licenciados do AEM Communities.***

>[!NOTE]
>
>**Componentes personalizados**: Para clientes licenciados do AEM Communities, a API SRP está disponível para desenvolvedores de componentes personalizados com o objetivo de acessar o UGC sem considerar a topologia subjacente. Consulte [Princípios básicos de SRP e UGC](srp-and-ugc.md).

Consulte também:

* [Princípios básicos de SRP e UGC](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais.

## Sobre o Repositório {#about-the-repository}

Para entender o SRP, é útil entender a função do repositório de AEM (OAK) em um site da comunidade AEM.

**Java Content Repository (JCR)**
Esse padrão define um modelo de dados e uma interface de programação de aplicativos ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) para repositórios de conteúdo. Ele combina características de sistemas de arquivos convencionais com as de bancos de dados relacionais e adiciona vários recursos adicionais que os aplicativos de conteúdo geralmente precisam.

Uma implementação do JCR é o repositório AEM, OAK.

**Apache Jackrabbit Oak (OAK)**
[OAK](../../help/sites-deploying/platform.md) O é uma implementação do JCR 2.0 que é um sistema de armazenamento de dados criado especificamente para aplicativos centrados em conteúdo. É um tipo de banco de dados hierárquico projetado para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo. A interface do usuário para acessar conteúdo é [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR e OAK normalmente são usados para se referir ao repositório AEM.

Depois de desenvolver o conteúdo do site no ambiente de autor privado, ele deve ser copiado para o ambiente de publicação público. Isso geralmente é feito por meio de uma operação chamada *[replicação](deploy-communities.md#replication-agents-on-author)*. Isso acontece sob controle do autor/desenvolvedor/administrador.

Para o UGC, o conteúdo é inserido por visitantes do site registrados (membros da comunidade) no ambiente de publicação público. Isso acontece aleatoriamente.

Para fins de gerenciamento e relatórios, é útil ter acesso ao UGC a partir do ambiente de criação privado. Com o SRP, o acesso ao UGC do autor é mais consistente e eficaz, pois a replicação reversa da publicação para o autor não é necessária.

## Sobre SRP {#about-srp}

Quando o UGC é salvo no armazenamento compartilhado, há uma única instância do conteúdo do membro que pode, na maioria das implantações, ser acessada dos ambientes do autor e de publicação. Independentemente da escolha de SRP (MSRP, ASRP, JSRP), todas devem ser acessadas programaticamente com a API do SRP.

>[!NOTE]
>
>Consulte [Princípios básicos de SRP e UGC](srp-and-ugc.md) para código de amostra e detalhes adicionais.
>
>Consulte [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) para práticas recomendadas ao codificar.

### ASRP {#asrp}

No caso de ASRP, o UGC não é armazenado no JCR, ele é armazenado em um serviço de nuvem hospedado e gerenciado pelo Adobe. O UGC armazenado no ASRP não pode ser visualizado com o CRXDE Lite nem acessado usando a API do JCR.

Consulte [ASRP - Provedor de Recursos de Armazenamento Adobe](asrp.md).

Não é possível para os desenvolvedores acessar o UGC diretamente.

O ASRP usa a nuvem Adobe para consultas.

### MSRP {#msrp}

No caso de MSRP, o UGC não é armazenado no JCR, ele é armazenado no MongoDB. O UGC armazenado no MSRP não pode ser visualizado com o CRXDE Lite nem acessado usando a API do JCR.

Consulte [MSRP - Provedor de recursos de armazenamento MongoDB](msrp.md).

Embora o MSRP seja comparável ao ASRP, como todas as instâncias de servidor AEM estão acessando o mesmo UGC, é possível usar ferramentas comuns para acessar diretamente o UGC armazenado no MongoDB.

O MSRP usa o Solr para consultas.

### JSRP {#jsrp}

O JSRP é o provedor padrão para acessar todos os UGC em uma única instância de AEM. Ele fornece a capacidade de experimentar rapidamente o AEM Communities 6.1 sem a necessidade de configurar o MSRP ou o ASRP.

Consulte [JSRP - Provedor de recursos de armazenamento JCR](jsrp.md).

No caso do JSRP, embora o UGC seja armazenado no JCR e acessível por meio da API do CRXDE Lite e do JCR, é altamente recomendável que a API do JCR nunca seja usada para fazer isso, caso contrário, alterações futuras podem afetar o código personalizado.

Além disso, o repositório dos ambientes de criação e publicação não é compartilhado. Embora um cluster de instâncias de publicação resulte em um repositório de publicação compartilhado, o UGC inserido na publicação não estará visível no autor, portanto, não há capacidade de gerenciar o UGC do autor. O UGC só é persistente no repositório AEM (JCR) da instância em que foi inserido.

O JSRP usa os índices Oak para consultas.

## Sobre nós de sombra no JCR {#about-shadow-nodes-in-jcr}

Os nós de sombra, que imitam o caminho para o UGC, existem no repositório local para servir dois propósitos:

1. [Controle de acesso (ACLs)](#for-access-control-acls)
1. [Recursos não existentes (NERs)](#for-non-existing-resources-ners)

Independentemente da implementação do SRP, o UGC real *não será *visível no mesmo local que o nó de sombra.

### Para Controle de Acesso (ACLs) {#for-access-control-acls}

Algumas implementações de SRP, como ASRP e MSRP, armazenam o conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções de SRP executam a mesma verificação do local de sombra antes de todas as operações de CRUD.

A verificação da ACL usa um método de utilitário que retorna um caminho adequado para verificar as permissões aplicadas ao UGC do recurso.

Consulte [Princípios básicos de SRP e UGC](srp-and-ugc.md) para código de amostra.

### Para recursos não existentes (NERs) {#for-non-existing-resources-ners}

Alguns componentes das Comunidades podem ser incluídos em um script e, portanto, exigem um nó endereçável do Sling para suportar recursos das Comunidades. [Componentes incluídos](scf.md#add-or-include-a-communities-component) são designados por recursos não existentes (NERs).

Os nós de sombra fornecem um local endereçável do Sling no repositório.

>[!CAUTION]
>
>Como o nó de sombra tem vários usos, a presença de um nó de sombra *not* Isso significa que o componente é um NER.

### Local de armazenamento {#storage-location}

A seguir, um exemplo de um nó de sombra, usando o [Componente Comentários](http://localhost:4502/content/community-components/en/comments.html) no [Guia de componentes da comunidade](components-guide.md):

* O componente existe no repositório local em:

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* O nó de sombra correspondente existe no repositório local em:

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Nenhum UGC será encontrado sob o nó de sombra.

O comportamento padrão é configurar nós de sombra em uma instância de publicação sempre que a subárvore relevante for referenciada para leitura ou gravação.

Por exemplo, suponha que a implantação seja [MSRP](msrp.md) com um farm de publicação TarMK.

Quando uma [membro](users.md) posta UGC no pub1 (armazenado no MongoDB), os nós de sombra são criados no JCR no pub1.

Na primeira vez que o UGC é lido no pub2, se nada for configurado, o comportamento padrão é criar os nós de sombra.

Se desejar outro comportamento diferente do padrão, ele deve ser configurado na instância de autor e encaminhado para todas as instâncias de publicação, que normalmente é um processo manual.
