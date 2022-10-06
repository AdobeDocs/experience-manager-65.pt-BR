---
title: Práticas recomendadas do MSM
description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia e consultoria de Adobe para ajudar a ativar e executar o AEM Multi Site Manager.
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: c6ccd204dbd514d6195424aff495bc38f1f31bce
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 43%

---

# Práticas recomendadas do MSM{#msm-best-practices}

## Geral {#general}

O MSM é uma estrutura configurável para automatizar a implantação de conteúdo. As implementações geralmente envolvem partes importantes de um site e abrangem organizações e regiões geográficas. Portanto, é altamente recomendável planejar as implementações do MSM com o cuidado necessário ao planejar seu site:

* Cuidadosamente **planeje a estrutura do plano e os fluxos de conteúdo** antes de iniciar a implementação.
* **Reduza a quantidade de cópias dinâmicas.** O processamento de cópias em tempo real é uma tarefa que consome muitos recursos. Quanto mais cópias dinâmicas existirem em seu sistema, mais desempenho poderá ser afetado: do processamento de índices internos de live copy, de operações de live copy, como implantações, a operações da interface do usuário, como mostrar relacionamentos de live copy no painel de referências do administrador de sites. A prática recomendada é criar cópias ao vivo de sites ou ramificações de um site, onde as relações de live copy são herdadas para páginas no site ou ramificação. Evite criar cópias ativas individuais para páginas em um site ou ramificação quando toda a estrutura puder ser transformada em uma live copy.
* **Personalize o quanto for necessário, mas o mínimo possível.** Embora o MSM suporte um alto grau de personalização (por exemplo, configurações de implementação), a prática recomendada para o desempenho, confiabilidade e atualização de seu site é minimizar a personalização.
* Estabeleça um modelo de **governança** desde o início e treine os usuários adequadamente para garantir o sucesso. Uma prática recomendada do ponto de vista da governança é **minimize a autoridade que os produtores de conteúdo locais têm** para alocar/conectar conteúdo a outros usuários locais e suas respectivas cópias ativas. Isso ocorre porque heranças encadeadas e sem governança podem aumentar significativamente a complexidade de uma estrutura do MSM e comprometer seu desempenho e confiabilidade.

* Quando existir um plano para sua estrutura, fluxos de conteúdo, automação e governança - **protótipo e teste completamente seu sistema**, antes de iniciar a implementação ao vivo.
* Lembre-se que a **Adobe Consulting e os principais integradores de sistema** têm ampla experiência em planejar e implementar a automação de conteúdo com o MSM, então eles podem ajudar você a começar o projeto do MSM e durante toda a implementação.

>[!NOTE]
>
>Mais informações sobre como trabalhar com o MSM estão disponíveis nos artigos da Base de conhecimento:
>
>* [Solução de problemas e perguntas frequentes do MSM](troubleshoot-msm.md)
>


>[!NOTE]
>
>Também é possível usar a variável [Componente de referência](/help/sites-authoring/default-components-foundation.md#reference) para reutilizar uma única página ou parágrafo. Lembre-se, no entanto:
>
>* O MSM é mais flexível e permite controle detalhado sobre qual conteúdo é sincronizado e quando.
>* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) agora são recomendados sobre os componentes fundamentais.
>


## Origens de Live Copy e configurações de blueprint {#live-copy-sources-and-blueprint-configurations}

