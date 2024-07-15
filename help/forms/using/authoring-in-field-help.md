---
title: Criação da ajuda em contexto para campos de formulário
description: O AEM Forms permite adicionar ajuda em contexto a campos e painéis de formulário adaptáveis, como texto ou mídia avançada, incluindo vídeos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Criação da ajuda em contexto para campos de formulário{#authoring-in-context-help-for-form-fields}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Introdução {#introduction}

Há situações em que os usuários finais que preenchem um formulário não têm certeza de como preencher detalhes em um campo de formulário específico. Para resolver esses problemas, os formulários adaptáveis fornecem suporte para adicionar texto ou ajuda rica em contexto a um campo de formulário. Isso ajuda a melhorar a experiência de preenchimento de formulário e evita qualquer ambiguidade para os usuários finais.

Este artigo discute como os autores de formulários podem adicionar ajuda em contexto ao criarem o Forms adaptável.

## Adicionar ajuda em contexto {#add-in-context-help}

Você pode especificar a ajuda em contexto usando as seguintes opções na seção Conteúdo da Ajuda da guia de propriedades na barra lateral.

* [Descrição curta](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Descrição longa](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Ajuda em contexto para campos de formulário](assets/descriptions.png)

>[!NOTE]
>
>A descrição longa substitui a descrição curta. Se você tiver especificado ambos, somente a descrição Longa será exibida.

### Descrição curta {#short-description}

O campo Short description fornece dicas rápidas e curtas sobre o preenchimento de um campo de formulário. O texto especificado no campo Descrição curta é exibido como uma dica de ferramenta ao passar o mouse sobre o campo.

![Breve descrição para adicionar ajuda em contexto para campos de formulário](assets/tooltip.png)

>[!NOTE]
>
>Selecione **Sempre mostrar descrição curta** para exibir permanentemente o texto de ajuda abaixo do campo.

![Ajuda contextual curta permanente abaixo do campo](assets/short1.png)

### Descrição longa {#long-description}

Você pode usar o campo Descrição longa para especificar texto longo ou incorporar conteúdo de mídia avançada, incluindo vídeos, como ajuda no contexto. Por exemplo, a imagem a seguir mostra como é possível incorporar um vídeo como ajuda em contexto.

![Adicionando mídia avançada como ajuda em contexto para campos de formulário](assets/long-descriptions.png)

Adicionar descrição longa exibe um **?Ícone** ao lado do campo. Clicar no ícone exibe o conteúdo adicionado na seção de descrição longa.

![Exemplo de ajuda em contexto de mídia avançada](assets/photoshop.png)

### Ajuda no nível do painel {#panel-level-help}

Além da ajuda em contexto para campos de formulário, você pode especificar a ajuda em nível de painel na guia Conteúdo da ajuda da caixa de diálogo de edição do painel.

![Adicionando ajuda em contexto para um painel de formulário](assets/panel-level-help.png)

Adicionar ajuda para o painel exibe um **?Ícone** ao lado da descrição do painel. Clicar no ícone exibe o conteúdo adicionado na seção Conteúdo da ajuda da caixa de diálogo de edição do painel.

![Exemplo de ajuda em contexto no nível do painel do formulário](assets/photoshop-1.png)
