---
title: Criação e uso de temas
seo-title: Criação e uso de temas
description: Você pode usar temas para estilizar e fornecer uma identidade visual para um formulário adaptável ou comunicação interativa. Você pode compartilhar um tema em qualquer número de formulários adaptáveis ou comunicações interativas.
seo-description: Você pode usar temas para estilizar e fornecer uma identidade visual para um formulário adaptável ou comunicação interativa. Você pode compartilhar um tema em qualquer número de formulários adaptáveis ou comunicações interativas.
uuid: 88b6b6fd-181b-48c5-ac15-2b37592bd14b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
content-strategy: max-2018
discoiquuid: 770e9174-b648-462a-abe9-05fefa967d86
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Criação e uso de temas {#creating-and-using-themes}

## Introdução {#introduction}

É possível criar e aplicar temas para estilizar um formulário adaptável ou uma comunicação interativa. Um tema contém detalhes de estilização para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes. Os temas são gerenciados de forma independente sem referência a um formulário adaptável ou comunicação interativa.

É possível:

* Criar um tema
* Editar e copiar um tema existente
* Baixar e carregar um tema existente no servidor de formulários AEM
* Gerenciar dependências para um tema

## Criação, download ou upload de um tema {#creating-downloading-or-uploading-a-theme}

Com o AEM Forms, você pode criar, baixar ou carregar temas. Um tema é criado como outros ativos, como formulários, documentos e letras. O tema é salvo como uma entidade separada, completa com meta-propriedades como formulários. Temas sendo uma entidade separada permitem a reutilização em vários formulários adaptáveis e comunicações interativas. Você também pode mover um tema para uma instância diferente do AEM Forms e reutilizá-lo.

### Criação de um tema {#creating-a-theme}

Execute as seguintes etapas para criar um tema:

1. Clique em **Adobe Experience Manager**, **Forms** e clique em **Temas**.

1. Na página Temas, clique em **Criar > Tema**.
Um assistente para criar um tema é iniciado.

1. Na guia Básico do assistente para Criar tema, forneça **Título** e **Nome** do tema. Estes são campos obrigatórios.

1. Na guia Avançado, você obtém dois campos:

   * **Localização** do Clientlib: Localização no repositório que armazena os clientlibs para o tema.

   * **Categoria** Clientlib: Fornece um campo de texto para inserir o nome da categoria clientlib para o tema.

1. Clique em **Criar** e, em seguida, clique em **Editar** para abrir o tema no Editor de temas ou clique em **Concluído** para retornar à página temas.

### Download de um tema {#downloading-a-theme}

Você pode exportar temas como um arquivo zip e usá-los em outros projetos ou instâncias do AEM. Para baixar um tema:

1. Clique em **Adobe Experience Manager**, **Forms** e clique em **Temas**.

1. Na página Temas, **selecione** um tema e clique em **Download**. Será exibida uma caixa de diálogo com os detalhes do tema.

1. Clique em **Download**. O tema é baixado como um arquivo zip.

>[!NOTE]
>
>Se você fizer download de um tema que tenha um formulário adaptável associado e o formulário adaptativo associado for baseado em um modelo personalizado, faça o download do modelo personalizado. Ao carregar o tema e o formulário adaptável baixados em um servidor de formulários AEM, faça upload do modelo personalizado relacionado também.

### Fazer upload de um tema {#uploading-a-theme}

Você pode usar temas criados com predefinições de estilização em seu projeto. Você pode importar pacotes de temas que outras pessoas criarem fazendo upload deles no seu projeto.

Para carregar um tema:

1. Clique em **Adobe Experience Manager**, **Forms** e clique em **Temas**.

1. Na página Temas, clique em **Criar > Upload** de arquivo.
1. No prompt Upload de arquivo, navegue e selecione um pacote de tema no computador e clique em **Carregar**.
O tema carregado está disponível na página temas.

## Metadados de um tema {#metadata-of-a-theme}

Lista de meta-propriedades de um tema (encontrado na página de propriedades de um tema).

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>Nome</strong></th>
   <th><strong>Pode ser editado</strong></th>
   <th><strong>Descrição da propriedade</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>Título</td>
   <td>Sim</td>
   <td>Nome de exibição do tema.</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>Descrição</td>
   <td>Sim</td>
   <td>Descrição sobre o tema.</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>Tipo</td>
   <td>Não</td>
   <td>
    <ul>
     <li>Tipo de ativo.</li>
     <li>Valor é sempre Tema.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>Criado</td>
   <td>Não</td>
   <td>Data da criação do tema</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>Nome do autor</td>
   <td>Sim</td>
   <td>Autor do tema. Calculado no momento da criação do tema.</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>Data da última modificação</td>
   <td>Não</td>
   <td>Data em que o tema foi modificado pela última vez.</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>Status</td>
   <td>Não</td>
   <td>Status do tema (Modificado/Publicado).</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>Data de início da publicação</td>
   <td>Sim</td>
   <td>Hora de publicar automaticamente o tema.</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>Data de término da publicação</td>
   <td>Sim</td>
   <td>Tempo para cancelar a publicação automática do tema.</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>Tags</td>
   <td>Sim</td>
   <td>Um rótulo anexado ao tema para identificação usado para melhorar a pesquisa.</td>
  </tr>
  <tr>
   <td>11.</td>
   <td>Referências</td>
   <td>Links</td>
   <td>
    <ul>
     <li>Contém a seção 'Referenciado por'. Listas formulários que usam o tema.</li>
     <li>Como o tema não se refere a nenhum outro ativo, não há seção "Referências".</li>
    </ul> </td>
  </tr>
  <tr>
   <td>12.</td>
   <td>Local do Clientlib</td>
   <td>Sim</td>
   <td>
    <ul>
     <li>O caminho do repositório definido pelo usuário em '/etc' onde os clientlibs correspondentes a esse tema são armazenados.</li>
     <li>Valor padrão - '/etc/clientlibs/fd/temas + caminho relativo do ativo do tema.</li>
     <li>Se o local não existir, a hierarquia de pastas será gerada automaticamente.</li>
     <li>Quando esse valor é alterado, a estrutura do nó clientlib é movida para o novo local inserido.<br /> <em><strong>Observação:</strong> Se você alterar o local padrão clientlib, no repositório CRXDE atribua <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>a <code>forms-users</code> e <code>crx:replicate</code>a <code>jcr:read </code><code>fd-service</code> no novo local. Além disso, anexe outra ACL adicionando <code>deny jcr:addChildNodes</code> para <code>forms-user</code></em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>13.</td>
   <td>Nome da categoria do Clientlib</td>
   <td>Sim</td>
   <td>
    <ul>
     <li>O nome de categoria clientlib definido pelo usuário para este tema.</li>
     <li>Um erro será exibido se o nome já estiver sendo usado por outro tema existente.</li>
     <li>Valor padrão - calculado usando a localização do tema.</li>
     <li>Quando esse valor é alterado, o nome da categoria é atualizado no nó clientlib correspondente. A atualização do Nome de Categoria Clientlib nos arquivos jsp não é necessária porque o nome de categoria clientlib é usado por referência.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Sobre o Editor de Temas {#about-the-theme-editor}

O AEM Forms é enviado com o Editor de Temas. Trata-se de uma interface amigável para usuários empresariais e Web designer/desenvolvedor, que oferece funcionalidades necessárias para especificar o estilo de vários formulários adaptáveis e elementos de comunicação interativa com facilidade. Ao criar um tema, ele é armazenado como uma entidade separada, como formulários, comunicações interativas, letras, fragmentos de documento e dicionários de dados.

O Editor de Temas permite personalizar estilos dos componentes estilizados em um tema. Você pode personalizar a aparência de um formulário ou de uma comunicação interativa em um dispositivo.

O Editor de Temas é dividido em dois painéis:

* **Tela** de desenho - Aparece no lado direito. Mostra um exemplo de formulário adaptável ou comunicação interativa em que todas as alterações de estilo refletem instantaneamente. Você também pode selecionar objetos diretamente da tela de desenho para procurar estilos associados a eles e editar esses estilos. Uma régua de resolução de dispositivo na parte superior governa a Tela. Selecionar um ponto de interrupção de resolução na régua mostra a pré-visualização do formulário de amostra ou a comunicação interativa para a respectiva resolução. A tela é discutida detalhadamente [abaixo](../../forms/using/themes.md#using-canvas).

* **Barra lateral**- Aparece no lado esquerdo. Ele tem os seguintes itens:

   * **Seletor:** Mostra o componente selecionado para estilização e suas propriedades que podem ser estilizadas. O seletor representa todos os componentes de um tipo. Se você selecionar um componente de caixa de texto em um tema para estilização, todas as caixas de texto em seu formulário ou comunicação interativa herdarão o estilo. Os seletores permitem selecionar um componente genérico ou um componente específico para estilização. Por exemplo, um componente de campo é um componente genérico e uma caixa de texto é um componente específico.

      **Componente genérico de estilo:**
Um campo pode ser um campo de caixa numérico, como idade, ou um campo de caixa de texto, como endereço.
Ao criar um estilo para um campo, todos os campos, como idade, nome e endereço, têm o estilo.

      **Componente**específico de estilo:
Um componente específico afeta objetos da categoria específica. Quando você estimula o componente de caixa numérica no tema, somente o objeto de caixa numérica na herda o estilo.

      Por exemplo, um campo de caixa de texto, como endereço, é maior e um campo de caixa numérica, como idade, é menor em comprimento. É possível selecionar um campo de caixa numérico, reduzir seu comprimento e aplicar ao formulário. A largura de todos os campos de caixa numérica é reduzida em seu formulário.

      Ao personalizar todos os componentes do campo com uma cor de plano de fundo específica, todos os campos, como idade, nome e endereço, herdam a cor de plano de fundo. Quando você seleciona uma caixa numérica, como idade, e reduz sua largura, largura de todas as caixas numéricas, como idade, o número de pessoas em uma família é reduzido. A largura das caixas de texto não é alterada.

   * **Estado:** Permite personalizar estilos de um objeto em um estado específico. Por exemplo, você pode especificar a aparência de um objeto quando ele está no padrão, foco, desativado, focalizado ou no estado de erro.
   * **Categorias de propriedades:** As propriedades de estilo são divididas em várias categorias. Por exemplo, Dimensão e posição, Texto, Plano de fundo, Borda e Efeitos. Em cada categoria, você fornece informações de estilização. Por exemplo, em Plano de fundo, é possível fornecer Cor do plano de fundo e Imagem e gradiente.

   * **Avançado:** Permite adicionar CSS personalizado a um objeto, que substitui as propriedades que os controles visuais definem se há uma sobreposição.

   * **CSS** de Visualização: Permite que você visualização o CSS do componente selecionado
   Além disso, na barra lateral, na parte inferior há uma seta. Ao clicar na seta, você obtém mais duas opções: **Simule o sucesso** e **simule o erro.** Essas opções, juntamente com as opções descritas acima, são discutidas detalhadamente [abaixo](../../forms/using/themes.md#using-rail).

[ Editor de ![temas com Painel e Tela realçada.](assets/themes.png)](assets/themes-1.png) **A.** Barra lateral **B.** Tela

### Componentes de estilo {#styling-components}

Você pode usar um tema em vários formulários adaptáveis e comunicações interativas, que importam a formatação de componentes especificada no tema. Você pode criar um estilo para vários componentes, como títulos, descrição, painéis, campos, ícones e caixas de texto. Use widgets para configurar as propriedades do componente em um tema. O conhecimento prévio do CSS ou MENOS não é necessário, mas é desejado, embora a seção Substituições de CSS permita que você escreva o código CSS ou forneça seletores personalizados. A seção Substituições de CSS é exibida quando você seleciona um componente na barra lateral.

![Componentes com estilo na barra lateral](assets/stylable-components.png)

Opções na barra lateral que permitem selecionar e estilizar componentes diferentes.

Clicar no botão editar em um componente na barra lateral seleciona o componente na Tela e permite que você estilize o componente usando opções na barra lateral.

Determinados componentes, como caixa de texto, caixa numérica, botão de opção e caixa de seleção, são classificados em componentes genéricos, como Campo. Por exemplo, você deseja personalizar o estilo de botões de opção. Para selecionar botões de opção para estilização, selecione **Campo > Widget > Botão** de opção.

Clique em **EXPANDIR TUDO** na barra lateral para visualização, selecionar e estilo de componentes categorizados que não estão visíveis no início.

### Layouts de painel de estilo {#styling-panel-layouts-br}

Temas no AEM Forms suportam estilos de elementos no layout de painéis em seus formulários e comunicações interativas. O estilo de elementos em layouts predefinidos e layouts personalizados é compatível.

Os painéis predefinidos incluem:

* Guias na esquerda
* Guias na parte superior
* Menu sanfonado
* Receptivo
* Assistente
* Layout móvel

   * Títulos de painel no cabeçalho
   * Sem títulos de painel no cabeçalho

Os seletores variam para cada layout.
O estilo de layouts personalizados do Editor de Temas envolve:

* Definição dos componentes para um layout que pode ser estilizado e seletores de CSS para identificar exclusivamente esses componentes
* Definição das propriedades de CSS que podem ser aplicadas a esses componentes
* Defina o estilo desses componentes interativamente na interface do usuário

### Estilos diferentes para tamanhos de tela diferentes {#different-styles-for-different-screen-sizes-br}

Os layouts para desktop e dispositivos móveis podem ter estilos levemente diferentes. Para dispositivos móveis, tablets e telefones compartilham layouts semelhantes, exceto tamanhos de componentes.

Use os pontos de interrupção do Editor de Temas para definir estilos alternativos para tamanhos de tela diferentes. Você pode selecionar um dispositivo ou uma resolução base na qual start criar o tema, e as variações de estilo para outras resoluções são geradas automaticamente. Você pode modificar explicitamente o estilo de todas as resoluções.

>[!NOTE]
>
>O tema é criado primeiro usando um formulário ou uma comunicação interativa e, em seguida, aplicado em diferentes formulários ou comunicações interativas. Os pontos de interrupção usados na criação de temas podem ser diferentes do formulário ou da comunicação interativa em que o tema é aplicado. Os query de mídia CSS são baseados no formulário ou na comunicação interativa usada na criação de temas, e não no formulário ou na comunicação interativa na qual o tema é aplicado.

### Alterações de contexto de propriedades de estilo na barra lateral ao selecionar objetos {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

Quando você seleciona um componente na Tela de desenho, suas propriedades de estilo são listadas na barra lateral. Selecione o tipo de objeto e seu estado e forneça seu estilo.

### Estilos usados recentemente no Editor de Temas {#recently-used-styles-in-theme-editor}

O editor de temas armazena em cache até 10 estilos aplicados a um componente. Você pode usar os estilos em cache com outro componente de um tema. Estilos usados recentemente estão disponíveis logo abaixo do componente selecionado na barra lateral como uma caixa de lista. Inicialmente, a lista de estilos usados recentemente está vazia.

![biblioteca de ativos](assets/asset-library.png)

À medida que você estimula um componente, os estilos são armazenados em cache e listados na caixa lista. Neste exemplo, o rótulo da caixa de texto tem o estilo de alterar o tamanho e a cor da fonte. Você pode seguir etapas semelhantes para escolher uma imagem ou alterar as cores para estilizar um componente. Observe como o estilo é armazenado em cache e listado na caixa lista quando o estilo do rótulo do campo é alterado.

![Estilo de fonte em cache para um componente disponível para outro](assets/font-style-cached.png)

Neste exemplo, o estilo do rótulo do campo é alterado e quando a opção Descrição do painel responsivo é selecionada para estilo, uma entrada de lista é adicionada à biblioteca de ativos. A entrada na biblioteca de ativos pode ser usada para alterar o estilo da Descrição do painel responsivo.

Quando um estilo é adicionado na biblioteca de ativos, ele fica disponível para outros temas e no modo [de](../../forms/using/inline-style-adaptive-forms.md) estilo do editor de formulários ou da interface do editor de comunicações interativa. Da mesma forma, quando você usa o modo de estilo do editor de formulário ou da interface do editor de comunicação interativa para criar o estilo de um componente, o estilo é armazenado em cache e está disponível em temas.

O botão mais na biblioteca de ativos permite salvar permanentemente o estilo com um nome que você fornece. O botão mais salva o estilo mesmo se você não clicar no botão Salvar na barra lateral para aplicar o estilo a um componente. O botão mais para salvar um estilo para uso posterior não está disponível no modo de estilo.

![Fornecer um nome de estilo personalizado para a biblioteca de ativos](assets/custom-style-name.png)

Quando você fornece um nome personalizado para um estilo, o estilo é vinculado a um tema e não está mais disponível para outros temas. Para excluir um estilo salvo:

1. Na barra de ferramentas CANVAS, clique em Opções **de** tema ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/theme-options.png) > **Gerenciar estilos**.
1. Na caixa de diálogo Gerenciar estilos, selecione um estilo salvo e clique em **Excluir**.

   ![Excluir o estilo salvo](assets/manage-styles.png)

### pré-visualização ao vivo, salvar e descartar alterações {#live-preview-save-and-discard-changes}

As modificações feitas no estilo são refletidas instantaneamente no formulário ou na comunicação interativa carregada na tela de desenho. A pré-visualização ao vivo permite que você defina e veja interativamente o impacto do estilo. Quando você altera o estilo de um componente, o botão **Concluído** é ativado na barra lateral. Para reter as alterações, use o botão **Concluído** .

>[!NOTE]
>
>Quando um caractere inválido é inserido em um campo, a cor do limite do campo muda para vermelho e uma mensagem de erro é exibida no canto superior esquerdo da tela. Por exemplo, se você digitar alfabetos em uma caixa de texto que aceita caracteres numéricos como entradas, a cor do limite da caixa de entrada mudará para vermelho. Não é possível salvar esse tema sem resolver o erro exibido na parte superior.

### Tema com outro formulário adaptável ou comunicação interativa {#theme-with-another-adaptive-form-or-interactive-communication}

Quando você cria um tema, ele é criado com um formulário enviado com o Editor de Temas. Você fornece estilização para componentes neste formulário. Em vez do formulário enviado com o Editor de Temas, você pode selecionar um formulário ou uma comunicação interativa de sua escolha para fornecer estilos e pré-visualização aos resultados.

Para substituir o formulário atual ou a comunicação interativa na Tela do Editor de Temas:

1. No painel EDITOR DE TEMAS, clique em Opções **de** tema ![opções](assets/theme-options.png) de tema > **Configurar**.

1. Na guia Geral, procure e selecione um formulário ou uma comunicação interativa para o campo Formulário **adaptável/Documento** .

### Refazer/Desfazer {#redo-undo}

Você pode desfazer ou refazer as alterações indesejadas que ocorrem acidentalmente. Use os botões de refazer/desfazer na tela de desenho.

![Refazer e desfazer ações](assets/redo_undo_new.png)

Botões Desfazer/Refazer na Tela de desenho

Os botões Refazer/Desfazer aparecem quando você estimula um componente no Editor de Temas.

## Uso do Editor de Temas {#using-the-theme-editor}

O Editor de Temas permite que você edite um tema criado ou carregado. Navegue até **Formulários e Documentos > Temas**, selecione um tema e abra-o. O tema é aberto no Editor de Temas.

Como discutido acima, o Editor de Temas tem dois painéis: Barra lateral e Tela de desenho.
![editor de temas](assets/theme-editor.png)

Personalizar o estilo de estado de sucesso do componente de Widget de caixa de texto no Editor de temas. O componente é selecionado na Tela de desenho e seu estado é selecionado na barra lateral. As opções de estilo disponíveis na barra lateral são usadas para personalizar a aparência de um componente.

### Uso da tela de desenho {#using-canvas}

O tema é criado usando o formulário pronto para uso ou usando um formulário ou uma comunicação interativa de sua escolha. A Tela de desenho mostra a pré-visualização do formulário ou a comunicação interativa usada para criar o tema com personalizações especificadas no tema. A régua acima do formulário é usada para determinar o layout de acordo com o tamanho da exibição do dispositivo.

Na barra de ferramentas Tela de desenho, você verá:

* **Alternar painel** lateral ![alternar painel](assets/toggle-side-panel.png): Permite mostrar ou ocultar a barra lateral.
* **Opções** do tema Opções do ![tema](assets/theme-options.png): Fornece três opções

   * Configurar: Fornece opções para selecionar o formulário de pré-visualização ou a comunicação interativa, a clientlib base e a configuração do typekit.
   * Tema de Visualização CSS: Gera CSS para o tema selecionado.
   * Gerenciar estilos: Fornece opções para gerenciar estilos de texto e imagem
   * Ajuda: Executa um tour guiado por imagem do Editor de Temas.

* **Emulador** ![de régua](assets/ruler.png): Emula a aparência do seu tema para tamanhos de exibição diferentes. Um tamanho de exibição é tratado como um ponto de interrupção no emulador. Você pode selecionar um ponto de interrupção e especificar um estilo para ele. Por exemplo, Desktop e Tablet são dois pontos de interrupção. Você pode especificar estilos diferentes para cada ponto de interrupção.

Ao selecionar um componente na Tela de desenho, você verá a barra de ferramentas do componente na parte superior. A barra de ferramentas do componente permite selecionar componentes ou alternar para componentes genéricos. Por exemplo, você seleciona uma caixa de texto numérico em um painel. Você verá as seguintes opções na barra de ferramentas do componente:

* **Widget** de caixa numérica: Permite selecionar o componente para personalizar sua aparência na barra lateral.
* **Widget** de campo: Permite selecionar o componente genérico para estilização. Neste exemplo, todos os componentes de entrada de texto (caixa de texto/caixa numérica/entrada de valor numérico/entrada de data) são selecionados para estilização.

* ![nível](assets/field-level.png)de campo: Permite alternar para o componente genérico para o estilo. Se você selecionar uma caixa numérica e tocar nesse ícone, o componente de campo será selecionado. Se você selecionar o componente de campo e tocar nesse ícone, o painel será selecionado. Se você continuar tocando nesse ícone para seleção, acabará selecionando o layout para estilização.

>[!NOTE]
>
>As opções disponíveis na barra de ferramentas do componente variam com base no componente selecionado.

![Barra de ferramentas Componente](assets/overlay.png)

Barra de ferramentas do componente na caixa numérica na Tela

### Uso da barra lateral {#using-rail}

A barra lateral no editor de temas fornece opções para personalizar estilos para componentes em um tema e usar seletores. Os seletores permitem selecionar um grupo de componentes ou componentes individuais e você pode procurar seletores na barra lateral. Você pode gravar seletores para componentes personalizados.

Quando você seleciona um componente da Tela de desenho ou seletores na barra lateral, a barra lateral mostra todas as opções que permitem personalizar estilos para ela.
Abaixo estão as opções exibidas na barra lateral ao selecionar um componente:

* Estado
* Folha de propriedades
* Simular erro/sucesso

#### Estado {#state}

Um estado é um indicador da interação do usuário com um componente. Por exemplo, quando um usuário digita dados errôneos em uma caixa de texto, o estado da caixa de texto muda para um estado de erro. O editor de temas permite que você especifique o estilo para um estado específico.

As opções para personalizar estilos de estado variam para componentes diferentes.

#### Folha de propriedades {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Uso</strong></td>
  </tr>
  <tr>
   <td><p>Dimensões e Posição</p> </td>
   <td><p>Permite estilizar o alinhamento, o tamanho, o posicionamento e o posicionamento dos componentes no tema. </p> <p>Suas opções são configurações de exibição, preenchimento, margem, largura, altura e índice Z.</p> <p>Você também pode usar o modo Layout para definir a largura dos componentes usando uma interface fácil de arrastar e soltar. Para obter mais informações, consulte <a href="../../forms/using/resize-using-layout-mode.md">Usar o modo Layout para redimensionar componentes</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Permite personalizar os estilos de texto no componente do tema.</p> <p>Por exemplo, você deseja alterar a aparência do texto inserido na caixa de texto.</p> <p>Suas opções são família de fontes, peso, cor, tamanho, altura da linha, alinhamento do texto, espaçamento entre letras, recuo do texto, sublinhado, itálico, transformação de texto, alinhamento vertical, linha de base e direção. </p> </td>
  </tr>
  <tr>
   <td><p>Segundo plano </p> </td>
   <td><p>Permite preencher o plano de fundo do componente com uma imagem ou uma cor. </p> </td>
  </tr>
  <tr>
   <td><p>Borda</p> </td>
   <td><p>Permite escolher a aparência da borda do componente. Por exemplo, você deseja que a caixa de texto tenha uma borda vermelha profunda e grossa com uma linha pontilhada. </p> <p>Suas opções são largura, estilo, raio e cor da borda.</p> </td>
  </tr>
  <tr>
   <td><p>Efeitos</p> </td>
   <td><p>Permite adicionar efeitos especiais aos componentes, como opacidade, modo de mesclagem e sombras. </p> </td>
  </tr>
  <tr>
   <td><p>Avançado  </p> </td>
   <td><p>Permite adicionar:</p>
    <ul>
     <li>Propriedades para <code>::before</code> e <code>::after</code> pseudo-elementos para adicionar conteúdo depois ou antes do conteúdo padrão no seletor, e estilizá-lo.<br /> Consulte Pseudo-elementos <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">do</a>CSS.</li>
     <li>O código CSS personalizado está em linha com um componente e grava seletores personalizados. </li>
    </ul> <p>Quando você adiciona um código CSS personalizado, ele substitui a personalização adicionada usando as opções na barra lateral. </p> </td>
  </tr>
 </tbody>
</table>

#### Simular erro/sucesso {#simulate-error-success}

As opções Simular erro e sucesso estão disponíveis na parte inferior da barra lateral. É possível vê-los usando uma seta de mostrar/ocultar visível na parte inferior da barra lateral. Usando o Editor de Temas, você pode criar um estilo para vários estados de um componente.

Por exemplo, você adiciona um campo numérico em seu formulário e especifica seu estilo no editor de temas. Quando um usuário digita um valor alfanumérico no campo, você deseja alterar a cor de fundo da caixa de texto. Selecione o campo numérico no tema e use a opção de estado na barra lateral. Selecione o estado Erro na barra lateral e altere a cor do plano de fundo para vermelho. Para pré-visualização do comportamento, use a opção Simular erro disponível na barra lateral. As opções Simular erro e sucesso são descritas em detalhes abaixo:

* **Simular sucesso**:
Permite ver a aparência de um componente se você especificar seu estilo para o estado de sucesso. Por exemplo, em um formulário, os clientes definem a senha. Os usuários podem definir a senha de acordo com as diretrizes fornecidas. Quando um usuário digita uma senha seguindo todas as orientações fornecidas, a caixa de texto fica verde. Quando a caixa de texto fica verde, ela está em estado de sucesso. Você pode especificar o estilo para um componente em estado de sucesso e simular sua aparência usando a opção Simular sucesso.

* **Erro**Simular:
Permite ver a aparência de um componente se você especificar seu estilo para o estado de erro. Por exemplo, em um formulário, os clientes definem a senha. Os usuários podem definir a senha de acordo com as diretrizes fornecidas. Quando um usuário digita uma senha que não segue todas as diretrizes fornecidas, a caixa de texto fica vermelha. Quando a caixa de texto fica vermelha, ela está em estado de erro. Você pode especificar o estilo de um componente em estado de erro e simular sua aparência usando a opção Simular erro.

### Estilo de um componente {#styling-a-component}

Por exemplo, no formulário, há dois tipos de caixas de texto: um que aceita somente valores numéricos e outro que aceita valores alfanuméricos. Você pode personalizar o estilo para a caixa de texto que aceita somente valores numéricos (uma caixa numérica).

Execute as seguintes etapas para personalizar o estilo de um componente específico (uma caixa numérica neste exemplo):

1. No Editor de Temas, selecione a caixa numérica na Área.
1. Ao selecionar a caixa numérica, é possível ver a barra de ferramentas do componente com três opções:

   * **Widget de caixa numérica**
   * **Nível de** campo do widget ![de campo](assets/field-level.png)

1. Selecione Widget **Caixa** numérica.
1. O título da barra lateral muda para Widget de caixa numérica e mostra opções para personalizar sua aparência.
Use a opção **Dimensão e posição** na barra lateral para personalizar o tamanho do componente. Verifique se o estado é **padrão**.

Em vez de selecionar Widget **de caixa** numérica, selecione Widget **de** campo na barra de ferramentas do componente e execute as etapas acima. Quando você seleciona dimensões para a opção Widget **de** campo, todas as caixas de texto, exceto a caixa numérica, têm o mesmo tamanho.

### Campos de estilo para um determinado estado {#styling-fields-given-state}

Com a barra de ferramentas do componente, também é possível especificar o estilo dos componentes para seus diferentes estados. Por exemplo, se um componente estiver desativado, ele estará em um estado desativado. Os estados comumente usados de um componente que você pode estilizar no editor de temas são: Padrão, Foco, Desativado, Erro, Êxito e Passe o mouse. Você pode selecionar um componente na Tela de desenho e usar a opção Estado na barra lateral para personalizar sua aparência.

Execute as seguintes etapas para personalizar o estilo de um componente em um estado específico:

1. Selecione um componente na Tela de desenho e selecione a opção apropriada na barra de ferramentas do componente.
A barra lateral mostra opções para personalizar o estilo do componente.
1. Selecione um estado na barra lateral. Por exemplo, Estado de erro.
1. Use opções como **Borda, Plano de fundo** na barra lateral para personalizar a aparência do componente.
1. Use a opção **Simular erro** na parte inferior da barra lateral para ver a aparência do estilo na edição.

Quando você personaliza o estilo de um componente depois de especificar seu estado, a personalização aparece para o componente somente para o estado especificado. Por exemplo, se você personaliza o estilo do componente quando o estado de passagem é selecionado. A personalização é exibida para o componente quando você move o ponteiro sobre o componente no formulário renderizado ou na comunicação interativa à qual você aplica o tema.

Para simular o comportamento de estados diferentes de erro e sucesso, use o modo de Pré-visualização. Para usar o modo de Pré-visualização, clique em **Pré-visualização** na barra de ferramentas da página.

### Layouts de estilo para telas menores {#styling-layouts-for-smaller-displays}

Use a régua na Tela de desenho para selecionar pontos de interrupção para dispositivos com telas menores. Clique na ![régua](assets/ruler.png) do emulador em Tela para visualização da régua e dos pontos de interrupção. Os pontos de interrupção permitem que você pré-visualização um formulário ou uma comunicação interativa para tamanhos de exibição pertencentes a diferentes dispositivos, como telefones e tablets. Vários tamanhos de exibição são suportados no Editor de Temas.

Para estilizar componentes para diferentes pontos de interrupção:

1. Na tela de desenho, selecione um ponto de interrupção acima da régua.
Um ponto de interrupção representa um dispositivo móvel e seu tamanho de exibição.
1. Use a barra lateral para personalizar o estilo de componentes de formulário ou comunicação interativa no tema para o tamanho de exibição selecionado.
1. Certifique-se de que a personalização esteja salva.

É possível criar um estilo de componentes de formulário ou comunicação interativa para vários dispositivos. Os componentes de forma e comunicação interativa para desktops e dispositivos móveis podem ter estilos completamente diferentes.

### Usar fontes da Web em um tema {#using-web-fonts-in-a-theme}

Agora é possível usar fontes disponíveis em um serviço da Web em um formulário adaptável ou comunicação interativa. O [Typekit](https://typekit.com/), o serviço de fontes da Web da Adobe, está disponível como uma configuração. Para usar o Typekit, crie um kit e fontes nele, e obtenha a ID do Kit no site [do](https://typekit.com/)Typekit.

Execute as seguintes etapas para configurar o Typekit no AEM:

1. Na instância do autor, clique em ![](assets/adobeexperiencemanager.png)adobeexperience emanagerAdobe Experience Manager > ![Martelo](assets/hammer.png) de ferramentas > Implantação > Serviços em nuvem.
1. Na página Serviços **da** Cloud, navegue até Serviços **de** terceiros > **Typekit** e clique em **Configurar agora** em Typekit. Se uma configuração já estiver disponível, clique no botão **+** para criar uma nova instância.
1. Na caixa de diálogo **Criar configuração** , especifique um título para a configuração e clique em **Criar**.

   Você é redirecionado para a página de configuração.

1. Na caixa de diálogo Editar componente que é exibida, forneça sua ID do Kit e clique em **OK**.

Execute as seguintes etapas para configurar um tema para usar a configuração TypeKit:

1. Na instância do autor, abra um tema no editor de temas.
1. No editor de temas, navegue até Opções **de** tema Opções ![de](assets/theme-options.png) tema > Opções **de** configuração.
1. No campo Configuração **do** Typekit, selecione um kit e clique em **Salvar**.

   Agora, você pode ver que as fontes são adicionadas na propriedade font-family do tema.

### Listar e selecionar fontes no editor de temas {#listing-and-selecting-fonts-in-theme-editor}

Você pode usar o serviço de configuração de tema para adicionar mais fontes ao editor de temas. Execute as seguintes etapas para adicionar fontes:

1. Faça logon no console da Web do AEM com privilégios administrativos. O URL do console da Web do AEM é `https://'[server]:[port]'/system/console/configMgr`.
1. Abra o Serviço **de configuração do tema de formulário** adaptável.

   ![configuração do tema](assets/theme-config.png)

1. Clique em +, especifique o nome da fonte e clique em **Salvar**. A fonte é adicionada e está disponível no editor de temas.

#### Seleção de fontes no editor de temas {#selecting-fonts-in-theme-editor}

Você pode usar o botão + para adicionar uma fonte. Quando você adiciona uma fonte, ela é listada na barra lateral.

![Nova fonte listada no editor de temas](assets/theme-font.png)

Além da opção de configuração de tema, também é possível adicionar a fonte do próprio editor de temas. Digite a fonte que deseja usar no campo família de fontes na barra lateral e pressione a tecla de retorno no teclado.

![Digitação e seleção de fonte no editor de temas](assets/font-selection.png)

Quando uma fonte é selecionada, ela é adicionada sob a lista da família de fontes. Você pode usar a opção Máscara no editor de temas para desativar ou ativar as fontes listadas.

![multifontes](assets/multi-fonts.jpg)

Você pode ver a alteração da fonte do componente.

O campo Família de fontes suporta várias fontes. Quando você digita uma fonte, o navegador a procura e a aplica ao componente selecionado. Se o navegador não conseguir localizar uma fonte, ele procurará uma fonte próxima a ela na família. Você pode start ao digitar a fonte específica que está procurando. Se você não encontrar a fonte que deseja usar, digite uma fonte genérica na família e use-a.

#### Estilos de máscara aplicados no editor de temas {#mask-styles-applied-in-theme-editor}

É possível mascarar estilos aplicados em um tema. Na barra lateral do editor de temas, você pode usar o ![toggle_](assets/toggle_eye.png)eyeicon para desativar um estilo aplicado. Por exemplo, se você mudar dimensão um componente em um formulário ou comunicação interativa, é possível usar o botão de máscara à esquerda de uma propriedade para desativá-la. Quando você salva um tema, as opções de máscara selecionadas são mantidas.

![Opção de máscara disponível na barra lateral do editor de temas](assets/mask-styles.png)

O exemplo abaixo mostra estilos mascarados e não mascarados em um tema.

![Canetas mascaradas e não mascaradas](assets/mask2.png)

## Aplicar um tema a um formulário ou comunicação interativa {#applying-a-theme-to-a-form-or-interactive-communication-br}

Para aplicar um tema a um formulário adaptável:

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione-o e clique em **Abrir**.
1. No modo de edição, selecione um componente, clique em nível ![de](assets/field-level.png) campo > Container **de formulário** adaptável e, em seguida, clique em ![cmppr](assets/cmppr.png).

   É possível editar as propriedades do formulário na barra lateral.

1. Na barra lateral, clique em **Estilo**.
1. Selecione seu tema no menu suspenso Tema **de formulário** adaptável e clique no botão de **seleção** Concluído ![](assets/check-button.png).

Para aplicar um tema a uma comunicação interativa:

1. Abra sua comunicação interativa no modo de edição. Para abrir uma comunicação interativa no modo de edição, selecione um formulário e clique em **Abrir**.
1. No modo de edição, selecione um componente, clique em nível ![de](assets/field-level.png) campo > Container **do** Documento e, em seguida, clique em ![cmppr](assets/cmppr.png).

   É possível editar as propriedades do formulário na barra lateral.

1. Na barra lateral, em** Básico**, selecione seu tema no menu suspenso **Tema** e clique no botão de **seleção** Concluído ![.](assets/check-button.png)

### Alterar tema de um formulário em tempo de execução {#change-theme-of-a-form-at-runtime}

Um tema estimula diferentes componentes de um formulário. É possível usar a `themeOverride` propriedade para alterar dinamicamente o tema de um formulário. Um URL típico de um formulário é:

`https://<server>:<port>/content/forms/af/test.html`

Você pode usar o parâmetro subjectOverride para aplicar um tema no tempo de execução.

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

A `themeOverride` opção permite fornecer um caminho para um tema. Altera o tema do formulário e atualiza o formulário com estilos atualizados.

## Obter aparência específica usando Temas {#specific-af-appearance}

Com o AEM Forms, juntamente com o tema de tela predefinido, há muitos outros temas. Se quiser projetar seu formulário ou comunicação interativa usando outros temas, juntamente com alterações adicionais, copie o tema da pasta Biblioteca de Temas. Cole os temas copiados fora da pasta Biblioteca de Temas e edite o tema copiado de acordo com as alterações desejadas.

Para copiar um tema, execute as seguintes etapas:

1. Na instância de criação, navegue até **Adobe Experience Manager > Formulários > Temas**.
1. Abra a pasta Biblioteca de Temas.
1. Na pasta Biblioteca de Temas, passe o ponteiro do mouse sobre o tema predefinido correspondente e toque em **Copiar**.
1. Cole o tema copiado fora da pasta Biblioteca de Temas.
1. Personalize o tema copiado.

Depois de personalizar o tema, aplique-o ao formulário ou à comunicação interativa.

>[!NOTE]
>
>Não modifique os temas disponíveis na pasta Biblioteca de Temas. Esta pasta contém temas do sistema. Todas as alterações feitas nesses temas são substituídas pela instalação de uma versão mais recente ou correção de AEM Forms.

## Impacto em outros casos de uso de formulários adaptáveis {#impact-on-other-adaptive-form-use-cases}

* **Publicar/desfazer a publicação de um formulário:** Ao publicar um formulário, o tema aplicado também é publicado (se ainda não estiver publicado)
* **Importar/exportar um formulário:** Ao importar ou exportar um formulário, seu tema associado também é automaticamente importado ou exportado.
* **Referências de um formulário:** A seção Referências em referências de formulário contém uma entrada extra para o tema.
* **Hora da última modificação de um formulário:** Atualizado quando o tema associado é alterado.
* **Teste A/B:** É possível aplicar um tema diferente a duas versões do formulário em testes A/B. As informações dos dois temas são armazenadas individualmente nos dois container-guia.

## Sequência de geração de CSS {#css-generation-sequence}

Quando você seleciona visualização CSS, o Editor de Temas coleta todas as informações de estilização e cria um CSS. Ele coleta informações na seguinte ordem:

1. Estilo definido na biblioteca de cliente base do tema.
1. Estilo definido pelo usuário, especificado usando as propriedades na barra lateral.
1. Estilo CSS fornecido usando a opção Substituir CSS.

Por exemplo, a cor de fundo de uma caixa de texto é azul na biblioteca de cliente base. Altere-o para rosa usando as propriedades na barra lateral. Ao gerar CSS, você verá a cor de fundo da caixa de texto como rosa. Depois de alterar a cor do plano de fundo usando as propriedades, outro autor usa a opção de substituição CSS para alterar a caixa de texto da cor do plano de fundo como branca. Quando você gera CSS, você vê a cor de fundo como branca no CSS gerado.

## Estilos de depuração {#debugging-styles}

Ao especificar estilos para componentes no Editor de Temas, um CSS é gerado. Quando você estimula um componente genérico, vários componentes incluídos nele também são estilizados. Por exemplo, quando você estimula um campo, a caixa de texto e o rótulo nele também têm o estilo. Quando você estimula a caixa de texto dentro do campo, ela recebe seu próprio CSS. Se você quiser depurar o CSS gerado para o campo e o componente, o Editor de Temas fornece opções que permitem a visualização do CSS.

Você pode ver o CSS gerado usando as seguintes opções:

* **Visualização da opção CSS** na barra lateral: Ao selecionar um componente no Tema, você pode ver a opção CSS de VISUALIZAÇÃO na barra lateral. Mostra o CSS gerado, incluindo o CSS para `::before` e `::after` pseudo-elementos.
* **Opção CSS** do tema da Visualização na barra de ferramentas da tela: Na barra de ferramentas Tela, clique em ![opções](assets/theme-options.png) de tema > CSS **do tema de** Visualização. Você pode ver todo o tema CSS gerado a partir das propriedades definidas no Editor de Temas.

## Solução de problemas, recomendações e práticas recomendadas {#troubleshooting-recommendations-and-best-practices}

* **Como evitar ativos de outro Tema**

   Ao editar um tema, você pode navegar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o plano de fundo de uma página. Por exemplo, ao selecionar **Página** , botão ![de](assets/edit-button.png)edição > **Plano de fundo** > **Adicionar** > **Imagem**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

* Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar navegar e adicionar ativos de outros temas.
* **Usar clientlib base, editor de temas e estilo incorporado**

   * **Clientlib** básico:

      A biblioteca de cliente base contém informações de estilização. Para usar informações de estilização em bibliotecas do lado do cliente em temas.

      1. Navegue até **Experience Manager > Formulários > Temas**.
      1. Na página Temas, selecione um tema e clique em Propriedades **da** Visualização.
      1. Na página Propriedades que é aberta, clique em **Avançado**.
      1. Na guia Avançado, no campo Local do Clientlib, procure e selecione a biblioteca de cliente que deseja usar.
      1. Clique em **Salvar**.
      O estilo especificado na biblioteca do cliente é importado no tema que o utiliza. Por exemplo, você especifica o estilo para caixa de texto, caixa numérica e alternar na biblioteca do cliente. Quando você importa a biblioteca do cliente no tema, o estilo da caixa de texto, da caixa numérica e do switch é importado. Em seguida, é possível estilizar outros componentes usando o editor de temas.
Você também pode criar um tema, criar cópias dele e modificar o estilo fornecido nos temas copiados para casos de uso semelhantes.
Consulte [Obtendo aparência específica usando Temas](#specific-af-appearance)

   * **Editor de temas:**

      O Editor de Temas permite criar temas para criar um estilo no formulário ou para comunicação interativa. Você pode especificar o estilo dos componentes em um tema, que permite a consistência na aparência entre vários formulários ou comunicações interativas desenvolvidas. É recomendável especificar informações de estilização em um tema e aplicar o tema a um formulário.

   * **Estilo em linha:**

      É possível criar um estilo de componentes usando o modo Estilo no editor de formulário ou de comunicação interativa multicanal ao trabalhar com um formulário. Usar o modo de estilo para alterar o estilo do componente de formulário substitui o estilo especificado no tema. Se desejar alterar o estilo de determinados componentes de um formulário específico, consulte Estilo [incorporado dos componentes](../../forms/using/inline-style-adaptive-forms.md).


* **Uso de bibliotecas do lado do cliente**

   Se quiser criar bibliotecas de clientes para importar informações de estilização, consulte [Uso de bibliotecas](/help/sites-developing/clientlibs.md)do lado do cliente. Depois de criar uma biblioteca de cliente, você pode importá-la no seu tema usando as etapas mencionadas acima.

* **Alteração da largura de layout do painel container**

   Não é recomendável alterar a largura de layout do painel container. Quando você especifica a largura de um painel de container, ele se torna estático e não se adapta a diferentes telas.

* **Quando usar o editor de formulário ou editor de tema para trabalhar com cabeçalho e rodapé**

   Use o editor de temas se desejar estilizar o cabeçalho e o rodapé usando opções de estilização, como estilo de fonte, plano de fundo e transparência.
Se desejar fornecer informações como uma imagem de logotipo, nome da empresa no cabeçalho e informações de copyright no rodapé, use as opções do editor de formulário.
