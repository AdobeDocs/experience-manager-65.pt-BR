---
title: Criar projetos de tradução
description: Saiba como criar projetos de tradução no AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Criar projetos de tradução {#creating-translation-projects}

Para criar uma cópia de idioma, dispare um dos seguintes fluxos de trabalho de cópia de idioma disponíveis no painel Referências na interface do usuário do AEM.

* **Criar e traduzir**:Neste fluxo de trabalho, os ativos a serem traduzidos são copiados para a raiz do idioma para o qual você deseja traduzir. Além disso, dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou pode ser executado automaticamente assim que o projeto de tradução for criado.

* **Atualizar cópias** de idioma: Execute esse fluxo de trabalho para traduzir um grupo adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta de destino que já contém ativos convertidos anteriormente.

>[!NOTE]
>
>Os binários de ativos são traduzidos somente se o provedor de serviços de tradução suportar a tradução de binários.

>[!NOTE]
>
>Se você iniciar um fluxo de trabalho de tradução para ativos complexos, como arquivos PDF e InDesign, seus subativos ou representações (se houver) não serão submetidos para conversão.

## Criar e traduzir fluxo de trabalho {#create-and-translate-workflow}

Use o fluxo de trabalho de criação e tradução para gerar cópias de idioma para um idioma específico pela primeira vez. O fluxo de trabalho fornece as seguintes opções:

* Criar somente estrutura
* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar somente estrutura {#create-structure-only}

Use a opção **[!UICONTROL Criar estrutura somente]** para criar uma hierarquia de pasta de destino na raiz do idioma de destino para corresponder à hierarquia da pasta de origem na raiz do idioma de origem. Nesse caso, os ativos de origem são copiados para a pasta de destino. No entanto, nenhum projeto de tradução é gerado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma estrutura na raiz do idioma de destino.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. Na lista Idiomas **[!UICONTROL de]** destino, selecione o idioma para o qual deseja criar uma estrutura de pastas.

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. Na lista **[!UICONTROL Projeto]** , escolha Somente **** Criar estrutura.

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. Click/tap **[!UICONTROL Create]**. A nova estrutura para o idioma de destino é listada em Cópias **[!UICONTROL de idiomas]**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Clique/toque na estrutura da lista e, em seguida, clique/toque em **[!UICONTROL Revelar nos ativos]** para navegar até a estrutura de pastas dentro do idioma de destino.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### Criar um novo projeto de tradução {#create-a-new-translation-project}

Se você usar essa opção, os ativos a serem traduzidos serão copiados para a raiz do idioma para o qual você deseja traduzir. Dependendo das opções escolhidas, um projeto de tradução é criado para os ativos no console Projetos. Dependendo das configurações, o projeto de tradução pode ser iniciado manualmente ou executado automaticamente assim que o projeto de tradução for criado.

1. Na interface do usuário do Assets, selecione a pasta de origem para a qual deseja criar uma cópia de Idioma.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Na lista Idiomas **[!UICONTROL de]** destino, selecione os idiomas para os quais deseja criar uma estrutura de pastas.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Na lista **[!UICONTROL Projeto]** , selecione **[!UICONTROL Criar um novo projeto]** de tradução.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. No campo Título **[!UICONTROL do]** projeto, informe um título para o projeto.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Click/tap **[!UICONTROL Create]**. Os ativos da pasta de origem são copiados para as pastas de destino das localidades selecionadas na etapa 4.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Para navegar até a pasta, selecione a cópia de idioma e clique em **[!UICONTROL Revelar em Ativos]**.

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. Navegue até o console Projetos. A pasta de tradução é copiada para o console Projetos.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Abra a pasta para exibir o projeto de tradução.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Clique/toque no projeto para abrir a página de detalhes.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Para exibir o status do trabalho de tradução, clique nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Para obter mais detalhes sobre status de trabalhos, consulte [Monitorando o Status de um Trabalho](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de Tradução.

1. Navegue até a interface do usuário Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   >[!NOTE]
   >
   >Este recurso está disponível para ativos e pastas. Quando um ativo é selecionado em vez de uma pasta, toda a hierarquia de pastas até a raiz do idioma é copiada para criar uma cópia do idioma para o ativo.

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project}

Se você usar essa opção, o fluxo de trabalho de tradução será executado para os ativos adicionados à pasta de origem após executar um fluxo de trabalho de tradução anterior. Somente os ativos recém-adicionados são copiados para a pasta de destino que contém ativos convertidos anteriormente. Nenhum novo projeto de tradução é criado neste caso.

1. Na interface do usuário Ativos, navegue até a pasta de origem que contém ativos não convertidos.
1. Selecione um ativo que deseja traduzir e abra o painel **** Referência. A seção Cópias **[!UICONTROL de]** idioma exibe o número de cópias de tradução atualmente disponíveis.
1. Clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]**. Uma lista de cópias de tradução disponíveis é exibida.
1. Clique/toque em **[!UICONTROL Criar e traduzir]** na parte inferior.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Na lista Idiomas **[!UICONTROL de]** destino, selecione os idiomas para os quais deseja criar uma estrutura de pastas.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Na lista **[!UICONTROL Projeto]** , selecione **[!UICONTROL Adicionar ao projeto]** de tradução existente para executar o fluxo de trabalho de tradução na pasta.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Se você escolher a opção **[!UICONTROL Adicionar ao projeto]** de tradução existente, seu projeto de tradução será adicionado a um projeto pré-existente somente se as configurações do projeto corresponderem exatamente às configurações do projeto pré-existente. Caso contrário, um novo projeto será criado.

1. Na lista Projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Click/tap **[!UICONTROL Create]**. Os ativos a serem convertidos são adicionados à pasta de destino. A pasta atualizada está listada na seção Cópias de **[!UICONTROL idioma]** .

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Navegue até o console Projetos e abra o projeto de tradução existente ao qual você adicionou.
1. Clique/toque na exibição do projeto de tradução na página de detalhes do projeto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

   >[!NOTE]
   >
   >Se você excluir a entrada para tags ou metadados, nenhuma tag ou metadados será traduzida para qualquer um dos ativos.

   >[!NOTE]
   >
   >Se você usar Tradução automática, os binários de ativos não serão traduzidos.

   >[!NOTE]
   >
   >Se o ativo adicionado ao trabalho de tradução incluir subativos, selecione os subativos e remova-os para que a tradução continue sem falhas.

1. Para iniciar a tradução dos ativos, clique/toque na seta no bloco Trabalho **[!UICONTROL de]** tradução e selecione **[!UICONTROL Iniciar]** na lista.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Uma mensagem notifica o início do trabalho de tradução.

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. Para exibir o status do trabalho de tradução, clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Para obter mais detalhes, consulte [Monitorando o Status de um Trabalho](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de Tradução.

1. Após a conclusão da tradução, o status é alterado para Pronto para Revisão. Navegue até a interface do usuário Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

## Atualizar cópias de idioma {#update-language-copies}

Execute esse fluxo de trabalho para traduzir qualquer conjunto adicional de ativos e incluí-lo em uma cópia de idioma para uma localidade específica. Nesse caso, os ativos convertidos são adicionados à pasta de destino que já contém ativos convertidos anteriormente. Dependendo da escolha das opções, um projeto de tradução é criado ou um projeto de tradução existente é atualizado para os novos ativos. O fluxo de trabalho de cópias de idioma de atualização inclui as seguintes opções:

* Criar um novo projeto de tradução
* Adicionar ao projeto de tradução existente

### Criar um novo projeto de tradução {#create-a-new-translation-project-1}

Se você usar essa opção, um projeto de tradução será criado para o conjunto de ativos para os quais você deseja atualizar uma cópia de idioma.

1. Na interface do usuário Ativos, selecione a pasta de origem na qual você adicionou um ativo.
1. Abra o painel **[!UICONTROL Referências]** e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.
1. Marque a caixa de seleção antes de Cópias **[!UICONTROL de]** idioma e selecione a pasta de destino correspondente à localidade apropriada.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Clique/toque em **[!UICONTROL Atualizar cópias]** de idioma na parte inferior.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Na lista **[!UICONTROL Projeto]** , escolha **[!UICONTROL Criar um novo projeto]** de tradução.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. No campo Título **[!UICONTROL do]** projeto, informe um título para o projeto.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Clique/toque em **[!UICONTROL Iniciar]**.
1. Navegue até o console Projetos. A pasta de tradução é copiada para o console Projetos.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Abra a pasta para exibir o projeto de tradução.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Clique/toque no projeto para abrir a página de detalhes.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Para iniciar a tradução dos ativos, clique na seta no bloco Trabalho **[!UICONTROL de]** tradução e selecione **[!UICONTROL Iniciar]** na lista.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Uma mensagem notifica o início do trabalho de tradução.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Para exibir o status do trabalho de tradução, clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Para obter mais detalhes sobre status de trabalhos, consulte [Monitorando o Status de um Trabalho](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)de Tradução.

1. Navegue até a interface do usuário Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

### Adicionar ao projeto de tradução existente {#add-to-existing-translation-project-1}

Se você usar essa opção, o conjunto de ativos será adicionado a um projeto de tradução existente para atualizar a cópia de idioma para a localidade escolhida.

1. Na interface do usuário Ativos, selecione a pasta de origem na qual você adicionou uma pasta de ativos.
1. Abra o painel **** Referências e clique/toque em Cópias **[!UICONTROL de]** idioma em **[!UICONTROL Cópias]** para exibir a lista de cópias de idioma.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Marque a caixa de seleção antes de Cópias **[!UICONTROL de]** idioma, que seleciona todas as cópias de idioma. Cancele a seleção de outras cópias, exceto a cópia de idioma (cópias) correspondente às localidades para as quais você deseja traduzir.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Clique/toque em **[!UICONTROL Atualizar cópias]** de idioma na parte inferior.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. Na lista **[!UICONTROL Projeto]** , escolha **[!UICONTROL Adicionar ao projeto]** de tradução existente.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Na lista Projeto **[!UICONTROL de tradução]** existente, selecione um projeto para adicionar o ativo para conversão.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Clique/toque em **[!UICONTROL Iniciar]**.
1. Consulte as etapas 9 a 14 de [Adicionar ao projeto](translation-projects.md#add-to-existing-translation-project) de tradução existente para concluir o restante do procedimento.

## Criar cópias de idioma temporárias {#creating-temporary-language-copies}

Quando você executa um fluxo de trabalho de tradução para atualizar uma cópia de idioma com versões editadas dos ativos originais, a cópia de idioma existente é preservada até que você aprove os ativos convertidos. O AEM Assets armazena os ativos recém-traduzidos em um local temporário e atualiza a cópia de idioma existente depois que você aprova explicitamente os ativos. Se você rejeitar o(s) ativo(s), a cópia de idioma permanecerá inalterada.

1. Clique/toque na pasta raiz de origem em Cópias **[!UICONTROL de]** idioma para as quais você já criou uma cópia de idioma e clique/toque em **[!UICONTROL Revelar nos ativos]** para abrir a pasta nos ativos AEM.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Na interface do usuário do Assets, selecione um ativo que já tenha sido convertido e clique/toque no ícone **[!UICONTROL Editar]** na barra de ferramentas para abrir o ativo no modo de edição.
1. Edite o ativo e salve as alterações.
1. Execute as etapas 2 a 14 do procedimento [Adicionar ao projeto](#add-to-existing-translation-project) de tradução existente para atualizar a cópia de idioma.
1. Clique/toque nas reticências na parte inferior do bloco Trabalho **[!UICONTROL de]** tradução. Na lista de ativos na página Trabalho **[!UICONTROL de]** tradução, é possível exibir claramente o local temporário onde a versão traduzida do ativo é armazenada.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Marque a caixa de seleção ao lado de **[!UICONTROL Título]**.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Aceitar tradução]** e, em seguida, clique/toque em **[!UICONTROL Aceitar]** na caixa de diálogo para substituir o ativo convertido na pasta de destino pela versão traduzida do ativo editado.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >Para permitir que o fluxo de trabalho de tradução atualize o(s) ativo(s) de destino, aceite o ativo e os metadados.

   Clique/toque em **[!UICONTROL Rejeitar tradução]** para manter a versão traduzida originalmente do ativo na raiz da localidade de destino e rejeitar a versão editada.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Navegue até o console Ativos e abra a página Propriedades de cada um dos ativos traduzidos para exibir os metadados traduzidos.

Para obter dicas sobre como traduzir metadados para ativos com eficiência, consulte [5 etapas para traduzir metadados](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)de forma eficiente.
