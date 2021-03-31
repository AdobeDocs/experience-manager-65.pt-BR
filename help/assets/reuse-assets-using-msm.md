---
title: Reutilizar ativos usando o MSM
description: Use ativos em várias páginas/pastas que são derivadas de e vinculadas a ativos principais. Os ativos permanecem sincronizados com uma cópia principal e, com alguns cliques, recebem as atualizações dos ativos principais.
contentOwner: AG
mini-toc-levels: 1
role: Profissional de negócios, Administrador, Arquiteto
feature: Gerenciamento de ativos, Gerenciador de vários sites
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '3375'
ht-degree: 9%

---


# Reutilizar ativos usando MSM para [!DNL Assets] {#reuse-assets-using-msm-for-assets}

A funcionalidade MSM (Multi Site Manager) em [!DNL Adobe Experience Manager] permite que os usuários reutilizem conteúdo criado uma vez e reutilizado em vários locais da Web. O mesmo está disponível para ativos digitais que o MSM para a funcionalidade [!DNL Assets]. Usando o MSM para [!DNL Assets], você pode:

* Crie ativos uma vez e faça cópias desses ativos para reutilização em outras áreas do site.
* Mantenha várias cópias sincronizadas e atualize a cópia principal original uma vez para enviar as alterações para as cópias secundárias.
* Faça alterações locais suspendendo temporária ou permanentemente a vinculação entre ativos pai e filho.

## Pré-requisitos {#prereq}

Para usar o MSM para [!DNL Assets], instale pelo menos [!DNL Experience Manager] 6.5 Service Pack 1. Para obter mais informações, consulte [as notas de versão do service pack mais recente](/help/release-notes/sp-release-notes.md).

## Entenda os benefícios e os conceitos {#concepts}

### Como funciona e os benefícios {#how-it-works-and-the-benefits}

Para entender os cenários de uso para reutilizar o mesmo conteúdo (texto e ativos) em vários locais da Web, consulte [possíveis cenários MSM](/help/sites-administering/msm.md). [!DNL Experience Manager] O mantém um link entre o ativo original e suas cópias vinculadas, chamadas de cópias em tempo real (LCs). A vinculação mantida permite que alterações centralizadas sejam enviadas para muitas cópias ativas. Isso permite atualizações mais rápidas, além de eliminar as limitações do gerenciamento de cópias duplicadas. A propagação das alterações é livre de erros e centralizada. A funcionalidade permite espaço para atualizações limitadas a cópias dinâmicas selecionadas. Os usuários podem desconectar a vinculação, ou seja, interromper a herança e fazer edições locais que não são substituídas quando a próxima vez que a cópia principal for atualizada e as alterações forem implementadas. A desanexação pode ser feita para alguns campos de metadados selecionados ou para um ativo inteiro. Ele permite flexibilidade para atualizar localmente ativos que são herdados originalmente de uma cópia primária.

O MSM mantém um relacionamento dinâmico entre o ativo de origem e suas cópias ativas, de modo que:

* As alterações nos ativos de origem são aplicadas (distribuídas) às cópias em tempo real, ou seja, as cópias em tempo real são sincronizadas com a fonte.
* Você pode atualizar as cópias ao vivo suspendendo o relacionamento ao vivo ou remover a herança de alguns campos limitados. As modificações na origem não são mais aplicadas à live copy.

### Glossário de MSM para termos [!DNL Assets] {#glossary}

**Fonte:** os ativos ou pastas originais. Cópia primária da qual são derivadas cópias dinâmicas.

**Live Copy:** a cópia dos ativos/pastas de origem que está em sincronização com sua origem. As cópias em tempo real podem ser uma fonte de outras cópias em tempo real. Consulte como criar LCs.

**Herança:** um link/referência entre um ativo/pasta de live copy e sua origem que o sistema usa para lembrar onde enviar as atualizações. A herança existe em um nível granular para campos de metadados. A herança pode ser removida para campos de metadados seletivos, preservando ao mesmo tempo a relação dinâmica entre a origem e sua live copy.

**Implantação:** uma ação que envia as modificações feitas à fonte downstream para suas cópias ativas. É possível atualizar uma ou mais cópias ativas de uma só vez usando a ação de implantação. Consulte implantação.

**Configuração de implantação:** regras que determinam quais propriedades são sincronizadas, como e quando. Essas configurações são aplicadas ao criar cópias ativas; pode ser editado posteriormente; e um filho pode herdar a configuração de implementação de seu ativo pai. Para MSM para [!DNL Assets], use apenas a configuração de implementação Padrão. As outras configurações de implementação não estão disponíveis para o MSM para [!DNL Assets].

