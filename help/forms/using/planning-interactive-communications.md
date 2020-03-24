---
title: '"Tutorial: Planeje a comunicação interativa"'
seo-title: Planeje sua comunicação interativa
description: Planeje a anatomia para sua comunicação interativa
seo-description: Planeje a anatomia para sua comunicação interativa
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375

---


# Tutorial: Planeje a comunicação interativa {#tutorial-plan-the-interactive-communication}

Planeje a anatomia para sua comunicação interativa

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial é uma etapa da série [Criar sua primeira comunicação](/help/forms/using/create-your-first-interactive-communication.md) interativa. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Especialistas de assuntos de departamentos como jurídico, financeiro, suporte ou marketing podem ajudá-lo a finalizar o conteúdo. Após a finalização do conteúdo, é necessário analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

## Considerações de planejamento {#planning-considerations}

Uma comunicação interativa inclui os seguintes elementos:

* **O texto** estático inclui principalmente as partes da comunicação interativa que são de natureza genérica e estão incluídas na comunicação com todos os clientes. Por exemplo, cabeçalho, rodapé, saudação ou isenções de responsabilidade.
* **Os dados originados de um sistema de backend (modelo de dados de formulário)** são específicos do cliente e são dinamicamente mesclados com a comunicação interativa. Por exemplo, o número ou endereço da política pode ser originado usando o modelo de dados de formulário.
* **Layout ou modelos** para as versões Imprimir e Web da Comunicação Interativa.
* **Ordem** em que os vários parágrafos de texto aparecem na Comunicação interativa.
* **Dados inseridos por um funcionário de linha de frente (IU do agente)** que está personalizando a comunicação antes de enviá-la. Por exemplo, a data de vencimento do pagamento.

* **Dados** condicionais que são preenchidos com base em condições predefinidas. Por exemplo, a data em que a comunicação interativa é gerada.
* **Imagens armazenadas em um repositório**, como logotipos e imagens de assinatura. Imagens como logotipos corporativos apareceriam na maioria ou em todas as comunicações interativas.
* **Gráficos e tabelas** necessários para simplificar a representação de dados complexos em uma comunicação interativa

## Anatomia da comunicação interativa {#anatomy-of-the-interactive-communication}

Depois de finalizar o conteúdo e os elementos usados para criar sua Comunicação interativa, você pode criar uma anatomia da Comunicação interativa. A anatomia deve ter os detalhes listados na seção Considerações [de](/help/forms/using/planning-interactive-communications.md#planning-considerations) Planejamento. Com base no nosso caso de uso, o exemplo a seguir é uma anatomia da conta mensal que um operador de telecom envia para seus clientes.

A anatomia inclui dados com os seguintes modos de entrada:

* Texto estático
* Modelo de dados de formulário
* IU do agente
* Dados condicionais
* Imagens

Em cada seção, o texto em negrito representa o texto estático. O banco de dados inclui tabelas de clientes, contas e chamadas. Um modelo de dados de formulário pode receber dados de qualquer uma dessas tabelas. Para obter mais informações, consulte [Criar modelo](/help/forms/using/create-form-data-model0.md)de dados de formulário.

A tabela a seguir ilustra a fonte de dados para cada campo na anatomia da Comunicação Interativa:

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
   <td><p>N.o da fatura</p> <p>Data da Cobrança</p> <p>Período de Cobrança</p> <p>Seu plano</p> </td>
   <td><p>Valor para o <strong>seu </strong>campo Plano</p> <p>Tabela - cliente</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>N.o da fatura</li>
     <li>Data da Cobrança</li>
     <li>Período de Cobrança</li>
    </ul> <p> </p> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Detalhes do cliente</td>
   <td><p>Local de fornecimento</p> <p>Código do Estado</p> <p>Número do celular</p> <p>Número de contato alternativo</p> <p>Número do Relacionamento</p> <p>Número de conexões</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Nome</li>
     <li>Endereço</li>
     <li>Número do celular</li>
     <li>Número de contato alternativo</li>
     <li>Número do Relacionamento</li>
    </ul> <p>Tabela - cliente</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Local de fornecimento</li>
     <li>Código do Estado</li>
     <li>Número de conexões</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumo da Lista</td>
   <td><p>Saldo anterior</p> <p>Pagamentos</p> <p>Ajustamentos</p> <p>Encargos do período de faturamento atual</p> <p>Valor Devido</p> <p>Data de vencimento</p> </td>
   <td><p>Valor para o campo Período de faturamento atual de <strong>Encargos </strong></p> <p>Tabela - faturas</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Saldo anterior</li>
     <li>Pagamentos</li>
     <li>Ajustamentos</li>
     <li>Valor Devido</li>
     <li>Data de vencimento</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumo das taxas</td>
   <td><p>Taxas de chamada</p> <p>Taxas de chamada de conferência</p> <p>Encargos SMS </p> <p>Taxas de Internet Móvel</p> <p>Taxas de roaming nacionais</p> <p>Taxas de roaming internacionais</p> <p>Encargos de Serviços de Valor Agregado</p> <p>Total de Encargos</p> <p>TOTAL A PAGAR</p> <p>Condição no campo Encargos de Serviços de Valor Agregado</p> </td>
   <td><p>Valores para os seguintes campos:</p>
    <ul>
     <li>Taxas de chamada</li>
     <li>Taxas de chamada de conferência</li>
     <li>Encargos SMS </li>
     <li>Taxas de Internet Móvel</li>
     <li>Taxas de roaming nacionais</li>
     <li>Taxas de roaming internacionais</li>
     <li>Encargos de Serviços de Valor Agregado</li>
     <li>Total de encargos (usagecharges campo calculado)</li>
     <li>TOTAL PAGÁVEL (campo de cálculo das taxas de utilização)</li>
    </ul> <p>Tabela - faturas</p> </td>
   <td>Nenhum campo</td>
   <td>--</td>
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
   <td>--</td>
  </tr>
  <tr>
   <td>Pagar Agora</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Serviços de valor agregado</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

