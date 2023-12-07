---
title: Dicionários de dados
description: O Dicionário de dados no Gerenciamento de correspondência permite integrar dados de back-end a cartas como entradas para uso na correspondência com o cliente.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 0%

---

# Dicionários de dados{#data-dictionary}

## Introdução {#introduction}

Um dicionário de dados permite que os usuários empresariais usem informações de fontes de dados de back-end sem conhecer detalhes técnicos sobre seus modelos de dados subjacentes. Um dicionário de dados é composto de elementos do dicionário de dados (DDEs). Você usa esses elementos de dados para integrar dados de back-end às cartas como entrada para uso em uma correspondência com o cliente.

Um dicionário de dados é uma representação independente de metadados que descreve as estruturas de dados subjacentes e seus atributos associados. Um dicionário de dados é criado usando o vocabulário empresarial. Ele pode ser mapeado para um ou mais modelos de dados subjacentes.

O dicionário de dados é composto de elementos de três tipos: Simples, Composto e Elementos de coleção. DDEs simples são elementos primitivos, como sequências, números, datas e valores booleanos que armazenam informações como o nome de uma cidade. Um DDE composto contém outros DDEs, que podem ser do tipo primitivo, composto ou coleção. Por exemplo, um endereço, que consiste em um endereço de rua, cidade, província, país e código postal. Uma coleção é uma lista de DDEs simples ou compostos semelhantes. Por exemplo, um cliente com vários locais ou endereços de cobrança e entrega diferentes.

O Gerenciamento de correspondência usa os dados específicos do back-end, cliente ou destinatário armazenados de acordo com a estrutura do dicionário de dados para criar correspondência destinada a clientes diferentes. Por exemplo, um documento pode ser criado com nomes amigáveis, como &quot;Prezado(a) {Nome}&quot;,&quot;Sr. {Last Name}&quot;.

Normalmente, os usuários empresariais não exigem conhecimento de representações de metadados, como XSD (esquema XML) e classes Java. No entanto, geralmente exigem acesso a essas estruturas de dados e atributos para criar soluções.

### Fluxo de trabalho do Dicionário de dados {#data-dictionary-workflow}

