---
title: Aplicar fluxos de trabalho a páginas de conteúdo
description: Ao criar, é possível invocar fluxos de trabalho para realizar ações em suas páginas. Também é possível aplicar mais de um fluxo de trabalho.
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 53%

---

# Aplicação de fluxos de trabalho a páginas{#applying-workflows-to-pages}

Ao criar, é possível invocar fluxos de trabalho para realizar ações em suas páginas. Também é possível aplicar mais de um fluxo de trabalho.

Ao aplicar o fluxo de trabalho, especifique as seguintes informações:

* O fluxo de trabalho a ser aplicado.
É possível aplicar qualquer fluxo de trabalho (ao qual você tenha acesso, conforme atribuído pelo administrador do AEM).
* Opcionalmente, um título que ajude a identificar a instância do fluxo de trabalho na Caixa de entrada de um usuário.
* A carga do fluxo de trabalho; pode ser uma ou mais páginas.

Os workflows podem ser iniciados de:

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

É possível iniciar um fluxo de trabalho a partir:

* [a opção Criar da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel Linha do tempo do console Sites](#starting-a-workflow-from-the-timeline).

Em ambos os casos, será necessário:

* [Especificar os Detalhes do Fluxo de Trabalho no Assistente de Criação de Fluxo de Trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Iniciar um fluxo de trabalho a partir da barra de ferramentas Sites {#starting-a-workflow-from-the-sites-toolbar}

É possível iniciar um fluxo de trabalho na barra de ferramentas do console do **Sites**:

1. Navegue até página desejada e selecione-a.

1. Na opção **Criar** da barra de ferramentas, você pode agora selecionar **Fluxo de trabalho**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. A variável **Criar fluxo de trabalho** o assistente o ajudará [especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Iniciar um fluxo de trabalho a partir da linha do tempo {#starting-a-workflow-from-the-timeline}

No **Linha do tempo** é possível iniciar um fluxo de trabalho a ser aplicado ao recurso selecionado.

1. [Selecione o recurso](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) e abra a [Linha do tempo](/help/sites-authoring/basic-handling.md#timeline) (ou abra a Linha do tempo e depois selecione o recurso).
1. A ponta da seta no campo de comentário pode ser usada para revelar a opção **Iniciar fluxo de trabalho**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. A variável **Criar fluxo de trabalho** o assistente o ajudará [especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Especificação de Detalhes do Workflow no Assistente de Criação de Workflow {#specifying-workflow-details-in-the-create-workflow-wizard}

A variável **Criar fluxo de trabalho** O assistente o ajudará a selecionar o fluxo de trabalho e especificar os detalhes necessários.

Depois de abrir o **Criar fluxo de trabalho** assistente de:

* [a opção Criar da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel Linha do tempo do console Sites](#starting-a-workflow-from-the-timeline).

Você pode especificar detalhes:

1. No **Propriedades** , as opções básicas do fluxo de trabalho são definidas:

   * **Modelo de fluxo de trabalho**
   * **Título do fluxo de trabalho**

      * Você pode especificar um título para essa instância para ajudá-lo a identificá-la posteriormente.

   Dependendo do modelo de fluxo de trabalho, as seguintes opções também estão disponíveis. Isso permite que o pacote criado como carga seja mantido após a conclusão do fluxo de trabalho.

   * **Manter o pacote do fluxo de trabalho**
   * **Título do pacote**

      * Você pode especificar um título para o pacote, para ajudar na identificação.
   >[!NOTE]
   >
   >A opção **Manter pacote de fluxo de trabalho** estará disponível quando o fluxo de trabalho for configurado para Suporte a vários recursos e vários recursos foram selecionados.[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   Quando terminar, use **Próximo** para prosseguir.

   ![wf-52](assets/wf-52.png)

1. Na etapa **Escopo**, você pode selecionar:

   * **Adicione conteúdo** para abrir o [navegador de caminhos](/help/sites-authoring/author-environment-tools.md#path-browser) e selecionar recursos adicionais. Quando estiver no navegador, clique/toque em **Selecionar** para adicionar o conteúdo à instância do fluxo de trabalho.

   * Um recurso existente para ver ações adicionais:

      * **Incluir filhos** para especificar que os filhos desse recurso serão incluídos no fluxo de trabalho.
Uma caixa de diálogo será aberta, permitindo que você refine a seleção de acordo com:

         * Incluir somente secundárias imediatas.
         * Incluir somente as páginas modificadas.
         * Incluir somente páginas já publicadas.

         Quaisquer filhos especificados são adicionados à lista de recursos aos quais o fluxo de trabalho será aplicado.

      * **Remover seleção** para remover esse recurso do workflow.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Se você adicionar recursos extras, poderá usar **Voltar** para ajustar a configuração **Manter fluxo de trabalho do pacote** na etapa **Propriedades**.

1. Use **Criar** para fechar o assistente e criar a instância do fluxo de trabalho. Uma notificação é exibida no console Sites.

## Iniciar um fluxo de trabalho a partir do editor de páginas {#starting-a-workflow-from-the-page-editor}

Ao editar uma página, você pode selecionar **Informações da página** na barra de ferramentas. O menu suspenso tem a opção **Iniciar em Fluxo de Trabalho**. Isso abrirá uma caixa de diálogo na qual você pode especificar o fluxo de trabalho necessário, juntamente com um título, se necessário:

![wf-54](assets/wf-54.png)
