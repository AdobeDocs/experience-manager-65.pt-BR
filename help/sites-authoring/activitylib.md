---
title: Gerenciamento de atividades
seo-title: Gerenciamento de atividades
description: O console Atividades permite criar, organizar e gerenciar as atividades de marketing das suas marcas
seo-description: O console Atividades permite criar, organizar e gerenciar as atividades de marketing das suas marcas
uuid: 0aebf88e-f298-410a-8c82-4076b671624f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: ef2321a3-cd51-4298-8782-e1a2ca721868
docset: aem65
translation-type: tm+mt
source-git-commit: f62d2d639499c128fd4cafa5f9c39307ae9a607d
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 86%

---


# Gerenciamento de atividades{#managing-activities}

O console Atividades permite criar, organizar e gerenciar as [atividades](/help/sites-authoring/personalization.md#activities) de marketing das suas marcas:

* Adicionar marcas.
* Para cada marca, adicione e configure atividades.
* Administrar atividades.

>[!NOTE]
>
>Se estiver usando o Adobe Target como seu mecanismo de direcionamento, também é possível [visualizar dados de desempenho das suas atividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Se estiver usando testes de A/B, você poderá [converter vencedores](#viewing-performance-and-converting-winning-experiences-a-b-test).

No console Atividades, as atividades são organizadas por marca. É possível usar marcas e pastas para estruturar a organização das suas atividades. Navegue até o console Atividades tocando/clicando em **Personalização** e depois em **Atividades**.

Activities are available in Targeting mode for [authoring targeted content](/help/sites-authoring/content-targeting-touch.md), where you can also create activities. As atividades que você cria no modo Direcionar aparecem no console Atividades.

As atividades são exibidas com um rótulo descrevendo o tipo de atividade definido:

* XT - Direcionamento de experiência do Adobe Target
* A/B - Testes A/B do Adobe Target
* AEM - Direcionamento do Adobe Experience Manager (com base no contexthub ou no clientcontext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Os tipos de atividades disponíveis são determinados pelo seguinte:

>* Se a opção **xt_only** estiver ativada no inquilino do Adobe Target (clientcode) usado no lado do AEM para se conectar ao Adobe Target, você poderá criar **apenas** atividades XT no AEM.
   >
* Se a opção **xt_only** **não** estiver ativada no inquilino do Adobe Target (clientcode), você poderá criar **** atividades XT e A/B no AEM.

**Observação adicional:** a opção **xt_only** é uma configuração aplicada em um determinado inquilino do Target (clientcode) e só pode ser modificada diretamente no Adobe Target. Não é possível ativar ou desativar essa opção no AEM.

>[!CAUTION]
You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.

## Criação de uma marca com o uso do console Atividades {#creating-a-brand-using-the-activities-console}

Crie uma marca cujas atividades de marketing você deseja gerenciar.

When you create a brand using the Activities console, it also appears in the [Offers console](/help/sites-authoring/offerlib.md) where you can create offers for the experiences of your activities.

1. No console Navegação, clique ou toque em **Personalização**. Clique ou toque em **Atividades**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. No console Atividades, clique ou toque em **Criar** e depois em **Criar marca**.
1. Selecione o modelo da marca e clique ou toque em **Próximo**.
1. Digite o título que você deseja atribuir à exibição da marca nos consoles Atividades e Ofertas. Opcionalmente, digite ou selecione uma ou mais tags para associar à marca.
1. Clique ou toque em **Criar**. Sua marca aparece no console Atividades.

## Adição/edição de uma atividade com o uso do console Atividades {#adding-editing-an-activity-using-the-activities-console}

Adicione uma atividade ou edite uma atividade existente para concentrar seus esforços de marketing em públicos-alvo específicos. Ao criar/editar uma atividade, você especifica as seguintes informações:

* **Nome:** o nome da atividade.
* **Mecanismo de definição de metas:** o [AEM](/help/sites-authoring/personalization.md#aem) ou o [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) como mecanismo de conteúdo direcionado.

* **Selecionar uma configuração de destino:** (somente no Adobe Target) a configuração em nuvem que essa atividade deve usar para se conectar ao Adobe Target. Essa opção aparece somente quando o Adobe Target é selecionado para o Mecanismo de direcionamento.
* **Tipo de Atividade: **O tipo de atividade - teste A/B ou direcionamento de experiência
* **Objetivo:** (opcional) uma descrição da atividade.
* **Experiências:** mapeamentos entre os nomes de público-alvo e os segmentos de marketing que você está direcionando.
* **Porcentagens de tráfego:** se o teste A/B for selecionado, você poderá alterar a quantidade de tráfego (em porcentagem) de cada experiência.
* **Duração:** o período em que a atividade é aplicada.
* **Prioridade**: a prioridade relativa da atividade. Quando as atividades fornecem conteúdo para os mesmos segmentos de usuários, a atividade de maior prioridade é priorizada.
* **Métrica de meta:** se o Adobe Target for selecionado como o mecanismo de definição de metas, você poderá adicionar métricas de sucesso à atividade. É necessária uma métrica de sucesso.

>[!NOTE]
As novas atividades do Adobe Target precisam ser ***criadas*** no editor de conteúdo direcionado, não no console **Atividades**, pois a sincronização com o Adobe Target falhará.
No entanto, você pode editar as atividades existentes do Adobe Target no console.

Para adicionar uma atividade:

1. Click or tap the brand for which you are creating the activity, and then click or tap **Create **then** Create Activity. **Se estiver editando, selecione a atividade na tela Área mestre e clique ou toque em **Editar atividade**.
1. Forneça as informações a seguir e clique ou toque em **Próximo**:

   * Um nome para a atividade.
   * O mecanismo de direcionamento que será usado. ContextHub (AEM) é a opção selecionada por padrão. Se precisar usar o Adobe Target, crie a atividade no editor de conteúdo direcionado.
   * Se o Adobe Target estiver selecionado como mecanismo de segmentação, selecione/edite a configuração da nuvem a ser usada para conexão com o Adobe Target. (Cuidado para não selecionar uma estrutura criada para a sua configuração da nuvem.)
   * (Opcional) O objetivo ou uma descrição da atividade.
   * Selecione o Tipo de atividade.

1. Adicione uma ou mais experiências à atividade. Clique ou toque em **Adicionar experiência**.
1. Se estiver usando o direcionamento do AEM ou o direcionamento de experiência do Adobe Target:

   1. Clique ou toque em **Selecione a Audiência **e selecione o segmento cujos públicos alvos de experiência você possui.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.

   1. Clique ou toque em **Próximo**.

   Se estiver usando a opção Teste A/B do Adobe Target:

   1. Clique ou toque no ícone de lápis na caixa de públicos-alvo para selecionar um público-alvo.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.

   1. Insira a porcentagem de tráfego que exibe cada experiência.
   1. Clique ou toque em **Próximo**.


1. Para especificar quando a atividade começa, use o menu suspenso **Início** para selecionar um dos seguintes valores:

   * **Quando ativado:** a atividade é iniciada quando a página que inclui o conteúdo direcionado é ativada.
   * **Data e hora especificada:** um horário específico. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.

1. Para especificar quando a atividade termina, use o menu suspenso Fim para selecionar um dos seguintes valores:

   * **Quando desativado:** a atividade termina quando a página que inclui o conteúdo direcionado é desativada.
   * **Data e hora especificada**: um horário específico. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para concluir a atividade.

1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.
1. Se estiver usando o Adobe Target como mecanismo de direcionamento, selecione o que deseja medir com essa atividade. See [Configuring the Activity and Setting Goals](/help/sites-authoring/content-targeting-touch.md) for more information on the success metrics available. É necessário selecionar pelo menos um objetivo.
1. Clique ou toque em **Salvar**.

   >[!NOTE]
   Depois de criar uma atividade, você precisa publicá-la para que ela fique disponível.

## Publicar e cancelar a publicação de atividades {#publishing-and-unpublishing-activities}

É necessário publicar atividades para disponibilizá-las. Por outro lado, talvez você queira torná-las indisponíveis cancelando essa publicação.

>[!NOTE]
Ao cancelar a publicação de uma atividade, o status da atividade não é alterado a menos que você atualize a página.

Para publicar ou cancelar a publicação de atividades:

1. Clique ou toque na marca e, em seguida, na área que contém a atividade que você deseja publicar ou cuja publicação você deseja cancelar.
1. Toque ou clique no ícone ao lado das atividades que você deseja publicar ou cuja publicação você deseja cancelar.

   ![screen-shot_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Para publicar, toque ou clique em **Publicar**. Para cancelar a publicação, toque ou clique em **Cancelar publicação**. Suas atividades são publicadas ou sua publicação é cancelada, e seu status é alterado no console Atividades (pode exigir uma atualização).

## Atividades em instâncias de Autor e Publicação {#activities-on-author-and-publish-instances}

Quando uma atividade que usa o mecanismo direcionado do Adobe Target é ativada, uma segunda atividade é criada na instância de publicação:

* A atividade na instância de autor rastreia a atividade na instância de autor e é útil para simular a experiência do visitante. A análise registrada para essa atividade reflete apenas o que ocorre na instância de autor.
* A atividade na instância de publicação reflete e responde à atividade no servidor de publicação. Esta é a atividade que é executada no site público-alvo. Somente a atividade de publicação é relevante para rastrear e analisar o uso do site público-alvo real.

## Visualização do desempenho e conversão de experiências vencedoras (teste A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Você pode ver o desempenho de qualquer atividade do Adobe Target (XT ou A/B). Se estiver usando testes A/B, você também poderá converter a experiência vencedora, que então se tornará a experiência padrão.

Para visualizar o desempenho da atividade e converter experiências vencedoras:

1. In **Personalization**, click or tap **Activities** to navigate to the **Activities** console.
1. Clique ou toque na marca cujas atividades você deseja ver.
1. Selecione a atividade e clique ou toque em **Propriedades da exibição**, clique na guia **Relatórios** e selecione a atividade na qual deseja exibir o desempenho/converter experiências vencedoras. Os dados de desempenho são exibidos.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Click or tap the **Push winner** link to push that experience as the default experience.

   A conversão do vencedor faz o seguinte:

   * Desativa a atividade atual
   * Modifica todas as páginas e substitui o conteúdo segmentado pelo conteúdo real da experiência vencedora. The content of the winning experience becomes part of the normal page **without** targeting.

   ![chlimage_1-116](assets/chlimage_1-116.png)

   Uma experiência vencedora é a experiência que gera mais Incentivo nos relatórios, que se baseia na taxa de conversão.

1. Clique ou toque em **Sim** para confirmar que você deseja converter o vencedor, desativando a experiência atual e substituindo-a pelo conteúdo da experiência vencedora.

## Sincronização de atividades com o Adobe Target {#synchronizing-activities-with-adobe-target}

As atividades que usam o mecanismo de direcionamento do Adobe Target são sincronizadas com campanhas do Adobe Target. Uma atividade é sincronizada automaticamente com o Adobe Target quando as seguintes condições são atendidas:

* A atividade contém pelo menos uma experiência.
* Pelo menos uma experiência contém um segmento mapeado e uma oferta.
* Cada experiência na atividade deve ter o mesmo número de ofertas.

Essas condições se aplicam a atividades em instâncias de autor e publicação.

Quando uma atividade é sincronizada, uma campanha correspondente é criada no Adobe Target:

* As atividades na instância de publicação têm o mesmo nome que a campanha do Adobe Target correspondente.
* Activities on the author instance correspond with Target campaigns of the same name with the `_author` suffix.

![chlimage_1-117](assets/chlimage_1-117.png)

As atividades _author são sincronizadas imediatamente quando a atividade é modificada. A sincronização imediata permite a simulação de atividades com o ClientContext ou o ContextHub.

Atividades de publicação são sincronizadas quando a atividade é publicada na instância de publicação do AEM.

## Solução de problemas com a sincronização de atividades {#troubleshooting-activity-synchronization}

When AEM synchronizes an activity with Adobe Target, AEM includes a property of the activity named `thirdPartyId`. O valor dessa propriedade se baseia no caminho da atividade no repositório do AEM. Nenhuma campanha no Adobe Target pode ter o mesmo valor para a propriedade `thirdPartyId`. Portanto, uma atividade não será sincronizada se uma campanha existente (de um tipo diferente AB, XT) no Adobe Target usar o mesmo valor para `thirdPartyId`.

Essa situação pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target.
1. Em outra instância do AEM, uma atividade é criada com a mesma marca e usando o mesmo nome. A sincronização dessa atividade falha ao ser tentada.

Essa situação também pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target. A atividade é então excluída no AEM.
1. Uma atividade é criada com a mesma marca e usando o mesmo nome da atividade excluída. A sincronização dessa atividade falha ao ser tentada.

Para evitar problemas de sincronização, use sempre nomes exclusivos para atividades. Se uma atividade não for sincronizada, você poderá excluir a campanha no Adobe Target que usa o mesmo nome se essa campanha não estiver sendo usada.

>[!NOTE]
When you create a campaign in Adobe Target, it assigns a property called `thirdPartyId t`o each campaign. Quando você exclui a campanha no Adobe Target, a propriedade `thirdPartyId` não é excluída. Não é possível reutilizar o `thirdPartyId` para campanhas de tipos diferentes (AB, XT) e ele não pode ser removido manualmente. Para evitar esse problema, nomeie cada campanha como um nome exclusivo; Assim, os nomes de campanhas não podem ser reutilizados em tipos de campanha diferentes.
Se você usar o mesmo nome no mesmo tipo de campanha, a campanha existente será substituída.
Se, durante a sincronização, você encontrar o erro “A solicitação falhou. `thirdPartyId` já existe”, altere o nome da campanha e sincronize novamente.

