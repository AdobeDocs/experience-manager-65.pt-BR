---
title: Instalar e configurar o ImageMagick
description: Saiba mais sobre o software ImageMagick, como instalá-lo, configurar a etapa do processo da linha de comando e usá-lo para editar, compor e gerar miniaturas de imagens.
contentOwner: AG
role: Administrator
feature: Renditions,Developer Tools
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# Instale e configure o ImageMagick para trabalhar com [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

O ImageMagick é um plug-in de software para criar, editar, compor ou converter imagens de bitmap. Ele pode ler e gravar imagens em vários formatos (mais de 200), incluindo PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF e SVG. Use o ImageMagick para redimensionar, virar, espelhar, girar, distorcer, distorcer e transformar imagens. Você também pode ajustar as cores das imagens, aplicar vários efeitos especiais ou desenhar texto, linhas, polígonos, elipses e curvas usando o ImageMagick.

Use o manipulador de mídia [!DNL Adobe Experience Manager] da linha de comando para processar imagens por meio do ImageMagick. Para trabalhar com vários formatos de arquivo usando o ImageMagick, consulte [Práticas recomendadas para formatos de arquivo de ativos](/help/assets/assets-file-format-best-practices.md). Para saber mais sobre todos os formatos de arquivo compatíveis, consulte [Formatos compatíveis com ativos](/help/assets/assets-formats.md).

Para processar arquivos grandes usando o ImageMagick, considere requisitos de memória mais altos do que o normal, possíveis alterações necessárias às políticas de IM e o impacto geral no desempenho. Os requisitos de memória dependem de vários fatores como resolução, profundidade de bits, perfil de cor e formato de arquivo. Se você pretende processar arquivos muito grandes usando o ImageMagick, faça o benchmark adequado do servidor [!DNL Experience Manager]. Alguns recursos úteis são fornecidos no final.

>[!NOTE]
>
>Se estiver usando [!DNL Experience Manager] em [!DNL Adobe Managed Services] (AMS), entre em contato com o Atendimento ao Cliente do Adobe se planeja processar muitos arquivos PSD ou PSB de alta resolução. [!DNL Experience Manager] pode não processar arquivos PSB de alta resolução que tenham mais de 30000 x 23000 pixels.

## Instalar o ImageMagick {#installing-imagemagick}

Várias versões dos arquivos de instalação do ImageMagic estão disponíveis para vários sistemas operacionais. Use a versão apropriada para seu sistema operacional.

1. Baixe os [arquivos de instalação do ImageMagick](https://www.imagemagick.org/script/download.php) apropriados para seu sistema operacional.
1. Para instalar o ImageMagick no disco que hospeda o servidor [!DNL Experience Manager], inicie o arquivo de instalação.

1. Defina a variável de caminho Ambiente para o diretório de instalação do ImageMagic.
1. Para verificar se a instalação foi bem-sucedida, execute o comando `identify -version`.

## Configure a etapa do processo da linha de comando {#set-up-the-command-line-process-step}

Você pode configurar a etapa do processo da linha de comando para o caso de uso específico. Execute estas etapas para gerar uma imagem invertida e miniaturas (140x100, 48x48, 319x319 e 1280x1280) sempre que adicionar um arquivo de imagem JPEG a `/content/dam` no servidor [!DNL Experience Manager]:

1. No servidor [!DNL Experience Manager], vá para o console Fluxo de trabalho (`https://[aem_server]:[port]/workflow`) e abra o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**.
1. No modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**, abra a etapa **[!UICONTROL Miniaturas do EPS (alimentado pelo ImageMagick)]**.
1. Na guia **[!UICONTROL Argumentos]**, adicione `image/jpeg` à lista **[!UICONTROL Tipos MIME]**.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Na caixa **[!UICONTROL Commands]**, digite o seguinte comando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Selecione os sinalizadores **[!UICONTROL Excluir representação gerada]** e **[!UICONTROL Gerar representação da Web]** .

   ![select_flags](assets/select_flags.png)

1. Na guia **[!UICONTROL Imagem ativada pela Web]** , especifique os detalhes para a representação com dimensões de 1280x1280 pixels. Além disso, especifique `image/jpeg` na caixa **[!UICONTROL Mimetype]**.

   ![web_enabled_image](assets/web_enabled_image.png)

1. Clique em **[!UICONTROL OK]** para salvar as alterações.

   >[!NOTE]
   >
   >O comando `convert` pode não ser executado com determinadas versões do Windows (por exemplo, Windows SE), porque está em conflito com o utilitário nativo `convert` que faz parte da instalação do Windows. Nesse caso, mencione o caminho completo do utilitário ImageMagick. Por exemplo, especifique,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Abra a etapa **[!UICONTROL Processar miniaturas]** e adicione o tipo MIME `image/jpeg` em **[!UICONTROL Ignorar tipos MIME]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Na guia **[!UICONTROL Imagem ativada pela Web]**, adicione o tipo MIME `image/jpeg` sob o **[!UICONTROL Ignorar lista]**. Clique em **[!UICONTROL OK]** para salvar as alterações.

   ![web_enabled](assets/web_enabled.png)

1. Salve o workflow.

1. Para verificar o processamento correto, carregue uma imagem JPG para [!DNL Assets]. Após a conclusão do processamento, verifique se uma imagem invertida e as representações são geradas ou não.

## Reduzindo vulnerabilidades de segurança {#mitigating-security-vulnerabilities}

Há várias vulnerabilidades de segurança associadas ao uso do ImageMagick para processar imagens. Por exemplo, o processamento de imagens enviadas pelo usuário envolve o risco de execução remota de código (RCE).

Além disso, vários plug-ins de processamento de imagens dependem da biblioteca ImageMagick, incluindo, entre outros, a imagem do PHP, o clipe de papel e o clipe de imagem do nodejs.

Se você usar o ImageMagick ou uma biblioteca afetada, o Adobe recomenda atenuar as vulnerabilidades conhecidas executando pelo menos uma das seguintes tarefas (mas, de preferência, ambas):

1. Verifique se todos os arquivos de imagem começam com os [&quot;bytes mágicos&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) esperados correspondentes aos tipos de arquivo de imagem que você suporta antes de enviá-los para o ImageMagick para processamento.
1. Use um arquivo de política para desativar os codificadores vulneráveis do ImageMagick. A política global para ImageMagick é encontrada em `/etc/ImageMagick`.
