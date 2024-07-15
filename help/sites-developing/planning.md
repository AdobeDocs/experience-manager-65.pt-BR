---
title: Planejamento
description: Saiba o que precisa saber para planejar o teste do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# Planejamento{#planning}

Este documento descreve o que você precisa saber para planejar o teste. Além disso, você deve responder a estas perguntas antes de realizar seus testes:

* [Quais ambientes de teste serão necessários?](/help/sites-developing/test-environments.md)
* [Definição dos casos de teste](/help/sites-developing/test-cases.md)
* [Testes - quando e com quem?](/help/sites-developing/when-who.md)

## Antes de começar {#before-you-start}

Antes de começar com a análise e definição reais de testes, analise as seguintes informações:

**Arquitetura do AEM** - Consulte Conceitos Básicos para se apresentar à arquitetura e aos princípios básicos do AEM.

**Documentação** - Consulte qualquer uma das seções de documentação ou os artigos de instrução para obter mais informações.

**Princípios Básicos de Teste** - Você deve estar ciente dos princípios básicos de Teste de Software e Garantia de Qualidade. De preferência, você deve ter experiência em testes de projetos.

Há muitos sites, livros e cursos que lidam com esses princípios e, portanto, não serão tratados em detalhes neste documento.

**Suposições a serem evitadas** - A maior suposição é que seu site deve atender a milhões de solicitações todos os dias. Em certas circunstâncias, isso pode ser verdade, mas não pode ser presumido.

Embora os números futuros não possam ser previstos com 100% de precisão, observar o site existente e o tráfego experimentado fornecerá uma boa indicação. É possível fazer estimativas dependentes do fator pelo qual você espera/espera que o tráfego aumente.

**Compromisso com a qualidade** - É de suma importância que qualquer pessoa que realize testes permaneça neutra e simplesmente relate os resultados dos testes feitos.

É responsabilidade do Gerente de projetos decidir e iniciar ações dependendo dos resultados.

**Envolver-se** - Embora seja responsabilidade do Gerente de Projetos garantir que todas as partes estejam totalmente envolvidas em qualquer reunião (status, workshops, etc.), você também deve tentar se envolver o mais rápido possível no ciclo do projeto, incluindo a coleta de informações e os processos de análise de requisitos.

**Envolver o Cliente** - Em um tema semelhante, tente envolver o cliente (quando possível) ao definir seus casos e planos de teste.

## Tipos de testes {#types-of-tests}

Existem várias classificações padrão de testes que são apropriados para uso ao testar um projeto de AEM. Familiarize-se com isso para decidir qual usará:

>[!NOTE]
>
>Eles são listados em sua ordem cronológica de aplicação.

**Testes de Unidades** - Testes (geralmente) feitos pela equipe de desenvolvimento para garantir que os elementos individuais se comportem corretamente, embora isoladamente.

**Testes de integração** - Testa os módulos quando combinados. Esses testes são feitos após o Teste de unidade, mas antes do Teste do sistema.

**Testes de fumaça** - São testes rápidos e sujos usados para provar que o software está em execução e que a funcionalidade de alto nível está disponível. Os detalhes não foram testados.

**Testes funcionais** - Usados para testar a funcionalidade do software. Uma série de testes será projetada para abranger todos os detalhes funcionais, com entrada esperada e/ou incorreta.

Os testes de caixa preta são testes funcionais de uma unidade/componente/módulo completos, realizados sem o conhecimento do funcionamento interno do elemento em questão.

**Testes do sistema** - Estes testes testam o sistema inteiro uma vez que ele tenha sido totalmente integrado e instalado em uma plataforma adequada.

Eles testam a funcionalidade com base em uma caixa preta.

**Testes de desempenho** - Os testes de desempenho são cruciais ao testar o AEM.

Eles são usados para ilustrar o desempenho em condições diferentes:

* Normal

  Condições que o site experimentará por, digamos, 90% do tempo. Por exemplo, quando apenas uma proporção dos autores está usando o sistema.

* Pico

  Condições que serão enfrentadas por um tempo proporcionalmente curto devido a circunstâncias especiais; por exemplo, quando todos os autores usam o sistema simultaneamente ou quando o novo conteúdo é publicado e um número maior de visitantes visualizam o site.

* Extreme

  Pode ser usado para emular a previsão de desempenho quando um novo conteúdo extremamente interessante é publicado em seu site. Então, um pico extremo pode ser visto - embora isso nem sempre seja totalmente previsível.

  Essas circunstâncias são às vezes vistas quando ingressos para eventos específicos são disponibilizados ou um site muito aguardado é publicado pela primeira vez.

Os resultados são usados para ajustar o aplicativo.

**Testes de estresse** - Os testes de estresse são feitos para confirmar como um componente ou aplicativo se comporta em condições extremas. Esses testes são usados para mostrar como o comportamento se deteriora, quando o elemento falha e como.

**Testes de regressão** - Os testes de regressão são são usados para confirmar se a funcionalidade já comprovada em uma versão anterior do software ainda está funcionando corretamente.

Os testes de regressão são são bons candidatos para automação (se possível) a fim de garantir que possam ser repetidos de forma rápida e consistente.

**Testes de aceitação** - Os testes de aceitação são uma categoria especial, pois são usados para indicar a aceitação do projeto pelo cliente.

A lista de testes de aceitação pode conter uma combinação de testes das várias categorias acima e é selecionada para verificar se o projeto atende aos requisitos do cliente

Consulte [Aceitação e aprovação](/help/sites-developing/acceptance-signoff.md) para obter mais detalhes.

## Introdução {#getting-started}

Antes de iniciar os Casos de teste detalhados e o Plano de teste, você pode:

**Definir as metas** - Defina suas metas de alto nível para agir como ponto de partida para o ajuste à medida que o teste prossegue. Você deverá:

* Teste a funcionalidade de acordo com a Especificação de requisitos detalhada.
* Teste o desempenho de acordo com as [Métricas de destino](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre outros.

**Coletar estatísticas de tráfego do site existente** - Essas informações podem ser extraídas dos arquivos de log - consulte Monitoramento de Desempenho para obter mais detalhes.

Estes números darão uma indicação do tráfego atual (volume e propagação) no site existente e podem ser usados na formação de um ponto de base para o novo site.

**Coletar estatísticas de tráfego de sites externos** - Se possível, você pode tentar coletar estatísticas de tráfego de outros sites para comparação, mas esses números nem sempre são publicados.

**Confirmar métricas de destino** - As métricas são usadas para definir medidas quantitativas para a qualidade do site, pois representam as metas de desempenho a serem atingidas.

Eles devem ser definidos no início do projeto, juntamente com o cliente. Consulte [Métricas de destino](/help/sites-developing/planning.md) para obter mais informações.
