---
title: SRP - Armazenamento de conteúdo da comunidade
seo-title: SRP - Armazenamento de conteúdo da comunidade
description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos do armazenamento (SRP)
seo-description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos do armazenamento (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---


# SRP - Armazenamento de conteúdo da comunidade {#srp-community-content-storage}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos do armazenamento (SRP). Há várias opções de SRP a partir das quais escolher, como ASRP, MSRP e JSRP.

Diferentemente das versões anteriores, não há replicação reversa/direta do UGC em instâncias AEM. Em vez disso, o SRP torna o UGC diretamente acessível para operações de criação, leitura, atualização e exclusão (CRUD) de todas as instâncias de autor e publicação, com uma exceção para JSRP.

Veja a seguir as [características de cada opção](#characteristics-of-srp-options)SRP, que é uma informação crucial para o processo de decisão ao escolher o SRP apropriado e a implantação [](/help/communities/topologies.md)subjacente.

Para obter detalhes sobre o uso do SRP para UGC, consulte Visão geral [do provedor de recursos do](/help/communities/srp.md)Armazenamento.

>[!NOTE]
>
>O SRP se aplica somente ao conteúdo da comunidade. Isso não afeta o local em que o conteúdo do site é armazenado (armazenamento[de](/help/sites-deploying/data-store-config.md)nós) e não afeta a manipulação segura do registro do usuário, perfis de usuário e grupos de usuários entre AEM instâncias (consulte também [Gerenciamento de dados](#managing-user-data)do usuário).

>[!CAUTION]
>
>A partir AEM 6.1, o [UGC nunca é replicado](#ugc-never-replicated).
>
>Quando a implantação não incluir um armazenamento comum, como a topologia padrão [JSRP](/help/communities/topologies.md#jsrp) , o UGC estará visível somente na instância de publicação ou autor do AEM em que foi inserido. Somente se a topologia incluir um cluster de publicação, o UGC estará visível em qualquer instância de publicação.

## Características das opções de SRP {#characteristics-of-srp-options}

[ASRP - Provedor de Recursos de Armazenamento de Adobe](/help/communities/asrp.md)

Com essa opção, o UGC é mantido remotamente em um serviço de nuvem hospedado e gerenciado pelo Adobe. Requer uma licença adicional e trabalhar com um representante de conta para fornecer a conta dessa licença específica. O ASRP requer:

* Um serviço em nuvem associado fornecido e suportado pela Adobe para armazenar conteúdo da comunidade.
* Escolha de um data center em uma região geográfica específica (EUA, EMEA, APAC).

* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O ASRP é adequado:

* Para o farm de publicação do TarMK.
* Quando não há intenção de investir no armazenamento local.

>[!NOTE]
>
>Há um limite para carregar anexos em postagens (ou comentários) no ASRP, que é de 50 MB.

[MSRP - Provedor de recursos do Armazenamento MongoDB](/help/communities/msrp.md)

Com essa opção, o UGC é persistente diretamente em uma instância do MongoDB local.

O MSRP exige:

* Uma instalação local e licenciada do MongoDB para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O ASRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)

Com essa opção, o UGC é persistente diretamente em uma instância de banco de dados MySQL local.

O DSRP exige:

* Uma instalação local do MySQL para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O DSRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[JSRP - Provedor de recursos do Armazenamento JCR](/help/communities/jsrp.md)

Com a opção padrão, não há armazenamento comum. O UGC é persistente somente no mesmo repositório JCR que a instância AEM na qual foi inserido.

JSRP:

* Armazena o conteúdo da comunidade no repositório JCR do autor ou da instância de publicação AEM na qual foi postada.
* Exige que todo o acesso programático ao UGC seja feito por meio da API SRP.
* Requer um cluster de publicação se mais de uma instância de publicação estiver implantada (não há mecanismo de replicação entre instâncias de publicação em um farm do TarMK).
* a moderação é executada somente no ambiente de publicação (não há mecanismo de replicação reversa/direta entre autor e publicação).
* É melhor para desenvolvimento, demonstrações e treinamento.

## Configuração do SRP {#configuring-srp}

A especificação da opção de armazenamento padrão, com base na implantação subjacente, é feita pelo console [Configuração do](/help/communities/srp-config.md)Armazenamento.

Para obter detalhes de configuração de cada opção, consulte:

* [ASRP - Provedor de Recursos de Armazenamento de Adobe](/help/communities/asrp.md)
* [MSRP - Provedor de recursos do Armazenamento MongoDB](/help/communities/msrp.md)
* [DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)
* [JSRP - Provedor de recursos do Armazenamento JCR](/help/communities/jsrp.md)

Se nenhuma opção de armazenamento estiver ativamente selecionada, o JSRP será ativado por padrão.

## Informações adicionais {#additional-information}

### UGC Nunca Replicado {#ugc-never-replicated}

No ambiente do autor, um autor cria o conteúdo da página e o replica no ambiente de publicação. Quando uma página inclui um recurso interativo do AEM Communities, como comentários, revisões, fórum, blog ou QnA, a interação dos membros (conectados aos visitantes do site) em uma instância de publicação resulta em conteúdo gerado pelo usuário (UGC) inserido no ambiente de publicação.

Anteriormente, esse conteúdo da comunidade era replicado reverso para instâncias do autor e do autor replicado para instâncias de publicação. Foi problemático manter a consistência entre instâncias AEM com replicação reversa e posterior.

A partir do AEM Communities 6.1, a necessidade de replicação do UGC foi eliminada usando armazenamento compartilhado para UGC, conforme descrito acima.

Embora o conteúdo do site seja replicado, o UGC nunca é replicado.

### Gerenciamento de dados do usuário {#managing-user-data}

Além disso, interessam às Comunidades [*os usuários*, grupos *de* usuários e perfis *de*](/help/communities/users.md) usuários. Esses dados relacionados ao usuário, quando criados e atualizados no ambiente de publicação, precisam ser disponibilizados para outras instâncias de publicação quando a topologia for um farm [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicação.

A partir do AEM Communities 6.1, os dados relacionados ao usuário são sincronizados usando a distribuição Sling em vez da replicação. Para obter mais informações, acesse Sincronização [](/help/communities/sync.md)do usuário.

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

Ao atualizar para AEM 6.5 Comunidades, se o UGC pré-existente precisar ser retido, as etapas devem ser realizadas dependendo se a comunidade AEM 5.6.1 ou AEM 6.0 usou o armazenamento Adobe sob demanda ou o armazenamento local do UGC.

Para obter detalhes, visite [Upgrading to AEM Communities 6.5](/help/communities/upgrade.md).
