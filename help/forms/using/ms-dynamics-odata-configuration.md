---
title: Configuração OData do Microsoft Dynamics
description: Saiba como usar, integrar e trabalhar com serviços online e no local do Microsoft Dynamics por meio do modelo de dados de formulário.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Configuração OData do Microsoft Dynamics{#microsoft-dynamics-odata-configuration}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html) |
| AEM 6.5 | Este artigo |

![integração de dados](assets/data-integeration.png)

O Microsoft Dynamics é um software de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) e ERP (Enterprise Resource Planning, planejamento de recursos corporativos) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes. [A Integração de Dados do AEM Forms](../../forms/using/data-integration.md) fornece uma configuração do serviço de nuvem OData para integrar o Forms ao servidor do Microsoft Dynamics local e online. Ela permite criar um modelo de dados de formulário com base nas entidades, atributos e serviços definidos no serviço Microsoft Dynamics. O modelo de dados de formulário pode ser usado para criar formulários adaptáveis que interagem com o servidor do Microsoft Dynamics para habilitar fluxos de trabalho de negócios. Por exemplo:

* Consultar o servidor do Microsoft Dynamics para obter dados e preencher formulários adaptáveis
* Gravar dados no Microsoft Dynamics no envio de formulário adaptável
* Gravar dados no Microsoft Dynamics por meio de entidades personalizadas definidas no modelo de dados de formulário e vice-versa

O pacote complementar do AEM Forms também inclui a configuração OData de referência que você pode usar para integrar rapidamente o Microsoft Dynamics com o AEM Forms.

Quando o pacote é instalado, as seguintes entidades e serviços estão disponíveis na instância do AEM Forms:

* CLOUD SERVICE OData do MS Dynamics (Serviço OData)
* Modelo de dados de formulário com entidades e serviços pré-configurados do Microsoft Dynamics.

As entidades e os serviços pré-configurados do Microsoft Dynamics em um modelo de dados de formulário estarão disponíveis na instância do AEM Forms somente se o modo de execução da instância do AEM estiver definido como `samplecontent` (padrão). O MS Dynamics OData Cloud Service (OData Service) também está disponível com outros modos de execução. Para obter mais informações sobre como configurar os modos de execução para uma instância do AEM, consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md).

## Pré-requisitos {#prerequisites}

Antes de começar a instalar e configurar o Microsoft Dynamics, verifique se você tem:

* Instalado o [pacote complementar do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)
* O Microsoft Dynamics 365 foi configurado online ou instalou uma instância de uma das seguintes versões do Microsoft Dynamics:

   * Microsoft Dynamics 365 no local
   * Microsoft Dynamics 2016 no local

