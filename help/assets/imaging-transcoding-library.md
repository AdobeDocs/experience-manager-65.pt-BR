---
title: Biblioteca de transcodificação de imagens
description: Saiba como configurar e usar a Biblioteca de transcodificação de imagens da Adobe, uma solução de processamento de imagens que pode executar funções essenciais de manipulação de imagens, incluindo codificação, transcodificação, redefinição de imagens e redimensionamento de imagens.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b2628d37c3ad158913c28ecd890aee9fd0106de4
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---


# Biblioteca de transcodificação de imagens {#imaging-transcoding-library}

A Biblioteca de transcodificação de imagens da Adobe é uma solução proprietária de processamento de imagens que pode executar as principais funções de manipulação de imagens, incluindo:

* Codificação
* Transcodificação (conversão de formatos suportados)
* Redefinição da resolução da imagem usando algoritmos PS e Intel IPP
* Profundidade de bits e preservação de perfis coloridos
* Compactação de qualidade JPEG
* Redimensionamento de imagem

A Biblioteca de transcodificação de imagens fornece suporte a CMYK e suporte a alfa completo, exceto CMYK -Alpha.

Além de suportar uma grande variedade de formatos de arquivos e perfis, a Biblioteca de transcodificação de imagens tem vantagens significativas em relação a outras soluções de terceiros em termos de desempenho, escalabilidade e qualidade. Estes são alguns dos principais benefícios do uso da Biblioteca de transcodificação de imagens:

* **Dimensiona com tamanho ou resolução** cada vez maiores: O dimensionamento é obtido principalmente pela capacidade patenteada da Biblioteca de transcodificação de imagens de redimensionar ao decodificar arquivos. Essa capacidade garante que o uso da memória em tempo de execução seja sempre ótimo e não seja uma função quadrática do aumento do tamanho do arquivo ou da resolução dos megapixels. A Biblioteca de transcodificação de imagens pode processar arquivos maiores e de alta resolução (contendo megapixels mais altos). Ferramentas de terceiros, como o ImageMagick, não conseguem lidar com arquivos grandes e falhas ao processar esses arquivos.
* **Algoritmos** de compactação e redimensionamento de qualidade do Photoshop: Coerência com o padrão da indústria em termos de qualidade da amostragem decrescente (regular, nítida e automática, bicúbica) e qualidade de compressão. A Biblioteca de transcodificação de imagens avalia ainda mais o fator de qualidade da imagem de entrada e usa de forma inteligente as tabelas e configurações de qualidade ideais para a imagem de saída. Essa capacidade produz arquivos de tamanho ideal sem comprometer a qualidade visual.
* **Alta throughput:** O tempo de resposta é menor e o throughput é consistentemente maior que o ImageMagick. Portanto, a Biblioteca de transcodificação de imagens deve diminuir o tempo de espera dos usuários e o custo de hospedagem.
* **Dimensione melhor com carga simultânea:** A Biblioteca de transcodificação de imagens é executada de forma ideal em condições de carregamento simultâneas. Ele oferece alta throughput com desempenho otimizado da CPU, uso da memória e baixo tempo de resposta, o que ajuda a reduzir o custo da hospedagem.

## Supported platforms {#supported-platforms}

A Biblioteca de transcodificação de imagens está disponível somente para as distribuições RHEL 7 e CentOS 7.

>[!NOTE]
>
>O Mac OS e outras distribuições *nix (por exemplo, Debian e Ubuntu) não são compatíveis.

## Uso {#usage}

Os argumentos da linha de comando para a Biblioteca de transcodificação de imagens podem incluir o seguinte:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Você pode configurar as seguintes opções para o `-resize` parâmetro:

* `X`: Funciona de forma semelhante ao Experience Manager. Por exemplo - resize 319.
* `WxH`: A proporção não é mantida, por exemplo `-resize 319x319`.
* `Wx`: Corrige a largura e calcula a altura mantendo a proporção. Por exemplo `-resize 319x`.
* `xH`: Corrige a altura e calcula a largura que mantém a proporção. Por exemplo `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar a biblioteca de transcodificação de imagens {#configuring-imaging-transcoding-library}

Para configurar o processamento ITL, crie um arquivo de configuração e atualize o fluxo de trabalho para executá-lo.

### Criar arquivo de configuração para o pacote extraído {#create-conf-file}

Para configurar a biblioteca, crie um arquivo .conf para indicar as bibliotecas usando as etapas a seguir. Você precisa de permissões de administrador ou raiz.

1. Baixe o pacote da Biblioteca de transcodificação de [imagens do Compartilhamento](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) de pacotes ou da Distribuição [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) software e instale-o usando o Gerenciador de pacotes. O pacote é compatível com o Experience Manager 6.5.

1. Para saber uma ID de pacote para `com.day.cq.dam.cq-dam-switchengine`, faça logon no Console da Web e clique em **[!UICONTROL OSGi > Pacotes]**. Como alternativa, para abrir o console de pacotes, acesse o `https://[aem_server:[port]/system/console/bundles/` URL. Localize o `com.day.cq.dam.cq-dam-switchengine` pacote e sua ID.

