---
title: Práticas recomendadas para trabalhar com formulários adaptáveis
seo-title: Best practices for working with adaptive forms
description: Explica as práticas recomendadas para configurar um projeto do AEM Forms, desenvolver formulários adaptáveis e otimizar o desempenho do sistema AEM Forms.
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: 64ba9b1082e39552cd27e5616de2a35f7870270b
workflow-type: tm+mt
source-wordcount: '4398'
ht-degree: 0%

---

# Práticas recomendadas para trabalhar com formulários adaptáveis {#best-practices-for-working-with-adaptive-forms}

## Visão geral {#overview}

Os formulários Adobe Experience Manager (AEM) podem ajudar você a transformar transações complexas em experiências digitais simples e deliciosas. No entanto, requer um esforço concertado para implementar, construir, executar e manter um ecossistema AEM Forms eficiente e produtivo.

Este documento fornece diretrizes e recomendações que o administrador, autores e desenvolvedores de formulários podem aproveitar ao trabalhar com o AEM Forms, especialmente o componente de formulários adaptáveis. Ele discute as práticas recomendadas desde a configuração de um projeto de desenvolvimento de formulários até a configuração, personalização, criação e otimização do AEM Forms. Essas práticas recomendadas contribuem coletivamente para o desempenho geral do ecossistema AEM Forms.

Além disso, veja algumas leituras recomendadas para práticas recomendadas gerais de AEM:

* [Práticas recomendadas: Implantação e manutenção de AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas: Criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas: Administrar AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas: Desenvolver soluções](/help/sites-developing/best-practices.md)

## Configurar e configurar o AEM Forms {#set-up-and-configure-aem-forms}

### Configurar um projeto de desenvolvimento de formulários {#setting-up-forms-development-project}

Uma estrutura de projeto simplificada e padronizada pode reduzir significativamente os esforços de desenvolvimento e manutenção. O Apache Maven é uma ferramenta de código aberto recomendada para criar projetos AEM.

* Usar o Apache Maven `aem-project-archetype` para criar e gerenciar a estrutura para AEM projeto. Ele cria a estrutura e os modelos recomendados para o seu projeto de AEM. Além disso, ele fornece sistemas de automação de compilação e controle de alterações para ajudar a gerenciar o projeto.

   * Use o maven `archetype:generate` para gerar a estrutura inicial.
   * Use maven `eclipse:eclipse` para gerar os arquivos de projeto do eclipse e importar o projeto para o eclipse.

