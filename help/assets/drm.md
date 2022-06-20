---
title: Digital Rights Management de ativos
description: Saiba como gerenciar estados de expiração de ativos e informações de ativos licenciados no [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 6%

---

# Digital Rights Management para ativos {#digital-rights-management-in-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/drm.html?lang=en) |

Os ativos digitais geralmente são associados a uma licença que especifica os termos e a duração do uso. Porque [!DNL Adobe Experience Manager Assets] é totalmente integrado ao [!DNL Experience Manager] , você pode gerenciar com eficiência as informações de expiração de ativos e os estados de ativos. Você também pode associar informações de licenciamento a ativos.

## Expiração do ativo {#asset-expiration}

A expiração de ativos é uma maneira eficaz de aplicar requisitos de licença para ativos. Ela garante que o ativo publicado não seja publicado quando expira, o que evita a possibilidade de qualquer violação de licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualizar o status de expiração de um ativo no [!DNL Assets] nas exibições de cartão e lista.

![lista_sinalizador_expirado](assets/expired_flag_list.png)

*Figura: Na exibição em lista, a variável [!UICONTROL Status] exibe a [!UICONTROL Expirado] banner.*

Você pode visualizar o status de expiração de um ativo no [!UICONTROL Linha do tempo] no painel esquerdo.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>A data de expiração de um ativo é exibida de forma diferente para usuários em fusos horários diferentes.

Você também pode visualizar o status de expiração dos ativos na **[!UICONTROL Referências]** trilho. Ele gerencia status de expiração de ativos e relacionamentos entre ativos compostos e subativos, coleções e projetos referenciados.

1. Navegue até o ativo para o qual você deseja exibir as páginas da Web de referência e os ativos compostos.
1. Selecione o ativo e abra **[!UICONTROL Referências]** no painel esquerdo. Para ativos expirados, a variável [!UICONTROL Referências] painel exibe o status de expiração **[!UICONTROL O ativo está expirado]** no topo.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Se o ativo tiver expirado os subativos, a variável [!UICONTROL Referências] painel exibe o status **[!UICONTROL O ativo venceu os subativos]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Pesquisar ativos expirados {#search-expired-assets}

Você pode pesquisar ativos expirados, incluindo subativos expirados no painel Pesquisar .

1. No [!DNL Assets] clique no **[!UICONTROL Pesquisar]** na barra de ferramentas para exibir a caixa Omnisearch .

1. Com o cursor na caixa Omnisearch, selecione o `Enter` para exibir a página de resultados da pesquisa.
1. Abra o painel de pesquisa no painel esquerdo. Clique no botão **[!UICONTROL Status de expiração]** para expandi-la.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Choose **[!UICONTROL Expirado]**. Somente os ativos expirados são exibidos após a filtragem dos resultados da pesquisa.

Ao escolher a variável **[!UICONTROL Expirado]** , a variável [!DNL Assets] O console exibe somente os ativos e subativos expirados referenciados por ativos compostos. Os ativos compostos que fazem referência a subativos expirados não são exibidos imediatamente após a expiração dos subativos. Em vez disso, elas serão exibidas após [!DNL Experience Manager] O detecta que eles fazem referência a subativos expirados na próxima vez que o agendador for executado.

Se você modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo do programador atual, a programação ainda detectará esse ativo como um ativo expirado na próxima vez que ele for executado e refletirá seu status de acordo.

Além disso, se um erro ou falha impedir que o programador detecte ativos expirados no ciclo atual, o programador reexamina esses ativos no próximo ciclo e detecta seu status expirado.

Para ativar o [!DNL Assets] para exibir os ativos compostos de referência junto com os subativos expirados, configure um **[!UICONTROL Notificação de expiração do Adobe CQ DAM]** fluxo de trabalho em [!DNL Experience Manager] Gerenciador de configuração.

1. Abrir [!DNL Experience Manager] Gerenciador de configuração.
1. Choose **[!UICONTROL Notificação de expiração do Adobe CQ DAM]**. Por padrão, **[!UICONTROL Scheduler baseado em tempo]** está selecionada, o que agendará uma tarefa para verificar em um horário específico se um ativo expirou subativos. Após a conclusão do trabalho, os ativos que expiraram os subativos e os ativos referenciados são exibidos como expirados nos resultados da pesquisa.

1. Para executar o trabalho periodicamente, desmarque o campo **[!UICONTROL Regra do agendador com base na hora]** e modifique o tempo em segundos no campo **[!UICONTROL Agendador periódico]**. Por exemplo, a expressão de exemplo `0 0 0 * * ?` aciona o trabalho às 00 horas.
1. Selecionar **[!UICONTROL enviar email]** para receber emails quando um ativo expira.

   >[!NOTE]
   >
   >Somente o criador do ativo (a pessoa que faz upload de um ativo específico para [!DNL Assets]) recebe um email quando o ativo expira. Consulte [como configurar a notificação por email](/help/sites-administering/notification.md) para obter detalhes adicionais sobre como configurar notificações por email no geral [!DNL Experience Manager] nível.

1. No **[!UICONTROL Notificação prévia em segundos]** , especifique o tempo em segundos antes do tempo em que um ativo expira, quando você deseja receber uma notificação sobre a expiração. Os criadores de ativos recebem uma mensagem antes da expiração do ativo notificando que o ativo está prestes a expirar após o tempo especificado. Depois que o ativo expirar, você receberá outra notificação que confirma a expiração. Além disso, os ativos expirados são desativados.

1. Clique em **[!UICONTROL Salvar]**.

## Estados do ativo {#asset-states}

O [!DNL Assets] O console pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, sua exibição de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitado e assim por diante.

1. No [!DNL Assets] interface do usuário, selecione um ativo.
1. Clique em **[!UICONTROL Publicar]** na barra de ferramentas. Se você não vir **Publicar** na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize **[!UICONTROL Publicar]** ![opção de publicação](assets/do-not-localize/publish-globe.png) opção.
1. Choose **[!UICONTROL Publicar]** no menu e feche a caixa de diálogo de confirmação.
1. Sair do modo de seleção. O status da publicação do ativo é exibido na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, a coluna Publicado exibe o horário em que o ativo foi publicado.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Para exibir a página de detalhes do ativo, no [!DNL Assets] selecione um ativo e clique em **[!UICONTROL Propriedades]** ![exibir propriedades](assets/do-not-localize/info-circle-icon.png).

1. No [!UICONTROL Avançado] , defina uma data de expiração para o ativo no **[!UICONTROL Expira]** campo.

   ![definir data e hora de expiração do ativo no campo Expira](assets/asset-properties-advanced-tab.png)

   *Figura: [!UICONTROL Avançado] guia no ativo [!UICONTROL Propriedades] para definir a expiração do ativo.*

1. Clique em **[!UICONTROL Salvar]** e, em seguida, clique em **[!UICONTROL Fechar]** para exibir o console Ativo .
1. O status da publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. No [!DNL Assets] selecione uma pasta e crie uma tarefa de revisão na pasta.
1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluído]**.
1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos que você aprovou/rejeitou é exibido na parte inferior da exibição de cartão. Na exibição em lista, os status de aprovação e expiração são exibidos em colunas apropriadas.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para pesquisar ativos com base em seu status, clique em **[!UICONTROL Pesquisar]** ![opção de pesquisa](assets/do-not-localize/search_icon.png) para exibir a barra Omnisearch.
1. Selecionar `Return` e clique em [!DNL Experience Manager] para exibir o painel de pesquisa.
1. No painel de pesquisa, clique em **[!UICONTROL Publicar status]** e selecione **[!UICONTROL Publicado]** para procurar ativos publicados em [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clique em **[!UICONTROL Status da aprovação]** e clique na opção apropriada para procurar ativos aprovados ou rejeitados.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para pesquisar ativos com base no status de expiração, selecione **[!UICONTROL Status de expiração]** no painel Pesquisar e escolha a opção adequada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Também é possível pesquisar ativos com base em uma combinação de status em vários aspectos de pesquisa. Por exemplo, você pode pesquisar ativos publicados que foram aprovados em uma tarefa de revisão e ainda não expiraram selecionando as opções apropriadas nos aspectos de pesquisa.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

Esse recurso impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado do [!DNL Adobe Experience Manager Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Baixar]**, você é redirecionado para uma página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a variável **[!UICONTROL Baixar]** não está disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue para baixar o ativo.

Um ativo é considerado protegido se qualquer uma dessas condições for satisfeita:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>A localização `/etc/dam/drm/licenses` utilizados para armazenar licenças em versões anteriores de [!DNL Experience Manager] for descontinuado.
>
>Se você criar ou modificar páginas de licença ou as portas das páginas anteriores [!DNL Experience Manager] versões, o Adobe recomenda que você as armazene em `/apps/settings/dam/drm/licenses` ou `/conf/&ast;/settings/dam/drm/licenses`.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na exibição de cartão, selecione os ativos que deseja baixar e clique em **[!UICONTROL Baixar]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No [!UICONTROL Licença] painel, escolha **[!UICONTROL Concordar]**. Uma marca de seleção aparece ao lado do ativo. Clique no botão **[!UICONTROL Baixar]** opção.

   >[!NOTE]
   >
   >O **[!UICONTROL Baixar]** A opção é ativada somente quando você opta por concordar com o contrato de licença de um ativo protegido. No entanto, se sua seleção incluir ativos protegidos e desprotegidos, somente os ativos protegidos serão listados no painel e a variável **[!UICONTROL Baixar]** está ativada para baixar os ativos desprotegidos. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Na caixa de diálogo , clique em **[!UICONTROL Baixar]** para baixar o ativo ou suas representações.
