---
title: Criar Adobe Campaign Forms no Adobe Experience Manager
description: O Adobe Experience Manager permite criar e usar formulários que interagem com o Adobe Campaign no seu site
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 0%

---

# Criação do Adobe Campaign Forms no AEM {#creating-adobe-campaign-forms-in-aem}

O AEM permite criar e usar formulários que interagem com o Adobe Campaign no seu site. Campos específicos podem ser inseridos em seus formulários e mapeados para o banco de dados do Adobe Campaign.

É possível gerenciar novas assinaturas de contatos, assinaturas canceladas e dados de perfil do usuário, tudo isso enquanto integra os dados dessas assinaturas ao banco de dados do Adobe Campaign.

Para usar o Adobe Campaign Forms no AEM, você precisa seguir estas etapas, descritas neste documento:

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

Antes de criar formulários específicos do Adobe Campaign, você deve disponibilizar os diferentes modelos no aplicativo do AEM.

Para fazer isso, consulte a [documentação sobre modelos](/help/sites-developing/templates.md#template-availability).

## Criação de um formulário {#creating-a-form}

Primeiro, verifique se a conexão entre as instâncias de autor e publicação e o Adobe Campaign está funcionando. Consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Integração com o Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifique se a propriedade **acMapping** no nó **jcr:content** da página está definida como **mapRecipient** ou **profile** ao usar o Adobe Campaign Classic ou o Adobe Campaign Standard, respectivamente
>

1. No AEM, no Sites, navegue até o local em que deseja criar uma página.
1. Crie uma página e selecione **Perfil do Adobe Campaign Classic** ou **Perfil do Adobe Campaign Standard** e clique em **Avançar**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se o modelo desejado não estiver disponível, consulte [Disponibilidade de Modelo](/help/sites-developing/templates.md#template-availability).

1. No campo **Nome**, adicione o nome da página. Deve ser um nome válido de JCR.
1. No campo **Título**, insira um título e clique em **Criar**.
1. Abra a página e selecione **Abrir propriedades**. Nos Serviços em Nuvem, adicione a configuração do Adobe Campaign e marque a marca de seleção para salvar as alterações.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Na página, no componente **Início do Formulário**, selecione o tipo de formulário que é - **Assinar, Cancelar Assinatura,** ou **Salvar Perfil**. Você só pode ter um tipo por formulário. Agora você pode [editar o conteúdo do formulário](#editing-form-content).

## Editar conteúdo do formulário {#editing-form-content}

O Forms dedicado ao Adobe Campaign tem componentes específicos. Esses componentes têm uma opção para permitir vincular cada campo do formulário a um campo no banco de dados do Adobe Campaign.

>[!NOTE]
>
>Se o modelo desejado não estiver disponível, consulte [Disponibilizando um modelo.](/help/sites-authoring/campaign.md)

Esta seção só detalha links específicos para o Adobe Campaign. Para obter mais informações sobre uma visão geral de como usar formulários no Adobe Experience Manager, consulte [Componentes do modo de edição](/help/sites-authoring/default-components-foundation.md).

1. Selecione **Abrir propriedades** e, nos Serviços em nuvem, adicione a configuração do Adobe Campaign e marque a marca de seleção para salvar as alterações.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Na página, no componente **Início do formulário**, clique no ícone Configuração.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Clique na guia **Avançado** e selecione o tipo de formulário que é - **Assinar, Cancelar Inscrição** ou **Salvar Perfil** e clique em **OK.** Só é possível ter um tipo por formulário.

   * **Adobe Campaign: Salvar perfil**: permite criar ou atualizar um destinatário no Adobe Campaign (valor padrão).
   * **Adobe Campaign: Assinar Serviços**: permite gerenciar as assinaturas de um destinatário no Adobe Campaign.
   * **Adobe Campaign: cancelar a assinatura dos serviços**: permite cancelar as assinaturas de um destinatário no Adobe Campaign.

1. Você deve ter um componente de **Chave primária criptografada** em cada formulário. Esse componente define qual parâmetro de URL é usado para aceitar a chave primária criptografada de um perfil do Adobe Campaign. Em Componentes, selecione Adobe Campaign para que somente os componentes fiquem visíveis.
1. Arraste o componente **Chave primária criptografada** para o formulário (em qualquer lugar) e clique no ícone **Configuração**. Na guia **Adobe Campaign**, especifique qualquer nome para o parâmetro de URL. Clique na marca de seleção para salvar as alterações.

   Os links gerados para este formulário precisam usar este parâmetro de URL e atribuir a ele a chave primária criptografada de um perfil do Adobe Campaign. A chave primária criptografada deve ser corretamente codificada no URL (porcentagem).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Adicione componentes ao formulário conforme necessário, como um campo de Texto, campo de Data, campo Caixa de seleção, campo de Opção e assim por diante. Consulte [Componentes de formulários do Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obter mais informações sobre cada componente.
1. Clique no ícone Configuração para abrir o componente. Por exemplo, no componente **Campo de texto (Campanha)**, altere o título e o texto.

   Clique em **Adobe Campaign** para mapear o campo de formulário para uma variável de metadados do Adobe Campaign. Ao enviar o formulário, o campo mapeado é atualizado no Adobe Campaign. Somente os campos com tipos correspondentes estão disponíveis no seletor de variáveis (por exemplo, variáveis de sequência para campos de texto).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Você pode adicionar/remover campos exibidos na tabela de destinatários seguindo as instruções aqui: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Clique em **Publicar página**. A página é ativada no site. Você pode visualizá-lo acessando a instância de publicação do AEM. Você também pode [testar um formulário](#testing-a-form).

   >[!CAUTION]
   >
   >Você precisa fornecer permissões de leitura ao usuário anônimo no Cloud Service para usar formulários na publicação. No entanto, esteja ciente dos possíveis problemas de segurança no fornecimento de permissões de leitura ao usuário anônimo e certifique-se de atenuá-los, por exemplo, configurando o dispatcher.

## Testando um formulário {#testing-a-form}

Depois de criar um formulário e editar o conteúdo do formulário, você pode testar manualmente se o formulário está funcionando como esperado.

>[!NOTE]
>
>Você deve ter um componente de **Chave primária criptografada** em cada formulário. Em Componentes, selecione Adobe Campaign para que somente os componentes fiquem visíveis.
>
>Embora neste procedimento você insira o número epk manualmente, na prática, os usuários obteriam um link para esta página (se cancelariam a inscrição, assinariam ou atualizariam seu perfil) em um boletim informativo. Com base no usuário, o epk é atualizado automaticamente.
>
>Para criar esse link, use a variável **Identificador de recurso principal**(Adobe Campaign Standard) ou **Identificador criptografado** (Adobe Campaign Classic) (por exemplo, em um componente **Text &amp; Personalization (Campaign)**), que se vincula ao epk no Adobe Campaign.

Para fazer isso, é necessário obter manualmente o EPK de um perfil do Adobe Campaign e anexá-lo ao URL:

1. Para obter a chave primária criptografada (EPK) de um perfil do Adobe Campaign:

   * No Adobe Campaign Standard - Navegue até **Perfis e públicos-alvo** > **Perfis**, que lista os perfis existentes. Verifique se a tabela exibe o campo **Identificador de Recurso Principal** em uma coluna (Isso pode ser configurado ao clicar/tocar em **Configurar lista**). Copie o identificador de recurso principal do perfil desejado.
   * No Adobe Campaign Classic, vá para **Profiles and Targets** > **Recipients**, que lista os perfis existentes. Verifique se a tabela exibe o campo **Identificador criptografado** em uma coluna (isso pode ser configurado ao clicar com o botão direito do mouse em uma entrada e selecionar **Configurar lista...**). Copie o identificador criptografado do perfil desejado.

1. No AEM, abra a página de formulário na instância de publicação e anexe o EPK da etapa 1 como um parâmetro de URL: use o mesmo nome definido anteriormente no componente EPK ao criar o formulário (por exemplo: `?epk=...`)
1. O formulário agora pode ser usado para modificar os dados e as assinaturas associados ao perfil vinculado do Adobe Campaign. Depois de modificar alguns campos e enviar o formulário, você pode verificar no Adobe Campaign se os dados apropriados foram atualizados.

Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.
