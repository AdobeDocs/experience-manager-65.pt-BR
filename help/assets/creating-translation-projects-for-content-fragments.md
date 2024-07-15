---
title: Criação de projetos de tradução para fragmentos de conteúdo
description: Saiba como traduzir fragmentos de conteúdo no Adobe Experience Manager.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
feature: Content Fragments
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# Criação de projetos de tradução para fragmentos de conteúdo {#creating-translation-projects-for-content-fragments}

Além dos ativos, o Adobe Experience Manager (AEM) Assets oferece suporte a fluxos de trabalho de cópia de idioma para [fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) (incluindo variações). Nenhuma otimização adicional é necessária para executar fluxos de trabalho de cópia de idioma em fragmentos de conteúdo. Em cada fluxo de trabalho, todo o fragmento de conteúdo é enviado para tradução.

Os tipos de fluxos de trabalho que você pode executar em fragmentos de conteúdo são exatamente semelhantes aos tipos de fluxos de trabalho que você executa para ativos. Além disso, as opções disponíveis em cada tipo de fluxo de trabalho correspondem às opções disponíveis nos tipos de fluxos de trabalho correspondentes para ativos.

Você pode executar os seguintes tipos de fluxos de trabalho de cópia de idioma em fragmentos de conteúdo:

**Criar e traduzir**

Nesse fluxo de trabalho, os fragmentos de conteúdo a serem traduzidos são copiados para a raiz do idioma para o qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os fragmentos de conteúdo no console de Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução é criado.

**Atualizar cópias de idioma**

Quando o fragmento de conteúdo de origem é atualizado ou modificado, o fragmento de conteúdo correspondente específico do local/idioma requer nova tradução. O fluxo de trabalho de cópias de idioma de atualização traduz um grupo adicional de fragmentos de conteúdo e o inclui em uma cópia de idioma para um local específico. Nesse caso, os fragmentos de conteúdo traduzidos são adicionados à pasta de destino que já contém fragmentos de conteúdo traduzidos anteriormente.

## Criar e traduzir fluxo de trabalho {#create-and-translate-workflow}

O fluxo de trabalho Create and translate inclui as seguintes opções. As etapas processuais associadas a cada opção são semelhantes às associadas à opção correspondente para ativos.

