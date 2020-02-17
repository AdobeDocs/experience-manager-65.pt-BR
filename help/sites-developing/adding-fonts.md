---
title: Adicionar fontes para renderização de gráficos
seo-title: Adicionar fontes para renderização de gráficos
description: O AEM permite que você gere gráficos que incorporam texto retirado dinamicamente do seu conteúdo
seo-description: O AEM permite que você gere gráficos que incorporam texto retirado dinamicamente do seu conteúdo
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adicionar fontes para renderização de gráficos{#adding-fonts-for-graphic-rendering}

O AEM permite que você gere gráficos que incorporam texto obtido dinamicamente do seu conteúdo.

Para fazer isso, você também pode carregar e usar suas próprias fontes.

Atualmente, todas as implementações da Plataforma Java oferecem suporte a fontes [TrueType](https://en.wikipedia.org/wiki/Truetype) .

1. Abra o CRXDE Lite e navegue até a pasta do aplicativo do projeto:

   `/apps/<your-project>/`

1. Em `/apps/<your-project>/` criar um novo nó:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`
   Salve todas as alterações.

1. Copie os arquivos de fonte nesta pasta; por exemplo, usando WebDAV.

   >[!NOTE]
   >
   >Os arquivos de fonte no repositório devem ter o sufixo `*.ttf` ou `*.TTF`.

1. Atualize a configuração [do](/help/sites-deploying/configuring-osgi.md) OSGi do [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Adicione o caminho à sua pasta de fontes; ou seja, `/apps/<your-project>/fonts`.

1. Retorne ao CRXDE Lite. Agora você deve ver um `.fontlist` nó na pasta que contém o nome das fontes importadas.

   Essas fontes estão prontas para serem usadas na API Java.

Para obter detalhes completos sobre como usar as fontes com a API Java, consulte a [documentação da classe Font da API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)Java.

