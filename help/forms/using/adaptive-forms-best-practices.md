---
title: Práticas recomendadas para trabalhar com formulários adaptáveis
seo-title: Práticas recomendadas para trabalhar com formulários adaptáveis
description: Explica as práticas recomendadas para configurar um projeto AEM Forms, desenvolver formulários adaptáveis e otimizar o desempenho do sistema AEM Forms.
seo-description: Explica as práticas recomendadas para configurar um projeto AEM Forms, desenvolver formulários adaptáveis e otimizar o desempenho do sistema AEM Forms.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 0%

---


# Práticas recomendadas para trabalhar com formulários adaptáveis {#best-practices-for-working-with-adaptive-forms}

## Visão geral {#overview}

Os formulários Adobe Experience Manager (AEM) podem ajudá-lo a transformar transações complexas em experiências digitais simples e deliciosas. No entanto, requer um esforço concertado para implementar, construir, executar e manter um ecossistema AEM Forms eficiente e produtivo.

Este documento fornece orientações e recomendações que podem ser beneficiadas pelo administrador, autores e desenvolvedores de formulários ao trabalhar com a AEM Forms, especialmente componentes de formulários adaptáveis. Ele discute as práticas recomendadas desde a configuração de um projeto de desenvolvimento de formulários até a configuração, personalização, criação e otimização do AEM Forms. Essas práticas recomendadas contribuem coletivamente para o desempenho geral do ecossistema AEM Forms.

Além disso, veja algumas leituras recomendadas para as práticas recomendadas gerais AEM:

* [Práticas recomendadas: Implantação e manutenção de AEM](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas: Criação de conteúdo](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas: Administração de AEM](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas: Desenvolver soluções](/help/sites-developing/best-practices.md)

## Configurar e configurar o AEM Forms {#set-up-and-configure-aem-forms}

### Configurar o projeto de desenvolvimento de formulários {#setting-up-forms-development-project}

Uma estrutura de projeto simplificada e normalizada pode reduzir significativamente os esforços de desenvolvimento e manutenção. O Apache Maven é uma ferramenta de código aberto recomendada para a construção de projetos AEM.

* Use o Apache Maven `aem-project-archetype` para criar e gerenciar a estrutura para AEM projeto. Ele cria a estrutura e os modelos recomendados para seu projeto AEM. Além disso, fornece sistemas de automação de criação e controle de alterações para ajudar a gerenciar o projeto.

   * Use o `archetype:generate` comando maven para gerar a estrutura inicial.
   * Use o `eclipse:eclipse` comando maven para gerar os arquivos de projeto do eclipse e importar o projeto para o eclipse.

