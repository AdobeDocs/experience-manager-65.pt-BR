---
title: 'Texto de espaço reservado no AEM Forms '
seo-title: 'Texto de espaço reservado no AEM Forms '
description: O texto de espaço reservado destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um valor de amostra ou uma breve descrição do formato esperado.
seo-description: O texto de espaço reservado destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um valor de amostra ou uma breve descrição do formato esperado.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Texto de espaço reservado no AEM Forms {#placeholder-text-in-aem-forms}

O texto do espaço reservado representa uma palavra ou frase curta. Destina-se a ajudar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um valor de amostra ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor, ele é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto de espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado  **B.** Componente de data sem texto de espaço reservado

O AEM Forms suporta o texto de espaço reservado para os campos Caixa de senha, Seletor de data, Caixa numérica e caixa de texto.\
Os textos de espaço reservado não são compatíveis com o widget de data HTML5 nativo. Para especificar um texto de Espaço reservado:

1. Clique com o botão direito do mouse em um componente que ofereça suporte ao Texto de espaço reservado e clique em **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra a guia **Título e texto**.
1. Especifique uma palavra ou uma frase curta na caixa de texto **Espaço reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto do espaço reservado não é suportado no Microsoft Internet Explorer 9.

