---
title: Biblioteca de transcodificação de imagens
description: Saiba como configurar e usar a Biblioteca de transcodificação de imagens Adobe Imaging, uma solução que pode executar funções essenciais de manipulação de imagens, incluindo codificação, transcodificação, redefinição de imagens e redimensionamento de imagens.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Biblioteca de transcodificação de imagens {#imaging-transcoding-library}

A Biblioteca de transcodificação de imagens proprietária é uma solução de processamento de imagens que pode executar funções principais de manipulação de imagens:

* Codificação
* Transcodificação (conversão de formatos compatíveis)
* Reamostragem de imagens, usando algoritmos PS e Intel IPP
* Profundidade de bits e preservação do perfil de cores
* Compactação de qualidade JPEG
* Redimensionamento de imagem

A Biblioteca de transcodificação de imagens oferece suporte a CMYK e suporte completo a alfa, exceto CMYK -Alpha.

Além de oferecer suporte a uma grande variedade de formatos de arquivo e perfis, a Biblioteca de transcodificação de imagens tem vantagens significativas em relação a outras soluções de terceiros em termos de desempenho, escalabilidade e qualidade. Estes são alguns dos principais benefícios do uso da Biblioteca de transcodificação de imagens:

* **Dimensiona com o aumento do tamanho ou da resolução do arquivo**: O dimensionamento é obtido principalmente pela capacidade patenteada da Biblioteca de transcodificação de imagens de redimensionar ao decodificar arquivos. Essa capacidade garante que o uso da memória em tempo de execução seja sempre ideal e não seja uma função quadrática de aumentar o tamanho do arquivo ou a resolução dos megapixels. A Biblioteca de transcodificação de imagens pode processar arquivos maiores e de alta resolução (contendo megapixels mais altos). Ferramentas de terceiros, como o ImageMagick, não conseguem lidar com arquivos grandes e falhas ao processar esses arquivos.
* **Algoritmos de compactação e redimensionamento de qualidade do Photoshop**: Coerência com o padrão da indústria em termos de qualidade da amostragem reduzida (bicúbica lisa, afiada e automática) e qualidade de compressão. A Biblioteca de transcodificação de imagens avalia ainda mais o fator de qualidade da imagem de entrada e usa de forma inteligente tabelas e configurações de qualidade ideais para a imagem de saída. Essa capacidade produz arquivos de tamanho ideal sem comprometer a qualidade visual.
* **Taxa de transferência elevada:** O tempo de resposta é menor e a taxa de transferência é consistentemente maior do que o ImageMagick. Portanto, a Biblioteca de transcodificação de imagens deve diminuir o tempo de espera dos usuários e o custo da hospedagem.
* **Dimensione melhor com carga simultânea:** A Biblioteca de transcodificação de imagens tem desempenho ideal em condições de carregamento simultâneas. Ele fornece alta throughput com desempenho otimizado da CPU, uso da memória e baixo tempo de resposta, o que ajuda a reduzir o custo da hospedagem.

## Plataformas compatíveis {#supported-platforms}

A Biblioteca de transcodificação de imagem está disponível somente para distribuições RHEL 7 e CentOS 7.

>[!NOTE]
>
>O Mac OS e outras distribuições *nix (por exemplo, Debian e Ubuntu) não são compatíveis.

## Uso {#usage}

Os argumentos da linha de comando para a Biblioteca de transcodificação de imagem podem incluir o seguinte:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Você pode configurar as seguintes opções para a variável `-resize` parâmetro:

* `X`: Trabalhos semelhantes a [!DNL Experience Manager]. Por exemplo, -resize 319.
* `WxH`: A taxa de proporção não é mantida, por exemplo `-resize 319x319`.
* `Wx`: Corrige a largura e calcula a altura mantendo a proporção. Por exemplo, `-resize 319x`.
* `xH`: Corrige a altura e calcula a largura mantendo a proporção. Por exemplo, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar a biblioteca de transcodificação de imagens {#configuring-imaging-transcoding-library}

Para configurar o processamento de ITL, crie um arquivo de configuração e atualize o workflow para executá-lo.

### Criar arquivo de configuração para o pacote extraído {#create-conf-file}

Para configurar a biblioteca, crie um arquivo CONF para indicar as bibliotecas usando as etapas a seguir. Você precisa de permissões de administrador ou raiz.

1. Baixe o [Pacote da biblioteca de transcodificação de imagens da distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e instale-o usando o Gerenciador de pacotes. O pacote é compatível com [!DNL Experience Manager] 6.5.

1. Para conhecer uma ID de pacote para `com.day.cq.dam.cq-dam-switchengine`, faça logon no Console da Web e clique em **[!UICONTROL OSGi]** > **[!UICONTROL Pacotes]**. Como alternativa, para abrir o console pacotes, acesse `https://[aem_server:[port]/system/console/bundles/` URL. Localizar `com.day.cq.dam.cq-dam-switchengine` e sua ID.

1. Certifique-se de que todas as bibliotecas necessárias sejam extraídas, verificando a pasta usando o comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, em que o nome da pasta é construído usando a ID do pacote. Por exemplo, o comando é `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se a id do pacote for `588`.

1. Criar `SWitchEngineLibs.conf` para vincular à biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Adicionar `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` caminho para o arquivo conf usando `cat SWitchEngineLibs.conf` comando.

1. Executar `ldconfig` para criar os links e o cache necessários.

1. Na conta usada para iniciar [!DNL Experience Manager], editar `.bash_profile` arquivo. Adicionar `LD_LIBRARY_PATH` adicionando o seguinte.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para garantir que o valor do caminho seja definido como `.`, use `echo $LD_LIBRARY_PATH` comando. A saída deve ser apenas `.`. Se o valor não estiver definido como `.`, reinicie a sessão.

### Configurar [!UICONTROL Ativo de atualização DAM] workflow {#configure-dam-asset-update-workflow}

Atualize o [!UICONTROL Ativo de atualização DAM] fluxo de trabalho para usar a biblioteca para processar imagens.

1. Em [!DNL Experience Manager] interface do usuário, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. No **[!UICONTROL Modelos de fluxo de trabalho]** , abra o **[!UICONTROL Ativo de atualização DAM]** modelo de fluxo de trabalho no modo de edição.

1. Abra o **[!UICONTROL Processar miniaturas]** etapa do processo do fluxo de trabalho. No **[!UICONTROL Miniaturas]** , adicione os tipos MIME para os quais deseja ignorar o processo de geração de miniaturas padrão no **[!UICONTROL Ignorar Tipos Mime]** lista.
Por exemplo, se você deseja criar miniaturas para uma imagem TIFF usando a Biblioteca de transcodificação de imagem, especifique `image/tiff` no **[!UICONTROL Ignorar Tipos Mime]** campo.

1. No **[!UICONTROL Imagem ativada na Web]** , adicione os tipos MIME para os quais deseja ignorar o processo de geração de renderização da Web padrão em **[!UICONTROL Ignorar Lista]**. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/tiff` para a lista de ignorados.

1. Abra o **[!UICONTROL Miniaturas do EPS (fornecidas pelo ImageMagick)]** , navegue até o **[!UICONTROL Argumentos]** guia . No **[!UICONTROL Tipos Mime]** adicione os tipos MIME que a Biblioteca de transcodificação de imagens deve processar. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/jpeg` para **[!UICONTROL Tipos Mime]** lista.

1. Remova os comandos padrão, se houver.

1. Alterne o painel lateral e, na lista de etapas, adicione **[!UICONTROL Manipulador SWitchEngine]**.

1. Adicione comandos ao [!UICONTROL Manipulador SwitchEngine] com base em seus requisitos personalizados. Ajuste os parâmetros dos comandos especificados para atender aos seus requisitos. Por exemplo, se você quiser preservar o perfil de cor da imagem do JPEG, adicione os seguintes comandos à **[!UICONTROL Comandos]** lista:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![calúnia](assets/chlimage_1-199.png)

1. (Opcional) Gere miniaturas de uma representação intermediária usando um único comando. A representação intermediária atua como fonte para gerar representações estáticas e da Web. Este método é mais rápido que o método anterior. No entanto, não é possível aplicar parâmetros personalizados a miniaturas usando esse método.

   ![calúnia](assets/chlimage_1-200.png)

1. Para gerar renderizações da Web, configure os parâmetros no **[!UICONTROL Imagem ativada na Web]** guia .

1. Sincronizar o atualizado [!UICONTROL Ativo de atualização DAM] modelo de fluxo de trabalho. Salve o workflow.

Verifique a configuração, carregue uma imagem de TIFF e monitore o arquivo error.log. Você notará `INFO` mensagens com menções de `SwitchEngineHandlingProcess execute: executing command line`. Os logs mencionam as representações geradas. Depois que o fluxo de trabalho for concluído, você poderá exibir as novas representações em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Artigo de tipos MIME suportados](assets-formats.md#supported-image-transcoding-library)

