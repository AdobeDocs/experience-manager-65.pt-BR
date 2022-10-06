---
title: Topologias recomendadas para comunidades
seo-title: Recommended Topologies for Communities
description: Como abordar a manipulação de conteúdo gerado pelo usuário (UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Topologias recomendadas para comunidades {#recommended-topologies-for-communities}

A partir do AEM Communities 6.1, uma abordagem única foi adotada para lidar com o conteúdo gerado pelo usuário (UGC) enviado pelos visitantes do site (membros) do ambiente de publicação.

Essa abordagem é fundamentalmente diferente da forma como a plataforma de AEM lida com o conteúdo do site, geralmente gerenciado a partir do ambiente de criação.

A plataforma de AEM usa uma loja de nós que replica o conteúdo do site do autor para publicar, enquanto o AEM Communities usa uma única loja comum para UGC que nunca é replicada.

Para o armazenamento UGC comum, é necessário escolher um [provedor de recursos de armazenamento (SRP)](working-with-srp.md). As opções recomendadas são:

* [DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](dsrp.md)
* [MSRP - Provedor de recursos de armazenamento MongoDB](msrp.md)
* [ASRP - Provedor de Recursos de Armazenamento Adobe](asrp.md)

Outra opção SRP, [JSRP - Provedor de recursos de armazenamento JCR](jsrp.md), não oferece suporte a uma loja UGC comum para os ambientes de autor e publicação para ambos os acessos.

Exigir um armazenamento comum resulta nas seguintes topologias recomendadas.

>[!NOTE]
>
>Para AEM Communities, [O UGC nunca é replicado](working-with-srp.md#ugc-never-replicated).
>
>Quando a implantação não inclui um [loja comum](working-with-srp.md), o UGC estará visível somente na instância de publicação ou autor do AEM na qual foi inserido.

>[!NOTE]
>
>Para obter mais informações sobre a plataforma de AEM, consulte [Implantações recomendadas](../../help/sites-deploying/recommended-deploys.md) e [Introdução à plataforma de AEM](../../help/sites-deploying/data-store-config.md).

## Para produção {#for-production}

É essencial estabelecer uma loja comum para o UGC e, portanto, a implantação subjacente depende da sua capacidade de suportar uma loja comum.

Dois exemplos:

1. Se o volume esperado de UGC for alto e uma instância MongoDB local for possível, a escolha será [MSRP](msrp.md).

1. Para obter o desempenho ideal para o conteúdo da página, a escolha de uma [publicar farm](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) e [ASRP](asrp.md) forneceria o dimensionamento ideal do UGC com operações relativamente simples.

Para ambos, a implantação pode ser baseada em qualquer microkernel OAK.

Para escolher a loja comum apropriada, considere cuidadosamente a [características](working-with-srp.md#characteristics-of-srp-options) de cada.

Para obter mais detalhes sobre os microkernals do Oak, visite [Implantações recomendadas](../../help/sites-deploying/recommended-deploys.md).

### Farm de Publicação TarMK {#tarmk-publish-farm}

Quando a topologia é um farm de publicação, os tópicos relevantes de importância são:

* [Sincronização de usuários](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

### Recomendado: DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTEÚDO DO SITE | CONTENTREPOSITÓRIO GERADO PELO USUÁRIO | PROVEDOR DE RECURSOS DE ARMAZENAMENTO | COMO CONSERVAR |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| qualquer | JCR | MySQL | DSRP | Sim |
| qualquer | JCR | MongoDB | MSRP | Sim |
| qualquer | JCR | Adobe on-demand storage | ASRP | Sim |

### JSRP {#jsrp}


| Implantação | CONTEÚDO DO SITE | CONTENTREPOSITÓRIO GERADO PELO USUÁRIO | PROVEDOR DE RECURSOS DE ARMAZENAMENTO | COMO CONSERVAR |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Farm TarMK (padrão) | JCR | JCR | JSRP | Não |
| Cluster Oak | JCR | JCR | JSRP | Sim somente para o ambiente de publicação |

## Para desenvolvimento {#for-development}

Para ambientes não relacionados à produção, [JSRP](jsrp.md) O oferece simplicidade na configuração de um ambiente de desenvolvimento com uma instância de autor e uma instância de publicação.

Se estiver escolhendo [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) para produção, também é possível configurar um ambiente de desenvolvimento semelhante usando o Adobe on demand storage ou o MongoDB. Para ver um exemplo, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

## Referências {#references}

* [Sincronização de usuários](sync.md)

   Discute a sincronização dos dados do usuário entre instâncias do farm de publicação.

* [Gerenciar usuários e grupos de usuários](users.md)

   Discute as funções de usuários e grupos de usuários nos ambientes de criação e publicação.

* UGC [loja comum](working-with-srp.md)

   Descreve o armazenamento de conteúdo da comunidade separado do conteúdo do site.

* [Armazenamento de nós e armazenamento de dados](../../help/sites-deploying/data-store-config.md)

   Basicamente, o conteúdo do site é armazenado em um armazenamento de nós. No Assets, um armazenamento de dados pode ser configurado para armazenar dados binários. Para Comunidades, um armazenamento comum deve ser configurado para selecionar a SRP.

* [Elementos de armazenamento](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Descreve as duas implementações de armazenamento de nó: Tar e MongoDB.
