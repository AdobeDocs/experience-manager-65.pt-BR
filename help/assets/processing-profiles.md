---
title: Perfis para processamento de metadados, imagens e vídeos
description: Um perfil de um conjunto de regras sobre as opções a serem aplicadas aos ativos carregados em uma pasta. Especifique o perfil de metadados e o perfil de codificação de vídeo a serem aplicados aos ativos de vídeo que você carrega. Para ativos de imagem, também é possível especificar qual perfil de imagem aplicar aos ativos de imagem para que eles sejam cortados corretamente.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 2%

---


# Perfis para processamento de metadados, imagens e vídeos{#profiles-for-processing-metadata-images-and-videos}

Um perfil é uma receita para quais opções se aplicam aos ativos que são carregados em uma pasta. Por exemplo, você pode especificar qual perfil de metadados e perfil de codificação de vídeo aplicar aos ativos de vídeo que você carrega. Ou qual perfil de geração de imagens aplicar aos ativos de imagem para que eles sejam cortados corretamente.

Essas regras podem incluir adição de metadados, recorte inteligente de imagens ou estabelecimento de perfis de codificação de vídeo. No AEM, você pode criar três tipos de perfis, que são abordados detalhadamente nos seguintes links:

* [Perfis de metadados](/help/assets/metadata-profiles.md)
* [perfis de imagem](/help/assets/image-profiles.md)
* [perfis de vídeo](/help/assets/video-profiles.md)

Você deve ter direitos de Administrador para criar, editar e excluir metadados, imagens ou perfis de vídeo.

Depois de criar seus metadados, imagem ou perfil de vídeo, atribua-o a uma ou mais pastas que você usa como destino para os ativos carregados recentemente.

Um conceito importante sobre o uso de perfis nos ativos AEM é que eles estão atribuídos a pastas. Dentro de um perfil estão as configurações na forma de perfis de metadados, juntamente com perfis de vídeo ou perfis de imagem. Essas configurações processam o conteúdo de uma pasta junto com qualquer uma de suas subpastas. Portanto, a forma como você nomeia arquivos e pastas, como você organiza as subpastas e como manipula os arquivos dessas pastas tem um impacto significativo na forma como esses ativos são processados por um perfil.
Usando estratégias de nomenclatura de arquivos e pastas consistentes e apropriadas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo sua coleção de ativos digitais e garantir que os arquivos corretos sejam processados pelo perfil certo.

>[!NOTE]
>
>Os ativos movidos de uma pasta para outra não são reprocessados. Por exemplo, suponha que você tenha a Pasta 1 com o perfil A atribuído a ela e a Pasta 2 com o perfil B atribuído a ela. Se você mover ativos da Pasta 1 para a Pasta 2, os ativos movidos manterão seu processamento original da Pasta 1.
>
>O mesmo ocorre mesmo quando você move ativos entre duas pastas que têm o mesmo perfil atribuído a ele.

## Reprocessando ativos em uma pasta {#reprocessing-assets}

>[!NOTE]
>
>Aplica-se ao modo *Mídia* dinâmica - Scene7 somente no AEM 6.4.6.0 ou posterior.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de processamento existente que você tenha alterado posteriormente.

Por exemplo, suponha que você tenha criado um perfil de imagem e o atribuiu a uma pasta. Todos os ativos de imagem carregados na pasta tinham automaticamente o perfil de imagem aplicado aos ativos. No entanto, depois você decide adicionar uma nova proporção de recorte inteligente ao perfil. Agora, em vez de ter selecionado e carregado novamente os ativos para a pasta, basta executar o *Scene7: Reprocessar fluxo de trabalho de Ativos* .

Você pode executar o fluxo de trabalho de reprocessamento em um ativo cujo processamento falhou na primeira vez. Assim, mesmo se você não tiver editado um perfil de processamento ou aplicado um perfil de processamento, ainda poderá executar o fluxo de trabalho de reprocessamento em uma pasta de ativos a qualquer momento.

Como opção, você pode ajustar o tamanho do lote do fluxo de trabalho de reprocessamento a partir de um padrão de 50 ativos até 1000 ativos. Ao executar o _Scene7: Reprocessar o fluxo de trabalho dos Ativos_ em uma pasta, os ativos são agrupados em lotes e enviados para o servidor de Dynamic Media para processamento. Após o processamento, os metadados de cada ativo em todo o conjunto de lotes são atualizados no AEM. Se o tamanho do lote for muito grande, pode ocorrer um atraso no processamento. Ou, se o tamanho do lote for muito pequeno, pode causar muitas viagens de ida e volta ao servidor de Dynamic Media.

