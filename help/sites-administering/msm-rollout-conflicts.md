---
title: Conflitos de implantação do MSM
description: Saiba como lidar com conflitos de implementação do Multi Site Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 22%

---

# Conflitos de implantação do MSM{#msm-rollout-conflicts}

Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação dependente da live copy.

Esses conflitos devem ser tratados e resolvidos na implantação.

## Tratamento de conflitos {#conflict-handling}

Quando páginas conflitantes existem (nas ramificações do blueprint e da live copy), o MSM permite definir como (ou mesmo se) elas devem ser tratadas.

Para garantir que a implantação não seja bloqueada, as possíveis definições podem incluir:

* qual página (blueprint ou live copy) tem prioridade durante a implantação,
* quais páginas são renomeadas (e como),
* como isso afeta qualquer conteúdo publicado.

  O comportamento padrão do Adobe Experience Manager (AEM) (pronto para uso) é que o conteúdo publicado não é afetado. Portanto, se uma página que foi criada manualmente na ramificação da live copy tiver sido publicada, esse conteúdo ainda será publicado após o tratamento do conflito e a implantação.

Além da funcionalidade padrão, os manipuladores de conflito personalizados podem ser adicionados para implementar regras diferentes. Eles também podem permitir a publicação de ações como um processo individual.

### Exemplo de cenário {#example-scenario}

Nas seções a seguir, você deve usar o exemplo de uma nova página `b`, criado na ramificação do blueprint e da live copy (criado manualmente), para ilustrar os vários métodos de resolução de conflitos:

* blueprint: `/b`

  Uma página principal; com uma página secundária, bp-level-1.

* live copy: `/b`

  Uma página criada manualmente na ramificação da live copy; com uma página secundária, `lc-level-1`.

   * Ativado ao publicar como `/b`, junto com a página secundária.

**Antes da implantação**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint antes da implantação</strong></td>
   <td><strong>live copy antes da implantação</strong></td>
   <td><strong>publicar antes da implantação</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (criado na ramificação do blueprint, pronto para implantação)<br /> </td>
   <td><code>b</code><br /> <br /> (criado manualmente na ramificação da live copy)<br /> </td>
   <td><code>b</code><br /> <br /> (contém o conteúdo da página b que foi criado manualmente na ramificação da live copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (criado manualmente na ramificação da live copy)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (contém o conteúdo da página)<br /> nível secundário-1 que foi criado manualmente na ramificação da live copy)</td>
  </tr>
 </tbody>
</table>

## Gerenciador de implantação e tratamento de conflito {#rollout-manager-and-conflict-handling}

O gerenciador de implantação permite ativar ou desativar o gerenciamento de conflitos.

Isso é feito usando o [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) de **Gerente de implantação do WCM CQ do dia**:

* **Lidar com conflitos com páginas criadas manualmente**:

  ( `rolloutmgr.conflicthandling.enabled`)

  Definido como verdadeiro se o gerenciador de implantação deve lidar com conflitos de uma página criada na live copy com um nome que existe no blueprint.

