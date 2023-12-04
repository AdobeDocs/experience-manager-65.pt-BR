---
title: Criação e sincronização de Live Copies
description: Saiba como criar e sincronizar Live Copies no Adobe Experience Manager.
feature: Multi Site Manager
exl-id: 896b35dd-4510-4c94-8615-03d9649c2f64
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '4194'
ht-degree: 40%

---

# Criação e sincronização de Live Copies{#creating-and-synchronizing-live-copies}

Você pode criar uma live copy de uma página ou configuração de blueprint e, em seguida, gerenciar a herança e a sincronização.

## Gerenciando configurações de blueprint {#managing-blueprint-configurations}

Uma configuração de blueprint identifica um site existente que você deseja usar como origem para uma ou mais páginas live copy.

>[!NOTE]
>
>As configurações de blueprint permitem enviar alterações de conteúdo para live copies. Consulte [Live Copies - Origem, blueprints e configurações de blueprint](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations).

Ao criar uma configuração de blueprint, você seleciona um modelo que define a estrutura interna do blueprint. O modelo de blueprint padrão presume que o site de origem tem as seguintes características:

* O site tem uma página raiz.
* As páginas secundárias diretas da raiz são ramificações de idioma do site. Ao criar uma live copy, os idiomas são apresentados como conteúdo opcional a ser incluído na cópia.
* A raiz de cada ramificação de idioma tem uma ou mais páginas secundárias. Ao criar uma live copy, as páginas secundárias são apresentadas como capítulos que podem ser incluídos na live copy.

>[!NOTE]
>
>Uma estrutura diferente requer outro modelo de blueprint.

Após criar a configuração de blueprint, configure as seguintes propriedades:

* **Nome**: o nome da configuração de blueprint.
* **Caminho de origem**: o caminho da página raiz do site que você está usando como origem (blueprint).
* **Descrição**. (Opcional) Uma descrição da configuração de blueprint. A descrição é exibida na lista de configurações de blueprint para escolher ao criar um site.

Quando sua configuração de blueprint é usada, você pode associá-la a uma configuração de implantação que determina como as live copies da origem/blueprint são sincronizadas. Consulte [Especificar as configurações de implantação a serem usadas](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use).

### Criação de uma configuração de blueprint {#creating-a-blueprint-configuration}

Para criar uma configuração de blueprint:

