---
title: Direcionamento sua campanha do Adobe Campaign
seo-title: Direcionamento sua campanha do Adobe Campaign
description: Você pode criar experiências direcionadas para o Adobe Campaign depois de configurar a segmentação
seo-description: Você pode criar experiências direcionadas para o Adobe Campaign depois de configurar a segmentação
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Direcionamento sua campanha do Adobe Campaign{#targeting-your-adobe-campaign}

Para segmentar seu informativo do Adobe Campaign, você precisa primeiro configurar a segmentação, que só está disponível na IU Clássica (para o contexto do cliente). Depois disso, será possível criar experiências direcionadas para o Adobe Campaign. Ambos os processos estão descritos nesta seção.

## Configuração da segmentação no AEM {#setting-up-segmentation-in-aem}

Para configurar a segmentação, você precisa usar a interface de usuário clássica para configurar os segmentos. As etapas restantes podem ser realizadas na interface de usuário padrão.

A configuração da segmentação inclui a criação de segmentos, uma marca, uma campanha e experiências.

>[!NOTE]
>
>O ID do segmento precisa ser mapeado para aquele no lado do Adobe Campaign.

### Criação de segmentos {#creating-segments}

Para criar segmentos:

1. Open the [segmentation console](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Create a new page and enter a title - for example, **AC Segments**- and select the **Segment (Adobe Campaign)** template.
1. Selecione a página criada na exibição em árvore no lado esquerdo.
1. Crie um segmento, por exemplo, direcionando usuários do sexo masculino, criando uma nova página no segmento criado com o nome Masculino, e selecione o modelo **Segmento (Adobe Campaign)**.
1. Abra a página de segmento criada e arraste e solte um **ID de segmento** do sidekick até a página.
1. Double-click the trait, enter the ID representing in this case, the male segment defined in Adobe Campaign - for example, **MALE** - and click **OK**. The following message should appear: *`targetData.segmentCode == "MALE"`*
1. Repita as etapas para outro segmento, por exemplo, um segmento direcionado para usuários do sexo feminino.

### Criação de uma marca {#creating-a-brand}

Para criar uma marca:

1. Em **Sites**, navegue até a pasta **Campanhas** (por exemplo, em We.Retail).
1. Clique em **Criar página** e insira um título para a página, por exemplo, Marca We.Retail, e selecione o modelo **Marca**.

### Criando uma campanha {#creating-a-campaign}

Para criar uma campanha:

1. Abra a página **Marca** que você acabou de criar.
1. Clique em **Criar página** e insira um título para a sua página, por exemplo, Campanha We.Retail, selecione o modelo **Campanha** e clique em **Criar**.

### Criação de experiências {#creating-experiences}

Para criar experiências para segmentos:

1. Abra a página **Campanha** que você acabou de criar.
1. Create experiences for your segments by clicking **Create Page** and entering a title for your page, for example, Male as you are creating an experience for the Male segment, and select the **Experience** template.
1. Abra a página de Experiência criada.
1. Clique em **Editar** e, em seguida, abaixo de Segmentos, clique em **Adicionar item**.
1. Enter the path to the male segment, for example **/etc/segmentation/ac-segments/male** and click **OK**. The following message should appear: *Experience is targeted at: Male*
1. Repita as etapas anteriores para criar uma experiência para todos os segmentos, por exemplo, o direcionamento de usuários do sexo feminino.

## Criação de um informativo com conteúdo direcionado {#creating-a-newsletter-with-targeted-content}

Depois de criar segmentos, uma marca, uma campanha e uma experiência, você pode criar um informativo com conteúdo direcionado. Depois de criar a experiência, você a vincula aos seus segmentos.

>[!NOTE]
>
>[Amostras de email estão disponíveis apenas no Geometrixx](/help/sites-developing/we-retail.md). Baixe o conteúdo de amostra do Geometrixx pelo Compartilhamento de pacotes.

Para criar um informativo com conteúdo direcionado:

1. Create a newsletter with targeted content: Below Email Campaigns in Geometrixx Outdoors, click or tap **Create** > **Page**, and select one of the Adobe Campaign Mail templates.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. No informativo, adicione um componente Texto e personalização.
1. Adicione texto ao componente Texto e personalização, como &quot;Este é o padrão&quot;.
1. Click the arrow next to **Edit** and select **Targeting**.
1. Selecione sua marca no menu suspenso Marca e selecione sua campanha. (Essa é a marca e a campanha que você criou anteriormente).
1. Clique em **Iniciar o direcionamento**. Você vê seus segmentos aparecerem na área Públicos. A experiência padrão será usada se nenhum dos segmentos definidos corresponder.

   >[!NOTE]
   >
   >Por padrão, as amostras de email incluídas no AEM usam o Adobe Campaign como mecanismo de direcionamento. Para informativos personalizados, talvez seja necessário selecionar o Adobe Campaign como mecanismo de direcionamento. Ao fazer o direcionamento, toque ou clique em + na barra de ferramentas, insira um título para a nova atividade e selecione **Adobe Campaign** como o mecanismo de direcionamento.

1. Clique em **Padrão** e depois no componente Texto e personalização adicionado. Você verá a mira com uma seta nela. Clique no ícone para direcionar esse componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Navegue até outro segmento (Masculino), clique em **Adicionar oferta** e clique no ícone de adição +. Em seguida, edite a oferta.
1. Navegue até outro segmento (Feminino), clique em **Adicionar oferta** e no ícone de adição +. Em seguida, edite essa oferta.
1. Click **Next** to see Mapping, then click **Next** to see Settings, which does not apply to Adobe Campaign, and click **Save**.

   O AEM gera automaticamente o código de direcionamento correto para o Adobe Campaign quando o conteúdo é usado em uma entrega dentro do Adobe Campaign

1. No Adobe Campaign, crie sua entrega. Selecione **Entrega de email com conteúdo do AEM** e escolha a conta do AEM local, conforme apropriado, e confirme suas alterações.

   Na exibição HTML, as diferentes experiências dos componentes de destino são incluídas no código de direcionamento do Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Se você também definir os segmentos no Adobe Campaign, clicar em **Visualizar** mostrará as experiências para cada segmento.

