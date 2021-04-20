---
title: SRP - Armazenamento de conteúdo da comunidade
seo-title: SRP - Armazenamento de conteúdo da comunidade
description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em um único armazenamento comum fornecido por um provedor de recursos de armazenamento (SRP)
seo-description: A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em um único armazenamento comum fornecido por um provedor de recursos de armazenamento (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---


# SRP - Armazenamento de conteúdo da comunidade {#srp-community-content-storage}

## Introdução {#introduction}

A partir do AEM Communities 6.1, o conteúdo gerado pelo usuário (UGC) é armazenado em uma única loja comum fornecida por um provedor de recursos de armazenamento (SRP). Há várias opções de SRP a partir das quais escolher, como ASRP, MSRP e JSRP.

Ao contrário de versões anteriores, não há replicação inversa/direta do UGC em instâncias AEM. Em vez disso, o SRP torna o UGC diretamente acessível para operações de criação, leitura, atualização e exclusão (CRUD) de todas as instâncias de criação e publicação, com uma exceção para o JSRP.

Veja a seguir as [características de cada opção SRP](#characteristics-of-srp-options), que são informações cruciais para o processo de decisão ao escolher o SRP apropriado e [implantação subjacente](/help/communities/topologies.md).

Para obter detalhes sobre o uso do SRP para UGC, consulte [Visão Geral do Provedor de Recursos de Armazenamento](/help/communities/srp.md).

>[!NOTE]
>
>O SRP se aplica somente ao conteúdo da comunidade. Isso não afeta o local onde o conteúdo do site é armazenado ([node store](/help/sites-deploying/data-store-config.md)) e não afeta a manipulação segura do registro de usuários, perfis de usuários e grupos de usuários entre AEM instâncias (consulte também [Gerenciando Dados do Usuário](#managing-user-data)).

>[!CAUTION]
>
>A partir AEM 6.1, [UGC nunca será replicado](#ugc-never-replicated).
>
>Quando a implantação não inclui um armazenamento comum, como a topologia padrão [JSRP](/help/communities/topologies.md#jsrp), o UGC estará visível somente na instância de publicação ou autor do AEM em que foi inserido. Somente se a topologia incluir um cluster de publicação, o UGC estará visível em qualquer instância de publicação.

## Características das opções do SRP {#characteristics-of-srp-options}

[ASRP - Provedor de Recursos de Armazenamento Adobe](/help/communities/asrp.md)

Com essa opção, o UGC é mantido remotamente em um serviço de nuvem hospedado e gerenciado pelo Adobe. Exige uma licença adicional e trabalha com um representante de conta para fornecer a conta dessa licença específica. O ASRP requer:

* Um serviço de nuvem associado fornecido e suportado pelo Adobe para armazenar conteúdo da comunidade.
* Escolha de um data center em uma região específica (EUA, EMEA, APAC).

* Todo o acesso programático ao UGC pode ser feito por meio da API do SRP.

O ASRP é adequado:

* Para o farm de publicação do TarMK.
* Quando não há intenção de investir em armazenamento local.

>[!NOTE]
>
>Há um limite para carregar anexos em postagens (ou comentários) no ASRP, que é de 50 MB.

[MSRP - Provedor de recursos de armazenamento MongoDB](/help/communities/msrp.md)

Com essa opção, o UGC é persistente diretamente em uma instância MongoDB local.

O MSRP requer:

* Uma instalação local licenciada do MongoDB para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC pode ser feito por meio da API do SRP.

O ASRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)

Com essa opção, o UGC é mantido diretamente em uma instância de banco de dados local do MySQL.

O DSRP requer:

* Uma instalação local do MySQL para armazenar conteúdo da comunidade.
* Uma instalação local do Apache Solr.
* Todo o acesso programático ao UGC pode ser feito por meio da API do SRP.

O DSRP é adequado:

* Para um farm de publicação TarMK existente.
* Para um cluster MongoMK ou RdbMK.
* Ao esperar grandes volumes de conteúdo da comunidade.

[JSRP - Provedor de recursos de armazenamento JCR](/help/communities/jsrp.md)

Com a opção padrão , não há um armazenamento comum. O UGC é persistente somente no mesmo repositório JCR que a instância AEM na qual foi inserido.

JSRP:

* Armazena o conteúdo da comunidade no repositório JCR do autor ou instância de publicação do AEM em que foi publicado.
* Requer que todo o acesso programático ao UGC seja feito por meio da API do SRP.
* Requer um cluster de publicação se mais de uma instância de publicação estiver implantada (não há mecanismo de replicação entre instâncias de publicação em um farm TarMK).
* a moderação é executada somente no ambiente de publicação (não há mecanismo de replicação inversa/direta entre autor e publicação).
* É o melhor para desenvolvimento, demonstrações e treinamento.

## Configuração do SRP {#configuring-srp}

A especificação da opção de armazenamento padrão, com base na implantação subjacente, é feita por meio do [Storage Configuration console](/help/communities/srp-config.md).

Para obter detalhes de configuração de cada opção, consulte:

* [ASRP - Provedor de Recursos de Armazenamento Adobe](/help/communities/asrp.md)
* [MSRP - Provedor de recursos de armazenamento MongoDB](/help/communities/msrp.md)
* [DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional](/help/communities/dsrp.md)
* [JSRP - Provedor de recursos de armazenamento JCR](/help/communities/jsrp.md)

Se nenhuma opção de armazenamento for selecionada ativamente, o JSRP será ativado por padrão.

## Informações adicionais {#additional-information}

### UGC Nunca Replicado {#ugc-never-replicated}

No ambiente de criação, um autor cria conteúdo de página e o replica no ambiente de publicação. Quando uma página inclui um recurso interativo do AEM Communities, como comentários, revisões, fórum, blog ou QnA, a interação dos membros (visitantes do site conectados) em uma instância de publicação resulta no conteúdo gerado pelo usuário (UGC) inserido no ambiente de publicação.

Anteriormente, esse conteúdo da comunidade era replicado inversamente para instâncias do autor e do autor replicado para instâncias de publicação. Era problemático manter a consistência entre instâncias AEM com replicação inversa e posterior.

A partir do AEM Communities 6.1, a necessidade de replicação do UGC foi eliminada usando o armazenamento compartilhado do UGC, conforme descrito acima.

Embora o conteúdo do site seja replicado, o UGC nunca é replicado.

### Gerenciando dados do usuário {#managing-user-data}

Além disso, de interesse para o CommunitIes são [*users*, *grupos de usuários* e *perfis de usuário*](/help/communities/users.md). Esses dados relacionados ao usuário, quando criados e atualizados no ambiente de publicação, precisam ser disponibilizados para outras instâncias de publicação quando a topologia for um [farm de publicação](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partir do AEM Communities 6.1, os dados relacionados ao usuário são sincronizados usando a distribuição do Sling em vez da replicação. Para obter mais informações, visite [Sincronização de Usuário](/help/communities/sync.md).

### Atualização para o AEM Communities 6.5 {#upgrading-to-aem-communities}

Ao atualizar para AEM 6.5 Comunidades, se o UGC pré-existente precisar ser retido, as etapas devem ser tomadas, dependendo se a comunidade AEM 5.6.1 ou AEM 6.0 usou o armazenamento Adobe on Demand ou o armazenamento local do UGC.

Para obter detalhes, visite [Atualizando para o AEM Communities 6.5](/help/communities/upgrade.md).
