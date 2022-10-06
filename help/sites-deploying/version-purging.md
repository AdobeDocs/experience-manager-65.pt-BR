---
title: Limpeza de versão
seo-title: Version Purging
description: Este artigo descreve as opções disponíveis para limpeza de versão.
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# Limpeza de versão{#version-purging}

Em uma instalação padrão, o AEM cria uma nova versão de uma página ou nó quando você ativa uma página após atualizar o conteúdo.

>[!NOTE]
>
>Se nenhuma alteração de conteúdo for feita, você verá a mensagem informando que a página foi ativada, mas nenhuma nova versão será criada

Você pode criar versões adicionais mediante solicitação usando o **Controle de versão** guia do sidekick. Essas versões são armazenadas no repositório e podem ser restauradas, se necessário.

Essas versões nunca são removidas, portanto, o tamanho do repositório aumentará com o tempo e, portanto, precisará ser gerenciado.

AEM é enviado com vários mecanismos para ajudá-lo a gerenciar seu repositório:

* o [Gerenciador de versão](#version-manager)
Isso pode ser configurado para limpar versões antigas quando novas versões forem criadas.

* o [Limpar versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ferramenta Isso é usado como parte do monitoramento e da manutenção do repositório.
Ela permite intervir para remover versões antigas de um nó ou uma hierarquia de nós, de acordo com estes parâmetros:

   * O número máximo de versões a serem mantidas no repositório.
Quando esse número é excedido, a versão mais antiga é removida.

   * A idade máxima de qualquer versão mantida no repositório.
Quando a idade de uma versão exceder esse valor, ela será removida do repositório.

* o [Tarefa de manutenção de limpeza de versão](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Você pode agendar a tarefa de manutenção da limpeza de versão para excluir automaticamente as versões antigas. Como resultado, isso minimiza a necessidade de usar manualmente as ferramentas de limpeza de versão.

>[!CAUTION]
>
>Para otimizar o tamanho do repositório, você deve executar a tarefa de limpeza de versão com frequência. A tarefa deve ser agendada fora do horário comercial, quando houver uma quantidade limitada de tráfego.

## Gerenciador de versão {#version-manager}

Além da limpeza explícita usando a ferramenta de limpeza, o Gerenciador de versões pode ser configurado para limpar versões antigas quando novas versões são criadas.

Para configurar o Gerenciador de versões, [criar uma configuração](/help/sites-deploying/configuring-osgi.md) a favor:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

As opções disponíveis são as seguintes:

* `versionmanager.createVersionOnActivation` (Booleano, padrão: true) Especifica a criação de uma versão quando as páginas forem ativadas.
Uma versão é criada a menos que o agente de replicação esteja configurado para suprimir a criação de versões, que é respeitada pelo Gerenciador de versões.
Uma versão é criada somente se a ativação ocorrer em um caminho contido em `versionmanager.ivPaths` (veja abaixo).

* `versionmanager.ivPaths`(String[], padrão: `{"/"}`) Especifica os caminhos nos quais as versões são criadas implicitamente na ativação se `versionmanager.createVersionOnActivation` está definida como true.

* `versionmanager.purgingEnabled` (Booleano, padrão: falso) Define se a limpeza deve ser ativada ou não quando novas versões são criadas.

* `versionmanager.purgePaths` (String[], padrão: {&quot;/content&quot;}) Especifica os caminhos para limpar versões quando novas versões forem criadas.

* `versionmanager.maxAgeDays` (int, padrão: 30) Na limpeza de versão, qualquer versão anterior ao valor configurado será removida. Se o valor for menor que 1, a limpeza não será executada com base na idade da versão.

* `versionmanager.maxNumberVersions` (int, padrão 5) Na limpeza de versão, qualquer versão anterior à n-ª versão mais recente será removida. Se o valor for menor que 1, a limpeza não será executada com base no número de versões.

* `versionmanager.minNumberVersions` (int, padrão 0) O número mínimo de versões que serão mantidas independentemente da idade. Se o valor for definido como um valor menor que 1, nenhum número mínimo de versões será retido.

>[!NOTE]
>
>Não é recomendável manter um grande número de versões no repositório. Portanto, ao configurar a operação de limpeza de versão, tenha cuidado para não excluir muitas versões da limpeza; caso contrário, o tamanho do repositório não será otimizado corretamente. Se você mantém um grande número de versões devido a requisitos comerciais, entre em contato com o suporte do Adobe para encontrar maneiras alternativas de otimizar o tamanho do repositório.

### Combinação de opções de retenção {#combining-retention-options}

As opções que definem como quais versões devem ser retidas ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), podem ser combinadas dependendo das suas necessidades.

Por exemplo, ao definir o número máximo de versões a serem retidas E a versão mais antiga a ser retida:

* Configuração:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Com:

   * 10 versões feitas nos últimos 60 dias
   * 3 dessas versões criadas nos últimos 30 dias

* Significará que:

   * As últimas 3 versões serão retidas

Por exemplo, ao definir o número mínimo e máximo de versões a serem retidas E a versão mais antiga a ser retida:

* Configuração:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Com:

   * 5 versões feitas há 60 dias

* Significará que:

   * 3 versões serão retidas

## Ferramenta Limpar versões {#purge-versions-tool}

O [Limpar versões](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) A ferramenta destina-se a limpar as versões de um nó ou uma hierarquia de nós em seu repositório. Seu objetivo principal é ajudar você a reduzir o tamanho do repositório, removendo versões antigas dos nós.
