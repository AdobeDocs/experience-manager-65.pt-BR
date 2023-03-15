---
title: Atualização para o AEM 6.5
seo-title: Upgrading to AEM 6.5
description: Saiba mais sobre as noções básicas para atualizar uma instalação de AEM mais antiga para a AEM 6.5.
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 02fc145d5ec1458d1f71a2f353b56b944a267f3e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---

# Atualização para o AEM 6.5 {#upgrading-to-aem}

Nesta seção, cobrimos a atualização de uma instalação AEM para AEM 6.5:

* [Planejamento da atualização](/help/sites-deploying/upgrade-planning.md)
* [Avaliação da complexidade da atualização com o Detector de padrões](/help/sites-deploying/pattern-detector.md)
* [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)

   <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md)
* [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Tarefas de manutenção de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Execução de uma atualização no local](/help/sites-deploying/in-place-upgrade.md)
* [Verificação e solução de problemas da pós-atualização](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md)
* [Migração de conteúdo ocioso](/help/sites-deploying/lazy-content-migration.md)
* [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Para facilitar a referência aos casos de AEM envolvidos nesses procedimentos, os termos a seguir são usados em todos esses artigos:

* O *source* instância é a instância AEM da qual você está atualizando.
* O *target* é a instância para a qual você está atualizando.

>[!NOTE]
>
>Como parte dos esforços para melhorar a confiabilidade das atualizações, a AEM passou por uma reestruturação abrangente do repositório. Para obter mais informações sobre como se alinhar com a nova estrutura, consulte [Reestruturação do Repositório em AEM.](/help/sites-deploying/repository-restructuring.md)

## O que mudou? {#what-has-changed}

Veja a seguir as principais mudanças observadas nas últimas versões do AEM:

AEM 6.0 apresentou o novo repositório Jackrabbit Oak. Os Managers de Persistência foram substituídos por [Micro Kernels](/help/sites-deploying/platform.md#contentbody_title_4). A partir da versão 6.1, o CRX2 não é mais suportado. Uma ferramenta de migração chamada crx2oak precisa ser executada para migrar repositórios CRX2 de instâncias 5.6.1. Para obter mais informações, consulte [Uso da ferramenta de migração CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Se o Assets Insights for usado e você estiver atualizando de uma versão anterior à AEM 6.2, os ativos deverão ser migrados e ter IDs geradas por meio de um Bean JMX. Em nossos testes internos, 125 mil ativos em um ambiente TarMK foram migrados em uma hora, mas seus resultados podem variar.

6.3 introduziu um novo formato para `SegmentNodeStore`, que é a base da implementação do TarMK. Se estiver atualizando de uma versão anterior à AEM 6.3, isso exigirá uma migração de repositório como parte da atualização, envolvendo tempo de inatividade do sistema.

A Engenharia de Adobe estima que seja em torno de 20 minutos. Observe que a reindexação não será necessária. Além disso, uma nova versão da ferramenta crx2oak foi lançada para funcionar com o novo formato de repositório.

**Essa migração não é necessária se estiver atualizando do AEM 6.3 para o AEM 6.5.**

As tarefas de manutenção de pré-atualização foram otimizadas para oferecer suporte à automação.

As opções de uso da linha de comando da ferramenta crx2oak foram alteradas para serem amigáveis à automação e suportar mais caminhos de atualização.

As verificações pós-atualização também foram amigáveis para automação.

A coleta periódica de lixo de revisões e coleta de lixo do armazenamento de dados agora são tarefas de manutenção de rotina que precisam ser executadas periodicamente. Com a introdução do AEM 6.3, o Adobe suporta e recomenda a Limpeza de Revisão Online. Consulte [Limpeza de Revisão](/help/sites-deploying/revision-cleanup.md) para obter informações sobre como configurar essas tarefas.

AEM apresenta recentemente a [Detector de padrões](/help/sites-deploying/pattern-detector.md) para avaliar a complexidade da atualização conforme você começa a planejar a atualização. 6.5 é também muito importante [compatibilidade com versões anteriores](/help/sites-deploying/backward-compatibility.md) de recursos. Por fim, práticas recomendadas para [atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md) também são adicionadas.

Para obter mais detalhes sobre o que foi alterado em versões recentes do AEM, consulte as notas de versão completas:

* [Notas de versão gerais do Adobe Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/release-notes.html?lang=pt-BR)
* [Notas de versão mais recentes do Adobe Experience Manager 6.5 Service Pack](/help/release-notes/release-notes.md)

## Visão geral da atualização {#upgrade-overview}

Atualizar AEM é um processo de várias etapas, às vezes de vários meses. A seguinte estrutura foi fornecida como uma visão geral do que está incluído em um projeto de atualização e do conteúdo que foi incluído nesta documentação:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Fluxo de atualização {#upgrade-overview-1}

O diagrama abaixo captura o fluxo geral recomendado realce a abordagem de atualização. Observe a referência aos novos recursos que introduzimos. A atualização deve começar com o Detector de padrões (consulte [Avaliação da complexidade da atualização com o Detector de padrões](/help/sites-deploying/pattern-detector.md)) que deve permitir decidir o caminho a ser seguido para compatibilidade com o AEM 6.4 com base nos padrões do relatório gerado.

Havia um grande foco na versão 6.5 para manter todos os novos recursos compatíveis com versões anteriores, mas nos casos em que ainda há alguns problemas de compatibilidade com versões anteriores, o modo de compatibilidade permite adiar temporariamente o desenvolvimento para manter seu código personalizado em conformidade com a versão 6.5. Essa abordagem ajuda você a evitar o esforço de desenvolvimento imediatamente após a atualização (consulte [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Finalmente, em seu ciclo de desenvolvimento 6.5, os recursos introduzidos em Upgrades sustentáveis (consulte [Atualizações sustentáveis](/help/sites-deploying/sustainable-upgrades.md)) ajuda você a seguir as práticas recomendadas para tornar as atualizações futuras ainda mais eficientes e ininterruptas.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
