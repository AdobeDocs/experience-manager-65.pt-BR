---
title: Visão geral das comunicações interativas
seo-title: Visão geral das comunicações interativas
description: Este artigo inclui visão geral, exemplos de casos de uso, fluxo de trabalho de criação e diferenças entre a Comunicação interativa e a carta.
seo-description: Recursos principais do Interative Communication, casos de uso de amostra, fluxo de trabalho de criação e diferenças entre o Interative Communication e o Gerenciamento de correspondência
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 5%

---


# Visão geral das comunicações interativas {#interactive-communications-overview}

Este artigo inclui visão geral, exemplos de casos de uso, fluxo de trabalho de criação e diferenças entre a Comunicação interativa e a carta.

![](do-not-localize/correspondence-management.png)

A Interative Communications centraliza e gerencia a criação, montagem e delivery de correspondências seguras, personalizadas e interativas, como correspondência comercial, documentos, declarações, avisos de benefícios, emails de marketing, contas e kits de boas-vindas.

## Principais recursos {#key-capabilities}

Veja a seguir os principais recursos das Comunicações interativas:

* Integração imediata com o modelo de dados de formulário para permitir acesso fácil e simplificado a bancos de dados back-end e outros sistemas CRM, como o MS® Dynamics
* Interface de criação integrada para canais de impressão e da Web com capacidade de gerar automaticamente canais da Web a partir do canal de impressão
* Gráficos para apresentar informações em formatos visuais facilmente compreensíveis na impressão e na Web
* Os fragmentos de documento oferecem suporte ao editor de regras e ao modelo de dados de formulário
* A interface do usuário do agente exibe a impressão e a pré-visualização da Web do Interative Communication
* Arraste e solte componentes para construir rapidamente canais de impressão e da Web

## Interactive Communication creation  {#interactive-communication-creation}

![interative_Communication-01](assets/interactive_communication-01.jpg)

### Fluxo de trabalho {#workflow}

Para criar uma comunicação interativa, tenha os [elementos básicos](#buildingblocks) para a comunicação interativa prontos e conclua as seguintes etapas:

1. Escolha para [criar uma comunicação](/help/forms/using/create-interactive-communication.md)interativa.

1. Especifique o modelo [de dados do](/help/forms/using/data-integration.md)formulário, o serviço de preenchimento prévio e os modelos [de](/help/forms/using/web-channel-print-channel.md)impressão e canal da Web. Você pode optar por gerar um canal da Web a partir do canal de impressão.

1. Usando a interface [de](/help/forms/using/introduction-interactive-communication-authoring.md)arrastar e soltar, adicione fragmentos de documento, imagens, componentes para imprimir e canal da Web da Interative Communication, conforme necessário.
1. Configure as propriedades dos componentes inseridos, como o seguinte:

   1. [Imagens](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabelas](/help/forms/using/create-interactive-communication.md#tables) (Incluindo Fragmentos de Layout)
   1. [Gráficos](/help/forms/using/chart-component-interactive-communications.md)
   1. [Fragmentos de documento](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Impressão de pré-visualização e canais da Web e, se necessário, edite a Comunicação interativa.
1. O agente usa a interface do agente para [preparar a Comunicação](/help/forms/using/prepare-send-interactive-communication.md) interativa para enviá-la ao processo de recipient/postagem.

### Elementos básicos {#buildingblocks}

A seguir estão os blocos de construção necessários para a criação de uma comunicação interativa:

* [Modelo de dados de formulário](/help/forms/using/data-integration.md)
* [Modelos de impressão e canal da Web](/help/forms/using/web-channel-print-channel.md)
* [Fragmentos de documento](/help/forms/using/document-fragments.md)
* Imagens
* [Temas](/help/forms/using/themes.md) para o canal Web

## Interative Communications Vs Correspondence Management {#interactive-communications-vs-correspondence-management}

A Interative Communication é a abordagem padrão e recomendada para criar comunicações de clientes. Para continuar usando as letras que criam no AEM 6.3 Forms e no AEM 6.2 Forms, é necessário [instalar um pacote](/help/forms/using/compatibility-package.md)de compatibilidade. Veja a seguir uma comparação entre os recursos de Comunicação interativa e carta.

<table>
 <tbody>
  <tr>
   <td><strong>Recurso</strong></td>
   <td><strong>Comunicação interativa</strong></td>
   <td><strong>Carta</strong></td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Imprimir e Web</td>
   <td>Impressão</td>
  </tr>
  <tr>
   <td>Esquema</td>
   <td>Modelo de dados de formulário </td>
   <td>Dicionário de dados </td>
  </tr>
  <tr>
   <td>Localização</td>
   <td>Não suportado no modelo de dados de formulário</td>
   <td>Suportado no dicionário de dados</td>
  </tr>
  <tr>
   <td>Editor de regras</td>
   <td>
    <ul>
     <li>Editor de regras de suporte a texto e condição para a criação de condições em linha</li>
     <li>O editor de comunicação interativa oferece suporte à aplicação de regras em componentes do canal da Web</li>
    </ul> </td>
   <td>Nenhuma interface do usuário para criação de expressão condicional</td>
  </tr>
  <tr>
   <td>Criação  </td>
   <td>Arraste e solte a interface para criar canais de impressão e da Web</td>
   <td>Nenhum mecanismo de arrastar e soltar </td>
  </tr>
  <tr>
   <td>Gráficos</td>
   <td>Gráficos suportados em impressão e canal da Web</td>
   <td>Não suportado</td>
  </tr>
  <tr>
   <td>Temas</td>
   <td>Usa temas para estilizar o canal da Web</td>
   <td>Não suporta temas</td>
  </tr>
  <tr>
   <td>Auditoria e controle de versão</td>
   <td>Não suportado</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Rascunhos e gerenciamento de instância</td>
   <td>Não suportado</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Processamento em lote</td>
   <td>Compatível </td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Assinatura do agente</td>
   <td>Não suportado</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Funções remotas</td>
   <td>Não suportado</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

