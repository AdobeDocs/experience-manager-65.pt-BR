---
title: Integrar o Adobe Sign com o AEM Forms
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
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 2%

---

# Integrar [!DNL Adobe Sign] com AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para formulários adaptáveis. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um [!DNL Adobe Acrobat Sign] e Adaptive Forms, um usuário preenche um Formulário adaptável para solicitar um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços analisa o aplicativo e usa [!DNL Adobe Acrobat Sign] para marcar o pedido como aprovado. O AEM Forms é compatível com Adobe Acrobat Sign e Adobe Acrobat Sign Solutions para o governo. Dependendo da sua licença e dos requisitos, você pode integrar ou conectar o AEM Forms a qualquer uma das soluções:

* [Conectar o AEM Forms com o Adobe Acrobat Sign](#adobe-sign)
* [Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo](#adobe-acrobat-sign-for-government)

## Conectar o AEM Forms com o Adobe Acrobat Sign {#adobe-sign}

Para conectar **[!DNL AEM Forms]** com **[!DNL Adobe Acrobat Sign]**, configure o software e as contas listados na seção de pré-requisitos e conecte o Adobe Sign a todas as instâncias de Autor e Publicação do AEM Forms:

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
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração.
1. Navegue até **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e selecione o contêiner de configuração que você criou na etapa acima.

   >[!NOTE]
   >
   >Você pode executar as etapas 1 a 4 para criar um novo contêiner de configuração e criar um [!DNL Adobe Sign] no contêiner ou use o existente `global` pasta em **Ferramentas** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se você criar a configuração no novo container de configuração, certifique-se de especificar o nome do container no **[!UICONTROL Contêiner de configuração]** ao criar um formulário adaptável.

   >[!NOTE]
   >
   Verifique se o URL da página de configuração do Cloud Services começa com **HTTPS**. Caso contrário, [ativar SSL](/help/sites-administering/ssl-by-default.md) para AEM [!DNL Forms] servidor.

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Sign] configuração no AEM [!DNL Forms].
1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um título e procurar para selecionar uma miniatura para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. É necessário configurar [!DNL Adobe Sign] aplicativo com AEM[!DNL Forms].

1. No **[!UICONTROL Configurações]** , a guia **[!UICONTROL URL do OAuth]** contém o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se você criar outro [!DNL Adobe Sign] para um recurso ou componente do Adobe Experience Manager, verifique se todas as [!DNL Adobe Sign] As configurações de nuvem apontam para o mesmo fragmento.

   >[!NOTE]
   >
   Mantenha a **Criar configuração do Adobe Sign** página aberta. Não feche. Você pode recuperar **ID do cliente** e **Segredo do cliente** após definir as configurações de OAuth para o [!DNL Adobe Sign] conforme descrito nas próximas etapas.


1. Defina as configurações de OAuth para o [!DNL Adobe Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon na [!DNL Adobe Sign] conta de desenvolvedor.
   1. Selecione o aplicativo configurado para AEM [!DNL Forms]e toque em **[!UICONTROL Configurar OAuth para Aplicativo]**.
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

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** , a guia **[!UICONTROL URL do OAuth]** menciona o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão.

   Você pode modificar o valor do fragmento de banco de dados. Reinicie o servidor para poder usar o novo valor para o fragmento de banco de dados.

   >[!NOTE]
   >
   Certifique-se de que as configurações da instância do autor e de publicação apontem para o mesmo fragmento. Se você criar várias configurações do Adobe Sign para uma organização, verifique se todas as configurações utilizam o mesmo fragmento.

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** especifique a **ID do cliente** (também conhecido como ID do aplicativo) e **Segredo do cliente**. Use o [ID do cliente e segredo do cliente do aplicativo Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado para o AEM Forms.

1. Selecione o **[!UICONTROL Ativar Adobe Sign também para anexos]** opção para anexar arquivos anexados a um formulário adaptável ao formulário correspondente [!DNL Adobe Sign] documento enviado para assinatura.

1. Toque **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Sign] aplicação.

1. Toque **[!UICONTROL Criar]** para criar o [!DNL Adobe Sign] configuração.

1. Abra o console da Web AEM. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abertura **[!UICONTROL Serviço de configuração comum do Forms].**
1. No **[!UICONTROL Permitir]** campo, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar [!DNL Adobe Sign].
1. Publique a configuração.
1. Uso [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=pt-BR) para criar configurações idênticas nas instâncias de publicação correspondentes.

Agora, [!DNL Adobe Sign] é integrado ao AEM [!DNL Forms] e pronto para uso em formulários adaptáveis. Para [usar o serviço Adobe Sign em um formulário adaptável](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), especifique o container de configuração criado acima nas propriedades do formulário adaptável.

## Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo {#adobe-acrobat-sign-for-government}

A conexão do AEM Forms com o Adobe Acrobat Sign Solutions para o governo é um processo de várias etapas. Envolve:

* Criação de um URL de redirecionamento para suas instâncias do AEM
* Compartilhamento do URL de redirecionamento e escopos com a equipe do Adobe Sign Solutions for Government
* Recebimento de credenciais da equipe do Adobe Sign
* Usar as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Antes de você iniciar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Antes de começar a conectar o AEM Forms com a solução da Adobe Acrobat Sign,

* Verifique se [Adobe Acrobat Sign Solutions para o governo](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) conta provisionada.
* Seu AEM [!DNL Forms] servidores são [SSL habilitado](/help/sites-administering/ssl-by-default.md) .
* Seu AEM [!DNL Forms] os servidores estão usando [chave criptográfica idêntica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.

### Conectar o AEM Forms ao Adobe Acrobat Sign Solutions para o governo {#connect-adobe-acrobat-sign-for-government}

#### Criar um URL de redirecionamento para sua instância do AEM

1. Na sua instância do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração. Certifique-se de que o nome do contêiner/pasta não contenha nenhum espaço.

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** e abra o container de configuração criado na etapa anterior. Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.
1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Acrobat Sign] configuração no AEM Forms.
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

1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]** e navegue para selecionar um **[!UICONTROL Miniatura]** para a configuração. Clique em **[!UICONTROL Avançar]**.

1. No **[!UICONTROL Configurações]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, para o **[!UICONTROL Selecionar solução]** selecione [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions para o governo](/help/forms/using/assets/adobe-sign-for-govt.png)

1. No **[!UICONTROL E-mail]** especifique o endereço de email associado à sua conta do Adobe Acrobat Sign Solutions for Government.

1. A variável **[!UICONTROL URL do OAuth]** campo especifica o fragmento de banco de dados do Adobe Sign. O campo contém o URL padrão. Não altere o URL.

1. Usar as credenciais compartilhadas pela Adobe Acrobat Sign para o representante de soluções do governo ([Membro da equipe do Adobe Professional Services]) na seção anterior como [**[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]**].

1. Selecione o **[!UICONTROL Ativar Adobe Acrobat Sign para anexos]** opção para anexar arquivos anexados a um Formulário adaptável aos arquivos correspondentes [!DNL Adobe Acrobat Sign] documento enviado para assinatura.

1. Toque **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando for solicitado que você confirme o acesso de `Adobe Acrobat Sign for Government Solutions` e , clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar o [!DNL Adobe Acrobat Sign] conta de desenvolvedor, uma mensagem de sucesso semelhante à seguinte é exibida.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando for solicitado que você confirme o acesso de `your account`e clique em **[!UICONTROL Permitir acesso]**.

1. Toque **[!UICONTROL Criar]** para criar a configuração.
1. Abra o console da Web AEM. O URL é `https://'[server]:[port]'/system/console/configMgr`
1. Abertura **[!UICONTROL Serviço de configuração comum do Forms].**
1. No **[!UICONTROL Permitir]** campo, **selecionar** Todos os usuários - Todos os usuários, anônimos ou conectados, podem visualizar anexos, verificar e assinar formulários e clicar em **[!UICONTROL Salvar].** A instância do autor está configurada para usar [!DNL Adobe Sign].

1. Publique a configuração.
1. Uso [replicação](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=pt-BR) para criar configurações idênticas nas instâncias de publicação correspondentes.

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
