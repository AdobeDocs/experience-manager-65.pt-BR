---
title: Topologias recomendadas para comunidades
description: Como abordar o manuseio de conteúdo gerado pelo usuário (UGC)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Topologias recomendadas para comunidades {#recommended-topologies-for-communities}

A partir do AEM Communities 6.1, uma abordagem única foi adotada para lidar com o conteúdo gerado pelo usuário (UGC) enviado pelos visitantes do site (membros) do ambiente de publicação.

Essa abordagem é fundamentalmente diferente da maneira como a plataforma AEM lida com o conteúdo do site, que geralmente é gerenciado no ambiente do autor.

A plataforma AEM usa um armazenamento de nós que replica o conteúdo do site do autor para a publicação, enquanto o AEM Communities usa um armazenamento único e comum para UGC que nunca é replicado.

Para o armazenamento UGC comum, é necessário escolher um [provedor de recursos de armazenamento (SRP)](working-with-srp.md). As opções recomendadas são:

* [DSRP - Provedor de Recurso de Armazenamento de Banco de Dados Relacional](dsrp.md)
* [MSRP - Provedor de Recurso de Armazenamento MongoDB](msrp.md)
* [ASRP - Provedor de recurso de armazenamento de Adobe](asrp.md)

Uma outra opção do SRP, [JSRP - Provedor de Recurso de Armazenamento JCR](jsrp.md), não oferece suporte a um armazenamento UGC comum para os ambientes de criação e publicação para ambos os acessos.

A exigência de um armazenamento comum resulta nas seguintes topologias recomendadas.

>[!NOTE]
>
>Para o AEM Communities, [o UGC nunca é replicado](working-with-srp.md#ugc-never-replicated).
>
>Quando a implantação não incluir um [armazenamento comum](working-with-srp.md), o UGC será visível somente na instância de publicação ou autor do AEM em que foi inserido.
>

>[!NOTE]
>
>Para obter mais informações sobre a plataforma AEM, consulte [Implantações recomendadas](../../help/sites-deploying/recommended-deploys.md) e [Introdução à plataforma AEM](../../help/sites-deploying/data-store-config.md).

## Para produção {#for-production}

Estabelecer um armazenamento comum para UGC é essencial e, portanto, a implantação subjacente depende de sua capacidade de dar suporte a um armazenamento comum.

Dois exemplos:

1. Se o volume esperado de UGC for alto e uma instância de MongoDB local for possível, a escolha será [MSRP](msrp.md).

1. Para um desempenho ideal do conteúdo da página, a escolha de um [farm de publicação](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) e [ASRP](asrp.md) forneceria o dimensionamento ideal de UGC com operações relativamente simples.

Para ambos, a implantação pode ser baseada em qualquer microkernel OAK.

Para escolher o armazenamento comum apropriado, considere cuidadosamente as [características](working-with-srp.md#characteristics-of-srp-options) exclusivas de cada uma.

Para obter mais detalhes sobre microkernals do Oak, visite [Implantações recomendadas](../../help/sites-deploying/recommended-deploys.md).

### Farm do Publish TarMK {#tarmk-publish-farm}

Quando a topologia é um farm de publicação, os tópicos relevantes de importância são:

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

### Recomendado: DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| Microkernel | SITE CONTENTREPOSITORY | CONTENTREPOSITORY GERADO PELO USUÁRIO | PROVEDOR DE RECURSOS DE ARMAZENAMENTO | ARMAZENAMENTO COMUM |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| qualquer | JCR | MySQL | DSRP | Sim |
| qualquer | JCR | MongoDB | MSRP | Sim |
| qualquer | JCR | Adobe on-demand storage | ASRP | Sim |

### JSRP {#jsrp}


| Implantação | SITE CONTENTREPOSITORY | CONTENTREPOSITORY GERADO PELO USUÁRIO | PROVEDOR DE RECURSOS DE ARMAZENAMENTO | ARMAZENAMENTO COMUM |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Farm TarMK (padrão) | JCR | JCR | JSRP | Não |
| Cluster Oak | JCR | JCR | JSRP | Sim somente para o ambiente de publicação |

## Para desenvolvimento {#for-development}

Para ambientes não relacionados à produção, o [JSRP](jsrp.md) oferece simplicidade na configuração de um ambiente de desenvolvimento com uma instância de autor e uma instância de publicação.

Se você escolher [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) para produção, também será possível configurar um ambiente de desenvolvimento semelhante usando o armazenamento sob demanda do Adobe ou o MongoDB. Para obter um exemplo, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

## Referências {#references}

* [Sincronização de usuário](sync.md)

  Discute a sincronização dos dados do usuário entre as instâncias do farm de publicação.

* [Gerenciar usuários e grupos de usuários](users.md)

  Discute as funções dos usuários e grupos de usuários nos ambientes do autor e de publicação.

* UGC [repositório comum](working-with-srp.md)

  Descreve o armazenamento do conteúdo da comunidade separado do conteúdo do site.

* [Armazenamentos de nós e armazenamentos de dados](../../help/sites-deploying/data-store-config.md)

  Basicamente, o conteúdo do site é armazenado em um armazenamento de nó. Para o Assets, um armazenamento de dados pode ser configurado para armazenar dados binários. Para Communities, um armazenamento comum deve ser configurado para selecionar o SRP.

* [Elementos de armazenamento](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Descreve as implementações de armazenamento de dois nós: Tar e MongoDB.
