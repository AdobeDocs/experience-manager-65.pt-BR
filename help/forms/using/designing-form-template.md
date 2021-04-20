---
title: Criação de modelos de formulário para formulários HTML5
seo-title: Criação de modelos de formulário para formulários HTML5
description: A AEM Forms oferece renderizar o modelo de formulário XFA para o formato HTML5. Os designers de formulários podem criar modelos de formulário usando o Designer e usar o recurso de representação HTML5.
seo-description: A AEM Forms oferece renderizar o modelo de formulário XFA para o formato HTML5. Os designers de formulários podem criar modelos de formulário usando o Designer e usar o recurso de representação HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Criação de modelos de formulário para formulários HTML5{#designing-form-templates-for-html-forms}

O componente de formulários HTML5 no AEM oferece a renderização do modelo de formulário XFA para o formato HTML5. Os designers de formulários podem criar modelos de formulário usando o [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e usar o recurso de representação HTML5. Esses modelos de formulário, juntamente com seus ativos, podem residir em AEM repositório, sistema de arquivos ou expostos via http. No entanto, se você planeja gerenciar seus formulários usando o Forms Manager, os modelos e ativos devem residir no repositório AEM.

Embora os formulários HTML5 correspondam ao comportamento dos PDF forms, há alguns recursos em ambos os formatos que não se aplicam ao outro formato. Por exemplo, a forma como os códigos de barras são aplicados em um formulário PDF no Adobe Reader varia de um formulário para dispositivos móveis ou como um formulário é assinado digitalmente também varia de acordo com os formatos. Para obter mais informações sobre essas variações, consulte [Diferenciação de recursos entre formulários HTML5 e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para obter recursos comuns do XFA, consulte as práticas recomendadas e diretrizes a seguir para projetar um formulário que funcione em ambos os formatos.

## Práticas recomendadas {#best-practices}

A maioria das etapas para criar um modelo de formulário, como vínculos de esquema ou escrever lógica de formulário, são as mesmas. No entanto, devido a diferenças inerentes entre renderização e mecanismo de script de um cliente espesso como o Adobe Reader e formulários baseados em navegador, há algumas recomendações descritas no artigo [práticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Essas práticas recomendadas ajudam você a projetar modelos de formulário para funcionar conforme esperado em ambos os formatos.

### Recursos no AEM Forms Designer para Forms HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Visualizar HTML {#preview-html}

A guia Visualizar HTML é adicionada no modo Design para que os designers de formulários visualizem formulários no formato HTML5 durante o processo de design. Para obter mais informações sobre como habilitar e configurar esse recurso no AEM Forms Designer, consulte [Visualizar HTML](../../forms/using/preview-xdp-forms-html.md).

#### Assinatura {#scribble-signature}

O alvo principal para formulários HTML5 é dispositivos de toque. Portanto, um novo controle de assinatura de rabisco é adicionado no AEM Forms Designer. Você pode clicar ou arrastar e soltar o controle de assinatura de rabisco no modelo de formulário e configurá-lo. Ele é renderizado como um campo de rabisco na representação HTML5 e pode ser usado para rabiscar a assinatura em dispositivos de toque. Em máquinas de desktop, ele pode ser usado como um campo de rabisco usando o controle do mouse. Para obter mais informações sobre como usar esse recurso, consulte [Campo de rabisco XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato Rich Text {#rich-text-format}

É possível converter um campo de texto em um campo de rich text. Ele adiciona uma lista de opções de formatação ao campo de texto. Para converter, abra o Forms Designer, toque no campo de texto em **[!UICONTROL Visualização de projeto]**. Na guia **[!UICONTROL Campo]**, selecione **[!UICONTROL Rich Text]** na lista suspensa **[!UICONTROL Formato de campo]**. Agora, quando o formulário XFA é renderizado como um Formulário HTML5, o campo é renderizado como um campo Rich Text. Toque em ![Maximizar](assets/maximize_icon.svg) para exibir opções adicionais de formatação.
