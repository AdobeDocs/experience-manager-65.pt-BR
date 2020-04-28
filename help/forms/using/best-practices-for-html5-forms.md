---
title: Práticas recomendadas para formulários HTML5
seo-title: Práticas recomendadas para formulários HTML5
description: Ajuste seus formulários HTML5 baseados em XFA para obter o melhor desempenho.
seo-description: Saiba como ajustar seus formulários HTML5 baseados em XFA para obter o melhor desempenho.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: b6c013a31b70166cba80fea53dffc3794ffee5b8

---


# Best practices for HTML5 forms{#best-practices-for-html-forms}

## Visão geral {#overview}

O AEM Forms tem um componente chamado formulários HTML5. Ajuda a renderizar formulários PDF baseados em XFA (arquivos XDP) existentes no formato HTML5. Este documento fornece orientações e recomendações para reduzir o tempo de carregamento e melhorar o desempenho de formulários HTML5 em dispositivos móveis.

A maioria dos dispositivos móveis tem um poder de processamento e recursos de memória limitados. Ajuda a melhorar o tempo de espera dos dispositivos móveis. Os navegadores da Web em execução em um dispositivo móvel têm acesso a recursos limitados (memória limitada e recursos de processamento). Depois que o limite é atingido, o comportamento do navegador fica lento. Este documento fornece recomendações para manter o tamanho de um formulário HTML5 em verificação. Um formulário menor não quebra os limites de memória e potência de processamento de um dispositivo e proporciona uma experiência suave.

Embora as recomendações discutidas neste artigo sejam direcionadas para formulários HTML5, elas são igualmente aplicáveis aos formulários PDF baseados em XFA. Essas práticas recomendadas contribuem coletivamente para o desempenho geral dos formulários HTML5. Requer um planejamento cuidadoso para desenvolver formas eficientes e produtivas. Vamos começar:

## Nós são moeda de formulários HTML5, gaste-os sabiamente {#nodes-are-currency-of-html-forms-spend-them-wisely}

Geralmente, um formulário XFA tem vários elementos. Por exemplo, tabela, campo de texto e imagens. Cada elemento tem várias propriedades para controlar o comportamento e a aparência do elemento. Quando um formulário XFA é renderizado no formato HTML5, todos os elementos XFA e as propriedades correspondentes são convertidos em nós DOM Modelo ou HTML. Esses nós adicionam ao tamanho e à complexidade de um DOM. Tornar o formulário HTML5 lento para renderização.

É mais fácil para os navegadores renderizar um DOM mais claro. Portanto, é possível executar as seguintes otimizações em um formulário XFA para reduzir o número de nós. Portanto, gere uma estrutura DOM magra:

* Use a propriedade caption para adicionar um rótulo a um campo. Não use um elemento de Texto separado para adicionar um rótulo. Ele ajuda a eliminar pesos extras, gerando ganhos de desempenho. Também ajuda a evitar problemas de layout.
* Mantenha o número mínimo de elementos de texto Desenhar em um formulário. Os elementos de desenho são úteis para melhorar a legibilidade e a aparência, mas não têm recursos de armazenamento de informações. Recomenda-se unir vários elementos de texto Desenhar em um único elemento de texto Desenhar. Não deixe nenhuma pedra por trás para tornar a forma mais leve.

## Os formulários Lite têm melhor desempenho, mantêm os recursos compactados {#lite-forms-perform-better-keep-the-resources-compressed}

Um formulário HTML5 pode conter vários recursos externos, como arquivos de imagem, JavaScript e CSS. Toda vez que um navegador solicita um formulário, os recursos externos são enviados pela rede. O tempo necessário para viajar pela rede é diretamente proporcional ao tamanho dos arquivos.

Assim, reduzir o tamanho dos recursos externos e utilizar apenas os recursos absolutamente necessários é o método preferido para melhorar o desempenho dos formulários. É possível executar as seguintes otimizações em um formulário XFA para reduzir o tamanho dos recursos externos de um formulário:

