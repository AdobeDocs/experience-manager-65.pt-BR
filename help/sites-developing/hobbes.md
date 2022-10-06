---
title: Testar sua interface do usuário
seo-title: Testing Your UI
description: AEM fornece uma estrutura para automatizar testes para sua interface AEM
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# Testar sua interface do usuário{#testing-your-ui}

>[!NOTE]
>
>A partir AEM 6.5, a estrutura de teste da interface do usuário do hobbes.js está obsoleta. O Adobe não planeja fazer aprimoramentos adicionais a ele e recomenda que os clientes usem a automação do Selenium.
>
>Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

O AEM fornece uma estrutura para automatizar testes para sua interface AEM. Usando a estrutura , você grava e executa testes de interface do usuário diretamente em um navegador da Web. A estrutura fornece uma API javascript para a criação de testes.

A estrutura de teste de AEM usa Hobbes.js, uma biblioteca de testes gravada em Javascript. A estrutura Hobbes.js foi desenvolvida para testar AEM como parte do processo de desenvolvimento. A estrutura agora está disponível para uso público para testar seus aplicativos de AEM.

>[!NOTE]
>
>Consulte o arquivo Hobbes.js [documentação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) para obter detalhes completos sobre a API.

## Estrutura dos ensaios {#structure-of-tests}

Ao usar testes automatizados no AEM, os seguintes termos são importantes para entender:

| Ação | Um **Ação** é uma atividade específica em uma página da Web, como clicar em um link ou em um botão. |
|---|---|
| Caso de teste | A **Caso de teste** é uma situação específica que pode ser constituída por um ou mais **Ações**. |
| Conjunto de testes | A **Conjunto de testes** é um grupo de **Casos de teste** que, em conjunto, testam um caso de uso específico. |

## Execução de testes {#executing-tests}

### Visualização de conjuntos de testes {#viewing-test-suites}

Abra o Console de teste para ver os Conjuntos de teste registrados. O painel Testes contém uma lista de conjuntos de testes e seus casos de teste.

Navegue até o console Ferramentas por meio do **Navegação global -> Ferramentas > Operações -> Teste**.

![chlimage_1-63](assets/chlimage_1-63.png)

Ao abrir o console, os Conjuntos de teste são listados à esquerda junto com uma opção para executá-los sequencialmente. O espaço à direita mostrado com um plano de fundo verificado é um espaço reservado para mostrar o conteúdo da página conforme os testes são executados.

![chlimage_1-64](assets/chlimage_1-64.png)

### Executando um único conjunto de testes {#running-a-single-test-suite}

Conjuntos de testes podem ser executados individualmente. Quando você executa um Test Suite, a página é alterada à medida que os Casos de teste e suas Ações são executados e os resultados são exibidos após a conclusão do teste. Os ícones indicam os resultados.

Um ícone de marca de verificação indica um teste aprovado:

![](do-not-localize/chlimage_1-2.png)

Um ícone &quot;X&quot; indica um teste com falha:

![](do-not-localize/chlimage_1-3.png)

Para executar um Test Suite:

1. No painel Testes, clique ou toque no nome do caso de teste que deseja executar para expandir os detalhes das ações.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Clique ou toque no **Executar teste** botão.

   ![](do-not-localize/chlimage_1-4.png)

1. O espaço reservado é substituído pelo conteúdo da página, conforme o teste é executado.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Revise os resultados do caso de teste tocando ou clicando na descrição para abrir o **Resultado** painel. Tocar ou clicar no nome do seu caso de teste na **Resultado** mostra todos os detalhes.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Execução de vários testes {#running-multiple-tests}

Os Conjuntos de teste são executados sequencialmente na ordem em que são exibidos no console. Você pode detalhar em um teste para ver os resultados detalhados.

![chlimage_1-68](assets/chlimage_1-68.png)

1. No painel Testes , toque ou clique em **Executar todos os testes** ou o botão **Executar testes** abaixo do título do Test Suite que você deseja executar.

   ![](do-not-localize/chlimage_1-5.png)

1. Para visualizar os resultados de cada caso de teste, toque ou clique no título do caso de teste. Tocar ou clicar no nome do teste na **Resultado** mostra todos os detalhes.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Criação e uso de um conjunto de teste simples {#creating-and-using-a-simple-test-suite}

O procedimento a seguir o orienta pela criação e execução de um Conjunto de teste usando [Conteúdo We.Retail](/help/sites-developing/we-retail.md), mas você pode modificar facilmente o teste para usar uma página da Web diferente.

Para obter detalhes completos sobre a criação de seus próprios Conjuntos de teste, consulte o [Documentação da API Hobbes.js](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. Abra o CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Clique com o botão direito do mouse no `/etc/clientlibs` e clique em **Criar > Criar pasta**. Tipo `myTests` para o nome e clique em **OK**.
1. Clique com o botão direito do mouse no `/etc/clientlibs/myTests` e clique em **Criar > Criar nó**. Use os seguintes valores de propriedade e clique em **OK**:

   * Nome: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Adicione as seguintes propriedades ao nó myFirstTest :

   | Nome | Tipo | Valor |
   |---|---|---|
   | `categories` | Sequência de caracteres[] | `granite.testing.hobbes.tests` |
   | `dependencies` | Sequência de caracteres[] | `granite.testing.hobbes.testrunner` |

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
1. No `js.txt` , insira o seguinte texto:

   ```
   #base=.
   myTestSuite.js
   ```

1. Clique em **Salvar tudo** e então feche a `js.txt` arquivo.
1. Clique com o botão direito do mouse no `myFirstTest` e clique em **Criar > Criar arquivo**. Nomeie o arquivo `myTestSuite.js` e clique em **OK**.
1. Copie o código a seguir para o `myTestSuite.js` em seguida, salve o arquivo:

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

1. Navegue até o **Teste** para experimentar seu conjunto de testes.
