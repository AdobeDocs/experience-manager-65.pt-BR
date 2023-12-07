---
title: Medir e melhorar a eficácia e a conversão de formulários
description: O AEM Forms integra-se às soluções da Adobe Target e da Adobe Analytics, o que permite medir e melhorar o desempenho e o índice de conversão de seus formulários.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Medir e melhorar a eficácia e a conversão de formulários{#measure-and-improve-effectiveness-and-conversion-of-forms}

## O desafio {#the-challenge-br}

As organizações estão cada vez mais capacitando e incentivando seus clientes a fazer transações usando autoserviços digitais em vários canais. No entanto, na ausência de um mecanismo de feedback individual, torna-se desafiador medir o sucesso e experimentar formulários digitais para melhorar a experiência do cliente e aumentar as conversões.

Para maximizar o ROI, as organizações devem monitorar como seus clientes interagem com os serviços e experimentar com seus artefatos digitais (formulários) para aprimorar as experiências do cliente. Para medir o sucesso e definir uma estratégia de aprimoramento, as organizações precisam de respostas para perguntas como:

* Quantos clientes tentaram acessar ou transacionar com meus formulários?
* Quantas delas concluíram com êxito a transação?
* Quantos abandonaram o formulário?
* Quais são as áreas problemáticas em que os clientes estão enfrentando problemas?
* Quais alterações eu trago e como testo o que causa uma conversão melhor?

## A solução {#the-solution}

O AEM Forms integra-se com [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluções - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - que podem ajudá-lo a monitorar e analisar o desempenho de seus formulários e permitir que você experimente e identifique a experiência que leva a um melhor índice de conversão.

## O fluxo de trabalho {#the-workflow}

Vamos analisar os detalhes de como você pode medir o desempenho e melhorar as taxas de conversão de formulários.

### Público alvo {#target-audience}

* Usuários empresariais e analistas responsáveis por estratégias de marketing e sucesso
* Equipe de TI que cuida da infraestrutura e da configuração e manutenção de soluções

### Componentes e recursos do AEM Forms envolvidos {#aem-forms-components-and-features-involved}

* Formulários adaptáveis
* Integração com o Adobe Analytics para coletar, organizar e relatar interações do cliente com seus formulários adaptáveis
* Integração com o Adobe Target para executar testes A/B para formulários adaptáveis

### Suposições {#assumptions}

* Você já tem uma conta do Adobe Marketing Cloud e está registrado para as soluções do Analytics e do Target.
* Você tem um formulário adaptável publicado que os clientes podem acessar.

### Etapas do fluxo de trabalho {#workflow-steps}

#### Etapa 1: configurar o Analytics e o Target no AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar o Analytics**

Para obter insights profundos sobre as interações do cliente com seus formulários, primeiro é necessário configurar o Analytics no AEM Forms. Execute as seguintes etapas:

1. Criar um conjunto de relatórios no Adobe Analytics
1. Criar configuração do serviço em nuvem no AEM
1. Criar estrutura de serviço em nuvem no AEM
1. Configurar o serviço de configuração do AEM Forms Analytics no AEM
1. Habilitar análise no formulário no AEM

Para obter etapas detalhadas, consulte [Configuração de análises e relatórios para formulários adaptáveis](../../forms/using/configure-analytics-forms-documents.md).

**Configurar o Target**

Para criar e executar testes A/B para seus formulários adaptáveis, configure o Target no AEM Forms conforme descrito em [Configurar e integrar o Target no AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Etapa 2: Exibir relatório de análise {#step-view-analytics-report-br}

À medida que os clientes acessam e interagem com formulários nos quais você ativou o Analytics, suas interações são capturadas em bancos de dados do Analytics altamente seguros. Os bancos de dados são segmentados por clientes e acessíveis por meio de conexões seguras.

Você pode visualizar um relatório do AEM para formulários habilitados para análise e analisar dados. Para exibir o relatório:

1. No servidor AEM, navegue até **Forms > Forms e documentos**.
1. Selecione o formulário para o qual deseja criar o relatório de análise.
1. Clique no ícone Relatórios do Analytics. O relatório é exibido.

Vamos analisar os pontos de dados que o Analytics coleta e relata para formulários.

**relatório de análise do Forms**

O relatório de análise para formulários adaptáveis captura os seguintes Indicadores principais de desempenho (KPIs) no nível do formulário:

* **Tempo médio de preenchimento**: Tempo médio gasto no preenchimento do formulário
* **Impressões**: Número de vezes que o formulário apareceu nos resultados da pesquisa

* **Representações**: Número de vezes que o formulário foi renderizado ou aberto
* **Rascunhos**: Número de vezes que o formulário foi salvo como rascunho

* **Envios**: Número de vezes que o formulário foi enviado
* **Anular**: Número de vezes que os usuários saíram sem preencher o formulário
* **Visitas/envios**: Taxa de visitas por envio

Além disso, você obtém os seguintes detalhes sobre cada painel no formulário:

* **Hora**: Tempo médio gasto (segundos) no painel e seus campos

* **Erro**: Número de erros encontrados no painel e seus campos por 1000 representações de formulário

* **Ajuda**: Número de vezes que os usuários acessaram a ajuda em contexto para o painel e seus campos por 1000 representações de formulário

![Um exemplo de relatório de análise para um formulário adaptável](assets/summary-report.png)

Para obter mais detalhes sobre os relatórios do Forms Analytics, consulte [Visualização e compreensão de relatórios do AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Você pode visualizar relatórios detalhados e obter insights mais profundos sobre os clientes e as interações deles com os formulários da sua conta do Analytics no Adobe Marketing Cloud.

#### Etapa 3: Analisar pontos de dados {#step-analyze-data-points}

Nesta etapa, você analisará pontos de dados no relatório do Analytics e inferirá o desempenho do formulário. Se não atender aos KPIs de sucesso, você construirá hipóteses, com base em dados, e encontrará possíveis soluções para corrigir os problemas. Por exemplo:

* Se o tempo médio de preenchimento do formulário for maior do que a sua expectativa, é possível que o formulário seja complexo para os clientes compreenderem, que o formulário não use terminologias padrão, que o formulário seja muito longo e assim por diante. Nesse caso, talvez você queira simplificar a estrutura e os campos do formulário, reprocessar o design do formulário, reduzir o comprimento do formulário ou adicionar descrições de ajuda e exemplos para campos de formulário não padrão.
* Se os dados indicarem que a maioria dos clientes está acessando a ajuda de um painel de formulário, é evidente que os clientes estão intrigados com quais informações preencher. Você pode usar terminologia alternativa ou adicionar algumas entradas de exemplo e descrição de ajuda para esse painel.
* Se a taxa de anulação ou abandono de um formulário for maior do que o esperado, talvez o formulário demore muito para ser renderizado, os clientes estejam entrando inadvertidamente no formulário ou ele seja muito complicado. Nesse caso, talvez você queira otimizar a descrição do formulário exibida nos resultados da pesquisa, simplificar o formulário, otimizá-lo para carregamento mais rápido e assim por diante.

Depois de analisar esses pontos de dados e chegar a uma hipótese, faça as alterações necessárias no formulário.

#### Etapa 4: validar a análise e as correções {#step-validate-your-analysis-and-fixes}

Nesta etapa, você validará as alterações feitas no formulário e verificará se elas afetam a taxa de conversão.

**Executar um teste A/B**

A integração do AEM Forms com o Target permite criar testes A/B para formulários adaptáveis. Nos testes A/B, você apresenta aleatoriamente diferentes experiências de um formulário aos seus clientes em tempo real para saber qual experiência funciona melhor ou causa mais conversões. Depois de ter dados significativos indicando que uma experiência oferece uma conversão melhor do que a outra, você pode declarar essas experiências como vencedoras e, a partir de agora, ela se tornará a experiência padrão visível para todos os clientes.

Para obter mais informações sobre como criar um teste A/B para um formulário adaptável, consulte [Teste A/B de formulários adaptáveis](../../forms/using/ab-testing-adaptive-forms.md).

![Um relatório de resumo de amostra do teste A/B para um formulário adaptável](assets/ab-test-report-4.png)

## Práticas recomendadas {#best-practices}

As práticas recomendadas reais são aquelas que você identifica a si mesmo ao executar esse fluxo de trabalho. Eles são exclusivos para seu ambiente e requisitos. Capture seus aprendizados por meio do fluxo de trabalho e documente-os como práticas recomendadas.

Algumas recomendações sobre como criar formulários e executar testes A/B são as seguintes:

**Design do Forms**

* Mantenha o formulário simples, curto e fácil de navegar. Use dicas direcionais para navegação.
* Use terminologias padrão ou comuns para campos de formulário.
* Explique o campo e a entrada necessária, com exemplos ou ajuda, em que os usuários podem ficar confusos.
* Valide as entradas do usuário à medida que elas são digitadas, sempre que possível, para evitar erros no envio do formulário.
* Otimizar layouts para dispositivos móveis e de desktop.
* Preencher automaticamente as informações para usuários conhecidos.

**Testes A/B**

* Construa uma hipótese e identifique métricas de sucesso antes de executar o teste A/B.
* Faça variações mínimas (idealmente uma de cada vez) em sua experiência alternativa para saber o que afetou o índice de conversão.
* Teste frequentemente para eliminar ineficiências.
