---
title: Configuração do Microsoft Dynamics OData
seo-title: Microsoft Dynamics ODtata configuration
description: Aproveite, integre e trabalhe com serviços Microsoft Dynamics online e local por meio de um modelo de dados de formulário.
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Configuração do Microsoft Dynamics OData{#microsoft-dynamics-odata-configuration}

![integração de dados](assets/data-integeration.png)

O Microsoft Dynamics é um software de CRM (relacionamento com o cliente) e ERP (Enterprise Resource Planning, planejamento de recursos empresariais) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes. [Integração de dados do AEM Forms](../../forms/using/data-integration.md) O fornece uma configuração de serviço de nuvem OData para integrar o Forms ao servidor Microsoft Dynamics online e local. Ele permite criar um modelo de dados de formulário com base nas entidades, atributos e serviços definidos no serviço Microsoft Dynamics. O modelo de dados de formulário pode ser usado para criar formulários adaptáveis que interagem com o servidor do Microsoft Dynamics para ativar fluxos de trabalho de negócios. Por exemplo:

* Consultar o servidor do Microsoft Dynamics para dados e pré-preencher formulários adaptáveis
* Gravar dados no Microsoft Dynamics no envio de formulário adaptável
* Gravar dados no Microsoft Dynamics por meio de entidades personalizadas definidas no modelo de dados de formulário e vice-versa

O pacote complementar do AEM Forms também inclui a configuração de referência de OData que você pode aproveitar para integrar rapidamente o Microsoft Dynamics ao AEM Forms.

Quando o pacote é instalado, as seguintes entidades e serviços estão disponíveis na sua instância do AEM Forms:

* MS Dynamics OData Cloud Service (Serviço OData)
* Modelo de dados de formulário com entidades e serviços pré-configurados do Microsoft Dynamics.

As entidades e os serviços pré-configurados do Microsoft Dynamics em um modelo de dados de formulário só estarão disponíveis na sua instância do AEM Forms se o modo de execução da instância de AEM estiver definido como `samplecontent` (padrão). O MS Dynamics OData Cloud Service (Serviço OData) também está disponível com outros modos de execução. Para obter mais informações sobre como configurar modos de execução para uma instância de AEM, consulte [Modos de Execução](/help/sites-deploying/configure-runmodes.md).

## Pré-requisitos {#prerequisites}

Antes de começar a configurar e configurar o Microsoft Dynamics, verifique se você:

* Instalado o [Pacote do complemento AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Configurado o Microsoft Dynamics 365 online ou instalado uma instância de uma das seguintes versões do Microsoft Dynamics:

   * Microsoft Dynamics 365 no local
   * Microsoft Dynamics 2016 no local

* [Registrado o aplicativo para o serviço online Microsoft Dynamics com o Microsoft Azure Ative Diretory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Anote os valores para a ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o serviço registrado. Esses valores são usados enquanto [configuração do serviço em nuvem para o serviço Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Definir URL de resposta para aplicativo Microsoft Dynamics registrado {#set-reply-url-for-registered-microsoft-dynamics-application}

Faça o seguinte para definir o URL de resposta para o aplicativo Microsoft Dynamics registrado:

>[!NOTE]
>
>Use este procedimento somente ao integrar o AEM Forms com o servidor Microsoft Dynamics online.

1. Vá para a conta do Microsoft Azure Ative Diretory e adicione o seguinte URL de configuração do serviço de nuvem em **URLs de resposta** configurações para seu aplicativo registrado:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Diretório do Azure](assets/azure_directory_new.png)

1. Salve a configuração.

## Configurar o Microsoft Dynamics para IFD {#configure-microsoft-dynamics-for-ifd}

O Microsoft Dynamics usa a autenticação baseada em declarações para fornecer acesso aos dados no servidor do Microsoft Dynamics CRM para usuários externos. Para habilitar isso, faça o seguinte para configurar o Microsoft Dynamics para implantação com acesso à Internet (IFD) e definir as configurações de solicitação.

>[!NOTE]
>
>Use esse procedimento apenas durante a integração do AEM Forms com o servidor Microsoft Dynamics local.

1. Configure a instância local do Microsoft Dynamics para IFD, conforme descrito em [Configurar o IFD para o Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Execute os seguintes comandos usando o Windows PowerShell para definir as configurações de afirmação no Microsoft Dynamics habilitado para IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro do aplicativo para CRM no local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obter detalhes.

## Configurar o cliente OAuth no computador AD FS {#configure-oauth-client-on-ad-fs-machine}

Faça o seguinte para registrar um cliente OAuth na máquina do Ative Diretory Federation Services (AD FS) e conceder acesso à máquina do AD FS:

>[!NOTE]
>
>Use esse procedimento apenas durante a integração do AEM Forms com o servidor Microsoft Dynamics local.

1. Execute o seguinte comando:

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Em que:

   * `Client-ID` é uma ID de cliente que você pode gerar usando qualquer gerador de GUID.
   * `redirect-uri` é o URL para o serviço de nuvem do Microsoft Dynamics OData no AEM Forms. O serviço em nuvem padrão instalado com o pacote AEM Forms é implantado no seguinte URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Execute o seguinte comando para conceder acesso na máquina AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Em que:

   * `resource` é o URL da organização do Microsoft Dynamics.

1. O Microsoft Dynamics usa o protocolo HTTPS. Para chamar pontos de extremidade do AD FS do servidor Forms, instale o certificado do site Microsoft Dynamics para o armazenamento de certificados Java usando o `keytool` no computador que executa o AEM Forms.

## Configurar o serviço em nuvem para o serviço Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

O **MS Dynamics OData Cloud Service (Serviço OData)** vem com a configuração padrão OData. Para configurá-lo para se conectar ao serviço Microsoft Dynamics, faça o seguinte:

1. Navegar para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]** e toque no `global` pasta de configuração.
1. Selecionar **MS Dynamics OData Cloud Service (Serviço OData)** configuração e toque em **[!UICONTROL Propriedades]**. A caixa de diálogo da propriedade de configuração do serviço em nuvem é aberta.

   No **Configurações de autenticação** guia :

   1. Insira o valor da variável **Raiz do serviço** campo. Vá para a instância do Dynamics e navegue até **Recursos do desenvolvedor** para exibir o valor do campo Service Root . Por exemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Substitua os valores padrão no **ID do cliente**(também designado por **ID do aplicativo**), **Segredo do cliente**, **URL de OAuth**, **Atualizar URL do token**, **URL do token de acesso** e **Recurso** campos com valores da configuração do serviço Microsoft Dynamics. É obrigatório especificar o URL da instância do dynamics no **Recurso** para configurar o Microsoft Dynamics com um modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância dinâmica. Por exemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especificar **openid** no **Escopo da Autorização** campo para o processo de autorização no Microsoft Dynamics.

   ![Configurações de autenticação](assets/dynamics_authentication_settings_new.png)

1. Clique em **[!UICONTROL Conectar-se ao OAuth]**. Você é redirecionado para a página de logon do Microsoft Dynamics.
1. Faça logon com as credenciais do Microsoft Dynamics e aceite permitir que a configuração do serviço de nuvem se conecte ao serviço do Microsoft Dynamics. É uma tarefa única estabelecer conexão entre o serviço de nuvem e o serviço.

   Em seguida, você é redirecionado para a página de configuração do serviço de nuvem, que exibe uma mensagem de que a configuração de OData foi salva com êxito.

O serviço em nuvem do MS Dynamics OData Cloud Service (Serviço OData) é configurado e conectado ao serviço de Dynamics.

## Criar modelo de dados de formulário {#create-form-data-model}

Ao instalar o pacote AEM Forms, um modelo de dados de formulário,**Microsoft Dynamics FDM**, é implantado na instância do AEM. Por padrão, o modelo de dados de formulário usa o serviço Microsoft Dynamics configurado no Cloud Service do MS Dynamics OData (Serviço OData) como fonte de dados.

Ao abrir o modelo de dados de formulário pela primeira vez, ele se conecta ao serviço Microsoft Dynamics configurado e busca entidades da instância do Microsoft Dynamics. As entidades &quot;contato&quot; e &quot;lead&quot; do Microsoft Dynamics já são adicionadas no modelo de dados de formulário.

Para revisar o modelo de dados de formulário, acesse **[!UICONTROL Forms > Integrações de dados]**. Selecionar **Microsoft Dynamics FDM** e clique em **Editar** para abrir o modelo de dados de formulário no modo de edição. Como alternativa, você pode abrir o modelo de dados de formulário diretamente do seguinte URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Em seguida, é possível criar um formulário adaptável com base no modelo de dados de formulário e usá-lo em vários casos de uso de formulário adaptável, como:

* Preencha previamente o formulário adaptável consultando informações das entidades e serviços do Microsoft Dynamics
* Chamar operações do servidor do Microsoft Dynamics definidas em um modelo de dados de formulário usando regras de formulário adaptáveis
* Gravar dados de formulário enviados para entidades do Microsoft Dynamics

É recomendável criar uma cópia do modelo de dados de formulário fornecido com o pacote AEM Forms e configurar modelos e serviços de dados para atender aos seus requisitos. Ele garantirá que qualquer atualização futura no pacote não substitua o modelo de dados de formulário.

Para obter mais informações sobre como criar e usar o modelo de dados de formulário em fluxos de trabalho, consulte [Integração de dados](../../forms/using/data-integration.md).
