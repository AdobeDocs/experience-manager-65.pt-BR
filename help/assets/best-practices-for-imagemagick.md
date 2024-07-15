---
title: Instalar e configurar o ImageMagick
description: Saiba mais sobre o software ImageMagick, como instalá-lo, configurar a etapa do processo de linha de comando e usá-lo para editar, compor e gerar miniaturas de imagens.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Instalar e configurar o ImageMagick para funcionar com [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick é um plug-in de software para criar, editar, compor ou converter imagens bitmap. Ele pode ler e gravar imagens em vários formatos (mais de 200), incluindo PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF e SVG. Use o ImageMagick para redimensionar, virar, espelhar, girar, distorcer, distorcer e transformar imagens. Você também pode ajustar cores da imagem, aplicar vários efeitos especiais ou desenhar texto, linhas, polígonos, elipses e curvas usando o ImageMagick.

Use o manipulador de mídia [!DNL Adobe Experience Manager] da linha de comando para processar imagens por meio do ImageMagick. Para trabalhar com vários formatos de arquivo usando o ImageMagick, consulte [Práticas recomendadas de formatos de arquivo do Assets](/help/assets/assets-file-format-best-practices.md). Para saber mais sobre todos os formatos de arquivo compatíveis, consulte [formatos compatíveis com o Assets](/help/assets/assets-formats.md).

Para processar arquivos grandes usando o ImageMagick, considere os requisitos de memória mais altos que o normal, as possíveis alterações necessárias às políticas de mensagens instantâneas e o impacto geral no desempenho. Os requisitos de memória dependem de vários fatores, como resolução, profundidade de bits, perfil de cor e formato de arquivo. Se você pretende processar arquivos muito grandes usando o ImageMagick, compare apropriadamente o servidor [!DNL Experience Manager]. Alguns recursos úteis são fornecidos no final.

>[!NOTE]
>
>Se você estiver usando o [!DNL Experience Manager] em [!DNL Adobe Managed Services] (AMS), entre em contato com o Suporte ao Cliente do Adobe se planejar processar muitos arquivos PSD ou PSB de alta resolução. O [!DNL Experience Manager] pode não processar arquivos PSB de resolução muito alta com mais de 30.000 x 23.000 pixels.

## Instalar o ImageMagick {#installing-imagemagick}

Várias versões dos arquivos de instalação do ImageMagic estão disponíveis para vários sistemas operacionais. Use a versão apropriada para seu sistema operacional.

1. Baixe os [arquivos de instalação do ImageMagick](https://www.imagemagick.org/script/download.php) apropriados para o seu sistema operacional.
1. Para instalar o ImageMagick no disco que hospeda o servidor [!DNL Experience Manager], inicie o arquivo de instalação.

1. Defina a variável de ambiente path para o diretório de instalação do ImageMagic.
1. Para verificar se a instalação teve êxito, execute o comando `identify -version`.

## Configurar a etapa do processo da linha de comando {#set-up-the-command-line-process-step}

Você pode configurar a etapa do processo de linha de comando para seu caso de uso específico. Execute estas etapas para gerar uma imagem invertida e miniaturas (140x100, 48x48, 319x319 e 1280x1280) sempre que adicionar um arquivo de imagem de JPEG a `/content/dam` no servidor [!DNL Experience Manager]:

1. No servidor [!DNL Experience Manager], vá para o console Fluxo de trabalho (`https://[aem_server]:[port]/workflow`) e abra o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.
1. No modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**, abra a etapa **[!UICONTROL Miniaturas do EPS (viabilizada pelo ImageMagick)]**.
1. Na **[!UICONTROL guia Argumentos]**, adicione `image/jpeg` à lista **[!UICONTROL Tipos MIME]**.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Na caixa **[!UICONTROL Comandos]**, digite o seguinte comando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Selecione os sinalizadores **[!UICONTROL Excluir representação gerada]** e **[!UICONTROL Gerar representação da Web]**.

   ![select_flags](assets/select_flags.png)

1. Na guia **[!UICONTROL Imagem Habilitada para Web]**, especifique os detalhes da representação com dimensões de 1280x1280 pixels. Além disso, especifique `image/jpeg` na caixa **[!UICONTROL Mimetype]**.

   ![imagem_habilitada_para_Web](assets/web_enabled_image.png)

1. Clique em **[!UICONTROL OK]** para salvar as alterações.

   >[!NOTE]
   >
   >O comando `convert` pode não ser executado com determinadas versões do Windows (por exemplo, Windows SE), porque está em conflito com o utilitário `convert` nativo que faz parte da instalação do Windows. Nesse caso, mencione o caminho completo para o utilitário ImageMagick. Por exemplo, especifique,
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Abra a etapa **[!UICONTROL Processar Miniaturas]** e adicione o tipo MIME `image/jpeg` em **[!UICONTROL Ignorar Tipos MIME]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Na guia **[!UICONTROL Imagem Habilitada para Web]**, adicione o tipo MIME `image/jpeg` na **[!UICONTROL Lista de permissões]**. Clique em **[!UICONTROL OK]** para salvar as alterações.

   ![web_enabled](assets/web_enabled.png)

1. Salve o workflow.

1. Para verificar o processamento correto, carregue uma imagem de JPG para [!DNL Assets]. Após a conclusão do processamento, verifique se uma imagem invertida e as representações são geradas ou não.

## Reduzindo vulnerabilidades de segurança {#mitigating-security-vulnerabilities}

Há várias vulnerabilidades de segurança associadas ao uso do ImageMagick para processar imagens. Por exemplo, o processamento de imagens enviadas pelo usuário envolve o risco de execução remota de código (RCE).

Além disso, vários plug-ins de processamento de imagens dependem da biblioteca ImageMagick, incluindo, mas não limitado a, a imagem do PHP, o Magick e o Clipe de Papel do Ruby e o Imagemagick do Nodejs.

Se você usa o ImageMagick ou uma biblioteca afetada, o Adobe recomenda que você reduza as vulnerabilidades conhecidas executando pelo menos uma das seguintes tarefas (mas preferencialmente ambas):

1. Verifique se todos os arquivos de imagem começam com os [&quot;bytes mágicos&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) esperados, correspondentes aos tipos de arquivos de imagem aos quais você oferece suporte, antes de enviá-los ao ImageMagick para processamento.
1. Use um arquivo de política para desativar os codificadores vulneráveis do ImageMagick. A política global para ImageMagick foi encontrada em `/etc/ImageMagick`.
