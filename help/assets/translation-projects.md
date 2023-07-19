---
title: Criar projetos de tradução
description: Saiba como criar projetos de tradução no [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Translation
exl-id: 8990feca-cfda-4974-915e-27aa9d8f2ee1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 15%

---

# Criar projetos de tradução {#creating-translation-projects}

Para criar uma cópia de idioma, acione um dos seguintes workflows de cópia de idioma disponíveis no painel Referências na [!DNL Experience Manager] interface do usuário.

* **Criar e traduzir**: nesse fluxo de trabalho, os ativos que serão traduzidos são copiados para a raiz do idioma para o qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console de Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução é criado.

* **Atualizar cópias de idioma**: execute este fluxo de trabalho para traduzir um grupo adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos traduzidos são adicionados à pasta de destino que já contém ativos traduzidos anteriormente.

>[!PREREQUISITES]
>
>* Os usuários que criam projetos de tradução são membros do grupo `projects-administrators`.
>* O provedor de serviços de tradução oferece suporte à tradução de binários.

## Criar e traduzir fluxo de trabalho {#create-and-translate-workflow}

Use o fluxo de trabalho criar e traduzir para gerar cópias de idioma para um idioma específico pela primeira vez. O fluxo de trabalho fornece as seguintes opções:

* Criar somente estrutura.
* Criar um novo projeto de tradução.
* Adicionar ao projeto de tradução existente.

### Criar somente estrutura {#create-structure-only}

Use a opção **[!UICONTROL Somente criar estrutura]** para criar uma hierarquia de pasta de destino na raiz do idioma de destino para corresponder à hierarquia da pasta de origem na raiz do idioma de origem. Nesse caso, os ativos de origem são copiados na pasta de destino. No entanto, nenhum projeto de tradução é gerado.

1. No [!DNL Assets] , selecione a pasta de origem para a qual deseja criar uma estrutura na raiz do idioma de destino.

1. Abra o **[!UICONTROL Referências]** e clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]**.

   ![Cópias de idioma](assets/translation-language-copies.png)

1. Clique em **[!UICONTROL Criar e traduzir]**. No **[!UICONTROL Idiomas de destino]** selecione o idioma para o qual deseja criar uma estrutura de pastas.

1. Na lista **[!UICONTROL Projeto]**, escolha **[!UICONTROL Somente criar estrutura]**.

1. Clique em **[!UICONTROL Criar]**. A nova estrutura do idioma de destino está listada em **[!UICONTROL Cópias de idioma]**.

   ![cópias de idioma](assets/lang-copy2.png)

1. Clique na estrutura da lista e clique em **[!UICONTROL Revelar no Assets]** para navegar até a estrutura de pastas no idioma de destino.

   ![revelar-em-ativos](assets/reveal-in-assets.png)

### Criar um novo projeto de tradução {#create-a-new-translation-project}

Se você usar essa opção, os ativos a serem traduzidos serão copiados para a raiz do idioma para o qual você deseja traduzir. Dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console de Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou executado automaticamente assim que o projeto de tradução é criado.

1. No [!DNL Assets] , selecione a pasta de origem para a qual deseja criar uma cópia de idioma.
1. Abra o **[!UICONTROL Referências]** e clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Clique em **[!UICONTROL Criar e traduzir]** na parte inferior.

1. No **[!UICONTROL Idiomas de destino]** selecione os idiomas para os quais deseja criar uma estrutura de pastas.

1. No **[!UICONTROL Projeto]** selecione **[!UICONTROL Criar um novo projeto de tradução]**.

1. No campo **[!UICONTROL Título do projeto]**, informe um título para o projeto.

1. Clique em **[!UICONTROL Criar]**. [!DNL Assets] da pasta de origem são copiadas para as pastas de destino das localidades selecionadas na etapa 4.

   ![cópias de idioma](assets/lang-copy2.png)

1. Para navegar até a pasta, selecione a cópia de idioma e clique em **[!UICONTROL Revelar no Assets]**.

   ![revelar-em-ativos](assets/reveal-in-assets.png)

1. Navegue até o console Projetos. A pasta de tradução é copiada para o console de Projetos.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Abra a pasta para exibir o projeto de tradução.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Clique no projeto para abrir a página de detalhes.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior da **[!UICONTROL Tarefa de tradução]** bloco.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Para obter mais detalhes sobre os status do trabalho, consulte [Monitorar o status de um trabalho de tradução](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Navegue até a [!DNL Assets] e abra a página [!UICONTROL Propriedades] para cada um dos ativos traduzidos para exibir os metadados traduzidos.

   ![exibir os metadados traduzidos na página Propriedades do ativo](assets/translated-metadata-asset-properties.png)

   *Figura: Metadados traduzidos na página de propriedades do ativo.*

   >[!NOTE]
   >
   >Esse recurso está disponível para ativos e pastas. Quando um ativo é selecionado em vez de uma pasta, a hierarquia inteira de pastas até a raiz de idioma é copiada para criar uma cópia de idioma para o ativo.

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project}

