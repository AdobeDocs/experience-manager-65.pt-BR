---
title: Compartilhar ativos usando um link
description: Compartilhar ativos, pastas e coleções como um URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 6%

---

# Compartilhar ativo como um link {#asset-link-sharing}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Experience Manager Assets] O permite compartilhar ativos, pastas e coleções como uma URL com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. O compartilhamento de ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon no [!DNL Assets].

>[!PREREQUISITES]
>
>* Você precisa `Edit ACL` na pasta ou no ativo que você deseja compartilhar como um link.
>* Para enviar emails aos usuários, configure os detalhes do servidor SMTP no [Serviço de email Day CQ](#configmailservice).

## Compartilhar ativos {#share-assets}

Para gerar o URL para ativos que você deseja compartilhar com os usuários, use o [!UICONTROL Compartilhamento de link] diálogo.

* Os usuários com privilégios de administrador ou com permissões de leitura em `/var/dam/share` O local pode exibir os links compartilhados com eles.
* Os usuários com permissões de leitura em `/var/dam/jobs/download` O local pode baixar ativos do link compartilhado.

1. No [!DNL Assets] selecione o ativo a ser compartilhado como um link.

1. Na barra de ferramentas, clique na guia **[!UICONTROL Compartilhar link]** ![ícone compartilhar ativos](assets/do-not-localize/assets_share.png). O link criado após clicar em **[!UICONTROL Compartilhar]** é exibido com antecedência no [!UICONTROL Compartilhar link] campo. O link não é criado até que você selecione **[!UICONTROL Enviar]**.

   ![Caixa de diálogo com o compartilhamento de link](assets/share-assets-as-link.png)

   *Figura: a caixa de diálogo para compartilhar ativos como um link.*

1. Na caixa de endereço de email da caixa de diálogo **[!UICONTROL Compartilhamento de links]**, digite a ID de email do usuário com o qual deseja compartilhar o link. É possível adicionar um ou mais usuários.

   >[!NOTE]
   >
   >Se você inserir uma ID de email de um usuário que não é membro da organização, as palavras [!UICONTROL Usuário externo] recebem o prefixo da ID de email do usuário.

1. No **[!UICONTROL Assunto]** insira um assunto para o ativo que deseja compartilhar.

1. No **[!UICONTROL Mensagem]** , digite uma mensagem opcional.

1. No **[!UICONTROL Expiração]** especifique uma data e hora de expiração para o link parar de funcionar. O tempo de expiração padrão do link é de um dia.

   ![Definir data de expiração do link compartilhado](assets/Set-shared-link-expiration.png)

1. Para permitir que os usuários baixem o ativo original, selecione **[!UICONTROL Permitir download do arquivo original]**. Para permitir que os usuários baixem somente as representações dos ativos compartilhados, selecione **[!UICONTROL Permitir download de representações de arquivo]**.

1. Clique em **[!UICONTROL Compartilhar]**. Uma mensagem confirma que o link é compartilhado com os usuários por meio de um email.

1. Para exibir o ativo compartilhado, clique no link do email enviado ao usuário. Para gerar uma visualização do ativo, clique no ativo compartilhado. Para fechar a visualização, clique em **[!UICONTROL Voltar]**. Se tiver compartilhado uma pasta, clique em **[!UICONTROL Pasta pai]** para retornar à pasta principal.

   ![Visualização do ativo compartilhado](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] suporta a geração da pré-visualização de ativos somente de [os tipos de arquivo compatíveis](/help/assets/assets-formats.md). Se outros tipos MIME forem compartilhados, você só poderá baixar os ativos e não poderá pré-visualizar.

1. Para baixar o ativo compartilhado, clique em **[!UICONTROL Selecionar]** na barra de ferramentas, clique no ativo e clique em **[!UICONTROL Baixar]** na barra de ferramentas.

   ![Opção da barra de ferramentas para baixar o ativo compartilhado](assets/chlimage_1-547.png)

1. Para exibir os ativos que você compartilhou como links, vá para a [!DNL Assets] e clique no link [!DNL Experience Manager] logotipo. Escolher **[!UICONTROL Navegação]**. No painel Navegação, escolha **[!UICONTROL Links compartilhados]** para exibir uma lista de ativos compartilhados.

1. Para cancelar o compartilhamento de um ativo, selecione-o e clique **[!UICONTROL Cancelar compartilhamento]** na barra de ferramentas. Uma mensagem de confirmação será exibida em seguida. A entrada do ativo é removida da lista.

## Configurar o serviço de email Day CQ {#configure-day-cq-mail-service}

1. No [!DNL Experience Manager] home page, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Na lista de serviços, localize **[!UICONTROL Serviço de email Day CQ]**.
1. Clique em **[!UICONTROL Editar]** ao lado do serviço, e configure os seguintes parâmetros para **[!UICONTROL Serviço de email Day CQ]** com os detalhes mencionados em seus nomes:

   * Nome do host do servidor SMTP: nome do host do servidor de email
   * Porta do servidor SMTP: porta do servidor de email
   * Usuário SMTP: nome de usuário do servidor de email
   * Senha SMTP: senha do servidor de e-mail

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Clique em **[!UICONTROL Salvar]**.

## Configurar tamanho máximo dos dados {#configure-maximum-data-size}

Ao baixar ativos do link compartilhado usando o recurso Compartilhamento de link, [!DNL Experience Manager] compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que podem ser compactados em um arquivo ZIP, quantidades enormes de dados estão sujeitas a compactação, o que causa erros de falta de memória na JVM. Para proteger o sistema contra um possível ataque de negação de serviço devido a essa situação, configure o tamanho máximo usando o **[!UICONTROL Tamanho máximo do conteúdo (descompactado)]** parâmetro para **[!UICONTROL Servlet de proxy de compartilhamento de ativos adhoc DAM do Day CQ]** no Configuration Manager. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download de ativos serão rejeitadas. O valor padrão é 100 MB.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No Console da Web, localize o **[!UICONTROL Servlet de proxy de compartilhamento de ativos adhoc DAM do Day CQ]** configuração.
1. Abra a configuração do **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** no modo de edição e modifique o valor do parâmetro **[!UICONTROL Tamanho máximo de conteúdo (descompactado)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salve as alterações.

## Práticas recomendadas e solução de problemas {#best-practices-and-troubleshooting}

* As pastas de ativos ou coleções que contêm um espaço em branco em seu nome não podem ser compartilhadas.
* Se os usuários não conseguirem baixar os ativos compartilhados, verifique com o [!DNL Experience Manager] administrador o que o [limites de download](#configure-maximum-data-size) são.
* Se não conseguir enviar um email com links para ativos compartilhados ou se os outros usuários não puderem receber seu email, verifique com o [!DNL Experience Manager] administrador se a variável [serviço de e-mail](#configure-day-cq-mail-service) está configurado ou não.
* Se não for possível compartilhar ativos usando a funcionalidade de compartilhamento de link, verifique se você tem as permissões apropriadas. Consulte [compartilhar ativos](#share-assets).
* Se um ativo compartilhado for movido para um local diferente, seu link deixará de funcionar. Recrie o link e compartilhe-o com os usuários.

* Se quiser compartilhar links de seu [!DNL Experience Manager] Implantação de autor em entidades externas, certifique-se de expor apenas os seguintes URLs usados para o compartilhamento de links, para `GET` somente solicitações. Bloquear outros URLs por motivos de segurança.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  Entrada [!DNL Experience Manager] interface, acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. Abra o **[!UICONTROL Day CQ Link Externalizer]** configure e modifique as seguintes propriedades na variável **[!UICONTROL Domínios]** campo com os valores mencionados em relação a `local`, `author`, e `publish`. Para o `local` e `author` propriedades, forneça o URL para as instâncias local e do Autor, respectivamente. Se você executar um único [!DNL Experience Manager] Instância do autor, use o mesmo valor para `local` e `author` propriedades. Para instâncias de Publicação, forneça o URL do [!DNL Experience Manager] Instância de publicação.
