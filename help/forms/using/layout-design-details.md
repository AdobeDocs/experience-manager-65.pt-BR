---
title: Design do layout
description: Detalhes do design de layout explica como você pode criar layouts a serem usados para suas cartas ou comunicações interativas.
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
exl-id: 9e1b0067-c7dc-4bbb-a209-d674592be858
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2171'
ht-degree: 0%

---

# Design do layout{#layout-design}

Os modelos de formulário XFA ou XDPs são os modelos para:

* [Cartas](/help/forms/using/create-letter.md)
* [Canal de impressão](/help/forms/using/web-channel-print-channel.md#printchannel) de [Comunicações interativas](/help/forms/using/interactive-communications-overview.md)

* Fragmentos de layout

Um XDP foi projetado no Adobe Forms Designer. Este artigo fornece detalhes sobre como projetar XDPs para criar correspondências/Comunicações interativas eficazes, como onde usar campos de formulário ou áreas de destino e quando usar fragmentos de layout.

## Criação de um layout para cartas ou para o canal de impressão de Comunicações Interativas {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Um layout define o layout gráfico de um canal de carta/impressão de uma comunicação interativa. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Crie o layout no designer do formulário e, quando concluído, o especialista em aplicativos o carrega no servidor AEM. Nesse local, é possível selecionar o layout ao criar um modelo de correspondência ou imprimir canal de uma comunicação interativa.

![Designer: criar um layout](assets/claimsubrogationlayout.png)

Siga estas etapas para criar layouts para letras/canais de impressão de Comunicações interativas:

1. Analise o layout e determine o conteúdo que está sendo repetido em todas as páginas; geralmente, o cabeçalho e o rodapé da página se encaixam nesta categoria. Esse conteúdo é colocado nas páginas mestras do layout. O conteúdo restante vai para o corpo das páginas do layout. Em uma jaqueta de política, o logotipo e o endereço da empresa podem ser adicionados ao cabeçalho e ao rodapé da página principal. Por exemplo, Aviso de cancelamento usa o mesmo layout.
1. Ao criar páginas de corpo, divida o conteúdo da página em seções. Cada seção é projetada como um subformulário incorporado no próprio layout ou como um layout de fragmento. Se a seção contiver tabela, modele a seção como um fragmento de layout.
1. Um layout pode ser criado da seguinte maneira:

   1. Torne cada seção um subformulário separado que contenha todos os elementos da seção.
   1. Tornar cada subformulário de seção filho do mesmo subformulário pai. O layout do subformulário pai é definido como fluxo para permitir que as seções sejam deslocadas abaixo se houver dados grandes mesclados nas seções anteriores.
   1. Seção A residência principal também pode ser reutilizada em outros layouts. Crie-o como um layout de fragmento.
   1. Seção Detalhes adicionais de interesse contém apenas dois elementos posicionados um abaixo do outro, podem conter dados grandes e foram projetados como fluídos.
   1. Outras seções contêm elementos em posições específicas para que sejam projetadas como layout posicionado.
   1. Divida uma seção em subformulários se a seção contiver elementos em posições específicas e esses elementos contiverem grandes quantidades de dados. Em seguida, organize os subformulários para alcançar o comportamento desejado.
   1. Para a seção Residência principal, adicione uma área de destino de espaço reservado. Esse espaço reservado é vinculado ao fragmento da residência principal no momento do design da carta/comunicação interativa.
   1. Faça upload do layout (e do fragmento, se houver, que usa o layout) no servidor do AEM Forms.

### Usar subformulário em um modelo XDP {#usesubformxdp}

Depois de analisar o layout necessário para criar a Comunicação interativa, é possível criar subformulários no modelo XDP usando o Forms Designer. Os componentes do subformulário em branco usados no modelo XDP resultam na exibição de áreas de destino no canal de impressão da comunicação interativa.

>[!NOTE]
>
>Adicione conteúdo ao canal de impressão da comunicação interativa em vez de adicionar conteúdo ao componente de subformulário no modelo XDP. Adicione conteúdo às áreas de destino no canal de impressão usando [fragmentos de documento, gráficos, imagens](create-interactive-communication.md#step2) e fragmentos de layout.

Execute as seguintes etapas para usar o subformulário em um modelo XDP:

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Usar um formulário em branco**, selecione **Avançar** e selecione **Concluir** para abrir o formulário para criação de modelo.

   Verifique se as opções **Biblioteca de Objetos** e **Objeto** estão selecionadas no menu **Janela**.

1. Arraste e solte o componente **Subformulário** da **Biblioteca de Objetos** no formulário.

   ![Componente Designer](assets/subform_component_designer_new.png)

1. Selecione o subformulário para exibir as opções do subformulário na janela **Objeto** no painel direito.
1. Selecione a guia **Subformulário** e selecione **Fluxo** na lista suspensa **Conteúdo**. Arraste a extremidade esquerda do subformulário para ajustar o comprimento.

   ![Subformulário com Fluxo](assets/object_subform_flowed_new.png)

1. Na guia **Associação**:

   1. Especifique um nome para o subformulário no campo **Nome**.
   1. Selecione **Nenhuma associação de dados** na lista suspensa **Associação de Dados**.

1. Da mesma forma, selecione o subformulário raiz no painel esquerdo.

   ![Subformulário raiz](assets/root_subform_designer_new.png)

1. Selecione a guia **Subformulário** e selecione **Fluxo** na lista suspensa **Conteúdo**. Na guia **Ligações**:

   1. Especifique um nome para o subformulário no campo **Nome**.
   1. Selecione **Nenhuma associação de dados** na lista suspensa **Associação de Dados**.

   Repita as etapas 2 a 5 para adicionar mais subformulários ao modelo XDP. Adicione [texto, fragmentos de documento, imagens e gráficos](create-interactive-communication.md#step2) às áreas de destino somente durante a criação da Comunicação Interativa.

1. Selecione **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local onde o arquivo será salvo e especifique um nome para o modelo XDP.
   1. Selecione **.xdp** na lista suspensa **Salvar como tipo**.

   1. Selecione **Salvar**.

### Usar o componente Campo de imagem em um modelo XDP {#use-image-field-component-in-an-xdp-template}

Use o componente Campo de imagem ou Subformulário no modelo XDP e adicione uma imagem ao criar a Comunicação interativa.

>[!NOTE]
>
>Adicione imagem ao canal de impressão da comunicação interativa em vez de adicionar imagem ao componente Campo de imagem ou Subformulário no modelo XDP. Para obter mais informações, consulte [Adicionando conteúdo à Comunicação Interativa](../../forms/using/create-interactive-communication.md#step2).

Execute as seguintes etapas para usar o componente Campo de imagem em um modelo XDP:

1. Arraste e solte o componente **Campo de Imagem** da **Biblioteca de Objetos** no formulário.
1. Selecione o subformulário para exibir as opções do subformulário na janela **Objeto** no painel direito.
1. Na guia **Associação**:

   1. Especifique um nome para o campo de imagem no campo **Nome**.
   1. Selecione **Nenhuma associação de dados** na lista suspensa **Associação de Dados**.

### Criar modelo XDP para fragmentos de layout {#xdplayoutfragments}

Use o componente Tabela no Forms Designer para criar fragmentos de layout e, em seguida, use-os para criar tabelas ao criar o canal de impressão de comunicação interativa. O uso de fragmentos de layout para criar tabelas garante que o conteúdo da tabela mantenha a estrutura quando o canal da Web for gerado automaticamente usando o canal de impressão.

>[!NOTE]
>
>Insira texto nas células da tabela ou [crie associação somente com os objetos do modelo de dados de formulário](create-interactive-communication.md#step2) durante a criação da Comunicação Interativa.

Execute as seguintes etapas para usar o componente Tabela no modelo XDP usando o Forms Designer:

1. Arraste e solte o componente **Tabela** da **Biblioteca de Objetos** no formulário.
1. Na caixa de diálogo **Inserir Tabela**:

   1. Especifique o número de linhas e colunas da tabela.
   1. Marque a caixa de seleção **Incluir linha de cabeçalho na tabela** para incluir uma linha para o cabeçalho da tabela.
   1. Selecione **OK**.

1. Selecione **+** no painel esquerdo ao lado do nome da tabela, clique com o botão direito nos nomes de células incluídos no cabeçalho e em outras linhas e selecione **Renomear Objeto** para renomear as células da tabela.
1. Clique nos campos de texto do cabeçalho da tabela na **Exibição de Design** e renomeie-os.
1. Arraste e solte o componente **Campo de Texto** da **Biblioteca de Objetos** em cada célula da tabela na **Exibição de Design**. Execute esta etapa para poder vincular células de tabela aos objetos de modelo de dados de formulário ao criar a Comunicação interativa.

   ![Campos de texto em uma tabela](assets/text_fields_table_new.png)

1. Selecione o nome da linha no painel esquerdo e selecione **Objeto** > **Associação** > **Repetir Linha para Cada Item de Dados**. Execute esta etapa para garantir que, se uma associação for criada entre as células desta linha com objetos de modelo de dados de formulário do tipo coleção, a linha da tabela será repetida automaticamente para cada item de dados disponível no banco de dados.

   Insira texto nas células da tabela ou [crie associação somente com os objetos do modelo de dados de formulário](create-interactive-communication.md#step2) durante a criação da Comunicação Interativa.

1. Selecione **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local onde o arquivo será salvo e especifique o nome do modelo XDP.
   1. Selecione **.xdp** na lista suspensa **Salvar como tipo**.

   1. Selecione **Salvar**.

### Fazer upload do modelo XDP para o servidor do AEM Forms {#uploadxdptemplate}

Depois de criar um modelo XDP usando o Forms Designer, você deve carregá-lo no servidor do AEM Forms para que o modelo fique disponível para uso ao criar a Comunicação interativa.

1. Selecione **Forms** > **Forms e Documentos**.
1. Selecione **Criar** > **Carregar arquivo**.
1. Navegue até o local do modelo XDP no sistema de arquivos local e selecione **Abrir** para importar o modelo XDP para o servidor do AEM Forms.

## Uso do schema {#using-schema}

Você pode usar um esquema em um layout ou fragmento de layout, mas isso não é obrigatório. Se você usar um schema, certifique-se do seguinte:

1. O layout e todos os layouts do fragmento usados em uma correspondência/comunicação interativa usam o mesmo esquema que a correspondência/comunicação interativa.
1. Todos os campos que devem ser preenchidos com dados são vinculados ao esquema.

## Criação de campos relacionáveis {#creating-relatable-fields}

Por padrão, todos os campos são considerados relacionáveis a várias outras fontes de dados. Se o layout contiver campos que não sejam relacionados a uma fonte de dados, nomeie o campo com um sufixo &quot;_int&quot; (interno); por exemplo, pageCount_int.

Um campo relacionável deve:

* ser um &lt;field> ou &lt;exclGroup> XFA
* têm uma referência de vinculação XFA
* se for um &lt;exclGroup>, deverá ter pelo menos um campo de botão de opção filho; caso contrário, seu tipo de valor não poderá ser determinado

Um campo relacionável deve:

* tem um nome

Um campo relacionável não deve:

* Incluir um sufixo &quot;_int&quot; em seu nome
* têm a vinculação definida como &quot;nenhum&quot;
* ser filho de um elemento &lt;exclGroup>

Desde que um campo relacionável atenda aos critérios descritos acima, ele pode estar em qualquer local e em qualquer profundidade de aninhamento no layout. Você pode usar campos relacionáveis nas páginas-mestre.

Os campos são mais flexíveis em sua configuração de layout do que os subformulários de área de destino; no entanto, estão vinculados a um único tipo de valor. Você pode tornar um campo grande ou defini-lo como uma largura e altura fixas, e assim por diante. O módulo resolvido ou o resultado da regra é enviado para o campo.

## Decisão sobre quando usar subformulários e campos de texto {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Use um subformulário se desejar capturar vários conteúdos do módulo em um layout de fluxo vertical de cima para baixo (vários parágrafos ou imagens). Seu layout deve lidar com o fato de que o subformulário cresce em altura para acomodar seu conteúdo. Se não puder ter certeza de que o comprimento do conteúdo associado ao subformulário/destino nunca excede o espaço reservado para o subformulário no layout, crie o subformulário como filho em um contêiner de subformulário fluído. Esse processo garante que os objetos de layout abaixo do subformulário fluam para baixo à medida que o subformulário cresce.

Use um campo se quiser capturar os dados do módulo ou os dados do elemento do dicionário de dados no esquema do layout (porque os campos estão vinculados aos dados) ou exibir o conteúdo do módulo em uma página-mestre. Lembre-se de que o conteúdo de uma página-mestre não pode fluir com o conteúdo da página de corpo, portanto, é necessário garantir que o campo de imagem seja usado como logotipo do cabeçalho. Esta tabela fornece mais critérios para decidir quando usar um subformulário ou um campo em um layout.

<table>
 <tbody>
  <tr>
   <td><p><strong>Usar um subformulário quando</strong></p> </td>
   <td><p><strong>Usar um campo de texto quando</strong></p> </td>
  </tr>
  <tr>
   <td><p>Ela contém uma combinação de elementos, como um Sobrenome e um Nome</p> </td>
   <td><p>Ele contém um único elemento, como um Número de política.</p> </td>
  </tr>
  <tr>
   <td><p>Inclui vários parágrafos</p> </td>
   <td><p>O texto está quebrado e justificado</p> </td>
  </tr>
  <tr>
   <td><p>Os grupos de dados repetitivos, opcionais e condicionais são vinculados aos subformulários para reduzir o risco de erros de design que podem ocorrer se os scripts forem usados para atingir os mesmos resultados</p> </td>
   <td><p>Elementos como o logotipo e o endereço de sua organização são exibidos em todas as páginas de uma correspondência/Comunicação interativa. Nesse caso, crie campos de formulário para esses elementos e coloque-os na página mestre. Se você definir a vinculação de campo como "Sem vinculação de dados", os campos não aparecerão como campos relacionáveis no Editor de carta/comunicação interativa. Se você quiser relacionar algum tipo de conteúdo a esses campos, eles devem ter vinculação.</p> <p>Se o endereço da sua empresa contiver mais de uma linha de dados, use o campo de texto com a opção "Permitir várias linhas" para representar o endereço no layout.</p> <p>Se o tipo de dados de um campo de texto for definido como texto sem formatação, a versão de texto sem formatação da saída do módulo será usada em vez da versão de rich text (toda a formatação será descartada). Para preservar a formatação, defina o tipo de dados do campo de texto como rich text.</p> </td>
  </tr>
  <tr>
   <td><p>O texto flui</p> </td>
   <td><p>Campos de texto e de imagem são usados em páginas-mestre. Páginas-mestre não podem usar subformulários como áreas de destino.</p> </td>
  </tr>
  <tr>
   <td><p>Os objetos são agrupados e organizados sem vincular o subformulário a um elemento de dados</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Há um campo de texto dentro do subformulário. O subformulário pode crescer e não substituir outros objetos abaixo dele no layout.</p> </td>
   <td><p>Você precisa de acesso fácil aos dados no pós-processo.</p> </td>
  </tr>
 </tbody>
</table>

## Configurar elementos repetitivos {#setting-up-repetitive-elements}

Quando elementos como o logotipo e o endereço de sua organização aparecem em todas as páginas de uma correspondência/comunicação interativa, crie campos de formulário para esses elementos e coloque-os na página principal. Use a vinculação de Nome (Nome do campo) para esses campos.

## Especificar o formato de renderização do servidor {#specify-the-server-nbsp-render-format}

Use o formato de renderização do servidor do layout para o Formulário XML Dinâmico; caso contrário, quaisquer letras/Comunicações interativas baseadas nesse layout não poderão ser renderizadas corretamente. Por padrão, o formato de renderização do servidor no Forms Designer é definido como Formulário XML dinâmico. Para garantir que você esteja usando o formato correto:

* No Designer, clique em **Arquivo** > **Propriedades do Formulário** > **Padrões** e verifique se a configuração Renderizar/Formatar PDF está definida como Formulário XML Dinâmico.
