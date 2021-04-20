---
title: Conflitos de implementação do MSM
seo-title: Conflitos de implementação do MSM
description: Saiba como lidar com conflitos de implementação do Multi Site Manager.
seo-description: Saiba como lidar com conflitos de implementação do Multi Site Manager.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# Conflitos de implementação do MSM{#msm-rollout-conflicts}

Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação de live copy dependente.

Tais conflitos devem ser tratados e resolvidos aquando da sua implantação.

## Tratamento de conflitos {#conflict-handling}

Quando páginas conflitantes existem (no blueprint e nas ramificações de live copy), o MSM permite definir como (ou mesmo se) elas devem ser tratadas.

Para garantir que a implantação não seja bloqueada, as possíveis definições podem incluir:

* qual página (blueprint ou live copy) terá prioridade durante a implantação,
* quais páginas serão renomeadas (e como),
* como isso afetará qualquer conteúdo publicado.

   O comportamento padrão do AEM (pronto para uso) é que o conteúdo publicado não será afetado. Portanto, se uma página que foi criada manualmente na ramificação da live copy tiver sido publicada, esse conteúdo ainda será publicado após a manipulação e implantação do conflito.

Além da funcionalidade padrão, os manipuladores de conflito personalizados podem ser adicionados para implementar regras diferentes. Isso também pode permitir a publicação de ações como um processo individual.

### Exemplo de cenário {#example-scenario}

Nas seções a seguir, usamos o exemplo de uma nova página `b`, criada tanto no blueprint quanto na ramificação da live copy (criada manualmente), para ilustrar os vários métodos de resolução de conflitos:

* blueprint: `/b`

   Uma página principal; com 1 página secundária, nível bp-1.

* live copy: `/b`

   Uma página criada manualmente na ramificação da live copy; com uma página filho, `lc-level-1`.

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
   <td><code>b</code> <br /> (criado na ramificação do blueprint, pronto para implantação)<br /> </td>
   <td><code>b</code> <br /> (criado manualmente na ramificação da live copy)<br /> </td>
   <td><code>b</code> <br /> (contém o conteúdo da página b que foi criada manualmente na ramificação da live copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (criado manualmente na ramificação da live copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contém o conteúdo da página<br /> nível-filho-1 que foi criada manualmente na ramificação da live copy)</td>
  </tr>
 </tbody>
</table>

## Gerenciador de implantação e tratamento de conflito {#rollout-manager-and-conflict-handling}

O gerenciador de implementação permite ativar ou desativar o gerenciamento de conflitos.

Isso é feito usando a [configuração OSGi](/help/sites-deploying/configuring-osgi.md) de **Gerenciador de implementação do WCM CQ do dia**:

* **Lidar com conflito com páginas** criadas manualmente:

   ( `rolloutmgr.conflicthandling.enabled`)

   Defina como true se o gerenciador de implementação deve lidar com conflitos de uma página criada na live copy com um nome que existe no blueprint.

AEM tem [comportamento predefinido quando o gerenciamento de conflitos foi desativado](#behavior-when-conflict-handling-deactivated).

## Manipuladores de conflito {#conflict-handlers}

O AEM usa manipuladores de conflitos para resolver quaisquer conflitos de página que existam ao implantar conteúdo de um blueprint em uma live copy. A renomeação de páginas é um método (o usual) para resolver esses conflitos. Mais de um manipulador de conflitos pode ser operacional para permitir uma seleção de comportamentos diferentes.

AEM fornece:

* O [manipulador de conflitos padrão](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* A possibilidade de implementar um [manipulador personalizado](#customized-handlers).
* O mecanismo de classificação de serviço que permite definir a prioridade de cada manipulador individual. O serviço com a classificação mais alta é usado.

### Manipulador de conflito padrão {#default-conflict-handler}

O manipulador de conflitos padrão:

* É chamado de `ResourceNameRolloutConflictHandler`

* Com esse manipulador, a página do blueprint recebe prioridade.
* A classificação de serviço desse manipulador é definida como baixa ( &quot;ou seja, abaixo do valor padrão da propriedade `service.ranking`), pois a suposição é que os manipuladores personalizados precisarão de uma classificação mais alta. No entanto, a classificação não é o mínimo absoluto para garantir a flexibilidade quando necessário.

Esse manipulador de conflitos dá prioridade ao blueprint. A página de Live Copy `/b` é movida (dentro da ramificação da Live Copy) para `/b_msm_moved`.

* live copy: `/b`

   É movido (dentro da live copy) para `/b_msm_moved`. Isso funciona como um backup e garante que nenhum conteúdo seja perdido.

   * `lc-level-1` não é movido.

* blueprint: `/b`

   É implantado na página de Live Copy `/b`.

   * `bp-level-1` é distribuída para a livecopy.

**Após a implantação**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint após a implantação</strong></td>
   <td><strong>live copy após a implantação</strong><br /> </td>
   <td></td>
   <td><strong>live copy após a implantação</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após a implantação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (tem o conteúdo da página de blueprint b que foi implementada)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (tem o conteúdo da página b que foi criada manualmente na ramificação da live copy)</td>
   <td><code>b</code> <br /> (sem alterações; contém o conteúdo da página original b que foi criada manualmente na ramificação da live copy e agora é chamada de b_msm_moved)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (sem alterações)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (sem alterações)</td>
  </tr>
 </tbody>
</table>

### Manipuladores personalizados {#customized-handlers}

Os manipuladores de conflito personalizados permitem que você implemente suas próprias regras. Usando o mecanismo de classificação de serviço, você também pode definir como eles interagem com outros manipuladores.

Os manipuladores de conflitos personalizados podem:

* Seja nomeado de acordo com suas necessidades.
* Ser desenvolvido/configurado de acordo com suas necessidades; por exemplo, você pode desenvolver um manipulador para que a página de Live Copy tenha prioridade.
* Pode ser projetado para ser configurado usando a configuração [OSGi](/help/sites-deploying/configuring-osgi.md); em especial:

   * **Classificação** do serviço:

      Define a ordem relacionada a outros manipuladores de conflito ( `service.ranking`).

      O valor padrão é 0.

### Comportamento ao lidar com conflitos desativado {#behavior-when-conflict-handling-deactivated}

Se você desativar manualmente [a manipulação de conflitos](#rollout-manager-and-conflict-handling) então AEM não executa nenhuma ação em quaisquer páginas conflitantes (páginas não conflitantes são implantadas conforme esperado).

>[!CAUTION]
>
>AEM não fornece qualquer indicação de que os conflitos estão sendo ignorados, pois esse comportamento deve ser configurado explicitamente, portanto, presume-se que é o comportamento necessário.

Nesse caso, a live copy tem prioridade. A página do blueprint `/b` não é copiada e a página da live copy `/b` é deixada intocada.

* blueprint: `/b`

   Não é copiado, mas é ignorado.

* live copy: `/b`

   Fica igual.

<table>
 <caption>
   Após a implantação
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint após a implantação</strong></td>
   <td><strong>live copy após a implantação</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após a implantação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (sem alterações; tem o conteúdo da página b que foi criada manualmente na ramificação da live copy)</td>
   <td><code>b</code> <br /> (sem alterações; contém o conteúdo da página b que foi criada manualmente na ramificação da live copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (sem alterações)</td>
   <td><code> /lc-level-1</code> <br /> (sem alterações)</td>
  </tr>
 </tbody>
</table>

### Classificações de serviço {#service-rankings}

A classificação de serviço [OSGi](https://www.osgi.org/) pode ser usada para definir a prioridade de manipuladores de conflito individuais.
