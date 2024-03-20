---
title: Criação de formulários com seções repetíveis
description: Seções repetíveis são painéis que podem ser dinamicamente adicionados ou removidos de um formulário.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms, Foundation Components
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---

# Criação de formulários com seções repetíveis {#creating-forms-with-repeatable-sections}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Seções repetíveis são painéis que podem ser adicionados ou removidos dinamicamente de um formulário.

Por exemplo, ao se candidatar a um cargo, o candidato a cargo fornece detalhes do emprego anterior, como nome da empresa, função, projeto e outras informações. A informação de todos os empregadores requer seções diferentes, mas semelhantes. Nesse cenário, o formulário de emprego fornece uma seção de empregador e também uma opção para adicionar dinamicamente mais seções. Essas seções, que são adicionadas dinamicamente, são conhecidas como seções Repetíveis.

Você pode usar um dos seguintes métodos para criar painéis repetíveis:

## Usando o Instance Manager por meio de scripts  {#using-instance-manager-via-scripts-nbsp}

1. No modo de edição, selecione um painel e, em seguida, ![cmppr](assets/cmppr.png). Na barra lateral, em Propriedades, ative **Tornar o painel repetível**. Especifique valores para o **[!UICONTROL Máximo]** e **[!UICONTROL Mínimo]** campos.

   O campo Máximo especifica o número máximo de vezes que um painel pode aparecer na página. Você pode especificar -1 no campo Contagem máxima para permitir que o painel apareça por um número infinito de vezes.

   O campo Minimum especifica o número mínimo de vezes que um painel é exibido no formulário. Se você definir o campo The Minimum Count como zero posteriormente, será possível remover todas as instâncias por meio de scripts depois que a representação for concluída.

   >[!NOTE]
   >
   >Para criar um painel não repetível, defina o valor dos campos Máximo e Mínimo como um. O layout do Accordion não é compatível com -1 no campo Contagem máxima. Você pode especificar um número alto para dar a noção de valor infinito.

1. O pai do painel, que deve ser repetido, deve conter os botões adicionar e excluir para gerenciar ocorrências dos painéis repetíveis. Execute as seguintes etapas para inserir botões no pai e ativar scripts nos botões:

   1. Na barra lateral, arraste e solte um componente de botão no pai do painel. Selecione o componente e selecione ![edit-rules](assets/edit-rules.png). As regras do botão são abertas no editor de regras.
   1. Na janela Editor de regras, clique em **Criar**.

      Selecionar **Editor visual** na linha Objetos de formulário e Funções.

      1. Na área regra, em QUANDO, selecione estado **foi clicado**.
      1. Em THEN:

         * Para criar um botão adicionar painel, selecione **Adicionar instância** e arraste e solte o painel usando ![ativar/desativar painel lateral](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**
         * Para criar um botão de exclusão do painel, selecione **Remover Instância** e arraste e solte o painel usando ![ativar/desativar painel lateral](assets/toggle-side-panel.png) ou selecione-o usando **Solte o objeto ou selecione aqui.**

      Selecionar **Editor de código** na linha Objetos de formulário e Funções. Clique em **Editar regras** e na área de código:

      * Para criar um botão Adicionar painel, especifique `this.panel.instanceManager.addInstance()`
      * Para criar um botão de exclusão do painel, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Clique em **Concluído**.

      >[!NOTE]
      >
      >Se um campo pertencer a um painel repetível, você não poderá acessá-lo diretamente usando seu nome nos scripts. Para acessar o campo, especifique a instância repetível à qual o campo pertence usando o `instances` API em `InstanceManager`. A sintaxe para usar o `instances` API em `InstanceManager` é:
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
      >Para ler os dados AA1, especifique:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Para ler os dados AA2, especifique:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Para obter mais informações, consulte: Classe: InstanceManager#instances em [Referência da API Java do AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Quando todas as instâncias de um painel forem removidas de um formulário adaptável, para adicionar uma instância do painel removido, use a sintaxe _panelName para capturar o gerenciador de instâncias do painel e a API addInstance do gerenciador de instâncias para adicionar a instância excluída. Por exemplo, _panelName.addInstance(). Ele adiciona uma instância do painel removido.

## Uso do layout do acordeão no painel principal   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Um painel tem várias opções de layout. A opção Layout para design do acordian tem suporte imediato para painéis repetíveis. Execute as seguintes etapas para o painel repetível com a opção Layout para design do acordian:

1. No pai do painel a ser repetido, selecione ![cmppr](assets/cmppr.png). Você pode ver as propriedades na barra lateral. No **Layout** selecione **Acordeão**.
1. Em um painel, que deve ser repetido, selecione ![cmppr](assets/cmppr.png). Você pode ver as propriedades do painel na barra lateral. Ativar o **Tornar o painel repetível** e especifique o valor para a variável **Máximo** e **Mínimo** campos.

   Agora, você pode usar o sinal de mais (+) e excluir ( ![delete-panel](assets/delete-panel.png)) para adicionar e remover os painéis.

## Uso de subformulários repetidos do Modelo de formulário (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

O subformulário repetível é semelhante aos painéis repetíveis no Adaptive Forms. No AEM Forms Designer, execute as seguintes etapas para criar um subformulário repetitivo:

1. Na paleta Hierarquia, selecione o subformulário pai do subformulário que deseja repetir.
1. Na paleta Objeto, clique na guia Subformulário e, na lista Conteúdo, selecione Fluxo.
1. Selecione o subformulário a ser repetido.
1. Na paleta Objeto, clique na guia Subformulário e, na lista Conteúdo, selecione Posicionado ou Fluxado.
1. Clique na guia Vinculação e selecione Repetir subformulário para cada item de dados.
1. Para especificar o número mínimo de repetições, selecione Contagem Mínima e digite um número na caixa associada. Se essa opção estiver definida como 0 e nenhum dado for fornecido para os objetos no subformulário no momento da mesclagem de dados, o subformulário não será colocado quando o formulário for renderizado.
1. Para especificar o número máximo de repetições do subformulário, selecione Máximo e digite um número na caixa associada. Se você não especificar um valor na caixa Máx., o número de repetições de subformulário será ilimitado.
1. Para especificar um número definido de repetições de subformulário, independentemente da quantidade de dados, selecione Contagem inicial e digite um número na caixa associada. Se você selecionar essa opção e não houver dados disponíveis ou houver menos entradas de dados do que o valor de Contagem inicial especificado, instâncias vazias do subformulário ainda serão colocadas no formulário.
1. Adicione dois botões no subformulário pai — um para adicionar a instância e outro para excluir a instância do subformulário repetível. Para obter etapas detalhadas, consulte [Criar uma ação](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Agora, vincule o Modelo de formulário ao Formulário adaptável. Para obter etapas detalhadas, consulte [Criar um formulário adaptável com base em um modelo](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Use os botões criados na etapa 9 para adicionar e remover subformulários.

O arquivo .zip anexado contém uma amostra de subformulário repetível.

[Obter arquivo](assets/samplerepeatablesubform.zip)

## Usando configurações de repetição de um Esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Você pode criar painéis repetíveis de um Esquema XML e da propriedade minOccours &amp; maxOccurs de qualquer elemento de tipo complexo. Para obter informações detalhadas sobre o Esquema XML, consulte [Criar formulários adaptáveis usando o esquema XML como modelo de formulário](/help/forms/using/adaptive-form-xml-schema-form-model.md).

No código a seguir, a variável `SampleType`O painel usa a propriedade minOccours &amp; maxOccurs.

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
>Para layout que não seja do acordeão, use componentes do botão de formulário adaptável para adicionar e remover instâncias.
