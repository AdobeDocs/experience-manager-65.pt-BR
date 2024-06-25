---
title: Práticas recomendadas para trabalhar com formulários adaptáveis
description: Explica as práticas recomendadas para configurar um projeto do AEM Forms, desenvolver formulários adaptáveis e otimizar o desempenho do sistema AEM Forms.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components,Core Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '5538'
ht-degree: 0%

---

# Práticas recomendadas para trabalhar com formulários adaptáveis {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

Os formulários Adobe Experience Manager (AEM) podem ajudar você a transformar transações complexas em experiências digitais simples e atraentes. No entanto, exige um esforço concertado para implementar, criar, executar e manter um ecossistema eficiente e produtivo do AEM Forms.

Este documento fornece diretrizes e recomendações das quais os administradores, autores e desenvolvedores de formulários podem se beneficiar ao trabalhar com o AEM Forms, especialmente o componente de formulários adaptáveis. Ele discute as práticas recomendadas desde a configuração de um projeto de desenvolvimento de formulários até a configuração, personalização, criação e otimização do AEM Forms. Essas práticas recomendadas contribuem coletivamente para o desempenho geral do ecossistema do AEM Forms.

Além disso, estas são algumas leituras recomendadas para práticas recomendadas gerais de AEM:

* [Práticas recomendadas: implantação e manutenção do AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas: criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas: administração de AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas: desenvolvimento de soluções](/help/sites-developing/best-practices.md)

## Instalar e configurar o AEM Forms {#set-up-and-configure-aem-forms}

### Configuração do projeto de desenvolvimento de formulários {#setting-up-forms-development-project}

Uma estrutura de projeto simplificada e padronizada pode reduzir significativamente os esforços de desenvolvimento e manutenção. O Apache Maven é uma ferramenta de código aberto recomendada para a construção de projetos AEM.

* Usar Apache Maven `aem-project-archetype` para criar e gerenciar a estrutura do projeto AEM. Ele cria a estrutura e os modelos recomendados para o projeto AEM. Além disso, fornece sistemas de automação de build e controle de alterações para ajudar a gerenciar o projeto.

   * Usar o Maven `archetype:generate` para gerar a estrutura inicial.
   * Usar maven `eclipse:eclipse` comando para gerar os arquivos de projeto do eclipse e importar o projeto para o eclipse.

