---
title: Planejamento
seo-title: Planning
description: O que você precisa saber para planejar seu teste
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

Este documento descreve o que você precisa saber para planejar o teste. Além disso, você deve responder a estas perguntas antes de realizar seus testes:

* [Quais ambientes de teste serão necessários?](/help/sites-developing/test-environments.md)
* [Definição dos casos de teste](/help/sites-developing/test-cases.md)
* [Testes - quando e com quem?](/help/sites-developing/when-who.md)

## Antes de começar {#before-you-start}

Antes de começar com a análise e definição reais de testes, analise as seguintes informações:

**Arquitetura do AEM** - Veja Conceitos básicos para se apresentar à arquitetura e aos princípios básicos do AEM.

**Documentação** - Consulte qualquer uma das seções de documentação ou os artigos de instruções para obter mais informações.

**Princípios básicos de teste** - Você deve estar ciente dos princípios básicos de Teste de Software e Garantia de Qualidade. De preferência, você deve ter experiência em testes de projetos.

Há muitos sites, livros e cursos que lidam com esses princípios e, portanto, não serão tratados em detalhes neste documento.

**Suposições a serem evitadas** - A maior suposição (feita regularmente) é que seu site precisará atender a milhões de solicitações todos os dias. Em certas circunstâncias, isso pode ser verdade, mas não pode ser presumido.

Embora os números futuros não possam ser previstos com 100% de precisão, observar o site existente e o tráfego experimentado fornecerá uma boa indicação. É possível fazer estimativas dependentes do fator pelo qual você espera/espera que o tráfego aumente.

**Compromisso com a qualidade** - É extremamente importante que qualquer pessoa que realize testes permaneça neutra e que comunique simplesmente os resultados dos testes realizados.

É responsabilidade do Gerente de projetos decidir e iniciar ações dependendo dos resultados.

**Envolva-se** - Embora seja responsabilidade do gerente de projeto garantir que todas as partes estejam totalmente envolvidas em qualquer reunião (status, workshops etc.), você também deve tentar se envolver o mais rápido possível no ciclo do projeto, incluindo os processos de coleta de informações e análise de requisitos.

**Envolver o cliente** - Em um tema semelhante, tente envolver o cliente (quando possível) ao definir seus casos de teste e planejar.

## Tipos de testes {#types-of-tests}

Existem várias classificações padrão de testes que são apropriados para uso ao testar um projeto de AEM. Familiarize-se com isso para decidir qual usará:

>[!NOTE]
>
>Eles são listados em sua ordem cronológica de aplicação.

**Testes de unidades** - Testes (geralmente) feitos pela equipe de desenvolvimento para garantir que os elementos individuais se comportem corretamente - embora isoladamente.

**Testes de integração** - Testa os módulos quando combinados. Esses testes são feitos após o Teste de unidade, mas antes do Teste do sistema.

**Testes de fumaça** - São testes rápidos e sujos usados para provar que o software está em execução e que a funcionalidade de alto nível está disponível. Os detalhes não foram testados.

**Testes funcionais** - Eles são usados para testar a funcionalidade do software. Uma série de testes será projetada para abranger todos os detalhes funcionais, com entrada esperada e/ou incorreta.

Os testes de caixa preta são testes funcionais de uma unidade/componente/módulo completos, realizados sem o conhecimento do funcionamento interno do elemento em questão.

**Testes do sistema** - Eles testam o sistema inteiro depois que ele estiver totalmente integrado e instalado em uma plataforma adequada.

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

**Testes de esforço** - São feitos testes de esforço para confirmar como um componente ou aplicativo se comporta em condições extremas. Esses testes são usados para mostrar como o comportamento se deteriora, quando o elemento falha e como.

**Testes de regressão** - Os testes de regressão são são usados para confirmar que a funcionalidade já comprovada em uma versão anterior do software ainda está funcionando corretamente.

Os testes de regressão são são bons candidatos para automação (se possível) a fim de garantir que possam ser repetidos de forma rápida e consistente.

**Testes de aceitação** - Os Testes de aceitação são uma categoria especial, pois são usados para indicar a aceitação do projeto pelo cliente.

A lista de testes de aceitação pode conter uma combinação de testes das várias categorias acima e é selecionada para verificar se o projeto atende aos requisitos do cliente

Consulte [Aceitação e aprovação](/help/sites-developing/acceptance-signoff.md) para obter mais detalhes.

## Introdução {#getting-started}

Antes de iniciar os Casos de teste detalhados e o Plano de teste, você pode:

**Definir as metas** - Defina suas metas de alto nível para agir como ponto de partida para o ajuste à medida que o teste continua. Você deverá:

* Teste a funcionalidade de acordo com a Especificação de requisitos detalhada.
* Desempenho do teste de acordo com a [Métricas do Target](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre outros.

**Coletar estatísticas de tráfego do site existente** - Essas informações podem ser extraídas dos arquivos de log - consulte Monitoramento de desempenho para obter mais detalhes.

Estes números darão uma indicação do tráfego atual (volume e propagação) no site existente e podem ser usados na formação de um ponto de base para o novo site.

**Coletar estatísticas de tráfego de sites externos** - Se possível, pode tentar recolher estatísticas de tráfego de outros sítios Web para comparação, mas estes números nem sempre são publicados.

**Confirmar métricas de direcionamento** - As métricas são utilizadas para definir medidas quantitativas para a qualidade do sítio Web, uma vez que representam os objetivos de desempenho a atingir.

Eles devem ser definidos no início do projeto, juntamente com o cliente. Consulte [Métricas do Target](/help/sites-developing/planning.md) para obter mais informações.
