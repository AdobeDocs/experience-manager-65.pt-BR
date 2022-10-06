---
title: Planejamento
seo-title: Planning
description: O que você precisa saber para planejar para seu teste
seo-description: What you need to know to plan for your test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Planejamento{#planning}

Este documento descreve o que você precisa saber para planejar seu teste. Além disso, você deve responder a essas perguntas antes de realizar seus testes:

* [Quais ambientes de teste serão necessários?](/help/sites-developing/test-environments.md)
* [Definição dos casos de teste](/help/sites-developing/test-cases.md)
* [Teste - quando e com quem?](/help/sites-developing/when-who.md)

## Antes de começar {#before-you-start}

Antes de começar com a análise real e a definição de testes, analise as seguintes informações:

**Arquitetura AEM** - Consulte Conceitos básicos para se apresentar à arquitetura e aos princípios básicos da AEM.

**Documentação** - Consulte qualquer uma das seções de documentação, ou artigos de Como, para obter mais informações.

**Princípios básicos dos testes** - Você deve estar ciente dos princípios básicos de teste de software e controle de qualidade. De preferência, você deve ter experiência em testar projetos.

Existem muitos sítios Web, livros e cursos que tratam desses princípios, pelo que não serão tratados em pormenor neste documento.

**Pressupostos para evitar** - A maior suposição (feita regularmente) é que o seu site precisará atender milhões de pedidos todos os dias. Em determinadas circunstâncias, isso pode ser verdade, mas não pode ser assumido.

Embora os números futuros não possam ser previstos com 100% de precisão, observar seu site existente e o tráfego experiente darão uma boa indicação. É possível tornar as estimativas dependentes do fator pelo qual você espera/espera que o tráfego aumente.

**Compromisso para a qualidade** - É de primordial importância que qualquer pessoa que faça testes permaneça neutra e que se limite a comunicar os resultados dos testes efetuados.

É da responsabilidade do gerente de projetos decidir e iniciar ações dependentes dos resultados.

**Tornar-se envolvido** - Embora seja da responsabilidade do Gestor de Projetos garantir que todas as partes estejam plenamente envolvidas em quaisquer reuniões (estatuto, workshops, etc.), deverá também tentar participar o mais cedo possível no ciclo do projeto, incluindo a recolha de informações e os processos de análise de requisitos.

**Envolva o cliente** - Em um tema semelhante, tente envolver o cliente (sempre que possível) ao definir seus casos de teste e plano.

## Tipos de testes {#types-of-tests}

Existem várias classificações-padrão de testes que são adequadas para serem usadas no teste de um projeto AEM. Familiarize-se com esses itens para decidir qual usará:

>[!NOTE]
>
>Estes estão enumerados na ordem cronológica de aplicação.

**Testes de Unidades** - Testes (geralmente) feitos pela equipe de desenvolvimento para garantir que os elementos individuais se comportem corretamente - ainda que isoladamente.

**Testes de integração** - Testa os módulos quando combinados. Esses testes são feitos após o teste de unidade, mas antes do teste do sistema.

**Testes de fumaça** - São testes rápidos e sujos usados para provar que o software está em execução e que a funcionalidade de alto nível está disponível. Os detalhes não são testados.

**Testes funcionais** - Elas são usadas para testar a funcionalidade do software. Será concebida uma série de ensaios para abranger todos os detalhes funcionais, com dados esperados e inesperados e/ou errôneos.

Os testes de caixa preta são testes funcionais de uma unidade/componente/módulo completo, realizados sem conhecimento do funcionamento interno do elemento em questão.

**Testes do sistema** - Teste todo o sistema assim que ele tiver sido totalmente integrado e instalado em uma plataforma adequada.

Eles testam a funcionalidade de caixa preta.

**Testes de desempenho** - Os testes de desempenho são cruciais para os testes de AEM.

Elas são usadas para ilustrar o desempenho em condições diferentes:

* Normal

   Condições que o site experimentará por 90% das vezes. Por exemplo, quando apenas uma proporção dos autores está usando o sistema.

* Pico

   Condições que serão experimentadas durante um período proporcionalmente curto devido a circunstâncias especiais; por exemplo, quando todos os autores usam o sistema simultaneamente ou quando novo conteúdo é publicado e um número maior de visitantes visualizam seu site.

* Extreme

   Pode ser usado para emular a previsão de desempenho quando um novo conteúdo extremamente interessante é publicado em seu site. Então pode-se observar um pico extremo - embora isto nem sempre seja totalmente previsível.

   Essas circunstâncias são, às vezes, vistas quando ingressos para eventos específicos são disponibilizados ou um site muito aguardado é publicado pela primeira vez.

Os resultados são então usados para ajustar o aplicativo.

**Testes de estresse** - São efetuados testes de esforço para confirmar o comportamento de um componente ou aplicativo em condições extremas. Em particular, esses testes são usados para mostrar como o comportamento se deteriora, quando o elemento falhará - e como.

**Testes de regressão** - Os testes de regressão são são usados para confirmar que a funcionalidade já comprovada em uma versão anterior do software ainda está funcionando corretamente.

Testes de regressão são são bons candidatos para automação (se possível) para garantir que possam ser repetidos de forma rápida e consistente.

**Testes de aceitação** - Os testes de aceitação são uma categoria especial, pois são usados para indicar a aceitação do projeto pelo cliente.

A lista de testes de aceitação pode conter uma combinação de testes das várias categorias acima e é selecionada para verificar se o projeto satisfaz os requisitos do cliente

Consulte [Aceitação e logoff](/help/sites-developing/acceptance-signoff.md) para obter mais detalhes.

## Introdução {#getting-started}

Antes de começar em seus Casos de teste e Plano de teste detalhados, você pode:

**Definir as metas** - Defina suas metas de alto nível para atuar como ponto de partida para o ajuste fino à medida que o teste prossegue. Você desejará:

* Teste a funcionalidade de acordo com a Especificação detalhada do requisito.
* Teste o desempenho de acordo com a [Métricas de meta](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre outros.

**Coletar estatísticas de tráfego do site existente** - Essas informações podem ser extraídas dos arquivos de log - consulte Monitoramento de desempenho para obter mais detalhes.

Estes números fornecerão uma indicação do tráfego (volume e difusão) atual no sítio Web existente e poderão ser utilizados para constituir um ponto de base para o novo sítio web.

**Coletar estatísticas de tráfego de sites externos** - Se possível, você pode tentar coletar estatísticas de tráfego de outros sites para comparação, mas esses números nem sempre são publicados.

**Confirmar métricas de meta** - As métricas são usadas para definir medidas quantitativas para a qualidade do site, pois representam os objetivos de desempenho a serem alcançados.

Devem ser definidas no início do projeto, juntamente com o cliente. Consulte [Métricas de meta](/help/sites-developing/planning.md) para obter mais informações.
