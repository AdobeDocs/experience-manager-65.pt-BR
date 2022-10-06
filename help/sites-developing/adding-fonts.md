---
title: Adicionar fontes para renderização de gráficos
seo-title: Adding Fonts for Graphic-Rendering
description: AEM permite gerar gráficos incorporando texto obtido dinamicamente do seu conteúdo
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# Adicionar fontes para renderização de gráficos{#adding-fonts-for-graphic-rendering}

AEM permite gerar gráficos incorporando texto obtido dinamicamente do seu conteúdo.

Para fazer isso, você também pode carregar e usar suas próprias fontes.

Atualmente, todas as implementações da plataforma Java são compatíveis [TrueType](https://en.wikipedia.org/wiki/Truetype) fontes.

1. Abra o CRXDE Lite e navegue até a pasta do aplicativo do projeto:

   `/apps/<your-project>/`

1. Em `/apps/<your-project>/` crie um novo nó:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salve todas as alterações.

1. Copie os arquivos de fonte nesta pasta; por exemplo, usando o WebDAV.

   >[!NOTE]
   >
   >Os arquivos de fonte no repositório devem ter o sufixo `*.ttf` ou `*.TTF`.

1. Atualize o [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Adicione o caminho à sua pasta de fontes; ou seja, `/apps/<your-project>/fonts`.

1. Volte para CRXDE Lite. Agora você deve ver um `.fontlist` na pasta que contém o nome das fontes importadas.

   Essas fontes agora estão prontas para serem usadas na API do Java.

Para obter detalhes completos sobre como usar as fontes com a API do Java, consulte o [documentação da classe Font da API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
