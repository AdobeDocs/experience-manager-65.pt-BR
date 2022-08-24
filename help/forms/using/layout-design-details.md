---
title: Design de layout
seo-title: Layout Design
description: Detalhes de design do layout explica como você pode criar layouts para serem usados em cartas ou comunicações interativas.
seo-description: Layout Design Details explains how you can create layouts to be used for your letters or Interactive Communications.
uuid: 469a8a71-88f7-4102-bb02-38ed05390f6c
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 683809ac-089b-49bf-a72c-67d32439081f
docset: aem65
feature: Correspondence Management
exl-id: 9e1b0067-c7dc-4bbb-a209-d674592be858
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2170'
ht-degree: 0%

---

# Design de layout{#layout-design}

Os modelos de formulário XFA ou XDPs são os modelos para:

* [Cartas](/help/forms/using/create-letter.md)
* [Canal de impressão](/help/forms/using/web-channel-print-channel.md#printchannel) de [Comunicações interativas](/help/forms/using/interactive-communications-overview.md)

* Fragmentos de layout

Um XDP foi projetado no Adobe Forms Designer. Este artigo fornece detalhes sobre como projetar seus XDPs para criar correspondências/Comunicações interativas eficazes, como onde usar campos de formulário ou áreas de destino e quando usar fragmentos de layout.

## Criação de um layout para letras ou para o canal de impressão do Interative Communications {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Um layout define o layout gráfico de um canal de letra/impressão de uma Comunicação interativa. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Crie o layout no designer de formulários e, quando concluído, o Application Specialist o fará upload para AEM servidor. A partir daí, é possível selecionar o layout ao criar um template de correspondência ou um canal de impressão de uma Comunicação interativa.

![Designer: criar um layout](assets/claimsubrogationlayout.png)

Siga estas etapas para criar layouts para letras/canal de impressão de Comunicações interativas:

1. Analise o layout e determine o conteúdo que está sendo repetido em todas as páginas; normalmente, o cabeçalho e o rodapé da página se encaixam nesta categoria. Esse conteúdo é colocado nas páginas principais do layout. O conteúdo restante vai para as páginas de corpo do layout. Em uma jaqueta de política, o logotipo e o endereço da empresa podem ser adicionados ao cabeçalho e rodapé principais da página. Por exemplo, o Aviso de cancelamento usa o mesmo layout.
1. Ao projetar páginas de corpo, divida o conteúdo da página em seções. Cada seção é projetada como um subformulário incorporado no próprio layout ou como um layout de fragmento. Se a seção contiver tabela, modele a seção como um fragmento de layout.
1. Um Layout pode ser projetado da seguinte maneira:

   1. Torne cada seção um subformulário separado contendo todos os elementos da seção.
   1. Torne cada subformulário de seção filho do mesmo subformulário pai. O layout do subformulário pai é definido para continuar, permitindo que as seções se alterem para baixo caso dados grandes sejam unidos em seções anteriores.
   1. A residência principal da seção também pode ser reutilizada em outros layouts. Crie-o como um layout de fragmento.
   1. Seção Os detalhes de interesse adicionais contêm apenas dois elementos colocados um abaixo do outro, podem conter dados grandes e são projetados como continuados.
   1. Outras seções contêm elementos em posições específicas para que sejam projetadas como layout posicionado.
   1. Divida uma seção em subformulários se a seção contiver elementos em posições específicas e esses elementos contiverem grandes quantidades de dados. Em seguida, organize os subformulários para alcançar o comportamento desejado.
   1. Para a seção Residência primária , adicione uma área de destino de espaço reservado. Esse espaço reservado está vinculado ao fragmento Residência primária no momento do design da letra/Comunicação interativa.
   1. Faça upload do layout (e do fragmento, se houver, que usa o layout) no servidor do AEM Forms.

### Usar subformulário em um modelo XDP {#usesubformxdp}

Após analisar o layout necessário para criar a Comunicação interativa, é possível criar subformulários no modelo XDP usando o Forms Designer. Os componentes de subformulário em branco usados no modelo XDP resultam na exibição de áreas de destino no canal Imprimir da Comunicação Interativa.

>[!NOTE]
>
>Adicione conteúdo ao canal Imprimir da Comunicação interativa em vez de adicionar conteúdo ao componente de subformulário no modelo XDP. Adicione conteúdo às áreas de destino do canal de impressão usando [fragmentos de documento, gráficos, imagens](create-interactive-communication.md#step2)e fragmentos de layout.

Execute as seguintes etapas para usar um subformulário em um modelo XDP:

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Usar um formulário em branco**, toque em **Próximo** e toque em **Concluir** para abrir o formulário para criação de template.

   Certifique-se de que **Biblioteca de objetos** e **Objeto** são selecionadas da variável **Window** menu.

1. Arraste e solte a **Subformulário** do **Biblioteca de objetos** ao formulário.

   ![Designer de componentes](assets/subform_component_designer_new.png)

1. Selecione o subformulário para exibir as opções do subformulário na **Objeto** no painel direito.
1. Selecione o **Subformulário** e selecione **Fluxo** do **Conteúdo** lista suspensa. Arraste o ponto de extremidade esquerdo do subformulário para ajustar o comprimento.

   ![Subformulário Fluxo](assets/object_subform_flowed_new.png)

1. No **Vínculo** guia :

   1. Especifique um nome para o subformulário no **Nome** campo.
   1. Selecionar **Sem vínculo de dados** do **Vínculo de dados** lista suspensa.

1. Da mesma forma, selecione o subformulário raiz no painel esquerdo.

   ![Subformulário raiz](assets/root_subform_designer_new.png)

1. Selecione o **Subformulário** e selecione **Fluxo** do **Conteúdo** lista suspensa. No **Ligações** guia :

   1. Especifique um nome para o subformulário no **Nome** campo.
   1. Selecionar **Sem vínculo de dados** do **Vínculo de dados** lista suspensa.

   Repita as etapas de 2 a 5 para adicionar mais subformulários ao modelo XDP. Adicionar [texto, fragmentos de documento, imagens e gráficos](create-interactive-communication.md#step2) para as áreas de destino somente durante a criação da Comunicação interativa.

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local para salvar o arquivo e especifique um nome para o modelo XDP.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.

### Usar o componente Campo de imagem em um modelo XDP {#use-image-field-component-in-an-xdp-template}

Use o campo de imagem ou o componente Subformulário no modelo XDP e adicione uma imagem ao criar a Comunicação interativa.

>[!NOTE]
>
>Adicione uma imagem ao canal Imprimir da Comunicação interativa em vez de adicionar uma imagem ao componente Campo de imagem ou Subformulário no modelo XDP. Para obter mais informações, consulte [Adicionar conteúdo à comunicação interativa](../../forms/using/create-interactive-communication.md#step2).

Execute as seguintes etapas para usar o componente Campo de imagem em um modelo XDP:

1. Arraste e solte a **Campo de imagem** do **Biblioteca de objetos** ao formulário.
1. Selecione o subformulário para exibir as opções do subformulário na **Objeto** no painel direito.
1. No **Vínculo** guia :

   1. Especifique um nome para o campo de imagem no **Nome** campo.
   1. Selecionar **Sem vínculo de dados** do **Vínculo de dados** lista suspensa.

### Criar modelo XDP para fragmentos de layout {#xdplayoutfragments}

Use o componente Tabela no Forms Designer para criar fragmentos de layout e depois usá-los para criar tabelas enquanto cria o canal Imprimir de Comunicação Interativa. O uso de fragmentos de layout para criar tabelas garante que o conteúdo da tabela retenha a estrutura quando o canal da Web for gerado automaticamente usando o canal de impressão.

>[!NOTE]
>
>Insira o texto nas células da tabela ou [criar vínculo com os objetos do modelo de dados de formulário](create-interactive-communication.md#step2) somente durante a criação da comunicação interativa.

Execute as seguintes etapas para usar o componente Tabela no modelo XDP usando o Forms Designer:

1. Arraste e solte a **Tabela** do **Biblioteca de objetos** ao formulário.
1. No **Inserir tabela** caixa de diálogo:

   1. Especifique o número de linhas e colunas para a tabela.
   1. Selecione o **Incluir linha do cabeçalho na tabela** caixa de seleção para incluir uma linha para o cabeçalho da tabela.
   1. Toque **OK**.

1. Toque **+** no painel esquerdo, ao lado do nome da tabela, clique com o botão direito do mouse nos nomes de células incluídos no cabeçalho e em outras linhas e selecione **Renomear objeto** para renomear as células da tabela.
1. Clique nos campos de texto do cabeçalho da tabela na **Visualização de projeto** e renomeie-as.
1. Arraste e solte a **Campo de texto** do **Biblioteca de objetos** para cada célula da tabela na **Visualização de projeto**. Execute esta etapa para poder vincular células da tabela aos objetos do modelo de dados de formulário durante a criação da Comunicação interativa.

   ![Campos de texto em uma tabela](assets/text_fields_table_new.png)

1. Selecione o nome da linha no painel esquerdo e selecione **Objeto** > **Vínculo** > **Repetir linha para cada item de dados**. Execute essa etapa para garantir que, se um vínculo for criado entre as células da tabela dessa linha com objetos de modelo de dados de formulário do tipo de coleção, a linha da tabela será repetida automaticamente para cada item de dados disponível no banco de dados.

   Insira o texto nas células da tabela ou [criar vínculo com os objetos do modelo de dados de formulário](create-interactive-communication.md#step2) somente durante a criação da comunicação interativa.

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local para salvar o arquivo e especifique o nome do modelo XDP.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.

### Fazer upload do modelo XDP no servidor do AEM Forms {#uploadxdptemplate}

Depois de criar um modelo XDP usando o Forms Designer, você deve carregá-lo no servidor AEM Forms para que o modelo fique disponível para uso ao criar a Comunicação interativa.

1. Selecionar **Forms** > **Forms &amp; Documents**.
1. Toque **Criar** > **Upload de arquivo**.
1. Navegue até o local do modelo XDP no sistema de arquivos local e toque em **Abrir** para importar o modelo XDP para o servidor do AEM Forms.

## Uso do schema {#using-schema}

Você pode usar um esquema em um layout ou fragmento de layout , mas ele não é necessário. Se você usar um schema, verifique o seguinte:

1. O layout e todos os layouts de fragmento usados em uma carta/Comunicação interativa usam o mesmo esquema da letra/Comunicação interativa.
1. Todos os campos necessários para serem preenchidos com dados estão vinculados ao esquema .

## Criação de campos relacionados {#creating-relatable-fields}

Por padrão, todos os campos são considerados relacionáveis a várias outras fontes de dados. Se o seu layout contiver quaisquer campos que não sejam relacionados a uma fonte de dados, nomeie o campo com um sufixo &quot;_int&quot; (interno); por exemplo, pageCount_int.

Um campo relativo deve:

* ser um XFA &lt;field> ou &lt;exclgroup>
* ter uma referência de vínculo XFA
* se for um &lt;exclgroup>, deve ter pelo menos um campo de botão de opção filho; caso contrário, seu tipo de valor não poderá ser determinado

Um campo relativo deve:

* tem um nome

Um campo relativo não deve:

* Incluir um sufixo &quot;_int&quot; em seu nome
* têm vínculo definido como &quot;nenhum&quot;
* ser um filho de um &lt;exclgroup> elemento

Desde que um campo relativo atenda aos critérios descritos acima, ele pode estar em qualquer local e em qualquer profundidade de aninhamento no layout. Você pode usar campos relacionados em páginas principais.

Os campos são mais flexíveis em sua configuração de layout do que os subformulários de área de destino; no entanto, elas estão vinculadas a um único tipo de valor. É possível tornar um campo grande ou configurá-lo para uma largura e altura fixas, e assim por diante. O módulo resolvido ou o resultado da regra é enviado para o campo .

## Como decidir quando usar subformulários e campos de texto {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Use um subformulário se desejar capturar vários conteúdos de módulo em um layout de fluxo vertical de cima para baixo (vários parágrafos ou imagens). O layout deve lidar com o fato de o subformulário crescer em altura para acomodar seu conteúdo. Se não for possível ter certeza de que o comprimento do conteúdo associado ao subformulário/destino nunca excede o espaço reservado para o subformulário no layout, crie o subformulário como filho dentro de um contêiner de subformulário continuado. Esse processo garante que os objetos de layout abaixo do subformulário continuem para baixo à medida que o subformulário for crescendo.

Use um campo se desejar capturar os dados do módulo ou os dados do elemento do dicionário de dados no esquema do seu layout (porque os campos estão vinculados aos dados) ou para exibir o conteúdo do módulo em uma página principal. Lembre-se de que o conteúdo de uma página principal não pode fluir com o conteúdo da página de corpo; portanto, você deve garantir que o campo de imagem seja usado como um logotipo de cabeçalho. Essa tabela fornece mais critérios para decidir quando usar um subformulário ou um campo em um layout.

<table>
 <tbody>
  <tr>
   <td><p><strong>Usar um subformulário quando</strong></p> </td>
   <td><p><strong>Usar um campo de texto ao</strong></p> </td>
  </tr>
  <tr>
   <td><p>Ele contém uma combinação de elementos, como Sobrenome e Nome</p> </td>
   <td><p>Ele contém um único elemento, como um Número de política.</p> </td>
  </tr>
  <tr>
   <td><p>Ele inclui vários parágrafos</p> </td>
   <td><p>O texto é embrulhado e justificado</p> </td>
  </tr>
  <tr>
   <td><p>Os grupos de dados repetitivos, opcionais e condicionais estão vinculados a subformulários, para reduzir o risco de erros de design que podem ocorrer se os scripts forem usados para alcançar os mesmos resultados</p> </td>
   <td><p>Elementos como o logotipo e o endereço de sua organização aparecem em todas as páginas de uma carta/comunicação interativa. Nesse caso, crie campos de formulário para esses elementos e os coloque na página principal. Se você definir o vínculo de campo como "Sem vínculo de dados", os campos no aparecerão como campos relacionados no Editor de comunicação Carta/Interativa. Se você quiser relacionar algum tipo de conteúdo a esses campos, eles deverão ter vínculo.</p> <p>Se o endereço da empresa contiver mais de uma linha de dados, use o campo de texto com a opção "Permitir linhas múltiplas" para representar o endereço no layout.</p> <p>Se o tipo de dados de um campo de texto for definido como texto sem formatação, a versão de texto sem formatação da saída do módulo será usada em vez da versão de rich text (toda a formatação será descartada). Para preservar a formatação, defina o tipo de dados do campo de texto como rich text.</p> </td>
  </tr>
  <tr>
   <td><p>O texto é continuado</p> </td>
   <td><p>Campos de texto e campos de imagem são usados em páginas principais. Páginas principais não podem usar subformulários como áreas de destino.</p> </td>
  </tr>
  <tr>
   <td><p>Os objetos são agrupados e organizados sem vincular o subformulário a um elemento de dados</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Existe um campo de texto dentro do subformulário. O subformulário pode crescer e não substituir outros objetos abaixo dele no layout.</p> </td>
   <td><p>Você precisa de acesso fácil aos seus dados no processo de publicação.</p> </td>
  </tr>
 </tbody>
</table>

## Configuração de elementos repetitivos {#setting-up-repetitive-elements}

Quando elementos como o logotipo e o endereço de sua organização forem exibidos em todas as páginas de uma carta/Comunicação interativa, crie campos de formulário para esses elementos e os coloque na página principal. Use o vínculo Nome (Nome do campo) para esses campos.

## Especificar o formato de renderização do servidor {#specify-the-server-nbsp-render-format}

Use o formato de renderização do servidor do layout para Formulário XML dinâmico; caso contrário, as letras/Comunicações interativas baseadas nesse layout não poderão ser renderizadas corretamente. Por padrão, o formato de renderização do servidor no Forms Designer é definido como Formulário XML dinâmico. Para garantir que você esteja usando o formato correto:

* No Designer, clique em **Arquivo** > **Propriedades do formulário** > **Padrões** e verifique se a configuração Renderizar/Formatar PDF está definida como Formulário XML dinâmico.