Para obter mais informações, consulte [Como construir projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

* A ferramenta FileVault ou VLT ajuda a mapear o conteúdo de uma instância de CRX ou AEM para o seu sistema de arquivos. Ele fornece operações de gerenciamento de controle de alterações, como check-in e check-out do conteúdo do projeto AEM. Consulte [Como usar a ferramenta VLT](/help/sites-developing/ht-vlttool.md).

* Se você usar um ambiente de desenvolvimento integrado ao Eclipse, poderá usar as ferramentas do desenvolvedor do AEM para integração perfeita do Eclipse IDE com as instâncias do AEM para criar aplicativos do AEM. Para obter detalhes, consulte [Ferramentas de desenvolvedor de AEM para Eclipse](/help/sites-developing/aem-eclipse.md).

* Não armazene conteúdo nem faça modificações na pasta /libs. Crie sobreposições nas pastas /app para estender ou substituir as funcionalidades padrão.

* Ao criar pacotes para mover o conteúdo, certifique-se de que os caminhos de filtro de pacote estejam corretos e que apenas os caminhos necessários sejam mencionados.

* Não armazene conteúdo nem faça modificações na pasta /libs. Crie sobreposições nas pastas /app para estender ou substituir as funcionalidades padrão.

* Defina as dependências corretas para os pacotes para forçar uma ordem/sequência de instalação predeterminada.

* Não crie nenhum nó referenciável em /libs ou /apps.

### Planejamento para o ambiente de criação {#planning-for-authoring-environment}

Depois de configurar o projeto AEM, defina a estratégia de criação e personalização de modelos e componentes de formulários adaptáveis.

* Um modelo de formulário adaptável é uma página AEM especializada que define a estrutura e as informações do cabeçalho-rodapé de um formulário adaptável. Um modelo tem layouts, estilos e estrutura básica pré-configurados para um formulário adaptável. O AEM Forms fornece modelos e componentes prontos para uso que você pode usar para criar formulários adaptáveis. No entanto, você pode criar modelos e componentes personalizados de acordo com seus requisitos. É recomendável coletar os requisitos para modelos e componentes adicionais necessários em seus formulários adaptáveis. Para obter detalhes, consulte [Personalização de formulários e componentes adaptáveis](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* É recomendável carregar os pacotes de formulário usando a interface do usuário do Gerenciador de pacotes, em vez da interface do Gerenciador de pacotes do CRX, pois o carregamento de pacotes pelo Gerenciador de pacotes do CRX pode, às vezes, levar a anomalias.
* O AEM Forms permite criar formulários adaptáveis com base nos seguintes modelos de formulário. Os modelos de formulário atuam como interface para a troca de dados entre um formulário e um sistema AEM e fornecem uma estrutura baseada em XML para o fluxo de dados dentro e fora de um formulário adaptável. Além disso, os modelos de formulário impõem regras e restrições aos formulários adaptáveis na forma de restrições de esquema e XFA.

   * **Nenhum**: os formulários adaptáveis criados com essa opção não usam nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.
   * **Esquema XML ou JSON**: os esquemas XML e JSON representam a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. Você pode associar um esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis na guia Objeto de modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. Você pode arrastar e soltar os elementos do esquema para criar o formulário.
   * **Modelo de formulário XFA**: é um modelo de formulário ideal se você tiver investimentos em formulários HTML5 baseados em XFA. Ele fornece uma maneira direta de converter seus formulários baseados em XFA em formulários adaptáveis. Quaisquer regras XFA existentes são mantidas nos formulários adaptáveis associados. Os formulários adaptáveis resultantes são compatíveis com construções XFA, como validações, eventos, propriedades e padrões.
   * **Modelo de dados do formulário**: é um modelo de formulário preferencial se você estiver procurando integrar seus sistemas de back-end, como bancos de dados, serviços da Web e perfil de usuário AEM, para preencher previamente formulários adaptáveis e gravar dados de formulário enviados de volta nos sistemas de back-end. Um editor de modelo de dados de formulário permite definir e configurar entidades e serviços em um modelo de dados de formulário que você pode usar para criar formulários adaptáveis. Para obter mais informações, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

É importante escolher cuidadosamente o modelo de dados que não apenas atenda aos seus requisitos, mas que estenda seus investimentos existentes em ativos XFA e XSD, se houver. Use o Modelo XSD para criar modelos de formulário porque o XML gerado contém dados de acordo com o XPATH definido pelo esquema. Usar o Modelo XSD como uma opção padrão para o Modelo de dados de formulário também ajuda, pois ele dissocia o design do formulário do sistema de back-end que processa e consome dados e melhora o desempenho do formulário devido ao mapeamento de um para um do campo de formulário. Além disso, BindRef do campo pode se tornar o XPATH de seu valor de dados em XML.

Para obter mais informações, consulte [Criar um formulário adaptável](/help/forms/using/creating-adaptive-form.md).

* Há algumas seções comuns em formulários adaptáveis. Você pode identificá-los e definir uma estratégia para promover a reutilização de conteúdo. Os formulários adaptáveis permitem criar fragmentos autônomos e reutilizá-los em formulários. Também é possível salvar um painel em um formulário adaptável como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários associados. Ele ajuda a reduzir o tempo de criação e garante a consistência entre formulários. Além disso, o uso de fragmentos torna os formulários adaptáveis mais leves, resultando em uma experiência de criação aprimorada, especialmente de formulários grandes. Para obter mais informações, consulte [Fragmentos de formulário adaptável](/help/forms/using/adaptive-form-fragments.md).

### Personalização de formulários e componentes adaptáveis {#customize-components}

* O AEM Forms fornece modelos de formulário adaptáveis prontos para uso que você pode usar para criar formulários adaptáveis. Você também pode criar seus próprios templates. O AEM fornece modelos estáticos e editáveis.

   * Os modelos estáticos são definidos e configurados pelos desenvolvedores.
   * Os modelos editáveis são criados pelos autores usando o editor de modelos. O editor de modelos permite definir uma estrutura básica e o conteúdo inicial em um modelo. Qualquer modificação na camada da estrutura é refletida em todos os formulários que usam esse modelo. O conteúdo inicial pode incluir tema pré-configurado, serviço de preenchimento prévio, ação de envio e assim por diante. No entanto, essas configurações podem ser modificadas para um formulário usando o editor de formulários. Para obter mais informações, consulte [Modelos de formulário adaptável](/help/forms/using/template-editor.md).

* Para estilizar uma ocorrência específica de campo ou painel, use [estilo em linha](/help/forms/using/inline-style-adaptive-forms.md). Como alternativa, você pode definir uma classe em um arquivo CSS e especificar o nome da classe na propriedade Classe CSS do componente.
* Inclua uma biblioteca do cliente em um componente para aplicar estilos de forma consistente em formulários ou fragmentos adaptáveis que usam esse componente. Para obter mais informações, consulte [Criar um componente de página de formulário adaptável](/help/forms/using/custom-adaptive-forms-templates.md).
* Aplique os estilos definidos em uma biblioteca do cliente para selecionar formulários adaptáveis, especificando o caminho para a biblioteca do cliente no campo Caminho do arquivo CSS nas propriedades do contêiner de formulários adaptáveis.
* Para criar uma biblioteca cliente de seus estilos, você pode configurar o arquivo CSS personalizado na clientlib base do Editor de temas ou nas propriedades do Contêiner de formulário.
* Os formulários adaptáveis fornecem layouts de painel, como responsivo, com guias, acordeões e assistente, para controlar como os componentes de formulário são posicionados em um painel. É possível criar layouts de painel personalizados e disponibilizá-los para uso por autores de formulário. Para obter mais informações, consulte [Criação de componentes de layout personalizados para formulários adaptáveis](/help/forms/using/custom-layout-components-forms.md).
* Você também pode personalizar componentes específicos do formulário adaptável, como campos e layout do painel.

   * Use o [Sobreposição](/help/sites-developing/overlays.md) funcionalidade do AEM para modificar uma cópia de um componente. Não é recomendável modificar componentes padrão.
   * Para personalizar o layout dos componentes de formulário adaptáveis prontos para uso em /libs, [criar componentes de layout personalizados](/help/forms/using/custom-layout-components-forms.md) além do [layouts padrão](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduza interatividades personalizadas criando widgets ou aparências personalizados. Não é recomendável modificar componentes padrão. Para obter mais informações, consulte [Estrutura de aparência](/help/forms/using/introduction-widgets.md).

* Consulte [Lidar com informações de identificação pessoal](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) para obter recomendações sobre como lidar com dados de PII.

### Criação de modelos de formulário

É possível criar um formulário adaptável usando os modelos de formulário habilitados em **Navegador de configuração**. Para ativar os modelos de formulário, consulte [Criação do modelo de formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

Os modelos de formulário também podem ser carregados de pacotes de formulários adaptáveis criados em outra máquina de criação. Os modelos de formulário são disponibilizados instalando [aemforms-references-* pacotes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). Algumas das práticas recomendadas são:

* A variável **nosamplecontent** o modo de execução é recomendado somente para o autor e não para os nós de publicação.
* A criação de ativos, como formulário adaptável, temas, modelos ou configurações de nuvem, é executada somente nos nós Autor, que podem ser publicados nos nós Publicar configurados.
Para obter mais informações, consulte [Publicação e cancelamento de publicação de formulários e documentos](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* O pacote complementar do Forms é necessário para que a Criação e a Publicação sejam compatíveis com as operações de serviço de documento, portanto, pode ser considerado uma dependência.
Se você quiser apenas templates de amostra, temas e pacotes DOR relacionados ao Forms, é possível baixá-los em [aemforms-references-* pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

Para obter mais informações, consulte as práticas recomendadas em [Introdução à criação de formulários adaptáveis](/help/forms/using/introduction-forms-authoring.md).

## Criar formulários adaptáveis {#author-adaptive-forms}

### Uso da interface otimizada para toque para criação {#using-touch-optimized-ui-for-authoring}

* Use o navegador de Objetos na barra lateral para acessar rapidamente os campos no fundo da hierarquia de formulários. Você pode usar a caixa de pesquisa para procurar objetos no formulário ou na árvore de objetos para navegar de um objeto para outro.
* Para exibir e editar as propriedades de um componente no navegador de componentes na barra lateral, selecione o componente e clique em ![cmppr-1](assets/cmppr-1.png). Você também pode clicar duas vezes em um componente para exibir suas propriedades no navegador de propriedades.
* Use atalhos de teclado para executar ações rápidas em seus formulários. Consulte [Atalhos de teclado do AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Os componentes de formulários adaptáveis são recomendados para uso somente em páginas de formulários adaptáveis. Os componentes têm dependência em sua hierarquia pai. Portanto, não os use em uma página de AEM.

Além disso, consulte descrições de componentes e práticas recomendadas em [Introdução à criação de formulários adaptáveis](/help/forms/using/introduction-forms-authoring.md).

### Uso de regras em formulários adaptáveis {#using-rules-in-adaptive-forms}

O AEM Forms fornece uma [editor de regras](/help/forms/using/rule-editor.md) que permite criar regras para adicionar comportamento dinâmico aos componentes de formulário adaptáveis. Usando essas regras, você pode avaliar condições e acionar ações em componentes, como mostrar ou ocultar campos, calcular valores, alterar a lista suspensa dinamicamente e assim por diante.

O editor de regras fornece um editor visual e um editor de código para escrever regras. Considere o seguinte ao escrever regras usando o modo do editor de código:

* Use nomes significativos e exclusivos para campos de formulário e componentes para evitar possíveis conflitos ao escrever regras.
* Uso `this` operador para um componente se referir a si mesmo em uma expressão de regra. Ela garante que a regra permaneça válida mesmo se o nome do componente for alterado. Por exemplo, `field1.valueCommit script: this.value > 10`.

* Usar nomes de componentes ao fazer referência a outros componentes de formulário. Use o `value` para buscar o valor de um campo ou componente. Por exemplo, `field1.value`.

* Consulte os componentes por hierarquia exclusiva relativa para evitar conflitos. Por exemplo, `parentName.fieldName`.

* Ao lidar com regras complexas ou de uso comum, considere escrever lógica de negócios como funções em uma biblioteca do cliente separada que você pode especificar e reutilizar em formulários adaptáveis. A biblioteca do cliente deve ser uma biblioteca independente e não deve ter dependências externas, exceto em jQuery e Underscore.js. Você também pode usar a biblioteca do cliente para impor [revalidação do lado do servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) de dados de formulário enviados.
* Os formulários adaptáveis fornecem um conjunto de APIs que você pode usar para se comunicar e executar ações em formulários adaptáveis. Algumas das principais APIs são as seguintes. Para obter mais informações, consulte [Referência da API da biblioteca JavaScript para o Adaptive Forms](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: redefine um formulário.
   * `guideBridge.submit()`: envia um formulário.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: define o foco para um campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: valida um formulário.
   * `guideBridge.getDataXML(options)`: obtém dados do formulário como XML.
   * `guideBridge.resolveNode(somExpression)`: obtém um objeto de formulário.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: define a propriedade de um objeto de formulário.
   * Além disso, você pode usar as seguintes propriedades de campo:

      * `field.value` para alterar o valor de um campo.
      * `field.enabled` para ativar/desativar um campo.
      * `field.visible` para alterar a visibilidade de um campo.

* Os autores do formulário adaptável podem precisar gravar código JavaScript para criar lógica de negócios em um formulário. Embora o JavaScript seja eficiente, é provável que ele comprometa as expectativas de segurança. Portanto, você deve garantir que o autor do formulário seja uma pessoa confiável e que haja processos para revisar e aprovar o código JavaScript antes que um formulário seja colocado em produção. O administrador pode restringir o acesso ao editor de regras a grupos de usuários com base em sua função. Consulte [Conceder acesso ao editor de regras para grupos de usuários selecionados](/help/forms/using/rule-editor-access-user-groups.md).
* Você pode usar expressões em regras para tornar formulários adaptáveis dinâmicos. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter mais informações sobre expressões e práticas recomendadas, consulte [Expressões de formulário adaptável](/help/forms/using/adaptive-form-expressions.md).

* O Adobe recomenda usar operações síncronas de JavaScript em relação a operações assíncronas ao criar regras com o editor de regras. O uso de operações assíncronas é altamente desencorajado. No entanto, se você estiver em uma situação em que as operações assíncronas são inevitáveis, é essencial implementar funções de Fechamento do JavaScript. Ao fazer isso, você pode se proteger efetivamente contra possíveis condições de corrida, garantindo que as implementações de regras forneçam o melhor desempenho e mantenham a estabilidade em todo o.

  Por exemplo, vamos supor que precisamos buscar dados de uma API externa e, em seguida, aplicar algumas regras com base nesses dados. Usamos um fechamento para lidar com a chamada de API assíncrona e garantir que as regras sejam aplicadas após a busca dos dados. Este é o código de exemplo:

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  Neste exemplo, `fetchDataFromAPI` simula uma chamada de API assíncrona usando `setTimeout`. Depois que os dados são buscados, ele chama a função de retorno de chamada fornecida, que é o fechamento para lidar com a aplicação de regra subsequente. A variável `ruleImplementation` contém a lógica da regra.


### Trabalhar com temas {#working-with-themes}

Adaptável para temas permite criar estilos reutilizáveis que podem ser aplicados em formulários para obter uma aparência e um estilo consistentes. Use Temas para definir o estilo de componentes de formulário e painéis. Algumas práticas recomendadas sobre temas são as seguintes:

* Use a biblioteca de ativos para aplicar rapidamente estilos de texto, plano de fundo e imagens. Quando adicionado na biblioteca de ativos, o estilo fica disponível para outros temas e no modo de estilo do editor de formulários.
* Aplique configurações globais como fonte e plano de fundo da página usando o seletor no nível da página.
* Use bibliotecas de clientes para importar estilos existentes ou avançados para seus temas.
* É possível substituir o estilo de campos, painéis ou botões específicos em uma camada de estilo de formulário.
* Se um tema não atender ao seu requisito de estilo, você poderá usar classes predefinidas, como guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode, para aplicar um estilo comum em todos os formulários.

Para obter mais informações, consulte [Temas](/help/forms/using/themes.md).

### Otimização do desempenho de formulários grandes e complexos {#optimizing-performance-of-large-and-complex-forms}

Os autores de formulários e os usuários finais normalmente enfrentam problemas de desempenho ao carregar formulários grandes no modo de criação ou no tempo de execução. À medida que o número de objetos (campos e painéis) no formulário aumenta, a experiência de criação e tempo de execução começa a ser degradada. Também impede que vários autores colaborem e criem um formulário simultaneamente.

Considere as seguintes práticas recomendadas para superar problemas de desempenho com formulários grandes:

* É recomendável criar formulários adaptáveis usando o modelo de dados de formulário XSD, mesmo ao converter um XFA em um formulário adaptável, se possível.
* Inclua apenas os campos e painéis em formulários adaptáveis que capturem informações do usuário. Considere manter o conteúdo estático mínimo ou use URLs para abri-los em uma janela separada.
* Embora cada formulário seja projetado para uma finalidade específica, há alguns segmentos comuns na maioria dos formulários. Por exemplo, detalhes pessoais, endereço, detalhes de emprego e assim por diante. Criar [fragmentos de formulário adaptáveis](/help/forms/using/adaptive-form-fragments.md) para elementos e seções de formulário comuns e usá-los em formulários. Também é possível salvar um painel em um formulário existente como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários adaptáveis associados. Ele promove a criação colaborativa, pois vários autores podem trabalhar simultaneamente em diferentes fragmentos que compõem um formulário.

   * Semelhante aos formulários adaptáveis, é recomendável que todo o estilo específico do fragmento e os scripts personalizados sejam definidos na biblioteca do cliente usando a caixa de diálogo do contêiner do fragmento. Além disso, tente criar fragmentos autossuficientes que não dependam de objetos fora dele.
   * Evite usar script de fragmentos cruzados. Se houver algum objeto fora do fragmento ao qual você deve se referir, tente tornar esse objeto uma parte do formulário principal. Se o objeto ainda precisar residir em outro fragmento, consulte-o pelo seu nome no script.

* Use Salvar e retomar com o salvamento automático para salvar o formulário adaptável periodicamente e permitir que os usuários visitem novamente mais tarde para preencher o formulário.
* Configurar fragmentos para carregar lentamente. No tempo de execução, os fragmentos marcados para carregamento lento são renderizados somente quando necessários. Ele reduz significativamente o tempo de carregamento de formulários grandes. Também é compatível com fragmentos com painéis repetíveis. Para obter mais informações, consulte [Configurar carregamento lento](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Não configure o carregamento lento em fragmentos em um layout de grade responsivo ou no primeiro painel.
   * Os componentes de Anexos de arquivo e Termos e condições não são compatíveis com fragmentos carregados lentamente.
   * Marque um valor em um painel carregado lento como Usar valor globalmente se esse valor for usado em alguma outra parte do formulário, de modo que o valor esteja disponível para uso quando o painel que o contém for descarregado.
   * Considere escrever regras de visibilidade para fragmentos que devem ser exibidos ou ocultados com base em uma condição.
* Defina o valor de **Número de chamadas por solicitação** no **Apache Sling Main Servlet** para um número relativamente grande. Ela permite que o servidor do Forms permita chamadas adicionais. A configuração exibe um valor padrão de 1500. O valor, 1500 chamadas, é para outros componentes do Experience Manager, como Sites e Assets. O conjunto de valores padrão de formulários adaptáveis é 20000. Se você encontrar a variável `too many calls` erro nos logs ou o formulário não é renderizado. tente aumentar o valor para um número grande para resolver o problema. Se o número de chamadas exceder 20000, significa que o formulário é complexo e pode levar algum tempo para renderizar o formulário no navegador. Isso só acontece na primeira vez que o formulário é carregado, depois que ele é armazenado em cache e, uma vez armazenado em cache, não há impacto significativo no desempenho.

### Preenchimento prévio de formulários adaptáveis {#prefilling-adaptive-forms}

É possível preencher previamente campos de formulário adaptáveis com dados obtidos do back-end para ajudar os usuários a preencher rapidamente o formulário e evitar erros de digitação.

* O AEM Forms fornece um serviço de preenchimento prévio para ler dados de um arquivo XML de dados predefinido e preencher previamente os campos de um formulário adaptável com o conteúdo no arquivo XML de preenchimento prévio.
* O XML de dados de preenchimento prévio deve ser compatível com o esquema do modelo de formulário associado ao formulário adaptável.
* Incluir `afBoundedData` e `afUnBoundedData` no XML de preenchimento prévio para preencher previamente os campos vinculados e não vinculados em um formulário adaptável.

* Para formulários adaptáveis com base no modelo de dados de formulário, o AEM Forms fornece o Serviço de preenchimento prévio do modelo de dados de formulário pronto para uso. O serviço de preenchimento consulta fontes de dados para objetos de modelo de dados no formulário adaptável e preenche valores de campo ao renderizar o formulário.
* Você também pode usar os protocolos de arquivo, crx, serviço ou http para preencher previamente formulários adaptáveis.
* O AEM Forms oferece suporte a serviços de preenchimento prévio personalizados que você pode conectar como um serviço OSGi para preencher previamente formulários adaptáveis.

Para obter mais informações, consulte [Preencher previamente campos de formulário adaptável](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Assinatura e envio de formulários adaptáveis {#signing-and-submitting-adaptive-forms}

Formulários adaptáveis exigem ações Enviar para processar dados especificados pelo usuário. A ação Enviar determina a tarefa executada nos dados enviados por meio de um formulário adaptável.

* Há várias ações de envio disponíveis prontas para uso em formulários adaptáveis. Para obter detalhes, consulte [Configuração da ação Enviar](/help/forms/using/configuring-submit-actions.md).
* Você poderá escrever uma ação de envio personalizada se as ações de envio padrão não atenderem ao seu caso de uso. Para obter mais informações, consulte [Gravação da ação enviar personalizada para formulários adaptáveis](/help/forms/using/custom-submit-action-form.md).
* Inclua validações do lado do servidor para impedir o envio de dados inválidos.

Você pode usar a experiência de vários sinais do Adobe Sign em formulários adaptáveis. Considere o seguinte ao configurar o Adobe Sign em formulários adaptáveis. Para obter detalhes, consulte [Uso do Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

* O formulário adaptável habilitado para Adobe Sign é enviado somente após todos os signatários terem assinado o formulário. O Forms é exibido no estado Assinatura pendente até que o formulário seja assinado por todos os signatários.
* Você pode configurar a experiência de assinatura no formulário ou redirecionar os signatários para uma página de assinatura no envio.
* Configure a experiência de assinatura sequencial ou paralela, conforme apropriado.

### Gerando documento de registro {#generating-document-of-record}

Um documento de registro (DoR) é uma versão de PDF nivelada de um formulário adaptável que você pode imprimir, assinar ou arquivar.

* Dependendo do modelo de dados de formulário em que um formulário adaptável é baseado, você pode configurar um modelo para DoR da seguinte maneira:

   * **Modelo de formulário XFA**: use o arquivo XDP associado como o modelo do DoR.
   * **Esquema XSD**: use o modelo XFA associado que usa o mesmo esquema XML usado pelo formulário adaptável.
   * **Nenhum**: Use o DoR gerado automaticamente.

* Configure cabeçalho, rodapé, imagens, cor, fonte e assim por diante, diretamente da guia Documento de registro do editor de formulário adaptável.
* Uso `DoRService` para gerar o DoR de forma programática.
* Excluir campos ocultos do DoR.
* Uso `afAcceptLang` parâmetro de solicitação para exibir o DoR em outro local.

### Depuração e teste de formulários adaptáveis {#debugging-and-testing-adaptive-forms}

[Plug-in AEM Chrome](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) é uma extensão de navegador para o Google Chrome que fornece ferramentas para depurar formulários adaptáveis. Os autores e desenvolvedores de formulários podem usar essas ferramentas para:

* Identificar gargalos e otimizar o desempenho da renderização de formulários
* Depurar palavras-chave e erros bindRef no formulário
* Habilitar e configurar logs
* Depurar regras e scripts no formulário
* Explore e saiba mais sobre as APIs do guideBridge

Para obter mais informações, consulte [Plug-in AEM Chrome - Formulário adaptável](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Validação de formulários adaptáveis no servidor AEM {#validating-adaptive-forms-on-aem-server}

As validações do lado do servidor são necessárias para impedir qualquer tentativa de ignorar validações no cliente e qualquer possível comprometimento de envios de dados e violações de regras de negócios. As validações do lado do servidor são executadas no servidor carregando a biblioteca do cliente necessária.

* Inclua funções em uma biblioteca do cliente para validar expressões em formulários adaptáveis e especifique a biblioteca do cliente na caixa de diálogo do contêiner de formulários adaptáveis. Para obter mais informações, consulte [Revalidação do lado do servidor](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca do cliente separada para validações e não misturá-la com outras coisas, como estilo de HTML e manipulação de DOM na mesma biblioteca do cliente.

### Localização de formulários adaptáveis {#localizing-adaptive-forms}

O AEM fornece fluxos de trabalho de tradução que podem ser usados para localizar formulários adaptáveis. Para obter informações, consulte [Uso do fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Algumas práticas recomendadas ao localizar formulários adaptáveis são as seguintes:

* Use fragmentos de formulário adaptáveis para elementos comuns em formulários e localizar fragmentos. Ela garante que você localize um fragmento uma vez e reflita em todas as formas em que o fragmento localizado é usado.
* Quaisquer modificações como adicionar um novo componente ou aplicar um script em um formulário localizado não são localizadas automaticamente. Portanto, você deve finalizar um formulário antes de localizá-lo para evitar vários ciclos de localização.
* Uso `afAcceptLang` parâmetro de solicitação para substituir a localidade do navegador e renderizar o formulário na localidade especificada. Por exemplo, a URL a seguir é forçada a renderizar o formulário na localidade japonesa, independentemente da localidade especificada na configuração do navegador:

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Atualmente, o AEM Forms oferece suporte à localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). No entanto, você pode adicionar suporte para novos locais para formulários adaptáveis no tempo de execução. Para obter mais informações, consulte [Suporte a novos códigos de idiomas para localização de formulários adaptáveis](/help/forms/using/supporting-new-language-localization.md).

## Preparar projeto de formulários para produção {#prepare-forms-project-for-production}

### Adicionar servidor de processamento de formulários {#adding-forms-processing-server}

Você pode configurar uma instância adicional do servidor AEM Forms que reside atrás do firewall em uma zona protegida. Você pode usar essa instância para:

* **Processamento em lote**: trabalhos que são recorrentes ou agendados em lotes com carga pesada. Por exemplo, imprimir declarações, gerar correspondências e usar serviços de documento como PDF Generator, Saída e Assembler.
* **Armazenamento de dados PII**: Salve os dados de PII no servidor de processamento. Isso não é necessário se você já estiver usando um provedor de armazenamento personalizado para armazenar dados de PII.

### Mover projeto para outro ambiente {#moving-project-to-another-environment}

Você geralmente precisa mover seus projetos de AEM de um ambiente para outro. Algumas das principais coisas que devem ser lembradas ao mover-se são as seguintes:

* Faça backup das bibliotecas de clientes existentes, do código personalizado e das configurações.
* Implante pacotes e patches de produtos manualmente e na ordem especificada no novo ambiente.
* Implante pacotes de código específicos do projeto e pacotes manualmente e como um pacote ou pacote separado no novo servidor AEM.
* (*AEM Forms somente no JEE*) Implantar LCAs e DSCs manualmente no servidor do Forms Workflow.
* Uso [Exportar-Importar](/help/forms/using/import-export-forms-templates.md) funcionalidade para mover ativos para o novo ambiente. Você também pode configurar o agente de replicação e publicar os ativos.
* Ao atualizar, substitua todos os recursos e APIs obsoletos por novas APIs e novos recursos.

### Configuração do AEM {#configuring-aem}

Algumas práticas recomendadas para configurar o AEM a fim de melhorar o desempenho geral são as seguintes:

* Ative a compactação da biblioteca do cliente HTML para JavaScript e CSS no Felix Console.
* Armazenar em cache todas as bibliotecas de clientes em `/etc.clientlibs/fd` e qualquer biblioteca de cliente personalizada adicional no AEM dispatcher para aumentar a capacidade de resposta e a segurança de seus formulários publicados. Para obter mais informações, consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Não armazenar em cache `/content/forms/af/` e `/content/dam/formsanddocuments/*` caminhos. para obter informações detalhadas sobre a configuração do armazenamento em cache de formulários adaptáveis, consulte [Armazenamento em cache de formulários adaptáveis](/help/forms/using/configure-adaptive-forms-cache.md).

* Habilite o HTML através do módulo de compactação do servidor Web. Para obter mais informações, consulte [Ajuste de desempenho do servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumente as chamadas por configuração de solicitação para formulários grandes. Consulte [Otimização do desempenho de formulários grandes e complexos](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Criar [páginas de erro personalizadas mostradas pelo manipulador de erros](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* Servidor AEM Forms seguro.

   * Uso `nosamplecontent` modo de execução para garantir que não haja conteúdo de amostra e usuários de amostra implantados no servidor de produção. Consulte [Execução do AEM no modo de produção pronta](/help/sites-administering/production-ready.md).

* Mantenha o tamanho do heap em no mínimo 8 GB. Para outras configurações, consulte [Ajuste de desempenho do servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Use sessões de usuário do serviço em vez de sessões de administrador para executar tarefas de nível de serviço. Para obter mais informações, consulte [Autenticação de serviço](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuração do armazenamento externo para rascunhos e dados de formulários enviados {#external-storage}

Em um ambiente de produção, é recomendável não armazenar dados de formulário enviados no repositório AEM. A implementação padrão das ações enviar do Forms Portal Store, Armazenar conteúdo e Armazenar PDF armazenam dados de formulário no repositório AEM. Essas ações de envio são destinadas apenas para fins de demonstração. Além disso, os recursos Salvar e Retomar e Salvar Automaticamente usam o armazenamento do portal por padrão. Portanto, considere as seguintes recomendações:

* **Armazenamento de dados de rascunho**: se estiver usando o recurso Rascunho de formulários adaptáveis, você deve implementar uma Interface de Provedor de Serviço (SPI) personalizada para armazenar dados de rascunho em um armazenamento mais seguro, como o banco de dados. Para obter mais informações, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

* **Armazenamento de dados de envio**: se estiver usando o Repositório de envio do portal de formulários, você deve implementar uma SPI personalizada para armazenar os dados de envio em um banco de dados. Consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md) para obter uma integração de exemplo.

  Você também pode escrever uma ação de envio personalizada que armazene dados de formulário e anexos em um armazenamento seguro. Consulte [Gravação da ação enviar personalizada para formulários adaptáveis](/help/forms/using/custom-submit-action-form.md) para obter mais informações.

* **Comprimento da ID de rascunho**: ao salvar um formulário adaptável como rascunho, uma ID de rascunho é gerada para identificar de forma exclusiva o rascunho. O valor mínimo para o comprimento do campo de ID de rascunho é de 26 caracteres. A Adobe recomenda definir o comprimento da ID de rascunho para 26 ou mais caracteres.

### Lidar com informações de identificação pessoal {#handling-personally-identifiable-information}

Um dos principais desafios para as organizações é como lidar com dados de identificação pessoal (PII). Algumas práticas recomendadas que ajudarão você a lidar com esses dados são as seguintes:

* Use um armazenamento externo seguro, como um banco de dados, para armazenar dados de formulários de rascunho e enviados. Consulte [Configuração do armazenamento externo para rascunhos e dados de formulários enviados](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Use o componente de formulário dos Termos e condições para obter consentimento explícito do usuário antes de habilitar o salvamento automático. Nesse caso, ative a opção Salvar automaticamente somente quando o usuário concordar com as condições no componente dos Termos e condições.

## Escolha o Editor de regras, o Editor de códigos ou as Bibliotecas personalizadas do cliente para o formulário adaptável {#RuleEditor-CodeEditor-ClientLibs}

### Editor de regras {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

O Editor de regras do AEM Forms fornece uma interface visual para criar e gerenciar regras, reduzindo a necessidade de codificação extensa. Pode ser especialmente útil para usuários empresariais ou designers de formulários que podem não ter habilidades avançadas de programação, mas precisam definir e manter regras de negócios nos formulários. Aqui, discutimos alguns casos de uso nos quais o editor de regras permite:

* <!-- Allows you --> Para definir regras de negócios para seus formulários sem a necessidade de uma programação extensa.
* <!-- Use the Rule Editor when you need --> Para implementar lógica condicional dentro de seus formulários. Isso inclui mostrar ou ocultar elementos de formulário, alterar valores de campo com base em determinadas condições ou alterar dinamicamente o comportamento dos formulários.
* <!--When you want --> Para aplicar regras de validação de dados em envios de formulário, o Editor de regras pode ser usado para definir condições de validação.
* <!-- When you need --> Para integrar seus formulários a fontes de dados externas (FDM) ou serviços, o Editor de regras pode ajudar a definir regras para buscar, exibir ou manipular dados durante as interações do formulário.
* <!-- If you want -->Para criar formulários dinâmicos e interativos que respondam às ações do usuário, o Editor de regras permite definir regras que controlam o comportamento dos elementos de formulário em tempo real.

O Editor de regras está disponível para Componentes do AEM Forms Foundation e Componentes principais.

### Editor de código {#code-editor}

O Editor de código é uma ferramenta do Adobe Experience Manager (AEM) Forms que permite escrever scripts e códigos personalizados para funcionalidades mais complexas e avançadas em seus formulários. Aqui, discutimos alguns casos de uso:

* Quando for necessário implementar lógica ou comportamento personalizado do lado do cliente que vá além dos recursos do Editor de regras do AEM Forms. O Editor de código permite escrever código JavaScript para lidar com interações, cálculos ou validações complexas.
* Se o formulário exigir processamento do lado do servidor ou integração com sistemas externos, você poderá usar o Editor de códigos para gravar um script personalizado do lado do servidor. Você pode acessar a API guideBridge no editor de código para implementar qualquer lógica complexa em eventos e objetos de formulário.
* Quando você precisa de interfaces de usuário altamente personalizadas que vão além dos recursos padrão dos componentes do AEM Forms, o Editor de código permite implementar estilos e comportamentos personalizados ou até mesmo criar componentes de formulário personalizados.
* Se o formulário envolver operações assíncronas, como carregamento de dados assíncrono, você poderá usar o Editor de códigos para gerenciar essas operações por meio do código JavaScript assíncrono personalizado.

É importante observar que o uso do Editor de código requer uma boa compreensão da arquitetura do JavaScript e do AEM Forms. Além disso, ao implementar o código personalizado, siga as práticas recomendadas, siga as diretrizes de segurança e teste completamente seu código para evitar possíveis problemas em ambientes de produção. Você pode implementar um retorno de chamada para o FDM usando o editor de código.

O Editor de códigos está disponível somente para o componente do AEM Forms Foundation. Para os Componentes principais do formulário adaptável, você pode usar funções personalizadas para criar suas próprias regras de formulário, descritas na próxima seção.

### Funções personalizadas {#custom-client-libs}

O uso de bibliotecas de clientes personalizadas no AEM Forms (Adobe Experience Manager Forms) pode ser benéfico em vários cenários para aprimorar a funcionalidade, o estilo ou o comportamento de seus formulários. Estas são algumas situações em que o uso de bibliotecas de clientes personalizadas pode ser apropriado:

* Se você precisar implementar um design ou uma marca exclusiva para seus formulários, que vão além dos recursos das opções de estilo padrão fornecidas pelo AEM Forms, poderá optar por criar bibliotecas de clientes personalizadas para controlar a aparência.
* Quando você precisa de lógica personalizada do lado do cliente, reutilização de métodos em vários formulários ou comportamentos que não podem ser obtidos por meio dos recursos padrão do AEM Forms. Isso pode incluir interações de formulário dinâmicas, validação personalizada ou integração com bibliotecas de terceiros.
* Para melhorar o desempenho dos formulários otimizando e minificando os recursos do lado do cliente. Bibliotecas de clientes personalizadas podem ser usadas para agrupar e compactar arquivos JavaScript e CSS, reduzindo o tempo geral de carregamento da página.
* Quando é necessário integrar bibliotecas ou estruturas JavaScript adicionais que não estão incluídas na configuração padrão do AEM Forms. Isso pode ser necessário para recursos como seletores de data aprimorados, gráficos ou outros componentes interativos.

Antes de decidir usar bibliotecas personalizadas de clientes, é importante considerar a sobrecarga de manutenção, os possíveis conflitos com atualizações futuras e a adesão às práticas recomendadas. Certifique-se de que suas personalizações estejam bem documentadas e testadas para evitar problemas durante as atualizações ou ao colaborar com outros desenvolvedores.

>[!NOTE]
> A Função personalizada está disponível para Componentes do AEM Forms Foundation e Componentes principais.

**Vantagens das funções personalizadas:**

**Funções personalizadas** oferecem uma vantagem notável sobre a **Editor de código** porque fornece uma separação clara entre conteúdo e código, o que melhora a colaboração e simplifica os fluxos de trabalho. É recomendável usar funções personalizadas para as seguintes vantagens:

* **Use o controle de versão facilmente como o Git:**
   * O isolamento do código do conteúdo reduz significativamente os conflitos do Git durante o gerenciamento de conteúdo e promove um repositório bem organizado.
   * As Funções personalizadas são valiosas para projetos com vários colaboradores que trabalham simultaneamente.

* **Benefícios técnicos:**
   * Funções personalizadas oferecem modularidade e encapsulamento.
   * Os módulos podem ser desenvolvidos, testados e mantidos de forma independente.
   * Aumenta a reutilização e a capacidade de manutenção do código.

* **Processo de desenvolvimento eficiente:**
   * A modularidade permite que os desenvolvedores se concentrem em funcionalidades específicas.
   * Diminui o fardo dos desenvolvedores ao reduzir as complexidades de toda a base de código para um processo de desenvolvimento mais eficiente.



