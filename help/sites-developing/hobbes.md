---
title: Teste da interface do usuário
description: O AEM fornece uma estrutura para automatizar testes na interface do AEM
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---

# Teste da interface do usuário{#testing-your-ui}

>[!NOTE]
>
>A partir do AEM 6.5, a estrutura de teste da interface do usuário do hobbes.js foi descontinuada. A Adobe não planeja fazer mais melhorias e recomenda que os clientes usem a automação Selenium.
>
>Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

O AEM fornece uma estrutura para automatizar testes para a interface do AEM. Usando a estrutura, você grava e executa testes de interface do usuário diretamente em um navegador da Web. A estrutura fornece uma API JavaScript para a criação de testes.

A estrutura de testes do AEM usa Hobbes.js, uma biblioteca de testes escrita em JavaScript. A estrutura Hobbes.js foi desenvolvida para testar o AEM como parte do processo de desenvolvimento. A estrutura agora está disponível para uso público para testar seus aplicativos de AEM.

>[!NOTE]
>
>Consulte o Hobbes.js [documentação](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) para obter detalhes completos da API.

## Estrutura dos ensaios {#structure-of-tests}

Ao usar testes automatizados no AEM, os seguintes termos são importantes para entender:

| Ação | Um **Ação** é uma atividade específica em uma página da Web, como clicar em um link ou em um botão. |
|---|---|
| Caso de teste | A **Caso de teste** é uma situação específica que pode ser composta por um ou mais **Ações**. |
| Conjunto de teste | A **Conjunto de teste** é um grupo de **Casos de teste** que, juntas, testam um caso de uso específico. |

## Execução de testes {#executing-tests}

### Exibição de conjuntos de teste {#viewing-test-suites}

Abra o Console de testes para ver os Conjuntos de testes registrados. O painel Testes contém uma lista de conjuntos de testes e seus casos de teste.

Navegue até o console Ferramentas via **Navegação global > Ferramentas > Operações > Teste**.

![chlimage_1-63](assets/chlimage_1-63.png)

Ao abrir o console, os Conjuntos de testes são listados à esquerda, juntamente com uma opção para executar todos eles sequencialmente. O espaço à direita mostrado com um plano de fundo quadriculado é um espaço reservado para mostrar o conteúdo da página à medida que os testes são executados.

![chlimage_1-64](assets/chlimage_1-64.png)

### Execução de um único conjunto de teste {#running-a-single-test-suite}

Conjuntos de testes podem ser executados individualmente. Quando você executa um Conjunto de testes, a página é alterada à medida que os Casos de teste e suas Ações são executados e os resultados são exibidos após a conclusão do teste. Os ícones indicam os resultados.

Um ícone de marca de seleção indica um teste bem-sucedido:

![Ícone de marca de seleção.](do-not-localize/chlimage_1-2.png)

Um ícone &quot;X&quot; indica um teste com falha:

![Falha no ícone de teste indicado por um X dentro de um círculo.](do-not-localize/chlimage_1-3.png)

Para executar um conjunto de teste:

1. No painel Testes, clique no nome do Caso de teste que deseja executar para expandir os detalhes das ações.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Clique em **Executar teste**.

   ![Uma imagem do botão Executar testes, indicada por um ponteiro voltado para a direita dentro de um círculo.](do-not-localize/chlimage_1-4.png)

1. O espaço reservado é substituído pelo conteúdo da página à medida que o teste é executado.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Revise os resultados do Caso de teste tocando ou clicando na descrição para abrir o **Resultado** painel. Tocar ou clicar no nome do Caso de teste no **Resultado** mostra todos os detalhes.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Execução de vários testes {#running-multiple-tests}

Os Conjuntos de testes são executados sequencialmente na ordem em que aparecem no console. Você pode detalhar um teste para ver os resultados detalhados.

![chlimage_1-68](assets/chlimage_1-68.png)

1. No painel Testes, clique no botão **Executar todos os testes** ou o botão **Executar testes** abaixo do título do Conjunto de testes que você deseja executar.

   ![Imagem do botão Executar todos os testes e do botão Executar testes, indicada por um ponteiro voltado para a direita dentro de um círculo.](do-not-localize/chlimage_1-5.png)

1. Para exibir os resultados de cada Caso de Teste, clique no título do Caso de Teste. Ao clicar no nome do teste na variável **Resultado** mostra todos os detalhes.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Criação e uso de um conjunto de teste simples {#creating-and-using-a-simple-test-suite}

O procedimento a seguir o orienta durante a criação e a execução de um Conjunto de testes usando [Conteúdo do We.Retail](/help/sites-developing/we-retail.md), mas você pode modificar facilmente o teste para usar uma página da Web diferente.

Para obter detalhes completos sobre como criar seus próprios Conjuntos de testes, consulte [Documentação da API de Hobbes.js](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. Abra o CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Clique com o botão direito do mouse no `/etc/clientlibs` e clique em **Criar > Criar pasta**. Tipo `myTests` para o nome e clique em **OK**.
1. Clique com o botão direito do mouse no `/etc/clientlibs/myTests` e clique em **Criar > Criar nó**. Use os seguintes valores de propriedade e clique em **OK**:

   * Nome: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Adicione as seguintes propriedades ao nó myFirstTest:

   | Nome | Tipo | Valor |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | String[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Somente AEM Forms**
   >
   >
   >Para testar formulários adaptáveis, adicione os seguintes valores às categorias e dependências. Por exemplo:
   >
   >
   >**categorias**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dependências**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Clique em **Salvar tudo**.
1. Clique com o botão direito do mouse no `myFirstTest` e clique em **Criar > Criar arquivo**. Nomeie o arquivo `js.txt` e clique em **OK**.
1. No `js.txt` insira o seguinte texto:

   ```
   #base=.
   myTestSuite.js
   ```

1. Clique em **Salvar tudo** e feche a `js.txt` arquivo.
1. Clique com o botão direito do mouse no `myFirstTest` e clique em **Criar > Criar arquivo**. Nomeie o arquivo `myTestSuite.js` e clique em **OK**.
1. Copie o código a seguir para o `myTestSuite.js` salve o arquivo:

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. Navegue até a **Testes** para experimentar o conjunto de testes.
