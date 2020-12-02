---
title: Criação de ajuda no contexto para campos de formulário
seo-title: Criação de ajuda no contexto para campos de formulário
description: A AEM Forms permite que você adicione ajuda contextual a campos e painéis de formulário adaptáveis, como texto ou mídia avançada, incluindo vídeos.
seo-description: A AEM Forms permite que você adicione ajuda contextual a campos e painéis de formulário adaptáveis, como texto ou mídia avançada, incluindo vídeos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---


# Criação de ajuda no contexto para campos de formulário{#authoring-in-context-help-for-form-fields}

## Introdução {#introduction}

Há situações em que os usuários finais que preenchem um formulário não têm certeza de como preencher os detalhes em um campo de formulário específico. Para resolver esses problemas, os formulários adaptáveis fornecem suporte para adicionar texto ou ajuda rich in-context a um campo de formulário. Isso ajuda a melhorar a experiência de preenchimento do formulário e evita qualquer ambiguidade para os usuários finais.

Este artigo aborda como os autores de formulários podem adicionar ajuda em contexto ao criar o Forms adaptativo.

## Adicionar ajuda no contexto {#add-in-context-help}

Você pode especificar a ajuda no contexto usando as seguintes opções na seção Conteúdo da Ajuda da guia de propriedades na barra lateral.

* [Descrição curta](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Descrição longa](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Ajuda contextual para campos de formulário](assets/descriptions.png)

>[!NOTE]
>
>A descrição longa substitui a Descrição curta. Se você tiver especificado ambos, somente a descrição Longa será exibida.

### Descrição curta {#short-description}

O campo Descrição curta fornece dicas rápidas e curtas sobre como preencher um campo de formulário. O texto especificado no campo Descrição curta é exibido como uma dica de ferramenta ao passar o mouse sobre o campo.

![Descrição curta para adicionar ajuda no contexto para campos de formulário](assets/tooltip.png)

>[!NOTE]
>
>Selecione **Sempre mostrar descrição curta** para exibir permanentemente o texto de ajuda abaixo do campo.

![Ajuda permanente curta no contexto abaixo do campo](assets/short1.png)

### Descrição longa {#long-description}

Você pode usar o campo Descrição longa para especificar texto longo ou incorporar conteúdo de mídia avançada, incluindo vídeos, como ajuda contextual. Por exemplo, a imagem a seguir mostra como você pode incorporar um vídeo como ajuda no contexto.

![Adicionar mídia avançada como ajuda contextual para campos de formulário](assets/long-descriptions.png)

Adicionar descrição longa exibe um **?** ícone ao lado do campo. Clicar no ícone exibe o conteúdo adicionado na seção de descrição longa.

![Exemplo de ajuda em contexto de mídia avançada](assets/photoshop.png)

### Ajuda no nível do painel {#panel-level-help}

Além da ajuda em contexto para campos de formulário, você pode especificar a ajuda em um nível de painel na guia Conteúdo da Ajuda da caixa de diálogo de edição do painel.

![Adicionar ajuda no contexto para um painel de formulários](assets/panel-level-help.png)

Adicionar ajuda para o painel exibe um **?** ao lado da descrição do painel. Clicar no ícone exibe o conteúdo adicionado na seção Conteúdo da Ajuda da caixa de diálogo de edição do painel.

![Exemplo de ajuda no contexto no nível do painel de formulários](assets/photoshop-1.png)

