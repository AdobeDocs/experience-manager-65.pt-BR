---
title: Trabalhar com o Adobe Campaign 6.1 e o Adobe Campaign Standard
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: Você pode criar conteúdo de email no AEM e processá-lo em emails do Adobe Campaign.
seo-description: You can create email content in AEM and process it in Adobe Campaign emails.
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Trabalhar com o Adobe Campaign 6.1 e o Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Você pode criar conteúdo de email no AEM e processá-lo em emails do Adobe Campaign. Para fazer isso, você deve:

1. Crie um novo boletim informativo no AEM a partir de um modelo específico do Adobe Campaign.
1. Selecionar [um serviço do Adobe Campaign](#selectingtheadobecampaigncloudservice) antes de editar o conteúdo para acessar todas as funcionalidades.
1. Editar o conteúdo.
1. Validar o conteúdo.

O conteúdo pode ser sincronizado com um delivery no Adobe Campaign. As instruções detalhadas estão descritas neste documento.

>[!NOTE]
>
>Antes de usar essa funcionalidade, é necessário configurar o AEM para integrar com o [Adobe Campaign](/help/sites-administering/campaignonpremise.md) ou [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Envio de conteúdo de e-mail via Adobe Campaign {#sending-email-content-via-adobe-campaign}

Depois de configurar o AEM e o Adobe Campaign, é possível criar conteúdo de delivery de email diretamente no AEM e processá-lo no Adobe Campaign.

Ao criar conteúdo do Adobe Campaign no AEM, você deve vincular a um serviço do Adobe Campaign antes de editar o conteúdo para acessar todas as funcionalidades.

Há dois casos possíveis:

* O conteúdo pode ser sincronizado com um delivery do Adobe Campaign. Isso permite usar conteúdo de AEM em um delivery.
* (Somente no Adobe Campaign local) O conteúdo pode ser enviado diretamente para o Adobe Campaign, que gera automaticamente um novo delivery de email. Esse modo tem limitações.

As instruções detalhadas estão descritas neste documento.

### Criação de novo conteúdo de email {#creating-new-email-content}

>[!NOTE]
>
>Ao adicionar modelos de email, adicione-os em **/content/campaigns** disponibilizá-las.

1. No AEM, selecione a variável **Sites** e navegue pelo explorador para encontrar onde suas campanhas de email são gerenciadas. No exemplo a seguir, o nó relacionado é **Sites** > **Campanhas** > **Geometrixx Outdoors** > **Campanhas de email**.

   >[!NOTE]
   >
   >[As amostras de email estão disponíveis somente no Geometrixx](/help/sites-developing/we-retail.md#weretail). Baixe o conteúdo de Geometrixx de amostra do Compartilhamento de pacotes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Selecionar **Novo** > **Nova página** para criar novo conteúdo de email.
1. Selecione um dos modelos disponíveis específicos para o Adobe Campaign e preencha as propriedades gerais da página. Três templates estão disponíveis por padrão:

   * **Email do Adobe Campaign (AC 6.1)**: permite adicionar conteúdo a um modelo predefinido antes de enviá-lo para o Adobe Campaign 6.1 para entrega.
   * **Email do Adobe Campaign (ACS)**: permite adicionar conteúdo a um modelo predefinido antes de enviá-lo para o Adobe Campaign Standard para entrega.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Clique em **Criar** para criar seu email ou informativo.

### Seleção do serviço de nuvem e do modelo do Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Para integrar ao Adobe Campaign, é necessário adicionar um serviço em nuvem do Adobe Campaign à página. Isso fornecerá acesso à personalização e outras informações do Adobe Campaign.

Além disso, talvez também seja necessário selecionar o modelo do Adobe Campaign, alterar o assunto e adicionar conteúdo de texto sem formatação para os usuários que não visualizarão o email no HTML.

1. Selecione o **Página** no sidekick, depois selecione **Propriedades da página.**
1. No **Serviços em nuvem** na janela pop-up, selecione **Adicionar serviço** para adicionar o serviço Adobe Campaign e clique em **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Selecione a configuração que corresponde à instância do Adobe Campaign na lista suspensa e clique em **OK**.

   >[!NOTE]
   >
   >Toque/clique **OK** ou **Aplicar** depois de adicionar o cloud service. Isso habilita a **Adobe Campaign** para funcionar corretamente.

1. Se quiser aplicar um template do delivery de email específico (do Adobe Campaign), diferente do padrão **email** modelo, selecione **Propriedades da página** novamente. No **Adobe Campaign** insira o nome interno do template de delivery de email na instância relacionada do Adobe Campaign.

   No Adobe Campaign Standard, o modelo é **Entrega com conteúdo AEM**. No Adobe Campaign 6.1, o modelo é **Entrega de email com conteúdo AEM**.

   Ao selecionar o modelo, o AEM ativa automaticamente a variável **Informativo do Adobe Campaign** componentes.

### Edição de conteúdo de email {#editing-email-content}

É possível editar conteúdo de email na interface clássica do usuário ou na interface otimizada para toque.

1. Insira o assunto e a versão de texto do email selecionando **Propriedades da página** > **E-mail** na caixa de ferramentas.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Edite o conteúdo do e-mail adicionando os elementos que você gostaria dos disponíveis no sidekick. Para fazer isso, arraste e solte-as. Em seguida, clique duas vezes no elemento que deseja editar.

   Por exemplo, você pode adicionar texto contendo campos de personalização.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Consulte [Componentes do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obter uma descrição dos componentes disponíveis para informativos/campanhas por email do Adobe Campaign.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Inserir personalização {#inserting-personalization}

Ao editar seu conteúdo, você pode inserir:

* Campos de contexto do Adobe Campaign. Esses são campos que você pode inserir no texto que serão adaptados de acordo com os dados do recipient (por exemplo, nome, sobrenome ou quaisquer dados da dimensão de destino).
* Blocos de personalização do Adobe Campaign. Esses são blocos de conteúdo predefinido que não estão relacionados aos dados do recipient, como um logotipo de marca ou um link para uma mirror page.

Consulte [Componentes do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obter uma descrição completa dos componentes do Campaign.

>[!NOTE]
>
>* Somente os campos do Adobe Campaign **Perfis** targeting dimension são considerados.
>* Ao visualizar Propriedades de **Sites**, você não tem acesso aos campos de contexto do Adobe Campaign. É possível acessá-los diretamente do email ao editar.
>


1. Inserir um novo **Informativo** > **Texto e personalização (Campanha)** componente.
1. Abra o componente clicando duas vezes nele. A variável **Editar** tem uma funcionalidade que permite inserir os elementos de personalização.

   >[!NOTE]
   >
   >Os campos de contexto disponíveis correspondem à variável **Perfis** targeting dimension no Adobe Campaign.
   >
   >Consulte [Vinculação de uma página do AEM a um email do Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Selecionar **Client Context** no sidekick para testar os campos de personalização usando os dados nos perfis de persona.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Uma janela é exibida e permite selecionar o perfil desejado. Os campos de personalização são substituídos automaticamente pelos dados do perfil selecionado.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Visualização de informativo {#previewing-a-newsletter}

Você pode visualizar como o informativo será exibido, bem como visualizar a personalização.

1. Abra o informativo que deseja visualizar e clique em Visualizar (lupa) para diminuir o sidekick.
1. Clique em um dos ícones de cliente de email para ver a aparência do informativo em cada cliente de email.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Expanda o sidekick para começar a editar novamente.

### Aprovar conteúdo no AEM {#approving-content-in-aem}

Após a conclusão do conteúdo, é possível iniciar o processo de aprovação. Vá para a **Fluxo de trabalho** da caixa de ferramentas e selecione o **Aprovar para o Adobe Campaign** fluxo de trabalho.

Esse workflow pronto para uso tem duas etapas: revisão e depois aprovação ou revisão e depois rejeição. No entanto, esse fluxo de trabalho pode ser estendido e adaptado a um processo mais complexo.

![chlimage_1-182](assets/chlimage_1-182.png)

Para aprovar o conteúdo do Adobe Campaign, aplique o fluxo de trabalho selecionando **Fluxo de trabalho** no sidekick e ao selecionar **Aprovar para o Adobe Campaign** e clique em **Iniciar fluxo de trabalho**. Percorra as etapas e aprove o conteúdo. Também é possível rejeitar o conteúdo selecionando **Rejeitar** em vez de **Aprovar** na última etapa do workflow.

![chlimage_1-183](assets/chlimage_1-183.png)

Depois que o conteúdo é aprovado, ele é exibido como aprovado no Adobe Campaign. O email pode ser enviado.

No Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

No Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>O conteúdo não aprovado pode ser sincronizado com um delivery no Adobe Campaign, mas o delivery não pode ser executado. Somente o conteúdo aprovado pode ser enviado por meio de deliveries do Campaign.

## Vinculação do AEM ao Adobe Campaign Standard e ao Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Consulte [Vinculação do AEM ao Adobe Campaign Standard e ao Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) em [Trabalhar com o Adobe Campaign 6.1 e o Adobe Campaign Standard](/help/sites-authoring/campaign.md) na documentação de criação padrão para obter detalhes.
