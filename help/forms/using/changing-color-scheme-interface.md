---
title: Alteração do esquema de cores da interface
description: Como modificar o esquema de cores das partes da interface do usuário do AEM Forms Workspace de forma seletiva.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

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
   >Para obter mais informações, consulte [Acesso ao WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=pt-BR).

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

Componente Categoria exibe as várias categorias de suas tarefas no painel esquerdo. Para alterar a cor, defina a cor do plano de fundo no elemento `.category` do arquivo CSS.

## Componente da tarefa {#task-component}

As tarefas são exibidas no painel do meio chamado de Componente Lista de tarefas. Para alterar sua cor, modifique o estilo associado ao seletor .task na folha de estilos.
