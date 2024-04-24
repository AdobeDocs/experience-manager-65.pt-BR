---
title: Fundamentos do Editor de Rich Text
description: Saiba mais sobre os fundamentos e recursos de um Editor de Rich Text que permite inserir texto com marcação.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# Fundamentos do Editor de Rich Text {#rich-text-editor-essentials}

## Visão geral {#overview}

Um Editor de Rich Text (RTE) permite inserir texto com marcação.

Para componentes das Comunidades, embora semelhantes ao [editor de rich text no ambiente do autor](../../help/sites-authoring/rich-text-editor.md), afeta o texto inserido no ambiente de publicação.

![rich-text-editor](assets/rich-text-editor.png)

## Ativação do editor de rich text {#enabling-rich-text-editor}

Os componentes das comunidades que permitem conteúdo gerado pelo usuário (UGC) podem ser habilitados para permitir RTE. Se o componente foi adicionado a uma página ou incluído em um [função](functions.md), o RTE pode ou não estar ativado por padrão.

Se não estiver ativado, basta inserir [modo de edição do autor](sites-console.md#authoring-site-content), selecione o componente para edição e selecione o `Rich Text Editor` caixa de seleção

O RTE está disponível para os seguintes componentes do Communities:

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Comentários](comments.md)
* [Filelibrary](file-library.md)
* [Fórum](forum.md)
* [Mensagens](configure-messaging.md)
* [QnA](working-with-qna.md)
* [Revisões](reviews.md)

## Personalização {#customization}

A personalização do editor de rich text é possível, pois a implementação é baseada em [CKEditor](https://ckeditor.com/).

A configuração atual dos componentes do Communities está em `cq.social.  scf   clientlib`, no repositório em

`/libs/clientlibs/social/commons/scf/ckrte.js`

Não é recomendado modificar o clientlib cq.social.scf, pois atualizações futuras podem substituir qualquer edição.

### Exemplo de personalização: links integrados {#example-customization-inline-links}

Por questões de segurança, as opções de hiperlink não estão incluídas no conjunto de ícones de rich text apresentado aos membros por padrão. A capacidade de danificar é extensa quando os hrefs são permitidos no UGC.

Para adicionar as opções de hiperlink à barra de ferramentas:

* Adicione uma barra de ferramentas chamada &quot; `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* Selecionar **[!UICONTROL Salvar tudo]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```
