---
title: Práticas recomendadas do MSM
seo-title: Práticas recomendadas do MSM
description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia e consultoria de Adobe para ajudar a ativar e executar o AEM Multi Site Manager.
seo-description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia e consultoria de Adobe para ajudar a ativar e executar o AEM Multi Site Manager.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: Gerenciamento de vários sites
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 1%

---

# Práticas recomendadas do MSM{#msm-best-practices}

## Geral {#general}

O MSM é uma estrutura configurável para automatizar a implantação de conteúdo. As implementações geralmente envolvem partes importantes de um site, organizações de extensão e regiões geográficas. Portanto, é altamente recomendável planejar as implementações do MSM com o cuidado necessário ao planejar seu site:

* Cuidadosamente **planeje a estrutura e os fluxos de conteúdo** antes de iniciar a implementação.
* **Reduza a quantidade de cópias dinâmicas.** O processamento de cópias em tempo real é uma tarefa que consome muitos recursos. Quanto mais cópias dinâmicas existirem em seu sistema, mais desempenho poderá ser afetado: do processamento de índices internos de live copy, de operações de live copy, como implantações, a operações da interface do usuário, como mostrar relacionamentos de live copy no painel de referências do administrador de sites. A prática recomendada é criar cópias ao vivo de sites ou ramificações de um site, onde as relações de live copy são herdadas para páginas no site ou ramificação. Evite criar cópias ativas individuais para páginas em um site ou ramificação quando toda a estrutura puder ser transformada em uma live copy.
* **Personalize o quanto for necessário, mas o mínimo possível.** Embora o MSM suporte um alto grau de personalização (por exemplo, configurações de implementação), a prática recomendada para o desempenho, confiabilidade e atualização de seu site é minimizar a personalização.
* Estabeleça um modelo de **governança** antecipadamente e treine os usuários de acordo, para garantir o sucesso. Uma prática recomendada do ponto de vista de governança é **minimizar a autoridade que os produtores de conteúdo local têm** para alocar/conectar conteúdo a outros usuários locais e suas respectivas cópias dinâmicas. Isso ocorre porque heranças encadeadas e não governadas podem aumentar significativamente a complexidade de uma estrutura MSM e comprometer seu desempenho e confiabilidade.

* Depois que houver um plano para sua estrutura, fluxos de conteúdo, automação e governança - **protótipo e teste completamente seu sistema**, antes de iniciar a implementação ativa.
* Lembre-se de que **Adobe Consulting e os principais integradores de sistema** têm um planejamento de experiência profundo e implementam a automação de conteúdo com o MSM, para que eles possam ajudá-lo a começar a usar o projeto MSM e em toda a implementação.

