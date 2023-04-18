---
title: Promover inicializações
description: Você promove páginas de lançamento para mover o conteúdo de volta para a fonte (produção) antes de publicar.
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 19%

---

# Promoção de inicializações{#promoting-launches}

É necessário promover páginas de lançamento para mover o conteúdo de volta para a fonte (produção) antes de publicar. Quando uma página de lançamento é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover apenas a página atual ou todo o lançamento.
* Promover as páginas secundárias da página atual.
* Promover o lançamento completo ou apenas as páginas que foram alteradas.
* Se o lançamento deve ser excluído após a promoção.

>[!NOTE]
>
>Depois de promover as páginas de lançamento ao destino (**Produção**), você pode ativar o **Produção** páginas como uma entidade (para tornar o processo mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-as como carga útil para um fluxo de trabalho que ativa um pacote de páginas. É necessário criar o pacote de fluxo de trabalho antes de promover o lançamento. Consulte [Processamento de Páginas promovidas usando AEM fluxo de trabalho](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção simultâneas em uma mesma inicialização podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover inicializações de *modificados* páginas, modificações nas ramificações de origem e de lançamento são consideradas.

## Promoção de páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de lançamento quando há apenas um nível de lançamento. Consulte:
>
>* [Promover um lançamento aninhado](#promoting-a-nested-launch) quando houver mais de um lançamento na estrutura.
>* [Lançamentos - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automática.
>


É possível promover inicializações do **Sites** ou o **Lançamentos** console:

1. Abrir:

   * o **Sites** console:

      1. Abra o [painel de referências](/help/sites-authoring/author-environment-tools.md#showingpagereferences) e selecione a página de origem desejada usando o [modo de seleção](/help/sites-authoring/basic-handling.md) (ou selecione e abra o painel de referências; a ordem não é importante). Todas as referências serão exibidas.

      1. Selecionar **Lançamentos** (por exemplo, Lançamentos (1)) para mostrar uma lista de lançamentos específica.
      1. Selecione o lançamento específico para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.
   * o **Lançamentos** console:

      1. Selecione o lançamento (toque/clique na miniatura).
      1. Selecionar **Promover**.


1. Na primeira etapa, é possível especificar:

   * **Target**

      * **Excluir inicialização após promoção**
   * **Escopo**

      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   Por exemplo, ao selecionar para promover somente as páginas modificadas:

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Isso abrange uma única inicialização, se você tiver lançamentos aninhados, consulte [Promover um lançamento aninhado](#promoting-a-nested-launch).

1. Selecionar **Próximo** para continuar.
1. É possível revisar as páginas a serem promovidas e isso dependerá do intervalo de páginas escolhido:

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. Selecionar **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de lançamento, a variável **Promover lançamento** a ação também está disponível em **Informações da página**. Isso abrirá o assistente para coletar as informações necessárias.

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Isso está disponível para único e único [lançamentos aninhados](#promoting-a-nested-launch).

## Promover um lançamento aninhado {#promoting-a-nested-launch}

Depois de criar um lançamento aninhado, você pode promovê-lo de volta a qualquer uma das fontes, incluindo a fonte raiz (produção).

![chlimage_1-104](assets/chlimage_1-104.png)

1. Como com [Criação de um lançamento aninhado](#creatinganestedlaunchlaunchwithinalaunch), navegue e selecione a inicialização necessária na **Lançamentos** ou o **Referências** trilho.
1. Selecione **Promover lançamento** para abrir o assistente.

1. Insira os detalhes necessários:

   * **Target**

      * **Meta de promoção**
É possível promover para qualquer uma das fontes.

      * **Excluir inicialização após promoção**
Após a promoção, o lançamento selecionado e todas as inicializações aninhadas dentro dele serão excluídos.
   * **Escopo**
Aqui, você pode escolher se deseja promover todo o lançamento ou somente as páginas que foram editadas. Se as últimas, você pode selecionar para incluir/excluir subpáginas. A configuração padrão é promover apenas as alterações de página da página atual:

      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![chlimage_1-106](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do **Escopo** definido e possivelmente as páginas que foram editadas.

1. Suas alterações serão promovidas e refletidas na função **Lançamentos** console:

   ![chlimage_1-107](assets/chlimage_1-107.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para executar o processamento em massa de páginas de Lançamentos promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando os autores promovem páginas do Launch, eles as armazenam no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como carga útil.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configurar um iniciador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Request Ativation quando o nó do pacote for modificado.

![chlimage_1-108](assets/chlimage_1-108.png)
