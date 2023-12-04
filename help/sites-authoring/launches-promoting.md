---
title: Promover lançamentos
description: Promova as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 76%

---

# Promoção de inicializações{#promoting-launches}

É necessário promover as páginas de lançamento para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de lançamento é promovida, a página de origem correspondente é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover somente a página atual ou todo o lançamento.
* Promover as páginas secundárias da página atual.
* Promover o lançamento completo ou somente as páginas alteradas.
* Excluir o lançamento após promovê-lo.

>[!NOTE]
>
>Após promover as páginas de lançamento para o destino (**Produção**), você pode ativar as páginas de **produção** como uma entidade (para tornar o processo mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-o como o conteúdo de um fluxo de trabalho que ativa um pacote de páginas. É necessário criar o pacote de fluxo de trabalho antes de promover o lançamento. Consulte [Processamento de páginas promovidas usando o fluxo de trabalho do AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção simultâneas em uma mesma inicialização podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover lançamentos para páginas *modificadas*, as modificações nas ramificações de origem e de lançamento são consideradas.

## Promover páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de lançamento quando há apenas um nível de lançamento. Consulte:
>
>* [Promover um lançamento aninhado](#promoting-a-nested-launch), quando houver mais de um lançamento na estrutura.
>* [Lançamentos - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automáticas.
>

É possível promover lançamentos a partir do console **Sites** ou do console **Lançamentos**:

1. Abrir:

   * o **Sites** console:

      1. Abra o [painel de referências](/help/sites-authoring/author-environment-tools.md#showingpagereferences) e selecione a página de origem desejada usando o [modo de seleção](/help/sites-authoring/basic-handling.md) (ou selecione e abra o painel de referências; a ordem não é importante). Todas as referências são mostradas.

      1. Selecione **Lançamentos** (por exemplo, Lançamentos [1]) para exibir uma lista de lançamentos específica.
      1. Selecione um lançamento específico para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.

   * o **Lançamentos** console:

      1. Selecione o seu lançamento (clique na miniatura).
      1. Selecione **Promover**.

1. Na primeira etapa, é possível especificar:

   * **Target**

      * **Excluir lançamento após a promoção**

   * **Escopo**

      * **Promover lançamento completo**
      * **Promover as páginas modificadas**
      * **Promover a página atual**
      * **Promover página atual e subpáginas**

   Por exemplo, ao selecionar para promover somente as páginas modificadas:

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Isso abrange um único lançamento, se você tiver lançamentos aninhados, consulte [Promover um lançamento aninhado](#promoting-a-nested-launch).

1. Selecione **Próximo** para continuar.
1. É possível revisar as páginas a serem promovidas, isso dependerá do intervalo de páginas escolhido:

   ![Revisar páginas a serem promovidas](assets/chlimage_1-102.png)

1. Selecione **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de lançamento, a ação **Promover lançamento** também está disponível em **Informações da página**. Isso abre o assistente para coletar as informações necessárias.

![Promover lançamento](assets/chlimage_1-103.png)

>[!NOTE]
>
>Está disponível para [lançamentos aninhados](#promoting-a-nested-launch) e individuais.

## Promover um lançamento aninhado {#promoting-a-nested-launch}

Após criar um lançamento aninhado, você pode promovê-lo de volta para qualquer uma das origens, incluindo a raiz (produção).

![Visão geral da promoção de uma inicialização aninhada](assets/chlimage_1-104.png)

1. Assim como com [Criação de uma inicialização aninhada](#creatinganestedlaunchlaunchwithinalaunch), navegue até o lançamento necessário e selecione-o no **Lançamentos** console ou o **Referências** ferroviário.
1. Selecione **Promover lançamento** para abrir o assistente.

1. Insira os detalhes necessários:

   * **Target**

      * **Destino de promoção**
É possível promover para qualquer uma das origens.

      * **Excluir inicialização após promoção**
Após a promoção, a inicialização selecionada e qualquer inicialização aninhada dentro dela será excluída.

   * **Escopo**
Aqui é possível promover toda a inicialização ou somente as páginas que foram editadas. Neste último caso, você pode optar por incluir/excluir subpáginas. A configuração padrão é promover alterações de página somente para a página atual:

      * **Promover lançamento completo**
      * **Promover as páginas modificadas**
      * **Promover a página atual**
      * **Promover página atual e subpáginas**

   ![Configurações para promover um lançamento](assets/chlimage_1-105.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![Revisar detalhes e Promover](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do tipo de **escopo** definido e, possivelmente, das páginas editadas.

1. Suas alterações serão promovidas e refletidas no **Lançamentos** console:

   ![Iniciar console](assets/chlimage_1-107.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para executar o processamento em massa das páginas de lançamento promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando autores(as) promovem as páginas de lançamento, elas são armazenadas no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como o conteúdo.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configurar um inicializador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar solicitações de ativação de página automaticamente quando autores(as) promoverem páginas de lançamento. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Solicitar ativação quando o nó do pacote for modificado.

![Iniciador do fluxo de trabalho](assets/chlimage_1-108.png)
