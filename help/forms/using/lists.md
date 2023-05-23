---
title: Fragmentos de documento no AEM
description: Fragmentos de documento, como Texto, listas, condições e fragmentos de layout, no Gerenciamento de correspondência permitem formar os componentes estáticos, dinâmicos e repetíveis de correspondência do cliente.
uuid: 4273323d-14f5-4b3b-8fed-80beef641efe
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d5436c6-1976-496c-b9a7-7dc6e830bb5d
docset: aem65
feature: Correspondence Management
exl-id: 71754e41-45d7-4cc5-ba49-0748bd51c0cf
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '6908'
ht-degree: 0%

---

# Fragmentos do documento{#document-fragments}

## Fragmentos do documento {#document-fragments-1}

Os fragmentos de documento são partes/componentes reutilizáveis de uma correspondência usando a qual você pode compor cartas/correspondência. Os fragmentos de documento são dos seguintes tipos:

* **Texto**: um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.
* **Lista**: Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens. A ordem dos elementos da lista pode ser fixa ou editável. Ao criar uma correspondência, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos.
* **Condição**: As condições permitem definir qual conteúdo é incluído no momento da criação da correspondência, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. Uma variável de controle pode ser um elemento do dicionário de dados ou um espaço reservado.
* **Fragmento de layout**: um fragmento de layout é um layout que pode ser usado com uma ou mais letras. Um fragmento de layout é usado para criar padrões repetíveis, especialmente tabelas dinâmicas. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Os layouts (XDPs) são criados no Designer e, em seguida, são carregados no AEM Forms.

## Texto {#text}

Um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico. Um parágrafo dinâmico contém referências a elementos de dados, cujos valores são fornecidos em tempo de execução. Por exemplo, o nome do cliente em uma saudação de correspondência pode ser um elemento de dados dinâmico, com seu valor disponibilizado no tempo de execução. Ao alterar esses valores, o mesmo modelo de correspondência pode ser usado para gerar cartas para clientes diferentes.

A Solução de gerenciamento de correspondência é compatível com dois tipos de itens de dados dinâmicos (dados variáveis):

* **Elementos do dicionário de dados**: esses elementos são vinculados ao dicionário de dados e obtêm seus valores da fonte de dados fornecida. Uma variável do dicionário de dados pode ser protegida ou desprotegida. Durante a criação de correspondência, o usuário pode modificar o valor padrão de variáveis desprotegidas do dicionário de dados, mas não pode modificar as protegidas.
* **Espaços reservados**: essas são variáveis que não estão vinculadas a uma fonte de dados de back-end. Eles exigem que o usuário preencha um valor durante a criação da correspondência. Os espaços reservados são desprotegidos por padrão.

>[!NOTE]
>
>Os modelos do Gerenciamento de correspondências não forçam a criação de nomes exclusivos ao criar espaços reservados. Se você criar dois espaços reservados com o mesmo nome, como um texto e uma condição, e usá-los em um modelo de correspondência, os valores do último espaço reservado inserido serão usados para ambos os espaços reservados. Se dois espaços reservados tiverem o mesmo nome, seus tipos serão comparados. Se os tipos forem diferentes, seu tipo se tornará String. No entanto, em um módulo, não é possível criar vários espaços reservados com o mesmo nome.

### Criar texto {#create-text}

1. Selecionar **Forms** > **Fragmentos do documento**.
1. Toque **Criar** > **Texto** Ou selecione um ativo de texto e toque em **Editar**.
1. Especifique as seguintes informações para o texto:

   * **Título: (opcional)** Insira o título do ativo de texto. Os títulos não precisam ser exclusivos e podem ter caracteres especiais e caracteres que não estejam em inglês. Os textos são referenciados por seus títulos (quando disponíveis), como em miniaturas e propriedades de ativos.
   * **Nome:** O nome exclusivo do ativo de texto. Não pode haver dois ativos (texto, condição ou lista) em nenhum estado com o mesmo nome. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título. Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.
   * **Descrição**: digite uma descrição do ativo.
   * **Dicionário de dados**: Opcionalmente, selecione o dicionário de dados para mapear. Esse atributo permite adicionar referências aos elementos do dicionário de dados no ativo de texto.
   * **Tags**: Opcionalmente, para criar uma tag personalizada, insira o valor no campo de texto e pressione Enter. Você pode ver sua tag abaixo do campo de texto das tags. Quando você salva esse texto, as tags recém-adicionadas também são criadas.

