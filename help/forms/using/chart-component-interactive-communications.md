---
title: Uso de gráficos em Comunicações interativas
seo-title: Componente de gráfico em Comunicações interativas
description: Usando gráficos em uma Comunicação Interativa, você pode condensar grandes quantidades de informações em um formato visual fácil de analisar
seo-description: O AEM Forms fornece um componente de gráfico que você pode usar para criar gráficos em sua Comunicação interativa. Este documento explica as configurações básicas e do agente do componente de gráfico.
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
feature: Comunicação interativa
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2648'
ht-degree: 2%

---


# Uso de gráficos em Comunicações interativas{#using-charts-in-interactive-communications}

Um gráfico ou um gráfico é uma representação visual de dados. Ela condensa grandes quantidades de informações em um formato visual fácil de entender, permitindo que os recipients da Comunicação interativa visualizem, interpretem e analisem melhor os dados complexos.

Ao criar uma Comunicação interativa, é possível adicionar gráficos para representar visualmente dados bidimensionais a partir do modelo de dados de formulário da Comunicação interativa. O componente Gráfico permite adicionar e configurar os seguintes tipos de gráficos: Pizza, Coluna, Rosca, Barra, Linha, Linha e Ponto, Ponto, Área e Quadrante.

## Adicionar e configurar um gráfico em uma Comunicação Interativa {#add-and-configure-chart-in-an-interactive-communication}

Execute as seguintes etapas para adicionar e configurar um gráfico em uma Comunicação interativa:

1. Toque em **Componentes** no sidekick da Comunicação interativa.
1. Arraste e solte o componente **Chart** para um dos seguintes componentes:

   * Canal de impressão: Área de destino ou campo de imagem
   * Canal da Web: Painel ou área de destino

1. Toque no componente de gráfico no editor de Comunicação interativa e selecione **[!UICONTROL Configurar (]** ![configurar_icon](assets/configure_icon.png)) na barra de ferramentas Componente.

   As Propriedades do Gráfico são exibidas no painel esquerdo.

   ![Propriedades básicas de um gráfico de tipo de linha no canal de impressão](assets/chart_properties_print_new.png)

   Propriedades básicas de um gráfico de tipo de linha no canal de impressão

   ![Propriedades básicas de um gráfico de tipo de linha no canal da Web](assets/chart_properties_web_new.png)

   Propriedades básicas de um gráfico de tipo de linha no canal da Web

1. Configure as [propriedades do gráfico](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) com base no tipo de canal.
1. (Somente canal de impressão) Nas **[!UICONTROL Configurações do Agente]**, especifique se é obrigatório que o agente use este gráfico. Se a opção i **[!UICONTROL t Is Mandatory To the Agent To Use This Chart]** não estiver selecionada, o agente poderá tocar no ícone de olho do gráfico na guia **[!UICONTROL Content]** da interface do usuário do agente para mostrar ou ocultar o gráfico.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. Toque em ![done_icon](assets/done_icon.png) para salvar as propriedades do gráfico.

   Toque em **[!UICONTROL Preview]** para exibir a aparência e os dados associados ao gráfico. Toque em **[!UICONTROL Editar]** para reconfigurar as propriedades do gráfico.

## Configurar propriedades do gráfico {#configure-chart-properties}

