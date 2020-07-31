---
title: '"Tutorial: Teste do formulário adaptável"'
seo-title: '"Tutorial: Teste do formulário adaptável"'
description: Use o teste automatizado para testar vários formulários adaptáveis ao mesmo tempo.
seo-description: Use o teste automatizado para testar vários formulários adaptáveis ao mesmo tempo.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
translation-type: tm+mt
source-git-commit: a842aa85652e5c04d5825a3e88aa6b64ef8a0088
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 2%

---


# Tutorial: Teste do formulário adaptável{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Este tutorial é uma etapa da série [Criar seu primeiro formulário](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) adaptável. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

Depois que o formulário adaptativo estiver pronto, é importante testar seu adaptador antes de distribuí-lo para os usuários finais. Você pode testar manualmente (teste funcional) todos os campos ou automatizar o teste do formulário adaptável. Quando você tem vários formulários adaptáveis, testar manualmente todos os campos de todos os formulários adaptativos se torna uma tarefa assustadora.

Os AEM Forms fornecem uma estrutura de teste, Calvin, para automatizar o teste de seus formulários adaptáveis. Usando a estrutura, você grava e executa testes de interface diretamente em um navegador da Web. A estrutura fornece APIs JavaScript para a criação de testes. O teste automatizado permite testar a experiência de preenchimento prévio de um formulário adaptável, enviar a experiência de um formulário adaptável, regras de expressão, de validações, carregamento lento e interações de UI. Este tutorial o orienta pelas etapas para criar e executar testes automatizados em um formulário adaptável. No final deste tutorial, você poderá:

