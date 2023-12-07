---
title: Configurar filas compartilhadas
description: Saiba como usar filas compartilhadas para fluxos de trabalho centrados no Forms no AEM Forms no OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---

# Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário {#share-and-request-access}

Uma fila é uma lista de itens na Caixa de entrada AEM de um usuário. Eles podem ser itens atribuídos a um usuário ou itens compartilhados com o grupo do qual um usuário é membro. Você pode acessar sua Caixa de entrada para exibir e executar ações no item Caixa de entrada. Por exemplo, compartilhe um item com outro usuário.

Você também pode compartilhar os itens da Caixa de entrada com outro usuário. Depois que outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá solicitar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso aos itens da Caixa de entrada de outros usuários.

## Pré-requisitos {#pre-requisites}

O usuário conectado deve ser membro do `workflow-users` grupo. O usuário pode compartilhar itens ou solicitar acesso aos itens somente aos usuários que o usuário conectado tem permissões de leitura ou somente aos usuários que ativaram o perfil público.

## Compartilhar um único item ou todos os itens da sua caixa de entrada com outro usuário

A caixa de entrada AEM permite compartilhar um único item ou todos os itens da caixa de entrada com outro usuário.

### Compartilhar todos os itens da caixa de entrada

Execute as seguintes etapas para compartilhar todos os itens em uma caixa de entrada com outro usuário:

1. Faça logon na instância do AEM. Selecione o ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione o ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** e selecione **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra o **[!UICONTROL Compartilhar]** na caixa de diálogo de configurações.
1. Insira o nome de um usuário no campo **[!UICONTROL Conceder acesso aos itens da sua Caixa de entrada]** caixa de texto e selecione **[!UICONTROL Conceder]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos seus itens aparecem no **Nome de usuário** seção.
1. Selecione **[!UICONTROL Salvar]**.

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[Permitir que o destinatário compartilhe através do compartilhamento da Caixa de entrada](aem-forms-workflow-step-reference.md)** opção do **Atribuir tarefa** etapa no fluxo de trabalho. Somente os itens que têm a opção acima ativada são exibidos para outros usuários.

### Compartilhar itens individuais

Execute as seguintes etapas para compartilhar um item da Caixa de entrada com outro usuário:

1. Faça logon na instância do AEM. Selecione o ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione um item e selecione **[!UICONTROL Compartilhar]**. Uma caixa de diálogo é exibida.
1. Insira o nome de um usuário na caixa de texto Adicionar usuários para compartilhar este item e selecione **[!UICONTROL Adicionar]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos seus itens aparecem no **[!UICONTROL Nome de usuário]** seção.
1. Selecione **[!UICONTROL Salvar]**.


>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[Permitir que o destinatário compartilhe explicitamente na Caixa de entrada](aem-forms-workflow-step-reference.md)** opção do **Atribuir tarefa** etapa no fluxo de trabalho. Somente os itens que têm a opção acima ativada são exibidos para outros usuários.

## Solicitar acesso aos itens da Caixa de entrada {#request-access}

Você pode solicitar acesso aos itens da Caixa de entrada de outro usuário. Depois que o acesso for concedido, você poderá exibir, reivindicar e tomar as ações apropriadas nos itens compartilhados. Execute as seguintes etapas para solicitar acesso aos itens da Caixa de entrada de outro usuário:

1. Faça logon na instância do AEM. Selecione o ![Exibir seletor](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**.
1. Selecione o ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** e selecione **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Insira o nome de um usuário no campo **[!UICONTROL Solicitar acesso aos itens da Caixa de entrada do usuário]** caixa de texto e selecione **[!UICONTROL Solicitação]**. Uma solicitação é enviada ao usuário e o status da solicitação é exibido em relação ao nome do usuário. Repita a etapa para adicionar mais usuários.
1. Selecionar **[!UICONTROL Salvar]**. A solicitação é enviada como um item da Caixa de entrada para os usuários. O usuário pode selecionar o item e selecionar Aprovar ou Rejeitar para conceder ou rejeitar o acesso.


## Itens de declaração compartilhados por outros usuários {#claim-items}

Você pode começar a trabalhar em um item compartilhado somente depois de reivindicá-lo. Isso impede que vários usuários trabalhem em um único item. Execute as seguintes etapas para reivindicar um item:

1. Faça logon na instância do AEM. Selecione a Caixa de entrada ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**.
1. Selecione o ![Somente conteúdo](assets/railleft.svg) ícone para abrir o seletor de filtros.
1. Selecione o **[!UICONTROL Selecionar responsável]** para visualizar e selecionar os usuários que compartilharam seus itens da Caixa de entrada com você.
1. Selecione um item e selecione **[!UICONTROL Reclamação]**. O item é adicionado à sua Caixa de entrada.

## Liberar itens solicitados {#release-items}

Você pode trabalhar em um item compartilhado somente depois de reivindicá-lo. Outros usuários não podem ver ou trabalhar em itens reivindicados. Se você não puder continuar trabalhando em um item, poderá liberá-lo de volta para o pool.   Depois que você liberar o item, outras pessoas poderão reivindicar e trabalhar no item:

Execute as seguintes etapas para liberar um item:

1. Faça logon na instância do AEM. Selecione a Caixa de entrada ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione o item a ser liberado e selecione **[!UICONTROL Cancelar reclamação]**. O item é adicionado de volta ao pool. Outros agora podem Requerer o item.

## Limitações {#limitations}

* Não há suporte para o compartilhamento de itens com um grupo.
* Não há suporte para o compartilhamento de tarefas de projeto.
