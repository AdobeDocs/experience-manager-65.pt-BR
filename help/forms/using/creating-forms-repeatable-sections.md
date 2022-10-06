---
title: Criação de formulários com seções repetíveis
seo-title: Creating forms with repeatable sections
description: Seções repetíveis são painéis que podem ser adicionados ou removidos dinamicamente de um formulário.
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 17%

---

# Criação de formulários com seções repetíveis {#creating-forms-with-repeatable-sections}

As seções repetidas são painéis que podem ser adicionados ou removidos de forma dinâmica a um formulário.

Por exemplo, ao se candidatar a um cargo, o candidato a cargo fornece detalhes de emprego anteriores, como nome da empresa, função, projeto e outras informações. A informação de todos os empregadores requer seções diferentes, mas semelhantes. Nesse cenário, o formulário de emprego fornece uma seção do empregador e também uma opção para adicionar dinamicamente mais seções. Essas seções, que são adicionadas dinamicamente, são conhecidas como seções repetidas.

Você pode usar um dos seguintes métodos para criar painéis repetíveis:

## Uso do Gerenciador de instâncias por scripts  {#using-instance-manager-via-scripts-nbsp}

1. No modo de edição, selecione um painel e toque em ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, ative **Tornar o painel repetível**. Especifique os valores para a **[!UICONTROL Máximo]** e **[!UICONTROL Mínimo]** campos.

   O campo Maximum especifica o número máximo de vezes que um painel pode aparecer na página. Você pode especificar -1 no campo Contagem máxima para permitir que o painel apareça por um número infinito de vezes.

   O campo Minimum especifica o número mínimo de vezes que um painel é exibido no formulário. Se você definir o campo A contagem mínima como zero, posteriormente, será possível remover todas as instâncias por meio de scripts após a conclusão da renderização.

   >[!NOTE]
   >
   >Para criar um painel não repetível, defina o valor dos campos Máximo e Mínimo como um. O layout da opção não suporta -1 no campo Contagem máxima . Você pode especificar um número alto para fornecer a noção de valor infinito.

1. O pai do painel, que deve ser repetido, deve conter botões Adicionar e Excluir para gerenciar instâncias dos painéis repetíveis. Execute as seguintes etapas para inserir botões no pai e ativar scripts nos botões:

   1. Na barra lateral, arraste e solte um componente de botão no pai do painel. Selecione o componente e toque em ![editar regras](assets/edit-rules.png). As regras do botão são abertas no editor de regras.
   1. Na janela Editor de regras, clique em **Criar**.

      Selecionar **Editor visual** na linha Objetos de formulário e funções .

      1. Na área de regras, em WHEN, selecione state **é clicado**.
      1. Em THEN:

         * Para criar um botão adicionar painel, selecione **Adicionar instância** e arraste e solte o painel usando ![painel lateral de alternância](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**
         * Para criar um botão Excluir painel, selecione **Remover instância** e arraste e solte o painel usando ![painel lateral de alternância](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**

      Selecionar **Editor de códigos** na linha Objetos de formulário e funções . Clique em **Editar regras** e na área do código:

      * Para criar um botão adicionar painel, especifique `this.panel.instanceManager.addInstance()`
      * Para criar um botão Excluir painel, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Clique em **Concluído**.

      >[!NOTE]
      >
      >Se um campo pertencer a um painel repetível, não será possível acessá-lo diretamente usando seu nome em seus scripts. Para acessar o campo, especifique a instância repetível à qual o campo pertence usando o `instances` API em `InstanceManager`. A sintaxe a ser usada na variável `instances` API em `InstanceManager` é:
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
      >Para obter mais informações, consulte: Classe: InstanceManager#instâncias em [Referência da API Java do AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Quando todas as instâncias de um painel forem removidas de um formulário adaptável, para adicionar uma instância do painel removido, use a sintaxe _panelName para capturar o gerenciador de instâncias do painel e use a API addInstance do gerenciador de instâncias para adicionar a instância excluída. Por exemplo, _panelName.addInstance(). Ele adiciona uma instância do painel removido.



## Uso do layout de opção para o painel pai   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Um painel tem várias opções de layouts. A opção Layout for acordian design tem suporte pronto para uso para painéis repetíveis. Execute as seguintes etapas para reproduzir o painel com Layout para opção de design do acordeão:

1. No pai do painel a ser repetido, toque em ![cmppr](assets/cmppr.png). Você pode ver as propriedades na barra lateral. No **Layout** , selecione **Acordeão**.
1. Em um painel, que deve ser repetido, toque em ![cmppr](assets/cmppr.png). É possível ver as propriedades do painel na barra lateral. Ative o **Tornar o painel repetível** e especifique o valor da variável **Máximo** e **Mínimo** campos.

   Agora, você pode usar o sinal de mais (+) e excluir ( ![excluir painel](assets/delete-panel.png)) para adicionar e remover os painéis.

## Uso de subformulários repetitivos do Modelo de formulário (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

O subformulário repetível é semelhante aos painéis repetíveis no Adaptive Forms. No AEM Forms Designer, execute as seguintes etapas para criar um subformulário repetitivo:

1. Na paleta Hierarquia, selecione o subformulário pai daquele que você deseja repetir.
1. Na paleta Objeto, clique na guia Subformulário e selecione Continuado na lista Conteúdo.
1. Selecione o subformulário para repetir.
1. Na paleta Objeto, clique na guia Subformulário e selecione Posicionado ou Continuado na lista Conteúdo.
1. Clique na guia Vínculo e selecione Repetir subformulário para cada item de dados.
1. Para especificar o número mínimo de repetições, selecione Contagem mín. e insira o número na caixa associada. Se esta opção estiver configurada como 0 e nenhum dado for fornecido para os objetos no subformulário no momento da incorporação de dados, o subformulário não é disposto quando o formulário é renderizado.
1. Para especificar o número máximo de repetições do subformulário, selecione Máx. e insira o número na caixa associada. Se um valor não for especificado na caixa Máx., o número de repetições do subformulário será ilimitado.
1. Para especificar um número definido de repetições de subformulários, independentemente da quantidade de dados, selecione Contagem inicial e digite o número na caixa correspondente. Se você selecionar essa opção e nenhum dado estiver disponível ou se houver uma quantidade inferior de dados em comparação ao valor especificado em Contagem inicial, as instâncias vazias do subformulários ainda serão posicionadas.
1. Adicione dois botões no subformulário pai - um para adicionar a instância e outro para excluir a instância do subformulário repetível. Para obter etapas detalhadas, consulte [Criar uma ação](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Agora, vincule o Modelo de formulário ao formulário adaptável. Para obter etapas detalhadas, consulte [Criar um formulário adaptável com base em um modelo](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Use os botões criados na etapa 9 para adicionar e remover subformulários.

O arquivo .zip anexado contém um subformulário repetitivo de amostra.

[Obter arquivo](assets/samplerepeatablesubform.zip)

## Usando configurações de repetição de um Esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Você pode criar painéis repetíveis a partir de um Esquema XML e da propriedade minOccours &amp; maxOccurs de qualquer elemento de tipo complexo. Para obter informações detalhadas sobre o Esquema XML, consulte [Criar formulários adaptáveis usando o Esquema XML como Modelo de formulário](/help/forms/using/adaptive-form-xml-schema-form-model.md).

No código a seguir, a variável `SampleType`O painel usa a propriedade minOccours &amp; maxOccurs .

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
>Para layout não-acordeão, use componentes de botão de formulário adaptáveis para adicionar e remover instâncias.
