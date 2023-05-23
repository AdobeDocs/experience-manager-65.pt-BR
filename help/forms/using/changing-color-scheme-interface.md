---
title: Alteração do esquema de cores da interface
seo-title: Changing the color scheme of the interface
description: Como modificar o esquema de cores das partes da interface do usuário do AEM Forms Workspace de forma seletiva.
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# Alteração do esquema de cores da interface {#changing-the-color-scheme-of-the-interface}

Você pode modificar o esquema de cores das partes da interface do usuário do AEM Forms Workspace para atender aos seus requisitos. Veja a seguir alguns exemplos de personalizações representativas do esquema de cores. Além das etapas discutidas neste artigo, consulte [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barra de navegação superior {#top-navigation-bar}

### Uso da imagem de plano de fundo {#using-background-image}

Para atualizar a barra de navegação na parte superior do Workspace do AEM Forms.

1. Criar uma imagem de plano de fundo para atualizar a cor. Nomeie o arquivo como newBackground.jpg.
1. Faça upload do arquivo de imagem de fundo na pasta /apps/ws/images usando um cliente WebDAV.

   >[!NOTE]
   >
   >Para obter mais informações sobre o acesso WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR).

1. Referencie a nova imagem de fundo em /apps/ws/css/newStyle.css adicionando o estilo a seguir.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Utilização da propriedade de cor no CSS {#using-color-property-in-css}

1. Adicione o seguinte estilo em newStyle.css em /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Componente da categoria {#category-component}

Componente Categoria exibe as várias categorias de suas tarefas no painel esquerdo. Para alterar a cor, defina a cor do plano de fundo em `.category` elemento do arquivo CSS.

## Componente da tarefa {#task-component}

As tarefas são exibidas no painel do meio chamado de Componente Lista de tarefas. Para alterar sua cor, modifique o estilo associado ao seletor .task na folha de estilos.
