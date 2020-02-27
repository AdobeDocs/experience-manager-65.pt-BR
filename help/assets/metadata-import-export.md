---
title: Importar e exportar metadados de ativos em massa
description: Importar e exportar metadados de ativos em massa
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Importar e exportar metadados de ativos em massa {#import-and-export-asset-metadata-in-bulk}

O AEM Assets permite importar metadados de ativos em massa usando um arquivo CSV. É possível fazer atualizações em massa para os ativos carregados recentemente ou os ativos existentes importando um arquivo CSV. Você também pode assimilar metadados de ativos em massa de sistemas de terceiros em formato CSV.

## Importar metadados {#import-metadata}

A importação de metadados é assíncrona e não impede o desempenho do sistema. A atualização simultânea dos metadados para vários ativos pode exigir muitos recursos devido à atividade de write-back de XMP se o sinalizador de fluxo de trabalho estiver marcado. Planeje tal importação durante o uso de servidor simplificado para que o desempenho para outros usuários não seja afetado.

>[!NOTE]
>
>Para importar metadados em namespaces personalizados, primeiro registre os namespaces.

1. Navegue até a interface do usuário Ativos e toque/clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. No menu, selecione **[!UICONTROL Metadados]**.
1. Na página **[!UICONTROL Importação de metadados]**, toque/clique em **[!UICONTROL Selecionar arquivo]**. Selecione o arquivo CSV com os metadados.
1. Especifique os seguintes parâmetros:

   | Parâmetros de importação de metadados | Descrição |
   |:---|:---|
   | [!UICONTROL Tamanho do lote] | Número de ativos em um lote para os quais os metadados devem ser importados. O valor padrão é 50. O valor máximo é 100. |
   | [!UICONTROL Separador de campos] | O valor padrão é `,` (uma vírgula). É possível especificar qualquer outro caractere. |
   | [!UICONTROL Delimitador de múltiplo valor] | Separador para valores de metadados. O valor padrão é `|`. |
   | [!UICONTROL Inicializar fluxos de trabalho] | False por padrão. Quando definidas como `true` e as configurações padrão do Iniciador estiverem em vigor para o fluxo de trabalho WriteBack de metadados DAM (que grava metadados nos dados binários XMP). Habilitar fluxos de trabalho de inicialização retarda o sistema. |
   | [!UICONTROL Nome de coluna do caminho do ativo] | Define o nome da coluna para o arquivo CSV com ativos. |

1. Toque/clique em **[!UICONTROL Importar]** na barra de ferramentas. Depois que os metadados são importados, uma notificação é enviada para sua caixa de entrada de Notificação. Navegue até a página de propriedade do ativo e verifique se os valores de metadados foram importados corretamente para ativos.

## Exportar metadados {#export-metadata}

É possível exportar metadados para vários ativos em um formato CSV. Os metadados são exportados de forma assíncrona e não afetam o desempenho do sistema. Para exportar metadados, o AEM percorre as propriedades do nó do ativo `jcr:content/metadata` e seus nós filhos e exporta as propriedades de metadados em um arquivo CSV.

Alguns casos de uso para exportar metadados em massa são:

* Importe os metadados em um sistema de terceiros ao migrar ativos.
* Compartilhe metadados de ativos com uma equipe de projeto mais ampla.
* Teste ou audite os metadados para verificar a conformidade.
* Externalize os metadados para localização separada.

1. Selecione a pasta de ativos que contém os ativos para os quais deseja exportar metadados. Na barra de ferramentas, selecione **[!UICONTROL Exportar metadados]**.
1. Na caixa de diálogo Exportação de metadados, especifique um nome para o arquivo CSV. Para exportar metadados para ativos em subpastas, selecione **[!UICONTROL Incluir ativos em subpastas]**.

   ![Interface e opções para exportar metadados de todos os ativos em uma](assets/export_metadata_page.png "folderInterface e opções para exportar metadados de todos os ativos em uma pasta")

1. Selecione as opções desejadas. Forneça um nome de arquivo e, se necessário, uma data.

1. No campo **[!UICONTROL Propriedades a serem exportadas]** , especifique se deseja exportar todas as propriedades ou propriedades específicas. Se você escolher Propriedades seletivas a serem exportadas, adicione as propriedades desejadas.

1. Na barra de ferramentas, toque/clique em **[!UICONTROL Exportar]**. Uma mensagem confirma que os metadados são exportados. Feche a mensagem.
1. Abra a notificação da caixa de entrada do trabalho de exportação. Selecione o trabalho e clique em **[!UICONTROL Abrir]** na barra de ferramentas. Para baixar o arquivo CSV com os metadados, toque/clique em **[!UICONTROL Download de CSV]** na barra de ferramentas. Clique em **[!UICONTROL Fechar]**.

   ![Caixa de diálogo para baixar o arquivo CSV que contém os metadados exportados em massa](assets/csv_download.png)

   *Figura: Caixa de diálogo para baixar o arquivo CSV que contém os metadados exportados em massa*

>[!MORELIKETHIS]
>
>* [Importação e exportação de metadados no AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

