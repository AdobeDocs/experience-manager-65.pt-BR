---
title: Aprimoramentos de tradução
seo-title: Translation Enhancements
description: Aprimoramentos de tradução em AEM.
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 28%

---

# Aprimoramentos de tradução{#translation-enhancements}

Esta página apresenta aprimoramentos e refinamentos incrementais para AEM recursos de gerenciamento de tradução.

## Automação de projetos de tradução {#translation-project-automation}

Foram adicionadas opções para melhorar a produtividade ao trabalhar com projetos de tradução, como promover e excluir automaticamente inicializações de tradução e agendar a execução recorrente de um projeto de tradução.

1. No seu projeto de tradução, clique ou toque nas reticências na parte inferior do **Resumo da tradução** mosaico.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Alterne para **Avançado** guia . Na parte inferior, você pode selecionar **Promover automaticamente inicializações de tradução**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. Como opção, você pode selecionar se, depois de receber o conteúdo traduzido, as inicializações de tradução devem ser promovidas e excluídas automaticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Para selecionar a execução recorrente de um projeto de tradução, selecione a frequência com a lista suspensa em **Repetir tradução**. A execução do projeto recorrente criará e executará automaticamente tarefas de tradução nos intervalos especificados.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Projetos de tradução multilíngues {#multilingual-translation-projects}

É possível configurar vários idiomas de destino em um projeto de tradução, para reduzir o número total de projetos de tradução criados.

1. No seu projeto de tradução, clique ou toque nos pontos na parte inferior da **Resumo da tradução** mosaico.

   ![screen_shot_2018-04-19at22622](assets/screen_shot_2018-04-19at222622.jpg)

1. Alterne para **Avançado** guia . Você pode adicionar vários idiomas em **Idioma de destino**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. Como alternativa, se você estiver iniciando a tradução por meio do painel de referências no Sites, adicione os idiomas e selecione **Criar projeto de tradução em vários idiomas**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. Os trabalhos de tradução serão criados no projeto para cada idioma de destino. Eles podem ser iniciados um por um no projeto ou de uma só vez executando o projeto globalmente no Administrador de projetos.

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Atualizações da memória de tradução {#translation-memory-updates}

As edições manuais de conteúdo traduzido podem ser sincronizadas com o Sistema de gerenciamento de tradução (TMS) para treinar a memória de tradução.

1. No console Sites , depois de atualizar o conteúdo do texto em uma página traduzida, selecione **Atualizar memória de tradução**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Uma exibição de lista mostra uma comparação lado a lado da origem e da tradução para cada componente de texto que foi editado. Selecione quais atualizações de tradução devem ser sincronizadas com a Memória de Tradução e selecione **Atualizar memória**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

O AEM atualiza a tradução dos segmentos existentes na memória de tradução do TMS configurado.

* A ação atualiza a tradução dos segmentos existentes na memória de tradução do TMS configurado.
* Isso não cria novos trabalhos de tradução.
* As traduções são enviadas de volta para o TMS, por meio da API de tradução do AEM (veja abaixo).

Para usar este recurso:

* Um TMS deve ser configurado para uso com o AEM.
* O conector precisa implementar o método [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * O código desse método determina o que acontece com a solicitação de atualização da memória de tradução.
   * A estrutura de tradução do AEM envia os pares de valores do segmento (tradução original e atualizada) para o TMS por meio da implementação desse método.

As atualizações da memória de tradução podem ser interceptadas e enviadas a um destino personalizado, nos casos em que uma memória de tradução própria for usada.

## Cópias de idioma em vários níveis {#language-copies-on-multiple-levels}

As raízes de idioma agora podem ser agrupadas em nós, por exemplo, por região, enquanto ainda são reconhecidas como raízes de cópias de idioma.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>Somente um nível é permitido. Por exemplo, o seguinte não permitirá que a página &quot;es&quot; seja resolvida para uma cópia de idioma:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>Essa `es` a cópia do idioma não será detectada, pois está a dois níveis (américas/américa central) longe do `en` nó .

>[!NOTE]
>
>As raízes de idioma podem ter qualquer nome de página, em vez de apenas o código ISO do idioma. AEM sempre verificará o caminho e o nome primeiro, mas se o nome da página não identificar um idioma, AEM verificará a propriedade cq:language da página para a identificação do idioma.

## Relatório de status da tradução {#translation-status-reporting}

Uma propriedade agora pode ser selecionada na exibição da lista Sites que mostra se uma página foi traduzida, está na tradução ou ainda não foi traduzida. Para exibi-lo:

1. Em Sites, alterne para **Exibição de lista.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Clique ou toque em **Exibir configurações**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Verificar **Traduzido** caixa de seleção em **Tradução** e toque/clique **Atualizar**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Agora você pode ver um **Traduzido** coluna que mostra o status de tradução das páginas.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
