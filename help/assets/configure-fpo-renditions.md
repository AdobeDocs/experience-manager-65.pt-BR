---
title: Gerar para representações somente posicionamento para o Adobe InDesign
description: Gere representações FPO de ativos novos e existentes usando o fluxo de trabalho do Experience Manager Assets e o ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Gerar para representações somente posicionamento para o Adobe InDesign {#fpo-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Este artigo |

Ao colocar ativos de grande porte do Experience Manager em documentos do Adobe InDesign, um profissional criativo deve aguardar por um tempo substancial depois que eles [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está bloqueado de usar o InDesign. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos InDesign para começar. Quando a saída final é necessária, digamos, para fluxos de trabalho de impressão e publicação, os ativos originais de resolução completa substituem a representação temporária em segundo plano. Essa atualização assíncrona em segundo plano acelera o processo de design para melhorar a produtividade e não dificulta o processo criativo.

O Adobe Experience Manager (AEM) fornece representações que são usadas somente para posicionamento (FPO). Essas renderizações de FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção. Se uma representação FPO não estiver disponível para um ativo, o Adobe InDesign usará o ativo original. Esse mecanismo de fallback garante que o fluxo de trabalho criativo continue sem interrupções.

## Abordagem para gerar representações FPO {#approach-to-generate-fpo-renditions}

O Experience Manager permite que vários métodos processem imagens que podem ser usadas para gerar as representações FPO. Os dois métodos mais comuns são usar fluxos de trabalho de Experience Manager integrados e usar o ImageMagick. Usando esses dois métodos, você configura a geração de representação de ativos recém-carregados e dos ativos que existem no Experience Manager.

Você pode usar o ImageMagick para processar imagens, incluindo para gerar representações de FPO. Essas representações têm resolução reduzida, ou seja, as dimensões em pixels da representação são proporcionalmente reduzidas se a imagem original tiver PPI maior que 72. Consulte [instale e configure o ImageMagick para funcionar com o Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Usando o fluxo de trabalho incorporado do Experience Manager | Uso do fluxo de trabalho do ImageMagick | Observações |
|--- |--- |---|--- |
| Para novos ativos | Habilitar representação FPO ([ajuda](#generate-renditions-of-new-assets-using-aem-workflow)) | Adicionar linha de comando ImageMagick no fluxo de trabalho do Experience Manager ([ajuda](#generate-renditions-of-new-assets-using-imagemagick)) | O Experience Manager executa o fluxo de trabalho Ativos de atualização do DAM para cada upload. |
| Para ativos existentes | Ative a representação FPO em um novo fluxo de trabalho dedicado do Experience Manager ([ajuda](#generate-renditions-of-existing-assets-using-aem-workflow)) | Adicione a linha de comando ImageMagick em um novo fluxo de trabalho dedicado do Experience Manager ([ajuda](#generate-renditions-of-existing-assets-using-imagemagick)) | As representações de FPO dos ativos existentes podem ser criadas sob demanda ou em massa. |

>[!CAUTION]
>
>Crie os workflows para gerar representações modificando uma cópia dos workflows padrão. Impede que as alterações sejam substituídas quando o Experience Manager for atualizado, por exemplo, instalando um novo service pack.

## Gerar representações de novos ativos usando o fluxo de trabalho do Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

A seguir estão as etapas para configurar o modelo de fluxo de trabalho Ativo de atualização do DAM para ativar a geração de representação:

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**. Selecionar **[!UICONTROL Ativo de atualização DAM]** modelo e clique em **[!UICONTROL Editar]**.

1. Selecionar **[!UICONTROL Processar miniaturas]** e clique em **[!UICONTROL Configurar]**.

1. Clique em **[!UICONTROL Representação de FPO]** guia . Selecionar **[!UICONTROL Habilitar criação de representação FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Ajuste o **[!UICONTROL Qualidade]** e adicionar ou modificar **[!UICONTROL Lista de Formatos]** conforme necessário. Por padrão, a lista de tipos MIME para gerar a representação FPO é pjpeg, jpeg, jpg, gif, png, x-png e tiff. Clique em **[!UICONTROL Concluído]**.

   >[!NOTE]
   >
   >A geração de representação é compatível com os tipos de arquivo JPEG, GIF, PNG, TIFF, PSD e BMP.

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.

>[!NOTE]
>
>Imagens com mais de 1280 pixels em um lado não retêm as dimensões de pixel na representação FPO.

## Gerar representações de novos ativos usando o ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

No Experience Manager, o fluxo de trabalho Ativos de atualização do DAM é executado quando um novo ativo é carregado. Para usar o ImageMagick para processar representações de ativos recém-carregados, adicione um novo comando ao modelo de fluxo de trabalho.

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. Selecionar **[!UICONTROL Ativo de atualização DAM]** modelo e clique em **[!UICONTROL Editar]**.

1. Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo e procure pela etapa da linha de comando.

1. Arraste o **[!UICONTROL Linha de comando]** e adicione-o antes da **[!UICONTROL Processar miniaturas]** etapa.

1. Selecionar **[!UICONTROL Linha de comando]** e clique em **[!UICONTROL Configurar]**.

1. Adicionar as informações desejadas como personalizadas **[!UICONTROL Título]** e **[!UICONTROL Descrição]**. Por exemplo, a representação FPO (fornecida pelo ImageMagick).

1. No **[!UICONTROL Argumentos]** guia , adicione relevante **[!UICONTROL Tipos Mime]** para fornecer uma lista de formatos de arquivo nos quais o comando se aplica.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. No **[!UICONTROL Argumentos]** na guia , no **[!UICONTROL Comandos]** , adicione um comando ImageMagick relevante para gerar representações FPO.

   Abaixo está um exemplo de comando que gera renderizações FPO em formato JPEG, com resolução reduzida para 72 PPI, com configuração de qualidade de 10% e processa arquivos Adobe Photoshop com várias camadas nivelando a saída:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.

Para obter informações detalhadas sobre os recursos da linha de comando ImageMagick, consulte [https://imagemagick.org](https://imagemagick.org).

## Gerar representações de ativos existentes usando o fluxo de trabalho do Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Para usar o fluxo de trabalho do Experience Manager para gerar a renderização FPO dos ativos existentes, crie um modelo de fluxo de trabalho dedicado que use a opção de renderização FPO integrada.

1. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. Para criar um modelo, clique em **[!UICONTROL Criar]** > **[!UICONTROL Criar modelo]**.

1. Adicione um **[!UICONTROL Título]** e **[!UICONTROL Nome]**.

1. Selecione o modelo e clique em **[!UICONTROL Editar]**. Clique em **[!UICONTROL Informações da página]** > **[!UICONTROL Abrir propriedades]** e selecione **[!UICONTROL Fluxo de trabalho transitório]**. Isso melhora a escalabilidade e o desempenho.

1. Clique em ******[!UICONTROL Salvar e fechar]**.

1. Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo e procure a etapa de miniatura do processo.

1. Selecionar **[!UICONTROL Processar miniaturas]** e clique em **[!UICONTROL Configurar]**. Siga as [configuração para gerar a representação de novos ativos usando o fluxo de trabalho do Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Para ativar as alterações, clique em **[!UICONTROL Sincronizar]**.


## Gerar representações de ativos existentes usando o ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Para usar os recursos de processamento do ImageMagick para gerar a representação FPO dos ativos existentes, crie um modelo de fluxo de trabalho dedicado que use a linha de comando ImageMagick para fazer isso.

1. Siga as etapas 1 a 3 de [configuração para gerar a representação de ativos existentes usando o fluxo de trabalho do Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow) seção.

1. Siga as etapas 4 a 8 de [configuração para gerar a representação de novos ativos usando o ImageMagick](#generate-renditions-of-new-assets-using-imagemagick) seção.


## Exibir representações de FPO {#view-fpo-renditions}

Você pode verificar as renderizações de FPO geradas após a conclusão do workflow. Na interface do usuário do Experience Manager Assets, clique no ativo para abrir uma visualização grande. Abra o painel à esquerda e selecione Representações. Como alternativa, use o atalho de teclado `Alt + 3` quando a visualização estiver aberta.

Clique em **[!UICONTROL Representação de FPO]** para carregar a visualização. Como opção, você pode clicar com o botão direito do mouse na representação e salvá-la em seu sistema de arquivos.

![rendition_list](assets/rendition_list.png)


## Dicas e limitações {#tips-limitations}

* Para usar a configuração baseada em ImageMagick, instale o ImageMagick na mesma máquina que o Experience Manager.
* Para gerar representações FPO de muitos ativos ou de todo o repositório, planeje e execute os workflows durante a duração do tráfego baixo. Gerar representações de FPO para um grande número de ativos é uma atividade que consome muitos recursos e os servidores de Experience Manager devem ter capacidade de processamento e memória disponíveis suficientes.
* Para obter desempenho e escalabilidade, consulte [Ajustar o ImageMagick](performance-tuning-guidelines.md).
* Para obter informações sobre o tratamento de linha de comando genérico de ativos, consulte [manipulador de linha de comando para processar ativos](media-handlers.md).
