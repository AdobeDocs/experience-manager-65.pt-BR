---
title: Criação de formulários do Adobe Campaign no AEM
seo-title: Criação de formulários do Adobe Campaign no AEM
description: O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site. Campos específicos podem ser inseridos nos seus formulários e mapeados para o banco de dados do Adobe Campaign.
seo-description: O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site. Campos específicos podem ser inseridos nos seus formulários e mapeados para o banco de dados do Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Criação de formulários do Adobe Campaign no AEM{#creating-adobe-campaign-forms-in-aem}

O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site. Campos específicos podem ser inseridos nos seus formulários e mapeados para o banco de dados do Adobe Campaign.

Você pode gerenciar novas assinaturas de contato, cancelamentos de assinatura e dados de perfis de usuário e, ao mesmo tempo, integrar todos esses dados ao seu banco de dados do Adobe Campaign.

Para usar formulários do Adobe Campaign no AEM, você precisa seguir as etapas descritas neste documento:

1. Disponibilizar um modelo.
1. Criar um formulário.
1. Editar o conteúdo do formulário.

Três tipos de formulários, específicos para o Adobe Campaign, estão disponíveis por padrão:

* Salvar um perfil
* Assinar um serviço
* Cancelar a assinatura de um serviço

Esses formulários definem um parâmetro de URL que aceita a chave primária criptografada de um perfil do Adobe Campaign. Com base nesse parâmetro de URL, o formulário atualiza os dados do perfil do Adobe Campaign associado.

Embora esses formulários sejam criados independentemente, em um caso de uso típico, você gera um link personalizado para uma página de formulário dentro do conteúdo do informativo, para que os destinatários possam abri-lo e fazer ajustes nos dados do perfil (seja cancelando a assinatura, assinando ou atualizando o perfil).

O formulário é atualizado automaticamente com base no usuário. Consulte [Edição do conteúdo do formulário](#editing-form-content) para obter mais informações.

## Disponibilizar um modelo {#making-a-template-available}

Antes de criar formulários específicos para o Adobe Campaign, você deve disponibilizar os diferentes modelos no seu aplicativo AEM.

To do this, see the [Templates documentation](/help/sites-developing/page-templates-static.md#templateavailability).

Em primeiro lugar, verifique a conexão entre as instâncias de autor e publicação e verifique se o Adobe Campaign está funcionando. Consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Integração com o Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifique se a propriedade **acMapping** no nó **jcr:content** da página está definida como **mapRecipient** ou **profile** ao usar o Adobe Campaign 6.1.x ou o Adobe Campaign Standard, respectivamente


### Criação de um formulário {#creating-a-form}

1. Comece em siteadmin.
1. Percorra a estrutura da árvore para chegar ao local em que você gostaria de criar o formulário no site escolhido.
1. **Selecione** Novo **>** Nova página... .
1. Select either **Adobe Campaign Profile (AC 6.1)** or **Adobe Campaign Profile (ACS)** template and enter the page properties.

   >[!NOTE]
   >
   >If the template is not available, refer to the [Making a template available](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) section.

1. Click **Create** to create the form.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Em seguida, você pode [editar e configurar o conteúdo do seu formulário](#editing-form-content).

## Edição do conteúdo do formulário {#editing-form-content}

Formulários dedicados ao Adobe Campaign têm componentes específicos. Esses componentes têm uma opção para permitir que você vincule cada campo do formulário a um campo no banco de dados do Adobe Campaign.

>[!NOTE]
>
>If the desired template is not available, see [Making a template available](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta seção apenas detalha links específicos para o Adobe Campaign. For more information on a more general overview of how to use forms in Adobe Experience Manager, see [Editmode components](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Navegue até o formulário que você deseja editar.
1. **Na caixa de ferramentas, selecione** Página **> Propriedades** da página... em seguida, vá para a guia Serviços **em** nuvem da janela pop-up.
1. Add the Adobe Campaign service by clicking **Add service**, and then selecting the configuration that corresponds to your Adobe Campaign instance in the service&#39;s drop down list. Essa configuração é realizada ao configurar a conexão entre as suas instâncias. For more information, see [Connecting AEM to Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessário, desbloqueie a configuração clicando no ícone de cadeado para adicionar o serviço do Adobe Campaign.

1. Access the form&#39;s general parameters using the **Edit** button found at the start of the form. The **Form** tab allows you to select a thank you page to which the user will be redirected after having validated the form.

   The **Advanced** form allows you to select the type of form. The **Post Options** field gives you the choice between three types of Adobe Campaign forms:

   * **Adobe Campaign: salvar perfil**: permite criar ou atualizar um destinatário no Adobe Campaign (valor padrão).
   * **Adobe Campaign: inscrever-se para os serviços**: permite gerenciar as assinaturas de um destinatário no Adobe Campaign.
   * **Adobe Campaign: cancelar a assinatura dos serviços**: permite cancelar as assinaturas de um destinatário no Adobe Campaign.
   The **Action Configuration** field lets you specify whether or not you would like to create the recipient profile in the Adobe Campaign database if it does not yet exist. To do this, check the **Create user if not existing** option.

1. Adicione os componentes selecionados arrastando-os da caixa de ferramentas e soltando-os no formulário. Para obter mais informações sobre os componentes específicos disponíveis do Adobe Campaign, consulte [Componentes do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure os campos adicionados clicando neles duas vezes. The **Adobe Campaign** tab lets you link the field to a field in the Adobe Campaign recipient table. Você também pode especificar se o campo faz parte da chave de reconciliação, que permite que os destinatários já presentes no banco de dados do Adobe Campaign sejam reconhecidos.

   >[!CAUTION]
   >
   >The **Element Name** must be different for each form field. Altere-o se necessário.
   >
   >Each form must contain an **Encrypted Primary Key** component in order to correctly manage recipients in the Adobe Campaign database.

1. Activate the page by selecting **Page** > **Activate Page** in the toolbox. A página está ativada no seu site. Você pode visualizá-la acessando a instância de publicação do AEM. Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.

## Teste de um formulário {#testing-a-form}

Depois de criar um formulário e editar seu conteúdo, convém testar manualmente se ele está funcionando conforme esperado.

>[!NOTE]
>
>You must have an **Encryted Primary Key** component on each form. Em Componentes, selecione Adobe Campaign para que apenas esses componentes fiquem visíveis.
>
>Neste procedimento, embora você insira o número da EPK manualmente, na prática os usuários receberiam um link para essa página (para cancelar a assinatura, assinar ou atualizar seu perfil) em um informativo. Com base no usuário, a EPK é atualizada automaticamente.
>
>To create that link, you use the variable **Main resource identifier**(Adobe Campaign Standard) or **Encrypted identifier** (Adobe Campaign 6.1) (for example, in a **Text &amp; Personalization (Campaign)** component), which links to the epk in Adobe Campaign.

Para fazer isso, você precisa obter manualmente a EPK de um perfil do Adobe Campaign e, em seguida, anexá-la ao URL:

1. Para obter a chave primária criptografada (EPK) de um perfil do Adobe Campaign:

   * In Adobe Campaign Standard - Navigate to **Profiles and Audiences** > **Profiles**, which lists the existing profiles. Make sure the table displays the **Main Resource Identifier** field in a column (This can be configured by clicking/tapping **Configure list**). Copie o identificador de recursos principal do perfil desejado.
   * In Adobe Campaign 6.11, go to **Profiles and Targets** >  **Recipients**, which lists the existing profiles. Make sure the table displays the **Encrypted identifier** field in a column (This can be configured by right-clicking on an entry and selecting **Configure list...**). Copie o identificador criptografado do perfil desejado.

1. In AEM, open the form page on the publish instance and append the EPK from step 1 as a URL parameter: use the same name that you previously defined in the EPK component when authoring the form (for example: `?epk=...`)
1. O formulário agora pode ser usado para modificar os dados e as assinaturas associadas ao perfil vinculado do Adobe Campaign. Depois de modificar alguns campos e enviar o formulário, você pode verificar no Adobe Campaign se os dados apropriados foram atualizados.

Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.
