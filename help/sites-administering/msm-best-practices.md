---
title: Práticas recomendadas do MSM
seo-title: Práticas recomendadas do MSM
description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia de Adobe e consultoria para ajudar a começar a trabalhar com o AEM Multi Site Manager.
seo-description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia de Adobe e consultoria para ajudar a começar a trabalhar com o AEM Multi Site Manager.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 1%

---


# Práticas recomendadas do MSM{#msm-best-practices}

## Geral {#general}

O MSM é uma estrutura configurável para automatizar a implantação de conteúdo. As implementações geralmente envolvem partes importantes de um site e abrangem organizações e geografias. Portanto, é altamente recomendável planejar implementações MSM tão cuidadosamente quanto planejar seu site:

* Planeje cuidadosamente a estrutura e os fluxos **** de conteúdo antes de iniciar a implementação.
* **Personalize o máximo necessário, mas o mínimo possível.** Embora o MSM suporte um alto grau de personalização (por exemplo, configurações de implementação), a prática recomendada para o desempenho, a confiabilidade e a capacidade de atualização do seu site é minimizar a personalização.
* Estabeleça um modelo de **governança** precocemente e treine os usuários em conformidade, para garantir o sucesso. Uma prática recomendada de um ponto de visualização de controle é **minimizar a autoridade que os produtores de conteúdo local têm** para alocar/conectar conteúdo a outros usuários locais e suas respectivas cópias online. Isso ocorre porque heranças encadeadas e não governadas podem aumentar significativamente a complexidade de uma estrutura MSM e comprometer seu desempenho e confiabilidade.

* Quando existir um plano para sua estrutura, fluxos de conteúdo, automação e controle - **protótipo e teste minuciosamente seu sistema**, antes de iniciar a implementação ativa.
* Lembre-se de que a **Adobe Consulting e os Integradores** de sistemas líderes têm um planejamento de experiência profunda e implementam a automação de conteúdo com a MSM, para que eles possam ajudá-lo a começar a usar o projeto MSM e toda a implementação.

