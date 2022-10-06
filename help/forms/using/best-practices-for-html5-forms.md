---
title: Práticas recomendadas para formulários HTML5
seo-title: Best practices for HTML5 forms
description: Ajuste seu Forms HTML5 baseado em XFA para obter o melhor desempenho.
seo-description: Learn how to tune your XFA-based HTML5 Forms for best performance.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 1%

---

# Práticas recomendadas para formulários HTML5{#best-practices-for-html-forms}

## Visão geral {#overview}

O AEM Forms tem um componente chamado formulários HTML5. Ajuda a renderizar PDF forms com base em XFA (arquivos XDP) existentes no formato HTML5. Este documento fornece diretrizes e recomendações para reduzir o tempo de carregamento e melhorar o desempenho dos formulários HTML5 em dispositivos móveis.

A maioria dos dispositivos móveis tem um poder de processamento e recursos de memória limitados. Ajuda a melhorar o tempo de espera dos dispositivos móveis. Os navegadores da Web em execução em um dispositivo móvel têm acesso a recursos limitados (memória limitada e recursos de processamento). Quando o limite é atingido, o comportamento do navegador fica lento. Este documento fornece recomendações para manter o tamanho de um formulário HTML5 sob controle. Um formulário menor não quebra limites de memória e potência de processamento de um dispositivo e fornece uma experiência perfeita.

Embora as recomendações discutidas neste artigo sejam direcionadas para formulários HTML5, no entanto, elas são igualmente aplicáveis a PDF forms baseados em XFA. Essas práticas recomendadas contribuem coletivamente para o desempenho geral dos formulários HTML5. Requer um planeamento cuidadoso para desenvolver formas eficientes e produtivas. Vamos começar:

## Nós são moeda de formulários HTML5, gastem-nos sabiamente {#nodes-are-currency-of-html-forms-spend-them-wisely}

Geralmente, um formulário XFA tem vários elementos. Por exemplo, tabela, campo de texto e imagens. Cada elemento tem várias propriedades para controlar o comportamento e a aparência do elemento. Quando um formulário XFA é renderizado no formato HTML5, todos os elementos XFA e as propriedades correspondentes são convertidos em nós Modelo ou HTML DOM. Esses nós adicionam ao tamanho e à complexidade de um DOM. Tornar o formulário HTML5 lento para renderização.

É mais fácil para os navegadores renderizar um DOM mais claro. Assim, você pode executar as seguintes otimizações em um formulário XFA para reduzir o número de nós. Portanto, gere uma estrutura DOM simples:

* Use a propriedade caption para adicionar um rótulo a um campo. Não use um elemento Texto separado para adicionar um rótulo. Ajuda a reduzir o peso extra, levando a ganhos de desempenho. Também ajuda a evitar problemas de layout.
* Mantenha o número mínimo de elementos de texto Desenhar em um formulário. Os elementos do desenho são úteis para melhorar a legibilidade e a aparência, mas não têm informações para armazenar recursos. É recomendável mesclar vários elementos de texto de Desenhar em um único elemento de texto de Desenhar . Não deixes cair pedra para deixar uma forma mais clara.

## Os formulários de sites têm melhor desempenho, mantêm os recursos compactados {#lite-forms-perform-better-keep-the-resources-compressed}

Um formulário HTML5 pode conter vários recursos externos, como arquivos de imagem, JavaScript e CSS. Toda vez que um navegador solicita um formulário, os recursos externos são enviados pela rede. O tempo necessário para viajar pela rede é diretamente proporcional ao tamanho dos arquivos.

Assim, reduzir o tamanho dos recursos externos e utilizar apenas os recursos absolutamente necessários é o método preferido para melhorar o desempenho dos formulários. Você pode executar as seguintes otimizações em um formulário XFA para reduzir o tamanho dos recursos externos de um formulário:

