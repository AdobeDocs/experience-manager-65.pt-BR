---
title: Integrar o Adobe Sign com o AEM Forms
description: Saiba como configurar o Adobe Sign para seu AEM Adaptive Forms. O Adobe Sign melhora o fluxo de trabalho e processa os documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components,Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Integrar [!DNL Adobe Sign] com AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=pt-BR#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um cenário típico do [!DNL Adobe Acrobat Sign] e do Adaptive Forms, um usuário preenche um Formulário adaptável para se candidatar a um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços revisa o aplicativo e usa [!DNL Adobe Acrobat Sign] para marcar o aplicativo como aprovado. O AEM Forms é compatível com Adobe Acrobat Sign e Adobe Acrobat Sign Solutions para o governo. Dependendo da sua licença e dos requisitos, você pode integrar ou conectar o AEM Forms a qualquer uma das soluções:

* [Conectar o AEM Forms com o Adobe Acrobat Sign](#adobe-sign)
* [Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo](#adobe-acrobat-sign-for-government)

## Conectar o AEM Forms com o Adobe Acrobat Sign {#adobe-sign}

Para conectar o **[!DNL AEM Forms]** ao **[!DNL Adobe Acrobat Sign]**, configure o software e as contas listados na seção de pré-requisitos e conecte o Adobe Sign a todas as instâncias do AEM Forms Author e do Publish:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar o [!DNL Adobe Sign] ao AEM [!DNL Forms]:

* Uma conta de desenvolvedor [Adobe Sign ativa.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um servidor [habilitado para SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Um [aplicativo de API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do Cliente e Segredo do Cliente) do aplicativo da API [!DNL Adobe Sign].
* Ao reconfigurar, remova a configuração [!DNL Adobe Sign] existente das instâncias do autor e de publicação.
* Use [chave de criptografia idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para as instâncias de autor e publicação.

## Configurar [!DNL Adobe Sign] com AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar o [!DNL Adobe Sign] com AEM [!DNL Forms] na instância do Autor:

1. Na instância do autor do AEM [!DNL Forms], navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.
1. Na página **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
   * Consulte a documentação do [Navegador de Configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um **[!UICONTROL Título]** para a configuração, habilite as **[!UICONTROL Configurações de Nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** e selecione o contêiner de configuração criado na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um contêiner de configuração e criar uma configuração [!DNL Adobe Sign] no contêiner ou usar a pasta `global` existente em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo contêiner de configuração, certifique-se de especificar o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]** ao criar um Formulário adaptável.

   >[!NOTE]
   >
   >Verifique se a URL da Página de Configuração do Cloud Service começa com **HTTPS**. Caso contrário, [habilite o SSL](/help/sites-administering/ssl-by-default.md) para o servidor AEM [!DNL Forms].


1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign] no AEM [!DNL Forms].
1. Na guia **[!UICONTROL Geral]** da página **[!UICONTROL Criar configuração do Adobe Sign]**, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Avançar]**. Opcionalmente, é possível especificar um título e procurar para selecionar uma miniatura para a configuração.
1. Agora você pode **[!UICONTROL Selecionar solução]** para selecionar [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. Copie a URL na janela do navegador atual para um bloco de notas e remova a parte /`ui#/aem` da URL. A URL modificada é então necessária para configurar o aplicativo [!DNL Adobe Acrobat Sign] com [!DNL AEM Forms], em uma etapa posterior. Toque em [!UICONTROL Próximo].

1. Na guia **[!UICONTROL Configurações]**,
   * o campo **[!UICONTROL URL do OAuth]** contém a URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/public/oauth/v2`

     Por exemplo:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * o campo **[!UICONTROL URL do token de acesso]** contém a URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/oauth/v2/token`

     Por exemplo:
     `https://api.na1.echosign.com/oauth/v2/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Verifique se as Configurações de Nuvem do [!DNL &#x200B; Adobe Acrobat Sign] apontam para o [Fragmento correto](https://helpx.adobe.com/br/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Mantenha aberta a página **Criar configuração do Adobe Acrobat Sign**. Não feche. Você pode recuperar a **ID do Cliente** e o **Segredo do Cliente** após definir as configurações OAuth para o aplicativo [!DNL Adobe Acrobat Sign] conforme descrito nas próximas etapas.
   >* Depois de fazer logon na conta do Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação dos Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar as informações relacionadas à URL do OAuth e à URL do Token de Acesso do Adobe Sign.

1. Defina as configurações de OAuth para o aplicativo [!DNL Adobe Sign]:

   1. Abra uma janela de navegador e entre na conta de desenvolvedor do [!DNL Adobe Sign].
   1. Selecione o aplicativo configurado para AEM [!DNL Forms] e selecione **[!UICONTROL Configurar OAuth para o Aplicativo]**.
   1. Copie a **[!UICONTROL ID do Cliente]** e o **[!UICONTROL Segredo do Cliente]** em um bloco de notas.
   1. Na caixa **[!UICONTROL Redirecionar URL]**, adicione o URL HTTPS copiado na etapa anterior.
   1. Habilite as seguintes configurações OAuth para o aplicativo [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Para obter informações passo a passo sobre como definir as configurações OAuth para um aplicativo [!DNL Adobe Sign] e obter as chaves, consulte [Definir configurações oAuth para a documentação do desenvolvedor do aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuração do OAuth](assets/oauthconfig_new.png)

<!--
1. Go back to the **[!UICONTROL Create Adobe Sign Configuration]** page. In the **[!UICONTROL Settings]** tab, the **[!UICONTROL OAuth URL]** field mentions the  default URL. The format of the URL is:

   `https://<shard>/public/oAuth/v2`

   For example: 
   `https://secure.na1.echosign.com/public/oauth/v2`

   where:

   **na1** refers to the default database shard.

   You can modify the value for the database shard. Restart the server to be able to use the new value for the database shard.

   >[!NOTE]
   >
   >Ensure that your author and publish instance configurations point to the same shard. If you create multiple Adobe Sign configurations for an organization, ensure all the configurations utilize the same shard. -->

1. Volte para a página **[!UICONTROL Criar configuração do Adobe Sign]**. Na guia **[!UICONTROL Configurações]**, especifique a **ID do Cliente** (também conhecida como ID do Aplicativo) e o **Segredo do Cliente**. Use a [ID do Cliente e o Segredo do Cliente do aplicativo Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado para o AEM Forms.

1. Selecione a opção **[!UICONTROL Habilitar Adobe Sign para anexos também]** para anexar arquivos anexados a um formulário adaptável ao documento [!DNL Adobe Sign] correspondente enviado para assinatura.

1. Selecione **[!UICONTROL Conectar ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL Adobe Sign].

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](assets/adobe-sign-cloud-configuration-success.png)

1. Toque em **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Sign].
1. Abra o console da Web AEM. A URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abra o **[!UICONTROL Serviço de Configuração Comum do Forms].**
1. No campo **[!UICONTROL Permitir]**, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].A instância do Autor** está configurada para usar [!DNL Adobe Sign].
1. Publish da configuração.
1. Use a [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=pt-BR) para criar configuração idêntica nas instâncias de publicação correspondentes.

Agora, o [!DNL Adobe Sign] está integrado ao AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o contêiner de configuração criado acima nas propriedades do formulário adaptável.

>[!NOTE]
>
>Para configurar a sandbox do Adobe Sign, você pode seguir as mesmas etapas de configuração descritas em [Adobe Sign](#adobe-sign).

## Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo {#adobe-acrobat-sign-for-government}

A conexão do AEM Forms com o Adobe Acrobat Sign Solutions para o governo é um processo de várias etapas. Envolve:

* Criação de um URL de redirecionamento para suas instâncias do AEM
* Compartilhamento do URL de redirecionamento e escopos com a equipe do Adobe Sign Solutions for Government
* Recebimento de credenciais da equipe do Adobe Sign
* Usar as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Antes de começar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Antes de começar a conectar o AEM Forms com a solução da Adobe Acrobat Sign,

* Verifique se a sua conta do [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) foi provisionada.
* Seus servidores AEM [!DNL Forms] estão [habilitados para SSL](/help/sites-administering/ssl-by-default.md).
* Seus servidores AEM [!DNL Forms] estão usando [chave criptográfica idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para as instâncias de autoria e publicação.

### Conectar o AEM Forms ao Adobe Acrobat Sign Solutions para o governo {#connect-adobe-acrobat-sign-for-government}

#### Criar um URL de redirecionamento para sua instância do AEM

1. Na sua instância do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.
1. Na página **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um **[!UICONTROL Título]** para a configuração, habilite as **[!UICONTROL Configurações de Nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração. Certifique-se de que o nome do contêiner/pasta não contenha nenhum espaço.

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e abra o contêiner de configuração criado na etapa anterior. Ao criar um Formulário adaptável, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]**.
1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL Adobe Acrobat Sign] no AEM Forms.
1. Copie o URL da janela do navegador atual para um bloco de notas do URL. Esta URL é referida como `re-direct URL`. Na próxima seção, você compartilha o `re-direct URL` e o `Scopes` com a equipe da Adobe Sign e solicita credenciais (ID do cliente e Segredo do cliente).

>[!NOTE]
>
>
>* Um `re-direct URL` deve conter um domínio [de nível superior](https://en.wikipedia.org/wiki/Top-level_domain). Por exemplo, `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
>* Não use uma URL local como um `re-direct URL`. Por exemplo, `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Compartilhar a URL de redirecionamento e os escopos com a equipe do Adobe Sign e receber credenciais

A equipe do Adobe Acrobat Sign for Government Solutions exige que o `re-direct URL` e determinados escopos sejam habilitados para que seu aplicativo Adobe Acrobat Sign (listado abaixo) gere credenciais (ID do cliente e Segredo do cliente) que permitam conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government.

Compartilhe o `scopes` (listado abaixo) e o `re-direct URL` criado e anotado na última etapa da seção anterior com o representante de Soluções para o Governo da Adobe Acrobat Sign [membro da equipe da Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_Escopos_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

O representante gera e compartilha credenciais com você. Na próxima seção, use as credenciais (ID do cliente e Segredo do cliente) para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government.

#### Use as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

1. Abra o `re-direct URL` no navegador. Você criou e anotou o `re-direct URL` na última etapa da seção [criar uma URL de redirecionamento na sua instância do AEM](#create-redirect-url).

1. Na guia **[!UICONTROL Geral]** da página **[!UICONTROL Criar configuração do Adobe Sign]**, especifique um **[!UICONTROL Nome]** para a configuração e selecione **[!UICONTROL Avançar]**. Opcionalmente, você pode especificar um **[!UICONTROL Título]** e procurar para selecionar uma **[!UICONTROL Miniatura]** para a configuração. Clique em **[!UICONTROL Avançar]**.

1. Na guia **[!UICONTROL Configurações]** da página **[!UICONTROL Criar Configuração do Adobe Sign]**, para a opção **[!UICONTROL Selecionar solução]**, selecione [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions para o governo](/help/forms/using/assets/adobe-sign-for-govt.png)

1. No campo **[!UICONTROL Email]**, especifique o endereço de email associado à sua conta do Adobe Acrobat Sign Solutions for Government.

1. Na guia **[!UICONTROL Configurações]**,
   * o campo **[!UICONTROL URL do OAuth]** contém a URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * o campo **[!UICONTROL URL do token de acesso]** contém a URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Verifique se as Configurações de Nuvem do [!DNL &#x200B; Adobe Acrobat Sign] apontam para o [Fragmento correto](https://helpx.adobe.com/br/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Depois de fazer logon na conta do Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação dos Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar as informações relacionadas à URL do Adobe Sign oAuth e à URL do Token de acesso.

1. Use as credenciais compartilhadas pela Adobe Acrobat Sign para o representante de Solução Governamental ([membro da equipe da Adobe Professional Services]) na seção anterior como [**[!UICONTROL ID do Cliente]** e **[!UICONTROL Segredo do Cliente]**].

1. Selecione a opção **[!UICONTROL Habilitar Adobe Acrobat Sign para anexos]** para anexar arquivos anexados a um Formulário Adaptável ao documento [!DNL Adobe Acrobat Sign] correspondente enviado para assinatura.

1. Selecione **[!UICONTROL Conectar ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL Adobe Acrobat Sign]. Quando solicitado a confirmar o acesso para `Adobe Acrobat Sign for Government Solutions` e , clique em **[!UICONTROL Permitir Acesso]**. Se as credenciais estiverem corretas e você permitir que o [!DNL AEM Forms] acesse sua conta de desenvolvedor do [!DNL Adobe Acrobat Sign], uma mensagem de êxito semelhante à seguinte será exibida.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL Adobe Acrobat Sign]. Quando solicitado a confirmar o acesso para `your account`, clique em **[!UICONTROL Permitir Acesso]**.

1. Selecione **[!UICONTROL Criar]** para criar a configuração.
1. Abra o console da Web AEM. A URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abra o **[!UICONTROL Serviço de Configuração Comum do Forms].**
1. No campo **[!UICONTROL Permitir]**, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].A instância do Autor** está configurada para usar [!DNL Adobe Sign].

1. Publish da configuração.
1. Use a [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=pt-BR) para criar configuração idêntica nas instâncias de publicação correspondentes.

Agora você pode [usar a opção adicionar campos do Adobe Acrobat Sign em um Formulário Adaptável](working-with-adobe-sign.md) ou o [Fluxo de Trabalho do AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Adicione o contêiner de configuração usado para a configuração Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL Adobe Acrobat Sign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.


## Configurar o agendador [!DNL Adobe Sign] para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um formulário adaptável habilitado para [!DNL Adobe Sign] é enviado somente depois que todos os signatários concluírem o processo de assinatura. Por padrão, os serviços do Agendador do [!DNL Adobe Sign] estão agendados para verificar (sondar) a resposta do assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Faça logon no servidor AEM [!DNL Forms] com credenciais de administrador e navegue até **Ferramentas** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra a opção **[!UICONTROL Serviço de Configuração do Adobe Sign]**. Especifique uma [expressão cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) no campo **[!UICONTROL Expressão do Agendador de Atualização de Status]** e clique em **[!UICONTROL Salvar]**. Por exemplo, para executar o serviço de configuração diariamente às 00:00, especifique `0 0 0 1/1 * ? *` no campo **[!UICONTROL Expressão do Agendador de Atualização de Status]**.

O intervalo padrão para sincronizar o status de [!DNL Adobe Sign] foi alterado.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign com fluxos de trabalho centrados em formulários](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Usando o Adobe Sign com o AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
