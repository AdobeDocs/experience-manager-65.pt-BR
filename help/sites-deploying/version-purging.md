---
title: Limpeza de versão
description: Este artigo descreve as opções disponíveis para limpeza de versão.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Limpeza de versão{#version-purging}

Em uma instalação padrão, o Adobe Experience Manager (AEM) cria uma versão de uma página ou nó quando você ativa uma página após atualizar o conteúdo.

>[!NOTE]
>
>Se não houver alterações de conteúdo, você verá a mensagem informando que a página foi ativada, mas nenhuma nova versão será criada.

Você pode criar versões adicionais mediante solicitação usando o **Controle de versão** guia do sidekick. Essas versões são armazenadas no repositório e podem ser restauradas, se necessário.

Essas versões nunca são removidas, portanto, o tamanho do repositório cresce com o tempo e, portanto, deve ser gerenciado.

O AEM é enviado com vários mecanismos para ajudar você a gerenciar seu repositório:

* o [Gerenciador de versão](#version-manager)
Isso pode ser configurado para limpar versões antigas quando novas versões são criadas.

* o [Limpar versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ferramenta É usado como parte do monitoramento e da manutenção do repositório.
Ela permite intervir para remover versões antigas de um nó, ou uma hierarquia de nós, de acordo com estes parâmetros:

   * O número máximo de versões a serem mantidas no repositório.
Quando esse número é excedido, a versão mais antiga é removida.

   * A idade máxima de qualquer versão mantida no repositório.
Quando a idade de uma versão exceder esse valor, ela será removida do repositório.

* o [Tarefa de manutenção de Limpeza de versão](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Você pode programar a tarefa de manutenção Limpeza de versão para excluir versões antigas automaticamente. Como resultado, isso minimiza a necessidade de usar manualmente as ferramentas de Limpeza de versão.

>[!CAUTION]
>
>Para otimizar o tamanho do repositório, execute a tarefa de limpeza de versão frequentemente. A tarefa deve ser agendada fora do horário comercial quando houver uma quantidade limitada de tráfego.

## Gerenciador de versão {#version-manager}

Além da limpeza explícita usando a ferramenta de limpeza, o Gerenciador de versões pode ser configurado para limpar versões antigas quando novas versões são criadas.

Para configurar o Gerenciador de versões, [criar uma configuração](/help/sites-deploying/configuring-osgi.md) para:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

As opções disponíveis são as seguintes:

* `versionmanager.createVersionOnActivation` (Booleano, padrão: true) Especifica se uma versão será criada quando as páginas forem ativadas.
Uma versão é criada, a menos que o agente de replicação esteja configurado para suprimir a criação de versões, que é aplicada pelo Gerenciador de versões.
Uma versão é criada somente se a ativação ocorrer em um caminho contido em `versionmanager.ivPaths` (veja abaixo).

* `versionmanager.ivPaths`(String[], padrão: `{"/"}`) Especifica os caminhos nos quais as versões são criadas implicitamente na ativação se `versionmanager.createVersionOnActivation` está definido como verdadeiro.

* `versionmanager.purgingEnabled` (Booleano, padrão: falso) Define se a limpeza será ativada quando novas versões forem criadas.

* `versionmanager.purgePaths` (String[], padrão: {&quot;/content&quot;}) Especifica em quais caminhos as versões serão removidas quando novas versões forem criadas.

* `versionmanager.maxAgeDays` (int, padrão: 30) Na limpeza da versão, qualquer versão anterior ao valor configurado é removida. Se o valor for menor que 1, a limpeza não será executada com base na idade da versão.

* `versionmanager.maxNumberVersions` (int, padrão 5) Na limpeza de versão, qualquer versão anterior à n-ésima versão mais recente é removida. Se o valor for menor que 1, a limpeza não será executada com base no número de versões.

* `versionmanager.minNumberVersions` (int, padrão 0) O número mínimo de versões que são mantidas independentemente da idade. Se o valor for definido como um valor menor que 1, nenhum número mínimo de versões será retido.

>[!NOTE]
>
>Não é recomendável manter muitas versões no repositório. Portanto, ao configurar a operação de limpeza da versão, lembre-se de não excluir muitas versões da limpeza; caso contrário, o tamanho do repositório não será otimizado corretamente. Se você mantiver um grande número de versões devido a requisitos comerciais, entre em contato com o suporte da Adobe para encontrar maneiras alternativas de otimizar o tamanho do repositório.

### Combinando Opções de Retenção {#combining-retention-options}

As opções que definem como as versões devem ser mantidas ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), podem ser combinados dependendo das suas necessidades.

Por exemplo, ao definir o número máximo de versões a serem mantidas E a versão mais antiga a ser mantida:

* Configuração:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Com:

   * Dez versões foram feitas nos últimos 60 dias
   * Três dessas versões foram criadas nos últimos 30 dias

* Isso significa que:

   * As três últimas versões são mantidas

Por exemplo, ao definir o número mínimo E máximo de versões a serem retidas E a versão mais antiga a ser retida:

* Configuração:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Com:

   * Cinco versões foram feitas há 60 dias

* Isso significa que:

   * Três versões são mantidas

## Ferramenta Limpar versões {#purge-versions-tool}

A variável [Limpar versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) A ferramenta de tem como objetivo limpar as versões de um nó ou de uma hierarquia de nós no repositório. Seu principal objetivo é ajudá-lo a reduzir o tamanho do repositório removendo versões antigas dos nós.
