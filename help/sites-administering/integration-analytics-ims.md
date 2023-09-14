---
title: Integração com o Adobe Analytics usando IMS
description: Saiba mais sobre a integração do AEM com o Adobe Analytics usando o IMS
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 54%

---


# Integração com o Adobe Analytics usando IMS {#integration-with-adobe-analytics-using-ims}

A integração do AEM com o Adobe Analytics por meio da API do Analytics Standard requer a configuração do Adobe IMS (Identity Management System) usando o console do Adobe Developer.

>[!NOTE]
>
>A compatibilidade com a API 2.0 do Adobe Analytics Standard é nova no AEM 6.5.12.0. Esta versão da API é compatível com autenticação IMS.
>
>O uso da API do Adobe Analytics Classic 1.4 no AEM ainda é compatível com versões anteriores. A variável [A API clássica do Analytics usa autenticação de credenciais do usuário](/help/sites-administering/adobeanalytics-connect.md).
>
>A seleção da API é orientada pelo método de autenticação usado para a integração do AEM/Analytics.
>
>Outras informações também estão disponíveis em [Migrar para as APIs 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Pré-requisitos {#prerequisites}

Antes de iniciar este procedimento:

* O [Suporte da Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) precisa provisionar sua conta com:

   * Adobe Console
   * Console do desenvolvedor da Adobe
   * Adobe Analytics e
   * Adobe IMS (Identity Management System)

* O administrador de sistemas da sua organização deve usar o Admin Console para adicionar os desenvolvedores necessários em sua organização aos perfis de produto relevantes.

   * Isso fornece aos desenvolvedores específicos permissões para ativar integrações no Console do Adobe Developer.
   * Consulte [Gerenciar desenvolvedores](https://helpx.adobe.com/enterprise/using/manage-developers.html).


## Configuração de IMS - Geração de uma Chave pública {#configuring-an-ims-configuration-generating-a-public-key}

O primeiro estágio da configuração é criar uma configuração do IMS no AEM e gerar a Chave pública.

1. No AEM, abra o menu **Ferramentas**.
1. No **Segurança** , selecione **Configurações do Adobe IMS**.
1. Selecione **Criar** para abrir a **Configuração de contas técnicas do Adobe IMS**.
1. Usando a lista suspensa em **Configuração na nuvem**, selecione **Adobe Analytics**.
1. Ative **Criar novo certificado** e insira um novo alias.
1. Confirme com **Criar certificado**.

   ![Assistente de configuração de conta técnica do Adobe IMS](assets/integrate-analytics-io-01.png)

1. Selecione **Baixar** (ou **Baixar chave pública**) para baixar o arquivo na unidade local, de modo que ele esteja pronto para uso ao [configurar o IMS para a integração do Adobe Analytics com o AEM](#configuring-ims-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenha essa configuração aberta; ela será necessária novamente quando [Concluir a configuração do IMS no AEM](#completing-the-ims-configuration-in-aem).

   ![Caixa de diálogo Informações para adicionar a chave ao Adobe I/O](assets/integrate-analytics-io-02.png)

## Configurar o IMS para integração do Adobe Analytics com o AEM {#configuring-ims-for-adobe-analytics-integration-with-aem}

Usando o Console do Adobe Developer, crie um Projeto (integração) com o Adobe Analytics (para uso do AEM) e, em seguida, atribua os privilégios necessários.

### Criação do projeto {#creating-the-project}

Para criar um projeto com o Adobe Analytics que o AEM possa usar, abra o Adobe Developer Console:

>[!CAUTION]
>
>No momento, o Adobe só é compatível com o console do Adobe Developer **Conta de serviço (JWT)** tipo de credencial.
>
>Não use o **Servidor OAuth para servidor** tipo de credencial, que terá suporte no futuro.

1. Abra os projetos do Adobe Developer Console:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Quaisquer projetos que você tiver serão mostrados. Selecionar **Criar novo projeto** - a localização e utilização dependem do seguinte:

   * Se você ainda não tiver um projeto, **Criar novo projeto** estará na parte inferior central.
     ![Criar novo projeto - Primeiro projeto](assets/integration-analytics-io-02.png)
   * Caso já tenha projetos existentes, eles são listados e **Criar novo projeto** está localizado no canto superior direito.
     ![Criar novo projeto - Vários projetos](assets/integration-analytics-io-03.png)


1. Selecione **Adicionar ao projeto**, seguido da **API**:

   ![Introdução ao novo projeto](assets/integration-analytics-io-10.png)

1. Selecione **Adobe Analytics** e, em seguida, **Próximo**:

   >[!NOTE]
   >
   >Se você estiver inscrito no Adobe Analytics, mas não o vir listado, verifique os [Pré-requisitos](#prerequisites).

   ![Adicionar uma API](assets/integration-analytics-io-12.png)

1. Selecionar **Conta de serviço (JWT)** como o tipo de autenticação, depois continue com **Próxima**:

   ![Selecione o tipo de autenticação](assets/integration-analytics-io-12a.png)

1. **Faça upload da sua chave pública** e, quando terminar, clique em **Próximo**:

   Selecione ![Fazer upload da sua chave pública](assets/integration-analytics-io-13.png)

1. Revise as credenciais e continue com **Próximo**:

   ![Revisar credenciais](assets/integration-analytics-io-15.png)

1. Selecione os perfis de produto necessários e clique em **Salvar API configurada**:

   ![Selecionar perfis de produto necessários](assets/integration-analytics-io-16.png)

1. A configuração é confirmada.

### Atribuir privilégios à integração {#assigning-privileges-to-the-integration}

Agora atribua os privilégios necessários à integração:

1. Abra o Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navegue até **Produtos** (barra de ferramentas superior) e, em seguida, selecione **Adobe Analytics - &lt;*your-tenant-id*>** (no painel esquerdo).
1. Selecione **Perfis de produto** e seu espaço de trabalho necessário na lista apresentada. Por exemplo, Espaço de trabalho padrão.
1. Selecione **Credenciais da API** e, em seguida, a configuração de integração necessária.
1. Selecione **Editor** como **Função do produto**, em vez de **Observador**.

## Detalhes armazenados para o projeto de integração do Adobe Developer Console {#details-stored-for-the-ims-integration-project}

No de Projetos do Adobe Developer Console, é possível ver uma lista de todos os projetos de integração:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Para mostrar mais detalhes sobre a configuração, selecione uma entrada de projeto específica. Dentre elas:

* Visão geral do projeto
* Insights
* Credenciais
   * Conta de serviço (JWT)
      * Detalhes da credencial
      * Gerar JWT
* APIS
   * Por exemplo, Adobe Analytics

Em alguns desses, você deve concluir a integração do Adobe Analytics no AEM.

## Concluir a configuração do IMS no AEM {#completing-the-ims-configuration-in-aem}

Ao retornar para o AEM, é possível concluir a configuração do IMS adicionando os valores necessários do projeto de integração do Analytics:

1. Retorne à [configuração do IMS aberta no AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Selecione **Próximo**.

1. Aqui você pode usar o [Detalhes armazenados para o projeto de integração do console do Adobe Developer](#details-stored-for-the-ims-integration-project):

   * **Título**: seu texto.
   * **Servidor de autorização**: copie/cole essa informação da linha `aud` da seção **Carga** abaixo, por exemplo, `https://ims-na1.adobelogin.com` no exemplo abaixo
   * **Chave da API**: copie da seção **Credenciais** na [Visão geral do projeto](#details-stored-for-the-ims-integration-project)
   * **Segredo do cliente**: gere isso na [guia Segredo do cliente da seção Conta de serviço (JWT)](#details-stored-for-the-ims-integration-project) e copie
   * **Carga**: copie isso da [guia Gerar JWT da seção Conta de Serviço (JWT)](#details-stored-for-the-ims-integration-project)

   ![Detalhes da configuração do AEM IMS](assets/integrate-analytics-io-10.png)

1. Confirme com **Criar**.

1. Sua configuração do Adobe Analytics será exibida no console do AEM.

   ![Configuração IMS](assets/integrate-analytics-io-11.png)

## Confirmação da configuração do IMS {#confirming-the-ims-configuration}

Para confirmar que a configuração está funcionando como esperado:

1. Abrir:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por exemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. Selecione sua configuração.
1. Selecione **Verificar integridade** na barra de ferramentas e, em seguida, **Verificar**.

   ![Configuração do IMS — Verificar integridade](assets/integrate-analytics-io-12.png)

1. Se tiver êxito, você verá uma mensagem de confirmação.

## Configuração do serviço Adobe Analytics Cloud {#configuring-the-adobe-analytics-cloud-service}

A configuração agora pode ser referenciada para um Cloud Service usar a API do Analytics Standard:

1. Abra o **Ferramentas** menu. Em seguida, no prazo de **Cloud Service** , selecione **Cloud Service herdados**.
1. Role para baixo até **Adobe Analytics** e selecione **Configurar agora**.

   A variável **Criar configuração** é aberta.

1. Insira um **Título** e, se desejar, um **Nome** (se deixado em branco, é gerado a partir do título).

   Você também pode selecionar o modelo necessário (se mais de um estiver disponível).

1. Confirme com **Criar**.

   A variável **Editar componente** é aberta.

1. Insira os detalhes na **Configurações do Analytics** guia:

   * **Autenticação**: IMS

   * **Configuração do IMS**: selecione o nome da configuração IMS

1. Para inicializar a conexão com o Adobe Analytics, clique em **Conectar-se ao Analytics**.

   Se a conexão for bem-sucedida, a mensagem **Conexão bem-sucedida** será exibida.

1. Selecionar **OK** na mensagem.

1. Preencha outros parâmetros conforme necessário, seguido por **OK** na caixa de diálogo para que você possa confirmar a configuração.

1. Agora você pode prosseguir para [Adicionar uma estrutura do Analytics](/help/sites-administering/adobeanalytics-connect.md) para configurar parâmetros enviados para o Adobe Analytics.
