---
title: Instalar e configurar o ImageMagick para trabalhar com os ativos AEM
description: Saiba mais sobre o software ImageMagick, como instalá-lo, configurar a etapa do processo da linha de comando e usá-lo para editar, compor e gerar miniaturas de imagens.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# Instalar e configurar o ImageMagick para trabalhar com os ativos AEM{#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick é um plug-in de software para criar, editar, compor ou converter imagens de bitmap. Ele pode ler e gravar imagens em vários formatos (mais de 200), incluindo PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF e SVG. Use o ImageMagick para redimensionar, virar, espelhar, girar, distorcer, distorcer e transformar imagens. Você também pode ajustar as cores da imagem, aplicar vários efeitos especiais ou desenhar texto, linhas, polígonos, elipses e curvas usando o ImageMagick.

Use o manipulador de mídia do Adobe Experience Manager (AEM) na linha de comando para processar imagens por meio do ImageMagick. Para trabalhar com vários formatos de arquivo usando o ImageMagick, consulte Práticas [recomendadas para formatos de arquivo de](/help/assets/assets-file-format-best-practices.md)Ativos. Para saber mais sobre todos os formatos de arquivo suportados, consulte Formatos [compatíveis com o](/help/assets/assets-formats.md)Assets.

Para processar arquivos grandes usando o ImageMagick, considere requisitos de memória mais altos do que o normal, possíveis alterações necessárias às políticas de IM e o impacto geral no desempenho. Os requisitos de memória dependem de vários fatores, como resolução, profundidade de bits, perfil de cores e formato de arquivo. Se você pretende processar arquivos muito grandes usando o ImageMagick, faça o benchmark adequado do servidor AEM. Alguns recursos úteis são fornecidos no final.

>[!NOTE]
>
>Se você estiver usando o AEM no Adobe Managed Services (AMS), entre em contato com o Atendimento ao cliente da Adobe se planeja processar muitos arquivos PSD ou PSB de alta resolução. O Experience Manager talvez não processe arquivos PSB de alta resolução com mais de 30000 x 23000 pixels.

## Instalação do ImageMagick {#installing-imagemagick}

Várias versões dos arquivos de instalação do ImageMagic estão disponíveis para vários sistemas operacionais. Use a versão apropriada para seu sistema operacional.

1. Baixe os arquivos [de instalação apropriados do](https://www.imagemagick.org/script/download.php) ImageMagick para seu sistema operacional.
1. Para instalar o ImageMagick no disco que hospeda o servidor AEM, inicie o arquivo de instalação.

1. Defina a variável path Ambiente para o diretório de instalação ImageMagic.
1. Para verificar se a instalação foi bem-sucedida, execute o `identify -version` comando.

## Configurar a etapa do processo da linha de comando {#set-up-the-command-line-process-step}

Você pode configurar a etapa do processo da linha de comando para seu caso de uso específico. Execute estas etapas para gerar uma imagem invertida e miniaturas (140x100, 48x48, 319x319 e 1280x1280) cada vez que você adicionar um arquivo de imagem JPEG `/content/dam` no servidor AEM:

1. No servidor AEM, vá para o console Fluxo de trabalho (`https://[aem_server]:[port]/workflow`) e abra o modelo de fluxo de trabalho Atualizar ativo **[!UICONTROL do]** DAM.
1. No modelo de fluxo de trabalho Atualizar ativo **[!UICONTROL do]** DAM, abra a etapa de miniaturas **[!UICONTROL EPS (acionada pelo ImageMagick)]** .
1. Na guia **** Argumentos, adicione `image/jpeg` à lista **[!UICONTROL Mime Types]** .

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Na caixa **[!UICONTROL Comandos]** , digite o seguinte comando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Selecione os sinalizadores **[!UICONTROL Excluir representação]** gerada e **[!UICONTROL Gerar representação]** da Web.

   ![select_flags](assets/select_flags.png)

1. Na guia Imagem **[!UICONTROL ativada pela]** Web, especifique os detalhes para a execução com dimensões de 1280x1280 pixels. Além disso, especifique `image/jpeg` a caixa **[!UICONTROL Tipo]** .

   ![web_enabled_image](assets/web_enabled_image.png)

1. Clique em **[!UICONTROL OK]** para salvar as alterações.

   >[!NOTE]
   >
   >O `convert` `convert` comando pode não ser executado com determinadas versões do Windows (por exemplo, Windows SE), pois está em conflito com o utilitário nativo que faz parte da instalação do Windows. Nesse caso, mencione o caminho completo do utilitário ImageMagick. Por exemplo, especifique,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Abra a etapa **[!UICONTROL Processar miniaturas]** e adicione o tipo MIME `image/jpeg` em **[!UICONTROL Ignorar tipos]** MIME.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Na guia Imagem **[!UICONTROL ativada pela]** Web, adicione o tipo MIME `image/jpeg` sob a Lista **[!UICONTROL Ignorar]**. Clique em **[!UICONTROL OK]** para salvar as alterações.

   ![web_enabled](assets/web_enabled.png)

1. Salve o fluxo de trabalho.
1. Para verificar se o ImageMagic consegue processar imagens corretamente, carregue uma imagem JPG para os ativos AEM. Verifique se uma imagem invertida e as execuções são geradas para ela.

## Reduzindo vulnerabilidades de segurança {#mitigating-security-vulnerabilities}

Há várias vulnerabilidades de segurança associadas ao uso do ImageMagick para processar imagens. Por exemplo, o processamento de imagens enviadas pelo usuário envolve o risco de execução remota de código (RCE).

Além disso, vários plug-ins de processamento de imagens dependem da biblioteca do ImageMagick, incluindo, mas não limitado às imagens do PHP, o rmagick e o clipe de papel de Ruby e o imagemagick do nodejs.

Se você usar o ImageMagick ou uma biblioteca afetada, a Adobe recomenda atenuar as vulnerabilidades conhecidas, executando pelo menos uma das seguintes tarefas (mas, de preferência, ambas):

1. Verifique se todos os arquivos de imagem começam com os [&quot;bytes mágicos&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) esperados correspondentes aos tipos de arquivos de imagem suportados antes de enviá-los para o ImageMagick para processamento.
1. Use um arquivo de política para desativar os codificadores vulneráveis do ImageMagick. A política global para ImageMagick encontra-se em `/etc/ImageMagick`.