**Sincronizar:** outra ação, além da implantação, que oferece paridade entre a origem e a live copy, enviando as atualizações da origem para as live copies. Uma sincronização é iniciada para uma determinada live copy e a ação extrai as alterações da origem. Com essa ação, é possível atualizar apenas uma das cópias ativas. Consulte sincronizar ação.

**Suspender:** Remova temporariamente a relação ativa entre uma live copy e seu ativo/pasta de origem. Você pode retomar o relacionamento. Consulte suspender ação.

**Retomar:** Retome o relacionamento dinâmico para que uma live copy comece a receber as atualizações da origem. Consulte retomar ação.

**Redefinir: a ação** Redefinir torna a Live Copy novamente uma réplica da origem, substituindo todas as alterações locais. Ele também remove cancelamentos de herança e redefine a herança em todos os campos de metadados. Para fazer modificações locais no futuro, você deve cancelar novamente a herança de campos específicos. Consulte modificações locais no LC.

**Desanexar:** remova irrevogavelmente a relação ativa de um ativo/pasta de live copy. Após a ação de desanexação, as cópias em tempo real nunca poderão receber atualizações da origem e não serão mais uma live copy. Consulte remover relacionamento.

## Criar uma live copy de um ativo {#createlc}

Para criar uma live copy a partir de um ou mais ativos ou pastas de origem, siga um destes procedimentos:

* Método 1: Selecione os ativos de origem e clique em **[!UICONTROL Criar]** > **[!UICONTROL Live Copy]** na barra de ferramentas na parte superior.
* Método 2: Na interface do usuário [!DNL Experience Manager], clique em **[!UICONTROL Criar]** > **[!UICONTROL Live Copy]** no canto superior direito da interface.

Você pode criar cópias ativas de um ativo ou uma pasta, uma de cada vez. Você pode criar cópias ativas derivadas de um ativo ou de uma pasta que seja uma live copy propriamente dita. Fragmentos de conteúdo (CFs) não são compatíveis com o caso de uso. Ao tentar criar suas cópias ao vivo, os CFs são copiados como estão sem nenhum relacionamento. Os CFs copiados são um instantâneo no tempo e não são atualizados quando os CFs originais são atualizados.

Para criar cópias ativas usando o primeiro método, siga estas etapas:

1. Selecione ativos ou pastas de origem. Na barra de ferramentas, clique em **[!UICONTROL Create]** > **[!UICONTROL Live Copy]**.

   ![Criar Live Copy na  [!DNL Experience Manager] interface](assets/create_lc1.png)

   *Figura: Crie uma live copy a partir da  [!DNL Experience Manager] interface.*

1. Selecione uma pasta de destino. Clique em **[!UICONTROL Avançar]**.
1. Forneça o título e o nome. Os ativos não têm filhos. Ao criar uma live copy de pastas, você pode optar por incluir ou excluir filhos.
1. Selecione uma configuração de implementação. Clique em **[!UICONTROL Criar]**.

Para criar cópias ativas usando o segundo método, siga estas etapas:

1. Na interface [!DNL Experience Manager], no canto superior direito, clique em **[!UICONTROL Criar]** > **[!UICONTROL Live Copy]**.

   ![Criar Live Copy na  [!DNL Experience Manager] interface](assets/create_lc2.png)

   *Figura: Crie uma live copy a partir da  [!DNL Experience Manager] interface.*

1. Selecione o ativo ou a pasta de origem. Clique em **[!UICONTROL Avançar]**.
1. Selecione a pasta de destino. Clique em **[!UICONTROL Avançar]**.
1. Forneça o título e o nome. Os ativos não têm filhos. Ao criar uma live copy de pastas, você pode optar por incluir ou excluir filhos.
1. Selecione uma configuração de implementação. Clique em **[!UICONTROL Criar]**.

>[!NOTE]
>
>Quando uma origem ou uma live copy é movida, os relacionamentos são retidos. Quando uma live copy é excluída, os relacionamentos são removidos.

## Exibir várias propriedades e status de origem e Live Copy {#properties}

Você pode exibir as informações e os status relacionados ao MSM da live copy, como relacionamento, sincronização, implantações e muito mais, das várias áreas da interface do usuário [!DNL Experience Manager].