* [Criar um conjunto de testes para seu formulário adaptável](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Criar testes para seu formulário adaptável](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Execute o conjunto de testes e os testes criados para seu formulário adaptável](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Etapa 1: Criar um conjunto de testes {#step-create-a-test-suite}

Os conjuntos de testes têm uma coleção de casos de teste. Você pode ter vários conjuntos de testes. É recomendável ter um conjunto de testes separado para cada formulário. Para criar um conjunto de testes:

1. Efetue logon na instância do autor do AEM Forms como administrador. Abra o CRXDE Lite. Você pode tocar AEM logotipo > **Ferramentas** > **Geral** > **CRXDE Lite** ou abrir o URL [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) em um navegador para abrir o CRXDE Lite.

1. Navegue até /etc/clientlibs no CRXDE Lite. Clique com o botão direito do mouse na subpasta /etc/clientlibs e clique em **Criar** > **Criar nó.** No campo Nome, digite **WeRetailFormTestCasos**. Selecione o tipo como **cq:ClientLibraryFolder** e clique em **OK**. Cria um nó. Você pode usar qualquer nome no lugar de WeRetailFormTestCasos.
1. Adicione as seguintes propriedades ao nó WeRetailFormTestCasos e toque em **Salvar TODAS**.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Multi</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>categorias</td>
   <td>Sequência de caracteres</td>
   <td>Ativado</td>
   <td>
    <ul>
     <li>granite.testing.hobbes.tests<br /> </li>
     <li>granite.testing.calvin.tests</li>
    </ul> </td>
  </tr>
  <tr>
   <td>dependências</td>
   <td>Sequência de caracteres</td>
   <td>Ativado</td>
   <td>
    <ul>
     <li>granite.testing.hobbes.testrunner <br /> </li>
     <li>granite.testing.calvin <br /> </li>
     <li>apps.testframework.all</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Certifique-se de que cada propriedade seja adicionada a uma caixa separada, conforme exibido abaixo:

![dependências](assets/dependencies.png)

1. Clique com o botão direito do mouse no nó **[!UICONTROL WeRetailFormTestCasos]** e clique em **Criar** > **Criar arquivo**. No campo Nome, digite `js.txt` e clique em **OK**.
1. Abra o arquivo js.txt para edição, adicione o seguinte código e salve o arquivo:

   ```text
   #base=.
    init.js
   ```

1. Crie um arquivo, init.js, no `WeRetailFormTestCases`nó. Adicione o código abaixo ao arquivo e toque em **[!UICONTROL Salvar tudo]**.

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   O código acima cria um conjunto de testes chamado **We retail - Tests**.

1. Abra AEM Teste a interface do usuário (AEM > Ferramentas > Operações > Teste). O conjunto de testes - **Varejo - Testes** - está listado na interface do usuário.

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## Etapa 2: Criar um caso de teste para preencher valores antecipadamente em um formulário adaptável {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Um caso de teste é um conjunto de ações para testar uma funcionalidade específica. Por exemplo, preencher todos os campos de um formulário e validar alguns campos para garantir que os valores corretos sejam inseridos.

Uma ação é uma atividade específica em um formulário adaptável, como clicar em um botão. Para criar um caso de teste e ações para validar a entrada do usuário para cada campo de formulário adaptável:

1. Na lista CRXDE, navegue até a `/content/forms/af/create-first-adaptive-form` pasta. Clique com o botão direito do mouse no nó da pasta **[!UICONTROL create-first-adaptive-form]** e clique em **[!UICONTROL Criar]**> **[!UICONTROL Criar arquivo]**. No campo Nome, digite `prefill.xml` e clique em **[!UICONTROL OK]**. Adicione o seguinte código ao arquivo:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. Vá até `/etc/clientlibs`. Clique com o botão direito do mouse na `/etc/clientlibs` subpasta e clique em **[!UICONTROL Criar]**> **[!UICONTROL Criar nó]**.

   No campo **[!UICONTROL Nome]** , digite `WeRetailFormTests`. Selecione o tipo como `cq:ClientLibraryFolder` e clique em **[!UICONTROL OK]**.

1. Adicione as seguintes propriedades ao nó **[!UICONTROL WeRetailFormTests]** .

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Multi</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>categorias</td>
   <td>Sequência de caracteres</td>
   <td>Ativado</td>
   <td>
    <ul>
     <li>granite.testing.hobbes.tests<br /> </li>
     <li>granite.testing.hobbes.tests.testForm</li>
    </ul> </td>
  </tr>
  <tr>
   <td>dependências</td>
   <td>Sequência de caracteres</td>
   <td>Ativado</td>
   <td>
    <ul>
     <li>granite.testing.calvin.tests</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

1. Crie um arquivo, js.txt, no nó **[!UICONTROL WeRetailFormTests]** . Adicione o seguinte ao arquivo:

   ```shell
   #base=.
   prefillTest.js
   ```

   Clique em **[!UICONTROL Salvar tudo]**.

1. Crie um arquivo, `prefillTest.js`no nó **[!UICONTROL WeRetailFormTests]** . Adicione o código abaixo ao arquivo. O código cria um caso de teste. O caso de teste preenche todos os campos de um formulário e valida alguns campos para garantir que os valores corretos sejam inseridos.

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   O caso de teste é criado e pronto para ser executado. É possível criar casos de teste para validar vários aspectos de um formulário adaptável, como verificar a execução do script calculate, validar padrões e validar a experiência de envio de um formulário adaptável. Para obter informações sobre vários aspectos do teste de formulários adaptáveis, consulte Automatizar o teste de formulários adaptáveis.

## Etapa 3: Executar todos os testes em uma suíte ou casos individuais {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Um conjunto de testes pode ter vários casos de teste. Você pode executar todos os casos de teste em um conjunto de testes de uma vez ou individualmente. Quando você executa um teste, os ícones indicam os resultados:

* Um ícone de marca de seleção indica um teste aprovado: ![save_icon](assets/save_icon.svg)
* Um ícone &quot;X&quot; indica uma falha no teste: ![ícone de fechamento](assets/close-icon.svg)

1. Navegue até o ícone AEM > **[!UICONTROL Ferramentas]**> **[!UICONTROL Operações]**> **[!UICONTROL Testes]**
1. Para executar todos os testes do Test Suite:

   1. No painel Testes, toque em **[!UICONTROL Varejo - Testes (1)]**. A suíte se expande para exibir a lista do teste.
   1. Toque no botão **[!UICONTROL Executar testes]** . A área em branco no lado direito da tela é substituída pela forma adaptável à medida que o teste é executado.

   ![teste &quot;run-all-test&quot;](assets/run-all-test.png)

1. Para executar um único teste a partir do Test Suite:

   1. No painel Testes, toque em **[!UICONTROL Varejo - Testes (1)]**. A suíte se expande para exibir a lista do teste.
   1. Toque em **[!UICONTROL Prefill Test (Teste]** de pré-preenchimento) e toque no botão **[!UICONTROL Run Tests (Executar testes]** ). A área em branco no lado direito da tela é substituída pela forma adaptável à medida que o teste é executado.

1. Toque no nome do teste, Teste de preenchimento prévio, para analisar os resultados do caso de teste. Ele abre o painel Resultado. Toque no nome do caso de teste na visualização do painel Resultado para obter todos os detalhes do teste.

   ![resultados da revisão](assets/review-results.png)

Agora o formulário adaptável está pronto para publicação.
