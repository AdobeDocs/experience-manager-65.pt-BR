---
title: Definição dos casos de teste
seo-title: Defining your Test Cases
description: Os casos de teste devem se basear nos casos de uso e na especificação detalhada dos requisitos
seo-description: Your test cases should be based upon the use cases and the detailed requirements specification
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Definição dos casos de teste{#defining-your-test-cases}

Os casos de teste devem se basear no seguinte:

**Casos de uso**

* Eles definem a funcionalidade necessária em termos da interação entre os Atores (funções que iniciam determinadas ações) e o sistema.
* Os Casos de uso devem ser definidos pelo cliente.

**Especificação detalhada dos requisitos**

* Todos os requisitos funcionais e de desempenho devem ser testados.

Os ensaios devem definir claramente:

* Pré-requisitos; podem abranger sistemas, configurações ou experiência de testador específicos.
* Etapas a seguir; a um nível adequado de pormenor.
* Resultados esperados.
* Critérios claros para aprovação ou falha.

A perspectiva de automatizar casos de testes é obviamente atraente, pois pode eliminar tarefas repetitivas.

## Testes manuais versus automatizados {#manual-versus-automated-tests}

No entanto, a automatização dos casos de ensaio constitui um investimento significativo, pelo que devem ser considerados alguns aspectos:

* Requer tempo, esforço e experiência para configurar e configurar.
* Se o navegador for baseado, há um risco aumentado de problemas quando as atualizações do navegador são instaladas; exigindo mais tempo para corrigir.
* Só é realmente viável para grandes projetos.
* Bom quando várias versões estão sendo geradas para teste ou no plano de lançamento de longo prazo.

## Teste de aspectos específicos {#testing-specific-aspects}

Ao testar AEM alguns detalhes específicos são de especial interesse:

**Criar e publicar ambientes**

Embora, coberto por [Ambientes](/help/sites-developing/the-basics.md#environments) vale a pena destacar um fator decisivo de AEM no que diz respeito aos testes.

Você deve considerar AEM como dois aplicativos:

* o *Autor* ambiente Essa instância permite que os autores insiram e publiquem conteúdo.
Ele tem um conjunto pequeno (er) e previsível de usuários, para os quais a funcionalidade e o desempenho específicos são cruciais.

* o *Publicar* ambiente Essa instância apresenta o site em seu formulário publicado para acesso de visitantes.
Isso geralmente tem um conjunto maior de usuários, onde o volume de tráfego nem sempre é 100% previsível. O desempenho ainda é fundamental ao responder às solicitações. O armazenamento em cache e o balanceamento de carga também devem ser considerados.

Embora o mesmo software como tal, eles:

* servir diferentes finalidades
* têm requisitos diferentes em relação à funcionalidade e ao desempenho
* são configuradas de forma diferente
* são afinadas separadamente
* cada um terá seu próprio conjunto de testes de aceitação

Por outras palavras, devem ser testados separadamente e com casos de ensaio diferentes.

**Personalização**

Ao testar a personalização, cada caso de uso individual deve ser repetido usando várias contas de usuário para provar o comportamento.

O armazenamento em cache também deve ser verificado para verificar o comportamento correto.

**O Dispatcher**

A maioria dos projetos instalará o Dispatcher para armazenamento em cache e balanceamento de carga.

O teste é difícil (o armazenamento em cache ocorre em vários níveis e em vários locais) e deve ser feito em caixa preta. Os principais aspectos a serem testados são:

* **Precisão**
garanta que as atualizações de conteúdo sejam vistas pelo visitante do site.

* **Continuidade**
certifique-se de que o site ainda esteja disponível quando um servidor for desligado.

* **Clusters**
Os clusters são usados para fornecer:

   * **Failover**
Se um servidor falhar, outros servidores no cluster assumirão o processamento.

   * **Desempenho**
O balanceamento de carga com failover completo aumenta o desempenho de um cluster.
Quando usado para um projeto do cliente, o cluster deve ser testado para confirmar a operação correta da configuração.

## Teste de software de terceiros {#testing-third-party-software}

Qualquer software de terceiros com interface de AEM será referenciado nas Especificações de Requisitos Detalhadas.

Os ensaios necessários (dependendo do âmbito definido) devem ser analisados e obtidos ensaios limpos.