Os dois métodos a seguir funcionam para ativos e pastas:

* Selecione o ativo de live copy e localize as informações na página Propriedades.
* Selecione a pasta de origem e localize as informações detalhadas de cada live copy a partir do [!UICONTROL Console da Live Copy].

>[!TIP]
>
>Para verificar o status de algumas live copies separadas, use o primeiro método para verificar a página **[!UICONTROL Properties]**. Para verificar os status de muitas cópias ativas, use o segundo método para verificar a página **[!UICONTROL Status do relacionamento]**.

### Informações e status de uma live copy {#statuslcasset}

Para verificar as informações e os status de um ativo de live copy ou de uma pasta, siga essas etapas.

1. Selecione um ativo de live copy ou uma pasta. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Como alternativa, use o atalho de teclado `p`.
1. Clique em **[!UICONTROL Live Copy]**. Você pode verificar o caminho da origem, status da suspensão, status da sincronização, data da última implantação e o usuário que fez a última implantação.

   ![As informações e os status da Live Copy são exibidos em um console nas Propriedades](assets/lcfolder_info_properties.png)

   *Figura: Informações e status da Live Copy.*

1. Você pode ativar ou desativar se os ativos filho pegarem a configuração da live copy emprestada.

1. Você pode escolher a opção da live copy para herdar a configuração de implementação do pai ou alterar a configuração.

### Informações e status de todas as cópias ativas de uma pasta {#status-lc-folder}

[!DNL Experience Manager] O fornece um console para verificar as estátuas de todas as live copies de uma pasta de origem. Esse console exibe o status de todos os ativos secundários.

1. Selecione uma pasta de origem. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Como alternativa, use o atalho de teclado `p`.
1. Clique em **[!UICONTROL Origem da Live Copy]**. Para abrir o console, clique em **[!UICONTROL Visão geral da Live Copy]**. Esse painel fornece um status de nível superior de todos os ativos secundários.

   ![Exibir status de cópias ativas no Console da Live Copy de origem](assets/livecopy-statuses.png)

   *Figura: Exibir status de cópias ativas no  [!UICONTROL Live Copy ] Consoleof source.*

1. Para exibir as informações detalhadas sobre cada ativo na pasta live copy, selecione um ativo e clique em **[!UICONTROL Status do relacionamento]** na barra de ferramentas.

   ![Informações detalhadas e status de um ativo filho de live copy em uma pasta](assets/livecopy_relationship_status.png)

   Informações detalhadas e status de um ativo filho de live copy em uma pasta

>[!TIP]
>
>Você pode ver rapidamente os status de cópias ativas de outras pastas sem precisar navegar muito. Altere a pasta da parte média superior da interface **[!UICONTROL Visão geral da Live Copy]**.

### Ações rápidas do painel Referências para a origem {#refrailsource}

Para um ativo ou pasta de origem, você pode ver as seguintes informações e realizar as seguintes ações diretamente do painel Referências :

* Veja os caminhos das cópias dinâmicas.
* Abra ou revele uma live copy específica na interface do usuário [!DNL Experience Manager].
* Sincronize as atualizações com uma live copy específica.
* Suspender relação ou alterar a configuração de implementação de uma live copy específica.
* Acesse o console de visão geral da live copy.

Selecione o ativo ou a pasta de origem, abra o painel à esquerda e clique em **[!UICONTROL Referências]**. Como alternativa, selecione um ativo ou pasta e use o atalho de teclado `Alt + 4`.

![Ações e informações disponíveis no painel Referências para a fonte selecionada](assets/referencerail_source.png)

*Figura: Ações e informações disponíveis no painel Referências para a fonte selecionada.*

Para uma live copy específica, clique em **[!UICONTROL Editar Live Copy]** para suspender o relacionamento ou alterar a configuração de implantação.

![Para uma live copy específica, a opção de suspender a relação ou alterar a configuração de implantação é acessível no painel Referências quando o ativo de origem é selecionado](assets/referencerail_editlc_options.png)

*Figura: Suspender relação ou alterar a configuração de implementação de uma live copy específica.*

### Ações rápidas do painel Referências para a live copy {#ref-rail-lc}

Para um ativo ou pasta de live copy, você pode ver as seguintes informações e realizar as seguintes ações diretamente do painel Referências :

* Consulte o caminho de sua origem.
* Abra ou revele uma live copy específica na interface do usuário [!DNL Experience Manager].
* Implemente as atualizações.