* [Registrado o aplicativo para o serviço online do Microsoft Dynamics com o Ative Diretory do Microsoft Azure](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Anote os valores da ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o serviço registrado. Esses valores são usados ao [configurar o serviço em nuvem para o serviço Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Definir URL de resposta para o aplicativo Microsoft Dynamics registrado {#set-reply-url-for-registered-microsoft-dynamics-application}

Faça o seguinte para definir o URL de resposta para o aplicativo registrado do Microsoft Dynamics:

>[!NOTE]
>
>Use esse procedimento somente ao integrar o AEM Forms ao servidor online do Microsoft Dynamics.

1. Vá para a conta do Ative Diretory do Microsoft Azure e adicione a seguinte URL de configuração do serviço de nuvem nas configurações de **URLs de resposta** para seu aplicativo registrado:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Diretório do Azure](assets/azure_directory_new.png)

1. Salve a configuração.

## Configurar o Microsoft Dynamics para IFD {#configure-microsoft-dynamics-for-ifd}

O Microsoft Dynamics usa autenticação baseada em declarações para fornecer acesso aos dados no servidor do Microsoft Dynamics CRM para usuários externos. Para habilitar isso, faça o seguinte para configurar o Microsoft Dynamics para implantação na Internet (IFD) e definir as configurações de declaração.

>[!NOTE]
>
>Use esse procedimento somente ao integrar o AEM Forms com o servidor local do Microsoft Dynamics.

1. Configure a instância local do Microsoft Dynamics para o IFD conforme descrito em [Configurar o IFD para o Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Execute os seguintes comandos usando o Windows PowerShell para definir configurações de declaração no Microsoft Dynamics habilitado para IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro de aplicativo para CRM local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obter detalhes.

## Configurar o cliente OAuth no computador do AD FS {#configure-oauth-client-on-ad-fs-machine}

Faça o seguinte para registrar um cliente OAuth em um computador do Ative Diretory Federation Services (AD FS) e conceder acesso a esse computador:

>[!NOTE]
>
>Use esse procedimento somente ao integrar o AEM Forms com o servidor local do Microsoft Dynamics.

1. Execute o seguinte comando:

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Em que:

   * `Client-ID` é uma ID de cliente que você pode gerar usando qualquer gerador de GUID.
   * `redirect-uri` é a URL para o serviço de nuvem OData do Microsoft Dynamics no AEM Forms. O serviço de nuvem padrão instalado com o pacote do AEM Forms é implantado no seguinte URL:

     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Execute o seguinte comando para conceder acesso à máquina do AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Em que:

   * `resource` é a URL da organização do Microsoft Dynamics.

1. O Microsoft Dynamics usa o protocolo HTTPS. Para invocar pontos de extremidade do AD FS do servidor do Forms, instale o certificado de site do Microsoft Dynamics no armazenamento de certificados Java usando o comando `keytool` no computador que executa o AEM Forms.

## Configurar o serviço em nuvem para o serviço Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

A configuração **OData Cloud Service (OData Service)** do MS Dynamics vem com a configuração OData padrão. Para configurá-lo para se conectar com o serviço Microsoft Dynamics, faça o seguinte.

1. Navegue até **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]** e selecione a pasta de configuração `global`.
1. Selecione a configuração **OData Cloud Service (OData Service)** do MS Dynamics e selecione **[!UICONTROL Propriedades]**. A caixa de diálogo de propriedade de configuração do Cloud Service é aberta.

   Na guia **Configurações de autenticação**:

   1. Insira o valor para o campo **Raiz de Serviço**. Vá para a instância do Dynamics e navegue até **Recursos do Desenvolvedor** para exibir o valor do campo Raiz do Serviço. Por exemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Substitua os valores padrão nos campos **ID do Cliente**(também conhecido como **ID do Aplicativo**), **Segredo do Cliente**, **URL do OAuth**, **URL do Token de Atualização**, **URL do Token de Acesso** e **Recurso** por valores da configuração do serviço Microsoft Dynamics. É obrigatório especificar a URL da instância do Dynamics no campo **Recurso** para configurar o Microsoft Dynamics com um modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância dinâmica. Por exemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especifique **openid** no campo **Escopo de Autorização** para o processo de autorização no Microsoft Dynamics.

   ![Configurações de autenticação](assets/dynamics_authentication_settings_new.png)

1. Clique em **[!UICONTROL Conectar ao OAuth]**. Você é redirecionado para a página de logon do Microsoft Dynamics.
1. Faça logon com as credenciais do Microsoft Dynamics e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço do Microsoft Dynamics. É uma tarefa única para estabelecer a conexão entre o serviço de nuvem e o serviço.

   Em seguida, você será redirecionado para a página de configuração do Cloud Service, que exibirá uma mensagem informando que a configuração OData foi salva com êxito.

O serviço de nuvem OData Cloud Service (OData Service) do MS Dynamics está configurado e conectado com seu serviço Dynamics.

## Criar modelo de dados de formulário {#create-form-data-model}

Quando você instala o pacote do AEM Forms, um modelo de dados de formulário,**Microsoft Dynamics FDM**, é implantado em sua instância do AEM. Por padrão, o modelo de dados de formulário usa o serviço Microsoft Dynamics configurado no Cloud Service OData (OData Service) do MS Dynamics como a fonte de dados.

Ao abrir o modelo de dados de formulário pela primeira vez, ele se conecta ao serviço configurado do Microsoft Dynamics e busca entidades da sua instância do Microsoft Dynamics. As entidades &quot;contato&quot; e &quot;cliente potencial&quot; do Microsoft Dynamics já foram adicionadas no modelo de dados de formulário.

Para revisar o modelo de dados do formulário, acesse **[!UICONTROL Forms > Integrações de dados]**. Selecione **FDM** do Microsoft Dynamics e clique em **Editar** para abrir o modelo de dados de formulário no modo de edição. Como alternativa, você pode abrir o modelo de dados de formulário diretamente da seguinte URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Em seguida, você pode criar um formulário adaptável com base no modelo de dados de formulário e usá-lo em vários casos de uso de formulário adaptável, como:

* Preencha previamente o formulário adaptável consultando informações de entidades e serviços do Microsoft Dynamics
* Invocar operações de servidor do Microsoft Dynamics definidas em um modelo de dados de formulário usando regras de formulário adaptáveis
* Gravar dados de formulário enviado em entidades do Microsoft Dynamics

É recomendável criar uma cópia do modelo de dados de formulário fornecido com o pacote do AEM Forms e configurar modelos de dados e serviços para atender aos seus requisitos. Ele garantirá que qualquer atualização futura do pacote não substitua o modelo de dados de formulário.

Para obter mais informações sobre como criar e usar o modelo de dados de formulário em fluxos de trabalho de negócios, consulte [Integração de Dados](../../forms/using/data-integration.md).
