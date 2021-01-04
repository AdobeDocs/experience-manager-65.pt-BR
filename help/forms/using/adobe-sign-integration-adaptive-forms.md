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
source-git-commit: 93ee9338fc2e78d01a9b62e8040c4674262ef6be
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# Integrar [!DNL Adobe Sign] com AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] habilita workflows de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os workflows para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras áreas.

Em um cenário típico de [!DNL Adobe Sign] e formulários adaptáveis, um usuário preenche um formulário adaptável para **se aplicar a um serviço**. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviço para que seja tomada uma ação adicional. O provedor de serviço revisa o aplicativo e usa [!DNL Adobe Sign] para marcar o aplicativo aprovado. Para ativar workflows semelhantes de assinatura eletrônica, é possível integrar [!DNL Adobe Sign] com AEM [!DNL Forms].

Para usar [!DNL Adobe Sign] com AEM [!DNL Forms], configure [!DNL Adobe Sign] nos serviços da AEM Cloud:

## Pré-requisitos {#prerequisites}

É necessário o seguinte para integrar [!DNL Adobe Sign] com AEM [!DNL Forms]:

* Uma conta de desenvolvedor ativa [Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um servidor [SSL habilitado](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Um [aplicativo da API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e segredo do cliente) do aplicativo da API [!DNL Adobe Sign].
* Ao reconfigurar, remova a configuração [!DNL Adobe Sign] existente das instâncias de autor e publicação.
* Use [chave criptográfica idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de autor e publicação.

## Configurar [!DNL Adobe Sign] com AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com AEM [!DNL Forms] na instância do autor:

1. Na instância do autor AEM [!DNL Forms], navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.
1. Na página **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
   * Consulte a documentação [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Na caixa de diálogo **[!UICONTROL Criar configuração]**, especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações de nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um container de configuração para serviços em nuvem.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e selecione o container de configuração criado na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1-4 para criar um novo container de configuração e uma configuração [!DNL Adobe Sign] no container ou usar a pasta `global` existente em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo container de configuração, especifique o nome do container no campo **[!UICONTROL Container de configuração]** ao criar um formulário adaptável.

   >[!NOTE]
   Certifique-se de que o URL da página de configuração dos serviços em nuvem seja start com **HTTPS**. Caso contrário, [ative SSL](/help/sites-administering/ssl-by-default.md) para AEM servidor [!DNL Forms].

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign] no AEM [!DNL Forms].
1. Na guia **[!UICONTROL Geral]** da página **[!UICONTROL Criar Configuração do Adobe Sign]**, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próximo]**. Como opção, você pode especificar um título e navegar para selecionar uma miniatura para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. É necessário configurar o aplicativo [!DNL Adobe Sign] com AEM[!DNL Forms].

1. Defina as configurações OAuth para o aplicativo [!DNL Adobe Sign]:

   1. Abra uma janela do navegador e faça logon na conta do desenvolvedor [!DNL Adobe Sign].
   1. Selecione o aplicativo configurado para AEM [!DNL Forms] e toque em **[!UICONTROL Configurar OAuth para Application]**.
   1. Copie as **[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]** para um bloco de notas.
   1. Na caixa **[!UICONTROL Redirecionar URL]**, adicione o URL HTTPS copiado na etapa anterior.
   1. Ative as seguintes configurações OAuth para o aplicativo [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Para obter informações passo a passo sobre como configurar o OAuth para um aplicativo [!DNL Adobe Sign] e obter as chaves, consulte [Configurar as configurações de Auth para a documentação do desenvolvedor do aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuração do OAuth](assets/oauthconfig_new.png)

1. Volte para a página **[!UICONTROL Criar Configuração do Adobe Sign]**. Na guia **[!UICONTROL Settings]**, o campo **[!UICONTROL URL OAuth]** menciona o seguinte URL padrão:

   https://secure.na1.echosign.com/public/oauth

   em que:

   **na1** refere-se ao compartilhamento de banco de dados padrão.

   Você pode modificar o valor do compartilhamento de banco de dados. Reinicie o servidor para poder usar o novo valor para o compartilhamento do banco de dados.

1. Especifique a **ID do cliente** (também chamada de ID da aplicação) e **Segredo do cliente** copiados na etapa 8. Selecione a opção **[!UICONTROL Habilitar Adobe Sign para anexos também]** para anexar arquivos anexados a um formulário adaptável ao documento [!DNL Adobe Sign] correspondente enviado para assinatura.

   Toque em **[!UICONTROL Ligar ao Adobe Sign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL Adobe Sign].

   Toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign].

1. Abra AEM Web Console. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abra **[!UICONTROL Forms Common Configuration Service].**
1. No campo **[!UICONTROL Permitir]**, **selecione** Todos os usuários - Todos os usuários, anônimos ou conectados, podem pré-visualização anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar  [!DNL Adobe Sign].
1. Publique a configuração.
1. Use [replicação](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) para criar configuração idêntica em instâncias de publicação correspondentes.

Agora, [!DNL Adobe Sign] é integrado ao AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o container de configuração criado acima nas propriedades de formulário adaptável.



## Configure o scheduler [!DNL Adobe Sign] para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um formulário adaptativo habilitado para [!DNL Adobe Sign] é enviado somente depois que todos os signatários concluírem o processo de assinatura. Por padrão, os serviços de Scheduler [!DNL Adobe Sign] estão programados para verificar (pesquisar) a resposta do assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Faça logon no servidor [!DNL Forms] AEM com credenciais de administrador e navegue até **Ferramentas** > **[!UICONTROL Operações]** > **[!UICONTROL Console Web]**.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra a opção **[!UICONTROL Adobe Sign Configuration Service]**. Especifique uma [expressão cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) no campo **[!UICONTROL Expressão Scheduler de Atualização de Estado]** e clique em **[!UICONTROL Guardar]**. Por exemplo, para executar o serviço de configuração diariamente às 00:00 am, especifique `0 0 0 1/1 * ? *` no campo **[!UICONTROL Expressão de Scheduler de Atualização de Status]**.

O intervalo padrão para o status de sincronização de [!DNL Adobe Sign] agora é alterado.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Uso do Adobe Sign com AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

