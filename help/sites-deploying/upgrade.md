---
title: Atualização para o Adobe Experience Manager 6.5
description: Saiba mais sobre as noções básicas para atualizar uma instalação mais antiga do Adobe Experience Manager (AEM) para o AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Atualização para o Adobe Experience Manager (AEM) 6.5 {#upgrading-to-aem}

Esta seção aborda a atualização de uma instalação de AEM para AEM 6.5:

* [Planejando sua atualização](/help/sites-deploying/upgrade-planning.md)
* [Avaliando a complexidade da atualização com o Detector de padrões](/help/sites-deploying/pattern-detector.md)
* [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md)
* [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tarefas de Manutenção de Pré-Atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Execução de uma atualização no local](/help/sites-deploying/in-place-upgrade.md)
* [Verificações de atualização e solução de problemas do Post](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md)
* [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md)
* [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Para facilitar a referência às instâncias de AEM envolvidas nesses procedimentos, os seguintes termos são usados nesses artigos:

* A instância de *origem* é a instância AEM da qual você está atualizando.
* A instância de *destino* é para a qual você está atualizando.

>[!NOTE]
>
>Como parte dos esforços para melhorar a confiabilidade das atualizações, o AEM passou por uma reestruturação abrangente dos repositórios. Para obter mais informações sobre como alinhar com a nova estrutura, consulte [Reestruturação do repositório no AEM.](/help/sites-deploying/repository-restructuring.md)

## O que mudou? {#what-has-changed}

A seguir, as principais alterações observadas nas últimas versões do AEM:

O AEM 6.0 apresentou o novo repositório do Jackrabbit Oak. Os Gerenciadores de Persistência foram substituídos por [Micro Kernels](/help/sites-deploying/platform.md#contentbody_title_4). A partir da versão 6.1, não há mais suporte para CRX2. Uma ferramenta de migração chamada crx2oak deve ser executada para migrar repositórios CRX2 de instâncias 5.6.1. Para obter mais informações, consulte [Usando a Ferramenta de Migração CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Se o Assets Insights estiver sendo usado e você estiver atualizando de uma versão anterior ao AEM 6.2, os ativos devem ser migrados e ter IDs geradas por meio de um bean JMX. Para testes internos do Adobe, 125K ativos em um ambiente TarMK foram migrados em uma hora, mas seus resultados podem variar.

A 6.3 introduziu um novo formato para `SegmentNodeStore`, que é a base da implementação do TarMK. Se você estiver atualizando de uma versão anterior ao AEM 6.3, será necessária uma migração de repositório como parte da atualização, envolvendo tempo de inatividade do sistema.

A engenharia de Adobe estima que isso aconteça em cerca de 20 minutos. A reindexação não é necessária. Além disso, uma nova versão da ferramenta crx2oak foi lançada para funcionar com o novo formato de repositório.

**Esta migração não é necessária se estiver atualizando do AEM 6.3 para o AEM 6.5.**

As tarefas de manutenção pré-atualização foram otimizadas para oferecer suporte à automação.

As opções de uso de linha de comando da ferramenta crx2oak foram alteradas para serem compatíveis com automação e mais caminhos de atualização.

As verificações pós-atualização também se tornaram amigáveis para automação.

A coleta de lixo periódica de revisões e a coleta de lixo do armazenamento de dados agora são tarefas de manutenção de rotina que devem ser executadas periodicamente. Com a introdução do AEM 6.3, o Adobe suporta e recomenda a Limpeza de revisão online. Consulte [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md) para obter informações sobre como configurar essas tarefas.

O AEM introduz recentemente o [Detector de Padrões](/help/sites-deploying/pattern-detector.md) para avaliação da complexidade da atualização à medida que você começa a planejar a atualização. O 6.5 também tem um forte foco na [compatibilidade com versões anteriores](/help/sites-deploying/backward-compatibility.md) dos recursos. Finalmente, as práticas recomendadas para [atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md) também são adicionadas.

Para obter mais detalhes sobre o que mais mudou nas versões recentes do AEM, consulte as notas de versão completas:

* [Notas de versão mais recentes do Service Pack do Adobe Experience Manager 6.5](/help/release-notes/release-notes.md)

## Visão geral da atualização {#upgrade-overview}

A atualização do AEM é um processo que envolve várias etapas e, às vezes, vários meses. A estrutura a seguir foi fornecida como uma visão geral do que está incluído em um projeto de atualização e do conteúdo que foi incluído nesta documentação:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Fluxo de atualização {#upgrade-overview-1}

O diagrama abaixo captura o fluxo geral recomendado e destaca a abordagem de atualização. Observe a referência aos novos recursos introduzidos pelo Adobe. A atualização deve começar com o Detector de Padrões (consulte [Avaliação da Complexidade da Atualização com o Detector de Padrões](/help/sites-deploying/pattern-detector.md)), que deve permitir que você decida o caminho que deseja seguir para compatibilidade com o AEM 6.4 com base nos padrões no relatório gerado.

Houve um foco significativo no 6.5 para manter todos os novos recursos compatíveis com versões anteriores, mas nos casos em que você ainda vê alguns problemas de compatibilidade com versões anteriores, o modo de compatibilidade permite adiar temporariamente o desenvolvimento para manter o código personalizado compatível com o 6.5. Essa abordagem ajuda a evitar o esforço de desenvolvimento imediatamente após a atualização (consulte [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Por fim, em seu ciclo de desenvolvimento do 6.5, os recursos introduzidos nas Atualizações sustentáveis (consulte [Atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md)) ajudam você a seguir as práticas recomendadas para tornar as atualizações futuras ainda mais eficientes e contínuas.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
