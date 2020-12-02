---
title: Promoção de lançamentos
seo-title: Promoção de lançamentos
description: 'Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. '
seo-description: 'Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. '
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 92%

---


# Promoção de lançamentos{#promoting-launches}

Você precisa promover as páginas de lançamento para retornar o conteúdo à fonte (produção) antes de publicar. Quando uma página de lançamento é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover apenas a página atual ou o lançamento inteiro.
* Promover as páginas-filho da página atual.
* Promover o lançamento completo ou apenas as páginas que foram alteradas.
* Se a inicialização será excluída após ser promovida.

>[!NOTE]
>
>Depois de promover as páginas de lançamento ao destino (**Produção**), é possível ativar as páginas de **Produção** como uma entidade (para tornar o processamento mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-as como carga útil para um fluxo de trabalho que ative um pacote de páginas. É preciso criar o pacote de fluxo de trabalho antes de promover o lançamento. Consulte [Processamento de páginas promovidas usando o fluxo de trabalho do AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção na mesma inicialização ao mesmo tempo podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover inicializações de páginas *modificadas*, as modificações nas ramificações de origem e de inicialização são consideradas.

## Promoção de páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de lançamento quando há somente um nível de inicialização. Consulte:
>
>* [Promover um lançamento aninhado](#promoting-a-nested-launch) quando há mais de um lançamento na estrutura.
>* [Lançamentos - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automática.

>



É possível promover os lançamentos no console de **Sites** ou de **Lançamentos**:

1. Abrir:

   * o console **Sites**:

      1. Abra o painel [referências](/help/sites-authoring/author-environment-tools.md#showingpagereferences) e selecione a página de origem necessária usando [modo de seleção](/help/sites-authoring/basic-handling.md) (ou selecione e abra o painel de referências, a ordem não é importante). Todas as referências serão exibidas.

      1. Selecione **Lançamentos** (por exemplo, Lançamentos [1]) para exibir uma lista de lançamentos específica.
      1. Selecione o lançamento específico para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.
   * o console de **Lançamentos**:

      1. Selecione seu lançamento (toque/clique na miniatura).
      1. Selecione **Promover**.


1. No primeiro Etapa, é possível especificar:

   * **Target**

      * **Excluir inicialização após promoção**
   * **Escopo**

      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   Por exemplo, ao selecionar para promover somente as páginas modificadas:

   ![launch-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Isso abrange um único lançamento, se tiver lançamentos aninhados, consulte[ Promover um lançamento aninhado](#promoting-a-nested-launch).

1. Selecione **Próximo** para continuar.
1. É possível analisar as páginas a serem promovidas e isso dependerá do intervalo de páginas escolhido:

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. Selecione **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de lançamento, a ação **Promover lançamento** também está disponível nas **Informações de página**. Isso abrirá o assistente para coletar as informações necessárias.

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Está disponível para [lançamentos aninhados](#promoting-a-nested-launch) e individuais.

## Promover um lançamento aninhado  {#promoting-a-nested-launch}

Depois de criar uma inicialização aninhada, é possível promovê-la para qualquer uma das origens, incluindo a origem raiz (produção).

![chlimage_1-104](assets/chlimage_1-104.png)

1. Da mesma forma que ao [Criar um lançamento aninhado](#creatinganestedlaunchlaunchwithinalaunch), navegue e selecione o lançamento necessário no console **Lançamentos** ou no painel **Referências**.
1. Selecione **Promover lançamento** para abrir o assistente.

1. Insira os detalhes necessários:

   * **Público alvo**

      * **Destino de promoção** É possível promover para qualquer uma das origens.

      * **Excluir a inicialização após promoção** Após a promoção, a inicialização selecionada e qualquer inicialização aninhada dentro dela será excluída.
   * **Escopo** Aqui é possível promover todo o lançamento ou somente as páginas que foram editadas. Nesse último caso, é possível incluir/excluir as subpáginas. A configuração padrão é promover apenas as alterações da página atual:

      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![chlimage_1-105](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do **Escopo** definido e, possivelmente, das páginas que foram editadas.

1. Suas alterações serão promovidas e refletidas no console de **Lançamentos**:

   ![chlimage_1-107](assets/chlimage_1-107.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para realizar o processamento em massa de páginas de Lançamentos promovidos:

1. Crie um pacote de fluxos de trabalho.
1. Quando os autores promovem páginas de Lançamento, eles as armazenam no pacote de fluxos de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como carga útil.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configure um ativador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um ativador de fluxo de trabalho para iniciar o fluxo de trabalho Solicitar ativação quando o nó do pacote for modificado.

![chlimage_1-108](assets/chlimage_1-108.png)