>[!NOTE]
>
>Mais informações sobre como trabalhar com o MSM estão disponíveis nos artigos da Base de conhecimento:
>
>* [Perguntas frequentes sobre o MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Solução de problemas do MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>Você também pode usar o [Componente de referência](/help/sites-authoring/default-components-foundation.md#reference) para reutilizar uma única página ou parágrafo. Lembre-se, no entanto:
>
>* O MSM é mais flexível e permite controle detalhado sobre qual conteúdo é sincronizado e quando.
>* [Os ](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) componentes principais agora são recomendados sobre os componentes fundamentais.

>



## Fontes de Live Copy e configurações do Blueprint {#live-copy-sources-and-blueprint-configurations}

Lembre-se de que uma live copy pode ser criada usando [páginas regulares](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ou [configuração do blueprint](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos são casos de uso válidos.

Os benefícios adicionais do uso de uma configuração do blueprint são:

* Permita que o autor use a opção **Rollout** em um blueprint - para (explicitamente) enviar modificações em live copies que herdam deste blueprint.
* Permitir que o autor use **Criar Site**; isso permite que o usuário selecione idiomas facilmente e configure a estrutura da live copy.
* Defina uma configuração de implementação padrão para cópias dinâmicas que tenham uma relação com o blueprint.

No caso de uma configuração do blueprint não ser referenciada, as implantações só poderão ser iniciadas a partir das próprias cópias ativas, obtendo essencialmente conteúdo da origem.

Ao criar um novo site com live copy, é vantajoso criar configurações de blueprint para garantir a disponibilidade do conjunto completo de recursos do MSM.

>[OBSERVAÇÃO!]
>
> Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de Blueprints. Planeje isso ao configurar a Live Copy.

## Sincronização de componentes e contêineres {#components-and-container-synchronization}

Em geral, a regra de implantação no MSM em relação à sincronização de componentes é:

* Os componentes são implementados sincronizando os recursos contidos no blueprint.
* Os contêineres sincronizam somente o recurso atual.

Isso significa que os componentes são tratados como um agregado e, em uma implementação, o próprio componente e todos os seus filhos são substituídos por aqueles nos blueprints. Isso significa que, se um recurso for adicionado localmente a esse componente, ele será perdido no conteúdo do blueprint na implantação.

Para suportar o aninhamento de componentes de modo que os componentes adicionados localmente sejam mantidos em uma implantação, o componente deve ser declarado como um contêiner. Como exemplo, o parsys padrão é declarado como um container para que possa suportar conteúdo adicionado localmente.

>[!NOTE]
>
>Adicione a propriedade `cq:isContainer` ao componente para designá-la como um container.

## Criar site {#create-site}

Observe que o AEM tem duas abordagens principais para a criação de cópias em tempo real:

* Quando [criar uma Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Essa pode ser considerada a abordagem mais genérica, permitindo criar cópias ao vivo de qualquer página. A estrutura de conteúdo de uma live copy corresponde exatamente à fonte.

* Quando [criar um Site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Essa é uma abordagem mais especializada, principalmente para criar sites com uma estrutura multilíngue.

Estas são algumas considerações que devem ser levadas em conta ao criar um site:

* Para criar um novo site, você precisa de uma [configuração do blueprint](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir a seleção de caminhos de idioma para criar em um novo site, as raízes de idioma correspondentes devem existir no blueprint (fonte).
* Depois que um [novo site tiver sido criado como uma live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Criar**, em seguida **Site**), os dois primeiros níveis desta live copy serão *Shallow*. Os filhos da página não pertencem ao relacionamento ao vivo, mas uma implantação ainda descerá se um relacionamento ao vivo que corresponda ao acionador for encontrado.

   Ajuda a evitar:

   * adicionar idiomas manualmente no blueprint (abaixo do primeiro nível)
   * adicionar manualmente o conteúdo diretamente abaixo da raiz do idioma,
   * O não resulta no carregamento automático desse novo conteúdo para a live copy na implantação.

## MSM e sites multilíngues {#msm-and-multilingual-websites}

O MSM pode ajudar na criação de sites multilíngues de duas maneiras:

* Ao criar mestres em linguagem.

   * Embora o próprio MSM **não forneça tradução de conteúdo**, ele pode ser integrado a conectores de tradução de terceiros que fornecem. Observe que:

      * O MSM permite cancelar a herança no nível da página e/ou do componente. Isso ajuda a impedir a substituição do conteúdo traduzido (de uma live copy, com conteúdo ainda não traduzido de um blueprint) na próxima implantação.
      * Alguns conectores de tradução de terceiros automatizam esse gerenciamento de heranças do MSM.

         Consulte seu provedor de serviços de tradução para obter mais informações.

      * Uma abordagem alternativa para criar e traduzir mestres de linguagem é usar cópias de idioma juntamente com AEM estrutura de integração de tradução pronta para uso.

* Ao implantar conteúdo de mestres em linguagem.

   * Por exemplo, do idioma francês principal a sites específicos de país, como França/Francês, Canadá/Francês, Suíça/Francês.

Para obter mais informações, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) e [Práticas recomendadas de tradução](/help/sites-administering/tc-bp.md).

## Alterações na estrutura e implantações {#structure-changes-and-rollouts}

As modificações na estrutura de conteúdo em uma árvore de blueprint/origem são refletidas de forma diferente em uma live copy. Depende do tipo de modificação:

* **** A criação de novas páginas em um blueprint resultará na criação de páginas correspondentes em cópias ao vivo após a implantação com a configuração padrão de implementação.

* **** A exclusão de páginas em um blueprint resultará na exclusão de páginas correspondentes de cópias ativas após a implantação com a configuração de implementação padrão.

* **** Mover páginas em um blueprint  **** não resultará na movimentação das páginas correspondentes em cópias ao vivo após a implantação com a configuração padrão de implementação:

   * O motivo para esse comportamento é que uma movimentação de página inclui implicitamente uma exclusão de página. Isso pode levar a um comportamento inesperado na publicação, já que a exclusão de páginas no autor desativa automaticamente o conteúdo correspondente na publicação. Isso também pode afetar itens relacionados, como links, marcadores e outros.
   * A herança de conteúdo nas respectivas páginas de Live Copy é atualizada para refletir o novo local de suas fontes no blueprint.
   * Para realizar totalmente uma mudança de página de um blueprint para cópias em tempo real, considere as seguintes práticas recomendadas:

>[!NOTE]
>
>Isso funcionará somente com o [On Rollout trigger](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Crie uma configuração de implementação personalizada:

   * Essa nova configuração deve incluir a ação :

      `PageMoveAction`

      Não adicione outras ações a essa configuração.

* Posicione a nova configuração:

   * Para implantar totalmente a movimentação da página, ao excluir as respectivas páginas no local antigo na live copy:

      * Posicione a configuração recém-criada antes da configuração de implementação padrão.

         A configuração de implementação padrão cuidará da exclusão das páginas em seu local antigo.
   * Para implantar a movimentação da página, mantendo as respectivas páginas no local antigo nas cópias ativas (essencialmente duplicando o conteúdo):

      * Posicione a configuração recém-criada após a configuração padrão de implementação.

         Isso garantirá que nenhum conteúdo seja excluído na live copy ou desativado da publicação.


## Personalizando implantações {#customizing-rollouts}

As configurações de implementação do MSM são altamente personalizáveis. Você deve estar ciente de que a automatização de implantações pode ter consequências de longo alcance. Como prática recomendada, você deve planejar *very* cuidadosamente antes, por exemplo:

* automatização das implantações; por exemplo, com [onModify triggers](#onmodify),
* personalizar [tipos de nó/propriedades](#node-types-properties),
* iniciar workflows subsequentes,
* e/ou ativação de conteúdo como parte de implantações.

### onModify {#onmodify}

Ao usar o [acionador de implementação](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, considere que:

* A automatização de implantações com `onModify` acionadores pode ter um impacto negativo no desempenho da criação à medida que acionam implantações após *cada* modificação de página.

* O resultado da implantação pode diferir do esperado como:

   * Não é possível especificar a ordem dos eventos de modificação resultantes.
   * A arquitetura baseada em eventos não pode garantir a sequência dos eventos transmitidos para o Gerenciador de implementação.

* O uso dessa configuração de implementação pode gerar conflitos se ocorrerem atualizações simultâneas do mesmo recurso.

Portanto, é recomendável usar *somente* acionadores `onModify` se os benefícios da iniciação de implementação automática compensarem quaisquer problemas de desempenho em potencial.

### Tipos de nó/Propriedades {#node-types-properties}

Lembre-se:

* Além de personalizar as ações de implantação, o MSM também permite personalizar as propriedades do nó que estão sendo implantadas. A configuração [MSM OSGi permite excluir os tipos de nó](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de serem copiados da origem para a live copy.

## Informações adicionais {#further-information}

Esta e as seguintes páginas abordam os problemas relacionados:

* [Criação e sincronização de cópias em tempo real](/help/sites-administering/msm-livecopy.md)
* [Console de Visão Geral da Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurar a sincronização da Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitos de implementação do MSM](/help/sites-administering/msm-rollout-conflicts.md)
