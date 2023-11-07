---
title: Adicionar fontes para renderização gráfica
seo-title: Adding Fonts for Graphic-Rendering
description: O AEM permite gerar gráficos incorporando texto dinamicamente retirado do seu conteúdo
seo-description: AEM lets you generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Adicionar fontes para renderização gráfica{#adding-fonts-for-graphic-rendering}

O AEM permite gerar gráficos incorporando texto dinamicamente retirado do seu conteúdo.

Para fazer isso, você também pode carregar e usar suas próprias fontes.

Atualmente, todas as implementações do suporte à plataforma Java [TrueType](https://en.wikipedia.org/wiki/Truetype) fontes.

1. Abra o CRXDE Lite e navegue até a pasta do aplicativo do projeto:

   `/apps/<your-project>/`

1. Em `/apps/<your-project>/` criar um nó:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salve todas as alterações.

1. Copie os arquivos de fonte nesta pasta; por exemplo, usando WebDAV.

   >[!NOTE]
   >
   >Os arquivos de fonte no repositório devem ter o sufixo `*.ttf` ou `*.TTF`.

1. Atualize o [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) de [Auxiliar de fontes Day Commons GFX](/help/sites-deploying/osgi-configuration-settings.md). Adicione o caminho para a pasta de fontes; por exemplo, `/apps/<your-project>/fonts`.

1. Retorne ao CRXDE Lite. Agora você deve ver uma `.fontlist` nó na pasta que contém o nome das fontes importadas.

   Essas fontes agora estão prontas para serem usadas na API do Java.

Para obter detalhes completos sobre como usar as fontes com a API Java, consulte a [Documentação da classe Fonte da API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
