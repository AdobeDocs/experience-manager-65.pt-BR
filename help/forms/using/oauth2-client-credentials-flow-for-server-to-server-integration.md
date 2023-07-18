---
title: Integração do Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Etapas para integrar a integração do Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# Integração do Salesforce usando o fluxo de credenciais do cliente OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html) |
| AEM 6.5 | Este artigo |


Para integrar o AEM Forms ao aplicativo Salesforce, o fluxo de credenciais do cliente OAuth 2.0 é usado. É um método padronizado e seguro para comunicação direta sem envolvimento do usuário. Nesse fluxo, o aplicativo cliente (Formulário AEM) troca as credenciais do cliente, definidas no aplicativo conectado do Salesforce, para obter um token de acesso. As credenciais do cliente necessárias incluem a chave do consumidor e o segredo do consumidor.

## Vantagens de integrar o Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0 {#advantages-of-integrating-saleforce-aemforms}

O AEM Forms oferece suporte à integração do Salesforce com o Fluxo de código de autorização, além do fluxo de credenciais do cliente OAuth 2.0. No fluxo de código de autorização OAuth 2.0, o aplicativo cliente (AEM Forms) obtém acesso aos recursos em nome de um usuário do Salesforce, que tem algumas limitações:

* São permitidas no máximo cinco conexões por usuário. Outras conexões revogam automaticamente conexões mais antigas.
* Se um usuário for desativado, perder acesso ou atualizar uma senha, a configuração da fonte de dados AEM para de funcionar.

## Pré-requisitos {#prerequisites}

Para recuperar e buscar dados entre os ambientes do Salesforce e do AEM, é necessário ter alguns pré-requisitos antes de continuar:

+++ **Configurar um aplicativo conectado do Saleforce com fluxo de credenciais do cliente e um usuário somente de API**

É obrigatório criar um aplicativo conectado do Salesforce com fluxo de credenciais de cliente OAuth 2.0 e um usuário somente de API para sua organização. Para obter etapas detalhadas, consulte o artigo [Fluxo de credenciais do cliente OAuth 2.0 para integração de servidor a servidor](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). Essas etapas ajudam a obter a chave do consumidor e o segredo do consumidor.

>[!NOTE]
>
> Anote a chave do consumidor e o segredo do consumidor, pois eles são necessários ao criar uma configuração de fonte de dados do AEM.

+++

+++ **Criar um arquivo do Swagger**

O Swagger é um conjunto de regras, especificações e ferramentas de código aberto para desenvolver e descrever APIs RESTful. [Criar um arquivo Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) antes de integrar o Salesforce com o AEM Forms.

>[!NOTE]
>
> O AEM 6.5 é compatível apenas com as especificações do arquivo Swagger 2.0.

+++

## Etapas para configurar o Salesforce com o fluxo de credenciais do cliente {#steps-to-create-aem-datasource-configuration}

1. Faça logon na instância do Author.
1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de dados]**.
1. Selecione a pasta de configuração.
1. Clique em **[!UICONTROL Criar]** e a variável **[!UICONTROL Criar configuração da fonte de dados]** é exibida.
1. Especifique a **[!UICONTROL Título]** e selecione o **[!UICONTROL Tipo de serviço]** as **[!UICONTROL Serviço RESTful]**.
1. Clique em **[!UICONTROL Avançar]**.
1. Selecione o **[!UICONTROL Origem do Swagger]** as **[!UICONTROL Arquivo].**
   >[!NOTE]
   >
   > Assim que o arquivo swagger for selecionado, o Esquema, o Nome do host e o Caminho base serão preenchidos automaticamente.

1. Faça upload do arquivo Swagger criado no computador local clicando em **[!UICONTROL Procurar]**.
1. Selecione o **[!UICONTROL Tipo de autenticação]** as **[!UICONTROL OAuth 2.0]** e a variável **[!UICONTROL Configurações de autenticação]** é exibido.
1. Selecione o **[!UICONTROL Tipo de concessão]** as **[!UICONTROL Credenciais do cliente]**.
1. Especifique a **[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]** obtido no aplicativo conectado do Salesforce.
1. Especifique a **[!UICONTROL URL do token de acesso]** no formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organização tem seu próprio nome de domínio específico.

1. Clique em **[!UICONTROL Testar conexão]**.
1. Se a conexão for bem-sucedida, clique no link **[!UICONTROL Criar]** botão.

Agora, você pode [criar o modelo de dados do formulário](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) para integrar a fonte de dados configurada ao Formulário adaptável.
