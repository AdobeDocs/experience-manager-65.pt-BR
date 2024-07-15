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

O [!DNL Adobe Experience Manager Assets] permite que você compartilhe ativos, pastas e coleções como uma URL com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. O compartilhamento de ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon no [!DNL Assets].

>[!PREREQUISITES]
>
>* Você precisa da permissão `Edit ACL` para a pasta ou o ativo que deseja compartilhar como um link.
>* Para enviar emails aos usuários, configure os detalhes do servidor SMTP no [Day CQ Mail Service](#configmailservice).

## Compartilhar ativos {#share-assets}

Para gerar a URL dos ativos que você deseja compartilhar com os usuários, use a caixa de diálogo [!UICONTROL Compartilhamento de links].

* Os usuários com privilégios de administrador ou com permissões de leitura no local `/var/dam/share` podem exibir os links compartilhados com eles.
* Os usuários com permissões de leitura no local `/var/dam/jobs/download` podem baixar ativos do link compartilhado.

1. Na interface de usuário do [!DNL Assets], selecione o ativo a ser compartilhado como um link.

1. Na barra de ferramentas, clique no **[!UICONTROL ícone Compartilhar link]** ![compartilhar ativos](assets/do-not-localize/assets_share.png). O link criado após clicar em **[!UICONTROL Compartilhar]** é exibido com antecedência no campo [!UICONTROL Compartilhar Link]. O link só será criado depois que você selecionar **[!UICONTROL Enviar]**.

   ![Caixa de diálogo com o Compartilhamento de Link](assets/share-assets-as-link.png)

   *Figura: a caixa de diálogo para compartilhar ativos como um link.*

1. Na caixa de endereço de email da caixa de diálogo **[!UICONTROL Compartilhamento de links]**, digite a ID de email do usuário com o qual deseja compartilhar o link. É possível adicionar um ou mais usuários.

   >[!NOTE]
   >
   >Se você inserir uma ID de email de um usuário que não é membro da sua organização, as palavras [!UICONTROL Usuário externo] terão o prefixo da ID de email do usuário.

1. Na caixa **[!UICONTROL Assunto]**, insira um assunto para o ativo que deseja compartilhar.

1. Na caixa **[!UICONTROL Mensagem]**, digite uma mensagem opcional.

1. No campo **[!UICONTROL Expiration]**, especifique uma data e hora de expiração para o link parar de funcionar. O tempo de expiração padrão do link é de um dia.

   ![Definir data de expiração do link compartilhado](assets/Set-shared-link-expiration.png)

1. Para permitir que os usuários baixem o ativo original, selecione **[!UICONTROL Permitir download do arquivo original]**. Para permitir que os usuários baixem apenas as representações dos ativos compartilhados, selecione **[!UICONTROL Permitir download de representações do arquivo]**.

1. Clique em **[!UICONTROL Compartilhar]**. Uma mensagem confirma que o link é compartilhado com os usuários por meio de um email.

1. Para exibir o ativo compartilhado, clique no link do email enviado ao usuário. Para gerar uma visualização do ativo, clique no ativo compartilhado. Para fechar a visualização, clique em **[!UICONTROL Voltar]**. Se tiver compartilhado uma pasta, clique em **[!UICONTROL Pasta pai]** para retornar à pasta pai.

   ![Visualização do ativo compartilhado](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] dá suporte à geração de visualização de ativos de apenas [os tipos de arquivos com suporte](/help/assets/assets-formats.md). Se outros tipos MIME forem compartilhados, você só poderá baixar os ativos e não poderá pré-visualizar.

1. Para baixar o ativo compartilhado, clique em **[!UICONTROL Selecionar]** na barra de ferramentas, clique no ativo e em **[!UICONTROL Baixar]** na barra de ferramentas.

   ![Opção da barra de ferramentas para baixar o ativo compartilhado](assets/chlimage_1-547.png)

1. Para exibir os ativos compartilhados como links, vá para a interface do usuário do [!DNL Assets] e clique no logotipo do [!DNL Experience Manager]. Escolha **[!UICONTROL Navegação]**. No painel Navegação, escolha **[!UICONTROL Links compartilhados]** para exibir uma lista de ativos compartilhados.

1. Para cancelar o compartilhamento de um ativo, selecione-o e clique em **[!UICONTROL Cancelar compartilhamento]** na barra de ferramentas. Uma mensagem de confirmação será exibida em seguida. A entrada do ativo é removida da lista.

## Configurar o serviço de email Day CQ {#configure-day-cq-mail-service}

1. Na página inicial do [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Na lista de serviços, localize o **[!UICONTROL Day CQ Mail Service]**.
1. Clique em **[!UICONTROL Editar]** ao lado do serviço e configure os seguintes parâmetros para o **[!UICONTROL Day CQ Mail Service]** com os detalhes mencionados em seus nomes:

   * Nome do host do servidor SMTP: nome do host do servidor de email
   * Porta do servidor SMTP: porta do servidor de email
   * Usuário SMTP: nome de usuário do servidor de email
   * Senha SMTP: senha do servidor de e-mail

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Clique em **[!UICONTROL Salvar]**.

## Configurar tamanho máximo dos dados {#configure-maximum-data-size}

Ao baixar ativos do link compartilhado usando o recurso Compartilhamento de Link, o [!DNL Experience Manager] compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que podem ser compactados em um arquivo ZIP, quantidades enormes de dados estão sujeitas a compactação, o que causa erros de falta de memória na JVM. Para proteger o sistema contra um possível ataque de negação de serviço devido a essa situação, configure o tamanho máximo usando o **[!UICONTROL parâmetro de Tamanho máximo de conteúdo (descompactado)]** para o **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** no Configuration Manager. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download de ativos serão rejeitadas. O valor padrão é 100 MB.

1. Clique no logotipo [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No Console da Web, localize a configuração **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Abra a configuração do **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** no modo de edição e modifique o valor do parâmetro **[!UICONTROL Tamanho máximo de conteúdo (descompactado)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salve as alterações.

## Práticas recomendadas e solução de problemas {#best-practices-and-troubleshooting}

* As pastas de ativos ou coleções que contêm um espaço em branco em seu nome não podem ser compartilhadas.
* Se os usuários não conseguirem baixar os ativos compartilhados, verifique com o administrador do [!DNL Experience Manager] quais são os [limites de download](#configure-maximum-data-size).
* Se você não conseguir enviar emails com links para ativos compartilhados ou se os outros usuários não puderem receber seus emails, verifique com o administrador do [!DNL Experience Manager] se o [serviço de email](#configure-day-cq-mail-service) está configurado ou não.
* Se não for possível compartilhar ativos usando a funcionalidade de compartilhamento de link, verifique se você tem as permissões apropriadas. Consulte [compartilhar ativos](#share-assets).
* Se um ativo compartilhado for movido para um local diferente, seu link deixará de funcionar. Recrie o link e compartilhe-o com os usuários.

* Se você deseja compartilhar links da sua implantação de Autor do [!DNL Experience Manager] com entidades externas, certifique-se de expor apenas as seguintes URLs que são usadas para compartilhamento de links, somente para solicitações do `GET`. Bloquear outros URLs por motivos de segurança.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  Na interface [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. Abra a configuração **[!UICONTROL Day CQ Link Externalizer]** e modifique as seguintes propriedades no campo **[!UICONTROL Domínios]** com os valores mencionados em relação a `local`, `author` e `publish`. Para as propriedades `local` e `author`, forneça a URL para as instâncias local e do Autor, respectivamente. Se você executar uma única instância de Autor [!DNL Experience Manager], use o mesmo valor para as propriedades `local` e `author`. Para instâncias Publish, forneça a URL da instância Publish [!DNL Experience Manager].
