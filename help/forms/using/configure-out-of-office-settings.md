---
title: Definir configurações fora do escritório
seo-title: Configure Out of Office settings
description: Configurações de saída do escritório
seo-description: Configure Out of Office settings
exl-id: e4c9d74c-e08d-4675-91f2-4f9fc2f1bcea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Configurar configuração de ausência temporária {#configure-out-of-office-settings}

Se você planeja estar fora do escritório, você pode especificar o que acontece com os itens que são atribuídos a você para esse período.

Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que as configurações de ausência do escritório entrem em vigor. Se você estiver localizado em um fuso horário diferente do servidor, o fuso horário usado será o do cliente.

Você pode definir uma pessoa padrão para a qual todos os itens são enviados. Também é possível especificar exceções para itens de processos específicos que serão enviados a um usuário diferente ou para permanecer em sua Caixa de entrada até que você retorne. Se a pessoa designada também estiver fora do escritório, o item vai para o usuário que ela designou. Se o item não puder ser atribuído a um usuário que não esteja fora do escritório, ele permanecerá na sua Caixa de entrada.

Você pode segregar a delegação de itens com base nos modelos de fluxo de trabalho. Por exemplo, você pode atribuir um item relacionado ao Fluxo de trabalho A ao usuário A e atribuir um item relacionado ao Fluxo de trabalho B é atribuído ao usuário B.


>[!NOTE]
>
>* Quando você ativa a configuração Ausente, todos os itens disponíveis na Caixa de entrada, antes de ativar a configuração, permanecem na sua caixa de entrada. Somente os itens recebidos após a ativação da configuração são delegados.
>* Quando você desativa a configuração Esgotamento, os itens delegados não são automaticamente atribuídos a você. Você pode usar a funcionalidade de solicitação para atribuir itens a você.
>* Quando o Usuário A delega itens ao Usuário B e o Usuário B delega mais ao Usuário C, então os itens são atribuídos somente ao Usuário C e não ao Usuário B.
>* Quando há um loop na atribuição, as tarefas permanecem com o usuário original. Por exemplo, quando o Usuário A delega itens ao Usuário B, o Usuário B delega ao Usuário C, o Usuário C delega ao Usuário D e o Usuário D delega ao Usuário B, um loop é criado. Nessa situação, o item permanece com o Usuário original. O usuário A é o usuário original no exemplo acima.


## Ative a configuração Escritório para sua conta {#enable-out-of-office}

Execute as etapas a seguir para Ativar a configuração Fora do Escritório para sua conta e delegar os Itens da Caixa de Entrada a outro usuário:

1. Faça logon na instância do AEM. Toque no ![Caixa de entrada](assets/bell.svg) ícone e toque **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Toque no ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** botão e toque **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra o **[!UICONTROL Fora do Escritório]** na caixa de diálogo de configurações.
1. Toque no **[!UICONTROL Ativar/Desativar]** para ativar a configuração de ausência temporária.
1. Especifique a **[!UICONTROL Hora de início]**  e **[!UICONTROL Hora de Término]** para a configuração . Os itens são delegados apenas durante o período especificado. Deixe o **[!UICONTROL Hora de Término]** campo vazio para delegar itens por um período indefinido.
1. Selecione o **[!UICONTROL Encaminhar meus itens durante esse período]** caixa de seleção. Se você não selecionar a opção e não especificar um destinatário, os itens não serão encaminhados a nenhum usuário. Embora esteja ausente e a configuração esteja ativada, os itens permanecerão na sua Caixa de entrada.
1. Toque **[!UICONTROL Adicionar Destinatário]**. Especifique um usuário no **[!UICONTROL Destinatário]** campo para delegar os itens. Especifique a **[!UICONTROL Modelo de fluxo de trabalho]** para delegar ao usuário especificado. Você pode selecionar mais de um modelo de fluxo de trabalho.

   Além disso, para atribuir todos os itens, independentemente do modelo de fluxo de trabalho, a um usuário específico, selecione **[!UICONTROL Todos os fluxos de trabalho]** na lista suspensa Modelo de fluxo de trabalho . <br>

   Para atribuir itens a um usuário específico para todos os modelos de fluxo de trabalho, exceto alguns, selecione **[!UICONTROL Todos os fluxos de trabalho]** na lista suspensa Modelo de fluxo de trabalho , toque em **[!UICONTROL + Adicionar Exceções]**e especifique os modelos de fluxo de trabalho que serão deixados de fora.
   <br>

   Repita a etapa para adicionar mais destinatários. <br>

   >[!NOTE]
   >
   >A ordem dos destinatários é importante. Quando um item é atribuído a um usuário que habilitou a configuração de ausência do escritório, o item é avaliado em relação à lista de destinatários especificados na ordem em que os destinatários são adicionados. Quando um item corresponde aos critérios, ele é atribuído ao destinatário e o próximo destinatário não está marcado.

1. Toque **[!UICONTROL Salvar]**. A configuração entrará em vigor na data e hora de início especificadas. Se você fizer logon enquanto estiver fora do escritório, não será considerado no escritório até que você altere suas configurações.

Agora, os itens atribuídos a você durante o período Fora do Escritório são automaticamente atribuídos ao destinatário especificado.
![Fora do escritório](assets/out-of-office.png)

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative o **Permitir que o destinatário delegue usando configurações &#39;Fora do Escritório&#39;** da **Atribuir tarefa** no fluxo de trabalho. Somente os itens que têm a opção acima habilitada são delegados a outros usuários.

## Limitações {#limitations}

* Não há suporte para a atribuição de itens a um grupo.
* Atualmente, não há suporte para habilitar tarefas fora do escritório para tarefas do projeto.
