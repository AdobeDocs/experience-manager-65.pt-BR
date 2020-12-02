---
title: Criação de formulários do Adobe Campaign no AEM
seo-title: Criação de formulários do Adobe Campaign no AEM
description: O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site
seo-description: O AEM permite que você crie e use formulários que interajam com o Adobe Campaign no seu site
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
translation-type: tm+mt
source-git-commit: 2451f4994a18b1566ea0efddbefcaa5bb8e41c99
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 75%

---


# Criação de formulários do Adobe Campaign no AEM {#creating-adobe-campaign-forms-in-aem}

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

## Disponibilizar um modelo  {#making-a-template-available}

Antes de criar formulários específicos para o Adobe Campaign, você deve disponibilizar os diferentes modelos no seu aplicativo AEM.

Para fazer isso, consulte a documentação [Modelos](/help/sites-developing/templates.md#template-availability).

## Criação de um formulário {#creating-a-form}

Em primeiro lugar, verifique a conexão entre as instâncias de autor e publicação e verifique se o Adobe Campaign está funcionando. Consulte [Integração com o Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) ou [Integração com o Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifique se a propriedade **acMapping** no nó **jcr:content** da página está definida como **mapRecipient** ou **profile** ao usar o Adobe Campaign Classic ou o Adobe Campaign Standard, respectivamente


1. No AEM, em Sites, navegue até onde você deseja criar uma nova página.
1. Crie uma página e selecione **Perfil Adobe Campaign Classic** ou **Perfil Adobe Campaign Standard** e clique em **Próximo**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se o modelo desejado não estiver disponível, consulte [Disponibilidade do modelo](/help/sites-developing/templates.md#template-availability).

1. No campo **Nome**, adicione o nome da página. Ele deve ser um nome JCR válido.
1. No campo **Título**, insira um título e clique em **Criar**.
1. Abra a página e selecione **Abrir propriedades** e, em Serviços em nuvem, adicione a configuração do Adobe Campaign e selecione a marca de seleção para salvar as alterações.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Na página, no componente **Início do formulário**, selecione o tipo de formulário - **Assinar, Cancelar assinatura** ou **Salvar perfil**. É possível ter apenas um tipo por formulário. Agora, você pode [editar o conteúdo do formulário](#editing-form-content).

## Edição do conteúdo do formulário {#editing-form-content}

Formulários dedicados ao Adobe Campaign têm componentes específicos. Esses componentes têm uma opção para permitir que você vincule cada campo do formulário a um campo no banco de dados do Adobe Campaign.

>[!NOTE]
>
>Se o modelo desejado não estiver disponível, consulte [Disponibilizar um modelo](/help/sites-authoring/adobe-campaign.md).

Esta seção apenas detalha links específicos para o Adobe Campaign. Para obter mais informações sobre uma visão geral mais geral de como usar formulários no Adobe Experience Manager, consulte [Componentes do modo de edição](/help/sites-authoring/default-components-foundation.md).

1. Selecione **Abrir propriedades** e, em Serviços em nuvem, adicione a configuração do Adobe Campaign e selecione a marca de seleção para salvar suas alterações.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Na página, no componente **Start de formulário**, clique no ícone Configuração.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Clique na guia **Avançado** e selecione o tipo de formulário em que se encontra - **Assinar, Cancelar inscrição,** ou **Guardar Perfil** e clique em **OK.** É possível ter apenas um tipo por formulário.

   * **Adobe Campaign: salvar perfil**: permite criar ou atualizar um destinatário no Adobe Campaign (valor padrão).
   * **Adobe Campaign: inscrever-se para os serviços**: permite gerenciar as assinaturas de um destinatário no Adobe Campaign.
   * **Adobe Campaign: cancelar a assinatura dos serviços**: permite cancelar as assinaturas de um destinatário no Adobe Campaign.

1. Você deve ter um componente **Chave primária criptografada** em cada formulário. Esse componente define qual parâmetro de URL será usado para aceitar a chave primária criptografada de um perfil do Adobe Campaign. Em Componentes, selecione Adobe Campaign para que apenas esses componentes fiquem visíveis.
1. Arraste o componente **Chave primária criptografada** para o formulário (em qualquer lugar) e clique ou toque no ícone **Configuração**. Na guia **Adobe Campaign**, especifique qualquer nome para o parâmetro de URL. Clique ou toque na marca de seleção para salvar as alterações.

   Os links gerados para esse formulário precisam usar esse parâmetro de URL e atribuir a ele a chave primária criptografada de um perfil do Adobe Campaign. A chave primária criptografada deve ser corretamente codificada por URL (porcentagem).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Adicione componentes ao formulário conforme necessário, como um campo de Texto, um campo de Data, um campo de Caixa de seleção, um campo de Opção e assim por diante. Consulte [Componentes de formulário do Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obter mais informações sobre cada componente.
1. Clique no ícone Configuração para abrir o componente. Por exemplo, no componente **Campo de texto (Campanha)**, altere o título e o texto.

   Clique em **Adobe Campaign** para mapear o campo de formulário para uma variável de metadados do Adobe Campaign. Quando você envia o formulário, o campo mapeado é atualizado no Adobe Campaign. Somente campos com tipos correspondentes estão disponíveis no seletor de variáveis (por exemplo, variáveis de sequência de caracteres para campos de texto).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Você pode adicionar/remover campos exibidos na tabela recipient seguindo as instruções aqui: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Clique em **Publicar página**. A página está ativada no seu site. Você pode visualizá-la acessando a instância de publicação do AEM. Você também pode [testar um formulário](#testing-a-form).

   >[!CAUTION]
   >
   >É necessário fornecer permissões de leitura ao usuário anônimo no serviço de nuvem para usar formulários na publicação. No entanto, lembre-se dos possíveis problemas de segurança ao fornecer permissões de leitura ao usuário anônimo e certifique-se de atenuá-lo, por exemplo, configurando o Dispatcher.

## Teste de um formulário  {#testing-a-form}

Depois de criar um formulário e editar seu conteúdo, convém testar manualmente se ele está funcionando conforme esperado.

>[!NOTE]
>
>Você deve ter um componente **Chave primária criptografada** em cada formulário. Em Componentes, selecione Adobe Campaign para que apenas esses componentes fiquem visíveis.
>
>Neste procedimento, embora você insira o número da EPK manualmente, na prática os usuários receberiam um link para essa página (para cancelar a assinatura, assinar ou atualizar seu perfil) em um informativo. Com base no usuário, a EPK é atualizada automaticamente.
>
>Para criar esse link, use a variável **Identificador de recurso principal**(Adobe Campaign Standard) ou **Identificador criptografado** (Adobe Campaign Classic) (por exemplo, em um componente **Texto e personalização (Campanha)**), que vincula à epk no Adobe Campaign.

Para fazer isso, você precisa obter manualmente a EPK de um perfil do Adobe Campaign e, em seguida, anexá-la ao URL:

1. Para obter a chave primária criptografada (EPK) de um perfil do Adobe Campaign:

   * No Adobe Campaign Standard - navegue até **Perfis e Audiências** > **Perfis**, que lista os perfis existentes. Certifique-se de que a tabela exibe o campo **Identificador de Recurso Principal** em uma coluna (Isso pode ser configurado clicando/tocando em **Configurar lista**). Copie o identificador de recursos principal do perfil desejado.
   * No Adobe Campaign Classic, vá para **Perfis e Públicos alvos** > **Recipient**, que lista os perfis existentes. Verifique se a tabela exibe o campo **Identificador criptografado** em uma coluna (Isso pode ser configurado clicando com o botão direito do mouse em uma entrada e selecionando **Configurar lista...**). Copie o identificador criptografado do perfil desejado.

1. Em AEM, abra a página de formulário na instância de publicação e anexe o EPK da etapa 1 como um parâmetro de URL: use o mesmo nome definido anteriormente no componente EPK ao criar o formulário (por exemplo: `?epk=...`)
1. O formulário agora pode ser usado para modificar os dados e as assinaturas associadas ao perfil vinculado do Adobe Campaign. Depois de modificar alguns campos e enviar o formulário, você pode verificar no Adobe Campaign se os dados apropriados foram atualizados.

Os dados no banco de dados do Adobe Campaign são atualizados assim que um formulário é validado.
