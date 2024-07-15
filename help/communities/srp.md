---
title: Visão geral do provedor de recursos de armazenamento
description: Saiba como o conteúdo da comunidade, conhecido como conteúdo gerado pelo usuário (UGC), é armazenado em um armazenamento simples e comum fornecido por um provedor de recursos de armazenamento (SRP).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Visão geral do provedor de recursos de armazenamento {#storage-resource-provider-overview}

## Introdução {#introduction}

Desde o Adobe Experience Manager (AEM) Communities 6.1, o conteúdo da comunidade, comumente conhecido como conteúdo gerado pelo usuário (UGC), é armazenado em um único armazenamento comum fornecido por um [provedor de recursos de armazenamento](working-with-srp.md) (SRP).

Há várias opções de SRP, todas acessando o UGC por meio de uma nova interface do AEM Communities, a [API SocialResourceProvider](srp-and-ugc.md) (API SRP), que inclui todas as operações de criação, leitura, atualização e exclusão (CRUD).

Todos os componentes SCF são implementados usando a API SRP, permitindo que o código seja desenvolvido sem o conhecimento da [topologia subjacente](topologies.md) ou do local do UGC.

***A API SocialResourceProvider está disponível somente para clientes licenciados do AEM Communities.***

>[!NOTE]
>
>**Componentes personalizados**: para clientes licenciados do AEM Communities, a API SRP está disponível para desenvolvedores de componentes personalizados para acessar o UGC independentemente da topologia subjacente. Consulte [Fundamentos de SRP e UGC](srp-and-ugc.md).

Consulte também:

* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.

## Sobre o repositório {#about-the-repository}

Para entender o SRP, é útil compreender o papel do repositório do AEM (Oak) em um site da comunidade do AEM.

**Java™ Content Repository (JCR)**
Este padrão define um modelo de dados e uma interface de programação de aplicativos ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) para repositórios de conteúdo. Ele combina características de sistemas de arquivos convencionais com as de bancos de dados relacionais e adiciona vários recursos adicionais que os aplicativos de conteúdo geralmente precisam.

Uma implementação do JCR é o repositório AEM, Oak.

