---
title: Visualizar e entender os relatórios do AEM Forms Analytics
seo-title: View and understand AEM Forms analytics reports
description: O AEM Forms integra-se ao Adobe Analytics e fornece resumo e análises detalhadas sobre os formulários adaptáveis publicados.
seo-description: AEM Forms integrates with Adobe Analytics and provides you summary and detailed analytics about your published adaptive forms.
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 2%

---

# Visualizar e entender os relatórios do AEM Forms Analytics {#view-and-understand-aem-forms-analytics-reports}

O Adobe Experience Manager Forms integra-se ao Adobe Analytics, o que permite capturar e rastrear as métricas de desempenho dos formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões informadas com base em dados sobre as alterações necessárias para tornar os formulários ou documentos mais utilizáveis.

## Configuração de análises {#setting-up-analytics}

O recurso de análise no AEM Forms está disponível como parte do pacote complementar do AEM Forms. Para obter informações sobre como instalar o pacote complementar, consulte [Instalação e configuração do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Além do pacote complementar, você precisa de uma conta do Adobe Analytics. Para obter informações sobre a solução, consulte [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Depois de ter o pacote complementar do AEM Forms e uma conta do Adobe Analytics, integre a conta do Adobe Analytics ao AEM Forms e ative o rastreamento em seus formulários ou documentos, conforme descrito em [Configurar análises e relatórios](../../forms/using/configure-analytics-forms-documents.md).

### Como as informações de interação do usuário são registradas {#how-user-interaction-information-is-recorded}

Quando um usuário interage com o formulário, as interações são registradas e enviadas ao servidor do Analytics. A lista a seguir indica chamadas do servidor para várias atividades do usuário:

* 2 chamadas por campo por visita
* 1 para visita ao painel
* 1 para salvar
* 2 para envio
* 2 para salvar
* 1 para obter ajuda
* 1 para cada erro de validação
* 1 para Representação de formulário + 1 para visita de painel padrão + 1 para visita de campo padrão 1ª
* 2 para Abandono de formulário

>[!NOTE]
>
>Esta lista não é exaustiva.

### Exibição de relatórios de análise {#summary-report}

Execute as seguintes etapas para exibir relatórios de análise:

1. Faça logon no portal AEM em `https://[hostname]:'port'`
1. Clique em **Forms > Forms e documentos**.
1. Selecione o formulário para o qual deseja exibir os relatórios de análise.
1. Selecionar **Mais > Relatórios do Analytics**.

![analyticsreport](assets/analyticsreport.png)

**A.** comando Relatório do Analytics

O AEM Forms exibe relatórios do Analytics para o formulário e para cada painel no formulário, conforme mostrado abaixo.

![Relatório de resumo de um formulário adaptável](assets/analyticsdashboard_callout.png)

**A.** Conversões **B.** Resumo no nível do formulário **C** Resumo no nível do painel **D.** Navegadores de visitantes - filtro **E** SO de visitantes - filtro **F** Idioma dos visitantes - filtro

Por padrão, o relatório de análise dos últimos sete dias é exibido. Você pode exibir relatórios dos últimos 15 dias, do último mês e assim por diante, ou especificar um intervalo de datas.

>[!NOTE]
>
>As opções como Últimos 7 dias e Últimos 15 dias não incluem dados do dia em que você está gerando o relatório de análise. Para incluir os dados do dia atual, é necessário especificar o intervalo de datas, incluindo o dia atual, e executar o relatório.

![intervalo de datas](assets/date-range.png)

### Gráfico de conversões para formulários adaptáveis e HTML5 {#conversions-graph-for-adaptive-and-html-forms}

O gráfico de conversões no nível do formulário fornece informações sobre o desempenho do formulário nos seguintes KPIs (indicadores-chave de desempenho):

* **Representações**: O número de vezes que um formulário é aberto
* **Visitantes**: o número de visitantes do formulário
* **Envios**: Número de vezes que o formulário foi enviado

![gráfico de conversão](assets/conversion-graph.png)

### Relatório do Analytics para formulários adaptáveis e HTML5 {#analytics-report-for-adaptive-and-html-forms}

A seção de resumo no nível do formulário fornece informações sobre o desempenho do formulário nos seguintes KPIs (indicadores-chave de desempenho):

* **Tempo médio de preenchimento**: Tempo médio gasto no preenchimento do formulário. Quando os usuários passam tempo no formulário, mas não enviam, esse tempo não é incluído nesse cálculo.
* **Representações**: Número de vezes que o formulário foi renderizado ou aberto
* **Rascunhos**: Número de vezes que o formulário foi salvo como rascunho
* **Envios**: Número de vezes que o formulário foi enviado
* **Anular**: Número de vezes que os usuários começaram a preencher o formulário e depois saíram sem preenchê-lo
* **Visitantes únicos**: Número de vezes que o formulário é &quot;renderizado por visitantes únicos&quot;. Para obter mais informações sobre visitantes únicos, consulte [Visitantes únicos, visitas e comportamento do cliente](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html).

![Relatório de análise de resumo em nível de formulário expandido](assets/analytics-report.png)

### Relatório do painel {#bottom-summary-report}

A seção de resumo no nível do painel fornece as seguintes informações sobre cada painel no formulário:

* **Tempo Médio de Preenchimento**: Tempo médio gasto no painel, seja o formulário enviado ou não
* **Erros Encontrados**: Número médio de erros encontrados pelos usuários nos campos de um painel. Errors Encountered é obtido dividindo o total de erros em um campo pelo número de representações do formulário.
* **Ajuda Acessada**: Número médio de vezes que os usuários acessaram a ajuda em contexto para os campos no painel. A Ajuda acessada é obtida dividindo o número total de vezes que a Ajuda é acessada para um campo pelo número de representações do formulário.

#### Relatório detalhado do painel {#detailed-panel-report}

Você também pode exibir detalhes de cada painel clicando no nome de um painel no Relatório do painel.

![Relatório detalhado do painel](assets/panel-report-detailed.png)

O relatório detalhado mostra valores para todos os campos no painel.

O relatório do painel tem três guias:

* **Relatório de tempo**(Padrão): exibe o tempo, em segundos, gasto no preenchimento de cada um dos campos no painel
* **Relatório de erros**: exibe o número de erros encontrados pelos usuários durante o preenchimento dos campos
* **Relatório de ajuda**: Número de vezes que a ajuda de um determinado campo foi acessada

Você pode navegar entre os painéis, se vários painéis estiverem disponíveis.

### Filtros: navegador, sistema operacional e idioma {#filters-browser-os-and-language}

As tabelas Distribuição do navegador, Distribuição do sistema operacional e Distribuição de idioma exibem as representações, os visitantes e os envios de acordo com os navegadores, o sistema operacional e o Idioma dos usuários do formulário. Por padrão, essas tabelas exibem no máximo cinco entradas. Você pode clicar em Mostrar mais para exibir mais entradas e clicar em Mostrar menos para voltar às cinco entradas regulares ou menos.

Para filtrar ainda mais os dados de análise, você pode clicar em uma entrada em qualquer uma das tabelas. Por exemplo, se você clicar em Google Chrome na tabela Distribuição do navegador, o relatório será renderizado novamente com dados relevantes para o navegador Google Chrome, da seguinte maneira:

![Filtro aplicado ao relatório do Analytics - Google Chrome ](assets/filter-1.png)

Se você exibir o relatório do painel depois de aplicar um filtro, os dados do relatório do painel também serão exibidos de acordo com o filtro aplicado.

Depois que um filtro é aplicado:

* As tabelas de distribuição se tornam somente leitura, pois somente um filtro pode ser aplicado de cada vez.
* A tabela do filtro aplicado desaparece.
* Você pode clicar no botão Close (realçado abaixo) para remover o filtro aplicado.

![Botão Fechar para remover o filtro aplicado](assets/close-filter.png)

### Teste A/B {#a-b-testing}

Se você tiver o teste A/B ativado e configurado para o formulário, a página do relatório terá um menu suspenso que você pode usar para exibir o relatório de teste A/B. O relatório de teste A/B exibe o desempenho comparativo de duas versões do formulário conforme você configurou.

Para obter mais informações sobre o teste A/B, consulte [Criar e gerenciar teste A/B para formulários adaptáveis](../../forms/using/ab-testing-adaptive-forms.md).
