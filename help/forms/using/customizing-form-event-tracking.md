---
title: Personalização do rastreamento de eventos do formulário
seo-title: Customizing form event tracking
description: Se um usuário gastar mais de 60 segundos em um campo, um evento fieldvisit é acionado e os detalhes do campo são enviados ao Adobe SiteCatalyst.
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Personalização do rastreamento de eventos do formulário {#customizing-form-event-tracking}

Imediatamente, os seguintes eventos são rastreados em um Formulário adaptável habilitado para análise:

<table>
 <tbody>
  <tr>
   <th>Evento</th>
   <th>Variáveis disponíveis</th>
  </tr>
  <tr>
   <td>renderizar</td>
   <td>formName, formTitle, formInstance, origem</td>
  </tr>
  <tr>
   <td>abandonar</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>enviar</td>
   <td>formName, formTitle, formInstance, origem</td>
  </tr>
  <tr>
   <td>erro</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>Ajuda com o </td>
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

Na configuração padrão do formulário AEM, se um usuário gastar mais de 60 segundos em um campo, uma variável `fieldvisit` evento é acionado e os detalhes do campo são enviados para o Adobe Analytics. Você pode personalizar a linha de base do Rastreamento de tempo de campo em Configuração do AEM Forms Analytics no console de configuração do AEM (/system/console/configMgr) para aumentar ou diminuir o tempo limite.

## Personalização dos eventos de rastreamento {#customizing-the-tracking-events}

Você pode modificar a variável `trackEvent`função disponível em `/libs/afanalytics/js/custom.js` arquivo para personalizar o rastreamento de eventos. Sempre que um evento que está sendo rastreado ocorrer em um formulário adaptável, a variável `trackEvent`é chamada. A variável `trackEvent` A função aceita dois parâmetros: `eventName`e `variableValueMap`.

É possível avaliar o valor de *eventName* e *variableValueMap* argumentos para alterar o comportamento de rastreamento dos eventos. Por exemplo, você pode optar por enviar as informações para o servidor do Analytics após um determinado número de eventos de erro. Você também pode optar por executar qualquer uma das seguintes personalizações:

* Você pode definir um tempo limite antes de enviar o evento.
* É possível manter um estado para decidir a ação, por exemplo, *fieldVisit* envia um evento fictício com base no carimbo de data e hora do último evento.
* Você pode usar o `pushEvent` função para enviar o evento ao servidor do analytics *.*

* Você pode optar por não enviar o evento para o servidor do Analytics.

### Amostra {#sample}

No exemplo a seguir, digite para a variável *erro* evento de cada *fieldName* atributo é mantido. O evento é enviado ao servidor do Analytics somente se ocorrer um erro novamente.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalização do evento de visita do painel {#customizing-the-panelvisit-event}

Na configuração padrão do AEM Forms, após cada 60 segundos, é verificado se a janela que contém o formulário adaptável está ativa. Se a janela estiver ativa, uma variável `panelVisit`evento é acionado para o Adobe Analytics. Isso ajuda a verificar se o documento ou o formulário está ativo e a calcular o tempo gasto no formulário ou documento correspondente.

>[!NOTE]
>
>O nome do evento usado para determinar a atividade e calcular o tempo gasto é &quot;panelVisit&quot;. Esse evento é diferente do evento de visita do painel listado na tabela acima.

Você pode modificar a função scheduleHeartBeatCheck disponível na `/libs/afanalytics/js/custom.js` arquivo para alterar ou interromper esse evento enviado ao Adobe Analytics em um intervalo regular.
