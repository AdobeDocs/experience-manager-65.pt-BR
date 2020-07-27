---
title: Personalização do rastreamento de eventos de formulário
seo-title: Personalização do rastreamento de eventos de formulário
description: Se um usuário gastar mais de 60 segundos em um campo, um evento fieldvisit será acionado e os detalhes do campo serão enviados para o Adobe SiteCatalyst.
seo-description: Se um usuário gastar mais de 60 segundos em um campo, um evento fieldvisit será acionado e os detalhes do campo serão enviados para o Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Personalização do rastreamento de eventos de formulário {#customizing-form-event-tracking}

A partir da caixa, os seguintes eventos são rastreados em um formulário adaptativo habilitado para análise:

<table>
 <tbody>
  <tr>
   <th>Evento</th>
   <th>Variáveis disponíveis</th>
  </tr>
  <tr>
   <td>renderizar</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>abandono</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>erro</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>ajuda</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## Personalização do tempo limite do evento de visita de campo {#customizing-the-field-visit-event-timeout}

Na configuração padrão do formulário AEM, se um usuário gastar mais de 60 segundos em um campo, um `fieldvisit` evento será acionado e os detalhes do campo serão enviados para a Adobe Analytics. Você pode personalizar a linha de base de rastreamento de tempo de campo em Configuração do AEM Forms Analytics no console de configuração do AEM (/system/console/configMgr) para aumentar ou diminuir o limite de tempo limite.

## Personalização dos eventos de rastreamento {#customizing-the-tracking-events}

Você pode modificar a `trackEvent`função disponível no `/libs/afanalytics/js/custom.js` arquivo para personalizar o rastreamento de eventos. Sempre que um evento que está sendo rastreado ocorre em um formulário adaptável, a `trackEvent`função é chamada. A `trackEvent` função aceita dois parâmetros: `eventName`e `variableValueMap`.

Você pode avaliar o valor dos argumentos *eventName* e *variableValueMap* para alterar o comportamento de rastreamento dos eventos. Por exemplo, você pode optar por enviar as informações para o servidor do Analytics depois que ocorrer um determinado número de eventos de erro. Você também pode optar por executar qualquer uma das seguintes personalizações:

* É possível definir um tempo limite antes de enviar o evento.
* É possível manter um estado para decidir a ação, por exemplo, *fieldVisit* envia um evento fictício com base no carimbo de data e hora do último evento.
* Você pode usar a `pushEvent` função para enviar o evento para o servidor do Analytics *.*

* Você pode optar por não enviar o evento para o servidor do Analytics.

### Amostra {#sample}

No exemplo a seguir, o estado do evento de *erro* de cada atributo *fieldName* é mantido. O evento é enviado para o servidor do Analytics somente se ocorrer um erro novamente.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalização do evento panelvisit {#customizing-the-panelvisit-event}

Na configuração padrão dos AEM Forms, após cada 60 segundos, é verificado se a janela que contém o formulário adaptativo está ativa. Se a janela estiver ativa, um `panelVisit`evento será disparado para o Adobe Analytics. Isso ajuda a verificar se o documento ou o formulário está ativo e a calcular o tempo gasto no formulário ou documento correspondente.

>[!NOTE]
>
>O nome do evento usado para determinar a atividade e calcular o tempo gasto é &quot;panelVisit&quot;. Esse evento é diferente do evento de visita ao painel listado na tabela acima.

Você pode modificar a função ScheduleHeartBeatCheck disponível no `/libs/afanalytics/js/custom.js` arquivo para alterar ou parar esse evento enviado ao Adobe Analytics em um intervalo regular.