**Apache Jackrabbit Oak**
O [Oak](../../help/sites-deploying/platform.md) é uma implementação do JCR 2.0, que é um sistema de armazenamento de dados projetado para aplicativos centrados em conteúdo. É um tipo de banco de dados hierárquico projetado para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo. A interface para acessar conteúdo é [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

O JCR e o Oak normalmente são usados para fazer referência ao repositório AEM.

Depois de desenvolver o conteúdo do site no ambiente de autor privado, ele deve ser copiado para o ambiente de publicação público. Isso geralmente é feito por meio de uma operação chamada *[replicação](deploy-communities.md#replication-agents-on-author)*. Isso acontece sob o controle do autor/desenvolvedor/administrador.

Para UGC, o conteúdo é inserido por visitantes registrados do site (membros da comunidade) no ambiente de publicação público. Isso acontece aleatoriamente.

Para fins de gerenciamento e relatórios, é útil ter acesso ao UGC do ambiente de autor privado. Com o SRP, o acesso ao UGC do autor é mais consistente e eficiente, pois a replicação reversa do Publish para o autor não é necessária.

## Sobre o SRP {#about-srp}

Quando o UGC é salvo no armazenamento compartilhado, há uma única instância do conteúdo do membro que pode, na maioria das implantações, ser acessada dos ambientes do autor e de publicação. Independentemente da escolha do SRP (MSRP, ASRP, JSRP), todos devem ser acessados de forma programática com a API do SRP.

>[!NOTE]
>
>Consulte [SRP e UGC Essentials](srp-and-ugc.md) para obter o código de exemplo e detalhes adicionais.
>
>Consulte [Acessando o UGC com SRP](accessing-ugc-with-srp.md) para obter práticas recomendadas ao codificar.

### ASRP {#asrp}

Se houver ASRP, o UGC não será armazenado no JCR, ele será armazenado em um serviço de nuvem hospedado e gerenciado pelo Adobe. O UGC armazenado no ASRP pode não ser visualizado com o CRXDE Lite ou acessado usando a API JCR.

Consulte [ASRP - Provedor de Recurso de Armazenamento Adobe](asrp.md).

Os desenvolvedores não podem acessar o UGC diretamente.

O ASRP usa a nuvem de Adobe para consultas.

### MSRP {#msrp}

Se houver, MSRP, UGC não será armazenado no JCR e sim no MongoDB. O UGC armazenado no MSRP pode não ser visualizado com o CRXDE Lite ou acessado usando a API JCR.

Consulte [MSRP - Provedor de Recurso de Armazenamento MongoDB](msrp.md).

Embora o MSRP seja comparável ao ASRP, já que todas as instâncias do servidor AEM estão acessando o mesmo UGC, é possível usar ferramentas comuns para acessar diretamente o UGC armazenado no MongoDB.

O MSRP usa Solr para consultas.

### JSRP {#jsrp}

JSRP é o provedor padrão para acessar todo o UGC em uma única instância do AEM. Ele permite experimentar rapidamente o AEM Communities 6.1 sem a necessidade de configurar o MSRP ou o ASRP.

Consulte [JSRP - Provedor de Recurso de Armazenamento JCR](jsrp.md).

Se houver JSRP enquanto o UGC estiver armazenado em JCR e estiver acessível na API CRXDE Lite e JCR, a Adobe recomenda que você nunca use a API JCR para fazer isso. Se você fizer isso, alterações futuras poderão afetar o código personalizado.

Além disso, o repositório dos ambientes Autor e Publish não é compartilhado. Embora um cluster de instâncias de publicação resulte em um repositório de publicação compartilhado, o UGC inserido no Publish não está visível no Author, portanto, não há capacidade de gerenciar o UGC do author. O UGC só é mantido no repositório AEM (JCR) da instância em que foi inserido.

O JSRP usa os índices Oak para consultas.

## Sobre nós de sombra no JCR {#about-shadow-nodes-in-jcr}

Os nós de sombra, que simulam o caminho para UGC, existem no repositório local para atender a duas finalidades:

1. [Controle de acesso (ACLs)](#for-access-control-acls)
1. [Recursos não existentes (NER)](#for-non-existing-resources-ners)

Independentemente da implementação SRP, o UGC real é *não* visível no mesmo local que o nó de sombra.

### Para ACLs (Access Control, controle de acesso) {#for-access-control-acls}

Algumas implementações de SRP, como ASRP e MSRP, armazenam conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções SRP executam a mesma verificação do local de sombra antes de todas as operações CRUD.

A verificação de ACL usa um método de utilitário que retorna um caminho adequado para verificar as permissões aplicadas ao UGC do recurso.

Consulte [SRP e UGC Essentials](srp-and-ugc.md) para obter o código de exemplo.

### Para recursos não existentes (NERs) {#for-non-existing-resources-ners}

Alguns componentes das Comunidades podem ser incluídos em um script e, portanto, exigem um nó endereçável do Sling para oferecer suporte aos recursos das Comunidades. [Os componentes incluídos](scf.md#add-or-include-a-communities-component) são chamados de NERs (recursos não existentes).

Os nós sombra fornecem um local endereçável do Sling no repositório.

>[!CAUTION]
>
>Como o nó de sombra tem vários usos, a presença de um nó de sombra *não* implica que o componente é um NER.

### Local de armazenamento {#storage-location}

Veja a seguir um exemplo de um nó de sombra, usando o [componente de Comentários](http://localhost:4502/content/community-components/en/comments.html) no [Guia de Componentes da Comunidade](components-guide.md):

* O componente existe no repositório local em:

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* O nó de sombra correspondente existe no repositório local em:

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Nenhum UGC foi encontrado no nó de sombra.

O comportamento padrão é configurar nós de sombra em uma instância de publicação sempre que a subárvore relevante for referenciada para uma leitura ou gravação.

Por exemplo, suponha que a implantação seja [MSRP](msrp.md) com um farm de publicação TarMK.

Quando um [membro](users.md) publica UGC no pub1 (armazenado no MongoDB), os nós de sombra são criados em JCR no pub1.

Na primeira vez que o UGC for lido no pub2, se nada estiver configurado, o comportamento padrão será criar os nós de sombra.

Se você desejar um comportamento diferente do padrão, ele deverá ser configurado na instância de criação e rolado para frente para todas as instâncias de publicação, o que geralmente é um processo manual.