O AEM tem [comportamentos predefinidos quando o gerenciamento de conflitos foi desativado](#behavior-when-conflict-handling-deactivated).

## Manipuladores de conflito {#conflict-handlers}

O AEM usa manipuladores de conflito para resolver quaisquer conflitos de página que existam ao implantar conteúdo de um blueprint em uma live copy. A renomeação de páginas é um dos métodos (comuns) para resolver esses conflitos. Mais de um manipulador de conflitos pode estar operacional para permitir uma seleção de comportamentos diferentes.

O AEM fornece:

* O [manipulador de conflitos padrão](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* A possibilidade de implementar um [manipulador personalizado](#customized-handlers).
* O mecanismo de classificação de serviço que permite definir a prioridade de cada manipulador individual. O serviço com a classificação mais alta é usado.

### Manipulador de conflito padrão {#default-conflict-handler}

O manipulador de conflitos padrão:

* É chamado `ResourceNameRolloutConflictHandler`

* Com esse manipulador, a página do blueprint recebe prioridade.
* A classificação de serviço para esse manipulador é definida como baixa (ou seja, abaixo do valor padrão para o `service.ranking` propriedade ), pois a suposição é que os manipuladores personalizados precisam de uma classificação mais alta. No entanto, a classificação não é o mínimo absoluto para garantir flexibilidade quando necessária.

Esse manipulador de conflitos dá prioridade ao blueprint. A página da live copy `/b` é movido (dentro da ramificação da live copy) para `/b_msm_moved`.

* live copy: `/b`

  É movido (dentro da live copy) para `/b_msm_moved`. Isso funciona como um backup e garante que nenhum conteúdo seja perdido.

   * `lc-level-1` não é movido.

* blueprint: `/b`

  É implantado na página da live copy `/b`.

   * `bp-level-1` é implantado na live copy.

**Após a implantação**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint após implantação</strong></td>
   <td><strong>live copy após a implantação</strong><br /> </td>
   <td></td>
   <td><strong>live copy após a implantação</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após implantação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (tem o conteúdo da página b do blueprint que foi implantado)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (tem o conteúdo da página b que foi criado manualmente na ramificação da live copy)</td>
   <td><code>b</code><br /> <br /> (sem alterações; contém o conteúdo da página original b que foi criado manualmente na ramificação da live copy e agora é chamado de b_msm_moved)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (sem alteração)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (sem alteração)</td>
  </tr>
 </tbody>
</table>

### Manipuladores personalizados {#customized-handlers}

Os manipuladores de conflito personalizados permitem que você implemente suas próprias regras. Usando o mecanismo de classificação de serviço, você também pode definir como eles interagem com outros manipuladores.

Os manipuladores de conflito personalizados podem ter o seguinte:

* Nomeado de acordo com suas necessidades.
* Desenvolvido/configurado de acordo com seus requisitos; por exemplo, você pode desenvolver um manipulador para que a página da Live Copy tenha prioridade.
* Projetado para ser configurado usando o [Configuração OSGi](/help/sites-deploying/configuring-osgi.md)em especial:

   * **Classificação do serviço**:

     Define a ordem relacionada a outros manipuladores de conflito ( `service.ranking`).

     O valor padrão é 0.

### Comportamento quando o manuseio de conflitos é desativado {#behavior-when-conflict-handling-deactivated}

Se você [desativar tratamento de conflitos](#rollout-manager-and-conflict-handling), o AEM não executa nenhuma ação em páginas conflitantes (as páginas não conflitantes são implantadas conforme esperado).

>[!CAUTION]
>
>O AEM não dá nenhuma indicação de que os conflitos estão sendo ignorados, pois esse comportamento deve ser configurado explicitamente, portanto, presume-se que seja o comportamento necessário.

Nesse caso, a live copy tem prioridade efetiva. A página do blueprint `/b` não é copiado e a página da live copy `/b` é deixada intocada.

* blueprint: `/b`

  Não é copiado, mas é ignorado.

* live copy: `/b`

  O mesmo.

<table>
 <caption>
   Após a implantação
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint após implantação</strong></td>
   <td><strong>live copy após a implantação</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após implantação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (sem alterações; tem o conteúdo da página b que foi criado manualmente na ramificação da live copy)</td>
   <td><code>b</code><br /> <br /> (sem alterações; contém o conteúdo da página b que foi criado manualmente na ramificação da live copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (sem alteração)</td>
   <td><code> /lc-level-1</code><br /> <br /> (sem alteração)</td>
  </tr>
 </tbody>
</table>

### Classificações de serviço {#service-rankings}

A classificação de serviço do [OSGi](https://www.osgi.org/) pode ser usada para definir a prioridade de manipuladores de conflito individuais.
