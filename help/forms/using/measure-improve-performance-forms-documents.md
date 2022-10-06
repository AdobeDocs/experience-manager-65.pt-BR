---
title: Medir e melhorar a eficácia e a conversão de formulários
seo-title: Measure and improve effectiveness and conversion of forms
description: O AEM Forms integra-se com as soluções Adobe Target e Adobe Analytics, que permitem medir e melhorar o desempenho e a taxa de conversão de seus formulários.
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that allows you to measure and improve the performance and conversion rate of your forms.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Medir e melhorar a eficácia e a conversão de formulários{#measure-and-improve-effectiveness-and-conversion-of-forms}

## O desafio {#the-challenge-br}

As organizações estão cada vez mais capacitando e incentivando seus clientes a transacionarem usando autoserviços digitais em vários canais. No entanto, na ausência de um mecanismo de feedback um para um, torna-se desafiador medir o sucesso e experimentar formulários digitais para aprimorar a experiência do cliente e aumentar as conversões.

Para maximizar o ROI, as organizações devem monitorar como seus clientes interagem com os serviços e experimentar com seus artefatos digitais (formulários) para aprimorar as experiências do cliente. Para medir o sucesso e definir uma estratégia para melhorar, as organizações precisam de respostas para perguntas como:

* Quantos clientes tentaram acessar ou transacionar com meus formulários?
* Quantos deles concluíram com êxito a transação?
* Quantos deles abandonaram o formulário?
* Quais são as áreas problemáticas onde os clientes estão enfrentando problemas?
* Quais mudanças eu trago e como faço para testar o que causa uma conversão melhor?

## A solução {#the-solution}

O AEM Forms integra-se ao [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluções - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - que pode ajudá-lo a monitorar e analisar o desempenho de seus formulários e permitir que você experimente e identifique a experiência que leva a uma melhor taxa de conversão.

## O fluxo de trabalho {#the-workflow}

Vamos detalhar como você pode medir o desempenho e melhorar as taxas de conversão para formulários.

### Público-alvo {#target-audience}

* Usuários e analistas empresariais responsáveis por estratégias e sucesso de marketing
* Pessoal de TI responsável pela instalação e manutenção de infraestrutura e soluções

### Componentes e recursos do AEM Forms envolvidos {#aem-forms-components-and-features-involved}

* Formulários adaptáveis
* Integração com o Adobe Analytics para coletar, organizar e relatar interações do cliente com seus formulários adaptáveis
* Integração com o Adobe Target para executar testes A/B para formulários adaptáveis

### Pressupostos {#assumptions}

* Você já tem uma conta Adobe Marketing Cloud e está registrado para as soluções Analytics e Target.
* Você tem um formulário adaptável publicado que pode ser acessado pelos clientes.

### Etapas do fluxo de trabalho {#workflow-steps}

#### Etapa 1: Configurar o Analytics e o Target no AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar Analytics**

Para obter mais informações sobre as interações do cliente com os formulários, primeiro é necessário configurar o Analytics no AEM Forms. Execute as seguintes etapas:

1. Criar um conjunto de relatórios no Adobe Analytics
1. Criar configuração do serviço em nuvem no AEM
1. Criar estrutura do serviço em nuvem no AEM
1. Configurar o serviço de configuração do AEM Forms Analytics no AEM
1. Habilite o analytics no formulário no AEM

Para obter etapas detalhadas, consulte [Configuração de análises e relatórios para formulários adaptáveis](../../forms/using/configure-analytics-forms-documents.md).

**Configurar o Target**

Para criar e executar testes A/B para seus formulários adaptáveis, configure o Target no AEM Forms, conforme descrito em [Configurar e integrar o Target no AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Etapa 2: Exibir relatório de análise {#step-view-analytics-report-br}

À medida que seus clientes acessam e interagem com formulários nos quais o Analytics foi ativado, suas interações são capturadas em bancos de dados altamente seguros do Analytics. Os bancos de dados são segmentados pelos clientes e acessíveis por meio de conexões seguras.

Você pode visualizar um relatório de dentro do AEM para formulários habilitados para análise e analisar dados. Para exibir o relatório:

1. No servidor AEM, navegue até **Forms > Forms e documentos**.
1. Selecione o formulário para o qual deseja criar o relatório de análise.
1. Clique no ícone Relatórios do Analytics . O relatório é exibido.

Vamos analisar os pontos de dados que o Analytics coleta e cria relatórios para formulários.

**Relatório de análise do Forms**

O relatório de análise para formulários adaptáveis captura os seguintes KPIs (Indicadores-chave de desempenho) em nível de formulário:

* **Tempo médio de preenchimento**: Tempo médio gasto no preenchimento do formulário
* **Impressões**: Número de vezes que o formulário foi exibido nos resultados da pesquisa

* **Representações**: Número de vezes que o formulário foi renderizado ou aberto
* **Rascunhos**: Número de vezes que o formulário foi salvo como rascunho

* **Submissões**: Número de vezes que o formulário foi enviado
* **Abortar**: Número de vezes que os usuários ficaram sem preencher o formulário
* **Visitas/envios**: Taxa de visitas por envio

Além disso, você obtém os seguintes detalhes sobre cada painel no formulário:

* **Hora**: Tempo médio gasto (segundos) no painel e seus campos

* **Erro**: Número de erros encontrados no painel e em seus campos por 1000 execuções de formulário

* **Ajuda**: Número de vezes que os usuários acessaram a ajuda no contexto do painel e seus campos por 1000 execuções de formulário

![Um exemplo de relatório de análise para um formulário adaptável](assets/summary-report.png)

Para obter mais detalhes sobre relatórios de análise de formulários, consulte [Visualização e compreensão dos relatórios de análise do AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Você pode visualizar relatórios detalhados e obter informações mais detalhadas sobre seus clientes e suas interações com formulários da sua conta do Analytics no Adobe Marketing Cloud.

#### Etapa 3: Analisar pontos de dados {#step-analyze-data-points}

Nesta etapa, você analisará os pontos de dados no relatório de análise e descobrirá o desempenho do formulário. Se ele não atender seus KPIs de sucesso, você construirá hipóteses, com base em dados, e encontrará soluções possíveis para corrigir os problemas. Por exemplo:

* Se o tempo médio de preenchimento do formulário for maior do que a expectativa, é possível que o formulário seja complexo para os clientes compreenderem, o formulário não usa terminologias padrão, o formulário é muito longo e assim por diante. Nesse caso, convém simplificar a estrutura e os campos do formulário, retrabalhar o design do formulário, encurtar o comprimento do formulário ou adicionar descrições de ajuda e exemplos para campos de formulário não padrão.
* Se os dados indicarem que a maioria dos clientes está acessando a ajuda de um painel de formulário, é evidente que os clientes estão intrigados com relação a quais informações preencher. Você pode usar terminologia alternativa ou adicionar alguns exemplos de entradas e descrição de ajuda para esse painel.
* Se a taxa de aborto ou abandono de um formulário for maior do que o esperado, pode ser que o formulário esteja demorando muito para ser renderizado, que os clientes inadvertidamente acessem o formulário ou que seja muito complicado. Nesse caso, talvez você queira otimizar a descrição do formulário exibida nos resultados da pesquisa, simplificar o formulário, otimizar o formulário para um carregamento mais rápido e assim por diante.

Depois de analisar esses pontos de dados e chegar a uma hipótese, faça as alterações necessárias no formulário.

#### Etapa 4: Validar sua análise e correções {#step-validate-your-analysis-and-fixes}

Nesta etapa, você validará as alterações feitas no formulário e verificará se isso afeta a taxa de conversão.

**Executar um teste A/B**

A integração do AEM Forms com o Target permite criar testes A/B para formulários adaptáveis. Em testes A/B, você apresenta aleatoriamente diferentes experiências de um formulário para seus clientes em tempo real para saber qual experiência funciona melhor ou causa mais conversões. Quando você tiver dados significativos indicando uma experiência fornecendo uma conversão melhor que a outra, você pode declarar essas experiências como vencedoras e, a partir de agora, ela se tornará a experiência padrão visível para todos os clientes.

Para obter mais informações sobre como criar um teste A/B para um formulário adaptável, consulte [Teste A/B de formulários adaptáveis](../../forms/using/ab-testing-adaptive-forms.md).

![Um exemplo de relatório de resumo do teste A/B para um formulário adaptável](assets/ab-test-report-4.png)

## Práticas recomendadas {#best-practices}

As práticas recomendadas reais são aquelas que você mesmo identifica ao executar esse fluxo de trabalho. Elas são exclusivas do seu ambiente e requisitos. Capture seus aprendizados por meio do fluxo de trabalho e documente-os como práticas recomendadas.

Algumas recomendações sobre como criar formulários e executar testes A/B são as seguintes:

**Design do Forms**

* Mantenha o formulário simples, curto e fácil de navegar. Use dicas direcionais para navegação.
* Use terminologias padrão ou comum para campos de formulário.
* Explique o campo e a entrada necessária, com exemplos ou ajuda, onde os usuários podem ficar confusos.
* Valide as entradas de usuário, pois elas as digitam, sempre que possível, para evitar erros no envio do formulário.
* Otimizar layouts para desktop e dispositivos móveis.
* Preencher automaticamente informações para usuários conhecidos.

**Testes A/B**

* Crie uma hipótese e identifique métricas de sucesso antes de executar o teste A/B.
* Faça variações mínimas (idealmente uma de cada vez) na experiência alternativa para saber o que afetou a taxa de conversão.
* Teste com frequência para eliminar ineficiências.
