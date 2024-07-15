---
title: Criação do Adobe Campaign Forms no AEM
description: O AEM permite criar e usar formulários que interagem com o Adobe Campaign em seu site. Campos específicos podem ser inseridos em seus formulários e mapeados para o banco de dados do Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Criação do Adobe Campaign Forms no AEM{#creating-adobe-campaign-forms-in-aem}

O AEM permite criar e usar formulários que interagem com o Adobe Campaign em seu site. Campos específicos podem ser inseridos em seus formulários e mapeados para o banco de dados do Adobe Campaign.

É possível gerenciar novas assinaturas de contatos, assinaturas canceladas e dados de perfil do usuário, tudo isso enquanto integra os dados dessas assinaturas ao banco de dados do Adobe Campaign.

Para usar os formulários do Adobe Campaign no AEM, é necessário seguir estas etapas, descritas neste documento:

1. Disponibilize um modelo.
1. Crie um formulário.
1. Editar conteúdo do formulário.

Três tipos de formulários, específicos para o Adobe Campaign, estão disponíveis por padrão:

* Salvar um perfil
* Assinar um serviço
* Cancelar assinatura de um serviço

Esses formulários definem um parâmetro de URL que aceita a chave primária criptografada de um perfil do Adobe Campaign. Com base nesse parâmetro de URL, o formulário atualiza os dados do perfil do Adobe Campaign associado.

Embora esses formulários sejam criados de maneira independente, em um caso de uso típico, você gera um link personalizado para uma página de formulário dentro do conteúdo do boletim informativo, para que os destinatários possam abrir o link e fazer ajustes nos dados de perfil (seja para cancelar a assinatura, assinar ou atualizar o perfil).

O formulário é atualizado automaticamente com base no usuário. Consulte [Editando o Conteúdo do Formulário](#editing-form-content) para obter mais informações.

## Disponibilizar um modelo {#making-a-template-available}

Antes de criar formulários específicos para o Adobe Campaign, você deve disponibilizar os diferentes modelos no aplicativo AEM.

Para fazer isso, consulte a [documentação sobre modelos](/help/sites-developing/page-templates-static.md#templateavailability).

Primeiro, verifique se a conexão entre as instâncias de autor e publicação e o Adobe Campaign está funcionando. Consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Integração com o Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifique se a propriedade **acMapping** no nó **jcr:content** da página está definida como **mapRecipient** ou **profile** ao usar o Adobe Campaign 6.1.x ou o Adobe Campaign Standard, respectivamente
>

### Criação de um formulário {#creating-a-form}

1. Inicie no siteadmin.
1. Percorra a estrutura de árvore para chegar ao local em que deseja criar o formulário no site escolhido.
1. Selecione **Nova** > **Nova página...**.
1. Selecione o modelo **Perfil do Adobe Campaign (AC 6.1)** ou **Perfil do Adobe Campaign (ACS)** e insira as propriedades da página.

   >[!NOTE]
   >
   >Se o modelo não estiver disponível, consulte a seção [Disponibilizando um modelo](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

1. Clique em **Criar** para criar o formulário.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Em seguida, você pode [editar e configurar o conteúdo do seu formulário](#editing-form-content).

## Editar conteúdo do formulário {#editing-form-content}

O Forms dedicado ao Adobe Campaign tem componentes específicos. Esses componentes têm uma opção para permitir vincular cada campo do formulário a um campo no banco de dados do Adobe Campaign.

>[!NOTE]
>
>Se o modelo desejado não estiver disponível, consulte [Disponibilizando um modelo](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta seção só detalha links específicos para o Adobe Campaign. Para obter mais informações sobre uma visão geral de como usar formulários no Adobe Experience Manager, consulte [Componentes do modo de edição](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Navegue até o formulário que deseja editar.
1. Na caixa de ferramentas, selecione **Página** > **Propriedades da Página...** e vá para a guia **Cloud Service** da janela pop-up.
1. Adicione o serviço do Adobe Campaign clicando em **Adicionar serviço** e selecionando a configuração que corresponde à sua instância do Adobe Campaign na lista suspensa do serviço. Essa configuração é realizada ao configurar a conexão entre suas instâncias. Para obter mais informações, consulte [Conectando o AEM ao Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessário, desbloqueie a configuração clicando no ícone de cadeado para poder adicionar o serviço Adobe Campaign.

1. Acesse os parâmetros gerais do formulário usando o botão **Editar** localizado no início do formulário. A guia **Formulário** permite selecionar uma página de agradecimento para a qual o usuário será redirecionado após validar o formulário.

   O formulário **Advanced** permite selecionar o tipo de formulário. O campo **Opções do Post** fornece a escolha entre três tipos de formulários do Adobe Campaign:

   * **Adobe Campaign: Salvar perfil**: permite criar ou atualizar um destinatário no Adobe Campaign (valor padrão).
   * **Adobe Campaign: Assinar Serviços**: permite gerenciar as assinaturas de um destinatário no Adobe Campaign.
   * **Adobe Campaign: cancelar a assinatura dos serviços**: permite cancelar as assinaturas de um destinatário no Adobe Campaign.

   O campo **Configuração de ação** permite especificar se você deseja ou não criar o perfil do destinatário no banco de dados do Adobe Campaign se ele ainda não existir. Para fazer isso, marque a opção **Criar usuário se não existir**.

1. Adicione os componentes selecionados arrastando-os da caixa de ferramentas e soltando-os no formulário. Para obter mais informações sobre os componentes específicos disponíveis do Adobe Campaign, consulte [Componentes de forma do Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure os campos adicionados clicando duas vezes neles. A guia **Adobe Campaign** permite vincular o campo a um campo na tabela de destinatários do Adobe Campaign. Você também pode especificar se o campo faz parte da chave de reconciliação, que permite que os recipients que já estão presentes no banco de dados do Adobe Campaign sejam reconhecidos.

   >[!CAUTION]
   >
   >O **Nome do Elemento** deve ser diferente para cada campo de formulário. Altere-o se necessário.
   >
   >Cada formulário deve conter um componente **Chave primária criptografada** para gerenciar corretamente os destinatários no banco de dados do Adobe Campaign.

1. Ative a página selecionando **Página** > **Ativar Página** na caixa de ferramentas. A página é ativada no site. Você pode visualizá-lo acessando a instância de publicação do AEM. Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.

## Testando um formulário {#testing-a-form}

Depois de criar um formulário e editar o conteúdo do formulário, você pode testar manualmente se o formulário está funcionando como esperado.

>[!NOTE]
>
>Você deve ter um componente de **Chave primária criptografada** em cada formulário. Em Componentes, selecione Adobe Campaign para que somente os componentes fiquem visíveis.
>
>Embora neste procedimento você insira o número epk manualmente, na prática, os usuários obteriam um link para esta página (se cancelariam a inscrição, assinariam ou atualizariam seu perfil) em um boletim informativo. Com base no usuário, o epk é atualizado automaticamente.
>
>Para criar esse link, use a variável **Identificador de recurso principal**(Adobe Campaign Standard) ou **Identificador criptografado** (Adobe Campaign 6.1) (por exemplo, em um componente **Text &amp; Personalization (Campaign)**), que se vincula ao epk no Adobe Campaign.

Para fazer isso, é necessário obter manualmente o EPK de um perfil do Adobe Campaign e anexá-lo ao URL:

1. Para obter a chave primária criptografada (EPK) de um perfil do Adobe Campaign:

   * No Adobe Campaign Standard - Navegue até **Perfis e públicos-alvo** > **Perfis**, que lista os perfis existentes. Verifique se a tabela exibe o campo **Identificador de Recurso Principal** em uma coluna (Isso pode ser configurado ao clicar/tocar em **Configurar lista**). Copie o identificador de recurso principal do perfil desejado.
   * No Adobe Campaign 6.11, vá para **Profiles and Targets** > **Recipients**, que lista os perfis existentes. Verifique se a tabela exibe o campo **Identificador criptografado** em uma coluna (isso pode ser configurado ao clicar com o botão direito do mouse em uma entrada e selecionar **Configurar lista...**). Copie o identificador criptografado do perfil desejado.

1. No AEM, abra a página de formulário na instância de publicação e anexe o EPK da etapa 1 como um parâmetro de URL: use o mesmo nome definido anteriormente no componente EPK ao criar o formulário (por exemplo: `?epk=...`)
1. O formulário agora pode ser usado para modificar os dados e as assinaturas associados ao perfil vinculado do Adobe Campaign. Depois de modificar alguns campos e enviar o formulário, você pode verificar no Adobe Campaign se os dados apropriados foram atualizados.

Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.