Para obter mais informações, consulte [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

* A ferramenta FileVault ou VLT ajuda a mapear o conteúdo de uma instância do CRX ou AEM para seu sistema de arquivos. Fornece operações de gerenciamento de controle de alterações, como check-in e check-out do conteúdo do projeto AEM. Consulte [Como usar a ferramenta](/help/sites-developing/ht-vlttool.md)VLT.

* Se você usar o ambiente de desenvolvimento integrado do Eclipse, poderá usar as ferramentas do desenvolvedor AEM para a integração perfeita do Eclipse IDE com instâncias AEM para criar aplicativos AEM. Para obter detalhes, consulte [AEM ferramentas de desenvolvedor para o Eclipse](/help/sites-developing/aem-eclipse.md).

* Não armazene conteúdo nem faça modificações na pasta /libs. Crie sobreposições em pastas /app para estender ou substituir funcionalidades padrão.

* Ao criar pacotes para mover o conteúdo, verifique se os caminhos do filtro de pacote estão corretos e se apenas os caminhos necessários estão mencionados.

* Não armazene conteúdo nem faça modificações na pasta /libs. Crie sobreposições em pastas /app para estender ou substituir funcionalidades padrão.

* Defina as dependências corretas para os pacotes para forçar uma ordem/sequência de instalação predeterminada.

* Não crie nenhum nó referenciável em /libs ou /apps.

### Planejamento para criação de ambientes {#planning-for-authoring-environment}

Depois de configurar seu projeto AEM, defina uma estratégia para criar e personalizar os modelos e componentes de formulários adaptáveis.

* Um modelo de formulário adaptável é uma página AEM especializada que define a estrutura e as informações do rodapé do cabeçalho de um formulário adaptável. Um modelo tem layouts, estilos e estrutura básica pré-configurados para um formulário adaptável. A AEM Forms fornece modelos e componentes prontos para uso que podem ser usados para criar formulários adaptáveis. No entanto, você pode criar modelos e componentes personalizados de acordo com suas necessidades. É recomendável reunir os requisitos para modelos e componentes adicionais de que você precisará em seus formulários adaptáveis. Para obter detalhes, consulte [Personalizar formulários e componentes](/help/forms/using/adaptive-forms-best-practices.md#customize-components)adaptáveis.
* A AEM Forms permite criar formulários adaptáveis com base nos seguintes modelos de formulário. Os modelos de formulário atuam como interface para troca de dados entre um formulário e um sistema AEM e fornecem uma estrutura baseada em XML para fluxo de dados dentro e fora de um formulário adaptável. Além disso, os modelos de formulário impõem regras e restrições aos formulários adaptáveis na forma de restrições de schema e XFA.

   * **Nenhum**: Os formulários adaptáveis criados com essa opção não usam nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.
   * **SCHEMA** XML ou JSON: Os schemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema back-end em sua organização. É possível associar um schema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do schema estão disponíveis na guia Objeto de modelo de dados do navegador de conteúdo para a criação de formulários adaptáveis. É possível arrastar e soltar os elementos do schema para criar o formulário.
   * **Modelo** de formulário XFA: É um modelo de formulário ideal se você tiver investimentos em formulários HTML5 baseados em XFA. Ele fornece uma maneira direta de converter seus formulários baseados em XFA em formulários adaptáveis. Quaisquer regras XFA existentes são mantidas nos formulários adaptativos associados. Os formulários adaptativos resultantes suportam construções XFA, como validações, eventos, propriedades e padrões.
   * **Modelo** de dados de formulário: É o modelo de formulário preferido se você estiver procurando integrar seus sistemas de backend, como bancos de dados, serviços da Web e AEM perfil do usuário para pré-preencher formulários adaptáveis e gravar dados de formulário enviados de volta nos sistemas de backend. Um editor de Modelo de dados de formulário permite que você defina e configure entidades e serviços em um modelo de dados de formulário que pode ser usado para criar formulários adaptáveis. Para obter mais informações, consulte Integração [de dados da](/help/forms/using/data-integration.md)AEM Forms.

É importante escolher cuidadosamente o modelo de dados que atende não apenas às suas necessidades, mas amplia seus investimentos existentes em ativos XFA e XSD, se houver. É recomendável usar o Modelo XSD para criar modelos de formulário, pois o XML gerado contém dados conforme o XPATH definido pelo schema. O uso do Modelo XSD como uma opção padrão para o Modelo de dados de formulário também ajuda porque ele dissocia o design de formulário do sistema back-end que processa e consome dados e melhora o desempenho do formulário devido a um mapeamento de um para um campo de formulário. Além disso, BindRef do campo pode tornar-se o XPATH de seu valor de dados em XML.

Para obter mais informações, consulte [Criar um formulário](/help/forms/using/creating-adaptive-form.md)adaptável.

* Há algumas seções comuns em formulários adaptáveis. É possível identificá-los e definir uma estratégia para promover a reutilização do conteúdo. Formulários adaptáveis permitem criar fragmentos independentes e reutilizá-los em formulários. Também é possível salvar um painel em um formulário adaptável como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários associados. Isso ajuda a reduzir o tempo de criação e garante a consistência entre os formulários. Além disso, o uso de fragmentos torna os formulários adaptáveis leves, resultando em uma melhor experiência de criação, especialmente de formulários grandes. Para obter mais informações, consulte [Fragmentos](/help/forms/using/adaptive-form-fragments.md)de formulário adaptáveis.

### Personalização de formulários e componentes adaptáveis {#customize-components}

* A AEM Forms fornece modelos de formulário adaptáveis prontos para uso que podem ser usados para criar formulários adaptáveis. Você também pode criar seus próprios modelos. AEM fornece modelos estáticos e editáveis.

   * Os modelos estáticos são definidos e configurados pelos desenvolvedores.
   * Os modelos editáveis são criados pelos autores usando o editor de modelos. O editor de modelos permite que você defina uma estrutura básica e um conteúdo inicial em um modelo. Qualquer modificação na camada de estrutura é refletida em todos os formulários que usam esse modelo. O conteúdo inicial pode incluir tema pré-configurado, serviço de pré-preenchimento, ação de envio e assim por diante. No entanto, essas configurações podem ser modificadas para um formulário usando o editor de formulários. Para obter mais informações, consulte Modelos [de formulário](/help/forms/using/template-editor.md)adaptáveis.

* Para estilizar um campo ou uma instância de painel específica, use o estilo [em linha](/help/forms/using/inline-style-adaptive-forms.md). Como alternativa, você pode definir uma classe em um arquivo CSS e especificar o nome da classe na propriedade Classe CSS do componente.
* Inclua uma biblioteca cliente em um componente para aplicar estilos consistentemente em formulários adaptáveis ou fragmentos que usam esse componente. Para obter mais informações, consulte [Criar um componente](/help/forms/using/custom-adaptive-forms-templates.md)de página de formulário adaptável.
* Aplique estilos definidos em uma biblioteca cliente para selecionar formulários adaptáveis especificando o caminho para a biblioteca do cliente no campo de caminho do arquivo CSS nas propriedades do container de formulário adaptável.
* Para criar uma biblioteca de cliente de seus estilos, você pode configurar o arquivo CSS personalizado na clientlib base do Editor de Temas ou nas propriedades do Container de Formulário.
* Formulários adaptáveis fornecem layouts de painel, como responsivos, tabulados, acordeões e assistente, para controlar como os componentes de formulário são posicionados em um painel. Você pode criar layouts de painel personalizados e disponibilizá-los para uso pelos autores de formulário. Para obter mais informações, consulte [Criação de componentes de layout personalizados para formulários](/help/forms/using/custom-layout-components-forms.md)adaptáveis.
* Você também pode personalizar componentes de formulário adaptáveis específicos, como campos e layout de painel.

   * Use a funcionalidade [Sobreposição](/help/sites-developing/overlays.md) do AEM para modificar uma cópia de um componente. Não é recomendado modificar componentes padrão.
   * Para personalizar o layout dos componentes de formulário adaptáveis prontos para uso em /libs, [crie componentes](/help/forms/using/custom-layout-components-forms.md) de layout personalizados além dos layouts [](/help/forms/using/layout-capabilities-adaptive-forms.md)padrão.
   * Introduza interatividades personalizadas criando widgets ou aparências personalizados. Não é recomendado modificar componentes padrão. Para obter mais informações, consulte [Estrutura](/help/forms/using/introduction-widgets.md)de aparência.

* Consulte [Manuseio de informações](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) de identificação pessoal para obter recomendações sobre como manipular dados de PII.

## Formulários adaptativos do autor {#author-adaptive-forms}

### Usar a interface otimizada ao toque para criação {#using-touch-optimized-ui-for-authoring}

* Use o navegador Objetos na barra lateral para acessar rapidamente os campos na hierarquia do formulário. Você pode usar a caixa de pesquisa para procurar objetos no formulário ou na árvore de objetos para navegar de um objeto para outro.
* Para visualização e edição das propriedades de um componente no navegador de componentes na barra lateral, selecione o componente e clique em ![cmppr-1](assets/cmppr-1.png). Você também pode clicar com o duplo em um componente para visualização de suas propriedades no navegador de propriedades.
* Use atalhos do teclado para executar ações rápidas em seus formulários. Consulte Atalhos de teclado [do](/help/forms/using/keyboard-shortcuts.md)AEM Forms.

* Os componentes de formulário adaptáveis são recomendados para uso somente em páginas de formulário adaptáveis. Os componentes dependem de sua hierarquia pai. Portanto, não os use em uma página AEM.

Além disso, consulte as descrições de componentes e as práticas recomendadas em [Introdução à criação de formulários](/help/forms/using/introduction-forms-authoring.md)adaptáveis.

### Uso de regras em formulários adaptáveis {#using-rules-in-adaptive-forms}

A AEM Forms fornece um editor [de](/help/forms/using/rule-editor.md) regras que permite criar regras para adicionar comportamento dinâmico aos componentes de formulário adaptáveis. Usando essas regras, é possível avaliar condições e acionar ações em componentes, como mostrar ou ocultar campos, calcular valores, alterar a lista suspensa dinamicamente e assim por diante.

O editor de regras fornece um editor visual e um editor de código para escrever regras. Considere o seguinte ao gravar regras usando o modo editor de código:

* Use nomes significativos e exclusivos para campos de formulário e componentes a fim de evitar possíveis conflitos ao escrever regras.
* Use `this` o operador para que um componente se refira a si mesmo em uma expressão de regra. Isso garante que a regra permaneça válida mesmo se o nome do componente for alterado. Por exemplo, `field1.valueCommit script: this.value > 10`.

* Use nomes de componentes ao fazer referência a outros componentes de formulário. Use a `value` propriedade para buscar o valor de um campo ou componente. Por exemplo, `field1.value`.

* Consulte os componentes por hierarquia exclusiva relativa para evitar qualquer conflito. Por exemplo, `parentName.fieldName`.

* Ao lidar com regras complexas ou comumente usadas, considere escrever lógica comercial como funções em uma biblioteca de cliente separada que você pode especificar e reutilizar em formulários adaptáveis. A biblioteca do cliente deve ser uma biblioteca independente e não deve ter dependências externas, exceto em jQuery e Underscore.js. Você também pode usar a biblioteca do cliente para impor a revalidação [do lado do](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) servidor dos dados de formulário enviados.
* Os formulários adaptáveis fornecem um conjunto de APIs que você pode usar para se comunicar e executar ações em formulários adaptáveis. Algumas das principais APIs são as seguintes. Para obter mais informações, consulte Referência da API da biblioteca [JavaScript para Forms](https://adobe.com/go/learn_aemforms_documentation_63)adaptável.

   * `guideBridge.reset()`: Redefine um formulário.
   * `guideBridge.submit()`: Envia um formulário.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Define o foco para um campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: Valida um formulário.
   * `guideBridge.getDataXML(options)`: Obtém dados de formulário como XML.
   * `guideBridge.resolveNode(somExpression)`: Obtém um objeto de formulário.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Define a propriedade de um objeto de formulário.
   * Além disso, você pode usar as seguintes propriedades de campo:

      * `field.value` para alterar o valor de um campo.
      * f `ield.enabled` para ativar/desativar um campo.
      * `field.visible` para alterar a visibilidade de um campo.

* Os autores de formulários adaptativos podem precisar gravar código JavaScript para criar lógica comercial em um formulário. Embora o JavaScript seja poderoso e eficaz, é provável que possa comprometer as expectativas de segurança. Portanto, é necessário garantir que o autor do formulário seja uma pessoa confiável e que haja processos para revisar e aprovar o código JavaScript antes que um formulário seja colocado em produção. O administrador pode restringir o acesso do editor de regras aos grupos de usuários com base em sua função ou função. Consulte [Conceder acesso ao editor de regras para grupos](/help/forms/using/rule-editor-access-user-groups.md)de usuários selecionados.
* É possível usar o expressão em regras para tornar os formulários adaptáveis dinâmicos. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de certos tipos. Para obter mais informações sobre expressões e práticas recomendadas, consulte expressões de formulário [adaptáveis](/help/forms/using/adaptive-form-expressions.md).

### Trabalhar com temas {#working-with-themes}

Adaptável para temas permite criar estilos reutilizáveis que podem ser aplicados em formulários para proporcionar aparência e estilo consistentes. É recomendável usar Temas para definir estilos para componentes de formulário e painéis. Algumas práticas recomendadas para temas são as seguintes:

* Use a biblioteca de ativos para rápida aplicação de estilos de texto, plano de fundo e imagens. Quando um estilo é adicionado na biblioteca de ativos, ele fica disponível para outros temas e no modo de estilo do editor de formulários.
* Aplique configurações globais como fonte e plano de fundo da página usando o seletor de nível de página.
* Use bibliotecas de clientes para importar estilos existentes ou avançados para seus temas.
* É possível substituir o estilo de campos, painéis ou botões específicos em uma camada de estilo de formulário.
* Se um tema não atender ao seu requisito de estilo, você poderá usar classes predefinidas, como guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode, para aplicar um estilo comum aos formulários.

For more information, see [Themes](/help/forms/using/themes.md).

### Otimização do desempenho de formulários grandes e complexos {#optimizing-performance-of-large-and-complex-forms}

Os autores de formulários e usuários finais normalmente enfrentam problemas de desempenho ao carregar formulários grandes no modo de criação ou em tempo de execução. À medida que o número de objetos (campos e painéis) no formulário aumenta, a criação e o tempo de execução experimentam start degradantes. Também impede que vários autores colaborem e criem um formulário simultaneamente.

Considere as seguintes práticas recomendadas para solucionar problemas de desempenho com formulários grandes:

* É recomendável criar formulários adaptáveis usando o modelo de dados de formulário XSD mesmo ao converter um XFA em um formulário adaptável, se possível.
* Inclua apenas os campos e painéis em formulários adaptáveis que capturam informações do usuário. Considere manter o conteúdo estático mínimo ou use URLs para abri-los em uma janela separada.
* Embora cada formulário seja projetado para uma finalidade específica, há alguns segmentos comuns na maioria dos formulários. Por exemplo, detalhes pessoais, endereço, detalhes de emprego e assim por diante. Crie fragmentos [de formulário](/help/forms/using/adaptive-form-fragments.md) adaptáveis para elementos e seções de formulário comuns e use-os em formulários. Também é possível salvar um painel em um formulário existente como um fragmento. Qualquer alteração em um fragmento é refletida em todos os formulários adaptativos associados. Ela promove a criação colaborativa, já que vários autores podem trabalhar simultaneamente em diferentes fragmentos que compõem um formulário.

   * Semelhante aos formulários adaptáveis, recomenda-se que todos os estilos específicos do fragmento e scripts personalizados sejam definidos na biblioteca do cliente usando a caixa de diálogo do container do fragmento. Além disso, tente criar fragmentos autossuficientes que não dependem de objetos fora dele.
   * Evite usar scripts entre fragmentos. Se houver algum objeto fora do fragmento ao qual você deve se referir, tente tornar esse objeto parte do formulário pai. Se o objeto ainda precisar residir em outro fragmento, consulte-o pelo seu nome no script.

* Use Salvar e Retomar com o salvamento automático para salvar o formulário adaptável periodicamente e permitir que os usuários revisitem mais tarde para preencher o formulário.
* Configure os fragmentos para carregá-los de maneira fácil. No tempo de execução, o fragmento marcado para carregar com folga é renderizado somente quando necessário. Reduz significativamente o tempo de carga para formulários grandes. Também é compatível com fragmentos com painéis repetíveis. Para obter mais informações, consulte [Configurar carregamento](/help/forms/using/lazy-loading-adaptive-forms.md)lento.

   * Não configure o carregamento lento em fragmentos em um layout de grade responsivo ou no primeiro painel.
   * Os componentes de anexo de arquivo e Termos e condições não são suportados em fragmentos carregados de forma preguiçosa.
   * Marque um valor em um painel carregado com preguiça como Usar valor globalmente se esse valor for usado em alguma outra parte do formulário para que o valor esteja disponível para uso quando o painel contentor for descarregado.
   * Considere gravar regras de visibilidade para fragmentos que devem ser exibidos ou ocultados com base em uma condição.

### Preenchimento de formulários adaptáveis {#prefilling-adaptive-forms}

É possível pré-preencher campos de formulário adaptáveis com dados obtidos do backend para ajudar os usuários a preencher rapidamente o formulário e evitar erros de digitação.

* A AEM Forms fornece um serviço de preenchimento prévio para ler dados de um arquivo XML de dados predefinido e preencher previamente os campos de um formulário adaptável com o conteúdo no arquivo XML de preenchimento prévio.
* O XML de dados de preenchimento prévio deve ser compatível com o schema do modelo de formulário associado ao formulário adaptável.
* Inclua `afBoundedData` e `afUnBoundedData` seções no XML de preenchimento prévio para preencher previamente os campos vinculados e não vinculados em um formulário adaptável.

* Para formulários adaptáveis baseados no modelo de dados de formulário, a AEM Forms fornece serviço de preenchimento prévio do modelo de dados de formulário pronto para uso. O serviço de preenchimento prévio query fontes de dados para objetos de modelo de dados no formulário adaptável e preenche previamente os valores de campo ao renderizar o formulário.
* Você também pode usar os protocolos de arquivo, crx, service ou http para preencher formulários adaptáveis.
* A AEM Forms oferece suporte a serviços de preenchimento prévio personalizados que podem ser conectados como um serviço OSGi para preencher previamente formulários adaptáveis.

Para obter mais informações, consulte [Preencher campos](/help/forms/using/prepopulate-adaptive-form-fields.md)de formulário adaptável.

### Assinar e enviar formulários adaptativos {#signing-and-submitting-adaptive-forms}

Formulários adaptáveis exigem ações de envio para processar dados especificados pelo usuário. Uma ação Enviar determina a tarefa executada nos dados que você envia usando um formulário adaptável.

* Há várias ações de envio disponíveis prontamente em formulários adaptáveis. Para obter detalhes, consulte [Configuração da ação](/help/forms/using/configuring-submit-actions.md)Enviar.
* Você pode gravar uma ação de envio personalizada se as ações de envio padrão não preencherem seu caso de uso. Para obter mais informações, consulte Ação de [gravação de envio personalizado para formulários](/help/forms/using/custom-submit-action-form.md)adaptáveis.
* Inclua validações do lado do servidor para impedir o envio de dados inválidos.

Você pode aproveitar a experiência de vários sinais do Adobe Sign em formulários adaptáveis. Considere o seguinte ao configurar o Adobe Sign em formulários adaptáveis. Para obter detalhes, consulte [Uso do Adobe Sign em um formulário](/help/forms/using/working-with-adobe-sign.md)adaptável.

* O formulário adaptativo habilitado para Adobe Sign é enviado somente depois que todos os signatários assinarem o formulário. A Forms é exibida no estado Sinal pendente até que o formulário seja assinado por todos os signatários.
* Você pode configurar a experiência de assinatura no formulário ou redirecionar os signatários para uma página de assinatura no envio.
* Configure a experiência de assinatura sequencial ou paralela, conforme apropriado.

### Gerando documento de registro {#generating-document-of-record}

Um documento de registro (DoR) é uma versão em PDF achatada de um formulário adaptável que pode ser impresso, assinado ou arquivado.

* Dependendo do modelo de dados de formulário no qual um formulário adaptável é baseado, é possível configurar um modelo para DoR da seguinte maneira:

   * **Modelo** de formulário XFA: Use o arquivo XDP associado como modelo DoR.
   * **Schema** XSD: Use o modelo XFA associado que usa o mesmo schema XML usado pelo formulário adaptável.
   * **Nenhum**: Usar DoR gerado automaticamente.

* Configure o cabeçalho, o rodapé, as imagens, a cor, a fonte e assim por diante, diretamente da guia Documento de registro do editor de formulário adaptável.
* Use `DoRService` para gerar o DoR de forma programática.
* Excluir campos ocultos do DoR.
* Use o parâmetro `afAcceptLang` request para visualização DoR em outra localidade.

### Depuração e teste de formulários adaptáveis {#debugging-and-testing-adaptive-forms}

[AEM plug-in](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) do Chrome é uma extensão de navegador para o Google Chrome que fornece ferramentas para depurar formulários adaptáveis. Os autores e desenvolvedores de formulários podem usar essas ferramentas para:

* Identificar gargalos e otimizar o desempenho da renderização do formulário
* Depurar palavras-chave e erros bindRef no formulário
* Ativar e configurar registros
* Regras e scripts de depuração no formulário
* Explore e saiba mais sobre as APIs do guideBridge

Para obter mais informações, consulte Plug-in [AEM Chrome - Formulário](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)adaptável.

O Calvin SDK é uma API de utilitário para desenvolvedores do Adaptive Forms para testar o Adaptive Forms. O Calvin SDK foi criado sobre a estrutura [de teste do](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)Hobbes.js. Você pode usar a estrutura para testar o seguinte:

* Experiência de execução de um formulário adaptável
* Experiência de preenchimento prévio de um formulário adaptável
* Enviar experiência de um formulário adaptável
* Regras de expressão
* Validações
* Carregamento lento

Para obter mais informações, consulte [Automatizar o teste de formulários](/help/forms/using/calvin.md)adaptáveis.

### Validação de formulários adaptativos no servidor AEM {#validating-adaptive-forms-on-aem-server}

As validações do lado do servidor são necessárias para impedir tentativas de ignorar validações no cliente e qualquer possível comprometimento de envios de dados e violações de regras comerciais. As validações do lado do servidor são executadas no servidor carregando a biblioteca do cliente necessária.

* Inclua funções em uma biblioteca de cliente para validar expressões em formulários adaptáveis e especifique a biblioteca de cliente na caixa de diálogo container de formulários adaptáveis. Para obter mais informações, consulte Revalidação [](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)no servidor.
* A validação do servidor valida o modelo de formulário. É recomendável criar uma biblioteca de cliente separada para validações e não misturá-la com outros itens como estilo HTML e manipulação DOM na mesma biblioteca de cliente.

### Localização de formulários adaptáveis {#localizing-adaptive-forms}

AEM fornece workflows de tradução que podem ser usados para localizar formulários adaptáveis. Para obter informações, consulte [Usar AEM fluxo de trabalho de tradução para localizar formulários](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)adaptáveis.

Algumas práticas recomendadas ao localizar formulários adaptativos são as seguintes:

* Use fragmentos de formulário adaptáveis para elementos comuns nos formulários e localize fragmentos. Ela garante que você localize um fragmento uma vez e ele se reflita em todos os formulários nos quais o fragmento localizado é usado.
* Quaisquer modificações, como adicionar um novo componente ou aplicar um script em um formulário localizado, não são localizadas automaticamente. Portanto, é necessário finalizar um formulário antes de localizá-lo para evitar vários ciclos de localização.
* Use o parâmetro `afAcceptLang` request para substituir a localidade do navegador e renderizar o formulário na localidade especificada. Por exemplo, o URL a seguir forçará a renderização do formulário na localidade japonesa, independentemente da localidade especificada na configuração do navegador:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Atualmente, a AEM Forms suporta localização de conteúdo de formulários adaptáveis em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). No entanto, você pode adicionar suporte para novas localidades para formulários adaptáveis em tempo de execução. Para obter mais informações, consulte [Suporte a novas localidades para localização](/help/forms/using/supporting-new-language-localization.md)de formulários adaptáveis.

## Preparar projeto de formulários para produção {#prepare-forms-project-for-production}

### Adicionar servidor de processamento de formulários {#adding-forms-processing-server}

Você pode configurar uma instância adicional do servidor AEM Forms que reside atrás do firewall em uma zona protegida. Você pode usar esta instância para:

* **Processamento** em lote: trabalhos que são recorrentes ou programados em lotes com carga pesada. Por exemplo, imprimir declarações, gerar correspondências e usar serviços de documento como Gerador de PDF, Saída e Montador.
* **Armazenamento de dados** PII: Salve os dados PII no servidor de processamento. Não é necessário se você já estiver usando o provedor de armazenamentos personalizado para armazenar dados de PII.

### Mover projeto para outro ambiente {#moving-project-to-another-environment}

Você precisa, com frequência, mover seus projetos AEM de um ambiente para outro. Algumas das coisas principais a serem lembradas ao se mover são as seguintes:

* Faça backup das bibliotecas de clientes, código personalizado e configurações existentes.
* Implante pacotes de produtos e patches manualmente e na ordem especificada no novo ambiente.
* Implante pacotes de código específicos do projeto manualmente e como um pacote ou pacote separado no novo servidor AEM.
* (Somente ** AEM Forms em JEE) Implante LCAs e DSCs manualmente no servidor Forms Workflow.
* Use a funcionalidade [Exportar-Importar](/help/forms/using/import-export-forms-templates.md) para mover ativos para o novo ambiente. Você também pode configurar o agente de replicação e publicar os ativos.
* Ao atualizar, substitua todas as APIs e recursos obsoletos por novas APIs e recursos.

### Configuração de AEM {#configuring-aem}

Algumas práticas recomendadas para configurar AEM para melhorar o desempenho geral são as seguintes:

* Ative a compactação da biblioteca do cliente HTML para JavaScript e CSS do console do Felix. Consulte [Clientlibs explicados por exemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/).
* Armazene em cache todas as bibliotecas de clientes no `/etc.clientlibs/fd` e quaisquer bibliotecas personalizadas adicionais no AEM dispatcher para aumentar a capacidade de resposta e a segurança dos formulários publicados. For more information, see [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Não armazene em cache `/content/forms/af/` e `/content/dam/formsanddocuments/*` caminhos. para obter informações detalhadas sobre como configurar o cache de formulários adaptáveis, consulte [Armazenamento em cache de formulários](/help/forms/using/configure-adaptive-forms-cache.md)adaptáveis.

* Habilitar HTML por meio do módulo de compactação do servidor da Web. Para obter mais informações, consulte Ajuste [de desempenho do servidor](/help/forms/using/performance-tuning-aem-forms.md)AEM Forms.
* Aumente a configuração de chamadas por solicitação para formulários grandes. Consulte [Otimizar o desempenho de formulários](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)grandes e complexos.
* Crie páginas de erro [personalizadas exibidas pelo manipulador](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html)de erros.
* Servidor AEM Forms seguro.

   * Use o modo de `nosamplecontent` execução para garantir que não haja nenhum conteúdo de amostra e usuários de amostra implantados no servidor de produção. Consulte [Executando AEM no modo](/help/sites-administering/production-ready.md)Pronto para Produção.

* Mantenha o tamanho do heap com no mínimo 8 GB. Para outras configurações, consulte Ajuste [de desempenho do servidor](/help/forms/using/performance-tuning-aem-forms.md)AEM Forms.
* Use sessões de usuário de serviço em vez de sessões administrativas para executar tarefas de nível de serviço. Para obter mais informações, consulte Autenticação [](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)de serviço.

>[!VIDEO](https://vimeo.com/)

### Configurar armazenamento externo para rascunhos e dados de formulários enviados {#external-storage}

Em um ambiente de produção, é recomendável não armazenar dados de formulário enviados AEM repositório. A implementação padrão das ações de envio para Forms Portal Store, Store Content e Store PDF armazena dados de formulário AEM repositório. Estas ações apresentadas destinam-se apenas a fins de demonstração. Além disso, os recursos Salvar e Retomar e Salvar automaticamente usam o armazenamento do portal por padrão. Portanto, considere as seguintes recomendações:

* **Armazenamento de dados** de rascunho: Se você estiver usando o recurso Rascunho de formulários adaptáveis, deverá implementar uma SPI (Service Provider Interface) personalizada para armazenar dados de rascunho em um banco de dados como um armazenamento mais seguro. Para obter mais informações, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

* **Armazenamento de dados** de envio: Se você estiver usando o repositório de envio do portal de formulários, deverá implementar um SPI personalizado para armazenar dados de envio em um banco de dados. Consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md) para obter uma amostra da integração.

   Você também pode gravar uma ação de envio personalizada que armazena dados e anexos de formulário em um armazenamento seguro. Consulte [Gravação de ação de envio personalizado para formulários](/help/forms/using/custom-submit-action-form.md) adaptáveis para obter mais informações.

* **Extensão da ID** de rascunho: Ao salvar um formulário adaptável como rascunho, uma ID de rascunho é gerada para identificar exclusivamente o rascunho. O valor mínimo para o comprimento do campo de ID de rascunho é de 26 caracteres. O Adobe recomenda definir o comprimento da ID de rascunho para 26 ou mais caracteres.

### Tratamento de informações de identificação pessoal {#handling-personally-identifiable-information}

Um dos principais desafios para as organizações é como lidar com dados de identificação pessoal (PII). Algumas práticas recomendadas que ajudarão você a lidar com esses dados são as seguintes:

* Use um banco de dados seguro e externo como armazenamento para armazenar dados de formulários rascunhos e enviados. Consulte [Configurar armazenamento externo para rascunhos e dados](/help/forms/using/adaptive-forms-best-practices.md#external-storage)de formulários enviados.
* Use o componente de formulário Termos e condições para obter o consentimento explícito do usuário antes de habilitar o salvamento automático. Nesse caso, ative o salvamento automático somente quando o usuário concordar com as condições no componente Termos e condições.

