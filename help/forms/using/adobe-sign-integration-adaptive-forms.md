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
translation-type: tm+mt
source-git-commit: f0038c1f88ea0047cbaae4fe49456a665aa67f10
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---


# Integrar o Adobe Sign ao AEM Forms{#integrate-adobe-sign-with-aem-forms}

A Adobe Sign habilita workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras áreas.

Em um cenário típico de formulários adaptáveis e Adobe Sign, um usuário preenche um formulário adaptável para **solicitar um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviço para que seja tomada uma ação adicional. O provedor de serviço revisa o aplicativo e usa o Adobe Sign para marcar o aplicativo aprovado. Para habilitar workflows semelhantes de assinatura eletrônica, é possível integrar o Adobe Sign ao AEM Forms.

Para usar o Adobe Sign com o AEM Forms, configure o Adobe Sign nos serviços da AEM Cloud:

## Pré-requisitos {#prerequisites}

É necessário o seguinte para integrar o Adobe Sign à AEM Forms:

* Uma conta de desenvolvedor [Adobe Sign ativa.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um servidor AEM Forms habilitado para [SSL](/help/sites-administering/ssl-by-default.md) .
* Um aplicativo [API da](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)Adobe Sign.
* Credenciais (ID do cliente e segredo do cliente) do aplicativo da API Adobe Sign.
* Ao reconfigurar, remova a configuração existente do Adobe Sign das instâncias de autor e publicação.
* Use a chave [criptográfica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) idêntica para as instâncias de autor e publicação.

## Configurar o Adobe Sign com o AEM Forms {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem implementados, execute as seguintes etapas para configurar o Adobe Sign com o AEM Forms na instância Autor:

1. Na instância do autor do AEM Forms, navegue até **Ferramentas** ![martelo](assets/hammer.png) > **Geral** > Navegador **de** configuração.
1. Na página Navegador **[!UICONTROL de]** configuração, toque em **[!UICONTROL Criar]**.
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. Na caixa de diálogo **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative Configurações **[!UICONTROL da]** nuvem e toque em **[!UICONTROL Criar]**. Ele cria um container de configuração para serviços em nuvem.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **Cloud Services** > **Adobe Sign** e selecione o container de configuração criado na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um novo container de configuração e criar uma configuração Adobe Sign no container ou usar a `global` pasta existente em **Ferramentas** ![martelo](assets/hammer.png) > **Cloud Services** > **Adobe Sign**. Se você criar a configuração no novo container de configuração, especifique o nome do container no campo Container **** Configuração ao criar um formulário adaptável.

   >[!NOTE]
   Certifique-se de que o URL da página de configuração dos serviços em nuvem seja start com **HTTPS**. Caso contrário, [habilite o SSL](/help/sites-administering/ssl-by-default.md) para o servidor AEM Forms.

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar a configuração do Adobe Sign no AEM Forms.
1. Na guia **[!UICONTROL Geral]** da página **[!UICONTROL Criar configuração]** Adobe Sign, especifique um **Nome** para a configuração e toque em **Avançar**. Como opção, você pode especificar um título e navegar para selecionar uma miniatura para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. É necessário configurar o aplicativo Adobe Sign com o AEM Forms.

1. Defina as configurações OAuth para o aplicativo Adobe Sign:

   1. Abra uma janela do navegador e faça logon na conta do desenvolvedor Adobe Sign.
   1. Selecione o aplicativo configurado para AEM Forms e toque em Configurar OAuth para Aplicativo.
   1. Na caixa **Redirecionar URL** , adicione o URL HTTPS copiado na etapa anterior e clique em **Salvar**.
   1. Ative as seguintes configurações OAuth para o aplicativo Adobe Sign e clique em **Salvar**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obter informações detalhadas sobre como configurar as configurações OAuth para um aplicativo Adobe Sign e obter as chaves, consulte [Configurar as configurações de Auth para a documentação do desenvolvedor do aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) .

   ![Configuração do OAuth](assets/oauthconfig_new.png)

1. Volte para a página **Criar configuração** Adobe Sign. Na guia **[!UICONTROL Configurações]** , o campo URL **** OAuth menciona o seguinte URL padrão:

   https://secure.na1.echosign.com/public/oauth

   em que:

   **na1** refere-se ao compartilhamento de banco de dados padrão.

   Você pode modificar o valor do compartilhamento de banco de dados. Reinicie o servidor para poder usar o novo valor para o compartilhamento do banco de dados.

1. Especifique a ID **do** cliente (também chamada de ID da aplicação) e o segredo do **cliente**. Selecione a opção **Habilitar Adobe Sign para anexos também** para anexar arquivos conectados a um formulário adaptável ao documento Adobe Sign correspondente enviado para assinatura.

   Tap **[!UICONTROL Connect to Adobe Sign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo Adobe Sign.

   Toque em **[!UICONTROL Criar]** para criar a configuração do Adobe Sign.

1. Abra AEM Web Console. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abra o Serviço de configuração comum **Forms.**
1. No campo **Permitir** , **selecione** Todos os usuários - Todos os usuários, anônimos ou conectados, podem pré-visualização anexos, verificar e assinar formulários e clique em **Salvar.** A instância do autor está configurada para usar o Adobe Sign.
1. Publique a configuração.
1. Use a [replicação](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) para criar configurações idênticas em instâncias de publicação correspondentes.

Agora, a Adobe Sign está integrada ao AEM Forms e pronta para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)adaptável, especifique o container de configuração criado acima nas propriedades de formulário adaptável.



## Configurar o scheduler Adobe Sign para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um formulário adaptativo habilitado para Adobe Sign é enviado somente depois que todos os signatários concluírem o processo de assinatura. Por padrão, os serviços do Scheduler Adobe Sign estão programados para verificar (pesquisar) a resposta do assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Faça logon no servidor AEM Forms com credenciais de administrador e navegue até **Ferramentas** > **Operações** > Console **da** Web.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra a opção **Adobe Sign Configuration Service** . Especifique uma expressão [de](https://en.wikipedia.org/wiki/Cron#CRON_expression) cron no campo Expressão **Scheduler** Atualização de status e clique em **Salvar**. Por exemplo, para executar o serviço de configuração diariamente às 00:00, especifique `0 0 0 1/1 * ? *` o campo Expressão **Scheduler Atualização de** status.

O intervalo padrão para o status de sincronização do Adobe Sign agora é alterado.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Uso do Adobe Sign com AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

