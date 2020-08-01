---
title: Gerar um URL para ativos compartilhados
description: Este artigo descreve como compartilhar ativos, pastas e coleções [!DNL Experience Manager Assets] com um URL para terceiros externos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 6%

---


# Compartilhar ativos por meio de um link {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] permite que você compartilhe ativos, pastas e coleções como um URL com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon [!DNL Assets].

>[!NOTE]
>
>Você precisa da permissão Editar ACL na pasta ou no ativo que deseja compartilhar como um link.

## Compartilhar ativos {#sharelink}

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem visualização os links compartilhados com eles.

>[!NOTE]
>
>Antes de compartilhar um link com os usuários, verifique se o Day CQ Mail Service está configurado. Ocorre um erro se você tentar compartilhar um link sem primeiro [configurar o Serviço](/help/assets/link-sharing.md#configmailservice)de e-mail Day CQ.

1. Na interface do [!DNL Assets] usuário, selecione o ativo a ser compartilhado como um link.
1. Na barra de ferramentas, clique no ícone **[!UICONTROL Compartilhar ativos do Link]** ![](assets/do-not-localize/assets_share.png)Compartilhar.

   Um link de ativo é criado automaticamente no campo **[!UICONTROL Compartilhar link]** . Copie este link e compartilhe-o com os usuários. A hora de expiração padrão do link é um dia.

   ![Diálogo com o compartilhamento de links](assets/Link-sharing-dialog-box.png)

   *Figura: A caixa de diálogo para compartilhar ativos como um link.*

   Como alternativa, prossiga para executar as etapas 3 a 7 desse procedimento para adicionar recipient de e-mail, configurar o tempo de expiração do link e enviá-lo da caixa de diálogo.

   >[!NOTE]
   >
   >Se você quiser compartilhar links da implantação do [!DNL Experience Manager] Autor para entidades externas, certifique-se de apenas expor os seguintes URLs (que são usados para compartilhamento de links) para `GET` solicitações. Bloquear outros URLs para garantir a segurança do [!DNL Experience Manager] Autor.
   >
   >* http://[aem_server]:[porta]/linkshare.html
   >* http://[aem_server]:[porta]/linksharepreview.html
   >* http://[aem_server]:[porta]/linkexpired.html


   >[!NOTE]
   >
   >Se um ativo compartilhado for movido para um local diferente, seu link para de funcionar. Recrie o link e compartilhe-o novamente com os usuários.

1. Na [!DNL Experience Manager] interface, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. Para as propriedades `local` e `author` , forneça o URL para as instâncias local e autor, respectivamente. As propriedades `local` e `author` têm o mesmo valor se você executar uma única instância [!DNL Experience Manager] do autor. Por exemplo, `publish`forneça o URL da instância de [!DNL Experience Manager] publicação.

1. Na caixa de endereço de email da caixa de diálogo **[!UICONTROL Compartilhamento de links]**, digite a ID de email do usuário com o qual deseja compartilhar o link. Além disso, é possível compartilhar o link com vários usuários.

   Se o usuário for membro de sua organização, selecione a ID de email do usuário nas IDs de email sugeridas que aparecem na lista abaixo da área de digitação. Para um usuário externo, digite a ID de email completa e selecione-a na lista.

   Para permitir o envio de emails para usuários, configure os detalhes do servidor SMTP no [Day CQ Mail Service](#configmailservice).

   ![Compartilhar links com ativos diretamente da caixa de diálogo Compartilhamento de links](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Compartilhe links para ativos diretamente da caixa de diálogo Compartilhamento[!UICONTROL de]links.*

   >[!NOTE]
   >
   >Se você inserir uma ID de email de um usuário que não seja membro de sua organização, as palavras Usuário  externo receberão o prefixo ID de email do usuário.

1. No campo **[!UICONTROL Assunto]** , informe um assunto para o ativo que deseja compartilhar.

1. No campo **[!UICONTROL Mensagem]** , insira uma mensagem opcional.

1. No campo **[!UICONTROL Expiração]** , especifique uma data e hora de expiração para o link usando o seletor de datas. Por padrão, a data de expiração é definida para uma semana a partir da data em que você compartilha o link.

   ![Definir data de expiração do link compartilhado](assets/Set-shared-link-expiration.png)

1. Para permitir que os usuários baixem a imagem original junto com as execuções, selecione **[!UICONTROL Permitir download do arquivo]** original.

   >[!NOTE]
   >
   >Por padrão, os usuários podem baixar somente as representações do ativo que você compartilha como um link.

1. Clique em **[!UICONTROL Compartilhar]**. Uma mensagem confirma que o link é compartilhado com os usuários por meio de um email.
1. Para visualização do ativo compartilhado, clique no link no email enviado ao usuário. O ativo compartilhado é exibido na página **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Para alternar para a visualização da lista, clique na opção de layout na barra de ferramentas.

1. Para gerar uma pré-visualização do ativo, clique no ativo compartilhado. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] suporta a geração de pré-visualização de ativos destes tipos MIME: JPG, PNG, GIF, BMP, INDD, PDF e PPT. Você só pode baixar os ativos dos outros tipos MIME.

1. Para baixar o ativo compartilhado, clique em **[!UICONTROL Selecionar]** na barra de ferramentas, clique no ativo e, em seguida, clique em **[!UICONTROL Download]** na barra de ferramentas.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Para visualização dos ativos compartilhados como links, vá para a interface do [!DNL Assets] usuário e clique no [!DNL Experience Manager] logotipo. Escolha **[!UICONTROL Navegação]** na lista para exibir o painel de Navegação.
1. No painel Navegação, escolha **[!UICONTROL Links compartilhados]** para exibir uma lista de ativos compartilhados.
1. Para descompartilhar um ativo, selecione-o e clique em **[!UICONTROL Descompartilhar]** na barra de ferramentas. Uma mensagem de confirmação é exibida. A entrada do ativo é removida da lista.

## Configurar o serviço de e-mail Day CQ {#configmailservice}

1. No [!DNL Experience Manager] home page, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.
1. Na lista de serviços, localize o **[!UICONTROL Dia CQ Mail Service]**.
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nome do host do servidor SMTP: nome do host do servidor de email
   * Porta do servidor SMTP: porta do servidor de email
   * Usuário SMTP: nome de usuário do servidor de email
   * Senha SMTP: senha do servidor de email

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Clique em **[!UICONTROL Salvar]**.

## Configurar tamanho máximo de dados {#maxdatasize}

Quando você baixa ativos do link compartilhado usando o recurso Compartilhamento de link, [!DNL Experience Manager] compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que pode ser compactada em um arquivo ZIP, grandes quantidades de dados são submetidas à compactação, o que causa erros de memória esgotada no JVM. Para proteger o sistema de um possível ataque de negação de serviço devido a essa situação, configure o tamanho máximo usando o parâmetro **[!UICONTROL Máximo de tamanho de conteúdo (descompactado)]** para o Servlet [!UICONTROL Proxy de compartilhamento de ativos ad hoc do] Day CQ DAM no Configuration Manager. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download do ativo serão rejeitadas. O valor padrão é 100 MB.

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. No Console da Web, localize a configuração do Servlet **[!UICONTROL Adhoc de Compartilhamento de Ativo do]** Dia CQ DAM.
1. Abra a configuração do **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** no modo de edição e modifique o valor do parâmetro **[!UICONTROL Tamanho máximo de conteúdo (descompactado)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salve as alterações.

## Best practices and troubleshooting {#bestpractices}

* Pastas de ativos ou Coleções que contêm um espaço em branco em seu nome podem não ser compartilhadas.
* Se os usuários não puderem baixar os ativos compartilhados, verifique com seu [!DNL Experience Manager] administrador quais são os limites [de](#maxdatasize) download.
* Se você não puder enviar emails com links para ativos compartilhados ou se os outros usuários não puderem receber seu email, verifique com seu [!DNL Experience Manager] administrador se o serviço [de](#configmailservice) email está configurado ou não.
* Se você não puder compartilhar ativos usando a funcionalidade de compartilhamento de links, verifique se você tem as permissões apropriadas. Consulte [compartilhar ativos](#sharelink).