* Use [imagens compactadas](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Reduz a atividade da rede e a quantidade de memória necessária para renderizar um formulário. Portanto, o tempo de carregamento do formulário diminui substancialmente.
* Use a opção de diminuição no AEM Configuration Manager (Day CQ HTML Library Manager) para compactar arquivos JavaScript e CSS. Para obter detalhes, consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Habilite a compactação da Web. Reduz o tamanho das solicitações e respostas originadas de um formulário. Para obter detalhes, consulte [Ajuste de desempenho do servidor de formulários AEM](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html).

## Manter o interesse vivo, mostrar apenas os campos obrigatórios  {#keep-the-interest-alive-show-only-required-fields}

Um formulário HTML5 pode ser executado em centenas de páginas. Um formulário com um grande número de campos é carregado lentamente no navegador. Você pode executar as seguintes otimizações em um formulário XFA para otimizar os formulários com um grande número de campos e páginas:

* Avalie a divisão de formulários grandes em vários formulários. Também é possível usar um conjunto de formulários para agrupar todos os formulários menores e apresentá-los como uma única unidade. Um conjunto de formulários carrega apenas os formulários necessários. Além disso, em um conjunto de formulários, é possível configurar campos comuns em diferentes formulários para compartilhar vínculos de dados. Os vínculos de dados ajudam os usuários a preencher informações comuns apenas uma vez; as informações são preenchidas automaticamente em formulários subsequentes, resultando em melhorias substanciais de desempenho. Para obter mais detalhes sobre conjuntos de formulários, consulte [Formulário definido em formulários AEM](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* Considere dividir as seções e mover cada seção para uma página diferente. Os formulários HTML5 carregam dinamicamente cada página na solicitação de rolagem da página. Somente as páginas roladas (a página que está sendo exibida e as páginas anteriores a ela) são armazenadas na memória; o restante das páginas são carregadas sob demanda. Assim, dividir e mover uma seção em uma página própria reduz o tempo necessário para carregar um formulário. Você também pode usar a primeira página do formulário como página de aterrissagem. É semelhante ao índice de um livro. Uma landing page do formulário contém apenas links para as outras seções do formulário. Melhora significativamente o tempo de carregamento da primeira página do formulário e resulta em uma melhor experiência do usuário.
* Mantenha as seções condicionais ocultas, por padrão. Tornar essas seções visíveis somente quando uma determinada condição for atendida. Ajuda a manter o tamanho do DOM em um mínimo. Também é possível usar a navegação por guias para exibir apenas uma seção de cada vez.

## Menos é mais, reduza o número de páginas {#less-is-more-reduce-the-number-of-pages}

Formulários HTML5 podem conter campos orientados por dados (tabelas e subformulários). Esses campos expandem o tamanho do formulário no tempo de execução. Por exemplo, uma tabela orientada por dados em um formulário HTML5 pode se estender para milhares de linhas. Essas tabelas podem causar degradação do layout e do desempenho. As otimizações sugeridas abaixo podem ajudar você a reduzir o tempo de carregamento dos formulários HTML5 com campos orientados por dados:

* Use scripts XFA para obter a navegação por página e exibir campos orientados por dados (tabelas e subformulários). Na navegação por página, somente os dados específicos são exibidos em uma página. Limita a operação de pintar do navegador aos campos que estão sendo exibidos de cada vez e facilita a navegação de um formulário. Além disso, os usuários dos dispositivos móveis estão interessados apenas em um subconjunto de dados. Ajuda você a fornecer uma excelente experiência do usuário e reduz o tempo necessário para carregar os dados necessários. Você tem duas soluções pelo preço de uma.  Observe também que a navegação por paginação não está disponível imediatamente. Você pode usar scripts XFA para desenvolver a navegação por paginação.

* Avalie a mesclagem de várias colunas somente leitura em uma única coluna. Reduz a memória necessária para exibir o formulário. Além disso, evite exibir as colunas que não exigem entradas dos usuários.
* Avaliar a divisão do formulário controlado por dados em um [conjunto de formulários](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html), se as sugestões acima não produzirem muitas melhorias. Por exemplo, se uma tabela tiver mais de 1000 linhas, mova cada 100 linhas para um formulário diferente. Isso ajudaria a melhorar o tempo de carregamento e o desempenho dos formulários.  Observe também que um conjunto de formulários produz um XML de envio consolidado para todos os formulários. Para diferenciar dados de cada formulário, use raízes de dados diferentes. Para obter mais informações, consulte [Conjunto de formulários no AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potência de dois para Documento de Registro (DOR) {#power-of-two-for-document-of-record-dor}

Um formulário XFA pode ter um grande número de seções dedicadas apenas ao Documento de registro (DOR). Para reduzir o número de nós e melhorar o desempenho desse formulário, é possível manter diferentes cópias do formulário - uma cópia para preencher o formulário e outra para gerar o Documento de registro no servidor. Na cópia para preencher o formulário XFA, mostrar campos necessários apenas para capturar dados. No Documento de registro do, mantenha os campos obrigatórios somente na saída impressa do formulário. Antes de escolher a abordagem sugerida, avalie o ganho de desempenho e a sobrecarga de manutenção.

## Leituras recomendadas  {#recommended-reads}

Os formulários Adobe Experience Manager (AEM) podem ajudar você a transformar transações complexas em experiências digitais simples e deliciosas. No entanto, requer um esforço concertado para desenvolver formas eficientes e produtivas. Além do HTML5 Forms, veja algumas leituras recomendadas para práticas recomendadas gerais de AEM:

* [Práticas recomendadas para Implantação e manutenção de AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas para criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas para Administrar o AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas para Desenvolver soluções](/help/sites-developing/best-practices.md)
* [Práticas recomendadas para trabalhar com formulários adaptáveis](/help/forms/using/adaptive-forms-best-practices.md)
* [O servidor AEM Forms não incorpora fontes a um formulário PDF dinâmico](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Cartão de referência rápida {#quick-reference-card}

Você pode imprimir o seguinte cartão (clique no cartão para baixar uma versão de alta resolução) e mantê-lo em sua mesa para obter uma referência rápida:
[ ![HTML5 Cartão de referência rápida das práticas recomendadas da Forms](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
