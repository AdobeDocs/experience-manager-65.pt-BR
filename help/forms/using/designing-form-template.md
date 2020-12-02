---
title: Criar modelos de formulário para formulários HTML5
seo-title: Criar modelos de formulário para formulários HTML5
description: O AEM Forms oferta renderiza o modelo de formulário XFA para o formato HTML5. Os designers de formulário podem criar modelos de formulário usando o Designer e usar o recurso de execução HTML5.
seo-description: O AEM Forms oferta renderiza o modelo de formulário XFA para o formato HTML5. Os designers de formulário podem criar modelos de formulário usando o Designer e usar o recurso de execução HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Criar modelos de formulário para formulários HTML5{#designing-form-templates-for-html-forms}

O componente de formulários HTML5 no AEM oferta que renderiza o modelo de formulário XFA para o formato HTML5. Os designers de formulário podem criar modelos de formulário usando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e usar o recurso de execução HTML5. Esses modelos de formulário, juntamente com seus ativos, podem residir AEM repositório, sistema de arquivos ou expostos via http. No entanto, se você planeja gerenciar seus formulários usando o Forms Manager, os modelos e ativos devem residir no repositório AEM.

Embora os formulários HTML5 correspondam em grande medida ao comportamento dos PDF forms, há alguns recursos em ambos os formatos que não são aplicáveis ao outro formato. Por exemplo, o modo como os códigos de barras são aplicados em um formulário PDF no Adobe Reader varia de um formulário móvel ou como um formulário é assinado digitalmente também varia de acordo com os formatos. Para obter mais informações sobre essas variações, consulte [Diferenciação de recursos entre formulários HTML5 e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para obter recursos comuns do XFA, consulte as seguintes práticas recomendadas e diretrizes para projetar um formulário que funcione em ambos os formatos.

## Práticas recomendadas {#best-practices}

A maioria das etapas para criar um modelo de formulário, como vínculos de schema ou lógica de formulário de gravação, são as mesmas. No entanto, devido às diferenças inerentes entre a renderização e o mecanismo de scripts de um cliente espesso como o Adobe Reader e formulários baseados em navegador, há algumas recomendações descritas no artigo [práticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Essas práticas recomendadas ajudam você a projetar modelos de formulário para funcionarem como esperado em ambos os formatos.

### Recursos no AEM Forms Designer para HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML de pré-visualização {#preview-html}

A guia HTML de Pré-visualização é adicionada no modo Design para designers de formulário para pré-visualização de formulários no formato HTML5 durante o processo de design. Para obter mais informações sobre como habilitar e configurar esse recurso no AEM Forms Designer, consulte [HTML de Pré-visualização](../../forms/using/preview-xdp-forms-html.md).

#### Assinatura {#scribble-signature}

O público alvo principal para formulários HTML5 é dispositivos de toque. Portanto, um novo controle de assinatura de script é adicionado no AEM Forms Designer. Você pode clicar ou arrastar e soltar o controle de assinatura em seu modelo de formulário e configurá-lo. Ele é renderizado como um campo de script na execução HTML5 e pode ser usado para rabiscar a assinatura em dispositivos de toque. Em computadores desktop, ele pode ser usado como um campo de script usando o controle do mouse. Para obter mais informações sobre como usar esse recurso, consulte [Campo de script XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato Rich Text {#rich-text-format}

É possível converter um campo de texto em um campo de texto formatado. Adiciona uma lista de opções de formatação ao campo de texto. Para converter, abra o Forms Designer, toque no campo de texto em **[!UICONTROL Visualização de design]**. Na guia **[!UICONTROL Field]**, selecione **[!UICONTROL Rich Text]** na lista suspensa **[!UICONTROL Field Format]**. Agora, quando o formulário XFA é renderizado como um Formulário HTML5, o campo é renderizado como um campo Rich Text. Toque em ![Maximizar](assets/maximize_icon.svg) para visualização de opções de formatação adicionais.
