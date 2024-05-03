---
title: Integração do Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0
description: Etapas para integrar a integração do Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 4%

---

# Integração do Salesforce usando o fluxo de credenciais do cliente OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | Este artigo |

Você pode usar as credenciais do cliente OAuth 2.0 para integrar o AEM Forms ao aplicativo Salesforce. As credenciais do cliente OAuth 2.0 são um método padrão e seguro para a comunicação direta sem envolvimento do usuário.

![Fluxo de trabalho ao definir a comunicação entre o AEM Forms e o aplicativo Salesforce](/help/forms/using/assets/salesforce-workflow.png)

O AEM Forms troca as credenciais do cliente (chave do consumidor e segredo do consumidor), definidas no aplicativo conectado do Salesforce, para obter um token de acesso.

Há vários benefícios de usar credenciais de cliente OAuth 2.0 para autenticação em relação à autenticação de Fluxo de código de autorização:

* A autenticação de credenciais do cliente OAuth 2.0 permite mais de cinco conexões por usuário.
* A configuração da fonte de dados AEM continua trabalhando na desativação, alterações de acesso e atualização de senha para um usuário AEM.

## Pré-requisitos {#prerequisites}

Antes de definir a comunicação entre um aplicativo do Salesforce e um ambiente AEM:

* Criar um [Aplicativo conectado do Salesforce com fluxo de credenciais do cliente OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) e um usuário somente de API para sua organização, além de obter a chave do consumidor e o segredo do consumidor para o aplicativo.

* Verifique se o arquivo do Swagger está configurado corretamente para corresponder às APIs da sua organização. Como alternativa, você pode optar por [criar um arquivo do Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) do zero, personalizado para utilização em seu ambiente AEM.
>[!NOTE]
>
> O AEM 6.5 é compatível apenas com as especificações do arquivo Swagger 2.0.

+++

## Etapas para configurar o Salesforce com o fluxo de credenciais do cliente {#steps-to-create-aem-datasource-configuration}

1. Faça logon na instância do Author.
1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Fontes de dados]**.
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

Agora, você pode [criar o modelo de dados do formulário](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) para integrar a fonte de dados configurada ao Forms adaptável.
