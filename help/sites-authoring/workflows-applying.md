---
title: Aplicar fluxos de trabalho a páginas de conteúdo
description: Ao criar, é possível invocar fluxos de trabalho para realizar ações em suas páginas. Também é possível aplicar mais de um fluxo de trabalho.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 82%

---

# Aplicação de fluxos de trabalho a páginas{#applying-workflows-to-pages}

Ao criar, é possível invocar fluxos de trabalho para realizar ações em suas páginas. Também é possível aplicar mais de um fluxo de trabalho.

Ao aplicar o fluxo de trabalho, especifique as seguintes informações:

* O fluxo de trabalho a ser aplicado.
É possível aplicar qualquer fluxo de trabalho (ao qual você tenha acesso, conforme atribuído pelo administrador do AEM).
* Opcionalmente, um título que ajude a identificar a instância do fluxo de trabalho na caixa de entrada de um usuário.
* O conteúdo do fluxo de trabalho; pode ser uma ou mais páginas.

Os fluxos de trabalho podem ser iniciados:

* [o console Sites.](#starting-a-workflow-from-the-sites-console)
* [ao editar uma página, em Informações da página](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Consulte também:
>
>* [Como aplicar fluxos de trabalho a ativos do DAM](/help/assets/assets-workflow.md).
>* [Trabalhar com fluxos de trabalho de projeto](/help/sites-authoring/projects-with-workflows.md).
>

>[!NOTE]
>
>Os administradores do AEM podem [iniciar workflows usando vários outros métodos](/help/sites-administering/workflows-starting.md).

## Iniciar um fluxo de trabalho a partir do console Sites {#starting-a-workflow-from-the-sites-console}

Você pode iniciar um fluxo de trabalho usando:

* [a opção Criar da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel Linha do tempo do console Sites](#starting-a-workflow-from-the-timeline).

Em ambos os casos, você deve:

* [Especificar os detalhes do fluxo de trabalho no assistente de criação de fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Iniciar um fluxo de trabalho a partir da barra de ferramentas Sites {#starting-a-workflow-from-the-sites-toolbar}

É possível iniciar um fluxo de trabalho na barra de ferramentas do console do **Sites**:

1. Navegue até página desejada e selecione-a.

1. Na opção **Criar** da barra de ferramentas, você pode agora selecionar **Fluxo de trabalho**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. O assistente **Criar fluxo de trabalho** ajuda [a especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Iniciar um fluxo de trabalho a partir da linha do tempo {#starting-a-workflow-from-the-timeline}

Na **linha do tempo** é possível iniciar um fluxo de trabalho a ser aplicado ao recurso selecionado.

1. [Selecione o recurso](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) e abra a [Linha do tempo](/help/sites-authoring/basic-handling.md#timeline) (ou abra a Linha do tempo e depois selecione o recurso).
1. A ponta da seta no campo de comentário pode ser usada para revelar a opção **Iniciar fluxo de trabalho**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. O assistente **Criar fluxo de trabalho** ajuda [a especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Especificar detalhes do fluxo de trabalho no assistente de criação de fluxo de trabalho {#specifying-workflow-details-in-the-create-workflow-wizard}

O assistente **Criar fluxo de trabalho** ajuda a selecionar o fluxo de trabalho e especificar os detalhes necessários.

Após abrir o assistente **Criar fluxo de trabalho** usando:

* [a opção Criar da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel Linha do tempo do console Sites](#starting-a-workflow-from-the-timeline).

Você pode especificar detalhes:

1. Na etapa **Propriedades**, as opções básicas do fluxo de trabalho são definidas:

   * **Modelo de fluxo de trabalho**
   * **Título do fluxo de trabalho**

      * Você pode especificar um título para essa instância, para ajudar a identificá-la em um estágio posterior.

   Dependendo do modelo de fluxo de trabalho, as seguintes opções também estão disponíveis. Isso permite que o pacote criado como conteúdo seja mantido após a conclusão do fluxo de trabalho.

   * **Manter o pacote do fluxo de trabalho**
   * **Título do pacote**

      * Você pode especificar um título para o pacote, para ajudar na identificação.

   >[!NOTE]
   >
   >A variável **Manter pacote de fluxo de trabalho** estiver disponível quando o fluxo de trabalho tiver sido configurado para [Suporte a vários recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) e vários recursos foram selecionados.

   Quando terminar, use **Próximo** para prosseguir.

   ![wf-52](assets/wf-52.png)

1. Na etapa **Escopo**, você pode selecionar:

   * **Adicionar conteúdo** para abrir o [navegador de caminho](/help/sites-authoring/author-environment-tools.md#path-browser) e selecione recursos adicionais; quando estiver no navegador, clique em **Selecionar** para adicionar o conteúdo à instância do workflow.

   * Um recurso existente para ver ações adicionais:

      * **Incluir filhos** para especificar que os filhos desse recurso serão incluídos no fluxo de trabalho.
Uma caixa de diálogo é aberta, permitindo que você refine a seleção de acordo com:

         * Incluir somente tarefas derivadas imediatas.
         * Incluir somente as páginas modificadas.
         * Incluir somente páginas já publicadas.

        As tarefas derivadas especificadas são adicionadas à lista de recursos aos quais o fluxo de trabalho será aplicado.

      * A opção **Remover seleção** remove o recurso do fluxo de trabalho.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Se você adicionar recursos extras, poderá usar **Voltar** para ajustar a configuração **Manter fluxo de trabalho do pacote** na etapa **Propriedades**.

1. Use **Criar** para fechar o assistente e criar a instância do fluxo de trabalho. Uma notificação é exibida no console Sites.

## Iniciar um fluxo de trabalho a partir do editor de páginas {#starting-a-workflow-from-the-page-editor}

Ao editar uma página, você pode selecionar **Informações da página** na barra de ferramentas. O menu suspenso tem a opção **Iniciar no fluxo de trabalho**. Isso abre uma caixa de diálogo onde é possível especificar o fluxo de trabalho necessário, juntamente com um título, se necessário:

![wf-54](assets/wf-54.png)
