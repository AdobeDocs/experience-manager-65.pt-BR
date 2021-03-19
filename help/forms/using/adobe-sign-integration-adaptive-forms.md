---
title: Integrar o Adobe Sign ao AEM Forms
seo-title: Integrar o Adobe Sign ao AEM Forms
description: Saiba como configurar o Adobe Sign para AEM Forms
seo-description: Saiba como configurar o Adobe Sign para AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Integre [!DNL Adobe Sign] com AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] ativa fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras.

Em um cenário típico de [!DNL Adobe Sign] e formulários adaptáveis, um usuário preenche um formulário adaptável para **se aplicar a um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que você possa realizar mais ações. O provedor de serviços revisa o aplicativo e usa [!DNL Adobe Sign] para marcar o aplicativo aprovado. Para ativar workflows de assinatura eletrônica semelhantes, você pode integrar [!DNL Adobe Sign] com AEM [!DNL Forms].

Para usar [!DNL Adobe Sign] com AEM [!DNL Forms], configure [!DNL Adobe Sign] no AEM Cloud Services:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar [!DNL Adobe Sign] com AEM [!DNL Forms]:

* Uma conta ativa de desenvolvedor [Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um servidor [SSL habilitado](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Um [aplicativo da API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e Segredo do cliente) do aplicativo de API [!DNL Adobe Sign].
* Ao reconfigurar, remova a configuração [!DNL Adobe Sign] existente das instâncias de autor e de publicação.
* Use [chave de criptografia idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para criar e publicar instâncias.

## Configure [!DNL Adobe Sign] com AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com AEM [!DNL Forms] na instância do autor:

1. Em AEM instância do autor [!DNL Forms], navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. Na página **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
   * Consulte a documentação do [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Na caixa de diálogo **[!UICONTROL Criar configuração]**, especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações de nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para serviços de nuvem.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e selecione o contêiner de configuração que você criou na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um novo contêiner de configuração e criar uma configuração [!DNL Adobe Sign] no contêiner ou usar a pasta `global` existente em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo contêiner de configuração, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]** ao criar um formulário adaptável.

   >[!NOTE]
   Certifique-se de que o URL da página de configuração dos serviços de nuvem comece com **HTTPS**. Caso contrário, [ative SSL](/help/sites-administering/ssl-by-default.md) para AEM servidor [!DNL Forms].

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign] no AEM [!DNL Forms].
1. Na guia **[!UICONTROL General]** da página **[!UICONTROL Criar configuração do Adobe Sign]**, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próximo]**. Como opção, você pode especificar um título e procurar para selecionar uma miniatura para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. É necessário configurar o aplicativo [!DNL Adobe Sign] com AEM[!DNL Forms].

1. Defina as configurações de OAuth para o aplicativo [!DNL Adobe Sign]:

   1. Abra uma janela do navegador e faça logon na conta de desenvolvedor [!DNL Adobe Sign].
   1. Selecione o aplicativo configurado para AEM [!DNL Forms] e toque em **[!UICONTROL Configurar OAuth para Aplicativo]**.
   1. Copie o **[!UICONTROL ID do cliente]** e o **[!UICONTROL Segredo do cliente]** para um bloco de notas.
   1. Na caixa **[!UICONTROL Redirecionar URL]**, adicione o URL HTTPS copiado na etapa anterior.
   1. Ative as seguintes configurações OAuth para o aplicativo [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obter informações passo a passo para definir as configurações do OAuth para um aplicativo [!DNL Adobe Sign] e obter as chaves, consulte [Definir configurações de oAuth para a documentação do desenvolvedor do aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuração OAuth](assets/oauthconfig_new.png)

1. Volte para a página **[!UICONTROL Criar configuração do Adobe Sign]**. Na guia **[!UICONTROL Settings]**, o campo **[!UICONTROL OAuth URL]** menciona o seguinte URL padrão:

   https://secure.na1.echosign.com/public/oauth

   em que:

   **na1** se refere ao compartilhamento de banco de dados padrão.

   Você pode modificar o valor do compartilhamento de banco de dados. Reinicie o servidor para poder usar o novo valor para o compartilhamento de banco de dados.

   >[!NOTE]
   Certifique-se de que as configurações da instância de criação e publicação apontem para o mesmo compartilhamento. Se você criar várias configurações do Adobe Sign para uma organização, verifique se todas as configurações utilizam o mesmo compartilhamento.

1. Especifique o **ID do cliente** (também conhecido como ID do aplicativo) e o **Segredo do cliente** copiados na etapa 8. Selecione a opção **[!UICONTROL Ativar Adobe Sign para anexos também]** para anexar arquivos anexados a um formulário adaptável ao documento [!DNL Adobe Sign] correspondente enviado para assinatura.

   Toque em **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL Adobe Sign].

   Toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign].

1. Abra AEM Console da Web. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abra **[!UICONTROL Forms Common Configuration Service].**
1. No campo **[!UICONTROL Permitir]**, **selecione** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clique em **[!UICONTROL Salvar].** A instância do autor está configurada para usar  [!DNL Adobe Sign].
1. Publique a configuração.
1. Use [replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) para criar configurações idênticas nas instâncias de publicação correspondentes.

Agora, [!DNL Adobe Sign] é integrado com AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o contêiner de configuração criado acima nas propriedades de formulário adaptável.



## Configure o agendador [!DNL Adobe Sign] para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um formulário adaptável habilitado para [!DNL Adobe Sign] é enviado somente após a conclusão do processo de assinatura por todos os signatários. Por padrão, os [!DNL Adobe Sign] serviços do Scheduler são agendados para verificar (pesquisar) a resposta do assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Faça logon no servidor [!DNL Forms] AEM com credenciais de administrador e navegue até **Ferramentas** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra a opção **[!UICONTROL Adobe Sign Configuration Service]**. Especifique uma [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) no campo **[!UICONTROL Status Update Scheduler Expression]** e clique em **[!UICONTROL Save]**. Por exemplo, para executar o serviço de configuração diariamente às 00:00 am, especifique `0 0 0 1/1 * ? *` no campo **[!UICONTROL Status Update Scheduler Expression]**.

O intervalo padrão para sincronizar o status de [!DNL Adobe Sign] agora é alterado.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Uso do Adobe Sign com AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


