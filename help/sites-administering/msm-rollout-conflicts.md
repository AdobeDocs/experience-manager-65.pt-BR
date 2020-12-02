---
title: Conflitos de implantação do MSM
seo-title: Conflitos de implantação do MSM
description: Saiba como lidar com conflitos de implementação do Multi Site Manager.
seo-description: Saiba como lidar com conflitos de implementação do Multi Site Manager.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Conflitos de implantação do MSM{#msm-rollout-conflicts}

Os conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação blueprint e em uma ramificação de live copy dependente.

Tais conflitos devem ser tratados e resolvidos aquando da sua implementação.

## Tratamento de conflitos {#conflict-handling}

Quando existem páginas conflitantes (no blueprint e nas ramificações de live copy), o MSM permite que você defina como (ou mesmo se) elas devem ser manipuladas.

Para garantir que a implementação não seja bloqueada, as possíveis definições podem incluir:

* qual página (blueprint ou live copy) terá prioridade durante o lançamento,
* quais páginas serão renomeadas (e como),
* como isso afetará qualquer conteúdo publicado.

   O comportamento padrão da AEM (out-of-the-box) é que o conteúdo publicado não será afetado. Portanto, se uma página que foi criada manualmente na live copy branch tiver sido publicada, esse conteúdo ainda será publicado após o manuseio e a implementação de conflitos.

Além da funcionalidade padrão, os manipuladores de conflitos personalizados podem ser adicionados para implementar regras diferentes. Eles também podem permitir ações de publicação como um processo individual.

### Exemplo de cenário {#example-scenario}

Nas seções a seguir, usamos o exemplo de uma nova página `b`, criada tanto no blueprint quanto na live copy branch (criada manualmente), para ilustrar os vários métodos de resolução de conflitos:

* blueprint: `/b`

   Uma página principal; com 1 página secundária, bp-level-1.

* live copy: `/b`

   Uma página criada manualmente no ramo de live copy; com 1 página secundária, `lc-level-1`.

   * Ativado ao publicar como `/b`, junto com a página secundária.

**Antes da implantação**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint antes do lançamento</strong></td>
   <td><strong>live copy antes do lançamento</strong></td>
   <td><strong>publicar antes da implementação</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (criado na ramificação blueprint, pronto para implantação)<br /> </td>
   <td><code>b</code> <br /> (criado manualmente no ramo de live copy)<br /> </td>
   <td><code>b</code> <br /> (contém o conteúdo da página b que foi criada manualmente na live copy branch)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (criado manualmente no ramo de live copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contém o conteúdo da página<br /> filho-level-1 que foi criado manualmente na ramificação de live copy)</td>
  </tr>
 </tbody>
</table>

## Gerenciador de implantação e tratamento de conflitos {#rollout-manager-and-conflict-handling}

O gerenciador de roll-out permite ativar ou desativar o gerenciamento de conflitos.

Isso é feito usando a [configuração OSGi](/help/sites-deploying/configuring-osgi.md) de **Gerente de Rollout do Day CQ WCM**:

* **Lidar com o conflito com páginas** criadas manualmente:

   ( `rolloutmgr.conflicthandling.enabled`)

   Defina como true se o gerenciador de roll-out deve lidar com conflitos de uma página criada na live copy com um nome que existe no blueprint.

AEM tem [comportamento predefinido quando o gerenciamento de conflitos foi desativado](#behavior-when-conflict-handling-deactivated).

## Manipuladores de conflito {#conflict-handlers}

AEM usa manipuladores de conflitos para resolver quaisquer conflitos de página que existam ao implantar conteúdo de um blueprint em uma live copy. Renomear páginas é um método (o normal) para resolver esses conflitos. Mais de um manipulador de conflitos pode estar operacional para permitir uma seleção de comportamentos diferentes.

AEM fornece:

* O [processador de conflitos padrão](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* A possibilidade de implementar um [processador personalizado](#customized-handlers).
* O mecanismo de classificação de serviço que permite definir a prioridade de cada manipulador individual. O serviço com a classificação mais alta é usado.

### Manipulador de conflitos padrão {#default-conflict-handler}

O manipulador de conflitos padrão:

* É chamado de `ResourceNameRolloutConflictHandler`

* Com esse manipulador, a página de blueprint tem prioridade.
* A classificação de serviço para este manipulador está definida como baixa ( &quot;ou seja, abaixo do valor padrão para a propriedade `service.ranking`), pois presume-se que os manipuladores personalizados precisarão de uma classificação mais alta. No entanto, a classificação não é o mínimo absoluto para garantir flexibilidade quando necessário.

Este manipulador de conflitos dá prioridade ao projeto. A página live copy `/b` é movida (dentro da ramificação live copy) para `/b_msm_moved`.

* live copy: `/b`

   É movido (dentro da live copy) para `/b_msm_moved`. Isso funciona como um backup e garante que nenhum conteúdo seja perdido.

   * `lc-level-1` não é movido.

* blueprint: `/b`

   É lançado para a página de live copy `/b`.

   * `bp-level-1` é distribuída para a livecopy.

**Depois da implantação**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint após o lançamento</strong></td>
   <td><strong>live copy após o lançamento</strong><br /> </td>
   <td></td>
   <td><strong>live copy após o lançamento</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após a implementação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (tem o conteúdo da página de blueprint b que foi distribuída)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (tem o conteúdo da página b que foi criado manualmente na live copy branch)</td>
   <td><code>b</code> <br /> (sem alterações; contém o conteúdo da página original b que foi criada manualmente na ramificação da live copy e agora é chamada de b_msm_move)<br /> </td>
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

Os manipuladores de conflitos personalizados permitem que você implemente suas próprias regras. Usando o mecanismo de classificação de serviço, também é possível definir como eles interagem com outros manipuladores.

Os manipuladores de conflitos personalizados podem:

* Seja nomeado de acordo com seus requisitos.
* Ser desenvolvido/configurado de acordo com seus requisitos; por exemplo, você pode desenvolver um manipulador para que a página de cópia online tenha prioridade.
* Pode ser projetado para ser configurado usando a configuração [OSGi](/help/sites-deploying/configuring-osgi.md); nomeadamente:

   * **Classificação** do serviço:

      Define a ordem relacionada a outros manipuladores de conflito ( `service.ranking`).

      O valor padrão é 0.

### Comportamento ao lidar com conflitos desativado {#behavior-when-conflict-handling-deactivated}

Se você desativar manualmente [a manipulação de conflitos](#rollout-manager-and-conflict-handling), AEM não executará nenhuma ação em nenhuma página conflitante (as páginas não conflitantes são implantadas conforme esperado).

>[!CAUTION]
>
>AEM não fornece nenhuma indicação de que os conflitos estão sendo ignorados, pois esse comportamento deve ser configurado explicitamente, portanto, presume-se que seja o comportamento necessário.

Nesse caso, a live copy tem prioridade efetiva. A página de blueprint `/b` não é copiada e a página de live copy `/b` fica intocada.

* blueprint: `/b`

   Não é copiado, mas é ignorado.

* live copy: `/b`

   Continua o mesmo.

<table>
 <caption>
   Depois da implantação
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint após o lançamento</strong></td>
   <td><strong>live copy após o lançamento</strong><br /> <br /> <br /> </td>
   <td><strong>publicar após a implementação</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (sem alterações; tem o conteúdo da página b que foi criada manualmente na live copy branch)</td>
   <td><code>b</code> <br /> (sem alterações; contém o conteúdo da página b que foi criada manualmente na live copy branch)<br /> </td>
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
