---
title: Atualização para o AEM 6.5
seo-title: Atualização para o AEM 6.5
description: Saiba mais sobre as noções básicas de atualização de uma instalação antiga do AEM para o AEM 6.5.
seo-description: Saiba mais sobre as noções básicas de atualização de uma instalação antiga do AEM para o AEM 6.5.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Upgrading to AEM 6.5 {#upgrading-to-aem}

Nesta seção, cobrimos a atualização de uma instalação do AEM para o AEM 6.5:

* [Planejamento da atualização](/help/sites-deploying/upgrade-planning.md)
* [Avaliação da complexidade da atualização com o detector de padrões](/help/sites-deploying/pattern-detector.md)
* [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)
* [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md)
* [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tarefas de manutenção de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Execução de uma atualização no local](/help/sites-deploying/in-place-upgrade.md)
* [Verificações e solução de problemas da pós-atualização](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md)
* [Migração de conteúdo ociosa](/help/sites-deploying/lazy-content-migration.md)
* [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring-in-aem65.md)

Para facilitar a referência às instâncias do AEM envolvidas nesses procedimentos, os termos a seguir são usados nestes artigos:

* A instância *de origem* é a instância do AEM da qual você está atualizando.
* A instância de *destino* é aquela para a qual você está atualizando.

>[!NOTE]
>
>Como parte dos esforços para melhorar a confiabilidade das atualizações, o AEM passou por uma reestruturação abrangente do repositório. Para obter mais informações sobre como se alinhar com a nova estrutura, consulte Reestruturação [do repositório no AEM.](/help/sites-deploying/repository-restructuring.md)

## O Que Mudou? {#what-has-changed}

Veja a seguir as principais alterações observadas nas últimas várias versões do AEM:

O AEM 6.0 apresentou o novo repositório do Jackrabbit Oak. Os gerentes de persistência foram substituídos por [Micro Kernels](/help/sites-deploying/platform.md#contentbody_title_4). A partir da versão 6.1, o CRX2 não é mais suportado. Uma ferramenta de migração chamada crx2oak precisa ser executada para migrar repositórios CRX2 de instâncias 5.6.1. Para obter mais informações, consulte [Uso da ferramenta](/help/sites-deploying/using-crx2oak.md)de migração CRX2OAK.

Se o Asset Insights for usado e você estiver atualizando de uma versão anterior ao AEM 6.2, os ativos deverão ser migrados e ter IDs geradas por meio de um bean JMX. Em nossos testes internos, 125 mil ativos em um ambiente TarMK foram migrados em uma hora, mas seus resultados podem variar.

6.3 introduziu um novo formato para o TarMK `SegmentNodeStore`, que é a base da sua implementação. Se você estiver atualizando de uma versão anterior ao AEM 6.3, isso exigirá uma migração de repositório como parte da atualização, envolvendo tempo de inatividade do sistema.

O departamento de engenharia da Adobe estima que seja em torno de 20 minutos. Observe que a reindexação não será necessária. Além disso, uma nova versão da ferramenta crx2oak foi lançada para funcionar com o novo formato de repositório.

**Essa migração não é necessária se você atualizar do AEM 6.3 para o AEM 6.5.**

As tarefas de manutenção de pré-atualização foram otimizadas para suportar automação.

As opções de uso da linha de comando da ferramenta crx2oak foram alteradas para facilitar a automação e suportar mais caminhos de atualização.

As verificações pós-atualização também tornaram a automação fácil.

A coleta periódica de lixo de revisões e a coleta de lixo do armazenamento de dados agora são tarefas de manutenção de rotina que precisam ser executadas periodicamente. Com a introdução do AEM 6.3, a Adobe oferece suporte e recomenda a Limpeza de revisão online. Consulte Limpeza [de revisão](/help/sites-deploying/revision-cleanup.md) para obter informações sobre como configurar essas tarefas.

Recentemente, o AEM apresenta o Detector [de](/help/sites-deploying/pattern-detector.md) padrões para avaliar a complexidade da atualização à medida que você começa a planejar a atualização. 6.5 tem também um forte enfoque na compatibilidade [](/help/sites-deploying/backward-compatibility.md) com versões anteriores dos recursos. Por fim, as práticas recomendadas para upgrades [](/help/sites-deploying/sustainable-upgrades.md) sustentáveis também são adicionadas.

Para obter mais detalhes sobre o que mais mudou nas versões recentes do AEM, consulte as notas de versão completas:

* [https://helpx.adobe.com/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/experience-manager/6-5/release-notes.html)

## Visão geral da atualização {#upgrade-overview}

A atualização do AEM é um processo de várias etapas, às vezes de vários meses. A seguinte estrutura de tópicos foi fornecida como uma visão geral do que está incluído em um projeto de atualização e do conteúdo que foi incluído nesta documentação:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Fluxo de atualização {#upgrade-overview-1}

O diagrama abaixo captura a abordagem de atualização do fluxo geral recomendado. Observe a referência aos novos recursos que apresentamos. A atualização deve começar com o Detector de padrão (consulte [Avaliação da complexidade de atualização com o Detector](/help/sites-deploying/pattern-detector.md)de padrão), que deve permitir que você decida o caminho que deseja seguir para a compatibilidade com o AEM 6.4 com base nos padrões do relatório gerado.

Havia um grande foco na versão 6.5 para manter todos os novos recursos compatíveis com versões anteriores, mas nos casos em que ainda há problemas de compatibilidade com versões anteriores, o modo de compatibilidade permite adiar temporariamente o desenvolvimento para manter seu código personalizado em conformidade com a versão 6.5. Essa abordagem ajuda a evitar esforços de desenvolvimento imediatamente após a atualização (consulte Compatibilidade [com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Finalmente, em seu ciclo de desenvolvimento 6.5, os recursos apresentados em Atualizações sustentáveis (consulte Atualizações [](/help/sites-deploying/sustainable-upgrades.md)sustentáveis) ajudam a seguir as práticas recomendadas para tornar as atualizações futuras ainda mais eficientes e ininterruptas.

![6_4_upgrade_overviewfluxograma-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

