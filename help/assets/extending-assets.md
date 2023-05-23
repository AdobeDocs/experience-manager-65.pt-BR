---
title: Personalizar e estender [!DNL Assets]
description: Saiba mais sobre como personalizar e estender o Compartilhamento de ativos e o Editor de ativos, que apresentam aos usuários uma interface e um conjunto de funcionalidades especificamente adaptados.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Personalizar e estender [!DNL Assets] {#customizing-and-extending-assets}

O Editor de Ativos é o principal ponto de acesso que os usuários de um website do Adobe Enterprise Manager usarão para localizar, exibir e manipular os ativos digitais no seu repositório.

Como um [!DNL Experience Manager] desenvolvedor, você pode personalizar e estender o Editor de ativos de várias maneiras, apresentando aos usuários uma interface e um conjunto de funcionalidades especificamente adaptados.

Os seguintes aspectos da funcionalidade podem ser personalizados ou aprimorados:

* [Estender editor de ativos](asseteditorx.md)
* [Estender pesquisa de ativos](searchx.md)
* [Processar ativos usando manipuladores de mídia e fluxos de trabalho](media-handlers.md)
* [Integrar ativos ao fluxo de atividade](extending-activity-stream.md)
* [Desenvolvimento de proxy de ativos](proxy.md)
* [Práticas recomendadas para configurar o ImageMagick](best-practices-for-imagemagick.md)

## Personalizar a aparência {#customizing-the-look-and-feel}

Os seguintes aspectos da aparência do Editor de ativos são personalizáveis:

* Logotipo: você pode adicionar o logotipo de sua própria organização à interface do.
* Cores e fontes: é possível alterar as cores e as fontes usadas na interface.
* Código HTML: para uma personalização mais completa, é possível alterar o código HTML subjacente que define as interfaces.

## Personalizar representações {#customizing-renditions}

Entrada [!DNL Experience Manager Assets] terminologia uma representação é o formulário no qual um ativo é apresentado. Em geral, um ativo específico pode ter várias representações. Por exemplo, uma imagem colorida pode ter uma representação em seu tamanho original, outra em um tamanho reduzido e outra que é dimensionada e convertida em tons de cinza.

As representações em que um ativo específico está disponível podem ser personalizadas e novas representações podem ser criadas.
