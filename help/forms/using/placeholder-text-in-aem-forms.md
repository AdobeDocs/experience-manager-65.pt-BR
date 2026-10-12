---
title: Texto para espaço reservado no AEM Forms
description: O texto para espaço reservado tem como objetivo ajudar o usuário com a entrada de dados quando o controle não tem valor. Pode ser um exemplo de valor ou uma breve descrição do formato esperado.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 4%
---
# Texto para espaço reservado no AEM Forms {#placeholder-text-in-aem-forms}

A Adobe <span class="preview"> recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

O texto de espaço reservado representa uma palavra ou frase curta. Tem como objetivo auxiliar o usuário com a entrada de dados quando o controle não tem valor. Um texto de espaço reservado pode ser um exemplo de valor ou uma breve descrição do formato esperado. O texto do espaço reservado é mostrado antes que o usuário insira um valor e é removido quando o usuário insere ou seleciona um valor.

>[!NOTE]
>
>O texto do espaço reservado, se especificado, deve ter um valor que não contenha caracteres de nova linha.

![Componente de data com e sem texto de espaço reservado](assets/dat-picker-place-holder-text.png)

**A.** Componente de data com texto de espaço reservado **B.** Componente de data sem texto de espaço reservado

O AEM Forms oferece suporte a texto de espaço reservado para campos de caixa de senha, seletor de data, caixa numérica e caixa de texto.\
Os textos de espaço reservado não são compatíveis com o widget de data nativo do HTML5. Para especificar um texto de Espaço Reservado:

1. Clique com o botão direito do mouse em um componente que ofereça suporte ao Texto do Espaço Reservado e clique em **Editar**. A caixa de diálogo Editar componente é exibida.

1. Abra a guia **Título e texto**.
1. Especifique uma palavra ou uma frase curta na **caixa de texto Espaço Reservado**. Clique em **OK**.

>[!NOTE]
>
>O texto para espaço reservado não é compatível com o Microsoft Internet Explorer 9.
