---
title: "Tutorial: Planejar a Comunicação Interativa"
description: Planeje a anatomia para sua comunicação interativa
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---

# Tutorial: Planejar a comunicação interativa {#tutorial-plan-the-interactive-communication}

Planeje a anatomia para sua comunicação interativa

![02-criar-formulário-adaptável-imagem-principal](assets/02-create-adaptive-form-main-image.png)

Este tutorial é uma etapa da [Criar a primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Especialistas no assunto de departamentos como jurídico, financeiro, de suporte ou de marketing podem ajudar você a finalizar o conteúdo. Depois que o conteúdo for finalizado, você deverá analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

## Considerações de planejamento {#planning-considerations}

Uma comunicação interativa inclui os seguintes elementos:

* **Texto estático** na sua maioria, inclui as partes da comunicação interativa que são de natureza genérica e estão incluídas na comunicação com todos os clientes. Por exemplo, cabeçalho, rodapé, saudação ou avisos de isenção de responsabilidade.
* **Dados obtidos de um sistema de back-end (modelo de dados de formulário)** é específico do cliente e é mesclado dinamicamente com a comunicação interativa. Por exemplo, o número da política ou o endereço pode ser originado usando o modelo de dados de formulário.
* **Layout ou modelos** para a versão impressa e para Web da comunicação interativa.
* **Pedido** nos quais os vários parágrafos de texto aparecem na Comunicação interativa.
* **Dados inseridos por um funcionário de linha de frente (interface do agente)** que está personalizando a comunicação antes de enviá-la. Por exemplo, a data de pagamento.

* **Dados condicionais** que é preenchida com base em condições predefinidas. Por exemplo, a data em que a comunicação interativa é gerada.
* **Imagens armazenadas em um repositório**, como logotipos e imagens de assinatura. Imagens como logotipos corporativos apareceriam na maioria ou em todas as comunicações interativas.
* **Gráficos e tabelas** para simplificar a representação de dados complexos numa comunicação interativa

## Anatomia da comunicação interativa {#anatomy-of-the-interactive-communication}

Depois de finalizar o conteúdo e os elementos usados para criar a Comunicação interativa, você pode criar uma anatomia da Comunicação interativa. A anatomia deve ter os detalhes listados na [Considerações sobre o planejamento](/help/forms/using/planning-interactive-communications.md#planning-considerations) seção. Com base em nosso caso de uso, veja a seguir um exemplo de anatomia da conta mensal que uma operadora de telecomunicações envia aos seus clientes.

A anatomia inclui dados com os seguintes modos de entrada:

* Texto estático
* Modelo de dados do formulário
* IU do agente
* Dados condicionais
* Imagens

Em cada seção, o texto em negrito representa texto estático. O banco de dados inclui tabelas de clientes, contas e chamadas. Um modelo de dados de formulário pode receber dados de qualquer uma dessas tabelas. Para obter mais informações, consulte [Criar modelo de dados de formulário](/help/forms/using/create-form-data-model0.md).

A tabela a seguir ilustra a fonte de dados de cada campo na anatomia da Comunicação Interativa:

<table>
 <tbody>
  <tr>
   <td>Seção</td>
   <td>Texto estático</td>
   <td>FDM </td>
   <td>IU do agente</td>
   <td>Imagens</td>
  </tr>
  <tr>
   <td>Detalhes da Lista</td>
   <td><p>Número da Fatura</p> <p>Data de Cobrança</p> <p>Período de Cobrança</p> <p>Seu plano</p> </td>
   <td><p>Valor para <strong>Seu plano </strong>campo</p> <p>Tabela: cliente</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Número da Fatura</li>
     <li>Data de Cobrança</li>
     <li>Período de Cobrança</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Detalhes do cliente</td>
   <td><p>Local de fornecimento</p> <p>Código de Estado</p> <p>Número de celular</p> <p>Número de Contato Alternativo</p> <p>Número do relacionamento</p> <p>Número de conexões</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Nome</li>
     <li>Endereço</li>
     <li>Número de celular</li>
     <li>Número de Contato Alternativo</li>
     <li>Número do relacionamento</li>
    </ul> <p>Tabela: cliente</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Local de fornecimento</li>
     <li>Código de Estado</li>
     <li>Número de conexões</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Sumário da Lista</td>
   <td><p>Saldo Anterior</p> <p>Pagamentos</p> <p>Ajustes</p> <p>Cobra o período de faturamento atual</p> <p>Valor Devido</p> <p>Data de vencimento</p> </td>
   <td><p>Valor para o <strong>Cobra o período de faturamento atual </strong> campo</p> <p>Tabela - listas</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Saldo Anterior</li>
     <li>Pagamentos</li>
     <li>Ajustes</li>
     <li>Valor Devido</li>
     <li>Data de vencimento</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Resumo dos encargos</td>
   <td><p>Encargos de chamada</p> <p>Encargos de Chamada em Conferência</p> <p>Encargos de SMS </p> <p>Encargos de Internet Móvel</p> <p>Tarifas de roaming nacional</p> <p>Tarifas de roaming internacional</p> <p>Encargos de Serviços de Valor Agregado</p> <p>Total de Encargos</p> <p>TOTAL A PAGAR</p> <p>Condição no campo Encargos de Serviços de Valor Agregado</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Encargos de chamada</li>
     <li>Encargos de Chamada em Conferência</li>
     <li>Encargos de SMS </li>
     <li>Encargos de Internet Móvel</li>
     <li>Tarifas de roaming nacional</li>
     <li>Tarifas de roaming internacional</li>
     <li>Encargos de Serviços de Valor Agregado</li>
     <li>Total de Encargos (campo calculado encargos de uso)</li>
     <li>TOTAL A PAGAR (campo calculado encargos de uso)</li>
    </ul> <p>Tabela - listas</p> </td>
   <td>Nenhum campo</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Chamadas discriminadas - Saída</td>
   <td><p>Nomes das colunas:</p>
    <ul>
     <li>Data</li>
     <li>Hora</li>
     <li>Número</li>
     <li>Duração</li>
     <li>Encargos</li>
    </ul> </td>
   <td><p>Todos os valores</p> <p>Tabela - chamadas</p> </td>
   <td>Nenhum campo</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Pagar agora</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Serviços de valor agregado</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
