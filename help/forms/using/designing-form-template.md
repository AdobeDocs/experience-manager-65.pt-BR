---
title: Criação de modelos de formulário para formulários HTML5
description: O AEM Forms pode renderizar o modelo de formulário XFA para o formato HTML5. Os designers de formulário podem criar modelos de formulário usando o Designer e usar o recurso de representação do HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%
---
# Criação de modelos de formulário para formulários HTML5{#designing-form-templates-for-html-forms}

O componente de formulários do HTML5 no AEM pode renderizar o modelo de formulário XFA para o formato HTML5. Os designers de formulário podem criar modelos de formulário usando o [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e usar o recurso de representação do HTML5. Esses modelos de formulário, juntamente com seus ativos, podem residir no repositório do AEM, no sistema de arquivos ou expostos via http. No entanto, se você planeja gerenciar seus formulários usando o Forms Manager, os modelos e os ativos devem residir no repositório do AEM.

Embora os formulários HTML5 correspondam ao comportamento do PDF forms em grande parte, há alguns recursos em ambos os formatos que não se aplicam ao outro formato. Por exemplo, a forma como os códigos de barras são aplicados em um formulário do PDF no Adobe Reader varia de um formulário do Mobile ou como um formulário é assinado digitalmente também varia entre os formatos. Para obter mais informações sobre essas variações, consulte [Diferenciação de recursos entre formulários HTML5 e o PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Para obter recursos XFA comuns, consulte as seguintes práticas recomendadas e diretrizes para criar um formulário que funcione em ambos os formatos.

## Práticas recomendadas {#best-practices}

A maioria das etapas para criar um modelo de formulário, como associações de esquema ou escrever lógica de formulário, são as mesmas. No entanto, devido a diferenças inerentes entre a renderização e o mecanismo de script de um cliente thick como o Adobe Reader e os formulários baseados em navegador, há algumas recomendações descritas no artigo [práticas recomendadas](/help/forms/using/design-accessible-html5-forms.md). Essas práticas recomendadas ajudam você a criar modelos de formulário para funcionar conforme esperado em ambos os formatos.

### Recursos do AEM Forms Designer para HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### Visualizar HTML {#preview-html}

A guia Visualizar HTML é adicionada no modo Design para que os designers de formulários visualizem formulários no formato HTML5 durante o processo de design. Para obter mais informações sobre como habilitar e configurar este recurso no AEM Forms Designer, consulte [Visualizar HTML](../../forms/using/preview-xdp-forms-html.md).

#### Assinatura escrita {#scribble-signature}

O principal público-alvo para os formulários HTML5 são os dispositivos de toque. Portanto, um novo controle de assinatura de rabisco é adicionado ao AEM Forms Designer. Você pode clicar ou arrastar e soltar o controle de assinatura de rabisco no modelo de formulário e configurá-lo. Ele é renderizado como um campo de rabisco na representação do HTML5 e pode ser usado para rabiscar a assinatura em dispositivos de toque. Em computadores desktop, ele pode ser usado como um campo de rabisco usando o controle do mouse. Para obter mais informações sobre como usar este recurso, consulte [Campo de Rabisco do XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato Rich Text {#rich-text-format}

É possível converter um campo de texto em um campo rich text. Ele adiciona uma lista de opções de formatação ao campo de texto. Para converter, abra o Forms Designer, selecione o campo de texto no **[!UICONTROL Modo de Exibição de Design]**. Na guia **[!UICONTROL Campo]**, selecione **[!UICONTROL Rich Text]** na lista suspensa **[!UICONTROL Formato do Campo]**. Agora, quando o formulário XFA é renderizado como um formulário HTML5, o campo é renderizado como um campo de rich text. Selecione ![Maximizar](assets/maximize_icon.svg) para exibir opções de formatação adicionais.