1. Certifique-se de que todas as bibliotecas necessárias sejam extraídas, verificando a pasta usando o comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, onde o nome da pasta é construído usando a ID do pacote. Por exemplo, o comando é `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se a ID do pacote for `588`.

1. Crie um `SWitchEngineLibs.conf` arquivo para vincular à biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Adicione o `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` caminho ao arquivo conf usando o `cat SWitchEngineLibs.conf` comando.

1. Execute `ldconfig` o comando para criar os links e o cache necessários.

1. Na conta usada para o start Experience Manager, edite o arquivo `.bash_profile` . Adicione `LD_LIBRARY_PATH` adicionando o seguinte.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para garantir que o valor do caminho esteja definido como `.`, use o `echo $LD_LIBRARY_PATH` comando. A saída deve ser apenas `.`. Se o valor não estiver definido como `.`, reinicie a sessão.

### Configurar o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM {#configure-dam-asset-update-workflow}

Atualize o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM para usar a biblioteca para processar imagens.

1. Na interface do usuário do Experience Manager, selecione **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.

1. Na página Modelos **[!UICONTROL de]** fluxo de trabalho, abra o modelo de fluxo de trabalho Atualizar ativo **[!UICONTROL do]** DAM no modo de edição.

1. Abra a etapa do processo de fluxo de trabalho **[!UICONTROL Processar miniaturas]** . Na guia **[!UICONTROL Miniaturas]** , adicione os tipos MIME para os quais você deseja ignorar o processo de geração de miniaturas padrão na lista **[!UICONTROL Ignorar tipos]** MIME.
Por exemplo, se você quiser criar miniaturas para uma imagem TIFF usando a Biblioteca de transcodificação de imagens, especifique `image/tiff` no campo **[!UICONTROL Ignorar tipos]** MIME.

1. Na guia Imagem **[!UICONTROL ativada pela]** Web, adicione os tipos MIME para os quais você deseja ignorar o processo de geração de representação da Web padrão em **[!UICONTROL Ignorar Lista]**. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/tiff` à lista skip.

1. Abra a etapa de miniaturas **[!UICONTROL EPS (acionada por ImageMagick)]** e navegue até a guia **[!UICONTROL Argumentos]** . Na lista **[!UICONTROL Mime Types]** , adicione os tipos MIME que você deseja que a Biblioteca de transcodificação de imagens processe. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/jpeg` à lista **[!UICONTROL Mime Types]** .

1. Remova os comandos padrão, se houver.

1. Alterne o painel lateral e, na lista das etapas, adicione o **[!UICONTROL Manipulador]** SWitchEngine.

1. Adicione comandos ao [!UICONTROL SwitchEngine Handler] com base em seus requisitos personalizados. Ajuste os parâmetros dos comandos especificados para atender aos seus requisitos. Por exemplo, se você quiser preservar o perfil colorido da imagem JPEG, adicione os seguintes comandos à lista **[!UICONTROL Comandos]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![calúnia](assets/chlimage_1-199.png)

1. (Opcional) Gere miniaturas de uma execução intermediária usando um único comando. A execução intermediária atua como fonte para gerar representações estáticas e da Web. Este método é mais rápido do que o método anterior. No entanto, não é possível aplicar parâmetros personalizados a miniaturas usando esse método.

   ![calúnia](assets/chlimage_1-200.png)

1. Para gerar representações da Web, configure os parâmetros na guia Imagem **[!UICONTROL ativada pela]** Web.

1. Sincronize o modelo de fluxo de trabalho atualizado do Ativo [!UICONTROL de atualização do] DAM. Salve o fluxo de trabalho.

Verifique a configuração, carregue uma imagem TIFF e monitore o arquivo error.log. Você notará `INFO` mensagens com menções de `SwitchEngineHandlingProcess execute: executing command line`. Os registros mencionam as execuções geradas. Quando o fluxo de trabalho for concluído, você poderá visualização as novas execuções no Experience Manager.

>[!MORELIKETHIS]
>
>* [Artigo de tipos MIME suportados](assets-formats.md#supported-image-transcoding-library)