1. Toque **Próxima**. O Gerenciamento de correspondência exibe a página Editor, onde você pode adicionar parágrafos de texto e elementos de dados ao texto.

   O verificador ortográfico padrão do navegador verifica a ortografia no editor de texto. Para gerenciar a verificação ortográfica e gramatical, você pode editar as configurações do verificador ortográfico do navegador ou instalar plug-ins/complementos do navegador para verificar a ortografia e a gramática.

   Você também pode usar os vários atalhos de teclado no editor de texto para gerenciar, editar e formatar texto. Para obter mais informações sobre [Editor de texto](/help/forms/using/keyboard-shortcuts.md#p-formatting-p) atalhos de teclado no Gerenciamento de correspondências Atalhos de teclado.

1. Um editor de texto é aberto, insira o texto. Use a barra de ferramentas na parte superior da página para formatar o texto, inserir condições, links e quebras de página.

   ![Barra de ferramentas](assets/advancedediting.png)

   * **Link**: Inserir [hipertexto](#insert-hyperlink) no texto.
   * **Repetir**: A repetição imprime o elemento de coleção no Dicionário de dados usando um delimitador.
   * **Condição**: Toque para inserir uma condição. Inserir texto com base na condição. Se a condição for verdadeira, o texto será visível na letra; caso contrário, não será.
   * **Adicionar descrição**: adiciona uma anotação a um pedaço de texto. Esses metadados são visíveis para o Autor, mas não são parte da carta criada.
   * **Quebra de página**: se você definir o atributo de quebra de página de um módulo de texto como false, o módulo de texto não será quebrado entre páginas.

   Um editor de texto é aberto. Insira o texto. A barra de ferramentas muda dependendo do tipo de edição que você escolher fazer: Parágrafo, Alinhamento ou Listagem:

   ![Selecionar tipo de barra de ferramentas](assets/toolbarselection.png)

   Selecione o tipo de barra de ferramentas: Parágrafo, Alinhamento ou Listagem

   ![Barra de ferramentas Parágrafo](assets/fonteditingtoolbar.png)

   Barra de ferramentas Parágrafo
   [ ![Barra de ferramentas Alinhamento](assets/paragrapheditingtoolbar.png)](assets/paragrapheditingtoolbar-1.png)Barra de ferramentas Alinhamento

   ![Barra de ferramentas Listagem](assets/bulleteditingtoolbar.png)

   Barra de ferramentas de listagem (clique para abrir a imagem em tamanho real)

1. Para reutilizar um ou mais parágrafos de texto existentes em outro aplicativo, como páginas do MS Word ou HTML, copie e cole o texto no editor de texto. A formatação do texto copiado é mantida no editor de texto.

   Você pode copiar e colar um ou mais parágrafos de texto em um módulo de texto editável. Por exemplo, você pode ter um documento do MS Word com uma lista com marcadores de provas de residência aceitáveis, como as seguintes:

   ![pastetextmsword-1](assets/pastetextmsword-1.png)

   Você pode copiar e colar diretamente o texto do documento do MS Word em um módulo de texto editável. A formatação, como lista com marcadores, fonte e cor do texto, é mantida no módulo de texto.

   ![pastetexttextmodule](assets/pastetexttextmodule.png)

   >[!NOTE]
   >
   >A formatação do texto colado, no entanto, tem alguns [limitações](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

1. Se necessário, insira caracteres especiais no fragmento do documento. Por exemplo, você pode usar a paleta Caracteres especiais para inserir:

   * Símbolos de moeda, como €,¥ e £
   * Símbolos matemáticos como ∑, √, ‖ e ^
   * Símbolos de pontuação, como ‟ e &quot;

   ![caracteres especiais-1](assets/specialcharacters-1.png)

   O Gerenciamento de correspondências incorporou suporte para 210 caracteres especiais. O administrador pode [adicionar suporte para mais caracteres especiais/personalizados por personalização](/help/forms/using/custom-special-characters.md).

1. Para destacar\enfatizar partes do texto em um módulo incorporado editável, selecione o texto e toque em Realçar cor.

   ![textbackgroundcolorplied](assets/textbackgroundcolorapplied.png)

   Você pode tocar diretamente em uma cor básica `**[A]**` presente na paleta Cores básicas ou toque em **Selecionar** depois de usar o controle deslizante `**[B]**` para escolher o tom apropriado da cor.

   Como opção, você também pode ir para a guia Avançado para selecionar o Matiz, a Luminosidade e a Saturação apropriados `**[C]**` para criar a cor precisa e, em seguida, toque em Selecionar `**[D]**` para aplicar a cor para realçar o texto.

   ![textbackgroundcolor-1](assets/textbackgroundcolor-1.png)

1. No painel de dados, arraste e solte os elementos do dicionário de dados e os elementos do espaço reservado no texto.

   Para:

   * Adicione um elemento do dicionário de dados no texto, selecione um elemento de dados na lista e toque em Inserir ( ![inserir](assets/insert.png)). Se você selecionar Protegido, o elemento do dicionário de dados será somente leitura e aparecerá no editor de correspondências, mas não na interface do usuário Criar correspondência ou no Criador de correspondência.
   * Adicione um elemento de espaço reservado no texto, no painel Elementos de dados, toque em Criar novo, insira os detalhes do novo Elemento de dados e toque em Criar para adicionar o novo elemento à lista. O novo espaço reservado pode ser inserido no texto da mesma forma que o elemento do dicionário de dados. Para editar um espaço reservado, selecione-o e toque em Editar.

   ![Elementos de espaço reservado](assets/placeholder_elements_in_xmldata.png)

   Elementos de espaço reservado conforme especificado no arquivo de dados de amostra de um dicionário de dados

   ![Elementos de espaço reservado na carta](assets/placeholder_elements_in_text.png)

   Os valores do elemento de espaço reservado na visualização CCR são preenchidos a partir das variáveis do Dicionário de dados, conforme especificado no arquivo de dados de amostra

   Você também pode usar o símbolo @ para pesquisar e adicionar elementos de dicionário de dados e espaço reservado ao editor de texto. Coloque o cursor onde deseja inserir o elemento. Digite @ seguido pela sequência de pesquisa. O editor de texto executa a operação de pesquisa em todos os elementos de dicionário de dados e espaço reservado disponíveis no fragmento do documento de texto. A operação de pesquisa recupera e exibe os elementos que contêm a string de pesquisa como uma lista suspensa. Navegue pelos resultados da pesquisa e clique no elemento que deseja inserir no local do cursor. Pressione Esc para ocultar os resultados da pesquisa.

1. Você pode usar condições em linha e repetir para tornar sua carta altamente contextual e bem estruturada. Para obter mais informações sobre condição em linha e repetição, consulte [Condições em linha e repetir em letras](/help/forms/using/cm-inline-condition.md).
1. Toque **Salvar**.

#### Inserir hiperlink em um texto {#insert-hyperlink}

Execute as seguintes etapas para criar um hiperlink em um ativo de texto:

1. Selecione o texto ou o objeto de modelo de dados no editor de texto.

2. Toque **[!UICONTROL Link]**. Toque **[!UICONTROL Texto Alternativo]** para remover o nome ou texto do objeto de modelo de dados existente.

3. Especifique o URL e toque em ![Salvar](assets/save_icon.svg).

![Criar hiperlink no ativo de texto](assets/text-create-hyperlink.png)

#### Pesquisa e substituição de texto {#searching-and-replacing-text}

Ao trabalhar com elementos de texto contendo um corpo de texto grande, é necessário procurar uma string de texto específica. Talvez também seja necessário substituir uma sequência específica de texto por uma sequência alternativa.

O recurso Localizar e substituir permite procurar (e substituir) qualquer cadeia de caracteres de texto em um elemento de texto. O recurso também inclui uma pesquisa avançada de expressão regular.

#### Para pesquisar texto em um módulo de texto {#to-search-text-in-a-text-module}

1. Abra o módulo de texto no editor de texto.

1. Toque em Localizar e substituir.
1. Insira o texto a ser pesquisado na caixa de texto Localizar e pressione Localizar. O texto de pesquisa é destacado no módulo de texto.
1. Para procurar a próxima instância do texto, pressione Localizar novamente.

   Se você continuar pressionando o botão Localizar, a pesquisa continuará na página. Depois que a última instância do texto for encontrada, a mensagem **Atingiu o fim do módulo** indica que não foram encontrados mais resultados de pesquisa.

   No entanto, se nenhuma instância do texto de pesquisa for encontrada no módulo de texto, a mensagem exibida será: **Correspondência não encontrada**.

1. Se você pressionar Localizar novamente, a pesquisa continuará na parte superior da página.

#### Opções de pesquisa {#search-options}

**Diferenciar maiúsculas de minúsculas:** A pesquisa retorna resultados somente com letra maiúscula ou minúscula.

**Palavra inteira:** A pesquisa retorna somente palavras inteiras.

>[!NOTE]
>
>Se você inserir qualquer caractere especial na caixa de texto Localizar, a opção Palavra inteira será desativada.

**Reg ex:** Pesquisar usando expressões regulares. Por exemplo, a seguinte expressão regular pesquisa endereços de email em um módulo de texto:

`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}`

#### Para pesquisar e substituir texto em um módulo de texto {#to-search-and-replace-text-in-a-text-module}

1. Abra o módulo de texto no editor de texto.
1. Toque em Localizar e substituir.
1. Digite o texto a ser pesquisado na caixa de texto Localizar e o texto a ser substituído pelo texto localizado e pressione Substituir.
1. Se o texto de pesquisa for encontrado, ele será substituído pelo texto Substituir.

   * Se outra instância do texto de pesquisa for encontrada, essa instância será realçada no módulo de texto. Se você pressionar Substituir novamente, a instância destacada será substituída e o cursor avançará, se uma terceira instância for encontrada.
   * Se outra instância não for encontrada, o cursor pára na última instância substituída.

1. Se você pressionar Localizar novamente, a pesquisa continuará na parte superior da página.

   Use a opção Substituir tudo para substituir todas as instâncias de um texto no módulo de texto. Quando você usar &quot;, o número de substituições é exibido como uma mensagem na caixa de diálogo Localizar e substituir.

#### Práticas recomendadas/dicas e truques para módulos de texto {#best-practices-tips-and-tricks-for-text-modules}

* Use uma convenção de nomenclatura consistente para evitar duplicação.
* Use a vinculação apropriada do dicionário de dados em módulos de texto.
* As seguintes regras se aplicam ao usar o Editor de texto ao alterar um ativo de texto:

   * **Adição da variável:** Permitido
   * **Remoção da variável:** Permitido
   * **Atualização das propriedades:** Permitido
   * **Alteração do dicionário de dados:** Permitido até que o elemento do dicionário de dados não seja usado. Não é possível alterar o dicionário de dados na atualização.

## Lista {#list}

Uma lista é um grupo de fragmentos de documento, incluindo texto, (outras) listas, condições e imagens. A ordem dos elementos da lista pode ser fixa ou editável. Ao criar uma correspondência, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos. As listas se comportam basicamente como alvos que podem ser aninhados dentro de outros alvos.

### Listas de implementação {#implementing-lists}

As listas de implementação consistem em duas etapas:

1. Definição de propriedades principais, como nome, descrição e dicionário de dados.
1. Seção do conteúdo que faz parte da lista e definição de propriedades como ordem de bloqueio e acesso à biblioteca para a lista.

### Criar uma lista {#create-a-list}

Uma lista é um grupo de conteúdo relacionado que pode ser usado em um modelo de correspondência como uma única unidade. Qualquer tipo de conteúdo pode ser adicionado a uma lista. As listas também podem ser aninhadas. Os módulos de lista podem ser especificados como:

* **SOLICITADO**: a ordem não pode ser alterada no tempo de execução Criar correspondência.
* **Acesso à biblioteca**: os usuários podem adicionar módulos à lista. Esse sinalizador especifica se o acesso à biblioteca está ativado. Se ativado (aberto), o usuário pode adicionar módulos à lista ao visualizar a correspondência.
* Ao criar uma lista, você pode especificar um tipo, como:
* **Simples**: Nenhuma formatação de estilo adicional é aplicada à lista.
* **Com marcadores**: uma lista formatada com um marcador simples.
* **Numerado**: uma lista numérica com a opção de numerais Padrão (1,2,...), Romano Superior (I, II, ...) e Romano Inferior (i, ii,...).
* **Letterado**: uma lista alfabética com a opção de letras minúsculas (a,b,...) e maiúsculas (A,B,...).
* **Personalizado**: você pode criar qualquer tipo Numerado/Letterado e valores de prefixo e sufixo de sua escolha.

1. Selecionar **Forms** > **Fragmentos do documento**.

1. Selecionar **Criar** > **Lista**.

1. Especifique as seguintes informações para a lista:

   * **Título (opcional): insira** o título da lista. O título não precisa ser exclusivo e pode ter caracteres especiais e caracteres que não estejam em inglês. As listas são referenciadas por seus títulos (quando disponíveis), como em miniaturas e propriedades de ativos.
   * **Nome:** O nome exclusivo da lista. Não pode haver dois ativos (texto, condição ou lista) em nenhum estado com o mesmo nome. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com o valor no campo Título. Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.
   * **Descrição (opcional)**: digite uma descrição do ativo.
   * **Dicionário de dados (opcional)**: Opcionalmente, selecione o dicionário de dados ao qual deseja se conectar. Somente ativos que usam o mesmo dicionário de dados que a lista, ou ativos que não têm um dicionário de dados atribuído, podem ser adicionados à lista. Atribuir um dicionário de dados a uma lista facilita que a pessoa que cria um modelo de correspondência encontre a lista apropriada.
   * **Tags (opcional)**: selecione as tags a serem aplicadas. Você também pode digitar o nome de uma nova tag e criá-la. (A nova tag é criada ao tocar em **Salvar**.)

1. Toque **Próxima**.
1. Toque **Adicionar ativo**.
1. Para adicionar ativos à lista, selecione-os na página Selecionar ativos e toque em **Concluído**.

   ![Selecionar ativos para adicionar à lista](assets/selectassets.png)

1. Os ativos são adicionados à página Itens de lista.
Para alterar a ordem dos ativos na lista, toque e segure o ícone de setas ( ![arrastar e soltar](assets/dragndrop.png) ) e arrastar e soltar. Quando o usuário abre um modelo de correspondência na interface do usuário Criar correspondência, o conteúdo é montado na ordem definida aqui.

   ![Reordenar e configurar ativos em uma lista](assets/listitems.png)

1. Você pode selecionar as seguintes opções para especificar como a lista se comporta na interface do usuário do CCR:

   * **Acesso à biblioteca**: para ativar o acesso à biblioteca para adicionar ativos, toque em Acesso à biblioteca. Quando o Acesso à biblioteca está ativado, o ajustador de declarações pode adicionar mais conteúdo à lista. Caso contrário, o Ajustador de Declarações estará limitado ao conteúdo definido para a lista.
   * **Bloquear ordem**: para bloquear a ordem dos ativos na lista de modo que o Ajuste de Declarações não possa alterar a ordem, toque em Bloquear ordem. Se você não selecionar esta opção, o Ajuste de Reivindicações poderá alterar a ordem dos itens da lista.

   * **Adicionar marcadores**: use essa opção para aplicar um estilo de marcador ou numeração ao módulo. Você pode usar um estilo de lista pré-criado ou um personalizado. Você também pode especificar o texto a ser exibido antes e depois de cada um dos itens da lista.
   * **Quebra de página**: selecione esta opção ( ![interrupção](assets/break.png)) para adicionar uma quebra de página entre o conteúdo da lista. Quando esta opção não está selecionada ( ![nobreak](assets/nobreak.png)), se o conteúdo da lista estiver estourando para a próxima página, a lista inteira será deslocada para a próxima página em vez de quebrar na página entre a lista.

   * **Configuração da atribuição**: use essa opção para especificar o número mínimo e máximo de ativos que podem ser adicionados à lista.

1. Você pode selecionar as seguintes opções para especificar como cada ativo na lista se comporta no tempo de execução:

   * **Editável:** Quando essa opção é selecionada, o conteúdo pode ser editado na interface do usuário Criar correspondência. (Essa opção não está disponível para os módulos Lista e Imagem.)
   * **Obrigatório:** Quando essa opção é selecionada, o conteúdo é necessário na interface do usuário Criar correspondência.
   * **Selecionado:** Quando essa opção é selecionada, o conteúdo é pré-selecionado na interface do usuário Criar correspondência.
   * **Ignorar estilo:** Quando essa opção é selecionada, o conteúdo ignora marcadores e numeração na interface do usuário Criar correspondência. (Essa opção não está disponível para módulos de Imagem. Além disso, entre Ignorar estilo, Composto e Ignorar estilo de lista, apenas uma das opções pode ser aplicada a um módulo. Uma dessas opções pode ser usada para um módulo ao selecionar Adicionar marcadores para um módulo.)
   * **Recuo:** É possível alterar o nível de recuo de cada módulo/conteúdo selecionado como parte da Lista. O recuo é especificado em termos de Níveis (começando com zero), de modo que cada nível de recuo corresponde a um preenchimento de 36 pontos.
   * **Composto:** Quando selecionada, a numeração composta é aplicada como uma combinação do estilo da Lista externa (principal) e seu próprio estilo. A numeração composta nessa Lista aninhada é baseada na ordem em que essa Lista aninhada aparece na Lista externa.
   * **Ignorar estilo de lista:** Se a opção &#39;Numeração composta&#39; estiver desmarcada, a opção &#39;Ignorar estilo de lista&#39; será ativada. Essa seleção ignora o próprio estilo da Lista aninhada e a numeração continua a partir da Lista externa. Portanto, os módulos da lista aninhada são tratados como parte da própria lista externa, desconsiderando quaisquer estilos especificados na Lista aninhada. Se a opção Ignorar estilo de lista estiver desmarcada em uma Lista aninhada, os módulos que fazem parte dessa Lista aninhada terão seu próprio estilo de numeração.
   * **Manter com o próximo:** Define a quebra de página dos ativos contidos em uma lista. Se você definir a propriedade Manter com o próximo de um ativo de uma lista como **Ligado**, esse ativo e o próximo ativo permanecem na mesma página. Isso implica que o conteúdo do ativo selecionado e do próximo ativo não quebrarão entre páginas.

1. Toque **Salvar**.

### Práticas recomendadas/dicas e truques {#best-practices-tips-and-tricks}

* Use uma convenção de nomenclatura consistente para evitar duplicação.
* Usar a vinculação de dicionário de dados apropriada
* As seguintes regras se aplicam ao usar o Editor de lista para alterar uma lista:

   * Atualização de propriedades: permitido
   * **Alteração do dicionário de dados:** Permitido até que nenhum item que use o dicionário de dados seja associado a ele. Não é possível alterar o dicionário de dados na atualização.

## Condições {#conditions}

As condições permitem definir qual conteúdo será incluído no momento da criação da correspondência/carta, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. Ao adicionar uma condição, você pode optar por incluir um ativo com base no valor que a variável de controle tem.

Com base nas opções escolhidas, somente a primeira expressão que for considerada verdadeira, com base na variável de condição atual, será avaliada para todas as condições. Ao preencher a correspondência em Criar correspondência (CCR), as condições se comportam como &quot;caixas brancas&quot;. Se uma condição resultar em uma lista, todos os itens obrigatórios e pré-selecionados da lista serão gerados. Se qualquer um desses itens for condições ou uma lista por si só, o conteúdo resultante também será gerado, de cima para baixo e em primeira ordem de profundidade, como uma lista simples de texto e conteúdo de imagem. Os resultados da condição podem ser de qualquer tipo (texto, lista, condição ou imagem).

### Condições de execução {#implementing-conditions}

O Editor de condições vem com uma [Construtor de expressões](/help/forms/using/expression-builder.md) A interface do usuário do que permite a criação de expressões usando vários espaços reservados e elementos do Dicionário de dados. Você pode usar operandos comuns e funções locais / globais em tais expressões. Cada expressão pode ser associada a algum conteúdo e, opcionalmente, pode haver uma seção padrão se nenhuma das expressões for avaliada como verdadeira. Todas as expressões são avaliadas na sequência em que são definidas, e as primeiras expressões que retornam true são selecionadas e seu conteúdo associado é retornado por esse módulo condicional.

Por exemplo, se o texto dos termos e condições em uma correspondência for diferente dependendo do estado em que o cliente está e o dicionário de dados contiver um elemento chamado &quot;estado&quot;, você poderá adicionar a condição da seguinte maneira:
* state = NY, selecione T&amp;C_NY parágrafo de texto
* state = NC, selecione parágrafo de texto T&amp;C_NC

O Editor de condições permite especificar uma condição padrão. Se o valor das variáveis de controle não corresponder a nenhuma das condições, o conteúdo associado à condição padrão será usado. Seguindo o exemplo anterior, você poderia adicionar esta linha de condição:
* Por padrão, selecione T&amp;C_Rest

### Criar uma condição {#create-a-condition}

1. Selecionar **Forms** > **Fragmentos do documento**.
1. Selecionar **Criar > Condição**.
1. Especifique as seguintes informações para a lista:

   * **Título (opcional):** Insira o título da condição. O título não precisa ser exclusivo e pode ter caracteres especiais e caracteres que não estejam em inglês. As condições são referenciadas por seus títulos (quando disponíveis), como em miniaturas e propriedades de ativos.
   * **Nome:** O nome exclusivo da condição. Não pode haver dois ativos (texto, condição ou lista) em nenhum estado com o mesmo nome. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título. Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.
   * **Descrição (opcional)** Digite uma descrição da condição.
   * **Dicionário de dados (opcional)**: Opcionalmente, selecione o dicionário de dados ao qual deseja se conectar. Somente os ativos que usam o mesmo dicionário de dados que a condição ou os ativos que não têm um dicionário de dados atribuído podem ser adicionados à lista. Atribuir um dicionário de dados a uma lista facilita para a pessoa que está criando um modelo de correspondência encontrar a condição apropriada.
   * **Tags (opcional)**: como opção, selecione as tags a serem aplicadas. Você também pode digitar o nome de uma nova tag e criá-la. (A nova tag é criada ao tocar em **Salvar**.)

1. Toque **Próxima**.
1. Toque **Adicionar ativo**.
1. Para adicionar um ativo à Condição, selecione-o na página Selecionar ativos e toque em **Concluído**. Os ativos são adicionados ao painel Expressão.
1. Você pode selecionar as seguintes opções para especificar como a condição se comporta no tempo de execução:

   * **Desativar a avaliação de resultados múltiplos\Ativar a avaliação de resultados múltiplos**: quando essa opção está ativada (aparece como &quot;Ativar várias...&quot;), todas as condições são avaliadas e o resultado é a soma de todas as condições verdadeiras. Se essa opção estiver desativada (aparecer como &quot;Desativar várias...&quot;), então somente a primeira condição que for considerada verdadeira será avaliada e se tornará a saída da condição.
   * **Quebra de página**: selecione esta opção ( ![interrupção](assets/break.png)) para adicionar uma quebra de página entre os módulos das condições. Quando esta opção não está selecionada ( ![nobreak](assets/nobreak.png)), se uma condição estiver transbordando para a próxima página, a condição inteira será deslocada para a próxima página em vez de quebrar na página entre a condição.

1. Para alterar a ordem dos ativos na condição, toque e segure o ícone de setas ( ![arrastar e soltar](assets/dragndrop.png) ) e arrastar e soltar. Quando o usuário abre um modelo de correspondência na interface do usuário Criar correspondência, o conteúdo é montado na ordem definida aqui.
1. Toque **Excluir** para excluir a linha. Se você tocar em Excluir na linha padrão, apenas as informações do ativo serão apagadas.
1. Toque **Copiar** para duplicar uma linha.
1. Toque **Editar** para alterar o ativo ou editar a expressão.

   Além disso:

   * Para atualizar o ativo, toque no ícone de pasta na coluna Ativo.
   * Para abrir o Construtor de expressões para inserir uma expressão, toque no ícone de pasta na coluna Expressão. Para obter mais informações sobre o Construtor de expressões, consulte [Construtor de expressões](/help/forms/using/expression-builder.md).

### Práticas recomendadas/dicas e truques {#best-practices-tips-and-tricks-1}

* Use uma convenção de nomenclatura consistente para facilitar a pesquisa e evitar a duplicação.
* As condições se comportam como declarações de maiúsculas e minúsculas, portanto, a ordem da condição é importante. A primeira correspondência é retornada.
* Usar a vinculação de dicionário de dados apropriada
* As seguintes regras se aplicam ao usar o Editor de condições para editar uma condição:

   * **Adição da variável:** Permitido
   * **Remoção da variável:** Permitido
   * **Atualização das propriedades:** Permitido
   * **Alteração do dicionário de dados:** Permitido até que o elemento do dicionário de dados não seja usado.

## Fragmentos de layout {#layoutfragments}

Um fragmento de layout é baseado em XDPs criados no Designer. Para criar fragmentos de layout, é necessário criar os XDPs e [fazer upload deles para o AEM Forms](/help/forms/using/import-export-forms-templates.md).

Um ou mais fragmentos de layout podem formar partes de uma correspondência e definir o layout gráfico dessas partes. Um fragmento de layout pode conter campos de formulário típicos, como Endereço e Número de referência, e subformulários vazios que denotam áreas de destino. Além disso, os fragmentos de layout permitem criar tabelas e inseri-las em cartas.

Um caso de uso comum é localizar padrões de layout reutilizáveis em cartas e criar fragmentos de layout para eles. Por exemplo, a saudação, o endereço e a parte do assunto da carta, que aparece na mesma ordem em várias letras. Outro exemplo pode ser uma tabela com um número semelhante de linhas e colunas usadas em várias letras.

Você pode criar um fragmento de layout com base em um XDP existente. Um fragmento de layout pode ser composto de campos e áreas de destino ou uma ou mais tabelas. As tabelas em um layout podem ser estáticas ou dinâmicas. Um XDP é criado no Designer e [carregado para o AEM Forms](/help/forms/using/import-export-forms-templates.md). Um XDP pode formar a estrutura de um fragmento de layout ou de uma letra. Mais informações sobre [Design do layout](/help/forms/using/layout-design-details.md).

O uso de fragmentos vinculados a áreas de destino permite que a correspondência seja alterada no momento da criação. O fragmento de layout com diferentes dimensões pode ser criado e o fragmento apropriado pode ser vinculado à área de destino. Os fragmentos de layout também permitem personalizar algumas das propriedades da tabela:

1. Você pode aumentar a contagem de linhas e colunas.
1. Você pode especificar o texto do cabeçalho e do rodapé para mais linhas e colunas.
1. Você pode definir a proporção da largura da coluna da tabela. No tempo de execução, as colunas da tabela são redimensionadas de acordo com a proporção definida e o espaço disponível. A soma da proporção de largura deve ser 100. Caso contrário, não é aplicável.
1. Se uma tabela for um marcador de posição (contiver apenas uma única célula em branco), você poderá definir o tipo (área/campo de destino) de novas colunas.
1. Você pode ocultar linhas de cabeçalho e rodapé.

Antes de executar esse procedimento, crie um fragmento XFA usando o Designer. O fragmento pode conter tabelas para organizar campos e áreas de destino. O Designer permite a criação de dois tipos de tabelas: estáticas e dinâmicas. As tabelas estáticas contêm um número fixo de linhas. As tabelas estáticas podem conter áreas de destino e campos. Esses campos e área de destino não podem ser vinculados a DDEs repetitivos. Uma tabela dinâmica também pode ter uma única linha. Os dados vinculados às células da tabela determinam o número de linhas das tabelas dinâmicas. Uma tabela dinâmica pode conter apenas campos. Os DDEs podem ser repetitivos ou não.

Considere os seguintes pontos ao criar tabelas:

1. As tabelas podem ser personalizadas no momento da criação do fragmento de layout. No entanto, a opção de personalização está habilitada somente quando o subformulário pai da tabela flui.
1. Para tabelas dinâmicas, todos os campos, linhas e tabelas repetíveis usam a vinculação &quot;usar nome&quot; para que os dados sejam mesclados corretamente.
1. Para tabelas dinâmicas, todos os DDEs repetidos vinculados aos campos da tabela fazem parte da mesma hierarquia. Para DDEs não repetitivas, não há essa restrição.
1. No momento da mesclagem do fragmento de layout em tabelas de área de destino pai são redimensionadas de acordo com o espaço disponível, no entanto, o redimensionamento ocorre somente quando o fragmento de layout não contém nenhuma área de destino ou campo diretamente dentro do subformulário de nível superior. A área de destino e os campos dentro da tabela são permitidos.
1. Você pode criar tabelas de marcadores de posição. As tabelas de espaços reservados têm apenas uma única célula em branco.

* Para tabelas de espaços reservados, é possível personalizar as seguintes propriedades no momento da criação do fragmento.

   * contagem de linhas
   * contagem de colunas
   * cabeçalho e rodapé para cada coluna
   * tipo (área/campo de destino) de cada coluna
   * proporção de largura para cada coluna

* Para uma tabela que não seja de espaço reservado, você pode personalizar as seguintes propriedades:

   * contagem de linhas
   * contagem de colunas
   * cabeçalho e rodapé da coluna adicional
   * proporção de largura para cada coluna

Você pode aninhar fragmentos em uma letra. Isso implica que você pode adicionar um fragmento em um fragmento. A solução de Gerenciamento de correspondência aceita até quatro níveis de aninhamento em uma correspondência: **Carta**->**Fragmento**->**Fragmento**->**Fragmento**->**Fragmento.**

Para obter um exemplo detalhado do uso de tabelas estáticas e dinâmicas em fragmentos de layout, consulte [Exemplo com arquivos de amostra: uso de tabelas estáticas e dinâmicas em uma correspondência de](#examplewithsamplefiles).

### Criação de um fragmento de layout {#creating-a-layout-fragment}

1. Selecionar **Criar** > **Fragmento do layout**.
1. O Gerenciamento de correspondência exibe os XDPs disponíveis. Selecione o XDP no qual deseja basear o fragmento de layout e toque em **Próxima**.
1. Especifique as seguintes informações para o layout:

   * **Título (opcional):** Insira o título do fragmento de layout. O título não precisa ser exclusivo e pode ter caracteres especiais e caracteres que não estejam em inglês. Os fragmentos de layout são referenciados por seus títulos (quando disponíveis), como em miniaturas e propriedades de ativos.
   * **Nome:** O nome exclusivo do fragmento de layout. Não pode haver dois ativos (texto, condição ou lista) em nenhum estado com o mesmo nome. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título. Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor. Esse nome aparece na lista da interface do usuário Gerenciar ativos.
   * **Descrição (opcional)**: descrição exibida na lista da interface do usuário Gerenciar ativos.
   * **Tags (opcional)**: como opção, selecione as tags a serem aplicadas à condição. Você também pode digitar o nome de uma nova tag e criá-la.

1. Toque no **Tabela** e especifique as seguintes informações para o layout:

   * **Configuração para**: selecione a tabela que está sendo configurada. Como um sufixo para o nome da tabela na lista suspensa é (Estático) se a tabela for estática, ou (Dinâmico) se a tabela for dinâmica. As tabelas estáticas contêm um número fixo de linhas. As tabelas estáticas podem conter áreas de destino e campos. Esses campos e área de destino não podem ser vinculados a DDEs repetitivos. Os dados vinculados às células da tabela determinam o número de linhas das tabelas dinâmicas.

   * **Linhas**: selecione o número de linhas para o layout. A contagem de linhas configurada deve ser maior ou igual à contagem de linhas original.
   * **Colunas**: selecione o número de colunas para o layout. A contagem de colunas configurada deve ser maior ou igual à contagem de colunas original.

   Para cada coluna são necessários os seguintes detalhes:

   * **Cabeçalho**: texto a ser exibido no cabeçalho
   * **Rodapé**: texto a ser exibido no rodapé
   * **Tipo**: tipo de coluna adicional. Campo ou área de destino. O tipo está habilitado para tabelas de espaços reservados estáticas. O tipo pode ser definido no nível da coluna e não no nível da célula. Todas as células em uma coluna estendida seriam do mesmo tipo. Para uma tabela dinâmica, todas as colunas são do tipo Field. Para tabelas que não sejam de espaço reservado, não é possível definir o tipo de colunas adicionais. Nesse caso, o tipo de células adicionais na coluna estendida é o mesmo que o tipo da última coluna nessa linha e o tipo de célula na linha adicional é o mesmo que o tipo da última célula nessa coluna.
   * **Relação de largura:** proporção das larguras de coluna da tabela.

   Para obter um exemplo detalhado do uso de tabelas estáticas e dinâmicas em fragmentos de layout, consulte [Exemplo com arquivos de amostra: uso de tabelas estáticas e dinâmicas em uma correspondência de](#examplewithsamplefiles).

1. Toque **Salvar**.

### Fazer upload de um XDP para o Gerenciamento de correspondência {#upload-an-xdp-to-correspondence-management}

Para obter instruções sobre como fazer upload/importar um XDP para o Gerenciamento de correspondência, consulte [Importação e exportação de ativos para o AEM Forms](/help/forms/using/import-export-forms-templates.md).

### Práticas recomendadas/dicas e truques {#best-practices-tips-and-tricks-2}

#### Definir a associação de subformulário padrão {#set-the-default-subform-binding}

Ao criar áreas de destino no Designer, é útil definir a associação padrão para todos os novos subformulários como &quot;nenhum&quot;.

Para definir a vinculação padrão:

1. No Designer, toque em **Ferramentas** > **Opções** > **Associações de Dados** > **Vinculação de subformulário**.

1. Na lista Associação padrão para novos subformulários, selecione **Sem associação de dados**.

Isso garante que os subformulários inseridos usando o comando Inserir > Subformulário ou arrastar e soltar da Paleta de objetos tenham uma vinculação de &quot;nenhum&quot; por padrão. Isso significa que, por padrão, qualquer novo subformulário é uma área de destino, a menos que você adicione conteúdo a ele, altere sua configuração de vinculação ou nomeie o subformulário com um sufixo &quot;_int&quot;.

#### Conformidade com a Seção 508 {#section-compliance}

Se a carta finalizada criada na interface do usuário Criar correspondência for usada para preencher um fluxo de trabalho posterior. Siga estas recomendações relacionadas à Seção 508 ao criar o layout. Caso contrário, a letra PDF será para exibição e você poderá ignorar essas recomendações:

* Todos os subformulários de área de destino e todos os campos em um layout têm uma ordem de tabulação.
* Os campos com legendas são compatíveis com 508 por padrão. O atributo /field/assist/speak@priority do campo é definido como &quot;personalizado&quot; por padrão, o que significa que, a menos que o texto do leitor de tela personalizado seja fornecido, o leitor de tela lerá a legenda do campo.
* Os campos sem legendas especificam uma dica de ferramenta e indicam que os leitores de tela leem a dica de ferramenta definindo

`/field/assist/speak@priority="toolTip"` e especificando o texto da dica de ferramenta em `/field/assist/toolTip`.

#### Formatos de data no Designer e no Gerenciador de configuração de ativos {#date-formats-in-designer-and-asset-configuration-manager}

Ao criar um layout no Designer, certifique-se de que os formatos dos campos de data correspondam aos formatos de data especificados em Formatos de exibição de dados no [Propriedades de configuração do gerenciamento de correspondência](/help/forms/using/cm-configuration-properties.md). Para obter mais informações, consulte &quot;Formatação de valores de campo e uso de padrões&quot; na Ajuda do Designer.

#### Captura de intervalos de datas {#capturing-date-ranges}

Ao lidar com uma combinação de datas, como startDate - endDate, use um único subformulário para garantir o alinhamento correto na correspondência concluída e minimizar o número de campos.

#### Definindo a vinculação no nível do formulário {#setting-form-level-binding}

Quando um layout contém muitos campos e áreas de destino mapeados para elementos XML únicos, use a vinculação no nível do formulário e crie um nó separado para cada elemento. Os campos vinculados no nível do formulário são ignorados ao mapear dados no Gerenciamento de correspondência.

#### Não usar áreas de destino do subformulário em uma página principal {#do-not-use-subform-target-areas-in-a-master-page}

As áreas de público-alvo do subformulário em uma página principal não estão visíveis na interface do usuário Gerenciar ativos e os dados não podem ser mapeados para elas.

#### Escolha de posições e tipos apropriados para áreas de destino {#choosing-appropriate-positions-and-types-for-target-areas}

Ao criar o layout, tenha cuidado ao escolher subformulários. Se o layout contiver um único subformulário, ele poderá ser um tipo com fluxo. Depois de posicionar campos no subformulário, você pode envolvê-lo em outro subformulário para que o subformulário inserido também flua e o layout não seja perturbado.

#### Inserção de campos em páginas principais {#placing-fields-on-master-pages}

Observe o seguinte ao colocar um campo em uma página principal:

* Definir a vinculação de campos de página principais para Usar dados globais
* Não coloque o campo diretamente abaixo da PageArea raiz da página principal.
* Vincule o campo em um subformulário nomeado e verifique se a vinculação do subformulário nomeado está definida como Usar nome.

## Criação de tabelas usando fragmentos de layout {#creating-tables-using-layout-fragments}

Muitos modelos de correspondência contêm tabelas. As tabelas podem ser estáticas, como uma tabela de termos e condições, onde cada linha representa uma condição e cada parte é mostrada em uma coluna separada. As tabelas também podem ser dinâmicas, como informações da conta, que contêm informações como nome do cliente, id da conta, número da transação e valor da transação.

* **Tabelas estáticas**: às vezes, as tabelas são criadas com linhas que têm um número diferente de colunas, como em uma tabela de termos e condições. Onde cada linha representa uma condição e cada condição pode ter subpartes diferentes. Cada parte é mostrada em uma coluna separada.
* **Tabelas dinâmicas**: os fragmentos de layout fornecem a capacidade de vincular campos de uma tabela dinâmica a DDEs de coleção. No momento da geração da correspondência, as linhas da tabela são geradas de acordo com o tamanho da coleção DDEs.

O DD tem um elemento de coleta Nominee_details que tem um elemento composto com três elementos primitivos: Nominee_name, Nominee_address e Nominee_gender.
O XDP dinâmico também tem os mesmos cabeçalhos. Assim, você pode mapear os campos XDP dinâmicos com os campos de DD mencionados acima.

### Exemplo com arquivos de amostra: Uso de tabelas estáticas e dinâmicas em uma correspondência {#examplewithsamplefiles}

Este exemplo mostra como criar uma tabela dinâmica e uma tabela estática, vincular a tabela dinâmica a DDEs e, em seguida, criar uma letra que inclua essas duas tabelas. Ao trabalhar com este exemplo, você pode criar arquivos do zero ou usar os arquivos de entrada fornecidos nas etapas.

1. Crie um Dicionário de Dados (DD) que você deseja usar no exemplo, conforme representado no gráfico.

   Em seguida, selecione DD e exporte dados de amostra. O arquivo XML que você obtém contém dados de Funcionário e três instâncias para Nominee_details (por padrão, são baixadas 3 instâncias. É possível adicionar ou excluir de acordo com sua necessidade). Atualize os valores e importe os dados de teste em DD. O arquivo CMP é o pacote e contém o DD. Portanto, importe o DD para o Gerenciamento de correspondência.

   Para obter mais informações sobre como trabalhar com dicionários de dados e dados de teste, consulte [Dicionário de dados](/help/forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Estrutura do dicionário de dados](assets/dd.jpeg)

[Obter arquivo](assets/exportpackage_1431709897770.cmp.zip)

1. No Designer, crie dois XDPs (fragmentos de layout): uma tabela dinâmica e uma tabela estática. Para ambos os layouts:

   * Adicionar subformulário à coluna da tabela. Altere o layout do subformulário pai da tabela para fluído e remova as associações do subformulário na tabela.
   * Adicione um subformulário à célula da tabela. Altere o layout do subformulário pai da tabela para fluído e remova as associações do subformulário na tabela.

   Ou use os XDPs estáticos e dinâmicos anexados a esta etapa.

   Para obter mais informações sobre como trabalhar com fragmentos de layout, consulte [Fragmentos de layout](#layoutfragments).
Para obter mais informações sobre criação de layouts, consulte [Ajuda do Designer](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/).

[Obter arquivo](assets/static.xdp.zip)

[Obter arquivo](assets/dynamic.xdp.zip)

1. Faça upload dos XDPs para o AEM Forms.
1. Crie um fragmento de layout com base no XDP dinâmico. A guia Table das propriedades exibe que a tabela é dinâmica (campo Configuration For ). O número de linhas (1) e colunas (3) é derivado do XDP/Fragmento de layout.

   Os campos desse layout são posteriormente vinculados ao DD importado e, na correspondência, o número de linhas é criado dinamicamente com base no número de registros no arquivo de dados de teste (o arquivo de dados XML anexado ao DD).

   ![Criar uma tela de fragmento de layout](assets/dynamictableproperties.png)

   Clique para abrir a imagem em tamanho real

1. Crie um fragmento de layout com base no XDP estático. A guia Table das propriedades exibe que a tabela é estática (campo Configuration For ). O número de linhas (1) e colunas (3) é derivado do XDP/Fragmento de layout.

   Você pode alterar o número de colunas e linhas aqui. De acordo com o que você escolhe nesta tela, o número de linhas e colunas de uma tabela estática permanece fixo na letra criada com este layout.
   [ ![Criar uma tela de fragmento de layout](assets/statictableproperties.png)](assets/statictableproperties-1.png)

1. Criar uma correspondência usando ambos os fragmentos de layout nela. Ao inserir o XDP dinâmico na correspondência, defina a vinculação de seus campos para os elementos de coleção do dicionário de dados.

   Para obter mais informações sobre a criação de modelos de cartas e cartas, consulte [Criar carta](/help/forms/using/create-letter.md).

1. Salve a carta e visualize-a. Quando você visualiza a correspondência, os valores do Dicionário de dados são exibidos nela. Para a tabela dinâmica, há três linhas. Isso ocorre porque os dados de teste têm três registros para essas linhas.

   Para a tabela estática, há quantas linhas e colunas você especificar ao criar o fragmento de layout.

   ![Tabela estática na carta](assets/statictableletter.png)

   Para a tabela dinâmica, as três linhas são exibidas de acordo com o número de registros no arquivo de dados de teste. Isso aconteceu porque, ao adicionar o layout à correspondência, você criou uma ligação entre os campos da tabela dinâmica e os elementos de coleção do dicionário de dados. Os valores Nome, Endereço e Gênero são preenchidos a partir do arquivo de dados de teste usado.

   ![Tabela dinâmica na carta](assets/dynamictableletter.png)

## Criar uma cópia de um fragmento de documento {#create-a-copy-of-a-document-fragment}

Para criar rapidamente um fragmento de documento com propriedades e conteúdo semelhantes a um fragmento de documento existente, você pode copiá-lo e colá-lo.

1. Na lista de fragmentos de documento, selecione um ou mais fragmentos de documento. A interface do usuário do exibe o ícone Copiar.
1. Toque em Copiar. A interface exibe o ícone Colar. Você também pode optar por entrar em uma pasta antes de colar. Pastas diferentes podem conter ativos com os mesmos nomes. Para obter mais informações sobre pastas, consulte [Pastas e organização de ativos](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Toque em Colar. A caixa de diálogo Colar é exibida. Se você estiver copiando e colando os fragmentos de documento no mesmo local, o sistema atribuirá automaticamente nomes e um título às novas cópias de letras, mas você poderá editar os títulos e nomes das letras.
1. Se necessário, edite o Título e o Nome com os quais deseja salvar a cópia do fragmento do documento.
1. Toque em Colar. A cópia do fragmento do documento é criada.
