---
title: Medir e melhorar a eficácia e a conversão dos formulários
seo-title: Medir e melhorar a eficácia e a conversão dos formulários
description: A AEM Forms integra-se às soluções Adobe Target e Adobe Analytics que permitem medir e melhorar o desempenho e a taxa de conversão de seus formulários.
seo-description: A AEM Forms integra-se às soluções Adobe Target e Adobe Analytics que permitem medir e melhorar o desempenho e a taxa de conversão de seus formulários.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
translation-type: tm+mt
source-git-commit: befbdfd574949a7f7449b70a15480e7c105418fe
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---


# Meça e melhore a eficácia e a conversão de formulários{#measure-and-improve-effectiveness-and-conversion-of-forms}

## O desafio {#the-challenge-br}

As organizações estão cada vez mais capacitando e incentivando seus clientes a transacionar usando autoserviços digitais em vários canais. No entanto, na ausência de um mecanismo de feedback individual, torna-se desafiador medir o sucesso e experimentar com formulários digitais para melhorar a experiência do cliente e aumentar as conversões.

Para maximizar o ROI, as organizações devem monitorar como seus clientes interagem com os serviços e experimentar seus artefatos digitais (formulários) para aprimorar as experiências dos clientes. Para medir o sucesso e definir uma estratégia de aprimoramento, as organizações precisam de respostas para perguntas como:

* Quantos clientes tentaram acessar ou transacionar com meus formulários?
* Quantos deles concluíram com êxito a transação?
* Quantos deles abandonaram o formulário?
* Quais são as áreas problemáticas nas quais os clientes enfrentam problemas?
* Que mudanças eu trago e como faço para testar o que causa melhor conversão?

## A solução {#the-solution}

