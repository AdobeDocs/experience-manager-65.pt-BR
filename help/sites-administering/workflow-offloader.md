---
title: Descarregamento do fluxo de trabalho de ativos
seo-title: Descarregamento do fluxo de trabalho de ativos
description: Saiba mais sobre o Assets Workflow Offloader.
seo-description: Saiba mais sobre o Assets Workflow Offloader.
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# Descarregamento do fluxo de trabalho de ativos{#assets-workflow-offloader}

O carregador de fluxo de trabalho de ativos permite ativar várias instâncias dos ativos Adobe Experience Manager (AEM) para reduzir a carga de processamento na instância principal (líder). A carga de processamento é distribuída entre a instância líder e as várias instâncias de descarregamento (trabalhador) que você adiciona a ela. A distribuição da carga de processamento de ativos aumenta a eficiência e a velocidade com que o AEM Assets processa ativos. Além disso, ajuda a alocar recursos dedicados para processar ativos de um tipo de MIME específico. Por exemplo, você pode alocar um nó específico em sua topologia para processar ativos do InDesign somente.

## Configurar a topologia do offloader {#configure-offloader-topology}

Use o Configuration Manager para adicionar o URL para a instância líder e os nomes de host de instâncias de offloader para solicitações de conexão na instância líder.

1. Toque/clique no logotipo do AEM e escolha **Ferramentas** > **Operações** > Console **da** Web para abrir o Configuration Manager.
1. No Console da Web, selecione **Sling** > **Topology Management**.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Na página Gerenciamento de topologia, toque/clique no link **Configurar serviço** Discovery.Oak.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Na página Configuração do serviço de descoberta, especifique o URL do conector para a instância líder no campo URLs **do conector de** topologia.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. No campo Lista de permissões do conector de **topologia** , especifique o endereço IP ou os nomes de host das instâncias do offloader que têm permissão para se conectar com a instância de pontilhado. Tap/click **Save**.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Para ver as instâncias do offloader conectadas à instância líder, vá até **Ferramentas** > **Implantação** > **Topologia** e toque/clique na visualização Cluster.

## Desabilitar descarregamento {#disable-offloading}

1. Toque/clique no logotipo do AEM e escolha **Ferramentas** > **Implantação** > **Descarregamento**. A página Navegador **de** descarga exibe tópicos e as instâncias do servidor que podem consumir os tópicos.

   ![chlimage_1-48](assets/chlimage_1-48a.png)

1. Desative o tópico *com/adobe/granite/workflow/offloading* nas instâncias principais com as quais os usuários interagem para carregar ou alterar ativos do AEM.

   ![chlimage_1-49](assets/chlimage_1-49a.png)

## Configurar inicializadores de fluxo de trabalho na instância líder {#configure-workflow-launchers-on-the-leader-instance}

Configure os iniciadores do fluxo de trabalho para usar o fluxo de trabalho de Descarregamento [!UICONTROL de ativos de atualização de] DAM na instância líder, em vez do fluxo de trabalho de ativo **de atualização de** DAM.

1. Toque/clique no logotipo do AEM e escolha **Ferramentas** > **Fluxo de trabalho** > **Iniciadores** para abrir o console Iniciadores de **fluxo de trabalho** .

   ![chlimage_1-50](assets/chlimage_1-50a.png)

1. Localize as duas configurações do Iniciador com o **Nó de tipo de evento Criado** e o **Nó Modificado** , respectivamente, que executam o fluxo de trabalho do Ativo **de atualização do** DAM.
1. Para cada configuração, marque a caixa de seleção antes dela e toque/clique no ícone Propriedades **da** Visualização na barra de ferramentas para exibir a caixa de diálogo Propriedades **do** Iniciador.

   ![chlimage_1-51](assets/chlimage_1-51a.png)

1. Na lista **Fluxo de trabalho** , escolha [!UICONTROL DAM Update Asset Offloading (Descarregamento] de ativo de atualização de DAM) e toque/clique em **Save (Salvar**).

   ![chlimage_1-52](assets/chlimage_1-52a.png)

1. Toque/clique no logotipo do AEM e escolha **Ferramentas** > **Fluxo de trabalho** > **Modelos** para abrir a página Modelos **de** fluxo de trabalho.
1. Selecione o fluxo de trabalho [!UICONTROL DAM Update Asset Offloading] e toque/clique em **Editar** na barra de ferramentas para exibir seus detalhes.

   ![chlimage_1-53](assets/chlimage_1-53a.png)

1. Exiba o menu de contexto da etapa de descarga **do fluxo de trabalho do** DAM e escolha **Editar**. Verifique a entrada no campo Tópico **do** trabalho da guia Argumentos **** genéricos da caixa de diálogo de configuração.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

## Desabilitar os iniciadores do fluxo de trabalho nas instâncias do offloader {#disable-the-workflow-launchers-on-the-offloader-instances}

Desative os iniciadores de fluxo de trabalho que executam o fluxo de trabalho do Ativo **de atualização do** DAM na instância líder.

1. Toque/clique no logotipo do AEM e escolha **Ferramentas** > **Fluxo de trabalho** > **Iniciadores** para abrir o console Iniciadores de **fluxo de trabalho** .

   ![chlimage_1-55](assets/chlimage_1-55a.png)

1. Localize as duas configurações do Iniciador com o **Nó de tipo de evento Criado** e o **Nó Modificado** , respectivamente, que executam o fluxo de trabalho do Ativo **de atualização do** DAM.
1. Para cada configuração, marque a caixa de seleção antes dela e toque/clique no ícone Propriedades **da** Visualização na barra de ferramentas para exibir a caixa de diálogo Propriedades **do** Iniciador.

   ![chlimage_1-56](assets/chlimage_1-56a.png)

1. Na seção **Ativar** , arraste o controle deslizante para desativar o iniciador do fluxo de trabalho e toque/clique em **Salvar** para desativá-lo.

   ![chlimage_1-57](assets/chlimage_1-57a.png)

1. Carregue qualquer ativo de imagem de tipo na instância de pontilhado. Verifique as miniaturas geradas e devolvidas para o ativo pela instância descarregada.

