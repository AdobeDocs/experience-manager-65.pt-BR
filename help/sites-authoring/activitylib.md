---
title: Gerenciamento de atividades
description: O console Atividades permite criar, organizar e gerenciar as atividades de marketing de suas marcas
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: f510ca08-977d-45d5-86af-c4b7634b01ba
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1937'
ht-degree: 75%

---

# Gerenciamento de atividades{#managing-activities}

O console Atividades permite criar, organizar e gerenciar as [atividades](/help/sites-authoring/personalization.md#activities) de marketing de suas marcas:

* Adicionar marcas.
* Para cada marca, adicione e configure atividades.
* Administrar atividades.

>[!NOTE]
>
>Se estiver usando o Adobe Target como mecanismo de direcionamento, você também poderá [visualizar os dados de desempenho de suas atividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Se estiver usando o teste A/B, você poderá [converter vencedores](#viewing-performance-and-converting-winning-experiences-a-b-test).

No console Atividades, as atividades são organizadas por marca. Você pode usar marcas e pastas para estruturar a organização de suas atividades. Navegue até o console Atividades tocando/clicando em **Personalização** e em **Atividades**.

As atividades estão disponíveis no modo Direcionar para a [criação de conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md), onde você também pode criar atividades. As atividades criadas no modo Direcionamento são exibidas no console Atividades.

As atividades são exibidas com um rótulo descrevendo que tipo de atividade foi definida:

* XT - Direcionamento de experiência do Adobe Target
* A/B - Teste A/B do Adobe Target
* AEM - Direcionamento do Adobe Experience Manager (orientado por contexthub ou clientcontext)

![chlimage_1-114](assets/chlimage_1-114.png)

>[!NOTE]
>
>Os tipos de atividades disponíveis são determinados pelo seguinte:
>
>* Se a opção **xt_only** estiver habilitada no locatário do Adobe Target (clientcode) usado no lado do AEM para se conectar ao Adobe Target AEM, você poderá criar atividades de XT **somente** no.
>
>* Se as opções **xt_only** estiverem **not** habilitadas no locatário do Adobe Target (clientcode), você poderá criar **ambas** atividades XT e A/B no AEM.
>
>**Observação adicional:** as opções **xt_only** são uma configuração aplicada a um determinado locatário do Target (clientcode) e só podem ser modificadas diretamente no Adobe Target. Não é possível ativar ou desativar essa opção no AEM.

>[!CAUTION]
>
>Proteja o nó de configurações de atividade **cq:ActivitySettings** na instância de publicação para que não possa ser acessado por usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte [Pré-requisitos para integração com o Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) para obter informações detalhadas.

## Criação de uma marca usando o console Atividades {#creating-a-brand-using-the-activities-console}

Crie uma marca para a qual deseja gerenciar atividades de marketing.

Ao criar uma marca usando o console Atividades, ela também aparece no [console Ofertas](/help/sites-authoring/offerlib.md), onde é possível criar ofertas para as experiências das suas atividades.

1. No console Navegação, clique em **Personalization**. Clique em **Atividades**.

   ![screen_shot_2018-03-21at151821](assets/screen_shot_2018-03-21at151821.png)

1. No console Atividades, clique em **Criar** depois **Criar Marca**.
1. Selecione o modelo da marca e clique em **Avançar**.
1. Digite um título para a marca conforme desejar que ele seja exibido nos consoles Atividades e Ofertas. Também é possível digitar ou selecionar uma ou mais tags para associar à marca.
1. Clique em **Criar**. Sua marca aparecerá no console Atividades.

## Adicionar/Editar uma atividade usando o console Atividades {#adding-editing-an-activity-using-the-activities-console}

Adicione uma atividade ou edite uma atividade já existente para concentrar seus esforços de marketing em públicos-alvo específicos. Ao criar/editar uma atividade, especifique as seguintes informações:

* **Nome:** o nome da atividade.
* **Mecanismo de definição de metas:** o [AEM](/help/sites-authoring/personalization.md#aem) ou o [Adobe Target](/help/sites-authoring/personalization.md#adobe-target) como mecanismo de conteúdo direcionado.

* **Selecionar uma configuração de destino:** (somente no Adobe Target) a configuração em nuvem que essa atividade deve usar para se conectar ao Adobe Target. Essa opção aparece somente quando o Adobe Target é selecionado para o Mecanismo de direcionamento.
* **Tipo de atividade: **o tipo de atividade — teste A/B ou direcionamento de experiência
* **Objetivo:** (opcional) uma descrição da atividade.
* **Experiências:** mapeamentos entre os nomes de público-alvo e os segmentos de marketing que você está direcionando.
* **Porcentagens de tráfego:** se o teste A/B for selecionado, você poderá alterar a quantidade de tráfego (em porcentagem) de cada experiência.
* **Duração:** o período em que a atividade é aplicada.
* **Prioridade**: a prioridade relativa da atividade. Quando as atividades fornecem conteúdo para os mesmos segmentos de usuários, a atividade de maior prioridade é priorizada.
* **Métrica de meta:** se o Adobe Target for selecionado como o mecanismo de definição de metas, você poderá adicionar métricas de sucesso à atividade. É necessária uma métrica de sucesso.

>[!NOTE]
>
>As novas atividades do Adobe Target precisam ser ***criadas*** no editor de conteúdo direcionado, não no console **Atividades**, pois a sincronização com o Adobe Target falhará.
>
>No entanto, é possível editar atividades já existentes do Adobe Target no console.

Para adicionar uma atividade:

1. Clique na marca para a qual você está criando a atividade, clique em **Criar** e em **Criar atividade**. Se você estiver editando, selecione a atividade e clique em **Editar**.
1. Forneça as seguintes informações e clique em **Avançar**:

   * Um nome para a atividade.
   * O mecanismo de direcionamento a ser usado. O ContextHub (AEM) é selecionado por padrão. Se precisar usar o Adobe Target, crie a atividade no editor de conteúdo direcionado.
   * Se você selecionou Adobe Target como mecanismo de direcionamento, selecione/edite a configuração de nuvem a ser usada para se conectar ao Adobe Target. (Tenha cuidado para não selecionar uma estrutura que você criou para a sua configuração da nuvem).
   * (Opcional) O objetivo ou uma descrição da atividade.
   * Selecione o Tipo de atividade.

1. Adicione uma ou mais experiências à atividade. Clique em **Adicionar experiência**.
1. Se estiver usando o direcionamento do AEM ou o direcionamento de experiência do Adobe Target:

   1. Clique em **Selecionar público-alvo **e selecione o segmento ao qual a sua experiência está direcionado.
   1. Clique em **Adicionar experiência**, digite um nome e clique em **OK**.

   1. Clique em **Avançar**.

   Se estiver usando o teste A/B do Adobe Target:

   1. Clique no lápis na caixa Públicos-alvo para selecionar um público-alvo.
   1. Clique em **Adicionar experiência**, digite um nome e clique em **OK**.

   1. Insira a porcentagem de tráfego que exibirá cada experiência.
   1. Clique em **Avançar**.

1. Para especificar quando a atividade será iniciada, use o menu suspenso **Início** para selecionar um dos seguintes valores:

   * **Quando ativada**: a atividade começa quando a página que contém o conteúdo direcionado é ativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, clique no ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.

1. Para especificar quando a atividade se encerra, use o menu suspenso Término para selecionar um dos seguintes valores:

   * **Quando desativada**: a atividade termina quando a página que contém o conteúdo direcionado é desativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, clique no ícone de calendário, selecione uma data e especifique a hora para encerrar a atividade.

1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.
1. Se estiver usando o Adobe Target como mecanismo de direcionamento, selecione o que deseja medir com essa atividade. Consulte [Configuração da atividade e definição de objetivos](/help/sites-authoring/content-targeting-touch.md) para obter mais informações sobre as métricas de sucesso disponíveis. Selecione pelo menos uma meta.
1. Clique em **Salvar**.

   >[!NOTE]
   >
   >Após criar uma atividade, é necessário publicá-la para que fique disponível.

## Publicação e Cancelamento de publicação de atividades {#publishing-and-unpublishing-activities}

É necessário publicar atividades para disponibilizá-las. Por outro lado, talvez você queira tornar as atividades indisponíveis cancelando a publicação.

>[!NOTE]
>
>Ao cancelar a publicação de uma atividade, o status da atividade não é alterado, a menos que você atualize a página.

Para publicar ou desfazer a publicação de atividades:

1. Clique na marca e na área que contém a atividade que você deseja publicar ou desfazer a publicação.
1. Clique no ícone ao lado da atividade ou atividades que deseja publicar ou desfazer a publicação.

   ![captura de tela_2019-03-05at123846](assets/screen-shot_2019-03-05at123846.png)

1. Para publicar, clique em **Publish**. Para desfazer a publicação, clique em **Desfazer publicação**. Sua atividade ou atividades serão publicadas ou desfarão a publicação, e o status é alterado no console Atividades (pode ser necessário atualizar a página).

## Atividades em instâncias de Autor e de Publicação {#activities-on-author-and-publish-instances}

Quando uma atividade que usa o mecanismo direcionado do Adobe Target é ativada, uma segunda atividade é criada na instância de publicação:

* A atividade na instância do autor rastreia a atividade na instância do autor e é útil para simular a experiência do visitante. A análise gravada para essa atividade reflete somente o que ocorre na instância do autor.
* A atividade na instância de publicação reflete e responde à atividade no servidor de publicação. Esta é a atividade executada no site público. Somente a atividade de publicação é relevante para rastrear e analisar o uso do site público real.

## Visualização de desempenho e conversão de experiências vencedoras (teste A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

É possível ver o desempenho de qualquer atividade do Adobe Target (XT ou A/B). Se estiver usando o teste A/B, você também poderá converter a experiência vencedora, que se tornará a experiência padrão.

Para visualizar o desempenho da atividade e converter experiências vencedoras:

1. Em **Personalization**, clique em **Atividades** para navegar até o console **Atividades**.
1. Clique na marca cujas atividades você deseja ver.
1. Selecione a atividade e clique em **Exibir propriedades**, clique na guia **Relatórios** e selecione a atividade na qual deseja exibir o desempenho/converter experiências vencedoras. Os dados de desempenho são exibidos.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Clique no link **Selecionar vencedor** para promover esta como a experiência padrão.

   A conversão do vencedor faz o seguinte:

   * Desativa a atividade atual
   * Modifica todas as páginas e substitui o conteúdo segmentado pelo conteúdo real da experiência vencedora. O conteúdo da experiência vencedora torna-se parte da página normal **sem** direcionamento.

   ![chlimage_1-116](assets/chlimage_1-116.png)

   Uma experiência vencedora é a aquela que os relatórios indicam que gerou um aumento maior, com base no índice de conversão.

1. Clique em **Sim** para confirmar que deseja converter o vencedor, desabilitando a experiência atual e substituindo-a pelo conteúdo da experiência vencedora.

## Sincronização de atividades com o Adobe Target {#synchronizing-activities-with-adobe-target}

As atividades que usam o mecanismo de direcionamento do Adobe Target são sincronizadas com as campanhas do Adobe Target. Uma atividade é sincronizada automaticamente com o Adobe Target quando as seguintes condições são atendidas:

* A atividade contém pelo menos uma experiência.
* Pelo menos uma experiência contém um segmento mapeado e uma oferta.
* Cada experiência na atividade deve ter o mesmo número de ofertas.

Essas condições se aplicam às atividades nas instâncias de autor e publicação.

Quando uma atividade é sincronizada, uma campanha correspondente é criada no Adobe Target:

* As atividades na instância de publicação têm o mesmo nome que a campanha correspondente do Adobe Target.
* As atividades na instância do autor correspondem às campanhas do Target com o mesmo nome, mais o sufixo `_author`.

![chlimage_1-117](assets/chlimage_1-117.png)

As atividades _author são sincronizadas imediatamente quando a atividade é modificada. A sincronização imediata permite a simulação de atividades com o Client Context ou o ContextHub.

As atividades de publicação são sincronizadas quando a atividade é publicada na instância de publicação do AEM.

## Solução de problemas de sincronização de atividades {#troubleshooting-activity-synchronization}

Quando o AEM sincroniza uma atividade com o Adobe Target, ele inclui uma propriedade dessa atividade denominada `thirdPartyId`. O valor dessa propriedade se baseia no caminho da atividade no repositório do AEM. Nenhuma campanha no Adobe Target pode ter o mesmo valor para a propriedade `thirdPartyId`. Portanto, uma atividade não será sincronizada se uma campanha existente (de um tipo diferente AB, XT) no Adobe Target usar o mesmo valor para `thirdPartyId`.

Essa situação pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target.
1. Em outra instância do AEM, uma atividade é criada com a mesma marca e usando o mesmo nome. A sincronização desta atividade falha ao tentar.

Essa situação também pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target. A atividade é, em seguida, excluída no AEM.
1. Uma atividade é criada com a mesma marca e usando o mesmo nome que a atividade excluída. A sincronização desta atividade falha ao tentar.

Para evitar problemas de sincronização, sempre use nomes exclusivos para atividades. Se uma atividade não for sincronizada, você poderá excluir a campanha no Adobe Target que usa o mesmo nome se essa campanha não estiver sendo usada.

>[!NOTE]
>
>Quando você cria uma campanha no Adobe Target, ele atribui uma propriedade chamada `thirdPartyId t` a cada campanha. Quando você exclui a campanha no Adobe Target, a propriedade `thirdPartyId` não é excluída. Não é possível reutilizar o `thirdPartyId` para campanhas de tipos diferentes (AB, XT) e ele não pode ser removido manualmente. Para evitar esse problema, nomeie cada campanha com um nome exclusivo. Nomes de campanhas não podem ser reutilizados em diferentes tipos de campanha.
>
>Se você usar o mesmo nome no mesmo tipo de campanha, a campanha existente será substituída.
>
>Se, durante a sincronização, você encontrar o erro “A solicitação falhou. `thirdPartyId` já existe”, altere o nome da campanha e sincronize novamente.