Se você usar essa opção, o fluxo de trabalho de tradução será executado para os ativos adicionados à pasta de origem após a execução de um fluxo de trabalho de tradução anterior. Somente os ativos adicionados recentemente são copiados para a pasta de destino que contém ativos traduzidos anteriormente. Nenhum novo projeto de tradução é criado nesse caso.

1. No [!DNL Assets] Interface do usuário do, navegue até a pasta de origem que contém ativos não traduzidos.
1. Selecione um ativo que deseja traduzir e abra o **[!UICONTROL painel Referência]**. A seção **[!UICONTROL Cópias de idioma]** exibe o número de cópias de tradução atualmente disponíveis.
1. Clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]**. Uma lista de cópias de tradução disponíveis é exibida.
1. Clique em **[!UICONTROL Criar e traduzir]** na parte inferior.

1. No **[!UICONTROL Idiomas de destino]** selecione os idiomas para os quais deseja criar uma estrutura de pastas.

1. Na lista **[!UICONTROL Projeto]**, selecione **[!UICONTROL Adicionar ao projeto de tradução existente]** para executar o fluxo de trabalho de tradução na pasta.

   >[!NOTE]
   >
   >Se você escolher a variável **[!UICONTROL Adicionar ao projeto de tradução existente]** , seu projeto de tradução será adicionado a um projeto pré-existente somente se as configurações do projeto corresponderem exatamente às configurações do projeto pré-existente. Caso contrário, um novo projeto será criado.

1. No **[!UICONTROL Projeto de tradução existente]** , selecione um projeto para adicionar o ativo para tradução.

1. Clique em **[!UICONTROL Criar]**. Os ativos que serão traduzidos são adicionados à pasta de destino. A pasta atualizada está listada na seção **[!UICONTROL Cópias de idioma]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Navegue até o console Projetos e abra o projeto de tradução existente adicionado a.
1. Clique no projeto de tradução para exibir a página de detalhes do projeto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Clique nas reticências na parte inferior do **Tarefa de tradução** mosaico para exibir os ativos no fluxo de trabalho de tradução. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

   >[!NOTE]
   >
   >Se você excluir a entrada de tags ou metadados, nenhuma tag ou metadado será traduzido para qualquer um dos ativos.

   >[!NOTE]
   >
   >Se o ativo que você adicionar ao trabalho de tradução incluir subativos, selecione os subativos e remova-os para que a tradução continue sem falhas.

1. Para iniciar a tradução dos ativos, clique na seta na guia **[!UICONTROL Tarefa de tradução]** mosaico e selecionar **[!UICONTROL Início]** da lista.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Uma mensagem notifica o início do trabalho de tradução.

