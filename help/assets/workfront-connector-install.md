---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 4%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-connector-install.html?lang=en) |

Um usuário com acesso de administrador em [!DNL Adobe Experience Manager] instala o conector aprimorado. Antes de instalar, revise o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam redundante este conector; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.
>
>* O Adobe oferece suporte ao conector avançado versões 1.7.4 e superior. Não há suporte para pré-lançamento e versões personalizadas anteriores. Para verificar a versão do conector aprimorado, navegue até a `digital.hoodoo` disponível no painel esquerdo em [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR).
>
>* Consulte [Exame de certificação de parceiro para Workfront para conector aprimorado Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia de exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Para instalar o conector, siga estas etapas:

1. Baixe o conector de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurar o firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. No dispatcher, permita cabeçalhos HTTP nomeados `authorization`, `username`e `apikey`. Permitir `GET`, `POST`e `PUT` solicitações para `/bin/workfront-tools`.
1. Verifique se os seguintes caminhos não existem em [!DNL Experience Manager] repositório:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Instale o pacote usando [!UICONTROL Gerenciador de pacotes]. Para saber como instalar pacotes, consulte [Documentação do Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Criar `wf-workfront-users` em [!DNL Experience Manager] Grupo de usuários e atribua a permissão `jcr:all` para `/content/dam`.

Um usuário do sistema `workfront-tools` O é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] os usuários do conector são adicionados automaticamente como parte desse grupo.

## Configure a conexão entre [!DNL Experience Manager] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com o Workfront, siga estas etapas:

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]**.

1. Selecionar `workfront-tools` no painel esquerdo e selecione **[!UICONTROL Criar]** na área superior direita da página.

1. No **[!UICONTROL Conexão Workfront]** , forneça os detalhes necessários de sua [!DNL Workfront] e selecione **[!UICONTROL Conectar-se ao Workfront]** opção. Depois de conectado com êxito, a variável [!DNL Workfront] a integração personalizada do documento é criada automaticamente no [!DNL Workfront] ambiente.

   ![Connect [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Para verificar a conexão, acesse-a em [!DNL Workfront] e verifique se a chave da API é a mesma e se a conexão é **[!UICONTROL Ativado]**. Para fazer isso, selecione **[!UICONTROL Configuração]** > **[!UICONTROL Documentos]** > **[!UICONTROL Integrações personalizadas]** em [!DNL Workfront].

## Atualizar o [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

O Experience Manager Assets permite atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente.

Para atualizar o [!DNL Workfront for Experience Manager enhanced connector] para a versão mais recente:

1. Baixe a versão mais recente do conector aprimorado em [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Instale o pacote usando [!UICONTROL Gerenciador de pacotes]. Para saber como instalar pacotes, consulte [Documentação do Gerenciador de pacotes](/help/sites-administering/package-manager.md).
