---
title: Planejamento
seo-title: Planejamento
description: O que você precisa saber para planejar seu teste
seo-description: O que você precisa saber para planejar seu teste
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---


# Planejamento{#planning}

Este documento descreve o que você precisa saber para planejar seu teste. Além disso, você deve responder a essas perguntas antes de realizar seus testes:

* [Quais Ambientes de teste serão necessários?](/help/sites-developing/test-environments.md)
* [Definição dos casos de teste](/help/sites-developing/test-cases.md)
* [Teste - quando e com quem?](/help/sites-developing/when-who.md)

## Antes de começar {#before-you-start}

Antes de start com a análise real e a definição dos testes, consulte as seguintes informações:

**Arquitetura**  AEM - Consulte Conceitos básicos para se apresentar à arquitetura e aos princípios básicos da AEM.

**Documentação**  - Consulte qualquer uma das seções de documentação ou os artigos &quot;Como&quot; para obter mais informações.

**Princípios básicos de teste**  - Você deve estar ciente dos princípios básicos de teste de software e controle de qualidade. De preferência, você deve ter experiência em projetos de teste.

Há muitos websites, livros e cursos que tratam desses princípios e, portanto, não serão tratados em detalhes neste documento.

**Pressupostos para evitar**  - A maior suposição (feita regularmente) é que seu site da Web precisará atender a milhões de solicitações todos os dias. Em determinadas circunstâncias, isso pode ser verdade, mas não pode ser assumido.

Embora os números futuros não possam ser previstos com 100% de precisão, a observação do site existente e do tráfego vivido dará uma boa indicação. Você pode, então, tornar as estimativas dependentes do fator pelo qual você espera / espera que o tráfego aumente.

**Compromisso com a qualidade**  - É da maior importância que qualquer pessoa que faça testes permaneça neutro e simplesmente comunique os resultados dos testes efetuados.

Cabe ao gestor do projeto decidir e iniciar ações em função dos resultados.

**Envolver** -se - Embora seja da responsabilidade do Gerente de projetos garantir que todas as partes estejam plenamente envolvidas em qualquer reunião (status, workshops, etc.), você também deve tentar se envolver o mais cedo possível no ciclo do projeto, incluindo os processos de coleta de informações e de análise obrigatória.

**Envolver o cliente**  - em um tema semelhante, tente envolver o cliente (sempre que possível) ao definir seus casos de teste e seu plano.

## Tipos de testes {#types-of-tests}

Existem várias classificações padrão de testes que são apropriadas para uso ao testar um projeto AEM. Familiarize-se com estes itens para decidir qual usará:

>[!NOTE]
>
>Estes estão listados por ordem cronológica de aplicação.

**Testes**  de unidades - Testes (geralmente) feitos pela equipe de desenvolvimento para garantir que os elementos individuais se comportem corretamente - embora isoladamente.

**Testes**  de integração - Testa os módulos quando combinados. Esses testes são feitos após o teste de unidade, mas antes do teste do sistema.

**Testes**  de fumaça - são testes rápidos e sujos usados para provar que o software está em execução e que a funcionalidade de alto nível está disponível. Os detalhes não são testados.

**Testes**  funcionais - são usados para testar a funcionalidade do software. Uma série de testes será concebida para abranger todos os pormenores funcionais, com dados esperados e inesperados e/ou errôneos.

Os ensaios em caixa preta são testes funcionais de uma unidade completa / componente / módulo, efetuados sem conhecimento do funcionamento interno do elemento em questão.

**Testes**  do sistema - Eles testam o sistema inteiro depois que ele estiver totalmente integrado e instalado em uma plataforma adequada.

Eles testam a funcionalidade com base em caixa preta.

**Testes**  de desempenho - Os testes de desempenho são cruciais ao testar AEM.

Eles são usados para ilustrar o desempenho em condições diferentes:

* Normal

   Condições que o site experimentará por, digamos, 90% das vezes. Por exemplo, quando apenas uma proporção dos autores está usando o sistema.

* Pico

   Condições que serão sentidas durante um período de tempo proporcionalmente curto devido a circunstâncias especiais; por exemplo, quando todos os autores usam o sistema simultaneamente ou quando novo conteúdo é publicado e um número maior de visitantes visualização seu site.

* Extreme

   Pode ser usado para emular a previsão de desempenho quando um novo conteúdo extremamente interessante é publicado em seu site. Então pode-se observar um pico extremo - embora isso nem sempre seja totalmente previsível.

   Essas circunstâncias são observadas às vezes quando ingressos para eventos específicos são disponibilizados, ou um site muito aguardado é publicado pela primeira vez.

Os resultados são então usados para ajustar o aplicativo.

**Testes**  de estresse - Testes de estresse são feitos para confirmar como um componente ou aplicativo se comporta em condições extremas. Em particular, esses testes são usados para mostrar como o comportamento se deteriora, quando o elemento falhará - e como.

**Testes**  de regressão - Os testes de regressão são são utilizados para confirmar que a funcionalidade já comprovada numa versão anterior do software ainda está a funcionar corretamente.

Os testes de regressão são são bons candidatos à automação (se possível) para garantir que possam ser repetidos rápida e consistentemente.

**Testes**  de aceitação - Os Testes de aceitação são uma categoria especial, pois são usados para indicar a aceitação do projeto pelo cliente.

A lista dos testes de aceitação pode conter uma combinação de testes das várias categorias acima e são selecionados para verificar se o projeto atende aos requisitos do cliente

Consulte [Aceitação e Logoff](/help/sites-developing/acceptance-signoff.md) para obter mais detalhes.

## Introdução {#getting-started}

Antes de iniciar em seus casos de teste e plano de teste detalhados, você pode:

**Defina as metas**  - Defina suas metas de alto nível para agir como um ponto de partida para o ajuste fino à medida que o teste prossegue. Você desejará:

* Teste a funcionalidade de acordo com a Especificação detalhada do requisito.
* Teste o desempenho de acordo com as [Métricas do Público alvo](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

entre outros.

**Colete estatísticas de tráfego do site**  existente - Essas informações podem ser extraídas dos arquivos de log - consulte Monitoramento de desempenho para obter mais detalhes.

Estes valores fornecerão uma indicação do tráfego atual (volume e difusão) no sítio Web existente e poderão ser utilizados para formar um ponto de base para o novo sítio web.

**Coletar estatísticas de tráfego de sites**  externos - Se possível, você pode tentar coletar estatísticas de tráfego de outros sites para comparação, mas esses números nem sempre são publicados.

**Confirmar métricas**  de Público alvo - as métricas são usadas para definir medidas quantitativas para a qualidade do site, já que representam as metas de desempenho a serem alcançadas.

Devem ser definidas no start do projeto, juntamente com o cliente. Consulte [Métricas de Público alvo](/help/sites-developing/planning.md) para obter mais informações.
