---
title: A geração de PDF não imprime um grande número de PDF com o WorkBench
description: Quando um cliente gera um grande número de PDF por meio de serviços implementados pelo WorkBench, ocorre uma falha no serviço de impressão.
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# A geração de PDF não imprime um grande número de PDF através do WorkBench {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## Problema {#issue}

Quando um cliente gera um grande número de PDF por meio de serviços implementados pelo WorkBench. Falha no serviço devido à memória insuficiente. O erro é exibido como:

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

Isso ocorre porque o número máximo de páginas em uma solicitação de impressão é limitado a aproximadamente 1000 páginas no Windows. Quando uma saída de impressão está sendo gerada, o modelo e os dados precisam ser carregados na memória e o layout resultante é construído na memória. Isso significa que há limites para o tamanho da saída final. O processo que gera a saída de impressão é uma tarefa de 32 bits, o que significa que ela é limitada a 2 GB de RAM no Windows <!--and 4 GB on UNIX-->.

## Aplica-se a {#applies-to}

A solução se aplica ao AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> para XMLFM x86_win32.

## Solução {#solution}

O fator mais importante que afeta o uso de memória é a quantidade de dados em um formulário. No entanto, há outros fatores em um design de formulário que afetam o uso da memória em menor grau. Quando estiver ciente desses fatores, você poderá criar um formulário para uma saída de impressão maior. A seção a seguir indica, em ordem de prioridade, fatores que influenciam o espaço ocupado pela memória:

### Fator de impacto {#impact-factor}

**Alta**

1. **Subformulários de escolha** - Um conjunto de subformulários de escolha é uma variação do objeto do conjunto de subformulários que permite personalizar a exibição de subformulários específicos de dentro do conjunto usando declarações condicionais.
1. **Usar texto estático no lugar de legendas** - Quase todos os campos fornecem uma legenda dentro do, o usuário deve usá-la em vez de ter um texto estático adicional como legenda.
1. Uso **Formato Rich Text (RTF)** possível.

**Média**

Outros fatores que devem ser considerados ao projetar o modelo de formulário para ajudar a melhorar o uso da memória:

1. Evite usar Texto estático para rotular um campo. Em vez disso, use legendas no Campo de texto.
2. Não use retângulos, linhas, objetos e tabelas em excesso.
3. Evite usar RichText e Subformulários de escolha, se possível.
4. Evite o uso excessivo de Subformulários e Subformulários aninhados.

### Limitação do tamanho de dados {#data-size-limitations}

Como somos limitados pela memória máxima do processo, a memória consumida pelo processo não depende apenas do tamanho do arquivo de dados. Ela está muito intimamente ligada ao design do formulário e, até certo ponto, à quantidade real de dados que estão sendo mesclados no formulário.

Se o formulário tiver muitos nós pequenos com dados pequenos, o processo consumirá mais memória (e, portanto, ficará sem memória mais rápido) do que um formulário que tenha menos nós (mesmo) com dados grandes.

Leia o [Apêndice abaixo](#appendix) para obter mais informações, onde os resultados dos testes são baseados no formulário Imprimir (PDF não marcado). O uso de requisitos de memória de processo de PDF marcado aumenta. Também depende do número de campos no formulário - aproximadamente, o requisito de memória do processo seria um pouco mais de 1,5 vez de PDF não marcado.

### Forms interativo {#interactive-forms}

Os formulários interativos consumiriam mais memória do que o Print Forms, já que os campos interativos são renderizados novamente. Nos testes realizados, o consumo de memória aumentou aproximadamente 1,5 vezes em relação aos formulários impressos, e eram formulários interativos estáticos.

### Formatos de imagem {#image-formats}

O Adobe não recomenda nenhum formato de imagem específico. Mas seria bom ter um tamanho menor de imagem, por exemplo, PNG (Portable Network Graphics). Também não é aconselhável usar imagens de alta resolução cujos tamanhos variam várias centenas de MegaBytes. Além disso, não é aconselhável usar imagens compactadas cujo tamanho, após a descompactação, se expande para várias centenas de Megabytes de dados.

### Apêndice {#appendix}

**Exemplos de tabela**

São mostradas abaixo diferentes variantes de tabelas que mostram a renderização do número de páginas em comparação ao tamanho dos dados de uma tabela simples e de uma tabela complexa.

1. Uma Tabela com uma única coluna onde são geradas 5.000 páginas de PDF, com tamanho de arquivo de dados de 24 MB e registros de 30 K.

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. Uma tabela com muitas colunas pequenas onde são geradas 800 páginas de PDF, o tamanho do arquivo de dados é de 4,6 MB e registros de 20 K.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. Uma tabela com muitas colunas pequenas, mas arquivos de dados maiores devido ao uso de nomes xmlTag maiores.
Aqui, tudo é igual ao anterior, mas os nomes das tags xml ficaram grandes (para que o tamanho do arquivo de dados aumente sem qualquer aumento nos dados efetivos reais), o resultado final (limite superior) é quase o mesmo. Embora o tamanho do arquivo de dados tenha aumentado de 4,6 MB para 44,6 MB. Aqui são geradas 800 páginas de PDF, o tamanho do arquivo de dados é de 44,6 MB e registros de 20 K.

   ![table_greater_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

Portanto, é difícil colocar um limite superior geral no tamanho do arquivo de dados. Cada formulário é único e, portanto, o consumo de memória seria diferente de forma para forma.