* Use imagens [compactadas](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Reduz a atividade da rede e a quantidade de memória necessária para renderizar um formulário. Portanto, o tempo de carregamento do formulário diminui substancialmente.
* Use a opção de minificação no AEM Configuration Manager (Day CQ HTML Library Manager) para compactar arquivos JavaScript e CSS. Para obter detalhes, consulte Configurações [do](/help/sites-deploying/osgi-configuration-settings.md)OSGi.
* Ative a compactação da Web. Reduz o tamanho das solicitações e respostas originadas de um formulário. Para obter detalhes, consulte Ajuste [de desempenho do servidor](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html)de formulários AEM.

## Manter os interesses vivos, mostrar apenas os campos obrigatórios {#keep-the-interest-alive-show-only-required-fields}

Um formulário HTML5 pode ser executado em centenas de páginas. Um formulário com um grande número de campos é lento para carregar no navegador. É possível executar as seguintes otimizações em um formulário XFA para otimizar os formulários com um grande número de campos e páginas:

* Avalie a divisão dos formulários grandes em vários formulários. Também é possível usar um conjunto de formulários para agrupar todos os formulários menores e apresentá-los como uma única unidade. Um conjunto de formulários carrega apenas os formulários necessários. Além disso, em um conjunto de formulários, é possível configurar campos comuns em diferentes formulários para compartilhar vínculos de dados. Os vínculos de dados ajudam os usuários a preencher informações comuns apenas uma vez; as informações são preenchidas automaticamente em formulários subsequentes, resultando em melhorias substanciais de desempenho. Para obter mais detalhes sobre conjuntos de formulários, consulte Conjunto de [formulários em formulários](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)AEM.
* Considere dividir seções e mover cada seção para uma página diferente. Os formulários HTML5 carregam dinamicamente cada página na solicitação de rolagem da página. Somente as páginas roladas (a página que está sendo exibida e as páginas anteriores a ela) são armazenadas na memória; o restante das páginas é carregado sob demanda. Assim, dividir e mover uma seção em uma página própria reduz o tempo necessário para carregar um formulário. Também é possível usar a primeira página do formulário como uma landing page. É semelhante ao sumário de um livro. Uma landing page do formulário contém apenas links para as outras seções do formulário. Melhora significativamente o tempo de carregamento da primeira página do formulário e resulta em uma melhor experiência do usuário.
* Mantenha as seções condicionais ocultas, por padrão. Torne essas seções visíveis somente quando uma determinada condição for atendida. Isso ajuda a manter o tamanho do DOM no mínimo. Também é possível usar a navegação com guias para exibir apenas uma seção por vez.

## Menos é mais, reduza o número de páginas {#less-is-more-reduce-the-number-of-pages}

Formulários HTML5 podem conter campos orientados por dados (tabelas e subformulários). Esses campos expandem o tamanho do formulário no tempo de execução. Por exemplo, uma tabela orientada por dados em um formulário HTML5 pode se estender a milhares de linhas. Tais tabelas podem causar degradação do layout e do desempenho. As otimizações sugeridas abaixo podem ajudá-lo a reduzir o tempo de carregamento de formulários HTML5 com campos orientados por dados:

* Use o script XFA para obter navegação paginada para exibir campos controlados por dados (tabelas e subformulários). Na navegação por página, somente dados específicos são exibidos em uma página. Limita a operação de pintura do navegador aos campos exibidos de cada vez e facilita a navegação em um formulário. Além disso, os usuários nos dispositivos móveis estão interessados apenas em um subconjunto de dados. Ele ajuda a fornecer uma excelente experiência do usuário e reduz o tempo necessário para carregar os dados necessários. Você tem duas soluções pelo preço de uma.  Observe também que a navegação por paginação não está disponível na caixa. Você pode usar scripts XFA para desenvolver navegação paginada.

* Avalie a união de várias colunas somente leitura em uma única coluna. Reduz a memória necessária para exibir o formulário. Além disso, evite exibir as colunas que não exigem entradas dos usuários.
* Avalie a divisão do formulário controlado por dados em um conjunto [de](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)formulários, se as sugestões acima não gerarem muitas melhorias. Por exemplo, se uma tabela tiver mais de 1.000 linhas, mova cada 100 linhas para um formulário diferente. Isso ajudaria a melhorar o tempo de carregamento e o desempenho dos formulários.  Observe também que um conjunto de formulários produz um XML de envio consolidado para todos os formulários. Para diferenciar dados de cada formulário, use raízes de dados diferentes. Para obter mais informações, consulte [Formulário definido em Formulários](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)AEM.

## Potência de dois para o Documento de registro (DOR) {#power-of-two-for-document-of-record-dor}

Um formulário XFA pode ter um grande número de seções dedicadas apenas ao Documento de Registro (DOR). Para reduzir o número de nós e melhorar o desempenho de tal formulário, é possível manter cópias diferentes do formulário - uma cópia para preencher o formulário e outra para gerar o Documento de Registro no servidor. Na cópia para preencher o formulário XFA, mostrar os campos necessários apenas para capturar dados. No Documento de geração do Registro XFA, mantenha os campos obrigatórios somente na saída impressa do formulário. Antes de escolher a abordagem sugerida, avalie o ganho de desempenho e a sobrecarga de manutenção.

## Leituras recomendadas {#recommended-reads}

Os formulários do Adobe Experience Manager (AEM) podem ajudá-lo a transformar transações complexas em experiências digitais simples e deliciosas. No entanto, requer um esforço concertado para desenvolver formas eficientes e produtivas. Além do HTML5 Forms, veja algumas leituras recomendadas para práticas recomendadas gerais do AEM:

* [Práticas recomendadas para implantação e manutenção do AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas para a criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas para Administrar o AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas para o Desenvolvimento de soluções](/help/sites-developing/best-practices.md)
* [Práticas recomendadas para trabalhar com formulários adaptáveis](/help/forms/using/adaptive-forms-best-practices.md)
* [O servidor de formulários AEM não incorpora fontes a um formulário PDF dinâmico](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Cartão de referência rápido {#quick-reference-card}

Você pode imprimir o cartão a seguir (clique no cartão para baixar uma versão de alta resolução) e mantê-lo em sua mesa para obter uma referência rápida:
Cartão de referência rápido das práticas recomendadas do[ ![HTML5 Forms](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
