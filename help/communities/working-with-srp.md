---
title: SRP - Armazenamento de conteúdo da comunidade
seo-title: SRP - Community Content Storage
description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em um único armazenamento comum fornecido por um provedor de recursos de armazenamento (SRP)
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# SRP - Armazenamento de conteúdo da comunidade {#srp-community-content-storage}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em um único armazenamento comum fornecido por um provedor de recursos de armazenamento (SRP). Há várias opções de SRP para escolher, como ASRP, MSRP e JSRP.

Ao contrário de versões anteriores, não há replicação reversa/encaminhada de UGC em instâncias AEM. Em vez disso, o SRP torna o UGC diretamente acessível para operações de criação, leitura, atualização e exclusão (CRUD) de todas as instâncias de autor e publicação, com exceção do JSRP.

Veja a seguir [características de cada opção SRP](#characteristics-of-srp-options)que são informações cruciais para o processo de decisão aquando da escolha do SRP adequado e [implantação subjacente](/help/communities/topologies.md).

Para obter detalhes sobre o uso do SRP para UGC, consulte [Visão geral do provedor de recursos de armazenamento](/help/communities/srp.md).

>[!NOTE]
>
>O SRP se aplica somente ao conteúdo da comunidade. Não afeta o local onde o conteúdo do site é armazenado ([armazenamento de nós](/help/sites-deploying/data-store-config.md)), e não afeta o tratamento seguro do registro de usuários, perfis de usuários e grupos de usuários entre instâncias AEM (consulte também [Gerenciamento de dados do usuário](#managing-user-data)).

>[!CAUTION]
>
>A partir do AEM 6.1, [O UGC nunca é replicado](#ugc-never-replicated).
>
>Quando a implantação não inclui um armazenamento comum, como o padrão [JSRP](/help/communities/topologies.md#jsrp) topologia, o UGC será visível somente na instância de publicação ou autor do AEM na qual foi inserido. Somente se a topologia incluir um cluster de publicação o UGC estará visível em qualquer instância de publicação.

## Características das opções de SRP {#characteristics-of-srp-options}

[ASRP - Provedor de recurso de armazenamento de Adobe](/help/communities/asrp.md)

Com essa opção, o UGC é mantido remotamente em um serviço de nuvem hospedado e gerenciado pelo Adobe. Exige uma licença adicional e o trabalho com um representante de conta para provisionar a conta para essa licença específica. ASRP requer:

* Um serviço de nuvem associado fornecido e suportado pelo Adobe para armazenar o conteúdo da comunidade.
* Escolha de um data center em uma região específica (EUA, EMEA, APAC).

* Todo o acesso programático ao UGC pode ser feito por meio da API SRP.

O ASRP é adequado:

* Para farm de publicação TarMK.
* Quando não há intenção de investir em armazenamento local.

>[!NOTE]
>
>Há um limite para fazer upload de anexos em publicações (ou comentários) no ASRP, que é de 50 MB.

[MSRP - Provedor de Recurso de Armazenamento MongoDB](/help/communities/msrp.md)

Com essa opção, o UGC é mantido diretamente em uma instância do MongoDB local.

O MSRP requer:

* Uma instalação local e licenciada do MongoDB para armazenar o conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC pode ser feito por meio da API SRP.

O ASRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[DSRP - Provedor de Recurso de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)

Com essa opção, o UGC é mantido diretamente em uma instância do banco de dados MySQL local.

O DSRP requer:

* Uma instalação local do MySQL para armazenar o conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC pode ser feito por meio da API SRP.

O DSRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[JSRP - Provedor de recurso de armazenamento JCR](/help/communities/jsrp.md)

Com a opção padrão, não há armazenamento comum. O UGC é mantido somente no mesmo repositório JCR que a instância do AEM na qual foi inserido.

JSRP:

* Armazena o conteúdo da comunidade no repositório JCR do autor ou instância de publicação do AEM no qual ele foi publicado.
* Exige que todo o acesso programático ao UGC seja por meio da API SRP.
* Exige um cluster de publicação se mais de uma instância de publicação estiver implantada (não há mecanismo de replicação entre as instâncias de publicação em um farm TarMK).
* a moderação é executada somente no ambiente de publicação (não há mecanismo de replicação reversa/encaminhada entre o autor e a publicação).
* É melhor para desenvolvimento, demonstrações e treinamento.

## Configuração do SRP {#configuring-srp}

A especificação da opção de armazenamento padrão, com base na implantação subjacente, é feita por meio da [Console de configuração de armazenamento](/help/communities/srp-config.md).

Para obter detalhes sobre a configuração de cada opção, consulte:

* [ASRP - Provedor de recurso de armazenamento de Adobe](/help/communities/asrp.md)
* [MSRP - Provedor de Recurso de Armazenamento MongoDB](/help/communities/msrp.md)
* [DSRP - Provedor de Recurso de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)
* [JSRP - Provedor de recurso de armazenamento JCR](/help/communities/jsrp.md)

Se nenhuma opção de armazenamento for selecionada ativamente, o JSRP será ativado por padrão.

## Informações adicionais {#additional-information}

### UGC nunca replicado {#ugc-never-replicated}

No ambiente de criação, um autor cria o conteúdo da página e o replica no ambiente de publicação. Quando uma página inclui um recurso interativo do AEM Communities, como comentários, revisões, fóruns, blogs ou QnA, a interação por membros (visitantes conectados do site) em uma instância de publicação resulta em conteúdo gerado pelo usuário (UGC) inserido no ambiente de publicação.

Anteriormente, esse conteúdo da comunidade era revertido e replicado para instâncias do autor, e do autor era replicado para instâncias de publicação. Era problemático manter a consistência entre instâncias de AEM com replicação reversa e direta.

A partir do AEM Communities 6.1, a necessidade de replicação do UGC foi eliminada com o uso do armazenamento compartilhado do UGC, conforme descrito acima.

Enquanto o conteúdo do site é replicado, o UGC nunca é replicado.

### Gerenciamento de dados do usuário {#managing-user-data}

Também é de interesse para as Comunidades [*usuários*, *grupos de usuários*, e *perfis de usuário*](/help/communities/users.md). Esses dados relacionados ao usuário, quando criados e atualizados no ambiente de publicação, precisam ser disponibilizados para outras instâncias de publicação quando a topologia é um [publicar farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partir do AEM Communities 6.1, os dados relacionados ao usuário são sincronizados usando a distribuição de Sling em vez de replicação. Para obter mais informações, visite [Sincronização de usuário](/help/communities/sync.md).

### Atualização para o AEM Communities 6.5 {#upgrading-to-aem-communities}

Ao atualizar para comunidades AEM 6.5, se a UGC pré-existente precisar ser mantida, as etapas devem ser tomadas dependendo se a comunidade AEM 5.6.1 ou AEM 6.0 usou o armazenamento Adobe sob demanda ou o armazenamento local de UGC.

Para obter detalhes, visite [Atualização para o AEM Communities 6.5](/help/communities/upgrade.md).