Lembre-se de que uma live copy pode ser criada usando [páginas regulares](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ou [configuração do blueprint](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos são casos de uso válidos.

Os benefícios adicionais de usar configurações de blueprint são que elas:

* Permitir que o autor use a variável **Implantação** em um blueprint - para (explicitamente) enviar modificações em live copies que herdam deste blueprint.
* Permitir que o autor use **Criar Site**; isso permite que o usuário selecione idiomas facilmente e configure a estrutura da live copy.
* Defina uma configuração de implementação padrão para cópias dinâmicas que tenham uma relação com o blueprint.

No caso de uma configuração do blueprint não ser referenciada, as implantações só poderão ser iniciadas a partir das próprias cópias ativas, obtendo essencialmente conteúdo da origem.

Ao criar um novo site com live copy, é vantajoso criar configurações de blueprint para garantir a disponibilidade do conjunto completo de recursos do MSM.

>[OBSERVAÇÃO!]
>
> Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de blueprints. Planeje isso ao configurar a Live Copy.

## Sincronização de componentes e contêineres {#components-and-container-synchronization}

Em geral, a regra de implantação no MSM em relação à sincronização de componentes é:

* Os componentes são implementados sincronizando os recursos contidos no blueprint.
* Os contêineres sincronizam somente o recurso atual.

Isso significa que os componentes são tratados como um agregado e, em uma implantação, o próprio componente e todos os seus componentes secundários são substituídos por aqueles nos blueprints. Isso significa que, se um recurso for adicionado localmente a esse componente, ele será perdido no conteúdo do blueprint durante a implantação.

Para suportar o aninhamento de componentes de modo que os componentes adicionados localmente sejam mantidos em uma implantação, o componente deve ser declarado como um contêiner. Como exemplo, o parsys padrão é declarado como um container para que possa suportar conteúdo adicionado localmente.

>[!NOTE]
>
>Adicione a propriedade `cq:isContainer` ao componente para designá-lo como um contêiner.

## Criar site {#create-site}

Observe que o AEM tem duas abordagens principais para a criação de cópias em tempo real:

* When [criação de uma Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Essa pode ser considerada a abordagem mais genérica, permitindo criar cópias ao vivo de qualquer página. A estrutura de conteúdo de uma live copy corresponde exatamente à fonte.

* When [criar um site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Essa é uma abordagem mais especializada, principalmente para criar sites com uma estrutura multilíngue.

Estas são algumas considerações que devem ser levadas em conta ao criar um site:

* Para criar um novo site, você precisa de uma [configuração de blueprint](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir a seleção de caminhos de idioma para criar em um novo site, as raízes de idioma correspondentes devem existir no blueprint (origem).
* Uma vez [novo site foi criado como uma live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Criar**, em seguida **Site**), os dois primeiros níveis dessa live copy são *superficial*. Os filhos da página não pertencem ao relacionamento dinâmico, mas uma implantação ainda descerá se um relacionamento dinâmico que corresponda ao acionador for encontrado.

   Ajuda a evitar:

   * adicionar idiomas manualmente no blueprint (abaixo do primeiro nível)
   * adicionar manualmente o conteúdo diretamente abaixo da raiz do idioma,
   * O não resulta no carregamento automático desse novo conteúdo para a live copy na implantação.

## MSM e sites multilíngues {#msm-and-multilingual-websites}

O MSM pode ajudar na criação de sites multilíngues de duas maneiras:

* Ao criar mestres em linguagem.

   * Embora o MSM em si **não forneça a tradução de conteúdo**, ele pode ser integrado a conectores de tradução de terceiros que o fazem. Observe que:

      * O MSM permite cancelar a herança no nível da página e/ou do componente. Isso ajuda a impedir a substituição do conteúdo traduzido (de uma live copy, com conteúdo ainda não traduzido de um blueprint) na próxima implantação.
      * Alguns conectores de tradução de terceiros automatizam esse gerenciamento de heranças do MSM.

         Consulte seu provedor de serviços de tradução para obter mais informações.

      * Uma abordagem alternativa para criar e traduzir matrizes de idioma é usar cópias de idioma juntamente com a estrutura de integração de tradução pronta para uso do AEM.

* Ao implantar conteúdo de mestres em linguagem.

   * Por exemplo, do idioma francês principal a sites específicos de país, como França/Francês, Canadá/Francês, Suíça/Francês.

Para obter mais informações, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) e as [Práticas recomendadas de tradução](/help/sites-administering/tc-bp.md).

## Alterações de estrutura e implantações {#structure-changes-and-rollouts}

As modificações na estrutura de conteúdo em uma árvore de blueprint/origem são refletidas de forma diferente em uma live copy. Isso depende do tipo de modificação:

* **Criação** novas páginas em um blueprint resultarão na criação de páginas correspondentes em live copies após a implantação com a configuração padrão de implantação.

* **Exclusão** as páginas em um blueprint resultarão na exclusão das páginas correspondentes das live copies após a implantação com a configuração padrão de implantação.

* **Movimentação** as páginas em um blueprint **not** O resultado é que as páginas correspondentes são movidas em live copies após a implantação com a configuração padrão de implementação:

   * O motivo para esse comportamento é que uma movimentação de página inclui implicitamente uma exclusão de página. Isso pode levar a um comportamento inesperado na publicação, já que a exclusão de páginas na criação desativa automaticamente o conteúdo correspondente na publicação. Isso também pode afetar itens relacionados, como links, marcadores e outros.
   * A herança de conteúdo nas respectivas páginas de Live Copy é atualizada para refletir o novo local de suas fontes no blueprint.
   * Para realizar totalmente uma mudança de página de um blueprint para cópias em tempo real, considere as seguintes práticas recomendadas:

>[!NOTE]
>
>Isso funcionará somente com a variável [No acionador de implantação](/help/sites-administering/msm-sync.md#rollout-triggers).

* Crie uma configuração de implantação personalizada:

   * Essa nova configuração deve incluir a ação:

      `PageMoveAction`

      Não adicione outras ações a essa configuração.

* Posicione a nova configuração:

   * Para implantar totalmente a movimentação da página, ao excluir as respectivas páginas no local antigo na live copy:

      * Posicione a configuração recém-criada antes da configuração de implantação padrão.

         A configuração de implementação padrão cuidará da exclusão das páginas em seu local antigo.
   * Para implantar a movimentação da página, mantendo as respectivas páginas no local antigo nas cópias ativas (essencialmente duplicando o conteúdo):

      * Posicione a configuração recém-criada após a configuração padrão de implantação.

         Isso garantirá que nenhum conteúdo seja excluído na live copy ou desativado da publicação.


## Personalização de implantações {#customizing-rollouts}

As configurações de implantação do MSM são altamente personalizáveis. Você deve estar ciente de que a automatização de implantações pode ter consequências abrangentes. Como prática recomendada, você deve planejar *very* antes, por exemplo:

* automatização das implantações; por exemplo, com [Acionadores onModify](#onmodify),
* personalização [tipos/propriedades de nó](#node-types-properties),
* iniciar workflows subsequentes,
* e/ou ativação de conteúdo como parte de implantações.

### onModify {#onmodify}

Ao usar o [acionador de implantação](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, você deve considerar que:

* A automatização de implantações com `onModify` acionadores pode ter um impacto negativo no desempenho da criação, pois ela aciona implantações após cada modificação de página.**

* O resultado da implantação pode diferir do esperado, uma vez que:

   * Não é possível especificar a ordem dos eventos de modificação resultantes.
   * A arquitetura baseada em eventos não pode garantir a sequência dos eventos transmitidos para o Gerenciador de implantação.

* O uso dessa configuração de implantação pode gerar conflitos se ocorrerem atualizações simultâneas do mesmo recurso.

Portanto, recomenda-se que você *only* use `onModify` dispara se os benefícios da iniciação automática de implementação ultrapassarem quaisquer possíveis problemas de desempenho.

### Tipos/propriedades de nós {#node-types-properties}

Lembre-se:

* Além de personalizar as ações de implantação, o MSM também permite personalizar as propriedades do nó que estão sendo implantadas. O [A configuração do MSM OSGi permite excluir tipos de nó](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de ser copiado da origem para a live copy.

## Informações adicionais {#further-information}

Esta e as seguintes páginas abordam os problemas relacionados:

* [Criação e sincronização de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Visão geral do console da Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurar a sincronização da Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitos de implantação do MSM](/help/sites-administering/msm-rollout-conflicts.md)
