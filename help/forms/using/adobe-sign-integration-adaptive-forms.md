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

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um [!DNL Adobe Acrobat Sign] e Adaptive Forms, um usuário preenche um Formulário adaptável para solicitar um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços analisa o aplicativo e usa [!DNL Adobe Acrobat Sign] para marcar o pedido como aprovado. O AEM Forms é compatível com Adobe Acrobat Sign e Adobe Acrobat Sign Solutions para o governo. Dependendo da sua licença e dos requisitos, você pode integrar ou conectar o AEM Forms a qualquer uma das soluções:

* [Conectar o AEM Forms com o Adobe Acrobat Sign](#adobe-sign)
* [Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo](#adobe-acrobat-sign-for-government)

## Conectar o AEM Forms com o Adobe Acrobat Sign {#adobe-sign}

Para conectar **[!DNL AEM Forms]** com **[!DNL Adobe Acrobat Sign]**, configure o software e as contas listados na seção de pré-requisitos e conecte o Adobe Sign a todas as instâncias do AEM Forms Author e do Publish:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar [!DNL Adobe Sign] com AEM [!DNL Forms]:

* Um ativo [Conta de desenvolvedor do Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Um [SSL habilitado](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] servidor.
* Um [aplicativo da API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e segredo do cliente) de [!DNL Adobe Sign] aplicativo da API.
* Ao reconfigurar, remova as existentes [!DNL Adobe Sign] configuração das instâncias do autor e de publicação.
* Uso [chave criptográfica idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.

## Configurar [!DNL Adobe Sign] com AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com AEM [!DNL Forms] na instância do Autor:

1. No AEM [!DNL Forms] instância do autor, navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** selecione **[!UICONTROL Criar]**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** e selecione o contêiner de configuração que você criou na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um contêiner de configuração e criar um [!DNL Adobe Sign] no contêiner ou use o existente `global` pasta em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo container de configuração, certifique-se de especificar o nome do container no **[!UICONTROL Contêiner de configuração]** ao criar um Formulário adaptável.

   >[!NOTE]
   >
   Verifique se o URL da página de configuração do Cloud Service começa com **HTTPS**. Caso contrário, [ativar SSL](/help/sites-administering/ssl-by-default.md) para AEM [!DNL Forms] servidor.


1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Sign] configuração no AEM [!DNL Forms].
1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um título e procurar para selecionar uma miniatura para a configuração.
1. Agora é possível **[!UICONTROL Selecionar solução]** para selecionar [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. Copie o URL na janela atual do navegador para um bloco de notas e remova a parte /`ui#/aem` do URL. O URL modificado é então necessário para configurar o [!DNL Adobe Acrobat Sign] aplicativo com [!DNL AEM Forms], em uma etapa posterior. Toque [!UICONTROL Próxima].

1. No **[!UICONTROL Configurações]** guia,
   * o **[!UICONTROL URL do OAuth]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/public/oauth/v2`

     Por exemplo:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * o **[!UICONTROL URL do token de acesso]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/oauth/v2/token`

     Por exemplo:
     `https://api.na1.echosign.com/oauth/v2/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Acrobat Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * Mantenha a **Criar configuração do Adobe Acrobat Sign** página aberta. Não feche. Você pode recuperar **ID do cliente** e **Segredo do cliente** após definir as configurações de OAuth para o [!DNL Adobe Acrobat Sign] conforme descrito nas próximas etapas.
   * Depois de fazer logon na conta da Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação de Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar informações relacionadas ao URL do OAuth e ao URL do token de acesso do Adobe Sign.

1. Defina as configurações de OAuth para o [!DNL Adobe Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon na [!DNL Adobe Sign] conta de desenvolvedor.
   1. Selecione o aplicativo configurado para AEM [!DNL Forms]e selecione **[!UICONTROL Configurar OAuth para Aplicativo]**.
   1. Copie o **[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]** em um bloco de notas.
   1. No **[!UICONTROL URL de redirecionamento]** adicione o URL HTTPS copiado na etapa anterior.
   1. Ative as seguintes configurações do OAuth para o [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Para obter informações passo a passo sobre como definir as configurações de OAuth para um [!DNL Adobe Sign] e obter as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentação do desenvolvedor.

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

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** especifique a **ID do cliente** (também conhecido como ID do aplicativo) e **Segredo do cliente**. Use o [ID do cliente e segredo do cliente do aplicativo Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado para o AEM Forms.

1. Selecione o **[!UICONTROL Ativar Adobe Sign também para anexos]** opção para anexar arquivos anexados a um formulário adaptável ao formulário correspondente [!DNL Adobe Sign] documento enviado para assinatura.

1. Selecionar **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Sign] aplicação.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](assets/adobe-sign-cloud-configuration-success.png)

1. Toque **[!UICONTROL Criar]** para criar o [!DNL Adobe Sign] configuração.
1. Abra o console da Web AEM. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abertura **[!UICONTROL Serviço de configuração comum do Forms].**
1. No **[!UICONTROL Permitir]** campo, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar [!DNL Adobe Sign].
1. Publish da configuração.
1. Uso [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) para criar configurações idênticas nas instâncias de publicação correspondentes.

Agora, [!DNL Adobe Sign] é integrado ao AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o container de configuração criado acima nas propriedades do formulário adaptável.

>[!NOTE]
>
Para configurar a sandbox da Adobe Sign, você pode seguir as mesmas etapas de configuração descritas em [Adobe Sign](#adobe-sign).

## Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo {#adobe-acrobat-sign-for-government}

A conexão do AEM Forms com o Adobe Acrobat Sign Solutions para o governo é um processo de várias etapas. Envolve:

* Criação de um URL de redirecionamento para suas instâncias do AEM
* Compartilhamento do URL de redirecionamento e escopos com a equipe do Adobe Sign Solutions for Government
* Recebimento de credenciais da equipe do Adobe Sign
* Usar as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Antes de começar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Antes de começar a conectar o AEM Forms com a solução da Adobe Acrobat Sign,

* Verifique se [Adobe Acrobat Sign Solutions para o governo](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) conta provisionada.
* Seu AEM [!DNL Forms] servidores são [SSL habilitado](/help/sites-administering/ssl-by-default.md) .
* Seu AEM [!DNL Forms] os servidores estão usando [chave criptográfica idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.

### Conectar o AEM Forms ao Adobe Acrobat Sign Solutions para o governo {#connect-adobe-acrobat-sign-for-government}

#### Criar um URL de redirecionamento para sua instância do AEM

1. Na sua instância do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração. Certifique-se de que o nome do contêiner/pasta não contenha nenhum espaço.

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e abra o container de configuração criado na etapa anterior. Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.
1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar [!DNL Adobe Acrobat Sign] configuração no AEM Forms.
1. Copie o URL da janela do navegador atual para um bloco de notas do URL. Esse URL é chamado de `re-direct URL`. Na próxima seção, você compartilhará o `re-direct URL` e `Scopes` com a equipe do Adobe Sign e solicite credenciais (ID do cliente e Segredo do cliente).

>[!NOTE]
>
>
* A `re-direct URL` deve conter uma [Nível superior](https://en.wikipedia.org/wiki/Top-level_domain) domínio. Por exemplo, `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* Não use um URL local como `re-direct URL`. Por exemplo, `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Compartilhar a URL de redirecionamento e os escopos com a equipe do Adobe Sign e receber credenciais

A equipe de soluções da Adobe Acrobat Sign para o governo exige a `re-direct URL` e os escopos específicos a serem ativados para que o aplicativo Adobe Acrobat Sign (listado abaixo) gere credenciais (ID do cliente e Segredo do cliente) que permitem conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government.

Compartilhe o `scopes` (listadas abaixo) e o `re-direct URL` criou e anotou a última etapa da seção anterior com seu representante de soluções para o governo da Adobe Acrobat Sign [Membro da equipe do Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

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

1. Abra o `re-direct URL` no navegador. Você criou e anotou o `re-direct URL` na última etapa do [criar um URL de redirecionamento na sua instância do AEM](#create-redirect-url) seção.

1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e selecione **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]** e navegue para selecionar um **[!UICONTROL Miniatura]** para a configuração. Clique em **[!UICONTROL Avançar]**.

1. No **[!UICONTROL Configurações]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, para o **[!UICONTROL Selecionar solução]** selecione [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions para o governo](/help/forms/using/assets/adobe-sign-for-govt.png)

1. No **[!UICONTROL E-mail]** especifique o endereço de email associado à sua conta do Adobe Acrobat Sign Solutions for Government.

1. No **[!UICONTROL Configurações]** guia,
   * o **[!UICONTROL URL do OAuth]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * o **[!UICONTROL URL do token de acesso]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Acrobat Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * Depois de fazer logon na conta da Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação de Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar informações relacionadas ao URL do Adobe Sign oAuth e ao URL do token de acesso.

1. Usar as credenciais compartilhadas pela Adobe Acrobat Sign para o representante de soluções do governo ([Membro da equipe do Adobe Professional Services]) na seção anterior como [**[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]**].

1. Selecione o **[!UICONTROL Ativar Adobe Acrobat Sign para anexos]** opção para anexar arquivos anexados a um Formulário adaptável aos arquivos correspondentes [!DNL Adobe Acrobat Sign] documento enviado para assinatura.

1. Selecionar **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando for solicitado que você confirme o acesso de `Adobe Acrobat Sign for Government Solutions` e , clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar o [!DNL Adobe Acrobat Sign] conta de desenvolvedor, uma mensagem de sucesso semelhante à seguinte é exibida.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando for solicitado que você confirme o acesso de `your account`e clique em **[!UICONTROL Permitir acesso]**.

1. Selecionar **[!UICONTROL Criar]** para criar a configuração.
1. Abra o console da Web AEM. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abertura **[!UICONTROL Serviço de configuração comum do Forms].**
1. No **[!UICONTROL Permitir]** campo, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar [!DNL Adobe Sign].

1. Publish da configuração.
1. Uso [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) para criar configurações idênticas nas instâncias de publicação correspondentes.

Agora, você pode [usar a opção adicionar campos do Adobe Acrobat Sign em um Formulário adaptável](working-with-adobe-sign.md) ou [Fluxo de trabalho do AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Adicione o contêiner de configuração usado para a configuração do Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL Adobe Acrobat Sign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.


## Configurar [!DNL Adobe Sign] scheduler para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Um [!DNL Adobe Sign] o formulário adaptável ativado é enviado somente depois que todos os signatários concluírem o processo de assinatura. Por padrão, a variável [!DNL Adobe Sign] Os serviços do agendador estão agendados para verificar (enquete) a resposta do assinante a cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente. Execute as seguintes etapas para alterar o intervalo padrão:

1. Fazer logon no AEM [!DNL Forms] servidor com credenciais de administrador e navegue até **Ferramentas** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   Você também pode abrir o seguinte URL em uma janela do navegador:
   `https://[localhost]:'port'/system/console/configMgr`

1. Localize e abra o **[!UICONTROL Serviço de configuração do Adobe Sign]** opção. Especificar um [expressão CRON](https://en.wikipedia.org/wiki/Cron#CRON_expression) no **[!UICONTROL Expressão do Agendador de Atualização de Status]** e clique em **[!UICONTROL Salvar]**. Por exemplo, para executar o serviço de configuração diariamente às 0h, especifique `0 0 0 1/1 * ? *` no **[!UICONTROL Expressão do Agendador de Atualização de Status]** campo.

Intervalo padrão para sincronizar o status de [!DNL Adobe Sign] foi alterado.

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign com fluxos de trabalho centrados em formulários](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Utilização do Adobe Sign com o AEM Forms (Vídeo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
