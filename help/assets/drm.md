---
title: Digital Rights Management de ativos
description: Saiba como gerenciar estados de expiração de ativos e informações para ativos licenciados em [!DNL Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 6%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

Os ativos digitais geralmente são associados a uma licença que especifica os termos e a duração do uso. Como [!DNL Adobe Experience Manager Assets] está totalmente integrado à [!DNL Experience Manager] plataforma, você pode gerenciar com eficiência as informações de expiração de ativos e os estados de ativos. Também é possível associar informações de licenciamento a ativos.

## Expiração do ativo {#asset-expiration}

A expiração do ativo é uma maneira eficaz de aplicar os requisitos de licença para ativos. Ela garante que o ativo publicado não seja publicado quando expirar, o que evita a possibilidade de qualquer violação de licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualização o status de expiração de um ativo no [!DNL Assets] console nas visualizações de cartão e lista.

![expired_flag_card](assets/expired_flag_card.png)

*Figura: Na visualização do cartão, um sinalizador no cartão indica o ativo expirado.*

![expired_flag_lista](assets/expired_flag_list.png)

*Figura: Na visualização da lista, a coluna[!UICONTROL Status]exibe o banner[!UICONTROL Expirado].*

Você pode visualização o status de expiração de um ativo na [!UICONTROL Linha do tempo] no painel esquerdo.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>A data de expiração de um ativo é exibida de forma diferente para usuários em fusos horários diferentes.

Você também pode visualização o status de expiração dos ativos no painel **[!UICONTROL Referências]** . Ele gerencia os status e as relações de expiração de ativos entre ativos compostos e subativos, coleções e projetos referenciados.

1. Navegue até o ativo para o qual você deseja visualização as páginas da Web e os ativos compostos.
1. Selecione o ativo e clique no [!DNL Experience Manager] logotipo.

1. Escolha **[!UICONTROL Referências]** no menu.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   Para ativos expirados, o painel Referências exibe o status de expiração **[!UICONTROL Ativo expirado]** na parte superior.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Se o ativo tiver subativos expirados, o painel Referências exibirá o status **[!UICONTROL Ativo tiver subativos]** expirados.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Pesquisar ativos expirados {#search-expired-assets}

Você pode pesquisar ativos expirados, incluindo subativos expirados no painel Pesquisar.

1. No [!DNL Assets] console, clique em **[!UICONTROL Pesquisar]** na barra de ferramentas para exibir a caixa Omnisearch.

1. Com o cursor na caixa Omnisearch, pressione a tecla Enter para exibir a página de resultados da pesquisa.

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. Clique no [!DNL Experience Manager] logotipo para exibir o painel de pesquisa.
1. Click the **[!UICONTROL Expiry Status]** option to expand it.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Escolha **[!UICONTROL Expirado]**. Os ativos expirados são exibidos nos resultados da pesquisa.

   ![chlimage_1-153](assets/chlimage_1-153.png)

Quando você escolhe a opção **[!UICONTROL Expirado]** , o [!DNL Assets] console exibe apenas os ativos e subativos expirados que são referenciados pelos ativos compostos. Os ativos compostos que fazem referência a subativos expirados não são exibidos imediatamente após a expiração dos subativos. Em vez disso, eles são exibidos após [!DNL Experience Manager] detectar que fazem referência a subativos expirados na próxima vez que o scheduler for executado.

Se você modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo de scheduleres atual, a programação ainda detectará esse ativo como um ativo expirado na próxima vez que ele for executado e refletirá seu status de acordo.

Além disso, se uma falha ou erro impedir que o scheduler detecte ativos expirados no ciclo atual, o scheduler examinará novamente esses ativos no ciclo seguinte e detectará seu status expirado.

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. Abra o [!DNL Experience Manager] Configuration Manager.
1. Escolha Notificação **[!UICONTROL de expiração do]** Adobe CQ DAM. Por padrão, o Scheduler **[!UICONTROL com base em]** tempo é selecionado, o que agenda uma tarefa para verificar em um horário específico se um ativo expirou subativos. Após a conclusão da tarefa, os ativos que têm subativos expirados e ativos referenciados são exibidos como expirados nos resultados da pesquisa.

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. Para executar o trabalho periodicamente, desmarque o campo **[!UICONTROL Regra do agendador com base na hora]** e modifique o tempo em segundos no campo **[!UICONTROL Agendador periódico]**. Por exemplo, a expressão de exemplo &#39;0 0 0 &amp;ast; &amp;ast; ?&#39; aciona o trabalho às 00 horas.
1. Selecione **[!UICONTROL enviar e-mail]** para receber e-mails quando um ativo expirar.

   >[!NOTE]
   >
   >Somente o criador do ativo (a pessoa para a qual o upload de um ativo específico é feito) recebe um email quando o ativo expira. [!DNL Assets] Consulte [como configurar a notificação](/help/sites-administering/notification.md) por email para obter mais detalhes sobre como configurar notificações por email no [!DNL Experience Manager] nível geral.

1. No campo Notificação **[!UICONTROL anterior em segundos]** , especifique o tempo em segundos antes do momento em que um ativo expira quando você deseja receber uma notificação sobre a expiração. Os criadores de ativos recebem uma mensagem antes da expiração do ativo notificando que o ativo está prestes a expirar após o tempo especificado. Depois que o ativo expirar, você receberá outra notificação que confirmará a expiração. Além disso, os ativos expirados são desativados.

1. Clique em **[!UICONTROL Salvar]**.

## Estados do ativo {#asset-states}

O [!DNL Assets] console pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, sua visualização de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitada e assim por diante.

1. Na interface do [!DNL Assets] usuário, selecione um ativo.

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. Click **[!UICONTROL Publish]** from the toolbar. Se você não vir **Publicar** na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize a opção **[!UICONTROL Publicar]** ![publicação](assets/do-not-localize/publish-globe.png) .
1. Escolha **[!UICONTROL Publicar]** no menu e feche a caixa de diálogo de confirmação.
1. Saia do modo de seleção. O status de publicação do ativo aparece na parte inferior da miniatura do ativo na visualização do cartão. Na visualização da lista, a coluna Publicado exibe a hora em que o ativo foi publicado.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Para exibir a página de detalhes do ativo, na [!DNL Assets] interface, selecione um ativo e clique em Propriedades **[!UICONTROL das propriedades]** de ![](assets/do-not-localize/info-circle-icon.png)visualização.

1. Na guia [!UICONTROL Avançado] , defina uma data de expiração para o ativo no campo **[!UICONTROL Expira]** .

   ![definir data e hora de expiração do ativo no campo Expira](assets/asset-properties-advanced-tab.png)

   *Figura:[!UICONTROL Guia Avançado]na página[!UICONTROL Propriedades]do ativo para definir a expiração do ativo.*

1. Clique em **[!UICONTROL Salvar]** e em **[!UICONTROL Fechar]** para exibir o console Ativos.
1. O status de publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na visualização do cartão. Na visualização da lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. No [!DNL Assets] console, selecione uma pasta e crie uma tarefa de revisão na pasta.
1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluir]**.
1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos que você aprovou/rejeita é exibido na parte inferior da visualização do cartão. Na visualização da lista, os status de aprovação e expiração são exibidos em colunas apropriadas.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para pesquisar ativos com base em seu status, clique na opção **** Pesquisar ![](assets/do-not-localize/search_icon.png) pesquisa para exibir a barra Omnisearch.
1. Pressione return (Retornar) e clique [!DNL Experience Manager] para exibir o painel de pesquisa.
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para pesquisar ativos com base no status de expiração, selecione **[!UICONTROL Status de expiração]** no painel Pesquisar e escolha a opção adequada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Você também pode pesquisar ativos com base em uma combinação de status em várias facetas de pesquisa. Por exemplo, você pode pesquisar ativos publicados que foram aprovados em uma tarefa de revisão e ainda não expiraram selecionando as opções apropriadas nas facetas de pesquisa.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

Este recurso impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado de [!DNL Adobe Experience Manager Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Download]**, será redirecionado para a página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a opção **[!UICONTROL Download]** não estará disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue com o download do ativo.

Um ativo é considerado protegido se uma dessas condições for cumprida:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>O local `/etc/dam/drm/licenses` usado para armazenar licenças em versões anteriores de [!DNL Experience Manager] está obsoleto.
>
>Se você criar ou modificar páginas de licença ou as portar de [!DNL Experience Manager] versões anteriores, o Adobe recomenda armazená-las em `/apps/settings/dam/drm/licenses` ou `/conf/&ast;/settings/dam/drm/licenses`.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na visualização do cartão, selecione os ativos que deseja baixar e clique em **[!UICONTROL Download]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No painel [!UICONTROL Licença] , escolha **[!UICONTROL Concordar]**. Uma marca de seleção é exibida ao lado do ativo. Clique na opção **[!UICONTROL Download]** .

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Download]** para baixar o ativo ou suas representações.
