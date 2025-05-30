---
title: Como conectar e enviar dados do formulário adaptável para o Microsoft&reg; Power Automate?
description: Um guia passo a passo para conectar e enviar dados do Formulário adaptável para o Microsoft&reg; Power Automate.
keywords: Forms Microsoft Power Automate adaptável, enviar dados do Forms adaptável para o Microsoft Power Automate
feature: Adaptive Forms,Foundation Components
exl-id: 3fd26ddb-d247-462f-a0f6-8af6166516c1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# Conectar e enviar dados do formulário adaptável para o Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

Você pode configurar um Formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente. Estes são alguns exemplos do que você pode fazer após integrar um formulário adaptável ao Microsoft® Power Automate:

* Usar dados adaptáveis do Forms em processos de negócios do Power Automate
* Use o Power Automate para enviar dados capturados para mais de 500 fontes de dados ou qualquer API disponível publicamente
* Realizar cálculos complexos em dados capturados
* Salve os dados do Forms adaptável em sistemas de armazenamento em uma programação predefinida

O editor Forms adaptável fornece a **ação de envio Chamar um fluxo do Microsoft® Power Automate** para enviar dados de formulários adaptáveis, anexos e Documentos de Registro para o fluxo da nuvem do Power Automate. Para usar a ação Enviar para enviar dados capturados para o Microsoft® Power Automate, [Conecte sua instância de autor do AEM Forms com o Microsoft® Power Automate] (#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)

## Pré-requisitos

Os seguintes itens são necessários para conectar um Formulário adaptável com o Microsoft® Power Automate:

* Licença do Microsoft® Power Automate Premium
* Fluxo do Microsoft® [Power Automate](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) com o acionador `When an HTTP request is received` para aceitar os dados de envio do Formulário adaptável
* Um usuário Experience Manager com os privilégios [Forms Author](/help/forms/using/forms-groups-privileges-tasks.md) e [Forms Admin](/help/forms/using/forms-groups-privileges-tasks.md)
* A conta usada para conectar ao Microsoft® Power Automate é proprietária do fluxo do Power Automate configurado para receber dados do Formulário adaptável


## Conecte sua instância do AEM Forms com o Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Execute as seguintes ações para conectar sua instância do AEM Forms Author ao Microsoft® Power Automate:

1. [Criar uma Microsoft](#ms-power-automate-application)
1. [Criar Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Criar Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publish Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Criar Aplicativo do Ative Diretory do Microsoft® Azure {#ms-power-automate-application}

1. Faça logon no [Portal do Azure](https://portal.azure.com/).
1. Selecione [!UICONTROL Azure Ative Diretory] na navegação à esquerda.
1. Na página Diretório padrão, selecione [!UICONTROL Registros de aplicativo] no painel esquerdo.
1. Na página Registros do aplicativo, clique em Novos registros.
1. Especifique Nome, Tipos de conta suportados e URI de redirecionamento na página. No URI de redirecionamento, especifique o seguinte e clique em Salvar.
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrar um Aplicativo do Azure Ative Diretory](assets/power-automate-application.png)

   >[!NOTE]
   >Você também pode especificar URIs de redirecionamento adicionais, se necessário, na página Autenticação.
   > Para os tipos de conta suportados, selecione um único locatário, vários locatários ou Conta pessoal da Microsoft®, dependendo do seu caso de uso


1. Na página Autenticação, ative as seguintes opções e clique em Salvar.


   * Tokens de acesso (usados para fluxos implícitos)
   * Tokens de ID (usados para fluxos implícitos e híbridos)

1. Na página de permissões da API, clique em Adicionar uma permissão.
1. Em APIs Microsoft®, selecione o Serviço de fluxo e selecione as seguintes permissões.
   * Flows.Manage.All
   * Flows.Read.All

   Clique em Adicionar permissões para salvar as permissões.
1. Na página de permissões da API, clique em Adicionar uma permissão. Selecione as APIs que minha organização usa e pesquise `DataVerse`.
1. Ative user_personation e clique em Adicionar permissões.
1. (Opcional) Na página Certificados e segredos, clique em Novo segredo de cliente. Na tela Adicionar um segredo do cliente, forneça uma descrição e um período para o segredo expirar e clique em Adicionar. Uma sequência secreta é gerada.
1. Anote a [URL de ambiente do Dynamics](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests) específica da sua organização.

### Criar configuração de nuvem do Microsoft® Power Automate Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.
1. Na página **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um **[!UICONTROL Título]** para a configuração, habilite as **[!UICONTROL Configurações de Nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Service. Verifique se o nome da pasta não contém nenhum espaço.
1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e abra o contêiner de configuração criado na etapa anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]**.

1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL Microsoft®® Power Automate Flow Service] no AEM Forms.
1. Na página **[!UICONTROL Configurar Serviço Dataverse para o Microsoft® Power Automate]**, especifique a **[!UICONTROL ID do Cliente]** (também conhecida como ID do Aplicativo), o **[!UICONTROL Segredo do Cliente]**, o **[!UICONTROL URL do OAuth]** e o **[!UICONTROL URL do Ambiente Dinâmico]**. Use a ID do Cliente, o Segredo do Cliente, a URL do OAuth e a URL do Ambiente Dinâmico do [Aplicativo do Microsoft® Azure Ative Diretory](#ms-power-automate-application) criados na seção anterior. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para encontrar o URL do OAuth

   ![Use a opção Endpoints na interface do usuário do aplicativo Microsoft Power Automate para localizar a URL do OAuth](assets/endpoints.png)

1. Selecione **[!UICONTROL Conectar]**. Se solicitado, faça logon em sua conta do Microsoft® Azure. Selecione **[!UICONTROL Salvar]**.

### Criar configuração de nuvem do serviço de fluxo do Microsoft® Power Automate {#create-microsoft-power-automate-flow-cloud-configuration}

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Serviço de fluxo do Microsoft® Power Automate]** e abra o contêiner de configuração criado na seção anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]**.
1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL Microsoft®® Power Automate Flow Service] no AEM Forms.
1. Na página **[!UICONTROL Configurar Dataverse para o Microsoft® Power Automate]**, especifique a **[!UICONTROL ID do Cliente]** (também conhecida como ID do Aplicativo), o **[!UICONTROL Segredo do Cliente]**, o **[!UICONTROL URL do OAuth]** e o **[!UICONTROL URL do Ambiente Dinâmico]**. Use a ID do cliente, o Segredo do cliente, o URL do OAuth e a ID de ambiente do Dynamics. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para localizar o URL do OAuth. Abra o link [Meus fluxos](https://us.flow.microsoft.com) e selecione Meus Fluxos para usar a ID listada na URL como ID de Ambiente do Dynamics.
1. Selecione **[!UICONTROL Conectar]**. Se solicitado, faça logon em sua conta do Microsoft® Azure. Selecione **[!UICONTROL Salvar]**.

### Publish Configurações de nuvem do Microsoft® Power Automate Dataverse e do Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e abra o contêiner de configuração criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) anterior.
1. Selecione a configuração `dataverse` e selecione **[!UICONTROL Publish]**.
1. Na página do Publish, selecione **[!UICONTROL Todas as configurações]** e **[!UICONTROL Publish]**. Publish: configurações de nuvem do Power Automate Dataverse e do Power Automate Flow Service.

Sua instância do AEM Forms Author agora está conectada ao Microsoft® Power Automate. Agora é possível enviar dados do Adaptive Forms para um fluxo do Power Automate.

## Use a ação Chamar um fluxo do Microsoft® Power Automate para enviar dados a um fluxo do Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Depois de [Conectar a instância do autor do AEM Forms com o Microsoft® Power Automate](#connect-forms-server-with-power-automate), execute a seguinte ação para configurar o formulário adaptável para enviar os dados capturados para um fluxo do Microsoft® no envio do formulário.

1. Faça logon na instância do Autor, selecione o Formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. No Contêiner de Configuração, navegue e selecione o contêiner criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) e selecione **[!UICONTROL Salvar e fechar]**.
1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. No contêiner de propriedades, em **[!UICONTROL Enviar Ações]**, selecione a opção **[!UICONTROL Invocar um fluxo do Power Automate]**. Uma lista de fluxos disponíveis do Power Automate fica disponível na opção **[!UICONTROL Fluxo do Power Automate]**. Selecione o fluxo necessário e os dados do Adaptive Forms serão enviados a ele no envio.

   ![Configurar Ação de Envio](assets/submission.png)

>[!NOTE]
>
> Antes de enviar o Formulário adaptável, verifique se o acionador `When an HTTP Request is received` com o Esquema JSON abaixo foi adicionado ao seu fluxo do Power Automate.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

## Consulte também,

* [Criação de um Formulário adaptável](create-an-adaptive-form-core-components.md)
* [Configurar uma ação de envio](configuring-submit-actions.md)
* [Conector do Adobe Experience Manager para Microsoft® Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