Consulte [Ajustar o tamanho do lote do fluxo de trabalho](#adjusting-load)de reprocessamento.

>[!NOTE]
>
>Se você estiver realizando uma migração em massa de ativos do Dynamic Media Classic para o AEM, deverá habilitar o agente de replicação de Migração no servidor de Dynamic Media. Quando a migração estiver concluída, desative o agente.
O agente de publicação de Migração deve estar desabilitado no servidor de Dynamic Media para que o fluxo de trabalho de Reprocessamento funcione como esperado.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Para reprocessar ativos em uma pasta**:
1. No AEM, na página Ativos, navegue até uma pasta de ativos que tem um perfil de processamento atribuído a ele e para a qual você deseja aplicar o **Scene7: Reprocessar fluxo de trabalho de ativos** ,

   As pastas que tiverem um perfil de processamento já atribuído a ele serão indicadas pela exibição do nome do perfil logo abaixo do nome da pasta na Visualização do cartão.

1. Selecione uma pasta.

   * O fluxo de trabalho considera todos os arquivos na pasta selecionada, recursivamente.
   * Se houver uma ou mais subpastas com ativos na pasta selecionada principal, o fluxo de trabalho reprocessará cada ativo na hierarquia de pastas.
   * Como prática recomendada, você deve evitar executar esse fluxo de trabalho em uma hierarquia de pastas que tenha mais de 1000 ativos.

1. Próximo ao canto superior esquerdo da página, na lista suspensa, clique em **[!UICONTROL Linha do tempo]**.
1. Perto do canto inferior esquerdo da página, à direita do campo Comentário, clique no ícone de carrinho ( **^** ) .

   ![Reprocessar fluxo de trabalho de ativos 1](/help/assets/assets/reprocess-assets1.png)

1. Clique em Fluxo de trabalho do **[!UICONTROL Start]**.
1. Na lista suspensa Fluxo de trabalho **[!UICONTROL do]** Start, escolha **[!UICONTROL Scene7: Reprocessar ativos]**.
1. (Opcional) No campo **Inserir título do campo de texto do fluxo de trabalho** , insira um nome para o fluxo de trabalho. Você pode usar o nome para fazer referência à instância do fluxo de trabalho, se necessário.

   ![Reprocessar ativos 2](/help/assets/assets/reprocess-assets2.png)

1. Clique em **[!UICONTROL Start]** e, em seguida, clique em **[!UICONTROL Confirmar]**.

   Para monitorar o fluxo de trabalho ou verificar seu progresso, na página principal do console do AEM, clique em **[!UICONTROL Ferramentas > Fluxo de trabalho]**. Na página Instâncias do fluxo de trabalho, selecione um fluxo de trabalho. Na barra de menus, clique em **[!UICONTROL Abrir histórico]**. Você também pode encerrar, suspender ou renomear um fluxo de trabalho selecionado na mesma página Instâncias de fluxo de trabalho.

### Ajustar o tamanho do lote do fluxo de trabalho de reprocessamento {#adjusting-load}

(Opcional) O tamanho padrão do lote no fluxo de trabalho de reprocessamento é de 50 ativos por tarefa. O tamanho ideal do lote é regido pelo tamanho médio do ativo e pelos tipos MIME de ativos nos quais o reprocessamento é executado. Um valor mais alto significa que você terá muitos arquivos em um único trabalho de reprocessamento. Dessa forma, o banner de processamento permanece nos ativos AEM por mais tempo. No entanto, se o tamanho médio do arquivo for pequeno a 1 MB ou menos, a Adobe recomenda que você aumente o valor para várias centenas, mas nunca mais que 1000. Se o tamanho médio do arquivo for grande - centenas de megabytes - a Adobe recomenda que você reduza o tamanho do lote para até 10.

**Como opção, ajuste o tamanho do lote do fluxo de trabalho de reprocessamento**

1. No Experience Manager, toque em **[!UICONTROL Adobe Experience Manager]** para acessar o console de navegação global e, em seguida, toque no ícone **[!UICONTROL Ferramentas]** (martelo) > **[!UICONTROL Fluxo de trabalho > Modelos]**.
1. Na página Modelos de fluxo de trabalho, em Visualização de cartão ou Visualização de Lista, selecione **[!UICONTROL Scene7: Reprocessar ativos]**.

   ![Página Modelos de fluxo de trabalho com o Scene7: Reprocessar fluxo de trabalho de Ativos selecionado na Visualização de Cartão](/help/assets/assets-dm/reprocess-assets7.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Editar]**. Uma nova guia do navegador abre o Scene7: Reprocessar página de modelo de fluxo de trabalho dos Ativos.
1. No Scene7: Reprocessar a página de fluxo de trabalho Ativos, próximo ao canto superior direito, toque em **[!UICONTROL Editar]** para &quot;desbloquear&quot; o fluxo de trabalho.
1. No fluxo de trabalho, selecione o componente de Upload em lote do Scene7 para abrir a barra de ferramentas e, em seguida, toque em **[!UICONTROL Configurar]** na barra de ferramentas.

   ![Componente de Upload em lote do Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. Na caixa de diálogo Carregamento em **[!UICONTROL lote para o Scene7—Step Properties]** , defina o seguinte:
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * Selecione **[!UICONTROL Manipulador avançado]** se o seu manipulador avançar para a próxima etapa.
   * No campo **[!UICONTROL Tempo limite]** , informe o tempo limite do processo externo (segundos).
   * No campo **[!UICONTROL Período]** , informe um intervalo de polling (segundos) para testar a conclusão do processo externo.
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * Selecione **[!UICONTROL Avançar no tempo limite]** se desejar avançar quando o tempo limite for atingido. Desmarque se deseja continuar com a caixa de entrada quando o tempo limite for atingido.
   ![Caixa de diálogo Propriedades](/help/assets/assets-dm/reprocess-assets3.png)

1. No canto superior direito da caixa de diálogo Carregamento em **[!UICONTROL lote para o Scene7 - Propriedades]** da etapa, toque em **[!UICONTROL Concluído]**.

1. No canto superior direito do Scene7: Reprocessar a página de modelo de fluxo de trabalho do Assets, toque em **[!UICONTROL Sincronizar]**. Quando você vê **[!UICONTROL Sincronizado]**, o modelo de tempo de execução do fluxo de trabalho é sincronizado e pronto para reprocessar ativos em uma pasta.

   ![Sincronizar o modelo de fluxo de trabalho](/help/assets/assets-dm/reprocess-assets1.png)

1. Feche a guia do navegador que mostra o Scene7: Reprocessar modelo de fluxo de trabalho de Ativos.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