Para obter mais informações, consulte [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

* A ferramenta FileVault ou VLT ajuda a mapear o conteúdo de uma instância CRX ou AEM para seu sistema de arquivos. Ele fornece operações de gerenciamento de controle de alterações, como check-in e check-out do conteúdo AEM projeto. Consulte [Como usar a ferramenta VLT](/help/sites-developing/ht-vlttool.md).

* Se você usar o ambiente de desenvolvimento integrado do Eclipse, poderá usar as ferramentas do Desenvolvedor AEM para integração perfeita do Eclipse IDE com instâncias AEM para criar aplicativos AEM. Para obter detalhes, consulte [Ferramentas de desenvolvedor AEM para Eclipse](/help/sites-developing/aem-eclipse.md).

* Não armazene conteúdo ou faça modificações na pasta /libs. Crie sobreposições em pastas /app para estender ou substituir funcionalidades padrão.

* Ao criar pacotes para mover o conteúdo, certifique-se de que os caminhos de filtro de pacote estejam corretos e que apenas os caminhos necessários sejam mencionados.

* Não armazene conteúdo ou faça modificações na pasta /libs. Crie sobreposições em pastas /app para estender ou substituir funcionalidades padrão.

* Defina as dependências corretas para os pacotes forçarem uma ordem/sequência de instalação predeterminada.

* Não crie nenhum nó referenciável em /libs ou /apps.

### Planejamento para o ambiente de criação {#planning-for-authoring-environment}

Depois de configurar seu AEM projeto, defina a estratégia para criar e personalizar modelos e componentes de formulários adaptáveis.

* Um modelo de formulário adaptável é uma página AEM especializada que define a estrutura e as informações do cabeçalho e do rodapé de um formulário adaptável. Um modelo tem layouts, estilos e estrutura básica pré-configurados para um formulário adaptável. O AEM Forms fornece modelos e componentes prontos para uso que podem ser usados para criar formulários adaptáveis. No entanto, você pode criar modelos e componentes personalizados de acordo com suas necessidades. É recomendável reunir os requisitos para modelos e componentes adicionais que você precisará em seus formulários adaptáveis. Para obter detalhes, consulte [Personalização de formulários e componentes adaptáveis](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* O AEM Forms permite criar formulários adaptáveis com base nos seguintes modelos de formulário. Os modelos de formulário atuam como interface para a troca de dados entre um formulário e um sistema de AEM e fornecem uma estrutura baseada em XML para o fluxo de dados dentro e fora de um formulário adaptável. Além disso, os modelos de formulário impõem regras e restrições em formulários adaptáveis na forma de restrições de esquema e XFA.

   * **Nenhum**: Os formulários adaptáveis criados com essa opção não usam nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.
   * **Esquema XML ou JSON**: Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. Você pode associar um esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis na guia Objeto do modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. Você pode arrastar e soltar os elementos do esquema para criar o formulário.
   * **Modelo de formulário XFA**: É um modelo de formulário ideal se você tiver investimentos em formulários HTML5 baseados em XFA. Ele fornece uma maneira direta de converter formulários baseados em XFA em formulários adaptáveis. Quaisquer regras XFA existentes são retidas nos formulários adaptáveis associados. Os formulários adaptáveis resultantes são compatíveis com construções XFA, como validações, eventos, propriedades e padrões.
   * **Modelo de dados do formulário**: É um modelo de formulário preferencial se você estiver procurando integrar seus sistemas de backend como bancos de dados, serviços da Web e AEM perfil de usuário para preencher previamente formulários adaptáveis e gravar dados de formulário enviados de volta nos sistemas de back-end. Um editor de Modelo de dados de formulário permite definir e configurar entidades e serviços em um modelo de dados de formulário que pode ser usado para criar formulários adaptáveis. Para obter mais informações, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

É importante escolher cuidadosamente o modelo de dados que não apenas atende aos seus requisitos, como estende seus investimentos existentes em ativos XFA e XSD, se houver. É recomendável usar o Modelo XSD para criar modelos de formulário, pois o XML gerado contém dados de acordo com o XPATH definido pelo esquema. Usar o Modelo XSD como uma opção padrão para o Modelo de dados de formulário também ajuda porque dissocia o design de formulário do sistema de back-end que processa e consome dados e melhora o desempenho do formulário devido a um para um mapeamento do campo de formulário. Além disso, BindRef do campo pode ser transformado em XPATH de seu valor de dados em XML.

Para obter mais informações, consulte [Criar um formulário adaptável](/help/forms/using/creating-adaptive-form.md).

* Há algumas seções comuns em formulários adaptáveis. Você pode identificá-los e definir uma estratégia para promover a reutilização do conteúdo. Formulários adaptáveis permitem criar fragmentos independentes e reutilizá-los em formulários. Também é possível salvar um painel em um formulário adaptável como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários associados. Ajuda a reduzir o tempo de criação e garante a consistência entre formulários. Além disso, o uso de fragmentos torna os formulários adaptáveis leves, resultando em uma melhor experiência de criação, especialmente de formulários grandes. Para obter mais informações, consulte [Fragmentos de formulário adaptáveis](/help/forms/using/adaptive-form-fragments.md).

### Personalização de formulários e componentes adaptáveis {#customize-components}

* O AEM Forms fornece modelos de formulário adaptáveis prontos para uso que podem ser usados para criar formulários adaptáveis. Você também pode criar seus próprios templates. AEM fornece modelos estáticos e editáveis.

   * Os modelos estáticos são definidos e configurados pelos desenvolvedores.
   * Os modelos editáveis são criados por autores usando o editor de modelo. O editor de modelo permite definir uma estrutura básica e um conteúdo inicial em um modelo. Qualquer modificação na camada de estrutura é refletida em todos os formulários que usam esse modelo. O conteúdo inicial pode incluir tema pré-configurado, serviço de preenchimento prévio, ação de envio e assim por diante. No entanto, essas configurações podem ser modificadas para um formulário usando o editor de formulários. Para obter mais informações, consulte [Modelos de formulário adaptável](/help/forms/using/template-editor.md).

* Para criar estilo em um campo ou instância de painel específico, use [estilo em linha](/help/forms/using/inline-style-adaptive-forms.md). Como alternativa, você pode definir uma classe em um arquivo CSS e especificar o nome da classe na propriedade Classe CSS do componente.
* Inclua uma biblioteca do cliente em um componente para aplicar estilos de maneira consistente em formulários adaptáveis ou fragmentos que usam esse componente. Para obter mais informações, consulte [Criar um componente de página de formulário adaptável](/help/forms/using/custom-adaptive-forms-templates.md).
* Aplique estilos definidos em uma biblioteca do cliente para selecionar formulários adaptáveis especificando o caminho para a biblioteca do cliente no campo de caminho do arquivo CSS nas propriedades do contêiner de formulário adaptável.
* Para criar uma biblioteca do cliente de seus estilos, você pode configurar o arquivo CSS personalizado na clientlib base do Editor de temas ou nas propriedades do Contêiner de formulários.
* Os formulários adaptáveis fornecem layouts de painel, como responsivos, com guias, opções e assistentes, para controlar como os componentes do formulário são posicionados em um painel. Você pode criar layouts de painel personalizados e disponibilizá-los para uso por autores de formulários. Para obter mais informações, consulte [Criação de componentes de layout personalizados para formulários adaptáveis](/help/forms/using/custom-layout-components-forms.md).
* Você também pode personalizar componentes de formulário adaptáveis específicos, como campos e layout do painel.

   * Use o [Sobreposição](/help/sites-developing/overlays.md) funcionalidade de AEM para modificar uma cópia de um componente. Não é recomendado modificar componentes padrão.
   * Para personalizar o layout dos componentes de formulário adaptáveis prontos para uso em /libs, [criar componentes de layout personalizados](/help/forms/using/custom-layout-components-forms.md) além do [layouts padrão](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduza interatividades personalizadas criando widgets ou aparências personalizados. Não é recomendado modificar componentes padrão. Para obter mais informações, consulte [Estrutura de aparência](/help/forms/using/introduction-widgets.md).

* Consulte [Tratamento de informações pessoais identificáveis](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) para recomendações sobre o tratamento de dados de PII.

## Formulários adaptáveis do autor {#author-adaptive-forms}

### Usar a interface otimizada para toque para criação {#using-touch-optimized-ui-for-authoring}

* Use o navegador Objetos na barra lateral para acessar rapidamente os campos na hierarquia do formulário. Use a caixa de pesquisa para procurar objetos na árvore de formulários ou objetos para navegar de um objeto para outro.
* Para exibir e editar as propriedades de um componente no navegador de componentes na barra lateral, selecione o componente e clique em ![cmppr-1](assets/cmppr-1.png). Você também pode clicar duas vezes em um componente para exibir suas propriedades no navegador de propriedades.
* Use atalhos de teclado para realizar ações rápidas em seus formulários. Consulte [Atalhos de teclado do AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Os componentes de formulário adaptável são recomendados para uso somente em páginas de formulário adaptáveis. Os componentes têm dependência de sua hierarquia principal. Portanto, não os use em uma página AEM.

Além disso, consulte descrições de componentes e práticas recomendadas em [Introdução à criação de formulários adaptáveis](/help/forms/using/introduction-forms-authoring.md).

### Uso de regras em formulários adaptáveis {#using-rules-in-adaptive-forms}

A AEM Forms fornece uma [editor de regras](/help/forms/using/rule-editor.md) que permite criar regras para adicionar comportamento dinâmico aos componentes de formulário adaptáveis. Usando essas regras, é possível avaliar as condições e acionar ações em componentes, como mostrar ou ocultar campos, calcular valores, alterar dinamicamente a lista suspensa e assim por diante.

O editor de regras fornece um editor visual e um editor de códigos para escrever regras. Considere o seguinte ao gravar regras usando o modo editor de código:

* Use nomes significativos e exclusivos para campos e componentes de formulário para evitar possíveis conflitos ao gravar regras.
* Use `this` para um componente se referir a si mesmo em uma expressão de regra. Ela garante que a regra permaneça válida mesmo se o nome do componente for alterado. Por exemplo, `field1.valueCommit script: this.value > 10`.

* Use nomes de componentes ao se referir a outros componentes de formulário. Use o `value` propriedade para buscar o valor de um campo ou componente. Por exemplo, `field1.value`.

* Consulte os componentes por hierarquia exclusiva relativa para evitar qualquer conflito. Por exemplo, `parentName.fieldName`.

* Ao manipular regras complexas ou de uso comum, considere escrever lógica de negócios como funções em uma biblioteca cliente separada que você pode especificar e reutilizar em formulários adaptáveis. A biblioteca do cliente deve ser uma biblioteca independente e não deve ter dependências externas, exceto em jQuery e Underscore.js. Você também pode usar a biblioteca do cliente para impor [revalidação do lado do servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) de dados de formulário enviados.
* Os formulários adaptáveis fornecem um conjunto de APIs que podem ser usadas para se comunicar e executar ações em formulários adaptáveis. Algumas das principais APIs são as seguintes. Para obter mais informações, consulte [Referência da API da biblioteca JavaScript para Adaptive Forms](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: Redefine um formulário.
   * `guideBridge.submit()`: Envia um formulário.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Define o foco de um campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: Valida um formulário.
   * `guideBridge.getDataXML(options)`: Obtém dados de formulário como XML.
   * `guideBridge.resolveNode(somExpression)`: Obtém um objeto de formulário.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Define a propriedade de um objeto de formulário.
   * Além disso, é possível usar as seguintes propriedades de campo:

      * `field.value` para alterar o valor de um campo.
      * f `ield.enabled` para ativar/desativar um campo.
      * `field.visible` para alterar a visibilidade de um campo.

* Os autores de formulários adaptativos podem precisar gravar o código JavaScript para criar a lógica comercial em um formulário. Embora o JavaScript seja eficiente e eficaz, é provável que possa comprometer as expectativas de segurança. Portanto, é necessário garantir que o autor do formulário seja uma pessoa confiável e que haja processos para revisar e aprovar o código JavaScript antes que um formulário seja colocado em produção. O administrador pode restringir o acesso ao editor de regras para grupos de usuários com base em sua função ou função. Consulte [Conceder acesso ao editor de regras para grupos de usuários selecionados](/help/forms/using/rule-editor-access-user-groups.md).
* É possível usar expressões em regras para tornar os formulários adaptáveis dinâmicos. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter mais informações sobre expressões e práticas recomendadas, consulte [Expressões de formulário adaptável](/help/forms/using/adaptive-form-expressions.md).

### Trabalhar com temas {#working-with-themes}

Adaptável para temas permite criar estilos reutilizáveis que podem ser aplicados em formulários para proporcionar aparência e estilo consistentes. É recomendável usar Temas para definir o estilo de componentes e painéis de formulário. Algumas práticas recomendadas em torno de temas são as seguintes:

* Use a biblioteca de ativos para uma aplicação rápida de estilos de texto, plano de fundo e imagens. Quando um estilo é adicionado na biblioteca de ativos, ele fica disponível para outros temas e no modo de estilo do editor de formulários.
* Aplique configurações globais como fonte e plano de fundo da página usando o seletor de nível de página.
* Use as bibliotecas de clientes para importar o estilo existente ou avançado para os seus temas.
* É possível substituir o estilo de campos, painéis ou botões específicos em uma camada de estilo de formulário.
* Se um tema não atender ao seu requisito de estilo, use classes predefinidas, como guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode para aplicar um estilo comum em formulários.

Para obter mais informações, consulte [Temas](/help/forms/using/themes.md).

### Otimização do desempenho de formulários grandes e complexos {#optimizing-performance-of-large-and-complex-forms}

Geralmente, os autores e usuários finais enfrentam problemas de desempenho ao carregar formulários grandes no modo de criação ou no tempo de execução. À medida que o número de objetos (campos e painéis) no formulário aumenta, a criação e a experiência de tempo de execução começam a degradar-se. Também impede que vários autores colaborem e criem um formulário simultaneamente.

Considere as seguintes práticas recomendadas para superar problemas de desempenho com formulários grandes:

* É recomendável criar formulários adaptáveis usando o modelo de dados de formulário XSD, mesmo ao converter um XFA em um formulário adaptável, se possível.
* Inclua apenas os campos e painéis em formulários adaptáveis que capturam informações do usuário. Considere manter o conteúdo estático mínimo ou use URLs para abri-los em uma janela separada.
* Embora cada formulário seja projetado para uma finalidade específica, há alguns segmentos comuns na maioria dos formulários. Por exemplo, detalhes pessoais, endereço, detalhes de emprego e assim por diante. Criar [fragmentos de formulário adaptáveis](/help/forms/using/adaptive-form-fragments.md) para elementos e seções de formulário comuns e usá-los em formulários. Também é possível salvar um painel em um formulário existente como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários adaptáveis associados. Ela promove a criação colaborativa, pois vários autores podem trabalhar simultaneamente em diferentes fragmentos que compõem um formulário.

   * Semelhante aos formulários adaptáveis, é recomendável que todos os estilos específicos de fragmento e scripts personalizados sejam definidos na biblioteca do cliente usando a caixa de diálogo contêiner de fragmento. Além disso, tente criar fragmentos autossuficientes que não dependam de objetos fora dele.
   * Evite usar scripts entre fragmentos. Se houver algum objeto fora do fragmento que você deve consultar, tente tornar esse objeto parte do formulário pai. Se o objeto ainda precisar estar em outro fragmento, consulte-o pelo nome no script.

* Use Salvar e retomar com o salvamento automático para salvar o formulário adaptável periodicamente e permitir que os usuários retornem posteriormente para preencher o formulário.
* Configure os fragmentos para carregar de maneira lenta. No tempo de execução, o fragmento marcado para carregar lentamente é renderizado somente quando necessário. Reduz significativamente o tempo de carregamento de formulários grandes. Também é compatível com fragmentos com painéis repetíveis. Para obter mais informações, consulte [Configurar carregamento lento](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Não configure o carregamento lento em fragmentos em um layout de grade responsivo ou no primeiro painel.
   * O anexo de arquivo e os componentes Termos e condições não são suportados em fragmentos carregados de forma preguiçosa.
   * Marque um valor em um painel carregado lento como Usar valor globalmente, se esse valor for usado em alguma outra parte do formulário, de modo que o valor esteja disponível para uso quando o painel contêiner for descarregado.
   * Considere escrever regras de visibilidade para fragmentos que devem mostrar ou ocultar com base em uma condição.
* Defina o valor da variável **Número de chamadas por solicitação** no **Servlet principal Apache Sling** para um número bastante grande. Ela permite que o servidor do Forms permita chamadas adicionais. A configuração exibe um valor padrão de 1500. O valor, 1500 chamadas, é para outros componentes do Experience Manager, como Sites e Ativos. O conjunto de valores padrão de formulários adaptáveis é 20000. Se você encontrar a variável `too many calls` em logs ou o formulário não for renderizado, tente aumentar o valor para um grande número para resolver o problema. Se o número de chamadas for superior a 20000, significa que o formulário é complexo e pode levar algum tempo para renderizar o formulário no navegador. Isso só acontece pela primeira vez em que o formulário é carregado, depois que o formulário é armazenado em cache e, uma vez armazenado em cache, não há impacto significativo no desempenho.

### Preenchimento prévio de formulários adaptáveis {#prefilling-adaptive-forms}

É possível preencher previamente campos de formulário adaptáveis com dados obtidos do backend para ajudar os usuários a preencher rapidamente o formulário e evitar erros de digitação.

* O AEM Forms fornece um serviço de preenchimento prévio para ler dados de um arquivo XML de dados predefinido e preencher previamente os campos de um formulário adaptável com o conteúdo no arquivo XML de preenchimento prévio.
* O XML de dados de preenchimento prévio deve estar em conformidade com o esquema do modelo de formulário associado ao formulário adaptável.
* Incluir `afBoundedData` e `afUnBoundedData` no XML de preenchimento prévio para preencher os campos vinculados e não vinculados em um formulário adaptável.

* Para formulários adaptáveis com base no modelo de dados de formulário, o AEM Forms fornece o Serviço de preenchimento prévio do modelo de dados de formulário pronto para uso. O serviço de preenchimento prévio consulta fontes de dados para objetos de modelo de dados no formulário adaptável e preenche os valores de campo ao renderizar o formulário.
* Também é possível usar os protocolos de arquivo, crx, service ou http para preencher formulários adaptáveis.
* O AEM Forms oferece suporte a serviços de preenchimento prévio personalizados, que podem ser conectados como um serviço OSGi para preencher previamente formulários adaptáveis.

Para obter mais informações, consulte [Preencher previamente campos de formulário adaptáveis](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Assinar e enviar formulários adaptáveis {#signing-and-submitting-adaptive-forms}

Formulários adaptáveis exigem ações de envio para processar dados especificados pelo usuário. Uma ação Enviar determina a tarefa executada nos dados enviados por meio de um formulário adaptável.

* Há várias ações de envio disponíveis prontas para uso em formulários adaptáveis. Para obter detalhes, consulte [Configuração da ação Enviar](/help/forms/using/configuring-submit-actions.md).
* Você pode gravar uma ação de envio personalizada se as ações de envio padrão não atenderem ao seu caso de uso. Para obter mais informações, consulte [Gravação da ação de Enviar personalizado para formulários adaptáveis](/help/forms/using/custom-submit-action-form.md).
* Incluir validações do lado do servidor para impedir o envio de dados inválidos.

Você pode aproveitar a experiência de vários sinais do Adobe Sign em formulários adaptáveis. Considere o seguinte ao configurar o Adobe Sign em formulários adaptáveis. Para obter detalhes, consulte [Uso do Adobe Sign em um formulário adaptável](/help/forms/using/working-with-adobe-sign.md).

* O formulário adaptável habilitado para Adobe Sign é enviado somente após todos os signatários terem assinado o formulário. O Forms é exibido no estado Sinal pendente até que o formulário seja assinado por todos os signatários.
* Você pode configurar a experiência de assinatura no formulário ou redirecionar assinantes para uma página de assinatura no envio.
* Configure a experiência de assinatura sequencial ou paralela, conforme apropriado.

### Gerando documento de registro {#generating-document-of-record}

Um documento de registro (DoR) é uma versão PDF nivelada de um formulário adaptável que pode ser impresso, assinado ou arquivado.

* Dependendo do modelo de dados de formulário no qual um formulário adaptável é baseado, é possível configurar um modelo para DoR da seguinte maneira:

   * **Modelo de formulário XFA**: Use o arquivo XDP associado como o modelo DoR.
   * **Esquema XSD**: Use o modelo XFA associado que usa o mesmo esquema XML usado pelo formulário adaptável.
   * **Nenhum**: Usar DoR gerado automaticamente.

* Configure o cabeçalho, o rodapé, as imagens, a cor, a fonte e assim por diante, diretamente da guia Document of Record do editor de formulário adaptável.
* Use `DoRService` para gerar o DoR de forma programática.
* Excluir campos ocultos do DoR.
* Use `afAcceptLang` parâmetro de solicitação para exibir DoR em outra localidade.

### Depuração e teste de formulários adaptáveis {#debugging-and-testing-adaptive-forms}

[Plug-in do AEM Chrome](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) é uma extensão de navegador para o Google Chrome que fornece ferramentas para depurar formulários adaptáveis. Os autores e desenvolvedores de formulários podem usar essas ferramentas para:

* Identificar gargalos e otimizar o desempenho da renderização do formulário
* Depurar palavras-chave e erros bindRef no formulário
* Habilitar e configurar logs
* Regras e scripts de depuração no formulário
* Explore e saiba mais sobre APIs do guideBridge

Para obter mais informações, consulte [Plug-in do AEM Chrome - Formulário adaptável](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

O SDK do Calvin é uma API de utilitário para os desenvolvedores do Adaptive Forms testarem o Adaptive Forms. O SDK do Calvin é criado sobre [Estrutura de teste do Hobbes.js](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html). Você pode usar a estrutura para testar o seguinte:

* Experiência de representação de um formulário adaptável
* Experiência de preenchimento prévio de um formulário adaptável
* Enviar experiência de um formulário adaptável
* Regras de expressão
* Validações
* Carregamento lento

Para obter mais informações, consulte [Automatizar o teste de formulários adaptáveis](/help/forms/using/calvin.md).

### Validação de formulários adaptáveis no servidor AEM {#validating-adaptive-forms-on-aem-server}

As validações do lado do servidor são necessárias para impedir qualquer tentativa de ignorar validações no cliente e qualquer possível compromisso de envios de dados e violações de regras comerciais. As validações do lado do servidor são executadas no servidor carregando a biblioteca do cliente necessária.

* Inclua funções em uma biblioteca do cliente para validar expressões em formulários adaptáveis e especifique a biblioteca do cliente na caixa de diálogo contêiner de formulários adaptáveis. Para obter mais informações, consulte [Revalidação do lado do servidor](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca cliente separada para validações e não misturá-la com outras coisas, como estilo de HTML e manipulação de DOM na mesma biblioteca do cliente.

### Localização de formulários adaptáveis {#localizing-adaptive-forms}

AEM fornece fluxos de trabalho de tradução que podem ser usados para localizar formulários adaptáveis. Para obter mais informações, consulte [Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Algumas práticas recomendadas ao localizar formulários adaptáveis são as seguintes:

* Use fragmentos de formulário adaptáveis para elementos comuns em formulários e localize fragmentos. Isso garante que você localize um fragmento uma vez e ele reflita em todos os formulários, onde o fragmento localizado é usado.
* Quaisquer modificações, como adicionar um novo componente ou aplicar um script em um formulário localizado, não são localizadas automaticamente. Portanto, é necessário finalizar um formulário antes de localizá-lo para evitar vários ciclos de localização.
* Use `afAcceptLang` parâmetro de solicitação para substituir a localidade do navegador e renderizar o formulário na localidade especificada. Por exemplo, o URL a seguir forçará a renderização do formulário no idioma japonês, independentemente do local especificado na configuração do navegador:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Atualmente, o AEM Forms suporta a localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). No entanto, é possível adicionar suporte a novas localidades para formulários adaptáveis em tempo de execução. Para obter mais informações, consulte [Suporte a novas localidades para localização de formulários adaptáveis](/help/forms/using/supporting-new-language-localization.md).

## Preparar projeto de formulários para produção {#prepare-forms-project-for-production}

### Adicionar servidor de processamento de formulários {#adding-forms-processing-server}

Você pode configurar uma instância adicional do servidor AEM Forms que fica atrás do firewall em uma zona segura. Você pode usar essa instância para:

* **Processamento em lote**: trabalhos que são recorrentes ou programados em lotes com carga pesada. Por exemplo, impressão de declarações, geração de correspondências e uso de serviços de documento como PDF Generator, Output e Assembler.
* **Armazenamento de dados de PII**: Salve os dados de PII no servidor de processamento. Não é necessário se você já estiver usando um provedor de armazenamento personalizado para armazenar dados PII.

### Transferência do projeto para outro ambiente {#moving-project-to-another-environment}

Geralmente, é necessário mover seus projetos de AEM de um ambiente para outro. Algumas das coisas-chave a lembrar ao mover-se são as seguintes:

* Faça backup das bibliotecas de clientes, código personalizado e configurações existentes.
* Implante pacotes de produtos e patches manualmente e na ordem especificada no novo ambiente.
* Implante pacotes de código específicos do projeto manualmente e como um pacote ou pacote separado no novo servidor de AEM.
* (*AEM Forms somente no JEE*) Implante LCAs e DSCs manualmente no servidor Forms Workflow.
* Use [Exportar-Importar](/help/forms/using/import-export-forms-templates.md) para mover ativos para o novo ambiente. Você também pode configurar o agente de replicação e publicar os ativos.
* Ao atualizar, substitua todas as APIs e recursos obsoletos por novas APIs e novos recursos.

### Configuração de AEM {#configuring-aem}

Algumas práticas recomendadas para configurar o AEM para melhorar o desempenho geral são as seguintes:

* Ative a compactação da biblioteca do cliente HTML para JavaScript e CSS a partir do Felix Console.
* Armazene em cache todas as bibliotecas de clientes em `/etc.clientlibs/fd` e quaisquer bibliotecas personalizadas adicionais do cliente no AEM dispatcher para aumentar a capacidade de resposta e a segurança de seus formulários publicados. Para obter mais informações, consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Não armazenar em cache `/content/forms/af/` e `/content/dam/formsanddocuments/*` caminhos. para obter informações detalhadas sobre como configurar o armazenamento de formulários adaptáveis em cache, consulte [Armazenamento em cache de formulários adaptáveis](/help/forms/using/configure-adaptive-forms-cache.md).

* Ative o HTML por meio do módulo de compactação do servidor da Web. Para obter mais informações, consulte [Ajuste de desempenho do servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumente as chamadas por configuração de solicitação para formulários grandes. Consulte [Otimização do desempenho de formulários grandes e complexos](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Criar [páginas de erro personalizadas mostradas pelo manipulador de erros](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* Servidor AEM Forms seguro.

   * Use `nosamplecontent` modo de execução para garantir que não haja conteúdo de amostra e usuários de amostra implantados no servidor de produção. Consulte [Executando AEM no modo Pronto para produção](/help/sites-administering/production-ready.md).

* Mantenha o tamanho do heap até um mínimo de 8 GB. Para outras configurações, consulte [Ajuste de desempenho do servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Use sessões de usuário de serviço em vez de sessões de administrador para executar tarefas de nível de serviço. Para obter mais informações, consulte [Autenticação de serviço](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuração do armazenamento externo para rascunhos e dados de formulários enviados {#external-storage}

Em um ambiente de produção, é recomendável não armazenar os dados de formulário enviados em AEM repositório. A implementação padrão das ações Forms Portal Store, Store Content e Store PDF submit armazenam dados de formulário em AEM repositório. Essas ações de envio destinam-se somente a fins de demonstração. Além disso, os recursos Salvar e Retomar e Salvar automaticamente usam o armazenamento do portal por padrão. Portanto, considere as seguintes recomendações:

* **Armazenamento de dados de rascunho**: Se estiver usando o recurso Rascunho de formulários adaptáveis, você deve implementar uma SPI (Service Provider Interface) personalizada para armazenar dados de rascunho em armazenamento mais seguro, como banco de dados. Para obter mais informações, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

* **Armazenamento de dados de envio**: Se estiver usando o armazenamento de envio do portal de formulários, você deve implementar um SPI personalizado para armazenar dados de envio em um banco de dados. Consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md) para obter uma integração de amostra.

   Você também pode gravar uma ação de envio personalizada que armazena dados e anexos de formulário em armazenamento seguro. Consulte [Gravação da ação de Enviar personalizado para formulários adaptáveis](/help/forms/using/custom-submit-action-form.md) para obter mais informações.

* **Comprimento da ID de rascunho**: Ao salvar um formulário adaptável como rascunho, uma ID de rascunho é gerada para identificar exclusivamente o rascunho. O valor mínimo para o comprimento do campo de ID de rascunho é de 26 caracteres. O Adobe recomenda definir o comprimento da ID de rascunho para 26 ou mais caracteres.

### Tratamento de informações pessoais identificáveis {#handling-personally-identifiable-information}

Um dos principais desafios para as organizações é como lidar com dados de identificação pessoal (PII). Algumas práticas recomendadas que ajudarão você a lidar com esses dados são as seguintes:

* Use um armazenamento externo seguro, como banco de dados, para armazenar dados de rascunhos e formulários enviados. Consulte [Configuração do armazenamento externo para rascunhos e dados de formulários enviados](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Use o componente de formulário Termos e condições para obter consentimento explícito do usuário antes de ativar o salvamento automático. Nesse caso, ative o salvamento automático somente quando o usuário concordar com as condições no componente Termos e condições .
