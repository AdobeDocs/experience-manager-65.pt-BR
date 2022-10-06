---
title: Personalização do rastreamento de eventos de formulário
seo-title: Customizing form event tracking
description: Se um usuário gastar mais de 60 segundos em um campo, um evento de visita de campo é acionado e os detalhes do campo são enviados para a Adobe SiteCatalyst.
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

# Personalização do rastreamento de eventos de formulário {#customizing-form-event-tracking}

Imediatamente, os seguintes eventos são rastreados em um Formulário adaptável habilitado para análise:

<table>
 <tbody>
  <tr>
   <th>Evento</th>
   <th>Variáveis disponíveis</th>
  </tr>
  <tr>
   <td>renderizar</td>
   <td>formName, formTitle, formInstance, fonte</td>
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
   <td>formName, formTitle, formInstance, fonte</td>
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

## Personalização do campo Tempo limite do evento de visita {#customizing-the-field-visit-event-timeout}

Na configuração padrão AEM formulário, se um usuário gastar mais de 60 segundos em um campo, uma `fieldvisit` é acionado e os detalhes do campo são enviados para o Adobe Analytics. Você pode personalizar a linha de base de Rastreamento de tempo do campo em Configuração do AEM Forms Analytics em AEM console Configuração (/system/console/configMgr) para aumentar ou diminuir o tempo limite.

## Personalização dos eventos de rastreamento {#customizing-the-tracking-events}

Você pode modificar o `trackEvent`função disponível em `/libs/afanalytics/js/custom.js` para personalizar o rastreamento de eventos. Sempre que um evento que está sendo rastreado ocorrer em um formulário adaptável, a variável `trackEvent`é chamada. O `trackEvent` aceita dois parâmetros: `eventName`e `variableValueMap`.

Você pode avaliar o valor de *eventName* e *variableValueMap* argumentos para alterar o comportamento de rastreamento dos eventos. Por exemplo, você pode optar por enviar as informações para o servidor do Analytics depois que ocorrer um determinado número de eventos de erro. Você também pode optar por executar qualquer uma das seguintes personalizações:

* Você pode definir um tempo limite antes de enviar o evento.
* É possível manter um estado para decidir a ação, por exemplo, *fieldVisit* envia um evento fictício com base no carimbo de data e hora do último evento.
* Você pode usar o `pushEvent` para enviar o evento para o servidor do analytics *.*

* Você pode optar por não enviar o evento para o servidor do Analytics.

### Amostra {#sample}

No exemplo a seguir, estado para a variável *erro* de cada *fieldName* for mantido. O evento é enviado para o servidor do Analytics somente se ocorrer um erro novamente.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalização do evento panelvisit {#customizing-the-panelvisit-event}

Na configuração padrão do AEM Forms, após cada 60 segundos, é verificado se a janela que contém o formulário adaptável está ativa. Se a janela estiver ativa, uma `panelVisit`é acionado para Adobe Analytics. Ajuda a determinar se o documento ou o formulário está ativo e a calcular o tempo gasto no formulário ou documento correspondente.

>[!NOTE]
>
>O nome do evento usado para determinar a atividade e calcular o tempo gasto é &quot;panelVisit&quot;. Esse evento é diferente do evento de visita do painel listado na tabela listada acima.

Você pode modificar a função scheduleHeartBeatCheck disponível na variável `/libs/afanalytics/js/custom.js` para alterar ou parar o evento enviado para a Adobe Analytics em um intervalo regular.