Selecione um ativo ou uma pasta de live copy, abra o painel à esquerda e clique em **[!UICONTROL Referências]**. Como alternativa, selecione um ativo ou pasta e use o atalho de teclado `Alt + 4`.

![Ações disponíveis no painel Referências para a live copy selecionada](assets/referencerail_livecopy.png)

*Figura: Ações disponíveis no painel Referências para a live copy selecionada.*

## Propagar modificações da origem para cópias ativas {#rolloutsync}

Depois que uma fonte é modificada, as alterações podem ser propagadas para as cópias em tempo real usando uma ação de sincronização ou uma ação de implantação. Para entender a diferença entre as duas ações, consulte [glossário](#glossary).

### Ação de implantação {#rollout}

Você pode iniciar uma ação de implantação a partir do ativo de origem e atualizar todas ou algumas cópias em tempo real selecionadas.

1. Selecione um ativo de live copy ou uma pasta. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Como alternativa, use o atalho de teclado `p`.
1. Clique em **[!UICONTROL Origem da Live Copy]**. Clique em **[!UICONTROL Implantação]** na barra de ferramentas.
1. Selecione as cópias em tempo real que deseja atualizar. Clique em **[!UICONTROL Implantação]**.
1. Para implantar as atualizações feitas nos ativos secundários, selecione **[!UICONTROL Fonte de implantação e todos os filhos]**.

   ![Implementar as modificações da origem em algumas ou todas as cópias ao vivo](assets/livecopy_rollout_page.png)

   *Figura: Implemente as modificações da origem em algumas ou todas as cópias ativas.*

>[!NOTE]
>
>As modificações feitas em um ativo de origem são implantadas somente nas cópias ativas diretamente relacionadas. Se uma live copy for derivada de outra live copy, as modificações não serão implementadas na live copy derivada.

Como alternativa, você pode iniciar uma ação de implantação no painel Referências depois de selecionar uma live copy específica. Para obter mais informações, consulte [Ações rápidas do painel Referências para live copy](#ref-rail-lc). Neste método de implementação, somente a live copy selecionada e, opcionalmente, seus filhos são atualizados.

![Implantar as modificações da origem na live copy selecionada](assets/livecopy_rollout_dialog.png)

*Figura: Implemente as modificações da origem na live copy selecionada.*

### Sobre a ação de sincronização {#about-sync}

Uma ação de sincronização extrai as modificações de uma fonte somente para a live copy selecionada. A ação de sincronização respeita e mantém as modificações locais feitas após cancelar a herança. As modificações locais não são substituídas e a herança cancelada não é restabelecida. Você pode iniciar uma ação de sincronização de três maneiras.

| Onde na interface [!DNL Experience Manager] | Quando e por que usar | Como usar |
|---|---|---|
|  Painel de referência | Sincronize rapidamente quando já tiver a origem selecionada. | Consulte [Ações rápidas do painel Referências para origem](#refrailsource) |
| Barra de ferramentas na página [!UICONTROL Propriedades] | Inicie uma sincronização quando já tiver as propriedades da live copy abertas. | Consulte [Sincronizar uma live copy](#sync-lc) |
| [!UICONTROL Console de ] visão geral da Live Copy | Sincronize vários ativos rapidamente (não necessariamente todos) quando a pasta de origem estiver selecionada ou o console [!UICONTROL Visão geral da Live Copy] já estiver aberto. A ação de sincronização é iniciada para um ativo de cada vez, mas é uma maneira mais rápida de fazer a sincronização de vários ativos de uma só vez. | Consulte [Ações em muitos ativos em uma pasta de live copy](#bulk-actions) |

### Sincronizar uma live copy {#sync-lc}

Para iniciar uma ação de sincronização, abra a página **[!UICONTROL Propriedades]** de uma live copy, clique em **[!UICONTROL Live Copy]** e na ação desejada da barra de ferramentas.

Para ver os status e as informações relacionadas a uma ação de sincronização, consulte [Informações e status de uma live copy](#statuslcasset) e [Informações e status de todas as live copies de uma pasta](#status-lc-folder).

![A ação Sincronizar extrai as alterações feitas na origem](assets/livecopy_sync.png)

*Figura: A ação Sincronizar extrai as alterações feitas na origem.*

>[!NOTE]
>
>Se a relação for suspensa, a ação de sincronização não estará disponível na barra de ferramentas. Embora a ação de sincronização esteja disponível no painel Referências, as modificações não são propagadas mesmo após uma implantação bem-sucedida.

## Suspender e retomar a relação {#suspend-resume}

Você pode suspender temporariamente o relacionamento para impedir que uma live copy receba modificações feitas no ativo ou na pasta de origem. A relação também pode ser retomada para que a live copy comece a receber as modificações da origem.

Para suspender ou retomar, abra a página **[!UICONTROL Propriedades]** de uma live copy, clique em **[!UICONTROL Live Copy]** e clique na ação desejada na barra de ferramentas.

Como alternativa, você pode suspender ou retomar rapidamente os relacionamentos de vários ativos em uma pasta de live copy a partir do console **[!UICONTROL Visão geral da Live Copy]**. Consulte [Realizar ações em muitos ativos nas pastas de live copy](#bulk-actions).

## Faça modificações locais em uma live copy {#local-mods}

Uma live copy é uma réplica da origem original quando ela é criada. Os valores de metadados de uma live copy são herdados da origem. Os campos de metadados mantêm individualmente a herança com os respectivos campos do ativo de origem.

Entretanto, você tem a flexibilidade de fazer modificações locais em uma live copy para alterar algumas propriedades selecionadas. Para fazer modificações locais, cancele a herança da propriedade desejada. Quando a herança de um ou mais campos de metadados é cancelada, o relacionamento em tampo real do ativo e a herança dos outros campos de metadados são mantidas. Qualquer sincronização ou implementação não substitui as modificações locais. Para fazer isso, abra a página **[!UICONTROL Properties]** de um ativo de live copy, clique na opção **[!UICONTROL cancel herança]** ao lado de um campo de metadados.

Você pode desfazer todas as modificações locais e reverter o ativo para o estado de sua origem. A ação Redefinir substituirá irrevogavelmente e instantaneamente todas as modificações locais e restabelecerá a herança em todos os campos de metadados. Para reverter, na página **[!UICONTROL Propriedades]** de um ativo de live copy, clique em **[!UICONTROL Redefinir]** na barra de ferramentas.

![A ação Redefinir substitui as edições locais e traz a Live Copy em parte com sua origem.](assets/livecopy_reset.png)

*Figura: A ação Redefinir substitui as edições locais e traz a Live Copy em parte com sua origem.*

## Remover relacionamento dinâmico {#detach}

Você pode remover completamente a relação entre uma origem e uma live copy usando a ação Desanexar . A live copy se torna um ativo ou pasta independente após ser desanexada. Ele é exibido como um novo ativo na interface [!DNL Experience Manager], imediatamente após a desconexão. Para desconectar uma live copy da origem, siga essas etapas.

1. Selecione um ativo ou uma pasta de live copy. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Como alternativa, use o atalho de teclado `p`.

1. Clique em **[!UICONTROL Live Copy]**. Clique em **[!UICONTROL Desanexar]** na barra de ferramentas. Clique em **[!UICONTROL Desanexar]** da caixa de diálogo apresentada.

   ![A ação de desanexar remove completamente a relação entre a origem e a Live Copy](assets/livecopy_detach.png)

   *Figura: A ação de desanexar remove completamente a relação entre a origem e a Live Copy.*

   >[!CAUTION]
   >
   >A relação é removida imediatamente quando você clica em **[!UICONTROL Desanexar]** da caixa de diálogo. Não é possível desfazer isso clicando em **[!UICONTROL Cancel]** na página Propriedades.

Como alternativa, você pode desanexar rapidamente vários ativos em uma pasta de live copy do console **[!UICONTROL Visão geral da Live Copy]**. Consulte [Realizar ações em muitos ativos nas pastas de live copy](#bulk-actions).

## Ações em massa em uma pasta de live copy {#bulk-actions}

Se você tiver vários ativos em uma pasta de live copy, iniciar ações em cada ativo pode ser entediante. Você pode iniciar rapidamente as ações básicas em muitos ativos a partir de [!UICONTROL Console da Live Copy]. Os métodos acima continuam a funcionar para ativos individuais.

1. Selecione uma pasta de origem. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas. Como alternativa, use o atalho de teclado `p`.
1. Clique em **[!UICONTROL Origem da Live Copy]**. Para abrir o console, clique em **[!UICONTROL Visão geral da Live Copy]**.
1. Nesse painel, selecione um ativo de live copy de uma pasta live copy. Clique nas ações desejadas na barra de ferramentas. As ações disponíveis são **[!UICONTROL Sincronizar]**, **[!UICONTROL Redefinir]**, **[!UICONTROL Suspender]** e **[!UICONTROL Desanexar]**. É possível iniciar rapidamente essas ações em qualquer ativo em qualquer número de pastas de live copy que estejam em um relacionamento dinâmico com a pasta de origem selecionada.

   ![Atualize facilmente muitos ativos nas pastas de live copy do console Visão geral da Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Figura: Atualize facilmente muitos ativos nas pastas de live copy do console  [!UICONTROL Live Copy ] Overviewer.*

## Estender MSM para [!DNL Assets] {#extend-api}

[!DNL Experience Manager] O permite estender a funcionalidade usando as APIs Java do MSM. Para [!DNL Assets], a extensão funciona exatamente da mesma forma que com o MSM para [!DNL Sites]. Para obter detalhes, consulte [Extensão do MSM](/help/sites-developing/extending-msm.md) e o seguinte para obter informações sobre tarefas específicas:

* [Visão geral das APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Criar uma ação de sincronização](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Criar uma configuração de implementação](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Criar e usar uma classe LiveActionFactory simples](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* O Blueprint no MSM para [!DNL Sites] é chamado de origem da Live Copy no MSM para [!DNL Assets].
>* A remoção da etapa de capítulos no assistente de criação de site não é compatível com o MSM para [!DNL Assets].
>* A configuração de bloqueios do MSM, nas propriedades da página (interface habilitada para toque), não é compatível com o MSM para [!DNL Assets].


## Impacto das tarefas de gerenciamento de ativos em cópias ativas {#manage-assets}

As cópias em tempo real e as fontes são ativos ou pastas que podem ser gerenciados, de certa forma, como ativos digitais. Algumas tarefas de gerenciamento de ativos em [!DNL Experience Manager] têm um impacto específico nas cópias ativas.

* Copiar uma live copy cria um ativo de live copy com a mesma origem da primeira live copy.
* Quando você move uma origem ou sua live copy, o relacionamento dinâmico é mantido.
* A ação Editar não funciona para ativos de Live Copy. Se a origem de uma live copy for uma live copy em si, a ação de edição não funcionará para ela.
* A ação de check-out não está disponível para ativos de live copy.
* Para a pasta de origem, a opção para criar tarefas de revisão está disponível.
* Ao visualizar a lista de ativos na exibição de lista e na exibição de coluna, um ativo ou pasta de live copy exibe &quot;live copy&quot; em relação a ele. Ele ajuda você a identificar facilmente as cópias dinâmicas em uma pasta.

## Comparar MSM para [!DNL Assets] e [!DNL Sites] {#comparison}

Em mais cenários, o MSM para [!DNL Assets] corresponde ao comportamento do MSM para a funcionalidade de sites. Algumas diferenças principais a serem observadas são:

* O Blueprint no MSM para [!DNL Sites] é chamado de origem da Live Copy no MSM para [!DNL Assets].
* No Sites, você pode comparar um blueprint e sua live copy, mas não é possível em [!DNL Assets] comparar uma fonte à sua live copy.
* Não é possível editar uma live copy em [!DNL Assets].
* Os sites geralmente têm filhos, mas [!DNL Assets] não. A opção para incluir ou excluir ativos secundários não está presente ao criar cópias ao vivo de ativos individuais.
* A remoção da etapa de capítulos no assistente de criação de site não é compatível com o MSM para [!DNL Assets].
* Não há suporte para a configuração de bloqueios MSM nas propriedades da página (interface habilitada para toque) no MSM para [!DNL Assets].
* Para MSM para [!DNL Assets], use apenas a **[!UICONTROL Configuração de implementação padrão]**. As outras configurações de implementação não estão disponíveis para o MSM para [!DNL Assets].

## Práticas recomendadas {#best-practices}

Algumas práticas recomendadas para MSM são:

* Planeje os relacionamentos pai-filho dos ativos e fluxos de conteúdo antes de iniciar a implementação.

## Limitações e problemas conhecidos do MSM para [!DNL Assets] {#limitations}

A seguir, há uma limitação do MSM para [!DNL Assets].

* Fragmentos de conteúdo (CFs) não são compatíveis com o caso de uso. Ao tentar criar suas cópias ao vivo, os CFs são copiados como estão sem nenhum relacionamento. Os CFs copiados são um instantâneo no tempo e não são atualizados quando os CFs originais são atualizados.

* O MSM não funciona com o write-back de metadados habilitado. Após o write-back, a herança é interrompida.
