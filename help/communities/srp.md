---
title: Visão geral do provedor de recursos do armazenamento
seo-title: Visão geral do provedor de recursos do armazenamento
description: Armazenamento comum das Comunidades
seo-description: Armazenamento comum das Comunidades
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# Visão geral do provedor de recursos do armazenamento {#storage-resource-provider-overview}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo da comunidade, geralmente conhecido como conteúdo gerado pelo usuário (UGC), é armazenado em uma única loja comum fornecida por um provedor [de recursos do](working-with-srp.md) armazenamento (SRP).

Existem várias opções de SRP, todas elas acessando o UGC por meio de uma nova interface AEM Communities, a API [SRP (](srp-and-ugc.md) SocialResourceProvider API), que inclui todas as operações de criação, leitura, atualização e exclusão (CRUD).

Todos os componentes do SCF são implementados usando a API SRP, permitindo que o código seja desenvolvido sem o conhecimento da topologia [](topologies.md) subjacente ou da localização do UGC.

***A API SocialResourceProvider está disponível somente para clientes licenciados da AEM Communities.***

>[!NOTE]
>
>**Componentes** personalizados: Para clientes licenciados da AEM Communities, a API SRP está disponível para desenvolvedores de componentes personalizados com o objetivo de acessar o UGC sem considerar a topologia subjacente. Consulte [SRP e UGC Essentials](srp-and-ugc.md).


Consulte também:

* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração](socialutils.md) SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

## Sobre o repositório {#about-the-repository}

Para entender o SRP, é útil entender a função do repositório AEM (OAK) em um site da comunidade AEM.

