---
title: Direcionamento da sua Adobe Campaign
description: Configurar a segmentação inclui a criação de segmentos, uma marca, campanha e experiências.
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
exl-id: e56986b2-397e-4802-992b-05a9ea7b2e36
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Direcionamento da sua Adobe Campaign{#targeting-your-adobe-campaign}

Para direcionar seu informativo do Adobe Campaign, primeiro você precisa configurar a segmentação, que só está disponível na interface clássica. Depois disso, você poderá criar experiências direcionadas para o Adobe Campaign.

## Configuração da segmentação no AEM {#setting-up-segmentation-in-aem}

Configurar a segmentação inclui a criação de segmentos, uma marca, campanha e experiências. Você só pode criar um segmento na interface clássica. Você pode criar marcas, campanhas e experiências na interface do usuário habilitada para toque.

>[!NOTE]
>
>A ID do segmento precisa ser mapeada para aquela no lado do Adobe Campaign.

### Criação de segmentos {#creating-segments}

Para criar segmentos:

1. Abra o [console de segmentação](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Crie uma nova página e insira um título - por exemplo, **Segmentos AC** - e selecione o **Segmento (Adobe Campaign)** modelo .
1. Selecione a página criada na visualização de árvore no lado esquerdo.
1. Crie um segmento, por exemplo, direcionando usuários do sexo masculino, criando uma nova página no segmento criado com o nome Masculino, e selecione o **Segmento (Adobe Campaign)** modelo .
1. Abra a página de segmento criada e arraste e solte uma **ID do segmento** do sidekick para a página.
1. Clique duas vezes na característica, insira a ID que representa, nesse caso, o segmento Masculino definido no Adobe Campaign - por exemplo, **MASCULINO** - e clique em **OK**. A seguinte mensagem deve aparecer: `targetData.segmentCode == "MALE"`
1. Repita as etapas para outro segmento, por exemplo, um segmento direcionado a usuários do sexo feminino.

### Criação de uma marca {#creating-a-brand}

Para criar uma marca:

1. Em **Sites**, navegue até o **Campanhas** pasta (por exemplo, em We.Retail).
1. Clique em **Criar página** e insira um título para a página, por exemplo, Marca We.Retail, e selecione o **Marca** modelo .

### Criar uma campanha {#creating-a-campaign}

Para criar uma campanha:

1. Abra o **Marca** página que você acabou de criar.
1. Clique em **Criar página** e insira um título para sua página, por exemplo, Campanha We.Retail, e selecione o **Campanha** modelo e clique em **Criar**.

### Criar experiências {#creating-experiences}

Para criar experiências para segmentos:

1. Abra o **Campanha** página que você acabou de criar.
1. Crie experiências para seus segmentos clicando em **Criar página** e inserir um título para sua página, por exemplo, Masculino, enquanto você cria uma experiência para o segmento Masculino, e selecionar o **Experiência** modelo .
1. Abra a página Experiência criada.
1. Clique em **Editar**, depois clique em Segmentos abaixo **Adicionar item**.
1. Insira o caminho para o segmento Masculino, por exemplo `/etc/segmentation/ac-segments/male` e clique em **OK**. A seguinte mensagem deve aparecer: *A experiência é direcionada para: Masculino*
1. Repita as etapas anteriores para criar uma experiência para todos os segmentos, por exemplo, o público-alvo feminino.

## Criação de um informativo com conteúdo direcionado {#creating-a-newsletter-with-targeted-content}

Após criar segmentos, uma marca, uma campanha e uma experiência, você pode criar um boletim informativo com conteúdo direcionado. Depois de criar a experiência, você vincula experiências aos seus segmentos.

Você pode criar o boletim informativo com conteúdo direcionado na interface do usuário habilitada para toque e clássica. Este documento descreve o procedimento para a interface habilitada para toque.

Para criar um informativo com conteúdo direcionado:

1. Crie um boletim informativo com conteúdo direcionado: Abaixo de Campanhas de email no Geometrixx Outdoors, clique ou toque **Criar** > **Página** e selecione um dos modelos do Adobe Campaign Mail.

   >[!NOTE]
   >
   >[Amostras de email estão disponíveis somente no Geometrixx](/help/sites-developing/we-retail.md#weretail). Baixe o conteúdo de amostra do Geometrixx do Compartilhamento de pacotes.

1. No boletim informativo, adicione um componente Texto e personalização .
1. Adicione texto ao componente Texto e personalização, como &quot;Este é o padrão&quot;.
1. Clique na seta ao lado de **Editar** e selecione **Direcionamento**.
1. Selecione sua marca no menu suspenso Marca e selecione sua Campanha. (Essa é a marca e a campanha que você criou anteriormente).
1. Clique em **Iniciar o direcionamento**. Você vê seus segmentos serem exibidos na área Públicos-alvo . A experiência padrão é usada se nenhum dos segmentos definidos corresponder.

   >[!NOTE]
   >
   >Por padrão, as amostras de email incluídas no AEM usam o Adobe Campaign como mecanismo de direcionamento. Para informativos personalizados, talvez seja necessário selecionar o Adobe Campaign como mecanismo de direcionamento. Ao direcionar, toque ou clique em + na barra de ferramentas, insira um título para a nova atividade e selecione **Adobe Campaign** como o mecanismo de direcionamento.

1. Clique em **Padrão** e, em seguida, o componente Texto e personalização adicionado, e você verá a Tela com uma seta nela. Clique no ícone para direcionar esse componente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Navegue até outro segmento (Masculino) e clique em **Adicionar oferta** e clique no ícone de adição +. Em seguida, edite a oferta.
1. Navegue até outro segmento (Feminino) e clique em **Adicionar oferta** e o ícone de adição +. Em seguida, edite esta oferta.
1. Clique em **Próximo** para ver Mapeamento, clique em **Próximo** para ver Configurações, que não se aplica ao Adobe Campaign, e clique em **Salvar**.

   AEM gera automaticamente o código de direcionamento correto para o Adobe Campaign quando o conteúdo é usado em um delivery dentro do Adobe Campaign

1. No Adobe Campaign, crie seu delivery - selecione **Delivery por email com conteúdo AEM** e selecione a conta de AEM local, conforme apropriado, e confirme suas alterações.

   Na exibição HTML, as diferentes experiências dos componentes direcionados são incluídas no código de direcionamento do Adobe Campaign.

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >Se você também configurar os segmentos no Adobe Campaign, clique em **Visualizar** mostrará as experiências para cada segmento.
