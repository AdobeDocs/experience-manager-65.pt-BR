---
title: Expurgação de versão
seo-title: Expurgação de versão
description: Este artigo descreve as opções disponíveis para a remoção de versão.
seo-description: Este artigo descreve as opções disponíveis para a remoção de versão.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# Expurgação da Versão{#version-purging}

Em uma instalação padrão, o AEM cria uma nova versão de uma página ou nó quando você ativa uma página depois de atualizar o conteúdo.

>[!NOTE]
>
>Se nenhuma alteração de conteúdo for feita, você verá a mensagem informando que a página foi ativada, mas nenhuma nova versão será criada

Você pode criar versões adicionais mediante solicitação usando a guia **Controle de versão** do sidekick. Essas versões são armazenadas no repositório e podem ser restauradas se necessário.

Essas versões nunca são expurgadas, portanto, o tamanho do repositório crescerá com o tempo e, portanto, precisará ser gerenciado.

AEM é enviado com vários mecanismos para ajudá-lo a gerenciar seu repositório:

* o [Gerenciador de versões](#version-manager)
Isso pode ser configurado para expurgar versões antigas quando novas versões forem criadas.

* a ferramenta [Expurgar Versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)
Isso é usado como parte do monitoramento e da manutenção do repositório.
Ele permite que você intervenha para remover versões antigas de um nó, ou uma hierarquia de nós, de acordo com estes parâmetros:

   * O número máximo de versões a serem mantidas no repositório.
Quando esse número é excedido, a versão mais antiga é removida.

   * A idade máxima de qualquer versão mantida no repositório.
Quando a idade de uma versão exceder esse valor, ele será removido do repositório.

* a tarefa de manutenção [Expurgação da versão](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Você pode agendar a tarefa de manutenção Expurgação da versão para excluir versões antigas automaticamente. Como resultado, isso minimiza a necessidade de usar manualmente as ferramentas de Expurgação de versão.

>[!CAUTION]
>
>Para otimizar o tamanho do repositório, execute a tarefa de expurgação da versão com frequência. A tarefa deve ser agendada fora do horário comercial quando houver uma quantidade limitada de tráfego.

## Gerenciador de versão {#version-manager}

Além da expurgação explícita usando a ferramenta de expurgação, o Gerenciador de versões pode ser configurado para expurgar versões antigas quando novas versões são criadas.

Para configurar o Gerenciador de versões, [crie uma configuração](/help/sites-deploying/configuring-osgi.md) para:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

As opções disponíveis são as seguintes:

* `versionmanager.createVersionOnActivation` (Booleano, padrão: true) Especifica se uma versão deve ser criada quando as páginas são ativadas.
Uma versão é criada, a menos que o agente de replicação esteja configurado para suprimir a criação de versões, que é respeitada pelo Gerenciador de versões.
Uma versão é criada somente se a ativação ocorrer em um caminho contido em `versionmanager.ivPaths` (consulte abaixo).

* `versionmanager.ivPaths`(String[], padrão:  `{"/"}`) Especifica os caminhos nos quais as versões são criadas implicitamente na ativação se  `versionmanager.createVersionOnActivation` estiverem definidas como true.

* `versionmanager.purgingEnabled` (Booleano, padrão: falso) Define se a remoção deve ser ativada ou não quando novas versões forem criadas.

* `versionmanager.purgePaths` (String[], padrão: {&quot;/content&quot;}) Especifica em quais caminhos expurgar versões quando novas versões são criadas.

* `versionmanager.maxAgeDays` (int, padrão: 30) Na limpeza da versão, qualquer versão anterior ao valor configurado será removida. Se o valor for menor que 1, a remoção não será realizada com base na idade da versão.

* `versionmanager.maxNumberVersions` (int, padrão 5) Na limpeza da versão, qualquer versão anterior à n-ª versão mais recente será removida. Se o valor for menor que 1, a expurgação não será realizada com base no número de versões.

* `versionmanager.minNumberVersions` (int, padrão 0) O número mínimo de versões que serão mantidas independentemente da idade. Se o valor for definido como um valor menor que 1, nenhum número mínimo de versões será retido.

>[!NOTE]
>
>Não é recomendável manter um grande número de versões no repositório. Portanto, ao configurar a operação de expurgação da versão, tenha cuidado para não excluir muitas versões da expurgação; caso contrário, o tamanho do repositório não será otimizado corretamente. Se você mantiver um grande número de versões devido a requisitos comerciais, entre em contato com o suporte da Adobe para encontrar formas alternativas de otimizar o tamanho do repositório.

### Combinando opções de retenção {#combining-retention-options}

As opções que definem como quais versões devem ser retidas ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`) podem ser combinadas, dependendo de seus requisitos.

Por exemplo, ao definir o número máximo de versões a serem retidas E a versão mais antiga a ser retida:

* Configuração:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Com:

   * 10 versões feitas nos últimos 60 dias
   * 3 dessas versões criadas nos últimos 30 dias

* Isso significa que:

   * As últimas três versões serão retidas

Por exemplo, ao definir o número máximo E mínimo de versões a serem retidas E a versão mais antiga a ser retida:

* Configuração:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Com:

   * 5 versões feitas há 60 dias

* Isso significa que:

   * 3 versões serão retidas

## Ferramenta Expurgar Versões {#purge-versions-tool}

A ferramenta [Expurgar Versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) destina-se a expurgar as versões de um nó ou uma hierarquia de nós no repositório. Seu objetivo principal é ajudar a reduzir o tamanho do repositório, removendo versões antigas de seus nós.
