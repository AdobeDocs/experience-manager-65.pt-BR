---
title: Texto para espaço reservado no AEM Forms
seo-title: Placeholder text in AEM Forms
description: O texto para espaço reservado tem como objetivo ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um exemplo de valor ou uma breve descrição do formato esperado.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# Texto para espaço reservado no AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

O texto de espaço reservado representa uma palavra ou frase curta. Tem como objetivo auxiliar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um exemplo de valor ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor e é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto do espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

O AEM Forms oferece suporte a texto de espaço reservado para campos de caixa de senha, seletor de data, caixa numérica e caixa de texto.\
Os textos de marcadores de posição não são suportados para o widget de data nativo do HTML5. Para especificar um texto de Espaço Reservado:

1. Clique com o botão direito do mouse em um componente que suporte Texto para espaço reservado e clique **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra o **Título e texto** guia.
1. Especifique uma palavra ou uma frase curta na variável **Caixa de texto Espaço reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto para espaço reservado não é compatível com o Microsoft Internet Explorer 9.
