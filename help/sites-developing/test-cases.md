---
title: Definição dos casos de teste
seo-title: Defining your Test Cases
description: Seus casos de teste devem se basear nos casos de uso e na especificação detalhada dos requisitos
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

Seus casos de teste devem se basear no:

**Casos de uso**

* Eles definem a funcionalidade necessária em termos da interação entre os Atores (funções que iniciam determinadas ações) e o sistema.
* Os casos de uso devem ser definidos pelo cliente.

**Especificação detalhada dos requisitos**

* Todos os requisitos funcionais e de desempenho devem ser testados.

Os ensaios devem definir claramente:

* Pré-requisitos; eles podem abranger sistemas específicos, configurações ou experiência do testador.
* Etapas a serem seguidas, em um nível apropriado de detalhes.
* Resultados esperados.
* Limpar critérios para aprovação ou reprovação.

A perspectiva de automatizar casos de teste é obviamente atraente, pois pode eliminar tarefas repetitivas.

## Testes manuais versus testes automatizados {#manual-versus-automated-tests}

No entanto, a automatização de casos de teste é um investimento significativo, portanto, alguns aspectos devem ser considerados:

* Requer tempo, esforço e experiência para instalar e configurar o.
* Se baseado em navegador, há um risco maior de problemas quando as atualizações do navegador são instaladas; é necessário mais tempo para corrigir.
* Apenas muito viável para grandes projetos.
* Bom quando várias versões estão sendo geradas para teste ou no plano de lançamento de longo prazo.

## Testar aspectos específicos {#testing-specific-aspects}

Ao testar o AEM, alguns detalhes específicos são de especial interesse:

**Ambientes de criação e publicação**

Embora, [Ambientes](/help/sites-developing/the-basics.md#environments) vale destacar um fator decisivo do AEM em relação aos testes.

Você deve considerar o AEM como dois aplicativos:

* o *Autor* ambiente Essa instância permite que os autores insiram e publiquem conteúdo.
Ele tem um pequeno conjunto previsível de usuários, para os quais a funcionalidade e o desempenho específicos são cruciais.

* o *Publish* ambiente Essa instância apresenta o site em seu formulário publicado para acesso dos visitantes.
Isso geralmente tem um conjunto maior de usuários, em que o volume de tráfego nem sempre é 100% previsível. O desempenho ainda é crucial ao responder às solicitações. O armazenamento em cache e o balanceamento de carga também devem ser considerados.

Embora sejam o mesmo software, eles:

* servir a diferentes propósitos
* têm requisitos diferentes em relação à funcionalidade e ao desempenho
* são configurados de forma diferente
* são ajustados separadamente
* cada um terá seu próprio conjunto de testes de aceitação

Em outras palavras, eles devem ser testados separadamente e com casos de teste diferentes.

**Personalização**

Ao testar a personalização, cada caso de uso individual deve ser repetido usando várias contas de usuário para provar o comportamento.

O armazenamento em cache também deve ser verificado para verificar o comportamento correto.

**O Dispatcher**

A maioria dos projetos instalará o Dispatcher para armazenamento em cache e balanceamento de carga.

Os testes são difíceis (o armazenamento em cache ocorre em vários níveis e em vários locais) e devem ser feitos em uma base de caixa preta. Os principais aspectos a serem testados são:

* **Precisão**
certifique-se de que as atualizações de conteúdo sejam vistas pelo visitante do site.

* **Continuidade**
verifique se o site ainda está disponível quando um servidor é desligado.

* **Clusters**
Os clusters são usados para fornecer:

   * **Failover**
Se um servidor falhar, outros servidores no cluster assumirão o processamento.

   * **Desempenho**
O balanceamento de carga com failover completo aumenta o desempenho de um cluster.
Quando usado para um projeto de cliente, o cluster deve ser testado para confirmar a operação correta da configuração.

## Teste de software de terceiros {#testing-third-party-software}

Qualquer software de terceiros com interface com AEM será mencionado nas Especificações detalhadas de requisitos.

Devem analisar-se todos os ensaios necessários (dependendo do âmbito definido) e obter-se um ensaio limpo.