A AEM Forms integra-se com [soluções Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - que podem ajudá-lo a monitorar e analisar o desempenho de seus formulários e permitir que você experimente e identifique a experiência que leva a uma melhor taxa de conversão.

## O fluxo de trabalho {#the-workflow}

Vamos detalhar como você pode medir o desempenho e melhorar as taxas de conversão para formulários.

### Audiência do público alvo {#target-audience}

* Usuários e analistas de negócios responsáveis por estratégias e sucesso de marketing
* Pessoal de TI que cuida da infraestrutura e da configuração e manutenção das soluções

### Os componentes e recursos do AEM Forms envolvidos {#aem-forms-components-and-features-involved}

* Formulários adaptáveis
* Integração com a Adobe Analytics para coletar, organizar e relatar interações do cliente com seus formulários adaptáveis
* Integração com a Adobe Target para executar testes A/B para formulários adaptáveis

### Pressupostos {#assumptions}

* Você já tem uma conta da Adobe Marketing Cloud e está registrado para as soluções do Analytics e do Público alvo.
* Você tem um formulário adaptativo publicado que os clientes podem acessar.

### Etapas do fluxo de trabalho {#workflow-steps}

#### Etapa 1: Configurar o Analytics e o Público alvo no AEM Forms {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar Analytics**

Para obter insights aprofundados sobre as interações de seus clientes com seus formulários, primeiro configure o Analytics no AEM Forms. Execute as seguintes etapas:

1. Criar um conjunto de relatórios no Adobe Analytics
1. Criar configuração de serviço em nuvem no AEM
1. Criar estrutura de serviço em nuvem em AEM
1. Configurar o serviço de configuração do AEM Forms Analytics no AEM
1. Habilitar análise no formulário no AEM

Para obter etapas detalhadas, consulte [Configurar análises e relatórios para formulários adaptáveis](../../forms/using/configure-analytics-forms-documents.md).

**Configurar Público alvo**

Para criar e executar testes A/B para seus formulários adaptáveis, configure o Público alvo no AEM Forms conforme descrito em [Configure e integre o Público alvo no AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Etapa 2: Relatório de análise de visualização {#step-view-analytics-report-br}

À medida que seus clientes acessam e interagem com formulários nos quais você ativou o Analytics, suas interações são capturadas em bancos de dados altamente seguros do Analytics. Os bancos de dados são segmentados por clientes e acessíveis por meio de conexões seguras.

É possível visualização um relatório de dentro do AEM para formulários habilitados para análise e análise de dados. Para visualização do relatório:

1. No servidor AEM, navegue até **Forms > Forms &amp; Documentos**.
1. Selecione o formulário para o qual deseja obter o relatório de análise.
1. Clique no ícone Relatórios do Analytics. O relatório é exibido.

Vamos analisar os pontos de dados que o Analytics coleta e relata para formulários.

**Relatório de análise do Forms**

O relatório de análise para formulários adaptáveis captura os seguintes KPIs (Indicadores-chave de desempenho) em um nível de formulário:

* **Tempo** médio de preenchimento: Tempo médio gasto no preenchimento do formulário
* **Impressões**: Número de vezes que o formulário foi exibido nos resultados da pesquisa

* **Representações**: Número de vezes que o formulário foi renderizado ou aberto
* **Rascunhos**: Número de vezes que o formulário foi salvo como rascunho

* **Envios**: Número de vezes que o formulário foi enviado
* **Abortar**: Número de vezes que os usuários deixaram sem preencher o formulário
* **Visitas/Envios**: Proporção de visitas por submissão

Além disso, você obtém os seguintes detalhes sobre cada painel no formulário:

* **Hora**: Tempo médio gasto (segundos) no painel e seus campos

* **Erro**: Número de erros encontrados no painel e seus campos por 1000 execuções de formulário

* **Ajuda**: Número de vezes que os usuários acessaram a ajuda no contexto para o painel e seus campos por 1000 execuções de formulário

![Um relatório de análise de amostra para um formulário adaptável](assets/summary-report.png)

Para obter mais detalhes sobre relatórios de análise de formulários, consulte [Visualizar e entender relatórios de análise do AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Você pode visualização relatórios detalhados e obter informações mais detalhadas sobre seus clientes e suas interações com seus formulários na conta do Analytics no Adobe Marketing Cloud.

#### Etapa 3: Analisar pontos de dados {#step-analyze-data-points}

Nessa etapa, você analisará os pontos de dados no relatório de análise e inferirá o desempenho do formulário. Se ele não atender seus KPIs de sucesso, você construirá hipóteses, com base em dados, e encontrará soluções possíveis para corrigir os problemas. Por exemplo:

* Se o tempo médio de preenchimento do formulário for maior do que a expectativa, é possível que o formulário seja complexo para que os clientes entendam, que o formulário não use terminologias padrão, que o formulário seja muito longo e assim por diante. Nesse caso, talvez você queira simplificar a estrutura e os campos do formulário, retrabalhar o design do formulário, encurtar o comprimento do formulário ou adicionar descrições de ajuda e exemplos para campos de formulário não padrão.
* Se os dados indicarem que a maioria dos clientes está acessando a ajuda de um painel de formulário, é evidente que os clientes estão intrigados com as informações a serem preenchidas. Você pode usar terminologia alternativa ou adicionar algumas entradas de exemplo e descrição de ajuda para esse painel.
* Se a taxa de aborto ou abandono de um formulário for maior do que o esperado, isso pode ocorrer devido ao fato de o formulário levar muito tempo para ser renderizado, os clientes estão chegando inadvertidamente no formulário ou é muito complicado. Nesse caso, talvez você queira otimizar a descrição do formulário que aparece nos resultados da pesquisa, simplificar o formulário, otimizar o formulário para um carregamento mais rápido e assim por diante.

Depois de analisar esses pontos de dados e chegar a uma hipótese, faça as alterações necessárias no formulário.

#### Etapa 4: Validar sua análise e correções {#step-validate-your-analysis-and-fixes}

Nesta etapa, você validará as alterações feitas no formulário e verificará se isso afeta a taxa de conversão.

**Executar um teste A/B**

A integração do AEM Forms com o Público alvo permite a criação de testes A/B para formulários adaptáveis. Em testes A/B, você apresenta aleatoriamente diferentes experiências de um formulário para seus clientes em tempo real para saber qual experiência funciona melhor ou causa mais conversões. Depois que você tiver dados significativos indicando uma experiência fornecendo uma conversão melhor que a outra, você poderá declarar que as experiências são vencedoras e, no futuro, a experiência padrão se tornará visível a todos os clientes.

Para obter mais informações sobre como criar um teste A/B para um formulário adaptável, consulte [Teste A/B de formulários adaptáveis](../../forms/using/ab-testing-adaptive-forms.md).

![Um exemplo de relatório de resumo do teste A/B para um formulário adaptável](assets/ab-test-report-4.png)

## Práticas recomendadas {#best-practices}

As práticas recomendadas reais são aquelas que você mesmo identifica ao executar esse fluxo de trabalho. Eles são exclusivos ao seu ambiente e aos seus requisitos. Capture seus aprendizados por meio do fluxo de trabalho e os documento como práticas recomendadas.

Algumas recomendações sobre como criar formulários e executar testes A/B são as seguintes:

**Design Forms**

* Mantenha o formulário simples, curto e fácil de navegar. Use dicas direcionais para navegação.
* Use terminologias padrão ou comuns para campos de formulário.
* Explique o campo e a entrada necessária, com exemplos ou ajuda, onde os usuários podem se confundir.
* Valide as entradas do usuário à medida que elas as digitam, sempre que possível, para evitar erros no envio do formulário.
* Otimize layouts para desktop e dispositivos móveis.
* Preencher automaticamente informações para usuários conhecidos.

**Testes A/B**

* Construa uma hipótese e identifique as métricas de sucesso antes de executar o teste A/B.
* Faça variações mínimas (idealmente uma de cada vez) na sua experiência alternativa para saber o que afetou a taxa de conversão.
* Teste frequentemente para eliminar ineficiências.