1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior da **[!UICONTROL Tarefa de tradução]** bloco.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Para obter mais detalhes, consulte [Monitorar o status de um trabalho de tradução](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Depois que a tradução for concluída, o status será alterado para Pronto para revisão. Navegue até a [!DNL Assets] e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

## Atualizar cópias de idioma {#update-language-copies}

Execute este fluxo de trabalho para traduzir qualquer conjunto adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos traduzidos são adicionados à pasta de destino que já contém ativos traduzidos anteriormente. Dependendo da escolha de opções, um projeto de tradução é criado ou um projeto de tradução existente é atualizado para os novos ativos. O workflow Atualizar cópias de idioma inclui as seguintes opções:

* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar um novo projeto de tradução {#create-a-new-translation-project-1}

Se você usar essa opção, um projeto de tradução será criado para o conjunto de ativos para o qual você deseja atualizar uma cópia de idioma.

1. No [!DNL Assets] Selecione a pasta de origem na qual você adicionou um ativo.
1. Abra o **[!UICONTROL Referências]** e clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.
1. Marque a caixa de seleção ao lado de **[!UICONTROL Cópias de idioma]** e selecione a pasta de destino correspondente ao local adequado.

   ![selecionar cópia de idioma](assets/lang-copy1.png)

1. Clique em **[!UICONTROL Atualizar cópias de idioma]** na parte inferior.

1. No **[!UICONTROL Projeto]** escolha **[!UICONTROL Criar um novo projeto de tradução]**.

1. No campo **[!UICONTROL Título do projeto]**, informe um título para o projeto.

1. Clique em **[!UICONTROL Início]**.
1. Navegue até o console Projetos. A pasta de tradução é copiada para o console de Projetos.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Abra a pasta para exibir o projeto de tradução.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Clique no projeto para abrir a página de detalhes.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para iniciar a tradução dos ativos, clique na seta na guia **[!UICONTROL Tarefa de tradução]** mosaico e selecionar **[!UICONTROL Início]** da lista.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Uma mensagem notifica o início do trabalho de tradução.

1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior da **[!UICONTROL Tarefa de tradução]** bloco.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Para obter mais detalhes sobre os status do trabalho, consulte [Monitorar o status de um trabalho de tradução](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Navegue até a [!DNL Assets] e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project-1}

Se você usar essa opção, o conjunto de ativos será adicionado a um projeto de tradução existente para atualizar a cópia de idioma para o local escolhido.

1. No [!DNL Assets] Interface do usuário do, selecione a pasta de origem na qual você adicionou uma pasta de ativos.
1. Abra o **[!UICONTROL Painel Referências]** e clique em **[!UICONTROL Cópias de idioma]** em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Marque a caixa de seleção ao lado de **[!UICONTROL Cópias de idioma]**, que seleciona todas as cópias de idioma. Desmarque as outras cópias, exceto a cópia de idioma (cópias) correspondente às localidades para as quais você deseja traduzir.

   ![selecionar cópia de idioma](assets/lang-copy1.png)

1. Clique em **[!UICONTROL Atualizar cópias de idioma]** na parte inferior.

1. No **[!UICONTROL Projeto]** escolha **[!UICONTROL Adicionar ao projeto de tradução existente]**.

1. No **[!UICONTROL Projeto de tradução existente]** , selecione um projeto para adicionar o ativo para tradução.

1. Clique em **[!UICONTROL Início]**.
1. Consulte as etapas 9 a 14 de [Adicionar ao projeto de tradução existente](translation-projects.md#add-to-existing-translation-project) para completar o resto do procedimento.

## Criar cópias temporárias de idioma {#creating-temporary-language-copies}

Quando você executa um fluxo de trabalho de tradução para atualizar uma cópia de idioma com versões editadas de ativos originais, a cópia de idioma existente é preservada até que você aprove o(s) ativo(s) traduzido(s). [!DNL Adobe Experience Manager Assets] O armazena os ativos recém-traduzidos em um local temporário e atualiza a cópia de idioma existente depois que você aprova explicitamente os ativos. Se você rejeitar os ativos, a cópia de idioma permanecerá inalterada.

1. Clique na pasta raiz de código-fonte em **[!UICONTROL Cópias de idioma]** para o qual você já criou uma cópia de idioma e clique em **[!UICONTROL Revelar no Assets]** para abrir a pasta no [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. No [!DNL Assets] selecione um ativo que você já traduziu e clique em **[!UICONTROL Editar]** na barra de ferramentas para abrir o ativo no modo de edição.
1. Edite o ativo e salve as alterações.
1. Execute as etapas 2 a 14 do [Adicionar ao projeto de tradução existente](#add-to-existing-translation-project) procedimento para atualizar a cópia de idioma.
1. Clique nas reticências na parte inferior do **[!UICONTROL Tarefa de tradução]** bloco. Na lista de ativos na lista **[!UICONTROL Tarefa de tradução]** é possível visualizar claramente o local temporário onde a versão traduzida do ativo está armazenada.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Marque a caixa de seleção ao lado de **[!UICONTROL Título]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Aceitar tradução]** ![aceitar tradução](assets/do-not-localize/thumb-up.png) e clique em **[!UICONTROL Aceitar]** na caixa de diálogo para substituir o ativo traduzido na pasta de destino pela versão traduzida do ativo editado.

   >[!NOTE]
   >
   >Para permitir que o fluxo de trabalho de tradução atualize os ativos de destino, aceite o ativo e os metadados.

   Clique em **[!UICONTROL Rejeitar tradução]** ![rejeitar tradução](assets/do-not-localize/thumb-down.png) para reter a versão originalmente traduzida do ativo na raiz do local de destino e rejeitar a versão editada.

1. Para exibir os metadados traduzidos, navegue até o [!DNL Assets] e abra o [!UICONTROL Propriedades] para cada um dos ativos traduzidos.

## Dicas e limitações {#tips-limitations}

* Se você iniciar um fluxo de trabalho de tradução para ativos complexos, como PDF e [!DNL Adobe InDesign] os arquivos, seus subativos ou representações (se houver) não são enviados para tradução.
* Se você usar a tradução automática, os binários de ativos não serão traduzidos.
