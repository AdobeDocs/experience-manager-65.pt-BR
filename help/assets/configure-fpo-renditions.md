---
title: Gerar para representações somente de posicionamento para o Adobe InDesign
description: Gerar representações FPO de ativos novos e existentes usando o fluxo de trabalho do Experience Manager Assets e o ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Gerar para representações somente de posicionamento para o Adobe InDesign {#fpo-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Este artigo |

Ao colocar ativos de grande porte do Experience Manager em documentos do Adobe InDesign, um profissional de criação deve aguardar um tempo considerável depois de [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário é impedido de usar o InDesign. Isso interrompe o fluxo de criação e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos do InDesign para começar. Quando a saída final é necessária, digamos para workflows de impressão e publicação, os ativos originais e de resolução completa substituem a representação temporária em segundo plano. Essa atualização assíncrona em segundo plano acelera o processo de design para melhorar a produtividade e não dificulta o processo criativo.

O Adobe Experience Manager (AEM) fornece representações usadas somente para posicionamento (FPO). Essas representações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção. Se uma representação FPO não estiver disponível para um ativo, a Adobe InDesign usará o ativo original. Esse mecanismo de fallback garante que o workflow criativo continue sem interrupções.

## Abordagem para gerar representações FPO {#approach-to-generate-fpo-renditions}

O Experience Manager permite que muitos métodos processem imagens que podem ser usadas para gerar as representações FPO. Os dois métodos mais comuns são usar workflows de Experience Manager incorporados e usar ImageMagick. Usando esses dois métodos, você configura a geração de representação de ativos recém-carregados e dos ativos que existem no Experience Manager.

Você pode usar o ImageMagick para processar imagens, incluindo para gerar representações FPO. Essas representações têm a resolução reduzida, ou seja, as dimensões em pixels da representação são proporcionalmente reduzidas se a imagem original tiver um PPI maior que 72. Consulte [instalar e configurar o ImageMagick para funcionar com o Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Uso do fluxo de trabalho criado no Experience Manager | Utilização do fluxo de trabalho do ImageMagick | Observações |
|--- |--- |---|--- |
| Para novos ativos | Habilitar representação FPO ([ajuda](#generate-renditions-of-new-assets-using-aem-workflow)) | Adicionar linha de comando do ImageMagick no fluxo de trabalho do Experience Manager ([help](#generate-renditions-of-new-assets-using-imagemagick)) | O Experience Manager executa o fluxo de trabalho DAM Update Assets para cada upload. |
| Para ativos existentes | Habilitar representação FPO em um novo fluxo de trabalho de Experience Manager dedicado ([help](#generate-renditions-of-existing-assets-using-aem-workflow)) | Adicionar linha de comando do ImageMagick em um fluxo de trabalho de Experience Manager novo e dedicado ([help](#generate-renditions-of-existing-assets-using-imagemagick)) | As representações FPO dos ativos existentes podem ser criadas sob demanda ou em massa. |

>[!CAUTION]
>
>Crie os workflows para gerar representações modificando uma cópia dos workflows padrão. Isso evita que suas alterações sejam substituídas quando o Experience Manager é atualizado, por exemplo, ao instalar um novo service pack.

## Gerar representações de novos ativos usando o fluxo de trabalho do Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

Veja a seguir as etapas para configurar o modelo de fluxo de trabalho Ativo de atualização do DAM para habilitar a geração de representação:

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**. Selecione o modelo de **[!UICONTROL Ativo de atualização do DAM]** e clique em **[!UICONTROL Editar]**.

1. Selecione a etapa **[!UICONTROL Processar miniaturas]** e clique em **[!UICONTROL Configurar]**.

1. Clique na guia **[!UICONTROL Representação FPO]**. Selecione **[!UICONTROL Habilitar criação de representação FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Ajuste a **[!UICONTROL Qualidade]** e adicione ou modifique os valores da **[!UICONTROL Lista de Formatos]** conforme necessário. Por padrão, a lista de tipos MIME para gerar a representação FPO é pjpeg, jpeg, jpg, gif, png, x-png e tiff. Clique em **[!UICONTROL Concluído]**.

   >[!NOTE]
   >
   >A geração de representação é compatível com os tipos de arquivos JPEG, GIF, PNG, TIFF, PSD e BMP.

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.

>[!NOTE]
>
>Imagens com mais de 1280 pixels em um lado não retêm as dimensões de pixel na representação FPO.

## Gerar representações de novos ativos usando o ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

No Experience Manager, o fluxo de trabalho Atualizar ativo do DAM é executado quando um novo ativo é carregado. Para usar o ImageMagick para processar representações de ativos recém-carregados, adicione um novo comando ao modelo de fluxo de trabalho.

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.

1. Selecione o modelo de **[!UICONTROL Ativo de atualização do DAM]** e clique em **[!UICONTROL Editar]**.

1. Clique em **[!UICONTROL Alternar Painel Lateral]** no canto superior esquerdo e procure a etapa da linha de comando.

1. Arraste a etapa **[!UICONTROL Linha de Comando]** e adicione-a antes da etapa **[!UICONTROL Processar Miniaturas]**.

1. Selecione a etapa **[!UICONTROL Linha de comando]** e clique em **[!UICONTROL Configurar]**.

1. Adicione as informações desejadas como **[!UICONTROL Título]** e **[!UICONTROL Descrição]** personalizados. Por exemplo, representação FPO (ativado por ImageMagick).

1. Na guia **[!UICONTROL Argumentos]**, adicione **[!UICONTROL Tipos MIME]** relevantes para fornecer uma lista de formatos de arquivo aos quais o comando se aplica.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. Na guia **[!UICONTROL Argumentos]**, na seção **[!UICONTROL Comandos]**, adicione um comando ImageMagick relevante para gerar representações FPO.

   Abaixo está um exemplo de comando que gera representações FPO no formato JPEG, reduz a resolução para 72 PPI, com 10% de configuração de qualidade, e lida com arquivos Adobe Photoshop de várias camadas, nivelando a saída:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.

Para obter informações detalhadas sobre os recursos de linha de comando do ImageMagick, consulte [https://imagemagick.org](https://imagemagick.org).

## Gerar representações de ativos existentes usando o fluxo de trabalho do Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Para usar o fluxo de trabalho Experience Manager para gerar a representação FPO dos ativos existentes, crie um modelo de fluxo de trabalho dedicado que use a opção de representação FPO integrada.

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.

1. Para criar um modelo, clique em **[!UICONTROL Criar]** > **[!UICONTROL Criar Modelo]**.

1. Adicione um **[!UICONTROL Título]** e um **[!UICONTROL Nome]** significativos.

1. Selecione o modelo e clique em **[!UICONTROL Editar]**. Clique em **[!UICONTROL Informações da Página]** > **[!UICONTROL Abrir Propriedades]** e selecione **[!UICONTROL Fluxo de Trabalho Temporário]**. Isso melhora a escalabilidade e o desempenho.

1. Clique em **[!UICONTROL Salvar]** e **[!UICONTROL Fechar]**.

1. Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo e procure a etapa de miniatura do processo.

1. Selecione **[!UICONTROL Processar miniaturas]** e clique em **[!UICONTROL Configurar]**. Siga a [configuração para gerar a representação de novos ativos usando o fluxo de trabalho do Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.


## Gerar representações de ativos existentes usando o ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Para usar os recursos de processamento do ImageMagick para gerar a representação FPO dos ativos existentes, crie um modelo de fluxo de trabalho dedicado que use a linha de comando ImageMagick para fazer isso.

1. Siga a etapa 1 a etapa 3 da configuração [ para gerar a representação de ativos existentes usando a seção de fluxo de trabalho do Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow).

1. Siga a etapa 4 a etapa 8 da configuração [ para gerar a representação de novos ativos usando a seção ImageMagick](#generate-renditions-of-new-assets-using-imagemagick).


## Exibir representações FPO {#view-fpo-renditions}

Você poderá verificar as representações FPO geradas após a conclusão do fluxo de trabalho. Na interface do usuário do Experience Manager Assets, clique no ativo para abrir uma visualização grande. Abra o painel à esquerda e selecione Representações. Como alternativa, use o atalho de teclado `Alt + 3` quando a visualização estiver aberta.

Clique em **[!UICONTROL Representação FPO]** para carregar sua visualização. Como opção, você pode clicar com o botão direito do mouse na representação e salvá-la em seu sistema de arquivos.

![lista_de_representações](assets/rendition_list.png)


## Dicas e limitações {#tips-limitations}

* Para usar a configuração baseada no ImageMagick, instale o ImageMagick na mesma máquina que o Experience Manager.
* Para gerar representações FPO de muitos ativos ou de todo o repositório, planeje e execute os workflows durante a duração de tráfego baixo. Gerar representações FPO para um grande número de ativos é uma atividade que consome muitos recursos e os servidores Experience Manager devem ter capacidade de processamento e memória suficientes disponíveis.
* Para obter desempenho e escalabilidade, consulte [Ajustar ImageMagick](performance-tuning-guidelines.md).
* Para manipulação de linha de comando genérica de ativos, consulte [manipulador de linha de comando para processar ativos](media-handlers.md).
