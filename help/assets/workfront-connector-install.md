---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] instala o conector aprimorado. Antes de instalar, consulte o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam esse conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso desse conector.
>
>* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, navegue até a `digital.hoodoo` grupo disponível no painel esquerdo no [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulte [Exame de certificação de parceiros para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia do exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Para instalar o conector, siga estas etapas:

1. Baixe o conector de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurar o firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. No Dispatcher, permita cabeçalhos HTTP chamados `authorization`, `username`, e `apikey`. Permitir `GET`, `POST`, e `PUT` solicitações para `/bin/workfront-tools`.
1. Verifique se os seguintes caminhos não existem no [!DNL Experience Manager] repositório:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Instale o pacote usando [!UICONTROL Gerenciador de pacotes]. Para saber como instalar pacotes, consulte [Documentação do Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Criar `wf-workfront-users` in [!DNL Experience Manager] Grupo de usuários e atribuir a permissão `jcr:all` para `/content/dam`.
1. Adicionar uma propriedade personalizada à definição de índice pronta para uso para **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**. Execute as etapas abaixo:
   * Adicionar um **`nt:unstructured`** propriedade chamada **`wfReferenceNumber`** para:
     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`.
   * Reindexe o `index /oak:index/ntFolderDamLucene` invertendo o sinalizador de reindexação para `true`.

Um usuário do sistema `workfront-tools` O é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] que usam o conector são automaticamente adicionados como parte desse grupo.

## Configurar a conexão entre [!DNL Experience Manager] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com o Workfront, siga estas etapas:

1. Entrada [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de ferramentas do Workfront]**.

1. Selecionar `workfront-tools` no painel esquerdo e selecione **[!UICONTROL Criar]** na área superior direita da página.

1. No **[!UICONTROL Conexão Workfront]** , forneça os detalhes necessários do seu [!DNL Workfront] e selecione **[!UICONTROL Conectar-se ao Workfront]** opção. Depois de conectado com êxito, o [!DNL Workfront] a integração personalizada de documentos é criada automaticamente na [!DNL Workfront] ambiente.

   ![Conectar [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Para verificar a conexão, acesse-a em [!DNL Workfront] e verifique se a chave da API é a mesma e se a conexão é **[!UICONTROL Ativado]**. Para fazer isso, selecione **[!UICONTROL Configuração]** > **[!UICONTROL Documentos]** > **[!UICONTROL Integrações personalizadas]** in [!DNL Workfront].

## Atualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

O Experience Manager Assets permite atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente.

Para atualizar o [!DNL Workfront for Experience Manager enhanced connector] para a versão mais recente:

1. Baixe a versão mais recente do conector aprimorado em [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Instale o pacote usando [!UICONTROL Gerenciador de pacotes]. Para saber como instalar pacotes, consulte [Documentação do Gerenciador de pacotes](/help/sites-administering/package-manager.md).
