---
title: Direcionar seu Adobe Campaign
description: Você pode criar experiências direcionadas para o Adobe Campaign após configurar a segmentação.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Direcionamento do seu Adobe Campaign{#targeting-your-adobe-campaign}

Para direcionar seu informativo no Adobe Campaign, primeiro é necessário configurar a segmentação, que só está disponível na interface clássica (para contexto de cliente). Depois disso, será possível criar experiências direcionadas para o Adobe Campaign. Ambos são descritos nesta seção.

## Configuração da segmentação no AEM {#setting-up-segmentation-in-aem}

Para configurar a segmentação, é necessário usar a interface clássica para configurar os segmentos. As etapas restantes podem ser executadas na interface padrão do usuário.

A configuração da segmentação inclui a criação de segmentos, uma marca, uma campanha e experiências.

>[!NOTE]
>
>A ID de segmento precisa ser mapeada para a do lado do Adobe Campaign.

### Criação de segmentos {#creating-segments}

Para criar segmentos:

1. Abra o [console de segmentação](http://localhost:4502/miscadmin#/etc/segmentation) em **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Crie uma página e insira um título - por exemplo, **Segmentos AC**- e selecione o modelo **Segmento (Adobe Campaign)**.
1. Selecione a página criada na visualização de árvore no lado esquerdo.
1. Crie um segmento, por exemplo, direcionando usuários do sexo masculino, criando uma página no segmento criado chamado Masculino e selecione o modelo **Segmento (Adobe Campaign)**.
1. Abra a página de segmento criada e arraste e solte uma **ID de segmento** do sidekick na página.
1. Clique duas vezes na característica, insira a ID que representa, neste caso, o segmento macho definido no Adobe Campaign - por exemplo, **MASCULINO** - e clique em **OK**. A seguinte mensagem deve ser exibida: *`targetData.segmentCode == "MALE"`*
1. Repita as etapas para outro segmento, por exemplo, um segmento direcionado a usuários do sexo feminino.

### Criar uma marca {#creating-a-brand}

Para criar uma marca:

1. Em **Sites**, navegue até a pasta **Campanhas** (por exemplo, em We.Retail).
1. Clique em **Criar Página** e insira um título para a página, por exemplo, Marca We.Retail, e selecione o modelo **Marca**.

### Criar uma campanha {#creating-a-campaign}

Para criar uma campanha:

1. Abra a página **Marca** que você criou.
1. Clique em **Criar página** e insira um título para sua página, por exemplo, Campanha We.Retail, selecione o modelo **Campanha** e clique em **Criar**.

### Criação de experiências {#creating-experiences}

Para criar experiências para segmentos:

1. Abra a página **Campanha** que você criou.
1. Crie experiências para seus segmentos clicando em **Criar página** e inserindo um título para sua página, por exemplo, Masculino, já que você está criando uma experiência para o segmento Masculino, e selecione o modelo **Experiência**.
1. Abra a página Experiência criada.
1. Clique em **Editar** e abaixo de Segmentos clique em **Adicionar item**.
1. Insira o caminho para o segmento macho, por exemplo, **/etc/segmentation/ac-segments/male** e clique em **OK**. A seguinte mensagem deve ser exibida: *A experiência está direcionada para: Masculino*
1. Repita as etapas anteriores para criar uma experiência para todos os segmentos, por exemplo, o público-alvo feminino.
