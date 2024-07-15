---
title: Digital Rights Management de ativos
description: Saiba como gerenciar estados de expiração de ativos e informações de ativos licenciados no [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 6%

---

# Digital Rights Management para ativos {#digital-rights-management-in-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=en) |
| AEM 6.5 | Este artigo |

Os ativos digitais são frequentemente associados a uma licença que especifica os termos e a duração do uso. Como o [!DNL Adobe Experience Manager Assets] é totalmente integrado à plataforma [!DNL Experience Manager], você pode gerenciar com eficiência as informações de expiração de ativos e os estados dos ativos. Você também pode associar informações de licenciamento a ativos.

## Expiração do ativo {#asset-expiration}

A expiração de ativos é uma maneira eficaz de aplicar os requisitos de licença para ativos. Ela garante que a publicação do ativo seja cancelada quando expirar, o que evita a possibilidade de qualquer violação de licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualizar o status de expiração de um ativo no console [!DNL Assets] nas exibições de cartão e de lista.

![lista_de_sinalizadores_expirados](assets/expired_flag_list.png)

*Figura: na exibição de lista, a coluna [!UICONTROL Status] exibe o banner [!UICONTROL Expirado].*

Você pode visualizar o status de expiração de um ativo na [!UICONTROL Linha do tempo] no painel esquerdo.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>A data de expiração de um ativo é exibida de forma diferente para usuários em fusos horários diferentes.

Você também pode exibir o status de expiração dos ativos no painel **[!UICONTROL Referências]**. Ele gerencia os status de expiração dos ativos e os relacionamentos entre ativos compostos e subativos, coleções e projetos referenciados.

1. Navegue até o ativo para o qual deseja exibir páginas da Web de referência e ativos compostos.
1. Selecione o ativo e abra **[!UICONTROL Referências]** no painel esquerdo. Para ativos expirados, o painel [!UICONTROL Referências] exibe o status de expiração **[!UICONTROL Ativo expirado]** na parte superior.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Se o ativo tiver subativos expirados, o painel [!UICONTROL Referências] exibirá o status **[!UICONTROL O ativo expirou na subAssets]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Pesquisar ativos expirados {#search-expired-assets}

Você pode pesquisar ativos expirados, incluindo subativos expirados no painel Pesquisar.

1. No console [!DNL Assets], clique em **[!UICONTROL Search]** na barra de ferramentas para exibir a caixa Omnisearch.

1. Com o cursor na caixa Omnisearch, selecione a chave `Enter` para exibir a página de resultados da pesquisa.
1. Abra o painel de pesquisa no painel esquerdo. Clique na opção **[!UICONTROL Status de expiração]** para expandi-la.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Escolha **[!UICONTROL Expirado]**. Somente os ativos expirados são exibidos após a filtragem dos resultados da pesquisa.

Ao escolher a opção **[!UICONTROL Expirado]**, o console [!DNL Assets] exibe somente os ativos e subativos expirados referenciados por ativos compostos. Os ativos compostos que fazem referência aos subativos expirados não são exibidos imediatamente após os subativos expirarem. Em vez disso, eles são exibidos depois que [!DNL Experience Manager] detecta que fazem referência a subativos expirados na próxima vez que o agendador for executado.

Se você modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo do programador atual, o agendamento ainda detectará esse ativo como um ativo expirado na próxima vez que for executado e refletirá seu status de acordo.

Além disso, se uma falha ou erro impedir que o scheduler detecte ativos expirados no ciclo atual, o scheduler reexamina esses ativos no próximo ciclo e detecta seu status expirado.

Para permitir que o console [!DNL Assets] exiba os ativos compostos de referência junto com os ativos secundários expirados, configure um fluxo de trabalho de **[!UICONTROL Notificação de expiração do Adobe CQ DAM]** no Configuration Manager [!DNL Experience Manager].

1. Abra o Configuration Manager [!DNL Experience Manager].
1. Escolha **[!UICONTROL Notificação de expiração do DAM do Adobe CQ]**. Por padrão, o **[!UICONTROL Agendador baseado em tempo]** está selecionado, o que agenda um trabalho para verificar em um momento específico se um ativo expirou subativos. Após a conclusão do trabalho, os ativos que expiraram subativos e os ativos referenciados são exibidos como expirados nos resultados da pesquisa.

1. Para executar o trabalho periodicamente, desmarque o campo **[!UICONTROL Regra do agendador com base na hora]** e modifique o tempo em segundos no campo **[!UICONTROL Agendador periódico]**. Por exemplo, a expressão de exemplo `0 0 0 * * ?` aciona o trabalho às 00 horas.
1. Selecione **[!UICONTROL enviar email]** para receber emails quando um ativo expirar.

   >[!NOTE]
   >
   >Somente o criador do ativo (a pessoa que carrega um ativo específico para [!DNL Assets]) recebe um email quando o ativo expira. Consulte [como configurar notificação por email](/help/sites-administering/notification.md) para obter detalhes adicionais sobre como configurar notificações por email no nível [!DNL Experience Manager] geral.

1. No campo **[!UICONTROL Notificação prévia em segundos]**, especifique o tempo em segundos antes do tempo em que um ativo expira quando você deseja receber uma notificação sobre a expiração. Os criadores de ativos recebem uma mensagem antes da expiração do ativo notificando que o ativo está prestes a expirar após o tempo especificado. Depois que o ativo expirar, você receberá outra notificação que confirma a expiração. Além disso, os ativos expirados são desativados.

1. Clique em **[!UICONTROL Salvar]**.

## Estados do ativo {#asset-states}

O console [!DNL Assets] pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, a exibição de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitado etc.

1. Na interface do usuário do [!DNL Assets], selecione um ativo.
1. Clique em **[!UICONTROL Publish]** na barra de ferramentas. Se você não vir **Publish** na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize a opção **[!UICONTROL Publish]** ![publicar](assets/do-not-localize/publish-globe.png).
1. Escolha **[!UICONTROL Publish]** no menu e feche a caixa de diálogo de confirmação.
1. Saia do modo de seleção. O status de publicação do ativo aparece na parte inferior da miniatura do ativo na exibição de cartão. Na exibição em lista, a coluna Publicado exibe a hora em que o ativo foi publicado.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Para exibir sua página de detalhes do ativo, na interface [!DNL Assets], selecione um ativo e clique em **[!UICONTROL Propriedades]** ![exibir propriedades](assets/do-not-localize/info-circle-icon.png).

1. Na guia [!UICONTROL Avançado], defina uma data de expiração para o ativo no campo **[!UICONTROL Expira]**.

   ![definir data e hora de expiração do ativo no campo Expira](assets/asset-properties-advanced-tab.png)

   *Figura: guia [!UICONTROL Avançado] na página [!UICONTROL Propriedades] do ativo para definir a expiração do ativo.*

1. Clique em **[!UICONTROL Salvar]** e em **[!UICONTROL Fechar]** para exibir o console de Ativos.
1. O status de publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. No console [!DNL Assets], selecione uma pasta e crie uma tarefa de revisão na pasta.
1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluir]**.
1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos aprovados/rejeitados é exibido na parte inferior da exibição de cartão. Na exibição em lista, os status de aprovação e expiração são exibidos nas colunas apropriadas.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para pesquisar ativos com base em seu status, clique em **[!UICONTROL Pesquisar]** ![opção de pesquisa](assets/do-not-localize/search_icon.png) para exibir a barra Omnisearch.
1. Selecione `Return` e clique em [!DNL Experience Manager] para exibir o painel de pesquisa.
1. No painel de pesquisa, clique em **[!UICONTROL Status do Publish]** e selecione **[!UICONTROL Publicado]** para procurar ativos publicados em [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clique em **[!UICONTROL Status de aprovação]** e clique na opção apropriada para procurar ativos aprovados ou rejeitados.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para pesquisar ativos com base no status de expiração, selecione **[!UICONTROL Status de expiração]** no painel Pesquisar e escolha a opção adequada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Também é possível pesquisar ativos com base em uma combinação de status em vários aspectos da pesquisa. Por exemplo, procure por ativos publicados que foram aprovados em uma tarefa de revisão e ainda não expiraram selecionando as opções apropriadas nos aspectos de pesquisa.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

Este recurso impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado do [!DNL Adobe Experience Manager Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Baixar]**, será redirecionado para uma página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a opção **[!UICONTROL Baixar]** não estará disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue para baixar o ativo.

Um ativo é considerado protegido se qualquer uma destas condições for satisfeita:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>O local `/etc/dam/drm/licenses` usado para armazenar licenças em versões anteriores do [!DNL Experience Manager] está obsoleto.
>
>Se você criar ou modificar páginas de licença, ou portá-las de versões anteriores do [!DNL Experience Manager], a Adobe recomenda que você as armazene em `/apps/settings/dam/drm/licenses` ou `/conf/&ast;/settings/dam/drm/licenses`.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na exibição de cartão, selecione os ativos que deseja baixar e clique em **[!UICONTROL Baixar]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No painel [!UICONTROL Licença], escolha **[!UICONTROL Concordar]**. Uma marca de seleção aparece ao lado do ativo. Clique na opção **[!UICONTROL Baixar]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Download]** é habilitada somente quando você opta por concordar com o contrato de licença de um ativo protegido. No entanto, se sua seleção incluir ativos protegidos e desprotegidos, somente os ativos protegidos serão listados no painel e a opção **[!UICONTROL Download]** será habilitada para baixar os ativos desprotegidos. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Baixar]** para baixar o ativo ou suas representações.
