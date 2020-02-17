---
title: '"Reutilizando conteúdo: Multi Site Manager e Live Copy"'
seo-title: '"Reutilizando conteúdo: Multi Site Manager e Live Copy"'
description: Saiba mais sobre como reutilizar conteúdo com Live Copies e o Multi Site Manager.
seo-description: Saiba mais sobre como reutilizar conteúdo com Live Copies e o Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Reutilizando conteúdo: Multi Site Manager e Live Copy{#reusing-content-multi-site-manager-and-live-copy}

O Multi Site Manager (MSM) permite que você use o mesmo conteúdo do site em vários locais. O MSM usa sua funcionalidade de Live Copy para conseguir isso:

* Com o MSM é possível:

   * Criar conteúdo uma vez e depois
   * Copie esse conteúdo para e reutilize esse conteúdo em outras áreas (cópias[](#live-copies)ativas) do mesmo site ou de outros sites.

* Em seguida, o MSM mantém os relacionamentos (ao vivo) entre seu conteúdo de origem e suas cópias ao vivo para que:

   * Quando você faz alterações no conteúdo de origem, as cópias de origem e ao vivo são sincronizadas (para aplicar essas alterações também às cópias ao vivo).
   * Você pode fazer ajustes no conteúdo das cópias ativas desconectando a relação ativa de subpáginas e/ou componentes individuais. Ao fazer isso, as alterações na fonte não serão mais aplicadas à live copy.

Esta e as seguintes páginas cobrem os problemas relacionados:

* [Criando e Sincronizando Live Copies](/help/sites-administering/msm-livecopy.md)
* [Console de Visão Geral do Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurar a sincronização da Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitos de implantação do MSM](/help/sites-administering/msm-rollout-conflicts.md)
* [Práticas recomendadas do MSM](/help/sites-administering/msm-best-practices.md)

## Cenários possíveis {#possible-scenarios}

Há muitos casos de uso para MSM e cópias online, alguns casos incluem:

* **Multinacionais - Global para Empresa Local**

   Um caso típico de uso suportado pela MSM é a reutilização de conteúdo em vários sites multinacionais de mesma língua. Isto permite a reutilização do conteúdo de base, permitindo ao mesmo tempo variações nacionais.

   Por exemplo, a seção Inglês da amostra Site de referência We.Retail é criada para clientes nos EUA. A maior parte do conteúdo deste site também pode ser usada para outros sites Web.Retail que atendem clientes de língua inglesa de diferentes países e culturas. O conteúdo principal continua a ser o mesmo em todos os sítios, enquanto podem ser feitos ajustamentos regionais.

   A seguinte estrutura pode ser usada para sites dos Estados Unidos, Reino Unido, Canadá e Austrália:

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >O MSM não traduz o conteúdo. É usado para criar a estrutura necessária e implantar o conteúdo.
   >
   >
   >Consulte [Traduzir conteúdo para sites](/help/sites-administering/translation.md) multilíngues se desejar estender um exemplo desse tipo.

* **Nacional - Gabinete Diretor das Sucursais Regionais**

   Em alternativa, uma empresa com uma rede de concessionários poderia querer sítios Web separados para as suas concessionárias individuais, cada uma das quais constitui uma variação do sítio principal fornecido pela sede. Isto pode ser feito para uma única empresa com vários escritórios regionais, ou para um sistema nacional de franquia composto por um franqueador central e vários franqueados locais.

   A sede pode fornecer as informações essenciais, enquanto as entidades regionais podem acrescentar informações locais, tais como os dados de contato, o horário de abertura e os eventos.

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **Várias versões**

   Ou você pode usar o MSM para criar versões de uma subramificação específica. Por exemplo, um subsite de suporte contendo detalhes das diferentes versões de um produto específico, no qual as informações básicas permanecem constantes e apenas os recursos atualizados precisam ser alterados:

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >Nesse cenário, há sempre a questão de se fazer uma cópia direta ou usar cópias ao vivo.
   >
   >Existe um equilíbrio entre:
   >
   >  * Quanto do conteúdo principal precisará ser atualizado em várias versões.
   >
   >Contra:
   >
   >  * A quantidade de cópias individuais que terá de ser ajustada.


## MSM da interface do usuário {#msm-from-the-ui}

O MSM está diretamente acessível na interface do usuário usando várias opções do console apropriado. Para fornecer uma introdução, a lista a seguir mostra os principais locais:

* **Criar site** (**sites**)

   * O MSM ajuda a gerenciar vários sites que compartilham conteúdo comum; por exemplo, os sites geralmente são fornecidos para públicos internacionais de forma que a maioria do conteúdo é comum em todos os países, com um subconjunto do conteúdo específico para cada país. O MSM permite que você [crie cópias ativas que atualizam automaticamente um ou mais sites com base no site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)de origem. Isso também ajuda a impor uma estrutura básica comum, usar o conteúdo comum em vários sites, manter uma aparência comum e concentrar esforços no gerenciamento do conteúdo que realmente difere entre os sites.
   * Requer uma configuração predefinida do blueprint para especificar a origem.
   * Cria uma cópia ao vivo da fonte (predefinida).
   * Fornece ao usuário o botão **Rollout** .

* **Criar Live Copy** (**Sites**)

   * O MSM permite que você [crie uma cópia ad hoc (one-off) em tempo real de uma página ou subramificação individual de um site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page); por exemplo, duplicar uma subramificação para fornecer informações sobre uma versão nova/atualizada de um produto.
   * Cria uma live copy ad-hoc (nenhuma configuração blueprint é necessária).
   * Pode ser usado para (imediatamente) criar uma cópia ao vivo de qualquer página/ramificação.
   * Requer **sincronização** (não fornece o botão **implantação** ).

* **Propriedades** da exibição (**Sites**)

   * Quando apropriado, essa opção ajuda a [monitorar sua live copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) fornecendo informações sobre o **Live** Copy ou o **Blueprint** relacionado.

* **Referências** (**Sites**)

   * O painel [Referências](/help/sites-authoring/basic-handling.md#references) fornece informações sobre Cópias **** ao vivo, juntamente com o acesso às ações apropriadas.

* **Visão Geral** da Live Copy (**Sites**)

   * Esse console permite que você [visualize e gerencie seu blueprint e suas cópias](/help/sites-administering/msm-livecopy-overview.md)ativas.

* **Blueprints** (**Ferramentas** - **Sites**)

   * Esse console permite que você [crie e gerencie suas configurações](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)blueprint.

>[!NOTE]
>
>Os aspectos da funcionalidade MSM são usados em vários outros recursos do AEM (por exemplo, Inicializações, Catálogo); nesses casos, a live copy é gerenciada por esse recurso.

### Termos usados {#terms-used}

A título de introdução, a tabela seguinte apresenta uma panorâmica dos principais termos utilizados com a MSM. eles serão abordados em mais detalhes nas seções e páginas subsequentes:

<table>
 <tbody>
  <tr>
   <td><strong>Term</strong></td>
   <td><strong>Definição</strong></td>
   <td><strong>Detalhes adicionais</strong></td>
  </tr>
  <tr>
   <td><strong>Origem</strong></td>
   <td>As páginas originais.</td>
   <td>Sinônimo de páginas do Blueprints e/ou do Blueprint.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>A cópia (da origem), mantida pelas ações de sincronização, conforme definido pelas configurações de implantação. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuração da Live Copy</strong></td>
   <td>Definição dos detalhes de configuração para uma live copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Relacionamento ao vivo</strong><br /> </td>
   <td>Definição eficaz da herança para um determinado recurso; a(s) conexão(ões) entre a fonte e as cópias online.<br /> </td>
   <td>Certifique-se de que as alterações na origem possam ser sincronizadas com a live copy.</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>Sinônimo de Source.</td>
   <td>Pode ser definido por uma configuração blueprint.</td>
  </tr>
  <tr>
   <td><strong>Configuração do Blueprint</strong></td>
   <td>Configuração predefinida que especifica um caminho de origem.</td>
   <td>Quando uma página de blueprint é referenciada em uma configuração de blueprint, o comando Rollout fica disponível.</td>
  </tr>
  <tr>
   <td><strong>Sincronização</strong></td>
   <td>O termo genérico para sincronização de conteúdo entre a origem e as cópias online (tanto por <strong>implantação</strong> quanto por <strong>sincronização</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Implantação</strong><br /> </td>
   <td>Sincroniza da origem para a livecopy.<br /> Pode ser acionado por um autor (em uma página de blueprint) ou por um evento do sistema (conforme definido pela configuração de lançamento).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuração de implantação</strong></td>
   <td>Regras que determinam quais propriedades serão sincronizadas, como e quando.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sincronizar</strong></td>
   <td>Uma solicitação manual de sincronização, feita a partir das páginas do live copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Herança</strong></td>
   <td>Uma página/componente de live copy herda o conteúdo de sua página/componente de origem quando a sincronização ocorre.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Suspender</strong></td>
   <td>Remove temporariamente a relação ao vivo entre uma live copy e sua página de blueprint.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Destacar</strong></td>
   <td>Remove permanentemente a relação ao vivo entre uma live copy e sua página de blueprint.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Redefinir</strong></td>
   <td><p>Redefinir uma página de cópia online para:</p>
    <ul>
     <li>Remova todos os cancelamentos de herança e<br /> </li>
     <li>Retorna a página ao mesmo estado que a página de origem.</li>
    </ul> <p>A redefinição afeta todas as alterações feitas nas propriedades da página, no sistema de parágrafo e nos componentes.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Superficial</strong></td>
   <td>Uma cópia ao vivo de uma única página.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Profundo</strong></td>
   <td>Uma cópia ao vivo de uma página, juntamente com suas páginas secundárias.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Consulte [Visão geral da API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) Java para obter os nomes dos objetos.

## Live Copies {#live-copies}

Uma cópia online MSM é uma cópia do conteúdo específico do site para o qual é mantida uma relação ativa com a fonte original:

* A live copy herda o conteúdo de sua origem.
* A sincronização executa a transferência real do conteúdo quando as alterações são feitas na fonte.
* Uma live copy pode ser considerada como:

   * Superficial: uma única página
   * Profundo: a página, juntamente com suas páginas secundárias

* As regras de sincronização, chamadas de configurações de implantação, determinam quais propriedades são sincronizadas e quando a sincronização ocorre.

No exemplo anterior, `/content/we-retail/language-masters/en` é o site mestre global em inglês. Para reutilizar o conteúdo deste site, são criadas cópias online MSM:

* O conteúdo abaixo `/content/we-retail/language-masters/en` é a fonte.

* O conteúdo abaixo `/content/we-retail/language-masters/en` é copiado abaixo dos nós `/content/we-retail/us/en/`, `/content/we-retail/gb/en`e `/content/we-retail/ca/en``/content/we-retail/au/en` . Estas são as cópias ao vivo.

* Os autores fazem alterações nas páginas abaixo `/content/we-retail/language-masters/en`.
* Quando acionado, o MSM sincroniza essas alterações nas cópias online.

### Live Copies - Composição {#live-copies-composition}

>[!NOTE]
>
>Os diagramas e descrições desta seção representam instantâneos de possíveis cópias online. Não são abrangentes, mas fornecem uma visão geral para destacar características específicas.

Quando você cria uma live copy, as páginas de origem selecionadas são refletidas em uma base 1:1 na live copy. Depois disso, novos recursos (páginas e/ou parágrafos) também podem ser criados diretamente na live copy, portanto, é útil estar ciente dessas variações e como elas afetam a sincronização. As composições possíveis incluem:

* [Live Copy com páginas que não são Live-Copy](#live-copy-with-non-live-copy-pages)
* [Cópias online aninhadas](#nested-live-copies)

A forma básica de live copy tem:

* Páginas de Live Copy que refletem as páginas de origem selecionadas em uma base 1:1.
* Uma definição de configuração.
* Uma relação ao vivo definida para cada recurso:

   * Vincule o recurso live copy ao seu blueprint/fonte.
   * São usados ao realizar herança e implantação.

* As alterações podem ser [sincronizadas](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) de acordo com os requisitos.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy com páginas que não são Live-Copy {#live-copy-with-non-live-copy-pages}

Ao criar uma live copy no AEM, você pode ver e navegar pela live copy branch e usar a funcionalidade normal do AEM na live copy branch. Isso significa que você (ou um processo) pode criar novos recursos (páginas e/ou parágrafos) dentro da ramificação da live copy (por exemplo, `myCanadaOnlyProduct`).

* Esses recursos não têm relação ativa com as páginas de origem/blueprint e não são sincronizados.
* Podem ocorrer cenários que o MSM trata como casos especiais. Por exemplo, quando você (ou um processo) cria uma página com a mesma posição e nome nas ramificações de origem/blueprint e live copy. Para essas situações, consulte Conflitos [de implantação do](/help/sites-administering/msm-rollout-conflicts.md) MSM para obter mais informações.

![chlimage_1-368](assets/chlimage_1-368.png)

#### Cópias online aninhadas {#nested-live-copies}

Quando você (ou um processo) cria uma [nova página em uma cópia](#live-copy-with-non-live-copy-pages) ativa existente, essa nova página também pode ser configurada como uma cópia em tempo real de um blueprint diferente. Isso é conhecido como uma Live Copy aninhada, onde o comportamento da segunda (interna) live copy é afetado pela primeira (externa) live copy da seguinte maneira:

* Um roll-out profundo acionado para a live copy de nível superior pode ser continuado na live copy aninhada (por exemplo, se o acionador corresponder).
* Quaisquer links entre as fontes serão reescritos dentro das cópias online.

   Por exemplo, os links do segundo ao primeiro blueprint serão regravados como links da live copy aninhada/segundo para a primeira live copy.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Se você mover/renomear uma página dentro da ramificação da live copy, então (internamente) isso será tratado como uma live copy aninhada para permitir que o AEM rastreie os relacionamentos.

#### Cópias online empilhadas {#stacked-live-copies}

Uma live copy é conhecida como uma Live Copy empilhada quando é criada como filho de uma live copy rasa. Ele se comporta da mesma maneira que uma Live Copy [aninhada](#nested-live-copies).

### Configurações de origem, Blueprints e Blueprint {#source-blueprints-and-blueprint-configurations}

Qualquer página ou ramificação de páginas pode ser usada como a origem de uma live copy.

No entanto, o MSM também permite definir uma configuração de blueprint que especifica um caminho de origem. Os benefícios do uso de uma configuração blueprint são:

* Permita que o autor use a opção **Rollout** em um blueprint - para (explicitamente) modificações de envio para cópias online herdadas deste blueprint.
* Permitir que o autor use **Criar site**; isso permite que o usuário selecione facilmente os idiomas e configure a estrutura da live copy.
* Defina uma configuração padrão de implementação para cópias online que tenham uma relação com o blueprint.

A origem de uma live copy pode ser páginas regulares ou páginas cobertas por uma configuração blueprint - ambos são casos de uso válidos.

A fonte forma o plano para a live copy. O blueprint é definido quando você:

* [Criar uma configuração do Blueprint](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   A configuração define (antecipadamente) as páginas a serem usadas para criar a live copy.

* [Criar uma cópia online de uma página](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   As páginas usadas para criar a live copy (as páginas de origem) são as páginas de blueprint.

   A página de origem pode ser referenciada por uma configuração de blueprint, ou não.

### Implantação e sincronização {#rollout-and-synchronize}

Uma implementação é a ação MSM central que sincroniza cópias ao vivo com a origem. Você pode executar implantações manualmente ou elas podem ocorrer automaticamente:

* Uma configuração [de](#rollout-configurations) implantação pode ser definida para que [eventos](/help/sites-administering/msm-sync.md#rollout-triggers) específicos possam fazer com que uma implantação ocorra automaticamente.
* Ao criar uma página de blueprint, você pode usar o comando [Rollout](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) para encaminhar alterações para a live copy.

   **O comando Rollout** está disponível em uma página de blueprint referenciada por uma configuração de blueprint.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Ao criar uma página de live copy, você pode usar o comando [Sincronizar](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) para extrair as alterações da origem para a live copy.

   O comando **Sincronizar** está sempre disponível na página de live copy (independentemente de a página de origem/blueprint ser incluída por uma configuração de blueprint).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### Configurações de implementação {#rollout-configurations}

Uma configuração de implantação define quando e como uma live copy é sincronizada com o conteúdo de origem. Uma configuração de implantação consiste em um acionador e uma ou mais ações de sincronização:

* **Acionar**

   Um acionador é um evento que faz com que a sincronização da ação ativa ocorra, como a ativação de uma página de origem. O MSM define os acionadores que você pode usar.

* **Ações de sincronização**

   São executados na live copy para sincronizá-la com a fonte. As ações de exemplo são copiar conteúdo, ordenar nós filhos e ativar a página de cópia online. O MSM fornece várias ações de sincronização.

   >[!NOTE]
   >
   >Você pode criar ações personalizadas para sua instância usando a API Java.

As configurações de implantação podem ser reutilizadas para que mais de uma live copy possa usar a mesma configuração de implantação. Várias configurações [de](/help/sites-administering/msm-sync.md#installed-rollout-configurations) implementação estão incluídas em uma instalação padrão.

### Conflitos de implantação {#rollout-conflicts}

As implantações podem se tornar complicadas, especialmente quando os autores estão editando o conteúdo na fonte e na live copy, portanto é útil estar ciente de como o AEM lida com quaisquer [conflitos que possam ocorrer durante a implantação](/help/sites-administering/msm-rollout-conflicts.md).

### Suspender e cancelar herança e sincronização {#suspending-and-cancelling-inheritance-and-synchronization}

Cada página e componente em uma live copy é associado à página e ao componente de origem por meio de uma relação ativa. A relação ao vivo configura a sincronização do conteúdo de live copy da origem.

Você pode **Suspender** a herança de uma live copy para uma página de live copy para que você possa alterar as propriedades e os componentes da página. Quando você suspende a herança, as propriedades e os componentes da página não são mais sincronizados com a origem.

Ao editar uma página individual, os autores podem **Cancelar herança** para um componente. Quando a herança é cancelada, a relação ao vivo é suspensa e a sincronização não ocorre para esse componente. Cancelar herança e sincronização é útil quando as subseções do conteúdo precisam ser personalizadas.

### Desanexar uma Live Copy {#detaching-a-live-copy}

Você também pode [desanexar uma cópia](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) ao vivo de seu blueprint para remover todas as conexões.

>[!CAUTION]
>
>A ação Detach é permanente e não reversível.

A ação de desanexar remove permanentemente a relação ativa entre uma live copy e sua página de blueprint. Todas as propriedades relevantes para MSM são removidas da live copy e as páginas live copy se tornam uma cópia independente.

>[!NOTE]
>
>Consulte [Desanexar uma Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) para obter detalhes completos; incluindo o impacto relacionado nas páginas sub e pai.

## Etapas padrão para usar o MSM {#standard-steps-for-using-msm}

As etapas a seguir descrevem o procedimento padrão de uso do MSM para reutilizar conteúdo e sincronizar alterações em cópias online.

1. Desenvolver o conteúdo do site de origem.
1. Determine a configuração de implantação a ser usada.

   1. O MSM [instala várias configurações](/help/sites-administering/msm-sync.md#installed-rollout-configurations) de implantação que podem atender a vários casos de uso.
   1. Opcionalmente, você pode [criar uma configuração](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) de implantação, se necessário.

1. Determine onde é necessário [especificar as configurações de implantação a serem usadas](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) e configuradas conforme necessário.
1. Se necessário, [crie uma configuração](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) blueprint que identifique o conteúdo de origem da live copy.
1. [Crie uma cópia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy)ao vivo.
1. Faça alterações no conteúdo de origem, conforme necessário. Você deve usar o processo normal de revisão e aprovação de conteúdo estabelecido pela sua organização.
1. [Implantar](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) o blueprint ou [sincronizar a live copy](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) com as alterações.

## Personalização do MSM {#customizing-msm}

O MSM fornece ferramentas para que sua implementação possa se adaptar às complexidades excepcionais que podem existir ao compartilhar conteúdo:

* **Configurações personalizadas de implantação**
   [Crie uma configuração](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) de implementação quando as configurações de implementação instaladas não atenderem aos seus requisitos. Você pode usar qualquer acionador de implantação e ação de sincronização disponíveis.

* **Ações de sincronização personalizadas**
   [Crie uma ação](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) de sincronização personalizada quando as ações instaladas não atenderem aos requisitos específicos do aplicativo. O MSM fornece uma API Java para criar ações de sincronização personalizadas.

## Práticas recomendadas {#best-practices}

A página Práticas recomendadas [do](/help/sites-administering/msm-best-practices.md) MSM contém informações importantes sobre sua implementação.
