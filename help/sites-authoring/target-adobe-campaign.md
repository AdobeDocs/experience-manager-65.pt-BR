---
title: Direcione sua Adobe Campaign
description: Você pode criar experiências direcionadas para o Adobe Campaign após configurar a segmentação.
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Direcionamento da sua Adobe Campaign{#targeting-your-adobe-campaign}

Para direcionar seu informativo do Adobe Campaign, primeiro você precisa configurar a segmentação, que só está disponível na interface clássica (para contexto de cliente). Depois disso, você poderá criar experiências direcionadas para o Adobe Campaign. Ambos estão descritos nesta seção.

## Configuração da segmentação no AEM {#setting-up-segmentation-in-aem}

Para configurar a segmentação, é necessário usar a interface clássica para configurar os segmentos. As etapas restantes podem ser executadas na interface de usuário padrão.

Configurar a segmentação inclui a criação de segmentos, uma marca, campanha e experiências.

>[!NOTE]
>
>A ID do segmento precisa ser mapeada para aquela no lado do Adobe Campaign.

### Criação de segmentos {#creating-segments}

Para criar segmentos:

1. Abra o [console de segmentação](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Crie uma nova página e insira um título - por exemplo, **Segmentos AC**- e selecione o **Segmento (Adobe Campaign)** modelo .
1. Selecione a página criada na visualização de árvore no lado esquerdo.
1. Crie um segmento, por exemplo, direcionando usuários do sexo masculino, criando uma nova página no segmento criado com o nome Masculino, e selecione o **Segmento (Adobe Campaign)** modelo .
1. Abra a página de segmento criada e arraste e solte uma **ID do segmento** do sidekick para a página.
1. Clique duas vezes na característica, insira a ID que representa, nesse caso, o segmento Masculino definido no Adobe Campaign - por exemplo, **MASCULINO** - e clique em **OK**. A seguinte mensagem deve aparecer: *`targetData.segmentCode == "MALE"`*
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
1. Insira o caminho para o segmento Masculino, por exemplo **/etc/segmentation/ac-segments/male** e clique em **OK**. A seguinte mensagem deve aparecer: *A experiência é direcionada para: Masculino*
1. Repita as etapas anteriores para criar uma experiência para todos os segmentos, por exemplo, o público-alvo feminino.

## Criação de um informativo com conteúdo direcionado {#creating-a-newsletter-with-targeted-content}

Após criar segmentos, uma marca, uma campanha e uma experiência, você pode criar um boletim informativo com conteúdo direcionado. Depois de criar a experiência, você vincula experiências aos seus segmentos.

>[!NOTE]
>
>[Amostras de email estão disponíveis somente no Geometrixx](/help/sites-developing/we-retail.md). Baixe o conteúdo de amostra do Geometrixx do Compartilhamento de pacotes.

Para criar um informativo com conteúdo direcionado:

1. Crie um boletim informativo com conteúdo direcionado: Abaixo de Campanhas de email no Geometrixx Outdoors, clique ou toque **Criar** > **Página** e selecione um dos modelos do Adobe Campaign Mail.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. No boletim informativo, adicione um componente Texto e personalização .
1. Adicione texto ao componente Texto e personalização, como &quot;Este é o padrão&quot;.
1. Clique na seta ao lado de **Editar** e selecione **Direcionamento**.
1. Selecione sua marca no menu suspenso Marca e selecione sua Campanha. (Essa é a marca e a campanha que você criou anteriormente).
1. Clique em **Iniciar o direcionamento**. Você vê seus segmentos serem exibidos na área Públicos-alvo . A experiência padrão é usada se nenhum dos segmentos definidos corresponder.

   >[!NOTE]
   >
   >Por padrão, as amostras de email incluídas no AEM usam o Adobe Campaign como mecanismo de direcionamento. Para informativos personalizados, talvez seja necessário selecionar o Adobe Campaign como mecanismo de direcionamento. Ao direcionar, toque ou clique em + na barra de ferramentas, insira um título para a nova atividade e selecione **Adobe Campaign** como o mecanismo de direcionamento.

1. Clique em **Padrão** e, em seguida, o componente Texto e personalização adicionado, e você verá a Tela com uma seta nela. Clique no ícone para direcionar esse componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Navegue até outro segmento (Masculino) e clique em **Adicionar oferta** e clique no ícone de adição +. Em seguida, edite a oferta.
1. Navegue até outro segmento (Feminino) e clique em **Adicionar oferta** e o ícone de adição +. Em seguida, edite esta oferta.
1. Clique em **Próximo** para ver Mapeamento, clique em **Próximo** para ver Configurações, que não se aplica ao Adobe Campaign, e clique em **Salvar**.

   AEM gera automaticamente o código de direcionamento correto para o Adobe Campaign quando o conteúdo é usado em um delivery dentro do Adobe Campaign

1. No Adobe Campaign, crie seu delivery - selecione **Delivery por email com conteúdo AEM** e selecione a conta de AEM local, conforme apropriado, e confirme suas alterações.

   Na exibição HTML, as diferentes experiências dos componentes direcionados são incluídas no código de direcionamento do Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Se você também configurar os segmentos no Adobe Campaign, clique em **Visualizar** mostrará as experiências para cada segmento.