* Somente criar estrutura: para etapas de procedimento, consulte [Criar estrutura somente para ativos](translation-projects.md#create-structure-only).
* Criar um projeto de tradução: para obter etapas de procedimento, consulte [Criar um projeto de tradução para ativos](translation-projects.md#create-a-new-translation-project).
* Adicionar ao projeto de tradução existente: para obter as etapas do procedimento, consulte [Adicionar ao projeto de tradução existente para ativos](translation-projects.md#add-to-existing-translation-project).

## Atualizar fluxo de trabalho de cópias de idioma {#update-language-copies-workflow}

O fluxo de trabalho Atualizar cópias de idioma inclui as seguintes opções. As etapas processuais associadas a cada opção são semelhantes às associadas à opção correspondente para ativos.

* Criar um projeto de tradução: para etapas de procedimento, consulte [Criar um projeto de tradução para ativos](translation-projects.md#create-a-new-translation-project) (fluxo de trabalho de atualização).
* Adicionar ao projeto de tradução existente: para obter as etapas do procedimento, consulte [Adicionar ao projeto de tradução existente para ativos](translation-projects.md#add-to-existing-translation-project) (fluxo de trabalho de atualização).

Também é possível criar cópias temporárias de idioma para fragmentos semelhantes à maneira como você cria cópias temporárias para ativos. Para obter detalhes, consulte [Criação de cópias temporárias de idioma para ativos](translation-projects.md#creating-temporary-language-copies).

## Tradução de fragmentos de mídia mista {#translating-mixed-media-fragments}

O AEM permite traduzir fragmentos de conteúdo que incluem vários tipos de ativos de mídia e coleções. Se você traduzir um fragmento de conteúdo que inclui ativos em linha, as cópias traduzidas desses ativos serão armazenadas na raiz do idioma de destino.

Se o fragmento de conteúdo incluir uma coleção, os ativos na coleção serão traduzidos junto com o fragmento de conteúdo. As cópias traduzidas dos ativos são armazenadas na raiz do idioma de destino apropriada em um local que corresponde ao local físico dos ativos de origem na raiz do idioma de origem.

Para poder traduzir fragmentos de conteúdo que incluem mídia mista, edite primeiro a estrutura de tradução padrão para permitir a tradução de ativos e coleções em linha associados a fragmentos de conteúdo.

1. Clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Implantação > Cloud Service]**.
1. Localize **[!UICONTROL Integração de Tradução]** em **[!UICONTROL Adobe Marketing Cloud]** e clique em **[!UICONTROL Mostrar Configurações]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. Na lista de configurações disponíveis, clique em **[!UICONTROL Configuração padrão (configuração de Integração de Tradução)]** para abrir a página **[!UICONTROL Configuração padrão]**.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. Clique em **[!UICONTROL Editar]** na barra de ferramentas para exibir a caixa de diálogo **[!UICONTROL Configuração de tradução]**.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. Navegue até a guia **[!UICONTROL Assets]** e escolha **[!UICONTROL Media Assets embutido e Coleções associadas]** na lista **[!UICONTROL Traduzir Assets de Fragmento de Conteúdo]**. Clique em **[!UICONTROL OK]** para salvar as alterações.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. Na pasta raiz em inglês, abra um fragmento de conteúdo.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. Clique no ícone **[!UICONTROL Inserir ativo]**.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. Insira um ativo no fragmento de conteúdo.

   ![inserir ativo no fragmento de conteúdo](assets/column-view.png)

1. Clique no ícone **[!UICONTROL Associar conteúdo]**.

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. Clique em **[!UICONTROL Associar conteúdo]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. Selecione uma coleção e inclua-a no fragmento de conteúdo. Clique em **[!UICONTROL Salvar]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. Selecione o fragmento de conteúdo e clique no ícone **[!UICONTROL GlobalNav]**.
1. Selecione **[!UICONTROL Referências]** no menu para exibir o painel **[!UICONTROL Referências]**.

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. Clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]** para exibir as cópias de idioma.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. Clique em **[!UICONTROL Criar e traduzir]** na parte inferior do painel para exibir a caixa de diálogo **[!UICONTROL Criar e traduzir]**.

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. Selecione o idioma de destino na lista **[!UICONTROL Idiomas de Destino]**.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. Selecione o tipo de projeto de tradução na lista **[!UICONTROL Projeto]**.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. Especifique o título do projeto na caixa **[!UICONTROL Título do projeto]** e clique em **Criar**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. Navegue até o console **[!UICONTROL Projetos]** e abra a pasta do projeto de tradução que você criou.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. Clique no bloco do projeto para abrir a página de detalhes do projeto.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. No bloco Tarefa de tradução, verifique o número de ativos a serem traduzidos.
1. No bloco **[!UICONTROL Trabalho de tradução]**, inicie o trabalho de tradução.

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. Clique nas reticências na parte inferior do bloco Tarefa de tradução para exibir o status do trabalho de tradução.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. Clique no fragmento de conteúdo para verificar o caminho dos ativos associados traduzidos.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. Revise a cópia de idioma da coleção no console Coleções.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   Observe que somente o conteúdo da coleção é traduzido. A coleção em si não é traduzida.

1. Navegue até o caminho do ativo associado traduzido. Observe que o ativo traduzido é armazenado na raiz de idioma de destino.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. Navegue até os ativos na coleção que são traduzidos junto com o fragmento de conteúdo. Observe que as cópias traduzidas dos ativos são armazenadas na raiz do idioma de destino apropriada.

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >Os procedimentos para adicionar um fragmento de conteúdo a um projeto existente ou executar workflows de atualização são semelhantes aos procedimentos correspondentes para ativos. Para obter orientação sobre esses procedimentos, consulte os procedimentos descritos para ativos.