>[!NOTE]
>
>Mais informações sobre como trabalhar com MSM estão disponíveis nos artigos da Base de conhecimento:
>
>* [Perguntas frequentes do MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Solução de problemas de MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>Você também pode usar o componente [](/help/sites-authoring/default-components-foundation.md#reference) Referência para reutilizar uma única página ou parágrafo. No entanto, lembre-se:
>
>* O MSM é mais flexível e permite controle detalhado sobre qual conteúdo é sincronizado e quando.
>* [Agora, os componentes](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) principais são recomendados pelos componentes básicos.

>



## Fontes de Live Copy e configurações do Blueprint {#live-copy-sources-and-blueprint-configurations}

Lembre-se de que uma cópia ao vivo pode ser criada usando páginas [](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) regulares ou uma configuração [de](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)blueprint. Ambos são casos de uso válidos.

Os benefícios adicionais do uso de uma configuração de blueprint são:

* Permita que o autor use a opção **Rollout** em um blueprint - para (explicitamente) modificações de envio para cópias online herdadas deste blueprint.
* Permitir que o autor use **Criar site**; isso permite que o usuário selecione facilmente os idiomas e configure a estrutura da live copy.
* Defina uma configuração padrão de implementação para cópias online que tenham uma relação com o blueprint.

Caso uma configuração de blueprint não seja mencionada, as rotações só podem ser iniciadas a partir das próprias cópias ativas, essencialmente retirando o conteúdo da fonte.

Ao criar um novo site com live copy, é vantajoso criar configurações de blueprint para garantir a disponibilidade do conjunto completo de recursos MSM.

## Sincronização de componentes e Container {#components-and-container-synchronization}

Em geral, a regra de implantação no MSM em relação à sincronização de componentes é:

* Os componentes são implantados sincronizando quaisquer recursos contidos no blueprint.
* Container sincronizam somente o recurso atual.

Isso significa que os componentes são tratados como uma agregação, e em um lançamento o próprio componente e todos os seus filhos são substituídos pelos componentes do projeto. Isso significa que, se um recurso for adicionado localmente a esse componente, ele será perdido para o conteúdo do blueprint no lançamento.

Para suportar o aninhamento de componentes, de modo que os componentes adicionados localmente sejam mantidos em uma implementação, o componente deve ser declarado como um container. Como exemplo, o parsys padrão é declarado como um container para que ele possa suportar conteúdo adicionado localmente.

>[!NOTE]
>
>Adicione a propriedade `cq:isContainer` ao componente para designá-lo como um container.

## Criar site {#create-site}

Observe que AEM tem duas abordagens principais para a criação de cópias online:

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Isso pode ser considerado como a abordagem mais genérica, permitindo que você crie cópias online de qualquer página. A estrutura de conteúdo de uma live copy corresponde exatamente à fonte.

* Ao [criar um site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Esta é uma abordagem mais especializada, principalmente para criar sites com uma estrutura multilíngue.

Veja a seguir algumas considerações para ter em mente ao criar um site:

* Para criar um novo site, você precisa de uma configuração [](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)blueprint.
* Para permitir a seleção de caminhos de idioma para criar em um novo site, as raízes de idioma correspondentes devem existir no blueprint (origem).
* Depois que um [novo site é criado como uma live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Criar** e, em seguida, **Site**), os dois primeiros níveis dessa live copy são *superficiais*. Os filhos da página não pertencem ao relacionamento ao vivo, mas uma implementação ainda descerá se uma relação ao vivo que corresponde ao acionador for encontrada.

   Ajuda a evitar:

   * adicionar manualmente idiomas no blueprint (abaixo do primeiro nível)
   * adicionar manualmente o conteúdo diretamente abaixo da raiz do idioma,
   * não resulta no carregamento automático desse novo conteúdo para a live copy na execução.

## Sites MSM e multilíngues {#msm-and-multilingual-websites}

A MSM pode ajudar na criação de sites multilíngues de duas formas:

* Ao criar mestres em linguagem.

   * Embora o próprio MSM **não forneça tradução** de conteúdo, ele pode ser integrado a conectores de tradução de terceiros que o fazem. Note que:

      * O MSM permite que você cancele a herança no nível da página e/ou do componente. Isso ajuda a impedir a substituição de conteúdo traduzido (de uma cópia ao vivo, com conteúdo ainda não traduzido de um blueprint) no próximo lançamento.
      * Alguns conectores de tradução de terceiros automatizam esse gerenciamento de heranças MSM.

         Consulte seu provedor de serviço de tradução para obter mais informações.

      * Uma abordagem alternativa para criar e traduzir mestres de linguagem é usar cópias de idioma em conjunto com AEM estrutura de integração de tradução pronta para uso.

* Ao implantar conteúdo de mestres em idiomas.

   * Por exemplo, da língua francesa principal a sites específicos de cada país, como França/Francês, Canadá/Francês, Suíça/Francês.

Para obter mais informações, consulte [Traduzir conteúdo para sites](/help/sites-administering/translation.md) multilíngues e as práticas recomendadas [](/help/sites-administering/tc-bp.md)de tradução.

## Alterações na estrutura e rolagens {#structure-changes-and-rollouts}

As modificações na estrutura do conteúdo em uma árvore de blueprint/origem são refletidas de forma diferente em uma cópia ao vivo. Isso depende do tipo de modificação:

* **A criação** de novas páginas em um blueprint resultará na criação das páginas correspondentes em cópias online após a implantação com a configuração padrão de implantação.

* **A exclusão** de páginas em um blueprint resultará na exclusão de páginas correspondentes de cópias online após a implantação com a configuração padrão de implantação.

* **Mover** páginas em um blueprint **não** resultará na movimentação das páginas correspondentes em cópias online após a implantação com a configuração padrão de roll-out:

   * O motivo desse comportamento é que uma movimentação de página inclui implicitamente uma exclusão de página. Isso pode levar a um comportamento inesperado na publicação, já que a exclusão de páginas no autor desativa automaticamente o conteúdo correspondente na publicação. Isso também pode ter um efeito de repercussão em itens relacionados, como links, marcadores e outros.
   * A herança de conteúdo nas respectivas páginas de live copy é atualizada para refletir a nova localização de suas fontes no blueprint.
   * Para realizar uma mudança completa de página de um blueprint para cópias online, considere as seguintes práticas recomendadas:

>[!NOTE]
>
>Isso funcionará somente com o acionador [Ativado](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Crie uma configuração de implantação personalizada:

   * Esta nova configuração deve incluir a ação:

      `PageMoveAction`

      Não adicione outras ações a esta configuração.

* Posicione a nova configuração:

   * Para implantar completamente a movimentação da página, ao excluir as respectivas páginas em seu local antigo na live copy:

      * Posicione a configuração recém-criada antes da configuração de implantação padrão.

         A configuração padrão de implantação cuidará da exclusão das páginas em seu local antigo.
   * Para implantar a movimentação da página mantendo as respectivas páginas em seu local antigo nas cópias online (essencialmente duplicando o conteúdo):

      * Posicione a configuração recém-criada após a configuração de implantação padrão.

         Isso garantirá que nenhum conteúdo seja excluído na live copy ou desativado da publicação.


## Personalização de roteiros {#customizing-rollouts}

As configurações de implementação MSM são altamente personalizáveis. Vocês devem estar cientes de que a automatização das rotações pode ter consequências de longo alcance. Como prática recomendada, você deve planejar com *muito* cuidado antes, por exemplo:

* automatização das rotações; por exemplo, com acionadores [onModify](#onmodify),
* personalização de tipos/propriedades [de](#node-types-properties)nós,
* iniciando workflows subsequentes,
* e/ou ativação de conteúdo como parte de lançamentos.

### onModify {#onmodify}

Ao usar o acionador [de](/help/sites-administering/msm-sync.md#rollout-triggers) roll-out, `onModify` você deve considerar que:

* Automatizar implementações com `onModify` acionadores pode ter um impacto negativo no desempenho de criação à medida que acionam implantações após *cada* modificação de página.

* O resultado do roll-out pode diferir do esperado como:

   * Não é possível especificar a ordem dos eventos de modificação resultantes.
   * A arquitetura baseada em eventos não pode garantir a sequência dos eventos passados para o Gerenciador de implantação.

* O uso dessa configuração de implementação pode levar à confirmação de conflitos se ocorrerem atualizações simultâneas do mesmo recurso.

Portanto, é recomendável que você *use* `onModify` acionadores apenas se os benefícios da iniciação automática de roll-out compensarem quaisquer possíveis problemas de desempenho.

### Tipos de nó/Propriedades {#node-types-properties}

Lembre-se de que:

* Além de personalizar ações de implementação, o MSM também permite personalizar as propriedades do nó que estão sendo implantadas. A configuração do [MSM OSGi permite excluir tipos](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de nó da cópia da origem para a live copy.

## Informações adicionais {#further-information}

Esta e as seguintes páginas cobrem os problemas relacionados:

* [Criando e Sincronizando Live Copies](/help/sites-administering/msm-livecopy.md)
* [Console de Visão Geral do Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurar a sincronização da Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitos de implantação do MSM](/help/sites-administering/msm-rollout-conflicts.md)

