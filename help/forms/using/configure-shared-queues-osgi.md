---
title: Configurar filas compartilhadas
seo-title: Configure shared queues
description: Saiba como usar filas compartilhadas para fluxos de trabalho centrados no Forms no AEM Forms no OSGi.
seo-description: Learn how to use shared queues for Forms-centric workflows on AEM Forms on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# Compartilhar e solicitar acesso aos itens da Caixa de entrada de um usuário {#share-and-request-access}

Uma fila é uma lista de itens AEM Caixa de entrada de um usuário. Estes podem ser itens atribuídos a um usuário ou itens compartilhados com o grupo do qual um usuário é membro. Você pode acessar a Caixa de entrada para visualizar e executar ações no item da Caixa de entrada. Por exemplo, compartilhe um item com outro usuário.

Também é possível compartilhar os itens da Caixa de entrada com outro usuário. Assim que outro usuário tiver acesso aos itens da Caixa de entrada, ele poderá reivindicar e tomar as medidas apropriadas nos itens compartilhados. Da mesma forma, você pode solicitar acesso aos itens da Caixa de entrada de outros usuários.

## Pré-requisitos {#pre-requisites}

O usuário conectado deve ser membro do `workflow-users` grupo. O usuário pode compartilhar itens ou solicitar acesso aos itens somente dos usuários em que o usuário conectado tem permissões de leitura ou somente dos usuários que ativaram o perfil público.

## Compartilhar um único ou todos os itens da sua caixa de entrada com outro usuário

AEM Caixa de entrada permite compartilhar um único ou todos os itens em sua caixa de entrada com outro usuário.

### Compartilhar todos os itens da caixa de entrada

Execute as seguintes etapas para compartilhar todos os itens em uma caixa de entrada com outro usuário:

1. Faça logon na instância do AEM. Toque no ![Caixa de entrada](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Toque no ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** botão e toque **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra o **[!UICONTROL Compartilhar]** na caixa de diálogo de configurações.
1. Insira o nome de um usuário no **[!UICONTROL Conceder acesso aos itens da Caixa de entrada]** caixa de texto e toque em **[!UICONTROL Subvenção]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos itens são exibidos na guia **Nome do usuário** seção.
1. Toque **[!UICONTROL Salvar]**.

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative o **[Permitir que o destinatário compartilhe via Compartilhamento da Caixa de entrada](aem-forms-workflow-step-reference.md)** da **Atribuir tarefa** no fluxo de trabalho. Somente os itens que têm a opção mencionada acima ativada são exibidos para outros usuários.

### Compartilhar itens individuais

Execute as seguintes etapas para compartilhar um item da Caixa de entrada com outro usuário:

1. Faça logon na instância do AEM. Toque no ![Caixa de entrada](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecionar um item e tocar em **[!UICONTROL Compartilhar]**. Uma caixa de diálogo é exibida.
1. Insira o nome de um usuário na caixa de texto Adicionar usuários para compartilhar este item e toque em **[!UICONTROL Adicionar]**. Repita a etapa para adicionar mais usuários. Todos os usuários com acesso aos itens são exibidos na guia **[!UICONTROL Nome do usuário]** seção.
1. Toque **[!UICONTROL Salvar]**.


>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative o **[Permitir que o destinatário compartilhe explicitamente na Caixa de entrada](aem-forms-workflow-step-reference.md)** da **Atribuir tarefa** no fluxo de trabalho. Somente os itens que têm a opção mencionada acima ativada são exibidos para outros usuários.

## Solicitar acesso aos itens da Caixa de entrada {#request-access}

Você pode solicitar acesso aos itens da Caixa de entrada de outro usuário. Depois que o acesso for concedido, você poderá visualizar, reivindicar e tomar as ações apropriadas em itens compartilhados. Execute as seguintes etapas para solicitar acesso aos itens da Caixa de entrada de outro usuário:

1. Faça logon na instância do AEM. Toque no ![Exibir seletor](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**.
1. Toque no ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** botão e toque **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Insira o nome de um usuário no **[!UICONTROL Solicitar acesso aos itens da Caixa de entrada do usuário]** caixa de texto e toque em **[!UICONTROL Solicitação]**. Uma solicitação é enviada ao usuário e o status da solicitação é exibido em relação ao nome do usuário. Repita a etapa para adicionar mais usuários.
1. Toque **[!UICONTROL Salvar]**. A solicitação é enviada como um item da Caixa de entrada para os usuários. O usuário pode selecionar o item e tocar em Aprovar ou Rejeitar para conceder ou rejeitar o acesso.


## Itens de solicitação compartilhados por outros usuários {#claim-items}

Você pode começar a trabalhar em um item compartilhado somente depois de reivindicá-lo. Impede que vários usuários trabalhem em um único item. Execute as seguintes etapas para reivindicar um item:

1. Faça logon na instância do AEM. Toque na Caixa de entrada ![Caixa de entrada](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**.
1. Toque no ![Somente conteúdo](assets/railleft.svg) ícone para abrir o seletor de filtro.
1. Toque no **[!UICONTROL Selecionar Destinatário]** para exibir e selecionar usuários que compartilharam seus itens da Caixa de entrada com você.
1. Selecionar um item e tocar em **[!UICONTROL Reclamação]**. O item é adicionado à sua Caixa de entrada.

## Liberar itens reclamados {#release-items}

Você pode trabalhar em um item compartilhado somente depois de reivindicá-lo. Outros usuários não podem ver ou trabalhar em itens que você solicitou. Se não puder continuar trabalhando em um item, você poderá liberá-lo de volta ao pool.   Depois de liberar o item, outras pessoas podem reivindicar e trabalhar no item:

Execute as seguintes etapas para liberar um item:

1. Faça logon na instância do AEM. Toque na Caixa de entrada ![Caixa de entrada](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione o item a ser lançado e toque em **[!UICONTROL Cancelar solicitação]**. O item é adicionado de volta ao pool. Outros podem agora reclamar o item.

## Limitações {#limitations}

* O compartilhamento de itens com um grupo não é suportado.
* Não há suporte para o compartilhamento de tarefas do projeto.