1. Um autor [cria o dicionário de dados](#createdatadictionary) fazendo upload de um esquema ou do zero.
1. O Autor cria cartas e Comunicações interativas com base no dicionário de dados e associa os elementos do dicionário de dados em cartas e Comunicações interativas sempre que necessário.
1. Um autor pode baixar um arquivo XML de dados de amostra, que se baseia no esquema de um dicionário de dados. O autor pode modificar o arquivo XML de dados de amostra, que pode ser associado como dados de teste ao dicionário de dados. O mesmo é usado durante a pré-visualização de cartas.
1. Enquanto [pré-visualização de uma carta](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p), um Autor escolhe visualizar a carta com dados (Visualização personalizada). A carta é aberta pré-preenchida com os dados fornecidos pelo Autor. Isso é aberto na interface criar correspondência. O agente que está visualizando esta carta pode modificar o conteúdo, os dados e os anexos nesta carta e pode enviar a carta final. Para obter mais informações sobre a criação de cartas, consulte [Criar correspondência](../../forms/using/create-letter.md).

## Pré-requisitos {#prerequisite}

Instale o [Pacote de compatibilidade](compatibility-package.md) para exibir o **Dicionários de dados** opção no **Forms** página.

## Criar um dicionário de dados {#createdatadictionary}

Você usa o Editor de dicionário de dados para criar um dicionário de dados ou pode fazer upload de um arquivo de esquema XSD para criar um dicionário de dados com base nele. É possível estender o dicionário de dados adicionando mais informações necessárias, incluindo campos. Independentemente de como o dicionário de dados foi criado, o proprietário do processo de negócios não precisa ter conhecimento dos sistemas back-end. O proprietário do processo de negócios precisa apenas do conhecimento dos objetos de domínio e de suas definições para o processo.

>[!NOTE]
>
>Para várias correspondências que exigem elementos semelhantes, é possível criar um dicionário de dados comum. No entanto, um grande dicionário de dados com um grande número de elementos pode causar problemas de desempenho ao usar o dicionário de dados e carregar os elementos, como em cartas e fragmentos de documentos. Se você tiver problemas de desempenho, tente criar dicionários de dados separados para cartas diferentes.

1. Selecionar **Forms** > **Dicionários de dados**.
1. Selecionar **Criar dicionário de dados**.
1. Na tela Propriedades, adicione o seguinte:

   * **Título:** (Opcional) Insira o título do dicionário de dados. O título não precisa ser exclusivo e pode ter caracteres especiais e caracteres que não estejam em inglês. Cartas e outros fragmentos de documentos são referenciados com seu título (quando disponível), como em miniaturas e propriedades de ativos. Os dicionários de dados são referenciados com seus nomes e não títulos.
   * **Nome:** O nome exclusivo do dicionário de dados. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título e os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.

   * **Descrição**: (Opcional) Descrição do dicionário de dados.
   * **Tags:** (Opcional) Para criar uma tag personalizada, insira o valor no campo de texto e pressione Enter. Você pode ver sua tag abaixo do campo de texto das tags. Quando você salva esse texto, as tags recém-adicionadas também são criadas.
   * **Propriedades estendidas**: (Opcional) Selecione **Adicionar campo** para especificar atributos de metadados para o seu dicionário de dados. Na coluna Nome da propriedade, digite um nome de propriedade exclusivo. Na coluna Valor, insira um valor para associar à propriedade.

   ![Propriedades do dicionário de dados especificadas em alemão](do-not-localize/1_ddproperties.png)

1. (Opcional) Para fazer upload de uma definição de esquema XSD para o seu dicionário de dados, no painel Estrutura do dicionário de dados, selecione **Fazer upload do esquema XML**. Navegue até o arquivo XSD, selecione-o e **Abertura**. Um dicionário de dados é criado com base no esquema XML carregado. Você precisa ajustar os nomes de exibição e as descrições dos elementos no dicionário de dados. Para fazer isso, selecione os nomes dos elementos tocando neles e edite suas descrições, nomes de exibição e outros detalhes nos campos no painel direito.

   Para obter mais informações sobre Elementos de DD Calculados, consulte [Elementos do dicionário de dados computados](#computedddelements).

   >[!NOTE]
   >
   >Você pode ignorar o upload do arquivo de esquema e criar seu dicionário de dados do zero usando a interface do usuário do. Para fazer isso, pule esta etapa e continue com as próximas etapas.

1. Selecione **Próximo**.
1. Na tela Adicionar propriedades, adicione os elementos ao dicionário de dados. Também é possível adicionar/excluir elementos e editar seus detalhes se você tiver carregado um esquema para obter uma estrutura básica do dicionário de dados.

   Você pode selecionar os três pontos no lado direito de um elemento e adicionar um elemento à estrutura do dicionário de dados.

   ![1_2_createanelement](assets/1_2_createanelement.png)

   Selecione Elemento Composto, Elemento de Coleta ou Elemento Primitivo.

   * Um DDE composto contém outros DDEs, que podem ser do tipo primitivo, composto ou coleção. Por exemplo, um endereço, que consiste em um endereço de rua, cidade, província, país e código postal.
   * Os DDEs primitivos são elementos, como sequências, números, datas e valores booleanos que contêm informações, como um nome de cidade.
   * Uma coleção é uma lista de DDEs simples ou compostos semelhantes. Por exemplo, um cliente com vários locais ou endereços de cobrança e entrega diferentes.

   Veja a seguir algumas regras para criar um dicionário de dados:

   * Somente o tipo composto é permitido como DDE de nível superior em um dicionário de dados.
   * Nome, nome de referência e tipo de elemento são campos obrigatórios para um dicionário de dados e DDEs.
   * O nome da referência deve ser exclusivo.
   * Um DDE pai (composto) não pode ter dois filhos com o mesmo nome.
   * Enumerações contêm apenas tipos de String primitivos.

   Para obter mais informações sobre os elementos Composto, Coleção e Primitivo e trabalhar com elementos do dicionário de dados, consulte [Mapeando elementos do dicionário de dados para o esquema XML](#mappingddetoschema).

   Para obter informações sobre validações no Dicionário de dados, consulte [Validações do Editor do dicionário de dados](#ddvalidations).

   ![2_addddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. (Opcional) Depois de selecionar um elemento, na guia Avançado você pode adicionar propriedades (atributos). Também é possível selecionar **Adicionar campo** e estenda as propriedades de um elemento DD.

   ![3_addddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. (Opcional) Você pode remover qualquer elemento tocando nos três pontos no lado direito de um elemento e selecionando **Excluir**.

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >A exclusão de um elemento composto/de coleção com nós filhos também exclui seus nós filhos.

1. (Opcional) Selecione um elemento no painel Estrutura do dicionário de dados e no painel Lista de campos e variáveis. Altere ou adicione atributos necessários associados ao elemento.
1. Selecione **Salvar**.

### Criar cópias de um ou mais dicionários de dados {#create-copies-of-one-or-more-data-dictionary}

Para criar rapidamente um ou mais dicionários de dados com propriedades e elementos semelhantes aos dicionários de dados existentes, você pode copiá-los e colá-los.

1. Na lista de dicionários de dados, selecione os dicionários de dados apropriados. A interface do usuário do exibe o ícone Copiar.
1. Selecione Copiar. A interface exibe o ícone Colar.
1. Selecione Colar. A caixa de diálogo Colar é exibida. O sistema atribui automaticamente nomes e títulos aos novos dicionários de dados.
1. Se necessário, edite o Título e o Nome com os quais deseja salvar a cópia do dicionário de dados.
1. Selecione Colar. A cópia do dicionário de dados é criada. Agora você pode fazer as alterações necessárias no dicionário de dados recém-criado.

## Consulte os fragmentos ou documentos do documento que se referem a um elemento do Dicionário de dados {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

Ao editar ou exibir um dicionário de dados, você pode ver quais elementos do dicionário de dados são referenciados em quais Textos, Condições, Letras e Comunicações interativas.

1. Siga um destes procedimentos para editar o dicionário de dados:

   * Passe o mouse sobre um dicionário de dados e selecione Editar.
   * Selecione um dicionário de dados e, em seguida, selecione Editar no cabeçalho.
   * Passe o mouse sobre um dicionário de dados e selecione Selecionar. Em seguida, selecione Editar no cabeçalho.

   Ou selecione em um dicionário de dados para visualizá-lo.

1. No dicionário de dados, selecione um elemento simples para selecioná-lo. Elementos compostos e de coleção não têm referências.

   Juntamente com as propriedades Básicas e Avançadas do elemento, o Conteúdo Emprestado também é exibido.

1. Selecione Conteúdo Emprestado.

   A guia Conteúdo Emprestado é exibida com o seguinte: Textos, Condições, Cartas e Comunicações interativas. Cada um desses cabeçalhos também exibe o número de referências ao elemento selecionado.

1. Selecione um cabeçalho para ver o nome dos ativos que se referem ao elemento.

   ![lentcontent](assets/lentcontent.png)

1. Para exibir o conteúdo concedido de outro elemento, selecione o elemento.
1. Para exibir um ativo que se refere ao elemento, selecione no nome. O navegador exibe o ativo, a carta ou a Comunicação interativa.

## Trabalho com dados de teste {#working-with-test-data}

1. Na página Dicionários de dados, selecione **Selecionar**.
1. Selecione um dicionário de dados para o qual deseja baixar dados de teste e selecione **Baixar dados de amostra XML**.
1. Selecionar **OK** na mensagem de alerta. Um arquivo XML é baixado.
1. Abra o arquivo XML com o Bloco de notas ou outro editor XML. O arquivo XML tem a mesma estrutura que o dicionário de dados e as strings de espaço reservado nos elementos. Substitua as cadeias de caracteres de espaço reservado pelos dados com os quais deseja testar uma letra.

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >Neste exemplo, o XML cria espaço para três valores para um elemento de coleção, mas o número de valores pode ser aumentado/diminuído de acordo com o requisito.

1. Depois de fazer as entradas de dados, você pode usar esse arquivo XML ao visualizar uma correspondência com dados de teste.

   Você pode adicionar esses dados de teste com DD (selecione DD e selecione Fazer upload de dados de teste e fazer upload deste arquivo xml). Assim, depois disso, quando você visualiza a correspondência normalmente (não personalizada), esses dados XML são usados na correspondência. Você também pode selecionar Personalizado e fazer upload desse XML.

## Amostras {#samples}

Os exemplos de código a seguir mostram os detalhes de implementação do Dicionário de dados.

### Exemplo de esquema que pode ser carregado no dicionário de dados {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## Atributos comuns associados a um DDE {#common-attributes-associated-with-a-dde}

A tabela a seguir detalha os atributos comuns associados a um DDE:

<table>
 <tbody>
  <tr>
   <td><strong>Atributo</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>String</td>
   <td>Obrigatório.<br /> Nome do DDE. Ele deve ser exclusivo.</td>
  </tr>
  <tr>
   <td>Referência<br /> Nome</td>
   <td>String</td>
   <td>Obrigatório. Nome de referência exclusivo para o DDE, permitindo referências ao DDE que são independentes de alterações na hierarquia ou na estrutura do dicionário de dados. Os módulos de texto são mapeados usando este nome</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>String</td>
   <td>Um nome amigável opcional do DDE.</td>
  </tr>
  <tr>
   <td>descrição</td>
   <td>String</td>
   <td>Descrição do DDE.</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>String</td>
   <td>Obrigatório. O tipo de DDE: STRING, NUMBER, DATE, Boolean, COMPOSITE, COLLECTION.</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>String</td>
   <td>O subtipo para DDE: ENUM. Permitido somente para STRING e NUMBER elementType.</td>
  </tr>
  <tr>
   <td>Chave</td>
   <td>Booleano</td>
   <td>Um campo booleano para indicar se um DDE é um elemento principal.</td>
  </tr>
  <tr>
   <td>Computado</td>
   <td>Booleano</td>
   <td>Um campo booleano para indicar se um DDE é calculado. Um valor DDE calculado é uma função de outros valores DDE. Por padrão, expressões jsp são suportadas.</td>
  </tr>
  <tr>
   <td>expressão</td>
   <td>String</td>
   <td>A expressão para o DDE "calculado". O serviço de avaliação de expressão enviado por padrão oferece suporte a expressões JSP EL. Você pode substituir o serviço de expressão por uma implementação personalizada.</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>Lista</td>
   <td>Um conjunto de valores permitidos para um DDE do tipo Enum. Por exemplo, o tipo de conta pode ter somente valores (Salvando, Atual).</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>Objeto</td>
   <td>Um Mapa de propriedades personalizadas adicionado ao DDE (específico da interface do usuário ou qualquer outra informação).</td>
  </tr>
  <tr>
   <td>Obrigatório</td>
   <td>Booleano</td>
   <td>O sinalizador indica que a origem dos dados da instância correspondentes ao dicionário de dados deve conter o valor desse DDE específico.</td>
  </tr>
  <tr>
   <td>Vínculo</td>
   <td>BindingElement</td>
   <td>A vinculação XML ou Java do elemento.</td>
  </tr>
 </tbody>
</table>

### Elementos do dicionário de dados computados {#computedddelements}

Um dicionário de dados também pode incluir elementos calculados. Um elemento do dicionário de dados calculado é sempre associado a uma expressão. Essa expressão é avaliada para obter o valor de um elemento do dicionário de dados no tempo de execução. Um valor DDE calculado é uma função de outros valores ou literais DDE. Por padrão, as expressões JSP Expression Language (EL) são suportadas. As expressões EL usam os caracteres ${ } e as expressões válidas podem incluir literais, operadores, variáveis (referências a elementos do dicionário de dados) e chamadas de função. Ao fazer referência a um elemento do dicionário de dados na expressão, o nome de referência do DDE é usado. O nome de referência é exclusivo para cada elemento do dicionário de dados em um dicionário de dados.

Um PersonFullName DDE calculado pode ser associado a uma expressão de concatenação EL, como ${PersonFirstName} ${PersonLastName}.

## Mapeamento de tipo de dados entre XSD e dicionário de dados {#data-type-mapping-between-xsd-and-data-dictionary-br}

A exportação de um XSD requer um mapeamento de dados específico, que é detalhado na tabela a seguir. A coluna DDI indica o tipo do valor DDE como disponível no DDI.

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>Dicionário de dados <br /> </p> </td>
   <td>DDI (Tipo de Dados de Valor da Instância)<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs:elemento do tipo - Tipo composto<br /> </p> </td>
   <td>DDE de tipo - COMPOSITE<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:element onde maxOccurs &gt; 1<br /> </p> </td>
   <td>DDE de tipo - COLEÇÃO-<br /> Um nó DDE é criado ao lado do DDE COLEÇÃO que captura informações do nó COLEÇÃO pai. O mesmo é criado para ambas as coleções de tipos de dados simples/composto. Sempre que você tem uma COLEÇÃO do tipo composto, a árvore do Dicionário de dados captura os campos constituintes nos filhos do DDE criado para capturar informações do tipo.<br /> - DDE (COLEÇÃO)<br /> - DDE(COMPOSITE para informações de tipo)<br /> - Campo DDE(STRING)1<br /> - Campo DDE(STRING) 2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>Atributo do tipo - xs:id <br /> </p> </td>
   <td>DDE de tipo - STRING <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs:string</p> </td>
   <td>DDE de tipo - STRING<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs: boolean <br /> </td>
   <td>DDE de tipo - Booleano <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs:date </td>
   <td>DDE de tipo - DATE </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs:integer </td>
   <td>DDE de tipo - NÚMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs:long</td>
   <td>DDE de tipo - NÚMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element of type - xs:double</td>
   <td>DDE de tipo - NÚMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>Elemento do tipo enum e baseType - xs:string</td>
   <td>DDE de<br /> type - STRING<br /> subtipo - ENUM<br /> valueSet - os valores permitidos para ENUM<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## Baixar um arquivo de dados de amostra de um dicionário de dados {#download-a-sample-data-file-from-a-data-dictionary}

Depois de criar um dicionário de dados, você pode baixá-lo como um arquivo de dados de amostra XML para fazer entradas de texto nele.

1. Na página Dicionários de dados, selecione **Selecionar** e, em seguida, selecione um dicionário de dados para selecioná-lo.
1. Selecionar **Baixar dados de amostra XML**.
1. Selecionar **OK** na mensagem de alerta.

   O Gerenciamento de correspondências cria um arquivo XML com base na estrutura do dicionário de dados selecionado e faz o download desse arquivo para seu computador com o nome &lt;data-dictionary-name>-Dados de amostra. Agora é possível editar esse arquivo em um editor de texto ou XML para fazer entradas de dados enquanto [criação de uma carta](../../forms/using/create-letter.md).

## Internacionalização de metadados {#internationalization-of-meta-data}

Quando quiser enviar a mesma carta em idiomas diferentes para os clientes, você poderá localizar o nome de exibição, a descrição e os conjuntos de valores de enumeração do Dicionário de dados e dos Elementos do dicionário de dados.

### Localizar dicionário de dados {#localize-data-dictionary}

1. Na página Dicionários de dados, selecione **Selecionar** e, em seguida, selecione um dicionário de dados para selecioná-lo.
1. Selecionar **Baixar dados de localização**.
1. Selecionar **OK** no alerta. O Gerenciamento de correspondências baixa um arquivo zip para seu computador com o nome DataDictionary-&lt;ddname>.zip.
1. O arquivo Zip contém um arquivo .properties. Esse arquivo define o dicionário de dados baixado. O conteúdo do arquivo de propriedade é semelhante ao seguinte:

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   A estrutura do arquivo de propriedades define uma linha para cada descrição e o nome de exibição do dicionário de dados, bem como cada elemento do dicionário de dados. Além disso, o arquivo de propriedades define uma linha para um valor de enumeração definido para cada elemento do dicionário de dados. Assim como em um dicionário de dados, o arquivo de propriedades correspondente pode ter várias definições de elementos do dicionário de dados. Além disso, o arquivo pode conter as definições de um ou mais conjuntos de valores de enumeração.

1. Para atualizar o arquivo .properties em um local diferente, atualize o nome de exibição e os valores de descrição no arquivo. Crie mais instâncias do arquivo para cada idioma que você deseja traduzir. Somente os idiomas francês, alemão, japonês e inglês são suportados.

1. Salve os diferentes arquivos de propriedades atualizados com os seguintes nomes:

   _fr_FR.properties Francês

   _de_DE.properties Alemão

   _ja_JA.properties Japonês

   _en_EN.properties Inglês

1. Arquive o arquivo .properties (ou arquivos para várias localidades) em um único arquivo .zip.

1. Na página Dicionários de dados, selecione **Mais** > **Carregar dados de localização** e selecione o arquivo zip com os arquivos de propriedades localizados.
1. Para exibir as alterações de localização, altere o local do navegador.

## Validações do dicionário de dados {#ddvalidations}

O Editor do dicionário de dados aplica as seguintes validações ao criar ou atualizar um dicionário de dados.

* Somente o tipo composto é permitido como Elemento de nível superior em um dicionário de dados.
* Elementos compostos e de coleção não são permitidos no nível folha. Somente elementos Primitivos (String, Date, Number, Boolean) são permitidos no nível folha. Essa validação garante que não haja nenhum elemento composto e de coleção sem um DDE filho.
* Ao fazer upload de um arquivo XSD para criar um dicionário de dados, o Editor do dicionário de dados solicita um elemento de nível superior, se houver vários, para criar o dicionário de dados.
* O nome é o único parâmetro necessário para um dicionário de dados.
* Um DDE pai (composto) não pode ter dois filhos com o mesmo nome
* Garante que um DDE seja marcado como computado, somente se não for um parâmetro obrigatório. Um elemento necessário não pode ser calculado e um elemento calculado não pode ser necessário. Além disso, a coleção e o elemento composto não podem ser elementos computados.
* Garante que um DDE seja marcado como obrigatório, somente quando não for calculado. Também garante que não seja o &quot;collectionElement&quot; que indica o tipo de Coleção (que são os únicos filhos de um Elemento de coleção).
* Chaves vazias ou chaves duplicadas não são permitidas em extendedProperties para um dicionário de dados ou DDE.
* Não use os caracteres dois pontos (:) ou barra vertical (|) dentro da chave ou valor de uma propriedade estendida. Não há validação para o uso desses caracteres proibidos.

Validações aplicadas no nível do dicionário de dados

* O nome do dicionário de dados não deve ser nulo.
* O nome do dicionário de dados deve conter apenas caracteres alfanuméricos.
* A lista de elementos secundários no Dicionário de Dados não deve ser nula ou vazia.
* O dicionário de dados não deve conter mais de um elemento de dicionário de dados de nível superior.
* Somente o tipo composto é permitido como Elemento de nível superior em um Dicionário de dados.

Validações aplicadas no Nível do Elemento do Dicionário de Dados.

* Todos os nomes DDE não devem ser nulos e não devem conter espaços.
* Todos os DDEs devem ter um tipo de elemento &quot;não nulo/não nulo&quot;.
* Todos os nomes de referência DDE não devem ser nulos.
* Todos os nomes de referência DDE devem ser exclusivos.
* Todas as referências DDE devem conter apenas caracteres alfanuméricos e &quot;_&quot;.
* Todos os nomes de exibição DDE devem conter apenas caracteres alfanuméricos e &quot;_&quot;.
* Elementos compostos e de coleção não são permitidos no nível folha. Somente elementos Primitivos (String, Date, Number, Boolean) são permitidos no nível folha. Essa validação garante que não haja nenhum elemento composto e de coleção sem um DDE filho.
* Um DDE pai composto não deve ter dois elementos filho com o mesmo nome.
* O subtipo ENUM é usado apenas para elementos String e Number.
* Os elementos Collection e Composite não podem ser computados.
* Um DDE não pode ser computado e necessário ao mesmo tempo.
* DDEs computados devem conter uma expressão válida.
* DDEs computados não devem ter vínculo XML.
* Um DDE que denota o tipo de um DDE de coleção não pode ser calculado ou exigido.
* DDEs do subtipo ENUM não devem conter conjuntos de valores nulos ou vazios.
* A associação XML de um DDE de coleção não deve mapear para um atributo.
* A sintaxe da vinculação XML deve ser válida; por exemplo, somente um @ é exibido, o @ só é permitido quando seguido por um nome de atributo.

## Mapeamento de elementos do dicionário de dados para o esquema XML {#mappingddetoschema}

Você pode criar um dicionário de dados a partir de um esquema XML ou criá-lo usando a interface do usuário do dicionário de dados. Todos os elementos do dicionário de dados (DDEs) em um dicionário de dados têm um campo Ligação XML para armazenar a ligação do DDE a um elemento no esquema XML. A vinculação em cada DDE é relativa ao DDE principal.

Os seguintes modelos de amostra de detalhes e amostras de código que mostram detalhes de implementação do Dicionário de dados.

## Mapeamento de elementos simples (primitivos) {#mapping-simple-primitive-elements}

Um DDE primitivo representa um campo ou atributo que é de natureza atômica. DDEs primitivos definidos fora do escopo de um tipo complexo (DDE composto) ou um elemento repetitivo (DDE coleção) podem ser armazenados em qualquer local dentro do Esquema XML. A localização dos dados correspondentes a um DDE primitivo não depende do mapeamento de seu DDE pai. O DDE primitivo usa as informações de mapeamento do campo Vinculação XML para determinar seu valor e os mapeamentos são traduzidos em um dos seguintes:

* um atributo
* um elemento
* um contexto de texto
* nada (um DDE ignorado)

O exemplo a seguir mostra um schema simples.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **Elemento do dicionário de dados** | **Vínculo XML padrão** |
|---|---|
| idade | /age |
| preço | /price |

### Mapeamento de elementos compostos {#mapping-composite-elements}

A associação não é suportada para elementos Composite; se a associação for fornecida, ela será ignorada. A ligação para todos os DDEs filho constituintes do tipo primitivo deve ser absoluta. Permitir o mapeamento absoluto para elementos filhos de um DDE composto fornece mais flexibilidade em termos de XPath Binding. Mapear um DDE composto para um elemento de tipo complexo no esquema XML limita o escopo de vinculação para seus elementos filhos.

O exemplo a seguir mostra o schema para uma observação.

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>Elemento do dicionário de dados</strong></td>
   <td><strong>Vínculo XML padrão</strong></td>
  </tr>
  <tr>
   <td>observação</td>
   <td>vazio (nulo)<br /> </td>
  </tr>
  <tr>
   <td>para</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>de</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>cabeçalho</td>
   <td>/note/header</td>
  </tr>
  <tr>
   <td>corpo</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### Mapeando Elementos de Coleta {#mapping-collection-elements}

Um elemento de coleção só é mapeado para outro elemento de coleção com cardinalidade > 1. Os DDEs filhos de um DDE de coleção têm uma Ligação XML relativa (local) em relação à Ligação XML do pai. Como os DDEs filhos de um elemento de coleção devem ter a mesma cardinalidade que o pai, a associação relativa é exigida para garantir a restrição de cardinalidade para que os DDEs filhos não apontem para um elemento de Esquema XML não repetitivo. No exemplo abaixo, a cardinalidade de &quot;TokenID&quot; deve ser igual a &quot;Tokens&quot;, que é a coleção principal DDE.

Ao mapear um DDE de coleção para um elemento do esquema XML:

* o vínculo para o DDE correspondente ao elemento Collection deve ser o XPath absoluto

* Não forneça nenhuma vinculação para o DDE que representa o tipo de elemento Collection. Se fornecido, a vinculação será ignorada.

* A associação para todos os DDEs filhos do elemento Collection deve ser relativa ao elemento Collection pai.

O Esquema XML abaixo declara um elemento com o nome Tokens e um atributo maxOccurs de &quot;unbounded&quot;. Assim, Tokens é um elemento de coleção.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

O Token.xsd associado a esta amostra seria:

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **Elemento do dicionário de dados** | **Vínculo XML padrão** |
|---|---|
| Raiz | vazio (nulo) |
| Tokens | /Root/Tokens |
| Composto | vazio (nulo) |
| TokenID | TokenID |
| TokenText | vazio (nulo) |
| TokenHeading | TextoToken/CabeçalhoTexto |
| TokenBody | TokenText/CorpoDeTexto |
