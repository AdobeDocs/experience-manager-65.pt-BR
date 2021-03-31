---
title: Personalizar e estender [!DNL Assets]
description: Saiba como personalizar e estender o Compartilhamento de ativos e o Editor de ativos, que apresenta aos usuários uma interface e um conjunto de funcionalidades especificamente personalizados.
contentOwner: AG
role: Desenvolvedor
feature: Ferramentas do desenvolvedor
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# Personalizar e estender [!DNL Assets] {#customizing-and-extending-assets}

O Editor de ativos é o principal ponto de acesso que os usuários de um site do Adobe Enterprise Manager usarão para localizar, exibir e manipular os ativos digitais em seu repositório.

Como desenvolvedor [!DNL Experience Manager], você pode personalizar e estender o Editor de ativos de várias maneiras, apresentando aos usuários uma interface especificamente personalizada e um conjunto de funcionalidades.

Os seguintes aspectos da funcionalidade podem ser personalizados ou aprimorados:

* [Estender editor de ativos](asseteditorx.md)
* [Estender pesquisa de ativos](searchx.md)
* [Processar ativos usando manipuladores de mídia e fluxos de trabalho](media-handlers.md)
* [Integrar ativos ao fluxo de atividades](extending-activity-stream.md)
* [Desenvolvimento de proxy de ativos](proxy.md)
* [Práticas recomendadas para configurar o ImageMagick](best-practices-for-imagemagick.md)

## Personalizar a aparência {#customizing-the-look-and-feel}

Os seguintes aspectos da aparência do Editor de ativos são personalizáveis:

* Logotipo: Você pode adicionar o logotipo de sua própria organização à interface.
* Cores e fontes: Você pode alterar as cores e as fontes usadas na interface.
* Código HTML: Para uma personalização mais completa, você pode alterar o código HTML subjacente que define as interfaces.

## Personalizar representações {#customizing-renditions}

Na terminologia [!DNL Experience Manager Assets], uma representação é a forma na qual um ativo é apresentado. Em geral, um ativo específico pode ter várias representações. Por exemplo, imagens de cores completas podem ter uma representação em seu tamanho original, outra em um tamanho reduzido e outra que é dimensionada para baixo e convertida em escala de cinza.

As representações em que um ativo específico está disponível podem ser personalizadas e novas representações podem ser criadas.