**Java Content Repository (JCR)** Este padrão define um modelo de dados e uma interface de programação de aplicativo (API[](https://jackrabbit.apache.org/jcr/jcr-api.html)JCR) para repositórios de conteúdo. Ele combina características de sistemas de arquivos convencionais com as de bancos de dados relacionais e adiciona vários recursos adicionais que os aplicativos de conteúdo frequentemente precisam.

Uma implementação do JCR é o repositório AEM, OAK.

**Apache Jackrabbit Oak (OAK)**[OAK](../../help/sites-deploying/platform.md) é uma implementação do JCR 2.0 que é um sistema de armazenamento de dados especificamente projetado para aplicativos centrados em conteúdo. É um tipo de banco de dados hierárquico projetado para dados não estruturados e semiestruturados. O repositório armazena não apenas o conteúdo voltado para o usuário, mas também todos os códigos, modelos e dados internos usados pelo aplicativo. A interface do usuário para acessar conteúdo é [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

O JCR e o OAK normalmente são usados para fazer referência ao repositório AEM.

Depois de desenvolver o conteúdo do site no ambiente do autor privado, ele deve ser copiado para o ambiente de publicação público. Isso geralmente é feito por meio de uma operação chamada *[replicação](deploy-communities.md#replication-agents-on-author)*. Isso acontece sob o controle do autor/desenvolvedor/administrador.

Para o UGC, o conteúdo é inserido por visitantes do site registrados (membros da comunidade) no ambiente de publicação pública. Isto acontece aleatoriamente.

Para fins de gerenciamento e relatórios, é útil ter acesso ao UGC do ambiente do autor privado. Com o SRP, o acesso ao UGC do autor é mais consistente e eficiente, já que a replicação reversa da publicação para o autor não é necessária.

## Sobre o SRP {#about-srp}

Quando o UGC é salvo no armazenamento compartilhado, há uma única instância do conteúdo do membro que pode, na maioria das implantações, ser acessado do autor e dos ambientes de publicação. Independentemente da escolha do SRP (MSRP, ASRP, JSRP), todos devem ser acessados de forma programática com a API do SRP.

>[!NOTE]
>
>Consulte [SRP e UGC Essentials](srp-and-ugc.md) para obter exemplos de código e detalhes adicionais.
>
>Consulte [Acessar o UGC com SRP](accessing-ugc-with-srp.md) para obter as práticas recomendadas na codificação.


### ASRP {#asrp}

No caso de ASRP, o UGC não é armazenado no JCR, ele é armazenado em um serviço de nuvem hospedado e gerenciado pelo Adobe. O UGC armazenado no ASRP não pode ser exibido com o CRXDE Lite nem acessado usando a API do JCR.

Consulte [ASRP - Provedor](asrp.md)de Recursos do Armazenamento.

Não é possível aos desenvolvedores acessar o UGC diretamente.

O ASRP usa a nuvem Adobe para query.

### MSRP {#msrp}

No caso do MSRP, o UGC não é armazenado no JCR, ele é armazenado no MongoDB. O UGC armazenado no MSRP pode não ser visualizado com o CRXDE Lite nem acessado usando a API do JCR.

Consulte [MSRP - Provedor](msrp.md)de recursos do Armazenamento MongoDB.

Embora o MSRP seja comparável ao ASRP, como todas as instâncias de servidor AEM estão acessando o mesmo UGC, é possível usar ferramentas comuns para acessar diretamente o UGC armazenado no MongoDB.

O MSRP usa o Solr para query.

### JSRP {#jsrp}

O JSRP é o provedor padrão para acessar todo o UGC em uma única instância AEM. Ele oferece a capacidade de experimentar rapidamente o AEM Communities 6.1 sem a necessidade de configurar o MSRP ou o ASRP.

Consulte [JSRP - Provedor](jsrp.md)de recursos do Armazenamento JCR.

No caso do JSRP, embora o UGC seja armazenado no JCR e acessível por meio da API do CRXDE Lite e do JCR, é altamente recomendável que a API do JCR nunca seja usada para isso, caso contrário, alterações futuras podem afetar o código personalizado.

Além disso, o repositório dos ambientes do autor e publicação não é compartilhado. Embora um cluster de instâncias de publicação resulte em um repositório de publicação compartilhado, o UGC inserido na publicação não estará visível no autor, portanto, não será possível gerenciar o UGC do autor. O UGC só é persistente no repositório AEM (JCR) da instância em que foi inserido.

O JSRP usa os índices Oak para query.

## Sobre nós de sombra no JCR {#about-shadow-nodes-in-jcr}

Os nós de sombra, que imitam o caminho para o UGC, existem no repositório local para atender a duas finalidades:

1. [controle de acesso (ACLs)](#for-access-control-acls)
1. [Recursos não existentes (NERs)](#for-non-existing-resources-ners)

Independentemente da implementação do SRP, o UGC real *não será *visível no mesmo local que o nó de sombra.

### Para Controle de acesso (ACLs) {#for-access-control-acls}

Algumas implementações SRP, como ASRP e MSRP, armazenam conteúdo da comunidade em bancos de dados que não fornecem verificação de ACL. Os nós de sombra fornecem um local no repositório local ao qual as ACLs podem ser aplicadas.

Usando a API SRP, todas as opções SRP executam a mesma verificação do local da sombra antes de todas as operações CRUD.

A verificação de ACL usa um método de utilitário que retorna um caminho adequado para verificar as permissões aplicadas ao UGC do recurso.

Consulte [SRP e UGC Essentials](srp-and-ugc.md) para obter exemplos de código.

### Para recursos não existentes (NERs) {#for-non-existing-resources-ners}

Alguns componentes das Comunidades podem ser incluídos em um script e, portanto, exigem um nó endereçável Sling para suportar os recursos das Comunidades. [Os componentes](scf.md#add-or-include-a-communities-component) incluídos são chamados de recursos não existentes (NERs).

Os nós de sombra fornecem um local endereçável Sling no repositório.

>[!CAUTION]
>
>Como o nó de sombra tem vários usos, a presença de um nó de sombra *não* implica que o componente seja um NER.


### Localização do armazenamento {#storage-location}

Veja a seguir um exemplo de um nó de sombra, usando o componente [](http://localhost:4502/content/community-components/en/comments.html) Comentários no Guia [de componentes da](components-guide.md)comunidade:

* O componente existe no repositório local em:

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* O nó de sombra correspondente existe no repositório local em:

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Nenhum UGC será encontrado sob o nó de sombra.

O comportamento padrão é configurar nós de sombra em uma instância de publicação sempre que a subárvore relevante for referenciada para leitura ou gravação.

Como exemplo, suponha que a implantação seja [MSRP](msrp.md) com um farm de publicação TarMK.

Quando um [membro](users.md) postar UGC no pub1 (armazenado em MongoDB), os nós de sombra são criados no JCR no pub1.

Na primeira vez que o UGC é lido no pub2, se nada estiver configurado, o comportamento padrão é criar os nós de sombra.

Se for desejado outro comportamento que não o padrão, ele deverá ser configurado na instância do autor e encaminhado para todas as instâncias de publicação, que geralmente é um processo manual.
