---
title: SRP - Armazenamento de conteúdo da comunidade
seo-title: SRP - Armazenamento de conteúdo da comunidade
description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos de armazenamento (SRP)
seo-description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos de armazenamento (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# SRP - Armazenamento de conteúdo da comunidade{#srp-community-content-storage}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos de armazenamento (SRP). Há várias opções de SRP a partir das quais escolher, como ASRP, MSRP e JSRP.

Diferentemente das versões anteriores, não há replicação reversa/direta do UGC em instâncias do AEM. Em vez disso, o SRP torna o UGC diretamente acessível para operações de criação, leitura, atualização e exclusão (CRUD) de todas as instâncias de autor e publicação, com exceção do JSRP.

Veja a seguir as [características de cada opção](#characteristics-of-srp-options)SRP, que é uma informação crucial para o processo de decisão ao escolher o SRP apropriado e a implantação [](/help/communities/topologies.md)subjacente.

Para obter detalhes sobre o uso do SRP para UGC, consulte Visão geral [do provedor de recursos de](/help/communities/srp.md)armazenamento.

>[!NOTE]
>
>O SRP se aplica somente ao conteúdo da comunidade. Isso não afeta o local em que o conteúdo do site é armazenado (armazenamento[de](/help/sites-deploying/data-store-config.md)nós) e não afeta a manipulação segura do registro do usuário, dos perfis de usuário e dos grupos de usuários entre as instâncias do AEM (consulte também [Gerenciamento de dados](#managing-user-data)do usuário).

>[!CAUTION]
>
>A partir do AEM 6.1, o [UGC nunca é replicado](#ugc-never-replicated).
>
>Quando a implantação não incluir uma loja comum, como a topologia padrão [JSRP](/help/communities/topologies.md#jsrp) , o UGC estará visível somente na instância de autor ou publicação do AEM na qual foi inserido. Somente se a topologia incluir um cluster de publicação, o UGC estará visível em qualquer instância de publicação.

## Características das opções de SRP {#characteristics-of-srp-options}

[ASRP - Provedor](/help/communities/asrp.md)de recursos de armazenamento da Adobe Com esta opção, o UGC é mantido remotamente em um serviço de nuvem hospedado e gerenciado pela Adobe. Requer uma licença adicional e trabalhar com um representante de conta para fornecer a conta dessa licença específica. O ASRP requer:

* Um serviço em nuvem associado fornecido e suportado pela Adobe para armazenar conteúdo da comunidade.
* Escolha de um data center em uma região geográfica específica (EUA, EMEA, APAC).

* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O ASRP é adequado:

* para o farm de publicação TarMK.
* quando não houver intenção de investir no armazenamento local.

>[!NOTE]
>
>Há um limite para carregar anexos em postagens (ou comentários) no ASRP, que é de 50 MB.

[MSRP - Provedor](/help/communities/msrp.md)de recursos de armazenamento MongoDB Com essa opção, o UGC é persistente diretamente em uma instância MongoDB local.

O MSRP exige:

* Uma instalação local e licenciada do MongoDB para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O ASRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[DSRP - Provedor](/help/communities/dsrp.md)de Recursos de Armazenamento de Banco de Dados Relacional Com essa opção, o UGC é persistente diretamente em uma instância de banco de dados MySQL local.

O DSRP exige:

* Uma instalação local do MySQL para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC deve ser feito por meio da API do SRP.

O DSRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[JSRP - Provedor](/help/communities/jsrp.md)de recursos de armazenamento JCR Com a opção padrão, não há armazenamento comum. O UGC é persistente somente no mesmo repositório JCR que a instância do AEM na qual foi inserido.

JSRP:

* Armazena o conteúdo da comunidade no repositório JCR do autor ou da instância de publicação do AEM na qual foi publicado.
* Exige que todo o acesso programático ao UGC seja feito por meio da API SRP.
* Requer um cluster de publicação se mais de uma instância de publicação estiver implantada (não há mecanismo de replicação entre instâncias de publicação em um farm TarMK).
* a moderação é executada somente no ambiente de publicação (não há mecanismo de replicação reversa/direta entre autor e publicação).
* É melhor para desenvolvimento, demonstrações e treinamento.

## Configuração do SRP {#configuring-srp}

A especificação da opção de armazenamento padrão, com base na implantação subjacente, é feita por meio do console [Configuração de](/help/communities/srp-config.md)armazenamento.

Para obter detalhes sobre a configuração de cada opção, consulte :

* [ASRP - Provedor de recursos de armazenamento da Adobe](/help/communities/asrp.md)
* [MSRP - Provedor de recursos de armazenamento MongoDB](/help/communities/msrp.md)
* [DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)
* [JSRP - Provedor de recursos de armazenamento JCR](/help/communities/jsrp.md)

Se nenhuma opção de armazenamento estiver ativamente selecionada, o JSRP será ativado por padrão.

## Informações adicionais {#additional-information}

### UGC Nunca Replicado {#ugc-never-replicated}

No ambiente do autor, um autor cria o conteúdo da página e o replica no ambiente de publicação. Quando uma página inclui um recurso AEM Communities interativo, como comentários, revisões, fórum, blog ou QnA, a interação dos membros (visitantes do site que fizeram logon) em uma instância de publicação resulta em conteúdo gerado pelo usuário (UGC) inserido no ambiente de publicação.

Anteriormente, esse conteúdo da comunidade era replicado reverso para instâncias do autor e do autor replicado para instâncias de publicação. Foi problemático manter a consistência entre as instâncias do AEM com replicação reversa e posterior.

A partir do AEM Communities 6.1, a necessidade de replicação do UGC foi eliminada com o uso do armazenamento compartilhado para UGC, conforme descrito acima.

Embora o conteúdo do site seja replicado, o UGC nunca é replicado.

### Gerenciamento de dados do usuário {#managing-user-data}

Além disso, interessam às Comunidades os [*usuários *, grupos* de *usuários e perfis* de *](/help/communities/users.md)usuários. Esses dados relacionados ao usuário, quando criados e atualizados no ambiente de publicação, precisam ser disponibilizados para outras instâncias de publicação quando a topologia for um farm[de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicação.

A partir do AEM Communities 6.1, os dados relacionados ao usuário são sincronizados usando a distribuição Sling em vez da replicação. Para obter mais informações, acesse Sincronização [](/help/communities/sync.md)do usuário.

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

Ao atualizar para o AEM 6.5 Communities, se o UGC pré-existente precisar ser retido, as etapas devem ser realizadas dependendo se a comunidade do AEM 5.6.1 ou AEM 6.0 usou o armazenamento sob demanda da Adobe ou o armazenamento local do UGC.

Para obter detalhes, consulte [Atualização para o AEM Communities 6.5](/help/communities/upgrade.md).