Configure as seguintes propriedades ao criar gráficos para canais de impressão e da Web:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
   <td>Tipo de canal</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Identificador para o elemento do gráfico. O nome do gráfico especificado neste campo não está visível no gráfico. Ele é usado ao se referir ao elemento de outros componentes, scripts e expressões SOM.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Tipo de gráfico</td>
   <td>Tipo de gráfico que você deseja gerar. As opções disponíveis são Pizza, Coluna, Rosca, Barra, Linha, Linha e Ponto, Ponto e Área.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Série &gt; Várias séries</td>
   <td>Selecione para adicionar várias séries para os itens de coleção do modelo de dados de formulário plotados no eixo X e no eixo Y.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Série &gt; Objeto do modelo de dados</td>
   <td>Nome do item de coleção do modelo de dados de formulário para adicionar várias séries ao gráfico.<br /> Escolha uma propriedade de objeto de modelo de dados de formulário pai para as propriedades plotadas no eixo X e no eixo Y para formar uma série significativa. O objeto de modelo de dados que você vincula deve ser do tipo Número, String ou Data.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Mostrar empilhado</td>
   <td>Opte por empilhar os valores de cada séria, um sobre o outro.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Eixo X &gt; Título</td>
   <td>Título do eixo X.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Eixo X &gt; Objeto do modelo de dados</td>
   <td><p>Nome do item de coleção do modelo de dados de formulário a ser plotado no eixo X.</p> <p>Escolha duas propriedades de tipo de coleção/matriz do mesmo objeto de modelo de dados pai que sejam significativas em relação umas às outras para plotar no eixo X e Y de um gráfico. O objeto de modelo de dados que você vincula deve ser do tipo Número, String ou Data.</p> </td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Eixo Y &gt; Título</td>
   <td>Título do eixo Y. </td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Eixo Y &gt; Objeto do modelo de dados</td>
   <td><p>Item de coleção do modelo de dados de formulário a ser plotado no eixo Y. No canal Impressão, o objeto de modelo de dados para o eixo Y deve ser do tipo Número.</p> <p>Escolha duas propriedades de tipo de coleção/matriz do mesmo objeto de modelo de dados pai que sejam significativas em relação umas às outras para plotar no eixo X e Y de um gráfico. </p> </td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Eixo Y &gt; Função</td>
   <td>Função estatística/personalizada a ser usada para calcular os valores no eixo y.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Ocultar objeto</td>
   <td>Selecione para ocultar o gráfico na saída final.</td>
   <td>Impressão e Web</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Título do gráfico. </td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Altura</td>
   <td>Altura do gráfico em pixels.</td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Largura</td>
   <td>Largura do gráfico em pixels. É possível controlar a largura do gráfico no canal da Web usando a camada de estilo ou aplicando um tema.</td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Quebra de Página Obrigatória Antes</td>
   <td>Selecione para adicionar uma quebra de página obrigatória antes do gráfico e coloque o gráfico na parte superior de uma nova página. </td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Quebra obrigatória de página após</td>
   <td>Selecione para adicionar uma quebra de página obrigatória após o gráfico e coloque o conteúdo após o gráfico na parte superior de uma nova página. </td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Recuo</td>
   <td>Recuo do gráfico à esquerda da página. </td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Dica</td>
   <td><p>Formato no qual a dica de ferramenta aparece ao passar o mouse sobre um ponto de dados no gráfico do canal da Web. O valor padrão é ${x}(${y}). Dependendo do tipo de gráfico, quando você aponta o mouse para um ponto, barra ou fatia no gráfico, as variáveis ${x}e ${y} são substituídas dinamicamente pelos valores correspondentes no eixo X e no eixo Y e exibidas na dica de ferramenta.</p> <p>Para desativar a dica de ferramenta, deixe o campo <span class="uicontrol">Dica de ferramenta</code> em branco. Essa opção não é aplicável para gráficos de linha e de área. Por exemplo, consulte <a href="#chartoutputprintweb">Exemplo 1: Saída do gráfico em print e web</a>.</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>Configurações específicas do gráfico</td>
   <td><p>Além de configurações comuns, a seguinte configuração específica do gráfico está disponível:</p>
    <ul>
     <li><strong>Mostrar legenda:  </strong>Mostra uma legenda para o gráfico de pizza ou rosca quando ativado.</li>
     <li><strong>Posição da legenda:  </strong>Especifica a posição da legenda em relação ao gráfico. As opções disponíveis são Direita, Esquerda, Superior e Inferior. É recomendável usar a legenda do lado direito no canal de impressão.</li>
     <li><strong>Raio</strong> interno: Disponível para gráficos de rosca para especificar o raio (em pixels) do círculo interno no gráfico.</li>
     <li><strong>Cor</strong> da linha: Disponível para gráficos de linha, ponto e área para especificar a cor da linha no gráfico.</li>
     <li><strong>Cor</strong> do ponto: Disponível para gráficos de Ponto e Linha e Ponto para especificar a cor dos pontos no gráfico.<br /> </li>
     <li><strong>Cor</strong> da área: Disponível para gráficos de área para especificar a cor da área sob a linha no gráfico.</li>
     <li><strong>Ponto de referência &gt; Tipo de vínculo:  </strong>Disponível para gráficos do Quadrante <strong> </strong>para especificar o tipo de vínculo para o ponto de referência. Use texto estático ou propriedade de objeto de modelo de dados para definir o valor do ponto de referência.</li>
     <li><strong>Ponto de referência &gt; Eixo X:  </strong>Disponível para gráficos de Quadrante se você selecionar  <span class="uicontrol"></code> Estático na lista suspensa Tipo de Vínculo para especificar o valor do eixo X para o ponto de referência.</code></li>
     <li><strong>Ponto de referência &gt; Eixo Y:  </strong>Disponível para gráficos de Quadrante se você selecionar  <span class="uicontrol"></code> Estático na lista suspensa Tipo de Vínculo para especificar o valor do eixo Y para o ponto de referência.</code></li>
     <li><strong>Ponto de referência &gt; Objeto de modelo de dados para séries:  </strong>Disponível para gráficos do Quadrante de várias séries, se você selecionar Objetos  <span class="uicontrol">do Modelo de </code> Dados na lista suspensa Tipo de Vínculo . Defina a propriedade do objeto de modelo de dados de formulário para identificar o conjunto do ponto de referência. </code></li>
     <li><strong>Ponto de referência &gt; Valor do objeto do modelo de dados para séries:  </strong>Disponível para gráficos do Quadrante de várias séries, se você selecionar Objetos  <span class="uicontrol">do Modelo de </code> Dados na lista suspensa Tipo de Vínculo . Use a propriedade de objeto de modelo de dados de formulário para a série e o valor definido neste campo para identificar a série para o ponto de referência.</code></li>
     <li><strong>Ponto de referência &gt; Objeto do modelo de dados para o ponto de referência:  </strong>Disponível para gráficos do Quadrante se você selecionar  <span class="uicontrol">Objeto do Modelo de </code> Dados na lista suspensa Tipo de Vínculo . Defina uma propriedade de objeto de modelo de dados de formulário que seja um irmão das propriedades plotadas no eixo X e no eixo Y. Além disso, para várias séries, defina uma propriedade de objeto de modelo de dados que seja uma entidade-filho da propriedade de objeto de modelo de dados definida para as séries.</code></li>
     <li><strong>Ponto de referência &gt; Valor do objeto do modelo de dados para o ponto de referência:  </strong>Disponível para gráficos do Quadrante se você selecionar  <span class="uicontrol">Objeto do Modelo de </code> Dados na lista suspensa Tipo de Vínculo . Use a propriedade de objeto de modelo de dados de formulário para o ponto de referência e o valor definido neste campo para identificar o ponto de referência do gráfico.<br /> <strong>Rótulos do quadrante &gt; Superior esquerdo: </strong> Disponível para gráficos do quadrante para especificar o nome do quadrante superior esquerdo.</code></li>
     <li><strong>Rótulos do quadrante &gt; Superior direito: </strong> disponível para gráficos do quadrante para especificar o nome do quadrante superior direito.</li>
     <li><strong>Rótulos do quadrante &gt; Parte inferior direita:  </strong>Disponível para gráficos de Quadros para especificar o nome do quadrante Inferior Direito.</li>
     <li><strong>Rótulos do quadrante &gt; Parte inferior esquerda:  </strong>Disponível para gráficos de Quadros para especificar o nome do quadrante Inferior Esquerdo.</li>
    </ul> </td>
   <td>Impressão e Web</td>
  </tr>
 </tbody>
