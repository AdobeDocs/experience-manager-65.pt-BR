---
title: Criação de formulários com seções repetíveis
seo-title: Criação de formulários com seções repetíveis
description: Seções repetidas são painéis que podem ser adicionados ou removidos dinamicamente a um formulário.
seo-description: Seções repetidas são painéis que podem ser adicionados ou removidos dinamicamente a um formulário.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 16%

---


# Criação de formulários com seções repetíveis {#creating-forms-with-repeatable-sections}

Seções repetidas são painéis que podem ser adicionados ou removidos de forma dinâmica a um formulário.

Por exemplo, ao se candidatar a um cargo, o candidato a cargo fornece detalhes de emprego anteriores, como nome da empresa, função, projeto e outras informações. A informação de todos os empregadores requer seções diferentes, mas semelhantes. Neste cenário, o formulário relativo ao emprego fornece uma seção do empregador e também uma opção para adicionar dinamicamente mais seções. Essas seções, que são adicionadas dinamicamente, são conhecidas como seções repetidas.

Você pode usar um dos seguintes métodos para criar painéis repetíveis:

## Uso do Gerenciador de instâncias por scripts  {#using-instance-manager-via-scripts-nbsp}

1. No modo de edição, selecione um painel e, em seguida, toque em ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, ative **Tornar painel repetível**. Especifique valores para os campos **[!UICONTROL Maximum]** e **[!UICONTROL Minimum]**.

   O campo Máximo especifica o número máximo de vezes que um painel pode aparecer na página. Você pode especificar -1 no campo Contagem máxima para permitir que o painel apareça infinito vezes.

   O campo Mínimo especifica o número mínimo de vezes que um painel é exibido no formulário. Se a Contagem mínima for definida como zero, posteriormente, você poderá remover todas as instâncias por meio de scripts depois que a execução for concluída.

   >[!NOTE]
   >
   >Para criar um painel não repetível, defina o valor dos campos Máximo e Mínimo como um. O layout acordeão não suporta -1 no campo Contagem máxima. Você pode especificar um número alto para dar a noção de valor infinito.

