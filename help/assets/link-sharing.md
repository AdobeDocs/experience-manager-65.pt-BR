---
title: Gerar um URL para ativos compartilhados
description: Este artigo descreve como compartilhar ativos, pastas e coleções dentro dos ativos AEM como um URL para terceiros externos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Compartilhar ativos por meio de um link {#asset-link-sharing}

Os ativos Adobe Experience Manager (AEM) permitem que você compartilhe ativos, pastas e coleções como um URL com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon nos ativos AEM.

>[!NOTE]
>
>Você precisa da permissão Editar ACL na pasta ou no ativo que deseja compartilhar como um link.

## Compartilhar ativos {#sharelink}

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem exibir os links compartilhados com eles.

>[!NOTE]
>
>Antes de compartilhar um link com os usuários, verifique se o Day CQ Mail Service está configurado. Ocorre um erro se você tentar compartilhar um link sem primeiro [configurar o Serviço](/help/assets/link-sharing.md#configmailservice)de e-mail Day CQ.

1. Na interface do usuário Ativos, selecione o ativo a ser compartilhado como um link.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Compartilhar link]** ![assets_share](assets/assets_share.png).

   Um link de ativo é criado automaticamente no campo **[!UICONTROL Compartilhar link]** . Copie este link e compartilhe-o com os usuários. A hora de expiração padrão do link é um dia.

   ![Diálogo com o compartilhamento de links](assets/Link-sharing-dialog-box.png)

   *Figura:Diálogo com o compartilhamento de links*

   Como alternativa, prossiga para executar as etapas 3 a 7 desse procedimento para adicionar destinatários de email, configurar a hora de expiração do link e enviá-lo da caixa de diálogo.

   >[!NOTE]
   >
   >Se você quiser compartilhar links da instância do autor de AEM com entidades externas, certifique-se de apenas expor os seguintes URLs (que são usados para compartilhamento de links) para `GET` solicitações. Bloqueie outros URLs para garantir a segurança do autor de AEM.
   >
   >* http://&lt;aem_server>:&lt;porta>/linkshare.html
   * http://&lt;aem_server>:&lt;porta>/linksharepreview.html
   * http://&lt;aem_server>:&lt;porta>/linkexpired.html


   >[!NOTE]
   Se um ativo compartilhado for movido para um local diferente, seu link para de funcionar. Recrie o link e compartilhe-o novamente com os usuários.

1. No console da Web, abra a configuração do **[!UICONTROL Day CQ Link Externalizer]** e modifique as seguintes propriedades no campo **[!UICONTROL Domínios]** com os valores mencionados em relação a cada:

   * local
   * author
   * publicação
   Para as propriedades local e autor, forneça o URL para as instâncias local e autor, respectivamente. As propriedades local e de autor têm o mesmo valor se você executar uma única instância de autor de AEM. Para publicar, forneça o URL da instância de publicação.

1. Na caixa de endereço de email da caixa de diálogo **[!UICONTROL Compartilhamento de links]**, digite a ID de email do usuário com o qual deseja compartilhar o link. Além disso, é possível compartilhar o link com vários usuários.

   Se o usuário for membro de sua organização, selecione a ID de email do usuário nas IDs de email sugeridas que aparecem na lista abaixo da área de digitação. Para um usuário externo, digite a ID de email completa e selecione-a na lista.

   Para permitir o envio de emails para usuários, configure os detalhes do servidor SMTP no [Day CQ Mail Service](#configmailservice).

   ![Compartilhar links com ativos diretamente da caixa de diálogo Compartilhamento de links](assets/Asset-Sharing-LinkShareDialog.png)

   Compartilhar links com ativos diretamente da caixa de diálogo Compartilhamento de links

   >[!NOTE]
   Se você inserir uma ID de email de um usuário que não seja membro de sua organização, as palavras &quot;Usuário externo&quot; receberão o prefixo ID de email do usuário.

1. Na caixa **[!UICONTROL Assunto]** , informe um assunto para o ativo que deseja compartilhar.
1. Na caixa **[!UICONTROL Mensagem]** , digite uma mensagem opcional.
1. No campo **[!UICONTROL Expiração]** , especifique uma data e hora de expiração para o link usando o seletor de datas. Por padrão, a data de expiração é definida para uma semana a partir da data em que você compartilha o link.

   ![Definir data de expiração do link compartilhado](assets/Set-shared-link-expiration.png)

1. Para permitir que os usuários baixem a imagem original junto com as execuções, selecione **[!UICONTROL Permitir download do arquivo]** original.

   >[!NOTE]
   Por padrão, os usuários podem baixar somente as representações do ativo que você compartilha como link.

1. Clique em **[!UICONTROL Compartilhar]**. Uma mensagem confirma que o link é compartilhado com os usuários por meio de um email.
1. Para exibir o ativo compartilhado, clique/toque no link no email enviado ao usuário. O ativo compartilhado é exibido na página da **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Para alternar para a exibição de lista, clique/toque na opção de layout na barra de ferramentas.

1. Para gerar uma visualização do ativo, clique/toque no ativo compartilhado. Para fechar a visualização e retornar à página da **[!UICONTROL Experience Cloud]**, clique/toque em **[!UICONTROL Voltar]** na barra de ferramentas. Se tiver compartilhado uma pasta, clique/toque em **[!UICONTROL Pasta pai]** para retornar à pasta principal.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   O AEM oferece suporte à geração da visualização de ativos desses tipos MIME: JPG, PNG, GIF, BMP, INDD, PDF e PPT. Você só pode baixar os ativos dos outros tipos MIME.

1. Para baixar o ativo compartilhado, toque em **[!UICONTROL Selecionar]** na barra de ferramentas, clique/toque no ativo e, em seguida, clique/toque em **[!UICONTROL Download]** na barra de ferramentas.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Para exibir os ativos compartilhados como links, vá para a interface do usuário do Assets e toque no logotipo do Experience Manager. Escolha **[!UICONTROL Navegação]** na lista para exibir o painel de Navegação.
1. No painel Navegação, escolha **[!UICONTROL Links compartilhados]** para exibir uma lista de ativos compartilhados.
1. Para descompartilhar um ativo, selecione-o e toque/clique em **[!UICONTROL Descompartilhar]** na barra de ferramentas. Uma mensagem de confirmação é exibida. A entrada do ativo é removida da lista.

## Configurar o serviço de e-mail Day CQ {#configmailservice}

1. Na página inicial do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web.
1. Na lista de serviços, localize o **[!UICONTROL Dia CQ Mail Service]**.
1. Tap **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nome do host do servidor SMTP: nome do host do servidor de email
   * Porta do servidor SMTP: porta do servidor de email
   * Usuário SMTP: nome de usuário do servidor de email
   * Senha SMTP: senha do servidor de email
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Click/tap **[!UICONTROL Save]**.

## Configurar tamanho máximo de dados {#maxdatasize}

Quando você baixa ativos do link compartilhado usando o recurso Compartilhamento de link, o AEM compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que pode ser compactada em um arquivo ZIP, grandes quantidades de dados são submetidas à compactação, o que causa erros de memória esgotada no JVM. Para proteger o sistema de um possível ataque de negação de serviço devido a essa situação, configure o tamanho máximo usando o parâmetro **[!UICONTROL Máximo de tamanho de conteúdo (descompactado)]** para o Servlet [!UICONTROL Proxy de compartilhamento de ativos ad hoc] Day CQ DAM no Configuration Manager. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download do ativo serão rejeitadas. O valor padrão é 100 MB.

1. Clique/toque no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No Console da Web, localize a configuração do Servlet **[!UICONTROL Adhoc de Compartilhamento de ativos Ad hoc do]** Day CQ DAM.
1. Abra a configuração do **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** no modo de edição e modifique o valor do parâmetro **[!UICONTROL Tamanho máximo de conteúdo (descompactado)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salve as alterações.

## Best practices and troubleshooting {#bestpractices}

* Pastas de ativos ou Coleções que contêm um espaço em branco em seu nome podem não ser compartilhadas.
* Se os usuários não puderem baixar os ativos compartilhados, verifique com o administrador do AEM quais são os limites [de](#maxdatasize) download.
* Se você não puder enviar emails com links para ativos compartilhados ou se os outros usuários não puderem receber seu email, verifique com o administrador do AEM se o serviço [de](#configmailservice) email está configurado ou não.
* Se você não puder compartilhar ativos usando a funcionalidade de compartilhamento de links, verifique se você tem as permissões apropriadas. Consulte [compartilhar ativos](#sharelink).
