---
title: Texto de espaço reservado no AEM Forms
seo-title: Placeholder text in AEM Forms
description: O texto de espaço reservado destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um valor de amostra ou uma breve descrição do formato esperado.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Texto de espaço reservado no AEM Forms {#placeholder-text-in-aem-forms}

O texto do espaço reservado representa uma palavra ou frase curta. Destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um valor de amostra ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor, ele é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto de espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

O AEM Forms suporta o texto de espaço reservado para os campos Caixa de senha, Seletor de data, Caixa numérica e caixa de texto.\
Os textos de espaço reservado não são suportados para o widget de data HTML5 nativo. Para especificar um texto de Espaço reservado:

1. Clique com o botão direito do mouse em um componente compatível com o Texto de espaço reservado e clique em **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra o **Título e texto** guia .
1. Especifique uma palavra ou uma frase curta no **Caixa de texto Espaço reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto de espaço reservado não é suportado no Microsoft Internet Explorer 9.
