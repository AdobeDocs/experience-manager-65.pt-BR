---
title: Usando o Serviço do Assembler
seo-title: Usando o Serviço do Assembler
description: O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF.
seo-description: O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Usando o Serviço do Assembler{#using-assembler-service}

O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Cada tarefa enviada ao serviço Assembler inclui um documento XML de Descrição de Documento (DDX), documentos de origem e recursos externos (strings e gráficos). Para obter mais informações sobre o serviço de montador, consulte [Visão geral do serviço](../../forms/using/overview-aem-document-services.md#p-assembler-service-p)de montador.

Você pode usar o serviço de montagem para as seguintes operações:

## Montagem de documentos PDF {#assemble-pdf-documents}

Você pode usar o serviço Assembler para montar dois ou mais documentos PDF em um único documento PDF ou Portfólio PDF. Você também pode aplicar recursos ao documento PDF que ajudam na navegação ou aprimoram a segurança. Estas são algumas das maneiras de montar documentos PDF:

### Montagem de um documento PDF simples {#assemble-a-simple-pdf-document}

A ilustração a seguir mostra três documentos de origem sendo mesclados em um único documento resultante.

![Montagem de um documento PDF simples a partir de vários documentos PDF](assets/as_document_assembly.png)

Montagem de um documento PDF simples a partir de vários documentos PDF

O exemplo a seguir é um documento DDX simples usado para montar o documento. Ela especifica os nomes dos documentos de origem usados para produzir o documento resultante, bem como o nome do documento resultante:

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

O conjunto de documentos produz um documento resultante que contém o seguinte conteúdo e\
características:

* Toda ou parte de cada documento de origem
* Todos ou parte dos marcadores de cada documento de origem, normalizados para o documento resultante montado
* Outras características adotadas no documento base (Doc1), incluindo metadados, rótulos de página e tamanho da página
* Como opção, o documento resultante inclui um sumário construído a partir dos marcadores nos documentos de origem

### Criar um portfólio PDF {#create-a-pdf-portfolio}

O serviço Assembler pode criar portfólios PDF que contêm uma coleção de documentos e uma interface de usuário independente. A interface é chamada de Layout de Portfólio PDF ou de um navegador de Portfólio PDF (navegador). Portfólios PDF estendem a capacidade de pacotes PDF adicionando um navegador, pastas e páginas de boas-vindas. A interface pode aprimorar a experiência do usuário aproveitando a sequência de caracteres de texto localizada, esquemas de cores personalizados e recursos gráficos. O Portfólio PDF também pode incluir pastas para organizar os arquivos no portfólio.

Quando o serviço Assembler interpreta o seguinte documento DDX, monta um Portfólio PDF que inclui um navegador de Portfólio PDF e um pacote de dois arquivos. O serviço obtém o navegador a partir do local especificado pela origem myNavigator. Ele altera o esquema de cores padrão do navegador para o esquema de cores rosaScheme.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### Montar documentos criptografados {#assemble-encrypted-documents}

Ao montar um documento, você também pode criptografar o documento PDF com uma senha. Depois que um documento PDF é criptografado com uma senha, o usuário deve especificar a senha para exibir o documento PDF no Adobe Reader ou Acrobat. Para criptografar um documento PDF com uma senha, o documento DX deve conter valores de elemento de criptografia necessários para criptografar um documento PDF.

O serviço de criptografia não precisa fazer parte da instalação do LiveCycle para criptografar um documento PDF com uma senha.

Se um ou mais documentos de entrada estiverem criptografados, forneça uma senha para abrir o documento como parte do DDX.

### Montar documentos usando a numeração de Bates {#assemble-documents-using-bates-numbering}

Ao montar um documento, você pode usar a numeração de Bates para aplicar um identificador de página exclusivo a cada página. Quando você usa a numeração de Bates, a cada página do documento (ou conjunto de documentos) é atribuído um número que identifica exclusivamente a página. Por exemplo, documentos de fabricação que contêm informações da lista de materiais e que estão associados à produção de uma montagem podem conter um identificador. Um número de Bates contém um valor numérico incrementado sequencialmente e um prefixo e sufixo opcionais. O prefixo + valor numérico + sufixo é chamado de padrão de barras.

A ilustração a seguir mostra um documento PDF que contém um identificador exclusivo localizado no cabeçalho do documento.

![Um documento PDF que contém um identificador exclusivo localizado no cabeçalho do documento](do-not-localize/as_batesnumber.png)

Um documento PDF que contém um identificador exclusivo localizado no cabeçalho do documento

### Nivelar e reunir documentos {#flatten-and-assemble-documents}

Você pode usar o serviço Assembler para transformar um documento PDF interativo (por exemplo, um formulário) em um documento PDF não interativo. Um documento PDF interativo permite que os usuários digitem ou modifiquem dados localizados nos campos do documento PDF. O processo de transformação de um documento PDF interativo em um documento PDF não interativo é chamado de nivelamento. Quando um documento PDF é nivelado, os campos de formulário mantêm sua aparência gráfica, mas não são mais interativos. Um motivo para nivelar um documento PDF é garantir que os dados não possam ser modificados. Além disso, os scripts associados aos campos não funcionam mais.

Ao criar um documento PDF que é montado a partir de documentos PDF interativos, o serviço Assembler niza esses formulários antes de montá-los no documento resultante.

>[!NOTE]
>
>O serviço Assembler usa o serviço de Saída para nivelar formulários XFA dinâmicos. Se o serviço Assembler processar um DDX que exija que ele achate um formulário dinâmico XFA e o serviço de Saída não estiver disponível, uma exceção será lançada. O serviço Assembler pode nivelar um formulário Acrobat ou um formulário XFA estático sem usar o serviço de Saída.

## Montar documentos XDP {#assemble-xdp-documents}

Você pode usar o serviço Assembler para reunir vários documentos XDP em um único documento XDP ou em um documento PDF. Para arquivos XDP de origem que incluem pontos de inserção, você pode especificar os fragmentos a serem inseridos.

Estas são algumas das maneiras de montar documentos XDP:

### Montagem de um documento XDP simples {#assemble-a-simple-xdp-document}

A ilustração a seguir mostra três documentos XDP de origem sendo montados em um único documento XDP resultante. O documento XDP resultante contém os três documentos XDP de origem, incluindo seus dados associados. O documento resultante obtém atributos básicos do documento base, que é o primeiro documento XDP de origem.

![Montagem de um documento XDP simples de vários documentos XDP](assets/as_assembler_xdpassembly.png)

Montagem de um documento XDP simples de vários documentos XDP

Este é um documento DDX que produz o resultado ilustrado acima.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### Resolvendo referências durante a montagem {#resolving-references-during-assembly}

Normalmente, os documentos XDP podem conter imagens referenciadas por meio de referências absolutas ou relativas. Por padrão, o serviço de montador retém as referências às imagens no documento XDP resultante.

Você pode especificar como o serviço Assembler manipula as imagens referenciadas nos documentos XDP de origem por meio de referências absolutas ou relativas nos arquivos XDP durante a montagem. É possível optar por incorporar todas as imagens no resultado para que não contenham referências relativas ou absolutas. Você define isso definindo o valor da tag resolveAssets, que pode ter qualquer uma das opções a seguir. Por padrão, nenhuma referência é resolvida no documento de resultado.

<table>
 <tbody> 
  <tr> 
   <th>Valor</th> 
   <th>Descrição</th> 
  </tr> 
  <tr> 
   <td>nenhum</td> 
   <td>Não resolve nenhuma referência.</td> 
  </tr> 
  <tr> 
   <td>all</td> 
   <td>Incorpora todas as imagens referenciadas no documento XDP de origem.</td> 
  </tr> 
  <tr> 
   <td>relativo</td> 
   <td>Incorpora todas as imagens referenciadas por meio de referências relativas no documento XDP<br /> de origem.</td> 
  </tr> 
  <tr> 
   <td>absoluto</td> 
   <td>Incorpora todas as imagens referenciadas por meio de referências absolutas no documento XDP<br /> de origem.</td> 
  </tr> 
 </tbody> 
</table>

Você pode especificar o valor do atributo resolveAssets na tag de origem XDP ou na tag de resultado XDP pai. Se o atributo for especificado para a tag de resultado XDP, ele será herdado por todos os elementos de origem XDP que são filhos do resultado XDP. No entanto, especificar explicitamente o atributo para um elemento de origem substitui a configuração do elemento de resultado somente para esse documento de origem.

#### Resolver todas as referências de origem em um documento XDP {#resolve-all-source-references-in-an-xdp-document}

Para resolver todas as referências nos documentos XDP de origem, especifique o atributo resolveAssets para a variável\
documento resultante para todos, como no exemplo abaixo:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

Você também pode especificar o atributo para todos os documentos XDP de origem independentemente para obter o mesmo\
resultado.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### Resolver referências de origem selecionadas em um documento XDP {#resolve-selected-source-references-in-an-xdp-document}

Você pode especificar seletivamente as referências de origem que deseja resolver especificando o atributo resolveAssets para elas. Os atributos para documentos de origem individuais substituem a configuração resultante do documento XDP. Neste exemplo, os fragmentos incluídos também são resolvidos.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### Resolver seletivamente referências absolutas ou relativas {#selectively-resolve-absolute-or-relative-references}

Você pode resolver seletivamente referências absolutas ou relativas em todos ou alguns documentos de origem, como mostrado no exemplo abaixo:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### Inserir dinamicamente fragmentos de formulário em um formulário XFA {#dynamically-insert-form-fragments-into-an-xfa-form}

Você pode usar o serviço Assembler para criar um formulário XFA criado a partir de outro formulário XFA no qual os fragmentos são inseridos. Usando esse recurso, é possível usar fragmentos para criar vários formulários.

O suporte para inserção dinâmica de fragmentos de formulário oferece suporte ao controle de origem única. Você mantém uma única fonte de componentes usados com frequência. Por exemplo, você pode criar um fragmento para o banner da sua empresa. Se o banner mudar, você só precisará modificar o fragmento. Os outros formulários que incluem o fragmento não são alterados.

Os designers de formulário usam o LiveCycle Designer para criar fragmentos de formulário. Esses fragmentos são subformulários nomeados exclusivamente em um formulário XFA. Os designers de formulário também usam o Designer para criar formulários XFA que têm pontos de inserção nomeados exclusivamente. Você (o programador) grava documentos DX que especificam como os fragmentos são inseridos no formulário XFA.

A ilustração a seguir mostra dois formulários XML (modelos XFA). O formulário à esquerda contém um ponto de inserção chamado myInsertionPoint. O formulário à direita contém um fragmento chamado myFragment.

![Inserir fragmentos de formulário em um formulário XFA](assets/as_assembler_fragment_assy_assembled.png)

Inserir fragmentos de formulário em um formulário XFA

Quando o serviço Assembler interpreta o seguinte documento DDX, ele cria um formulário XML que contém outro formulário XML. O subformulário myFragment do documento myFragmentSource é inserido no myInsertionPoint no documento myFormSource.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### Compactar um documento XDP como PDF {#package-an-xdp-document-as-pdf}

Você pode usar o serviço Assembler para empacotar um documento XDP como um documento PDF, conforme mostrado neste documento DDX.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## Desmontar documentos PDF {#disassemble-pdf-documents}

Você pode usar o serviço Assembler para desmontar um documento PDF. O serviço pode extrair páginas do documento de origem ou dividir um documento de origem com base em marcadores. Normalmente, essa tarefa é útil se o documento PDF foi criado originalmente de muitos documentos individuais, como uma coleção de declarações.

### Extrair páginas de um documento de origem {#extract-pages-from-a-source-document}

Na ilustração a seguir, as páginas 1 a 3 são extraídas do documento de origem e colocadas em um novo documento resultante.

![Extrair páginas específicas de um documento de origem](assets/as_intro_page_extraction.png)

Extrair páginas específicas de um documento de origem

O exemplo a seguir é um documento DDX usado para desmontar o documento.

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### Dividir um documento de origem com base em marcadores {#divide-a-source-document-based-on-bookmarks}

Na ilustração a seguir, o DocA é dividido em vários documentos resultantes. O primeiro marcador de nível 1 em uma página identifica o início de um novo documento resultante.

![Dividir um documento de origem com base em marcadores em vários documentos](assets/as_intro_pdfsfrombookmarks.png)

Dividir um documento de origem com base em marcadores em vários documentos

O exemplo a seguir é um documento DDX que usa marcadores para desmontar um documento de origem.

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## Determine se os documentos são compatíveis com PDF/A {#determine-whether-documents-are-pdf-a-compliant}

Você pode usar o serviço Assembler para determinar se um documento PDF é compatível com PDF/A. O PDF/A é um formato de arquivo destinado à preservação de longo prazo do conteúdo do documento. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

## Obter informações sobre um documento PDF {#obtain-information-about-a-pdf-document}

Você pode usar o serviço Assembler para obter as seguintes informações sobre um documento PDF:

* Informações de texto.

   * Palavras em cada página do documento
   * Posição de cada palavra em cada página do documento
   * Frases em cada parágrafo de cada página do documento

* Marcadores, incluindo o número da página, o título, o destino e a aparência. Você pode exportar isso\
   dados de um documento PDF e importá-los para um documento PDF.

* Anexos de arquivo, incluindo informações de arquivo. Para anexos em nível de página, também inclui a variável\
   localização da anotação do anexo de arquivo. É possível exportar esses dados de um documento PDF e\
   importe-o para um documento PDF.

* Empacotar arquivos, incluindo informações de arquivo, pastas, pacote, esquema e dados de campo. É possível exportar esses dados de um documento PDF e importá-los para um documento PDF.

## Validar documentos DDX {#validate-ddx-documents}

Você pode usar o serviço Assembler para determinar se um documento DX é válido. Por exemplo, se você atualizou de uma versão anterior do LiveCycle, a validação garante que o documento DX seja válido.

## Ligar para outros serviços {#call-other-services}

Você pode usar documentos DDX que fazem com que o serviço Assembler chame os seguintes serviços do LiveC ycle. O serviço Assembler pode chamar apenas os serviços instalados com o LiveCycle.

**Serviço** do Reader Extensions: Permite que os usuários do Adobe Reader assinem digitalmente o documento PDF resultante.

**Serviço** de formulários: Une um arquivo XDP e um arquivo de dados XML para produzir um documento PDF que contenha o formulário interativo preenchido.

**Serviço** de saída: Converte um formulário XML dinâmico em um documento PDF que contém um formulário não interativo (acelera o formulário). O serviço Assembler nivela formulários XML estáticos e formulários Acrobat sem chamar o serviço de Saída.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

O uso do DDX e do serviço Assembler para chamar outros serviços do LiveC ycle pode simplificar o diagrama do processo. Ele pode até reduzir o esforço que você gasta personalizando seus fluxos de trabalho. (Consulte também
