---
title: Promover lançamentos
description: Promova as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar.
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 21%

---

# Promoção de inicializações{#promoting-launches}

É necessário promover as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de inicialização é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de inicialização:

* Se deve promover somente a página atual ou toda a inicialização.
* Se as páginas secundárias da página atual devem ser promovidas.
* Se deve promover a inicialização completa ou somente as páginas que foram alteradas.
* Se o lançamento deve ser excluído após ser promovido.

>[!NOTE]
>
>Depois de promover as páginas de inicialização ao target (**Produção**), você pode ativar a variável **Produção** páginas como uma entidade (para tornar o processo mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-o como a carga de um fluxo de trabalho que ativa um pacote de páginas. É necessário criar o pacote de workflow antes de promover a inicialização. Consulte [Processamento de páginas promovidas usando o fluxo de trabalho do AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção simultâneas em uma mesma inicialização podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover inicializações para *modificado* páginas, modificações nas ramificações de origem e de inicialização são consideradas.

## Promover páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de inicialização quando há apenas um nível de inicialização. Consulte:
>
>* [Promover uma inicialização aninhada](#promoting-a-nested-launch) quando houver mais de uma inicialização na estrutura.
>* [Inicializações - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automáticas.
>

É possível promover inicializações a partir do **Sites** console ou o **Lançamentos** console:

1. Abrir:

   * o **Sites** console:

      1. Abra o [painel de referências](/help/sites-authoring/author-environment-tools.md#showingpagereferences) e selecione a página de origem desejada usando o [modo de seleção](/help/sites-authoring/basic-handling.md) (ou selecione e abra o painel de referências; a ordem não é importante). Todas as referências serão exibidas.

      1. Selecione **Lançamentos** (por exemplo, Lançamentos [1]) para exibir uma lista de lançamentos específica.
      1. Selecione a inicialização específica para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.

   * o **Lançamentos** console:

      1. Selecione o seu lançamento (toque/clique na miniatura).
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
   >Isso abrange uma única inicialização, se você tiver inicializações aninhadas, consulte [Promover uma inicialização aninhada](#promoting-a-nested-launch).

1. Selecionar **Próxima** para continuar.
1. É possível revisar as páginas a serem promovidas, isso dependerá do intervalo de páginas escolhido:

   ![Revisar páginas a serem promovidas](assets/chlimage_1-102.png)

1. Selecionar **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de inicialização, a variável **Promover lançamento** a ação também está disponível em **Informações da página**. Isso abrirá o assistente para coletar as informações necessárias.

![Promover lançamento](assets/chlimage_1-103.png)

>[!NOTE]
>
>Ele está disponível para single e [inicializações aninhadas](#promoting-a-nested-launch).

## Promover uma inicialização aninhada {#promoting-a-nested-launch}

Depois de criar uma inicialização aninhada, você pode promovê-la de volta para qualquer uma das origens, incluindo a origem raiz (produção).

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
Aqui é possível promover toda a inicialização ou somente as páginas que foram editadas. No último caso, você pode optar por incluir/excluir subpáginas. A configuração padrão é promover alterações de página somente para a página atual:

      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   ![Configurações para promover um lançamento](assets/chlimage_1-105.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![Revisar detalhes e Promover](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do tipo de **Escopo** e possivelmente as páginas que foram editadas.

1. Suas alterações serão promovidas e refletidas no **Lançamentos** console:

   ![Iniciar console](assets/chlimage_1-107.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Usar modelos de fluxo de trabalho para executar o processamento em massa das páginas de inicializações promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando os autores promovem as páginas do Launch, eles as armazenam no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como a carga.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, [configurar um inicializador de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) para o nó do pacote.

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Ativação de solicitação quando o nó do pacote for modificado.

![Iniciador do fluxo de trabalho](assets/chlimage_1-108.png)
