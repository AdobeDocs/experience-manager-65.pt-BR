---
title: Configurar filas compartilhadas
seo-title: Configurar filas compartilhadas
description: Saiba como usar filas compartilhadas para fluxos de trabalho centrados no Forms no AEM Forms no OSGi.
seo-description: Saiba como usar filas compartilhadas para fluxos de trabalho centrados no Forms no AEM Forms no OSGi.
uuid: null
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: null
docset: aem65
translation-type: tm+mt
source-git-commit: 9a250e739adcf094856f1eafa75de2649d6d3d5f

---


# Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário {#share-and-request-access}

Uma fila é uma lista de itens na Caixa de entrada do AEM de um usuário. Estes podem ser itens atribuídos a um usuário ou itens compartilhados ao grupo do qual um usuário é membro. Você pode acessar sua Caixa de entrada para exibir e executar ações no item Caixa de entrada. Por exemplo, compartilhe um item com outro usuário.

Você também pode compartilhar seus itens da Caixa de entrada com outro usuário. Quando outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá solicitar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso a itens da Caixa de entrada de outros usuários.

## Pré-requisitos {#pre-requisites}

O usuário conectado deve ser membro do `workflow-users` grupo. O usuário pode compartilhar itens ou solicitar acesso aos itens somente dos usuários nos quais o usuário conectado tem permissões de leitura ou somente dos usuários que habilitaram o perfil público.

## Compartilhar um único ou todos os itens da sua caixa de entrada com outro usuário

A Caixa de entrada do AEM permite que você compartilhe um único item ou todos os itens na sua caixa de entrada com outro usuário.

### Compartilhar todos os itens da caixa de entrada

Execute as seguintes etapas para compartilhar todos os itens em uma caixa de entrada com outro usuário:

1. Faça logon na sua instância do AEM. Toque no ícone ![Caixa de entrada](assets/bell.svg) e toque em **[!UICONTROL Exibir tudo]**. Uma lista dos itens da sua caixa de entrada é exibida.
1. Toque no ícone ![Exibir seletor](assets/viewlist.svg) ou Seletor ![de](assets/calendar.svg) visualização ao lado do botão **[!UICONTROL Criar]** e toque em **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra a guia **[!UICONTROL Compartilhar]** na caixa de diálogo de configurações.
1. Digite o nome de um usuário na caixa de texto **[!UICONTROL Conceder acesso aos itens]** da Caixa de entrada e toque em **[!UICONTROL Conceder]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos itens são exibidos na seção **Nome de usuário** .
1. Toque em **[!UICONTROL Salvar]**.

>[!NOTE]
>
> (Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[Permitir que o destinatário compartilhe por meio da opção Compartilhamento](aem-forms-workflow-step-reference.md)**da caixa de entrada da etapa **Atribuir tarefa**no fluxo de trabalho. Somente os itens com a opção mencionada acima ativada são exibidos para outros usuários.

### Compartilhar itens individuais

Execute as seguintes etapas para compartilhar um item da Caixa de entrada com outro usuário:

1. Faça logon na sua instância do AEM. Toque no ícone ![Caixa de entrada](assets/bell.svg) e toque em **[!UICONTROL Exibir tudo]**. Uma lista dos itens da sua caixa de entrada é exibida.
1. Selecione um item e toque em **[!UICONTROL Compartilhar]**. Uma caixa de diálogo é exibida.
1. Digite o nome de um usuário na caixa de texto Adicionar usuários para compartilhar esse item e toque em **[!UICONTROL Adicionar]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos itens são exibidos na seção **[!UICONTROL Nome de usuário]** .
1. Toque em **[!UICONTROL Salvar]**.


>[!NOTE]
>
> (Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[Permitir que o destinatário compartilhe explicitamente na Caixa de entrada](aem-forms-workflow-step-reference.md)**da etapa **Atribuir tarefa**no fluxo de trabalho. Somente os itens com a opção mencionada acima ativada são exibidos para outros usuários.

## Solicitar acesso aos itens da Caixa de entrada {#request-access}

Você pode solicitar acesso aos itens da Caixa de entrada de outro usuário. Depois que o acesso for concedido, você poderá exibir, reivindicar e tomar as ações apropriadas em itens compartilhados. Execute as seguintes etapas para solicitar acesso aos itens da Caixa de entrada de outro usuário:

1. Faça logon na sua instância do AEM. Toque no ícone ![Visualizar seletor](assets/bell.svg) e toque em **[!UICONTROL Visualizar tudo]**.
1. Toque no ícone ![Exibir seletor](assets/viewlist.svg) ou Seletor ![de](assets/calendar.svg) visualização ao lado do botão **[!UICONTROL Criar]** e toque em **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Digite o nome de um usuário na caixa de texto **[!UICONTROL Solicitar acesso aos itens da Caixa de entrada do usuário]** e toque em **[!UICONTROL Solicitar]**. Uma solicitação é enviada ao usuário e o status da solicitação é exibido em relação ao nome do usuário. Repita a etapa para adicionar mais usuários.
1. Toque em **[!UICONTROL Salvar]**. A solicitação é enviada como um item Caixa de entrada para os usuários. O usuário pode selecionar o item e tocar em Aprovar ou Rejeitar para conceder ou rejeitar o acesso.


## Itens de solicitação compartilhados por outros usuários {#claim-items}

Você pode começar a trabalhar em um item compartilhado somente depois de afirmá-lo. Impede que vários usuários trabalhem em um único item. Execute as seguintes etapas para solicitar um item:

1. Faça logon na sua instância do AEM. Toque no ícone Caixa de ![entrada](assets/bell.svg) da caixa de entrada e toque em **[!UICONTROL Exibir tudo]**.
1. Toque no ícone Somente ![](assets/railleft.svg) conteúdo para abrir o seletor de filtro.
1. Toque no menu suspenso **[!UICONTROLSSelecionar destinatário]** para exibir e selecionar os usuários que compartilharam seus itens da Caixa de entrada com você.
1. Selecione um item e toque em **[!UICONTROL Reivindicação]**. O item é adicionado à sua Caixa de entrada.

## Liberar itens solicitados {#release-items}

Você pode trabalhar em um item compartilhado somente depois de reivindicá-lo. Outros usuários não podem ver ou trabalhar em itens que você tenha solicitado. Se não puder continuar trabalhando em um item, você pode liberá-lo de volta ao pool.   Depois de liberar o item, outras pessoas podem reivindicar e trabalhar no item:

Execute as seguintes etapas para liberar um item:

1. Faça logon na sua instância do AEM. Toque no ícone Caixa de ![entrada](assets/bell.svg) da caixa de entrada e toque em **[!UICONTROL Exibir tudo]**. Uma lista dos itens da sua caixa de entrada é exibida.
1. Selecione o item a ser lançado e toque em **[!UICONTROL Cancelar solicitação]**. O item é adicionado de volta ao pool. Outros podem agora reclamar o item.

## Limitações {#limitations}

* Não há suporte para o compartilhamento de itens com um grupo.
* Não há suporte para o compartilhamento de tarefas do projeto.