1. [Navegue](/help/sites-authoring/basic-handling.md#global-navigation) até o menu **Ferramentas** e, em seguida, selecione o menu **Sites**.
1. Selecione **Blueprints** para abrir o console de **Configurações de blueprint**:

   ![Configurações de blueprint](assets/blueprint-configurations.png)

1. Selecione **Criar**.
1. Selecione o modelo de blueprint e depois selecione **Próximo** para continuar.
1. Selecione a página de origem a ser usada como blueprint; depois, selecione **Próximo** para continuar.
1. Defina:

   * **Título**: título obrigatório para o blueprint
   * **Descrição**: uma descrição opcional para fornecer mais detalhes.

1. **Criar** irá criar a configuração de blueprint com base em sua especificação.

### Editar ou excluir uma configuração de blueprint {#editing-or-deleting-a-blueprint-configuration}

É possível editar ou excluir uma configuração de blueprint existente:

1. [Navegue](/help/sites-authoring/basic-handling.md#global-navigation) até o menu **Ferramentas** e, em seguida, selecione o menu **Sites**.
1. Selecione **Blueprints** para abrir o console de **Configurações de blueprint**:

   ![Configurações de blueprint](assets/blueprint-configurations.png)

1. Selecione a configuração necessária para o blueprint; as ações apropriadas ficarão disponíveis na barra de ferramentas:

   * **Propriedades**; é possível usar essa opção para visualizar e editar as propriedades da configuração.
   * **Excluir**

## Criação de uma Live Copy {#creating-a-live-copy}

### Criação de uma Live Copy de uma página {#creating-a-live-copy-of-a-page}

É possível criar uma Live Copy de qualquer página ou ramificação. Ao criar a live copy, é possível especificar as configurações de implantação a serem usadas para sincronizar o conteúdo:

* As configurações de implantação selecionadas se aplicam à página de live copy e suas páginas secundárias.
* Se você não especificar nenhuma configuração de implantação, o MSM determinará quais configurações de implantação usar. Consulte [Especificação da configuração de implantação a ser usada](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use).

É possível criar uma Live Copy de qualquer página:

* Páginas referenciadas por um [configuração do blueprint](#creating-a-blueprint-configuration).
* E páginas que não têm conexão com uma configuração.
* O AEM também permite criar uma live copy nas páginas de outra live copy.

A única diferença é que a disponibilidade do comando **Implantação** nas páginas de origem/blueprint depende da origem ser ou não referenciada por uma configuração de blueprint:

* Se você criar a live copy a partir de uma página de origem que **é** referenciado em uma configuração de blueprint, o comando Implantação estará disponível nas páginas de origem/blueprint.
* Se você criar a live copy a partir de uma página de origem que **não é** referenciado em uma configuração de blueprint, o comando Implantação não estará disponível nas páginas de origem/blueprint.

Para criar uma live copy:

1. No console do **Sites**, selecione **Criar** e, em seguida, **Live Copy**.

   ![Criar Live Copy](assets/chlimage_1-212.png)

1. Selecione a página de origem e clique em **Próxima**. Por exemplo:

   ![Selecionar página de origem](assets/chlimage_1-213.png)

1. Especifique o caminho de destino da live copy (abra a pasta/página principal da live copy) e clique em **Próxima**.

   ![Especificar destino](assets/chlimage_1-214.png)

   >[!NOTE]
   >
   >O caminho de destino não pode estar dentro do caminho de origem.

1. Insira:

   * um **Título** para a página.
   * um **Nome**, que é usado no URL.

   ![Inserir título e nome](assets/chlimage_1-215.png)

1. Use a caixa de seleção **Excluir subpáginas**:

   * Selecionado: cria uma live copy somente da página selecionada (live copy superficial)
   * Não selecionado: cria uma live copy que inclui todos os descendentes da página selecionada (live copy profunda)

1. (Opcional) Para especificar uma ou mais configurações de implantação a serem usadas para a live copy, use o **Configurações de implantação** para selecioná-las; as configurações selecionadas são mostradas abaixo do seletor suspenso.
1. Clique em **Criar**. Uma mensagem de confirmação será exibida, e daqui será possível selecionar **Abrir** ou **Concluído**.

### Criação de uma Live Copy de um site a partir de uma configuração de blueprint {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

Crie uma live copy usando uma configuração de blueprint para criar um site com base no conteúdo do blueprint (origem). Ao criar uma live copy a partir de uma configuração de blueprint, você seleciona uma ou mais ramificações de idioma para serem copiadas da origem do blueprint e, em seguida, seleciona os capítulos a serem copiados das ramificações de idioma. Consulte [Criação de uma configuração de blueprint](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

Se omitir algumas ramificações de idioma ou capítulos da live copy, você poderá adicioná-los posteriormente; consulte [Criação de uma Live Copy dentro de uma Live Copy (configuração de blueprint)](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration).

>[!CAUTION]
>
>Quando a origem do blueprint contém links e referências que fazem referência a um parágrafo em uma ramificação diferente, os destinos não são atualizados nas páginas live copy, mas permanecem apontando para o destino original.

Ao criar o site, forneça valores para as seguintes propriedades:

* **Idiomas iniciais**: as ramificações de idioma da origem do blueprint a serem incluídas na live copy.
* **Capítulos iniciais**: as páginas secundárias das ramificações de idioma do blueprint a serem incluídas na live copy.
* **Caminho de destino**: o local da página raiz do site de live copy.
* **Título**: o título da página raiz do site de live copy.
* **Nome**: (opcional) o nome do nó JCR que armazena a página raiz da live copy. O valor padrão é baseado no título.
* **Proprietário do site**: (Opcional)
* **Live Copy**: selecione essa opção para estabelecer uma relação dinâmica com o site de origem. Se essa opção não for selecionada, uma cópia do blueprint será criada, mas não será sincronizada com a origem na sequência.
* **Configurações de implantação**: (opcional) selecione uma ou mais configurações de implantação a serem usadas para sincronizar a live copy. Por padrão, as configurações de implantação são herdadas do blueprint; consulte [Especificar as configurações de implantação a serem usadas](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) para obter mais detalhes.

Para criar uma Live Copy de um site a partir de uma configuração de blueprint:

1. No console dos **Sites**, selecione **Criar** e, em seguida, **Site** no seletor da lista suspensa.
1. Selecione a configuração de blueprint a ser usada como origem da live copy e prossiga com **Próxima**:

   ![Selecione a configuração de blueprint como origem da live copy](assets/blueprint-configuration-select.png)

1. Use o **Idiomas iniciais** seletor para especificar os idiomas do site do blueprint a serem usados na live copy.

   Todos os idiomas disponíveis estão selecionados por padrão. Para remover um idioma, clique no link **X** que aparece ao lado do idioma.

   Por exemplo:

   ![Selecionar idiomas iniciais](assets/chlimage_1-217.png)

1. Use o **Capítulos iniciais** para selecionar as seções do blueprint que serão incluídas na live copy. Novamente, todos os capítulos disponíveis são incluídos por padrão, mas podem ser removidos.
1. Forneça valores para as propriedades restantes e selecione **Criar**. Na caixa de diálogo de confirmação, selecione **Concluído** para retornar ao console do **Sites** ou **Abrir site** para abrir a página raiz do site.

### Criação de uma Live Copy dentro de uma Live Copy (configuração do blueprint) {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

Ao criar uma live copy dentro da live copy existente (criada usando uma configuração de blueprint), é possível inserir qualquer cópia de idioma ou capítulos que não foram incluídos quando a live copy foi criada originalmente.

## Monitorar a Live Copy {#monitoring-your-live-copy}

### Visualização do status de uma Live Copy {#seeing-the-status-of-a-live-copy}

As propriedades de uma página de live copy mostram as seguintes informações sobre a live copy:

* **Origem**: a página de origem da página de live copy.
* **Status**: o status de sincronização da live copy. O status inclui se a live copy está atualizada em relação à origem, quando a última sincronização ocorreu e quem executou a sincronização.
* **Configuração**:

   * Se a página ainda está sujeita à herança da Live Copy.
   * Se a configuração é herdada da página principal.
   * Quaisquer configurações de implantação que a live copy usa.

Para exibir as propriedades:

1. No **Sites** selecione a página live copy e abra as propriedades.
1. Selecione a guia **Live Copy**.

   Por exemplo:

   ![Selecionar Live Copy](assets/chlimage_1-218.png)

   >[!NOTE]
   >
   >Para obter mais detalhes, consulte também o artigo da Base de conhecimento [Mensagem de status da Live Copy - Atualizada/Verde/Em sincronia](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

### Visualizar as Live Copies de uma página de blueprint {#seeing-the-live-copies-of-a-blueprint-page}

As páginas de blueprint (referenciadas em uma configuração de blueprint) fornecem uma lista das páginas live copy que usam a página atual (blueprint) como origem. Use esta lista para rastrear as live copies. A lista é exibida na guia **Blueprint** das [propriedades da página](/help/sites-authoring/editing-page-properties.md).

![Guia Blueprint](assets/chlimage_1-219.png)

## Sincronização da Live Copy {#synchronizing-your-live-copy}

### Implantação de um blueprint {#rolling-out-a-blueprint}

Implante uma página de blueprint para enviar alterações de conteúdo para live copies. Uma ação de **Implantação** executa as configurações de implementação que usam acionador [Na implantação](/help/sites-administering/msm-sync.md#rollout-triggers).

>[!NOTE]
>
>Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação dependente da live copy.
>
>Tais [conflitos precisam ser tratados e resolvidos na implantação](/help/sites-administering/msm-rollout-conflicts.md).
>

#### Implantação de um blueprint nas propriedades da página {#rolling-out-a-blueprint-from-page-properties}

1. No console do **Sites**, selecione a página no blueprint e abra as propriedades.
1. Abra a guia **Blueprint.**
1. Selecione **Implantação**.

   ![Selecionar implantação](assets/chlimage_1-220.png)

1. Especifique as páginas e quaisquer subpáginas e, em seguida, confirme com a marca de seleção:

   ![Especificar páginas e subpáginas](assets/chlimage_1-221.png)

1. Especifique se o trabalho de implantação deve ser executado imediatamente (**Agora**) ou em outra data/hora (**Mais tarde**).

   ![Blueprint de implantação](assets/rollout-blueprint.png)

As implantações são processadas como trabalhos assíncronos e podem ser verificadas no [**Status de trabalhos assíncronos** painel](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação global** > **Ferramentas** > **Operações** > **Tarefas**

>[!NOTE]
>
>O processamento assíncrono de implantação requer AEM 6.5.3.0 ou superior. Nas versões anteriores, as páginas eram processadas de forma imediata e síncrona.

#### Implantar um blueprint a partir do painel de referência {#roll-out-a-blueprint-from-the-reference-rail}

1. No console do **Sites**, selecione a página na Live Copy e abra o painel **[Referências](/help/sites-authoring/basic-handling.md#references)** (na barra de ferramentas).
1. Selecione a opção **Blueprint** na lista para mostrar os blueprints associados a esta página.
1. Selecione o blueprint desejado na lista.
1. Clique em **Implantação**.
1. Você receberá uma solicitação para confirmar os detalhes da implantação:

   * **Escopo da implantação**:

     Especifique se o escopo é apenas para a página selecionada ou deve incluir subpáginas.

   * **Programação**:

     Especifique se o trabalho de implantação deve ser executado imediatamente (**Agora**) ou em data/hora posterior (**Mais tarde**).

     ![Especificar o agendamento](assets/rollout-live-copy.png)

1. Depois de confirmar esses detalhes, selecione **Implantação** para executar a ação.

As implantações são processadas como trabalhos assíncronos e podem ser verificadas no [**Status de trabalhos assíncronos** painel](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação global** > **Ferramentas** > **Operações** > **Tarefas**

>[!NOTE]
>
>O processamento assíncrono de implantação requer AEM 6.5.3.0 ou superior. Em versões anteriores, as páginas eram processadas de forma imediata e síncrona, a menos que o **Implantação do plano de fundo** opção foi marcada.

#### Implantar um blueprint a partir de uma visão geral da Live Copy {#roll-out-a-blueprint-from-the-live-copy-overview}

A variável [A ação de implantação também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página do Blueprint é selecionada.

1. Abra a [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma página do blueprint.
1. Selecione **Implantação** na barra de ferramentas.
1. Especifique as páginas e quaisquer subpáginas e, em seguida, confirme com a marca de seleção:

   ![Selecionar as páginas e subpáginas](assets/chlimage_1-223.png)

1. Especifique se o trabalho de implantação deve ser executado imediatamente (**Agora**) ou em outra data/hora (**Mais tarde**).

   ![Blueprint de implantação](assets/rollout-blueprint.png)

As implantações são processadas como trabalhos assíncronos e podem ser verificadas no [**Status de trabalhos assíncronos** painel](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) em **Navegação global** > **Ferramentas** > **Operações** > **Tarefas**

>[!NOTE]
>
>O processamento assíncrono de implantação requer AEM 6.5.3.0 ou superior. Nas versões anteriores, as páginas eram processadas de forma imediata e síncrona.

### Sincronizar uma Live Copy {#synchronizing-a-live-copy}

Sincronize uma página de live copy para extrair as alterações de conteúdo da origem para a live copy.

#### Sincronizar uma Live Copy a partir das propriedades da página {#synchronize-a-live-copy-from-page-properties}

Sincronize uma live copy para extrair as alterações da origem para a live copy.

>[!NOTE]
>
>A sincronização executa as configurações de implantação que usam o acionador [Na implantação](/help/sites-administering/msm-sync.md#rollout-triggers).

1. No **Sites** selecione a página live copy e abra as propriedades.
1. Abra a guia **Live Copy**.
1. Clique em **Sincronizar**.

   ![Sincronizar](assets/chlimage_1-224.png)

   A confirmação será solicitada, use **Sincronizar** para continuar.

#### Sincronizar uma Live Copy a partir da visão geral da Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

A [ação Sincronizar também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página de Live Copy é selecionada.

1. Abra a [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma página de Live Copy.
1. Selecione **Sincronizar** na barra de ferramentas.
1. Confirme a ação de **Implantação** na caixa de diálogo depois de especificar se deseja incluir:

   * **Páginas e subpáginas**
   * **Somente página**

   ![Confirmar implantação](assets/chlimage_1-225.png)

## Alterar conteúdo da Live Copy {#changing-live-copy-content}

Para alterar o conteúdo da live copy, é possível:

* Adicionar parágrafos à página.
* Atualizar o conteúdo existente quebrando a herança da live copy para qualquer página ou componente.

>[!NOTE]
>
>Se você criar manualmente uma página na live copy, ela será local para a live copy, o que significa que não terá uma página de origem correspondente à qual anexar.
>
>A prática recomendada para criar uma página local que faça parte do relacionamento seria criá-la na origem e fazer uma implantação (profunda). Isso criará a página localmente como Live Copies.

>[!NOTE]
>
>Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação dependente da live copy.
>
>Tais [conflitos precisam ser tratados e resolvidos na implantação](/help/sites-administering/msm-rollout-conflicts.md).
>

### Adicionar componentes a uma página de Live Copy {#adding-components-to-a-live-copy-page}

Adicione componentes a uma página de live copy a qualquer momento. O status de herança da live copy e de seu sistema de parágrafo não controla sua capacidade de adicionar componentes.

Quando a página de live copy é sincronizada com a página de origem, os componentes adicionados permanecem inalterados. Consulte também [Alterar a ordem dos componentes em uma página de Live Copy](#changing-the-order-of-components-on-a-live-copy-page).

>[!NOTE]
>
>As alterações feitas localmente em um componente marcado como um contêiner não serão substituídas pelo conteúdo do blueprint em uma implantação. Consulte [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obter mais informações.

### Suspender a herança de uma página {#suspending-inheritance-for-a-page}

Ao criar uma live copy, a configuração da live copy é salva na página raiz das páginas copiadas. Todas as páginas secundárias da página raiz herdam as configurações da live copy. Os componentes nas páginas de live copy também herdam a configuração da live copy.

Você pode suspender a herança da live copy de uma página de live copy para poder alterar as propriedades e os componentes da página. Ao suspender a herança, as propriedades e os componentes da página não são mais sincronizados com a origem.

>[!NOTE]
>
>Também é possível [desanexar uma live copy](#detaching-a-live-copy) do blueprint para remover todas as conexões. A ação Desconectar é permanente e irreversível.

>[!NOTE]
>
>Se o componente estiver marcado como um contêiner, as ações de cancelamento e suspensão não se aplicam aos componentes filho. Consulte também [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obter informações adicionais.

#### Suspensão da herança das propriedades da página {#suspending-inheritance-from-page-properties}

Para suspender a herança em uma página:

1. Abra as propriedades da página de live copy usando o **Propriedades da exibição** comando do **Sites** console ou usando **Informações da página** na barra de ferramentas da página.
1. Clique em **Live Copy** guia.
1. Selecione **Suspender** na barra de ferramentas. Em seguida, é possível selecionar:

   * **Suspender**: somente página atual
   * **Suspender com secundários**: a página atual junto com qualquer página secundária

1. Selecione **Suspender** na caixa de diálogo de confirmação.

#### Suspender a herança na visão geral da Live Copy {#suspending-inheritance-from-the-live-copy-overview}

A [ação Suspender também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página de Live Copy é selecionada.

1. Abra a [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma página de Live Copy.
1. Selecione **Suspender** na barra de ferramentas.
1. Selecione a opção apropriada de:

   * **Suspender**
   * **Suspender com secundários**

   ![Selecione a opção Suspender apropriada](assets/chlimage_1-226.png)

1. Confirme a ação **Suspender** na caixa de diálogo **Suspender Live Copy**:

   ![Suspender ação](assets/chlimage_1-227.png)

### Retomar a herança de uma página {#resuming-inheritance-for-a-page}

Suspender a herança da live copy para uma página é uma ação temporária. Uma vez suspensa, a ação **Retomar** fica disponível, permitindo que você restaure o relacionamento ativo.

Quando você reativa a herança, a página não é sincronizada automaticamente com a origem. Você pode solicitar uma sincronização, se necessário:

* Na caixa de diálogo **Retomar**/**Reverter**; por exemplo:

  ![Retomar ou Reverter](assets/chlimage_1-228.png)

* Em um estágio posterior, selecionando manualmente a ação de sincronização.

>[!CAUTION]
>
>Quando você reativa a herança, a página não é sincronizada automaticamente com a origem. Você pode solicitar manualmente uma sincronização, se necessário; no momento da retomada ou posteriormente.

#### Retomar a herança nas propriedades da página {#resuming-inheritance-from-page-properties}

Uma vez [suspensa](#suspending-inheritance-from-page-properties), a ação **Retomar** fica disponível na barra de ferramentas das propriedades de página:

![Retomar](assets/chlimage_1-229.png)

Quando selecionada, a caixa de diálogo é exibida. Você pode selecionar uma sincronização, se necessário, e confirmar a ação.

#### Retomar uma página de Live Copy na visão geral da Live Copy {#resume-a-live-copy-page-from-the-live-copy-overview}

A [ação Retomar também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página de Live Copy é selecionada.

1. Abra o [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma Página de Live Copy que foi suspensa; ela será exibida como **HERANÇA CANCELADA**.
1. Selecione **Retomar** na barra de ferramentas.
1. Indique se você deseja sincronizar a página após reverter a herança e, em seguida, confirme a ação **Retomar** na caixa de diálogo **Retomar Live Copy**.

### Alterar a profundidade da herança (superficial/profunda) {#changing-inheritance-depth-shallow-deep}

Em uma live copy existente, é possível alterar a profundidade de uma página, ou seja, se as páginas secundárias serão incluídas.

* Alternar para uma live copy superficial:

   * Terá efeito imediato e não será reversível.

      * As páginas secundárias são explicitamente desanexadas da live copy. Modificações posteriores nas páginas secundárias não podem ser preservadas, caso desfeitas.

      * Removerá qualquer `LiveRelationships` descendente, mesmo que haja `LiveCopies` aninhadas.

* Alternar para uma Live Copy profunda:

   * As páginas secundárias permanecem intactas.
   * Para ver o efeito da alteração, é possível fazer uma implantação. Qualquer modificação de conteúdo é aplicada de acordo com a configuração de implantação.

* Alternar para uma live copy superficial e, em seguida, de volta para uma profunda:

   * Todos os filhos da live copy superficial (anterior) são tratados como se tivessem sido criados manualmente e, portanto, são transferidos usando `[oldname]_msm_moved name`.

Para especificar ou alterar a profundidade:

1. Abra as propriedades da página de live copy usando o **Propriedades da exibição** comando do **Sites** console ou usando **Informações da página** na barra de ferramentas da página.
1. Clique em **Live Copy** guia.
1. Na seção **Configuração**, defina ou limpe a opção **Herança da Live Copy** dependendo se as páginas filhas estão incluídas:

   * marcado - uma live copy profunda (as páginas secundárias estão incluídas)
   * clear - uma live copy superficial (páginas secundárias são excluídas)

   >[!CAUTION]
   >
   >Alternar para uma live copy superficial terá efeito imediato e não será reversível.
   >
   >Consulte [Live Copies — Composição](/help/sites-administering/msm.md#live-copies-composition) para obter mais informações.

1. Clique em **Salvar** para continuar com suas atualizações.

### Cancelar herança de um Componente {#cancelling-inheritance-for-a-component}

Cancele a herança da live copy de um componente para que ele não seja mais sincronizado com o componente de origem. Você pode ativar a herança em um ponto posterior, se necessário.

>[!NOTE]
>
>Se o componente estiver marcado como um contêiner, as ações de cancelamento e suspensão não se aplicam aos componentes filho. Consulte também [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obter informações adicionais.

>[!NOTE]
>
>Quando você reativa a herança, o componente não é sincronizado automaticamente com a origem. Você pode solicitar manualmente uma sincronização, se necessário.

Cancelar a herança para alterar o conteúdo do componente ou excluir o componente:

1. Clique no componente para o qual deseja cancelar a herança.

   ![Selecionar componente para cancelar a ação de herança](assets/chlimage_1-230.png)

1. Na barra de ferramentas do componente, clique na guia **Cancelar herança** ícone.

   ![Cancelar herança](do-not-localize/chlimage_1-8.png)

1. Na caixa de diálogo Cancelar herança, confirme a ação com **Sim**.

   A barra de ferramentas do componente é atualizada para incluir todos os comandos de edição (apropriados).

### Ativar novamente a herança de um componente {#re-enabling-inheritance-for-a-component}

Para habilitar a herança de um componente, clique no **Reativar herança** ícone na barra de ferramentas do componente.

![Reativar herança](do-not-localize/chlimage_1-9.png)

### Alterar a ordem dos componentes em uma página de Live Copy {#changing-the-order-of-components-on-a-live-copy-page}

Se uma live copy contiver componentes que fazem parte de um sistema de parágrafo, a herança desse sistema de parágrafo seguirá as seguintes regras:

* A ordem dos componentes em um sistema de parágrafo herdado pode ser modificada, mesmo com a herança estabelecida.
* Na implantação, a ordem dos componentes será restaurada a partir do blueprint. se novos componentes tiverem sido adicionados à live copy antes da implantação, eles serão reorganizados junto com os componentes acima dos quais foram adicionados.
* Se a herança do sistema de parágrafo for cancelada, a ordem dos componentes não será restaurada na implantação e permanecerá como está na live copy.

>[!NOTE]
>
>Ao reverter uma herança cancelada em um sistema de parágrafo, a ordem dos componentes **não será restaurada automaticamente** no blueprint. Você pode solicitar manualmente uma sincronização, se necessário.

Use o procedimento a seguir para cancelar a herança do sistema de parágrafo.

1. Abra a página da live copy.
1. Arraste um componente existente para um novo local na página.
1. Na caixa de diálogo **Cancelar herança**, confirme a ação com **Sim**.

### Substituir as propriedades de uma página de Live Copy {#overriding-properties-of-a-live-copy-page}

As propriedades de página de uma página de Live Copy são herdadas (e não editáveis) da página de origem por padrão.

Você pode cancelar a herança de uma propriedade quando precisar alterar o valor da propriedade para a live copy. Um ícone de link indica que a herança está ativada para a propriedade.

![Cancelar herança da propriedade](assets/chlimage_1-231.png)

Ao cancelar a herança, você pode alterar o valor da propriedade. Um ícone de link quebrado indica que a herança foi cancelada.

![Alterar propriedade quando a herança for quebrada](assets/chlimage_1-232.png)

Posteriormente, você pode reativar a herança de uma propriedade, se necessário.

>[!NOTE]
>
>Quando você reativa a herança, a propriedade da página de live copy não é sincronizada automaticamente com a propriedade de origem. Você pode solicitar manualmente uma sincronização, se necessário.

1. Abra as propriedades da página de live copy usando a tag **Propriedades da exibição** opção do **Sites** console ou **Informações da página** ícone na barra de ferramentas da página.
1. Para cancelar a herança de uma propriedade, clique no ícone de link exibido à direita da propriedade.

   ![Cancelar herança da propriedade](do-not-localize/chlimage_1-10.png)

1. No **Cancelar herança** caixa de diálogo de confirmação, clique **Sim**.

### Reverter propriedades de uma página Live Copy {#revert-properties-of-a-live-copy-page}

Para ativar a herança de uma propriedade, clique no link **Reverter herança** ícone que aparece ao lado da propriedade.

![Reverter herança](do-not-localize/chlimage_1-11.png)

### Redefinir uma página Live Copy {#resetting-a-live-copy-page}

Redefinir uma página de live copy para:

* Remover todos os cancelamentos de herança e
* Retornar a página ao mesmo estado da página de origem.

A redefinição afeta as alterações feitas nas propriedades da página, no sistema de parágrafo e nos componentes.

#### Redefinir uma página Live Copy a partir das propriedades da página {#reset-a-live-copy-page-from-the-page-properties}

1. No **Sites** selecione a página live copy e selecione **Propriedades da exibição**.
1. Abra a guia **Live Copy**.
1. Selecione **Redefinir** na barra de ferramentas.

   ![Redefinir](assets/chlimage_1-233.png)

1. No caixa de diálogo **Redefinir Live Copy**, confirme com **Redefinir**.

#### Redefinir uma página Live Copy a partir da Visão geral da Live Copy {#reset-a-live-copy-page-from-the-live-copy-overview}

A variável [A ação de redefinição também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página de Live Copy é selecionada.

1. Abra a [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma página Live Copy.
1. Selecione **Redefinir** na barra de ferramentas.
1. Confirme a ação **Redefinir** na caixa de diálogo **Redefinir Live Copy**:

   ![Confirmar redefinição](assets/chlimage_1-234.png)

## Comparação de uma página Live Copy com uma página de blueprint {#comparing-a-live-copy-page-with-a-blueprint-page}

Para acompanhar as alterações feitas, é possível exibir a página do blueprint em **Referências** e compare-o com a página da live copy:

1. No **Sites** console, [navegue até uma página de blueprint ou live copy e selecione-a](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra o **[Referências](/help/sites-authoring/basic-handling.md#references)** e selecione:

   * **Blueprint** (quando uma página de live copy é selecionada)
   * **Live Copies** (quando uma página do blueprint é selecionada)

1. Selecione a live copy específica e:

   * **Comparar ao Blueprint** (quando uma página de live copy é selecionada)
   * **Comparar à Live Copy** (quando uma página do blueprint é selecionada)

   Por exemplo:

   ![Comparar](assets/chlimage_1-235.png)

1. As duas páginas (Live Copy e blueprint) serão abertas lado a lado.

   Para obter informações completas sobre como usar este recurso, consulte [Diferencial de página](/help/sites-authoring/page-diff.md).

## Desconectar uma Live Copy {#detaching-a-live-copy}

Desanexar remove permanentemente o relacionamento dinâmico entre uma live copy e sua página de origem/blueprint. Todas as propriedades relevantes ao MSM são removidas da live copy e as páginas da live copy se tornam uma cópia independente.

>[!CAUTION]
>
>Não é possível restabelecer o relacionamento dinâmico após desanexar a live copy.
>
>Para remover o relacionamento dinâmico com a opção de reinstalação posterior, é possível [cancelar herança da live copy](#suspending-inheritance-for-a-page) para a página.

Há implicações com relação ao local na árvore em que você usa **Desanexar**:

* **Desanexar em uma página raiz de uma Live Copy**

  Quando essa operação é executada na página raiz de uma live copy, ela remove o relacionamento dinâmico entre todas as páginas do blueprint e sua live copy.

  Mais alterações em páginas no blueprint (como estava) **não** afetar a livecopy (como estava).

* **Desanexar em uma subpágina de uma Live Copy**

  Quando esta operação é executada em uma subpágina (ou ramificação) dentro de uma live copy:

   * o relacionamento dinâmico é removido dessa subpágina (ou ramificação)
   * e as (sub)páginas na ramificação da live copy são tratadas como se tivessem sido criadas manualmente.

  *No entanto*, as subpáginas ainda estão sujeitas ao relacionamento dinâmico da ramificação principal; portanto, uma nova implantação da(s) página(s) de blueprint irá:

   1. Renomear a(s) página(s) desanexada(s):

      * Isso ocorre porque o MSM as considera como páginas criadas manualmente que causam um conflito, pois têm o mesmo nome das páginas de live copy que ele está tentando criar.

   1. Crie uma página (live copy) com o nome original, contendo as alterações da implantação.

  >[!NOTE]
  >
  >Consulte [Conflitos de implementação do MSM](/help/sites-administering/msm-rollout-conflicts.md) para obter detalhes sobre essas situações.

### Desanexar uma página Live Copy das propriedades da página {#detach-a-live-copy-page-from-the-page-properties}

Para desanexar uma live copy:

1. No **Sites** selecione a página live copy e clique em **Propriedades da exibição**.
1. Abra a guia **Live Copy**.
1. Na barra de ferramentas, selecione **Desanexar**.

   ![Desanexar](assets/chlimage_1-236.png)

1. Uma caixa de diálogo de confirmação é exibida, selecione **Desanexar** para concluir a ação.

### Desconectar uma página de Live Copy da visão geral da Live Copy {#detach-a-live-copy-page-from-the-live-copy-overview}

A [ação de desconectar também está disponível na visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), quando uma página de Live Copy é selecionada.

1. Abra a [Visão geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) e selecione uma página de Live Copy.
1. Selecione **Desconectar** na barra de ferramentas.
1. Confirme a ação **Desconectar** na caixa de diálogo **Desconectar Live Copy**:

   ![Confirmar desanexação](assets/chlimage_1-237.png)