1. O pai do painel, que deve ser repetido, deve conter botões adicionar e excluir para gerenciar instâncias dos painéis repetíveis. Execute as seguintes etapas para inserir botões no pai e ativar scripts nos botões:

   1. Na barra lateral, arraste e solte um componente de botão no pai do painel. Selecione o componente e toque em ![edit-rules](assets/edit-rules.png). As regras do botão são abertas no editor de regras.
   1. Na janela Editor de regras, clique em **Criar**.

      Selecione **Editor visual** na linha Objetos de formulário e funções.

      1. Na área de regra, em WHEN, o estado **selecionado é clicado**.
      1. Em THEN:

         * Para criar um botão adicionar painel, selecione **Adicionar instância** e arraste e solte o painel usando ![painel lateral de alternância](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione-o aqui.**
         * Para criar um botão do painel de exclusão, selecione **Remover instância** e arraste e solte o painel usando ![painel lateral de alternância](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione-o aqui.**

      Selecione **Editor de código** na linha Objetos de formulário e funções. Clique em **Editar regras** e na área de código:

      * Para criar um botão adicionar painel, especifique `this.panel.instanceManager.addInstance()`
      * Para criar um botão do painel Excluir, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Clique em **Concluído**.

      >[!NOTE]
      >
      >Se um campo pertencer a um painel repetível, você não poderá acessá-lo diretamente usando seu nome em seus scripts. Para acessar o campo, especifique a instância repetível à qual o campo pertence usando a API `instances` em `InstanceManager`. A sintaxe para usar a API `instances` em `InstanceManager` é:
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Por exemplo, você cria um formulário adaptável com um painel repetível com uma caixa de texto. Ao preencher previamente o formulário com três caixas de texto repetíveis, é necessário o xml abaixo:
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >Para ler dados AA1, especifique:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Para ler dados AA2, especifique:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Para obter mais informações, consulte: Classe: Instâncias do InstanceManager#em [Referência da API Java da AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Quando todas as instâncias de um painel forem removidas de um formulário adaptável, para adicionar uma instância do painel removido, use a sintaxe _panelName para capturar o Gerenciador de instâncias do painel e use a API addInstance do Gerenciador de instâncias para adicionar a instância excluída. Por exemplo, _panelName.addInstance(). Ela adiciona uma instância do painel removido.















## Uso do layout acordeão para o painel pai   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Um painel tem várias opções de layouts. A opção de design Layout para o acordian oferece suporte imediato a painéis repetíveis. Execute as seguintes etapas para reproduzir o painel com a opção Layout para o design do acordian:

1. No pai do painel a ser repetido, toque ![cmppr](assets/cmppr.png). É possível ver as propriedades na barra lateral. Na lista suspensa **Layout**, selecione **Acordeão**.
1. Em um painel, que deve ser repetido, toque ![cmppr](assets/cmppr.png). É possível ver as propriedades do painel na barra lateral. Ative a guia **Tornar painel repetível** e especifique o valor para os campos **Máximo** e **Mínimo**.

   Agora, você pode usar os botões de adição (+) e exclusão ( ![delete-panel](assets/delete-panel.png)) para adicionar e remover os painéis.

## Uso de subformulários repetitivos a partir do Modelo de formulário (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

O subformulário repetível é semelhante aos painéis repetíveis no Adaptive Forms. No AEM Forms Designer, execute as seguintes etapas para criar um subformulário repetitivo:

1. Na paleta Hierarquia, selecione o subformulário pai daquele que você deseja repetir.
1. Na paleta Objeto, clique na guia Subformulário e selecione Continuado na lista Conteúdo.
1. Selecione o subformulário para repetir.
1. Na paleta Objeto, clique na guia Subformulário e selecione Posicionado ou Continuado na lista Conteúdo.
1. Clique na guia Vínculo e selecione Repetir subformulário para cada item de dados.
1. Para especificar o número mínimo de repetições, selecione Contagem mín. e insira o número na caixa associada. Se esta opção estiver configurada como 0 e nenhum dado for fornecido para os objetos no subformulário no momento da incorporação de dados, o subformulário não é disposto quando o formulário é renderizado.
1. Para especificar o número máximo de repetições do subformulário, selecione Máx. e insira o número na caixa associada. Se um valor não for especificado na caixa Máx., o número de repetições do subformulário será ilimitado.
1. Para especificar um número definido de repetições de subformulários, independentemente da quantidade de dados, selecione Contagem inicial e digite o número na caixa correspondente. Se você selecionar essa opção e nenhum dado estiver disponível ou se houver uma quantidade inferior de dados em comparação ao valor especificado em Contagem inicial, as instâncias vazias do subformulários ainda serão posicionadas.
1. Adicione dois botões no subformulário pai - um para adicionar instância e outro para excluir instância de subformulário repetível. Para obter etapas detalhadas, consulte [Criar uma ação](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Agora, vincule o Modelo de formulário ao formulário Adaptável. Para obter etapas detalhadas, consulte [Criar um formulário adaptável com base em um modelo](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Use os botões criados na etapa 9 para adicionar e remover subformulários.

O arquivo .zip anexado contém um subformulário repetitivo de amostra.

[Obter arquivo](assets/samplerepeatablesubform.zip)

## Usando configurações de repetição de um Schema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Você pode criar painéis repetíveis a partir de um Schema XML e da propriedade minOccours &amp; maxOccurs de qualquer elemento de tipo complexo. Para obter informações detalhadas sobre o Schema XML, consulte [Criar formulários adaptáveis usando o Schema XML como Modelo de formulário](/help/forms/using/adaptive-form-xml-schema-form-model.md).

No código a seguir, o painel `SampleType`usa a propriedade minOccours &amp; maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Para o layout não-acordiano, use os componentes do botão de formulário adaptável para adicionar e remover instâncias.
