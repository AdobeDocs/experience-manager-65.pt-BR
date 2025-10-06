---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 633b1378d97ea0544f27822fb5801caa3ed15f8e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 3%

---

# Instalar o [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] instala o conector aprimorado. Antes de instalar, verifique o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* A Adobe requer a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantada e configurada sem um parceiro certificado ou [!DNL Adobe Professional Services], não é suportada pela Adobe.
>
>* A Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam este conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso deste conector.
>
>* O Adobe oferece suporte às versões avançadas de conectores 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, navegue até o grupo `digital.hoodoo` disponível no painel esquerdo no [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR).
>
>* Consulte [Exame de certificação de parceiro para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte o [Guia do Exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Para instalar o conector, siga estas etapas:

1. Baixe o conector do [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurar o firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. Na Dispatcher, permita cabeçalhos HTTP nomeados como `authorization`, `username` e `apikey`. Permitir solicitações de `GET`, `POST` e `PUT` a `/bin/workfront-tools`.
1. Verifique se os seguintes caminhos não existem no repositório [!DNL Experience Manager]:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Instale o pacote usando o [!UICONTROL Gerenciador de Pacotes]. Para saber como instalar pacotes, consulte a [documentação do Gerenciador de Pacotes](/help/sites-administering/package-manager.md).
1. Crie `wf-workfront-users` no Grupo de Usuários [!DNL Experience Manager] e atribua a permissão `jcr:all` a `/content/dam`.
1. Adicione uma propriedade personalizada à definição de índice pronta para uso para **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**. Execute as etapas abaixo:
   * Adicionar uma propriedade **`nt:unstructured`** chamada **`wfReferenceNumber`** a:
     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`.
   * Reindexe o `index /oak:index/ntFolderDamLucene` invertendo o sinalizador de reindexação para `true`.

Um usuário do sistema `workfront-tools` é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] que usam o conector são automaticamente adicionados como parte deste grupo.

>[!NOTE]
>
> Ao usar servidores proxy corporativos, inclua [!DNL workfront] na [!UICONTROL PID de Configuração de Proxy dos Componentes HTTP do Apache] para o [!UICONTROL Conector aprimorado do Workfront] para reconhecê-lo. O formato PID necessário é: `org.apache.http.proxyconfigurator~workfront`.

## Configurar a conexão entre [!DNL Experience Manager] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com o Workfront, siga estas etapas:

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração de Ferramentas do Workfront]**.

1. Selecione `workfront-tools` no painel esquerdo e selecione a opção **[!UICONTROL Criar]** na área superior direita da página.

1. Na caixa de diálogo **[!UICONTROL Conexão Workfront]**, forneça os detalhes necessários da sua implantação do [!DNL Workfront] e selecione a opção **[!UICONTROL Conectar-se ao Workfront]**. Depois de conectada com êxito, a integração personalizada do documento [!DNL Workfront] é criada automaticamente no ambiente [!DNL Workfront].

   ![Conectar [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Para verificar a conexão, acesse-a em [!DNL Workfront] e verifique se a chave de API é a mesma e se a conexão é **[!UICONTROL Habilitada]**. Para fazer isso, selecione **[!UICONTROL Configuração]** > **[!UICONTROL Documentos]** > **[!UICONTROL Integrações Personalizadas]** em [!DNL Workfront].

## Atualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

O Experience Manager Assets permite que você atualize o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente.

Para atualizar o [!DNL Workfront for Experience Manager enhanced connector] para a versão mais recente:

1. Baixe a versão mais recente do conector aprimorado do [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Instale o pacote usando o [!UICONTROL Gerenciador de Pacotes]. Para saber como instalar pacotes, consulte a [documentação do Gerenciador de Pacotes](/help/sites-administering/package-manager.md).
