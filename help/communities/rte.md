---
title: Princípios básicos do editor de rich text
seo-title: Rich Text Editor Essentials
description: Visão geral de recursos do Editor de Rich Text
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# Princípios básicos do editor de rich text {#rich-text-editor-essentials}

## Visão geral {#overview}

Um Editor de Rich Text (RTE) fornece a capacidade de inserir texto com marcação.

Para componentes das Comunidades, enquanto são semelhantes ao [editor de rich text no ambiente do autor](../../help/sites-authoring/rich-text-editor.md), afeta o texto inserido no ambiente de publicação.

![editor de rich text](assets/rich-text-editor.png)

## Ativação do editor de rich text {#enabling-rich-text-editor}

Os componentes de Comunidades que permitem conteúdo gerado pelo usuário (UGC) podem ser habilitados para permitir o RTE. Dependendo de o componente ter sido adicionado a uma página ou incluído em uma [função](functions.md), o RTE pode ou não ser ativado por padrão.

Se não estiver ativado, basta inserir [modo de edição do autor](sites-console.md#authoring-site-content), selecione o componente para edição e selecione o `Rich Text Editor` caixa de seleção.

O RTE está disponível para os seguintes componentes do Communities:

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Comentários](comments.md)
* [Filelibrary](file-library.md)
* [Fórum](forum.md)
* [Mensagens](configure-messaging.md)
* [Perguntas e respostas](working-with-qna.md)
* [Revisões](reviews.md)

## Personalização {#customization}

A personalização do editor de rich text é possível, pois a implementação é baseada em [Editor CKE](https://www.ckeditor.com/).

A configuração atual dos componentes das Comunidades está no `cq.social.  scf   clientlib`, localizado no repositório em

`/libs/clientlibs/social/commons/scf/ckrte.js`

A modificação da clientlib cq.social.scf não é recomendada, pois as atualizações futuras podem substituir qualquer edição.

### Exemplo de personalização: Links em linha {#example-customization-inline-links}

Devido a questões de segurança, as opções de hiperlink não são incluídas no conjunto de ícones de rich text apresentados aos membros por padrão. A habilidade para o mal é extensa quando os hrefs são permitidos no UGC.

Para adicionar as opções de hiperlink à barra de ferramentas:

* Adicionar uma barra de ferramentas chamada &quot; `links`&quot;
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
