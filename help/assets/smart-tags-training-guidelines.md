---
title: Diretrizes de treinamento do Serviço de conteúdo inteligente
description: Treinar o serviço de IA da Adobe Sensei para aplicar tags inteligentes aos ativos
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---


# Diretrizes de treinamento do Serviço de conteúdo inteligente {#smart-content-service-training-guidelines}

Para que as imagens de sua marca possam ser marcadas com eficácia, o Serviço de conteúdo inteligente exige que as imagens de treinamento estejam em conformidade com determinadas diretrizes.

## Orientações para a formação {#guidelines-for-training}

Para obter melhores resultados, as imagens em seu conjunto de treinamento devem estar em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 30 imagens por tag. Mínimo de 500 pixels no lado maior.

**Coerência**: As imagens de uma tag devem ser visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Deve haver uma variedade suficiente de imagens no treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que a Experience Manager aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para o *modelo de tag-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/completeness.png)

## Limitações           {#limitations}

Tags inteligentes aprimoradas são baseadas em modelos de aprendizado de imagens e suas tags. Esses modelos nem sempre são perfeitos para identificar tags. A versão atual do Serviço de conteúdo inteligente tem as seguintes limitações:

* Incapacidade de reconhecer diferenças sutis nas imagens. Por exemplo, camisas finas versus camisetas comuns.
* Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em camisetas.
* A marcação é suportada nas localidades nas quais [!DNL Experience Manager] há suporte. Para obter uma lista de idiomas, consulte Notas [de versão do](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)Smart Content Services.

Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas para treinamento. Para obter melhores resultados, o Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço de cada tag.
