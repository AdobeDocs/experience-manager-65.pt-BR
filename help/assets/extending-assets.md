---
title: Personalizar e estender [!DNL Assets]
description: Saiba como personalizar e estender o Asset Share e o Editor de ativos, que apresenta aos usuários uma interface especificamente personalizada e um conjunto de funcionalidades.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Personalizar e estender [!DNL Assets] {#customizing-and-extending-assets}

O Editor de ativos é o principal ponto de acesso que os usuários de um site do Adobe Enterprise Manager usarão para localizar, visualização e manipular os ativos digitais no repositório.

Como um [!DNL Experience Manager] desenvolvedor, você pode personalizar e estender o Editor de ativos de várias maneiras, apresentando aos usuários uma interface especificamente personalizada e um conjunto de funcionalidades.

Os seguintes aspectos da funcionalidade podem ser personalizados ou aprimorados:

* [Estender editor de ativos](asseteditorx.md)
* [Estender pesquisa de ativos](searchx.md)
* [Processar ativos usando manipuladores de mídia e Workflows](media-handlers.md)
* [Integrar ativos ao fluxo de atividade](extending-activity-stream.md)
* [Desenvolvimento proxy de ativos](proxy.md)
* [Práticas recomendadas para configurar o ImageMagick](best-practices-for-imagemagick.md)

## Personalizar a aparência {#customizing-the-look-and-feel}

Os seguintes aspectos da aparência do Editor de ativos são personalizáveis:

* Logotipo: Você pode adicionar o logotipo de sua própria organização à interface.
* Cores e fontes: É possível alterar as cores e as fontes usadas na interface.
* Código HTML: Para uma personalização mais completa, é possível alterar o código HTML subjacente que define as interfaces.

## Personalizar representações {#customizing-renditions}

Na [!DNL Experience Manager Assets] terminologia, uma representação é a forma na qual um ativo é apresentado. Em geral, um ativo específico pode ter várias representações. Por exemplo, imagens em cores completas podem ter uma representação em seu tamanho original, outra em tamanho reduzido e outra em escala decrescente e outra em escala de cinza.

As representações nas quais um ativo específico está disponível podem ser personalizadas e novas representações podem ser criadas.
