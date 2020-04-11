---
title: Alteração do esquema de cores da interface
seo-title: Alteração do esquema de cores da interface
description: Como modificar seletivamente o esquema de cores das partes da interface do usuário da área de trabalho do AEM Forms.
seo-description: Como modificar seletivamente o esquema de cores das partes da interface do usuário da área de trabalho do AEM Forms.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Alteração do esquema de cores da interface {#changing-the-color-scheme-of-the-interface}

Você pode modificar o esquema de cores das partes da interface do usuário da área de trabalho do AEM Forms para atender às suas necessidades. Veja a seguir alguns exemplos de personalizações representativas do esquema de cores. Além das etapas discutidas neste artigo, consulte Etapas [genéricas para personalização](/help/forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.

## Top navigation bar {#top-navigation-bar}

### Uso da imagem de plano de fundo {#using-background-image}

Para atualizar a barra de navegação na parte superior da área de trabalho do AEM Forms.

1. Crie uma imagem de plano de fundo para atualizar a cor. Nomeie o arquivo como newBackground.jpg.
1. Carregue o arquivo de imagem de plano de fundo na pasta /apps/ws/images usando um cliente WebDAV.

   >[!NOTE]
   >
   >Para obter mais informações sobre o acesso ao WebDAV, consulte [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Faça referência à nova imagem de plano de fundo em /apps/ws/css/newStyle.css adicionando o seguinte estilo.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Uso da propriedade color no CSS {#using-color-property-in-css}

1. Adicione o seguinte estilo em newStyle.css em /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## componente Categoria {#category-component}

O componente de Categoria exibe as várias categorias de suas tarefas no painel esquerdo. Para alterar sua cor, defina a cor do plano de fundo no `.category` elemento do arquivo CSS.

## componente Tarefa {#task-component}

As Tarefas são exibidas no painel do meio chamado Componente TaskList. Para alterar sua cor, modifique o estilo associado ao seletor .tarefa na folha de estilos.
