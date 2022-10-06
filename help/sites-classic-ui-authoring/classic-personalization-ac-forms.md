---
title: Criação de formulários do Adobe Campaign no AEM
seo-title: Creating Adobe Campaign Forms in AEM
description: O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site. Campos específicos podem ser inseridos nos seus formulários e mapeados para o banco de dados do Adobe Campaign.
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website. Specific fields can be inserted into your forms and mapped to the Adobe Campaign database.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 62%

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

Para fazer isso, consulte a [Documentação de modelos](/help/sites-developing/page-templates-static.md#templateavailability).

Em primeiro lugar, verifique a conexão entre as instâncias de autor e publicação e verifique se o Adobe Campaign está funcionando. Consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Integração com o Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifique se a propriedade **acMapping** no nó **jcr:content** da página está definida como **mapRecipient** ou **profile** ao usar o Adobe Campaign 6.1.x ou o Adobe Campaign Standard, respectivamente

### Criação de um formulário {#creating-a-form}

1. Comece em siteadmin.
1. Percorra a estrutura da árvore para chegar ao local em que você gostaria de criar o formulário no site escolhido.
1. Selecionar **Novo** > **Nova página...**.
1. Selecione um **Perfil do Adobe Campaign (AC 6.1)** ou **Perfil do Adobe Campaign (ACS)** e insira as propriedades da página.

   >[!NOTE]
   >
   >Se o modelo não estiver disponível, consulte a [Disponibilizar um template](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) seção.

1. Clique em **Criar** para criar o formulário.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Em seguida, você pode [editar e configurar o conteúdo do seu formulário](#editing-form-content).

## Edição do conteúdo do formulário {#editing-form-content}

Formulários dedicados ao Adobe Campaign têm componentes específicos. Esses componentes têm uma opção para permitir que você vincule cada campo do formulário a um campo no banco de dados do Adobe Campaign.

>[!NOTE]
>
>Se o modelo desejado não estiver disponível, consulte [Disponibilizar um template](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta seção apenas detalha links específicos para o Adobe Campaign. Para obter mais informações sobre uma visão geral de como usar formulários no Adobe Experience Manager, consulte [Componentes do modo de edição](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Navegue até o formulário que você deseja editar.
1. Na caixa de ferramentas, selecione **Página** > **Propriedades da Página...** em seguida, vá para o **Cloud Services** da janela pop-up.
1. Adicione o serviço Adobe Campaign clicando em **Adicionar serviço** e, em seguida, selecionando a configuração que corresponde à instância do Adobe Campaign na lista suspensa do serviço. Essa configuração é realizada ao configurar a conexão entre as suas instâncias. Para obter mais informações, consulte [Conectando AEM ao Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessário, desbloqueie a configuração clicando no ícone de cadeado para adicionar o serviço do Adobe Campaign.

1. Acesse os parâmetros gerais do formulário usando o **Editar** encontrado no início do formulário. O **Formulário** permite selecionar uma página de agradecimento para a qual o usuário será redirecionado após ter validado o formulário.

   O **Avançado** permite selecionar o tipo de formulário. O **Opções de publicação** O campo oferece a você a escolha entre três tipos de formulários do Adobe Campaign:

   * **Adobe Campaign: salvar perfil**: permite criar ou atualizar um destinatário no Adobe Campaign (valor padrão).
   * **Adobe Campaign: inscrever-se para os serviços**: permite gerenciar as assinaturas de um destinatário no Adobe Campaign.
   * **Adobe Campaign: cancelar a assinatura dos serviços**: permite cancelar as assinaturas de um destinatário no Adobe Campaign.

   O **Configuração de ação** permite especificar se deseja ou não criar o perfil do recipient no banco de dados do Adobe Campaign, caso ele ainda não exista. Para fazer isso, marque a opção **Criar usuário se não existir** opção.

1. Adicione os componentes selecionados arrastando-os da caixa de ferramentas e soltando-os no formulário. Para obter mais informações sobre os componentes específicos disponíveis do Adobe Campaign, consulte [Componentes do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure os campos adicionados clicando neles duas vezes. O **Adobe Campaign** permite vincular o campo a um campo na tabela de recipients do Adobe Campaign. Você também pode especificar se o campo faz parte da chave de reconciliação, que permite que os destinatários já presentes no banco de dados do Adobe Campaign sejam reconhecidos.

   >[!CAUTION]
   >
   >O **Nome do elemento** deve ser diferente para cada campo de formulário. Altere-o se necessário.
   >
   >Cada formulário deve conter um **Chave primária criptografada** para gerenciar corretamente os recipients no banco de dados do Adobe Campaign.

1. Ative a página selecionando **Página** > **Ativar página** na caixa de ferramentas. A página está ativada no seu site. Você pode visualizá-la acessando a instância de publicação do AEM. Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.

## Teste de um formulário {#testing-a-form}

Depois de criar um formulário e editar seu conteúdo, convém testar manualmente se ele está funcionando conforme esperado.

>[!NOTE]
>
>Você deve ter um **Chave primária criptografada** em cada formulário. Em Componentes, selecione Adobe Campaign para que apenas esses componentes fiquem visíveis.
>
>Neste procedimento, embora você insira o número da EPK manualmente, na prática os usuários receberiam um link para essa página (para cancelar a assinatura, assinar ou atualizar seu perfil) em um informativo. Com base no usuário, a EPK é atualizada automaticamente.
>
>Para criar esse link, use a variável **Identificador de recurso principal**(Adobe Campaign Standard) ou **Identificador criptografado** (Adobe Campaign 6.1) (por exemplo, em um **Texto e personalização (Campaign)** componente), que vincula à EPK no Adobe Campaign.

Para fazer isso, você precisa obter manualmente a EPK de um perfil do Adobe Campaign e, em seguida, anexá-la ao URL:

1. Para obter a chave primária criptografada (EPK) de um perfil do Adobe Campaign:

   * No Adobe Campaign Standard - navegue para **Perfis e públicos-alvo** > **Perfis**, que lista os perfis existentes. Certifique-se de que a tabela exiba a variável **Identificador de recurso principal** em uma coluna (É possível configurar clicando/tocando em **Configurar lista**). Copie o identificador de recursos principal do perfil desejado.
   * No Adobe Campaign 6.11, acesse **Perfis e metas** >  **Recipients**, que lista os perfis existentes. Certifique-se de que a tabela exiba a variável **Identificador criptografado** em uma coluna (É possível configurar clicando com o botão direito do mouse em uma entrada e selecionando **Configurar lista...**). Copie o identificador criptografado do perfil desejado.

1. Em AEM, abra a página do formulário na instância de publicação e anexe a EPK da etapa 1 como um parâmetro de URL: use o mesmo nome definido anteriormente no componente EPK ao criar o formulário (por exemplo: `?epk=...`)
1. O formulário agora pode ser usado para modificar os dados e as assinaturas associadas ao perfil vinculado do Adobe Campaign. Depois de modificar alguns campos e enviar o formulário, você pode verificar no Adobe Campaign se os dados apropriados foram atualizados.

Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.
