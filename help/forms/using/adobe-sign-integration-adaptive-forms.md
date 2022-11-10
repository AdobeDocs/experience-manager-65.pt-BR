---
title: Integrar o Adobe Sign ao AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: Saiba como configurar o Adobe Sign para AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# Integrar [!DNL Adobe Sign] com AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] ativa fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras.

Em um [!DNL Adobe Sign] e formulários adaptáveis, um usuário preenche um formulário adaptável para **solicitar um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que você possa realizar mais ações. O provedor de serviços revisa o aplicativo e os usos [!DNL Adobe Sign] para assinalar o pedido aprovado. Para ativar workflows semelhantes de assinatura eletrônica, é possível integrar [!DNL Adobe Sign] com AEM [!DNL Forms].

Para usar [!DNL Adobe Sign] com AEM [!DNL Forms], configurar [!DNL Adobe Sign] no AEM Cloud Services:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar [!DNL Adobe Sign] com AEM [!DNL Forms]:

* Uma atividade [Conta de desenvolvedor do Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um [SSL habilitado](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] servidor.
* Um [Aplicativo de API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e Segredo do cliente) de [!DNL Adobe Sign] Aplicativo de API.
* Ao reconfigurar, remova as [!DNL Adobe Sign] configuração das instâncias de autor e publicação.
* Use [chave de criptografia idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.

## Configurar [!DNL Adobe Sign] com AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com AEM [!DNL Forms] na instância do autor:

1. No AEM [!DNL Forms] instância do autor, navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, habilite **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para serviços de nuvem.
1. Navegar para **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e selecione o contêiner de configuração criado na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um novo contêiner de configuração e criar um [!DNL Adobe Sign] no contêiner ou use o `global` pasta em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo contêiner de configuração, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** ao criar um formulário adaptável.

   >[!NOTE]
   Certifique-se de que o URL da página de configuração dos serviços em nuvem comece com **HTTPS**. Caso contrário, [habilitar SSL](/help/sites-administering/ssl-by-default.md) para AEM [!DNL Forms] servidor.

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Sign] configuração no AEM [!DNL Forms].
1. No **[!UICONTROL Geral]** da guia **[!UICONTROL Criar configuração do Adobe Sign]** especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próximo]**. Como opção, você pode especificar um título e procurar para selecionar uma miniatura para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. É necessário configurar [!DNL Adobe Sign] aplicativo com AEM[!DNL Forms].

1. No **[!UICONTROL Configurações]** , a variável **[!UICONTROL URL de OAuth]** contém o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao compartilhamento de banco de dados padrão. Você pode modificar o valor do compartilhamento de banco de dados. Certifique-se de que [!DNL  Adobe Sign] As Configurações de nuvem apontam para a [Shard correto](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se você criar outro [!DNL Adobe Sign] para um recurso ou componente do Adobe Experience Manager, verifique se todas as [!DNL Adobe Sign] As Configurações de nuvem apontam para o mesmo compartilhamento.

   >[!NOTE]
   Mantenha o **Criar configuração do Adobe Sign** página aberta. Não feche. Você pode recuperar **ID do cliente** e **Segredo do cliente** após definir as configurações do OAuth para a variável [!DNL Adobe Sign] conforme descrito em etapas futuras.


1. Defina as configurações de OAuth para a variável [!DNL Adobe Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon no [!DNL Adobe Sign] conta do desenvolvedor.
   1. Selecione o aplicativo configurado para AEM [!DNL Forms]e toque em **[!UICONTROL Configurar o OAuth para aplicativo]**.
   1. Copie o **[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]** para um bloco de notas.
   1. No **[!UICONTROL Redirecionar URL]** , adicione o URL HTTPS copiado na etapa anterior.
   1. Ative as seguintes configurações de OAuth para o [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obter informações passo a passo sobre a configuração do OAuth para um [!DNL Adobe Sign] e obtenha as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentação do desenvolvedor.

   ![Configuração OAuth](assets/oauthconfig_new.png)

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** , a variável **[!UICONTROL URL de OAuth]** menciona o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao compartilhamento de banco de dados padrão.

   Você pode modificar o valor do compartilhamento de banco de dados. Reinicie o servidor para poder usar o novo valor para o compartilhamento de banco de dados.

   >[!NOTE]
   Certifique-se de que as configurações da instância de criação e publicação apontem para o mesmo compartilhamento. Se você criar várias configurações do Adobe Sign para uma organização, verifique se todas as configurações utilizam o mesmo compartilhamento.

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** , especifique o **ID do cliente** (também referido como ID do pedido) e **Segredo do cliente**. Use o [ID do cliente e Segredo do cliente do aplicativo Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado para o AEM Forms.

1. Selecione o **[!UICONTROL Habilitar o Adobe Sign para anexos também]** opção para anexar arquivos anexados a um formulário adaptável ao formulário correspondente [!DNL Adobe Sign] documento enviado para assinatura.

1. Toque **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Sign] aplicativo.

1. Toque **[!UICONTROL Criar]** para criar o [!DNL Adobe Sign] configuração.

1. Abra AEM Console da Web. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abrir **[!UICONTROL Serviço de configuração comum do Forms].**
1. No **[!UICONTROL Permitir]** campo , **select** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar [!DNL Adobe Sign].
1. Publique a configuração.
1. Use [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=pt-BR) para criar configurações idênticas nas instâncias de publicação correspondentes.

Agora, [!DNL Adobe Sign] é integrado ao AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o contêiner de configuração criado acima nas propriedades do formulário adaptável.



## Configurar [!DNL Adobe Sign] agendador para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um [!DNL Adobe Sign] o formulário adaptável ativado é enviado somente após todos os signatários concluírem o processo de assinatura. Por padrão, a variável [!DNL Adobe Sign] Os serviços do agendador estão agendados para verificar (pesquisar) a resposta do assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Faça logon no AEM [!DNL Forms] servidor com credenciais de administrador e navegue até **Ferramentas** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra o **[!UICONTROL Serviço de configuração do Adobe Sign]** opção. Especifique um [expressão cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) no **[!UICONTROL Expressão do Scheduler de Atualização de Status]** e clique em **[!UICONTROL Salvar]**. Por exemplo, para executar o serviço de configuração diariamente às 00:00, especifique `0 0 0 1/1 * ? *` no **[!UICONTROL Expressão do Scheduler de Atualização de Status]** campo.

Intervalo padrão para sincronizar o status de [!DNL Adobe Sign] agora é alterada.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Uso do Adobe Sign com AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