</table>

## Usar funções no gráfico {#use-functions-in-chart}

Você pode configurar um gráfico para usar funções estatísticas para calcular valores a partir dos dados de origem para plotar no gráfico. Ao aplicar funções em um gráfico, é possível plotar dados que não são fornecidos diretamente pelo modelo de dados do formulário.

![Funções em gráficos](assets/functions_charts_new.png)

Embora o componente Gráfico seja fornecido com algumas funções incorporadas, você pode gravar [funções personalizadas](#customfunctionsweb) e disponibilizá-las para uso na configuração do gráfico no canal da Web.

As seguintes funções estão disponíveis por padrão com o componente Gráfico :

**Média (Média)** Retorna a média dos valores no eixo X ou Y para um determinado valor no outro eixo.

**** SumRetorna a soma de todos os valores no eixo X ou Y para um determinado valor no outro eixo.

**** MaximumRetorna o máximo dos valores no eixo X ou Y para um determinado valor no outro eixo.

**** FrequencyRetorna o número de valores no eixo X ou Y para um determinado valor no outro eixo.

**** RangeRetorna a diferença entre o máximo e o mínimo dos valores no eixo X ou Y para um determinado valor no outro eixo.

**** MedianRetorna o valor que separa valores mais altos e mais baixos na metade no eixo X ou Y para um determinado valor no outro eixo.

**** MinimumRetorna o mínimo dos valores no eixo X ou Y para um determinado valor no outro eixo.

**** ModoRetorna o valor com a maioria das ocorrências no eixo X ou Y para um determinado valor no outro eixo.

Para obter mais informações, consulte [Exemplo 2: Aplicação das funções Soma e Frequência em um gráfico de linhas](#applicationsumfrequency).

### Funções personalizadas no canal da Web {#customfunctionsweb}

Além de usar as funções padrão em gráficos, você pode gravar funções personalizadas no JavaScript™ e disponibilizá-las na lista de funções no componente Gráfico do canal da Web.

Uma função pega uma matriz ou valores e um nome de categoria como entradas e retorna um valor. Por exemplo:

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

Depois de gravar uma função personalizada, faça o seguinte para disponibilizá-la para uso na configuração do gráfico:

1. Adicione a função personalizada na biblioteca do cliente associada à Comunicação interativa relevante. Para obter mais informações, consulte [Configuração da ação Enviar](/help/forms/using/configuring-submit-actions.md) e [Uso de bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md).

1. Para exibir a função personalizada no menu suspenso Função , no CRXDe Lite, crie um nó `nt:unstructured` na pasta de aplicativos com as seguintes propriedades:

   * Adicione a propriedade `guideComponentType` com o valor como `fd/af/reducer`. (mandatory)

   * Adicione a propriedade `value` a um nome totalmente qualificado da função JavaScript™ personalizada. (obrigatório) e defina seu valor com o nome da função personalizada, como Multiply.
   * Adicione a propriedade `jcr:description` com o valor que você deseja exibir como o nome da função personalizada que aparece no menu suspenso Função . Por exemplo, **Multiply**.

   * Adicione a propriedade `qtip` com o valor que será uma breve descrição da função personalizada. Ele aparece como uma dica de ferramenta ao passar o ponteiro sobre o nome da função na lista suspensa **Function**.

1. Clique em **Salvar tudo** para salvar a configuração.

A função agora está disponível para uso no Gráfico.

## Exemplo 1: Saída do gráfico na impressão e na Web {#chartoutputprintweb}

Na guia Básico , é possível definir o tipo de gráfico, as propriedades do modelo de dados do formulário de origem que contêm dados, os rótulos a serem representados no eixo X e no eixo Y do gráfico e, como opção, a função estatística para calcular os valores para plotamento no gráfico.

Vamos entender em detalhes as informações mínimas necessárias nas propriedades básicas, com a ajuda de uma instrução de cartão gerada por meio de uma Comunicação interativa. Considere que você deseja gerar um gráfico para descrever a quantidade de diferentes despesas na instrução. Você deseja usar diferentes tipos de gráficos para impressão e saída da Web da Comunicação interativa.

### Gráfico de colunas para Imprimir {#columnchartprint}

Para fazer isso, especifique as seguintes propriedades:

* **[!UICONTROL Nome]**  - Especifique o nome do gráfico.
* **[!UICONTROL Tipo de gráfico]**  - Selecione  **** Coluna na lista suspensa.
* **[!UICONTROL Título]**  - Especifique o Tipo de Despesa para o eixo X e a Quantia da Transação para o eixo Y.
* **[!UICONTROL Objetos do Modelo de Dados]**  - Selecione as propriedades do objeto do modelo de dados para criar vínculos de dados para o eixo X (Tipo de Despesa) e o eixo Y (Quantia da Transação).

![Gráfico de colunas no canal de impressão de uma comunicação interativa](assets/sample_chart_print_column_new.png)

Gráfico de colunas no canal de impressão de uma comunicação interativa

### Gráfico de rosca para web {#donutchartweb}

Para fazer isso, especifique as seguintes propriedades:

* **[!UICONTROL Nome]**  - Especifique o nome do gráfico.
* **[!UICONTROL Tipo de gráfico]**  - Selecione  **** Não na lista suspensa.
* **[!UICONTROL Objetos do Modelo de Dados]**  - Selecione as propriedades do objeto do modelo de dados para criar vínculos de dados para o eixo X (Tipo de Despesa) e o eixo Y (Quantia da Transação).
* **[!UICONTROL Raio interno]**  - Especifique o valor do Raio interno como 150 para especificar o raio (em pixels) do círculo interno no gráfico.
* **[!UICONTROL Dica de ferramenta]**  - Use o formato padrão ${x}(${y}) para exibir a dica de ferramenta. A dica de ferramenta é exibida como: Tipo de Despesa (Quantia da Transação). Exemplo: Débito para Bitcurrency(10000).

![Gráfico de rosca no canal Web de uma Comunicação Interativa](assets/sample_chart_web_new.png)

Gráfico de rosca no canal Web de uma Comunicação Interativa

## Exemplo 2: Aplicação das funções Soma e Frequência em um gráfico de linhas {#applicationsumfrequency}

Ao aplicar funções em um gráfico, é possível plotar dados que não são fornecidos diretamente pelo modelo de dados do formulário. Neste exemplo, usamos um exemplo de declaração de cartão de crédito para entender como as funções Soma e Frequência podem ser aplicadas ao gráfico.

![Gráfico de linhas sem uma função com duas transações &quot;Débito para AirBnB&quot;](assets/line_chart_web_new.png)

Gráfico de linhas sem uma função com duas transações &quot;Débito para AirBnB&quot;

### Função Sum {#sum-function}

É possível aplicar a função sum para adicionar valores de várias instâncias da mesma propriedade de dados e exibi-la apenas uma vez. Por exemplo, no gráfico a seguir, a função Sum é aplicada no eixo Y para somar o valor das duas transações Debit for AirBnB (2050 e 1050) e mostrar apenas uma transação (3100).

A função Sum pode tornar o gráfico mais útil quando você deseja comparar e exibir a soma de várias instâncias da mesma propriedade de dados.

![Soma do gráfico de linhas](assets/line_chart_web_sum_new.png)

### Função de frequência {#frequency-function}

A função Frequency retorna o número de valores do eixo Y para um determinado valor no outro eixo. Com a aplicação da função Frequency no eixo Y (Quantia da Transação), o gráfico exibe que houve duas ocorrências de Débito para transações AirBnB e uma ocorrência do resto dos tipos de transações.

![Frequência do gráfico de linhas](assets/line_chart_web_functions_frequency_new.png)

## Exemplo 3: Gráfico Quadrante de Várias Séries na Web {#example-multi-series-quadrant-chart-in-web}

O gráfico representa o valor das transações executadas em um determinado intervalo de datas. O Gráfico de quadrantes fornece a capacidade de dividir a área do gráfico em quatro seções rotuladas. O gráfico usa um ponto de referência estático para o eixo X e o eixo Y. Use o recurso de várias séries para segregar dados com base no nome do banco.

Para fazer isso, especifique as seguintes propriedades:

* **Nome:** especifique o nome do gráfico.
* **Tipo de gráfico:** selecione  **** Quadrante na lista suspensa.

* Marque a caixa de seleção **Multiple Series**.
* **Objeto** do Modelo de Dados: Especifique a propriedade de objeto do modelo de dados para a série. A propriedade de objeto do modelo de dados para o nome do banco é um pai das propriedades de objetos do modelo de dados plotadas no eixo X e no eixo Y.
* **Objetos do Modelo de Dados:** Selecione as propriedades do objeto do modelo de dados para criar vínculos de dados para o eixo X (Data da Transação) e o eixo Y (Quantia da Transação).
* Na seção **Ponto de referência**, selecione **Estático** como o Tipo de Vínculo.

* Especifique os valores para os pontos de referência do eixo X e do eixo Y.
* Especifique os rótulos do quadrante para os quadrantes Superior Esquerdo, Superior Direito, Inferior Direito e Inferior Esquerdo.
* Marque a caixa de seleção **Show legends** para exibir os códigos de cor dos nomes dos bancos.

![Gráficos de quadrante](assets/charts_quadrant_example_new.png)

