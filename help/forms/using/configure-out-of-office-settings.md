---
title: Definir configurações de Fora do Escritório
seo-title: Definir configurações de Fora do Escritório
description: Configurar configurações de Ausência Temporária
seo-description: Definir configurações de Fora do Escritório
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---



# Configuração Configurar Fora do Escritório {#configure-out-of-office-settings}

Se planeja estar fora do escritório, você pode especificar o que acontece com os itens que lhe são atribuídos para esse período.

Você tem a opção de especificar uma data e hora de start e uma data e hora de término para que suas configurações de fora do escritório entrem em vigor. Se você estiver localizado em um fuso horário diferente do servidor, o fuso horário usado será o do cliente.

É possível definir uma pessoa padrão para a qual todos os itens serão enviados. Você também pode especificar exceções para itens de processos específicos a serem enviados para um usuário diferente ou para permanecer em sua Caixa de entrada até retornar. Se a pessoa designada também estiver fora do escritório, o item vai para o usuário que ela designou. Se o item não puder ser atribuído a um usuário que não esteja fora do escritório, ele permanecerá em sua Caixa de entrada.

É possível separar a delegação de itens com base nos modelos de fluxo de trabalho. Por exemplo, você pode atribuir um item relacionado ao Workflow A ao usuário A e atribuir um item relacionado ao Workflow B ao usuário B.


>[!NOTE]
>
>* Quando você ativa a configuração Fora do escritório, todos os itens disponíveis na Caixa de entrada, antes de habilitar a configuração, permanecem na sua caixa de entrada. Somente os itens recebidos após a ativação da configuração são delegados.
>* Quando você desativa a configuração Fora do escritório, os itens delegados não são automaticamente atribuídos a você. Você pode usar a funcionalidade de solicitação para atribuir itens a você.
>* Quando o Usuário A delega itens para o Usuário B e o Usuário B delega ainda mais para o Usuário C, então os itens são atribuídos somente ao Usuário C e não ao Usuário B.
>* Quando há um loop na atribuição, as tarefas permanecem com o usuário original. Por exemplo, quando o Usuário A delega itens ao Usuário B O Usuário B delega ao Usuário C, o Usuário C delega ao Usuário D e o Usuário D delega ao Usuário B, um loop é criado. Nessa situação, o item permanece com o Usuário original. O usuário A é o usuário original no exemplo acima.


## Ative a configuração Fora do escritório para sua conta {#enable-out-of-office}

Execute as seguintes etapas para Ativar a configuração Fora do escritório para sua conta e delegar seus Itens da caixa de entrada a outro usuário:

1. Faça logon na sua instância AEM. Toque no ícone ![Caixa de entrada](assets/bell.svg) e toque em **[!UICONTROL Visualização tudo]**. Uma lista dos itens da caixa de entrada é exibida.
1. Toque no ícone ![Seletor de Visualizações](assets/viewlist.svg) ou ![Seletor de Visualizações](assets/calendar.svg) ao lado do botão **[!UICONTROL Criar]** e toque em **[!UICONTROL Definições]**. A caixa de diálogo de configurações é exibida.
1. Abra a guia **[!UICONTROL Fora do Office]** na caixa de diálogo de configurações.
1. Toque no botão **[!UICONTROL Ativar/Desativar]** para ativar a configuração Fora do Escritório.
1. Especifique **[!UICONTROL Hora do Start]** e **[!UICONTROL Hora de Fim]** para a definição. Os itens são delegados somente durante o período especificado. Deixe o campo **[!UICONTROL Hora Final]** vazio para delegar itens por um período de tempo indefinido.
1. Marque a caixa de seleção **[!UICONTROL Encaminhar meus itens durante esse período]**. Se você não selecionar a opção e não especificar um destinatário, seus itens não serão encaminhados a nenhum usuário. Embora esteja ausente e a configuração esteja ativada, os itens permanecerão em sua Caixa de entrada.
1. Toque em **[!UICONTROL Adicionar destinatário]**. Especifique um usuário no campo **[!UICONTROL Destinatário]** para delegar os itens. Especifique **[!UICONTROL Modelo de Fluxo de Trabalho]** para delegar ao usuário especificado. Você pode selecionar mais de um modelo de fluxo de trabalho.

   Além disso, para atribuir todos os itens, independentemente do modelo de fluxo de trabalho, a um usuário específico, selecione **[!UICONTROL Todos os Workflows]** na lista suspensa Modelo de fluxo de trabalho. <br>

   Para atribuir itens a um usuário específico para todos os modelos de fluxo de trabalho, exceto alguns, selecione **[!UICONTROL Todos os Workflows]** na lista suspensa Modelo de Fluxo de Trabalho, toque em **[!UICONTROL + Adicionar Exceções]** e especifique os modelos de fluxo de trabalho que serão deixados de fora.
   <br>

   Repita a etapa para adicionar mais destinatários. <br>

   >[!NOTE]
   >
   >A ordem dos destinatários é importante. Quando um item é atribuído a um usuário que ativou a configuração de não-escritório, o item é avaliado em relação à lista de destinatários especificados na ordem em que os destinatários são adicionados. Quando um item corresponde aos critérios, ele é atribuído ao destinatário e o destinatário seguinte não está marcado.

1. Toque em **[!UICONTROL Salvar]**. A configuração entra em vigor na data e hora do start especificadas. Se você fizer logon enquanto estiver fora do escritório, não será considerado no escritório até que você altere suas configurações.

Agora, os itens atribuídos a você durante o período Fora do escritório são automaticamente atribuídos ao destinatário especificado.
![Fora do escritório](assets/out-of-office.png)

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **Permitir que o destinatário delegue usando configurações &#39;Fora do Office&#39;** da etapa **Atribuir tarefa** no fluxo de trabalho. Somente os itens com a opção mencionada acima ativada são delegados a outros usuários.

## Limitações           {#limitations}

* Não há suporte para a atribuição de itens a um grupo.
* Atualmente, não há suporte para a ativação de Fora do Escritório para tarefas de projeto.
