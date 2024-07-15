---
title: Biblioteca de transcodificação de imagem
description: Saiba como configurar e usar a Biblioteca de transcodificação de imagem do Adobe, uma solução de processamento de imagem que pode executar funções principais de tratamento de imagem, incluindo codificação, transcodificação, reamostragem de imagem e redimensionamento de imagem.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Biblioteca de transcodificação de imagem {#imaging-transcoding-library}

A Biblioteca de transcodificação de imagem do Adobe é uma solução de processamento de imagem proprietária que pode executar funções principais de manipulação de imagem, incluindo:

* Codificação
* Transcodificação (conversão de formatos compatíveis)
* Nova amostra de imagem usando algoritmos PS e Intel IPP
* Profundidade de bits e preservação do perfil de cores
* compactação de qualidade do JPEG
* Redimensionamento de imagem

A Biblioteca de transcodificação de imagens oferece suporte a CMYK e suporte alfa total, exceto CMYK -Alpha.

Além de oferecer suporte a uma grande variedade de formatos de arquivo e perfis, a Biblioteca de transcodificação de imagens tem vantagens significativas em relação a outras soluções de terceiros no que diz respeito a desempenho, escalabilidade e qualidade. Estes são alguns dos principais benefícios do uso da Biblioteca de transcodificação de imagem:

* **Escala com aumento do tamanho ou da resolução de arquivos**: a escala é alcançada principalmente pela capacidade patenteada da Biblioteca de Transcodificação de Imagens de redimensionar ao decodificar arquivos. Essa capacidade garante que o uso de memória em tempo de execução seja sempre ideal e não seja uma função quadrática de aumento do tamanho do arquivo ou megapixels de resolução. A Biblioteca de transcodificação de imagens pode processar arquivos maiores e de alta resolução (contendo megapixels maiores). Ferramentas de terceiros, como o ImageMagick, são incapazes de lidar com arquivos grandes e falhas durante o processamento desses arquivos.
* **Algoritmos de compactação e redimensionamento de qualidade do Photoshop**: consistência com o padrão do setor em termos de qualidade de redução de resolução (bicúbico suave, nítido e automático) e qualidade de compactação. A Biblioteca de transcodificação de imagem avalia ainda mais o fator de qualidade da imagem de entrada e usa de forma inteligente tabelas e configurações de qualidade ideais para a imagem de saída. Essa capacidade produz arquivos de tamanho ideal sem comprometer a qualidade visual.
* **Taxa de transferência alta:** o tempo de resposta é menor e a taxa de transferência é consistentemente maior que ImageMagick. Portanto, a Biblioteca de transcodificação de imagens deve reduzir o tempo de espera dos usuários e o custo da hospedagem.
* **Dimensione melhor com o carregamento simultâneo:** A Biblioteca de Transcodificação de Imagens é executada de maneira ideal sob condições de carregamento simultâneas. Ele oferece alto throughput com desempenho otimizado da CPU, uso da memória e baixo tempo de resposta, o que ajuda a reduzir o custo da hospedagem.

## Plataformas compatíveis {#supported-platforms}

A Biblioteca de transcodificação de imagens está disponível somente para distribuições RHEL 7 e CentOS 7.

>[!NOTE]
>
>O sistema operacional Mac e outras distribuições *nix (por exemplo, Debian e Ubuntu) não são compatíveis.

## Uso {#usage}

Os argumentos de linha de comando para a Biblioteca de transcodificação de imagem podem incluir o seguinte:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Você pode configurar as seguintes opções para o parâmetro `-resize`:

* `X`: Funciona de forma semelhante a [!DNL Experience Manager]. Por exemplo, -resize 319.
* `WxH`: a taxa de proporção não é mantida. Por exemplo, `-resize 319x319`.
* `Wx`: corrige a largura e calcula a altura mantendo a proporção. Por exemplo, `-resize 319x`.
* `xH`: corrige a altura e calcula a largura mantendo a proporção. Por exemplo, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar biblioteca de transcodificação de imagens {#configuring-imaging-transcoding-library}

Para configurar o processamento de ITL, crie um arquivo de configuração e atualize o workflow para executá-lo.

### Criar arquivo de configuração para o pacote extraído {#create-conf-file}

Para configurar a biblioteca, crie um arquivo CONF para indicar as bibliotecas usando as etapas a seguir. Você precisa de permissões de administrador ou raiz.

1. Baixe o [pacote da Biblioteca de Transcodificação de Imagens da Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e instale-o usando o Gerenciador de Pacotes. O pacote é compatível com [!DNL Experience Manager] 6.5.

1. Para saber a ID do pacote de `com.day.cq.dam.cq-dam-switchengine`, faça logon no Console da Web e clique em **[!UICONTROL OSGi]** > **[!UICONTROL Pacotes]**. Como alternativa, para abrir o console de pacotes, acesse a URL `https://[aem_server:[port]/system/console/bundles/`. Localize o pacote `com.day.cq.dam.cq-dam-switchengine` e sua ID.

1. Verifique se todas as bibliotecas necessárias foram extraídas, verificando a pasta com o comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, em que o nome da pasta é construído usando a ID do pacote. Por exemplo, o comando é `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se a ID do pacote for `588`.

1. Crie o arquivo `SWitchEngineLibs.conf` para vincular à biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Adicione o caminho `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` ao arquivo conf usando o comando `cat SWitchEngineLibs.conf`.

1. Execute o comando `ldconfig` para criar os links e o cache necessários.

1. Na conta usada para iniciar [!DNL Experience Manager], edite o arquivo `.bash_profile`. Adicione `LD_LIBRARY_PATH` adicionando o seguinte.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para garantir que o valor do caminho esteja definido como `.`, use o comando `echo $LD_LIBRARY_PATH`. A saída deve ser apenas `.`. Se o valor não estiver definido como `.`, reinicie a sessão.

### Configurar o fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] {#configure-dam-asset-update-workflow}

Atualize o fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] para usar a biblioteca para processar imagens.

1. Na interface de usuário do [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.

1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, abra o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** no modo de edição.

1. Abra a etapa do processo de fluxo de trabalho **[!UICONTROL Processar Miniaturas]**. Na guia **[!UICONTROL Miniaturas]**, adicione os tipos MIME para os quais você deseja ignorar o processo de geração de miniaturas padrão na lista **[!UICONTROL Ignorar tipos MIME]**.
Por exemplo, se você deseja criar miniaturas para uma imagem de TIFF usando a Biblioteca de transcodificação de imagem, especifique `image/tiff` no campo **[!UICONTROL Ignorar tipos MIME]**.

1. Na guia **[!UICONTROL Imagem Habilitada para a Web]**, adicione os tipos MIME para os quais você deseja ignorar o processo de geração de representação da Web padrão em **[!UICONTROL Ignorar Lista]**. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/tiff` à lista de permissões.

1. Abra a etapa **[!UICONTROL Miniaturas do EPS (ativado por ImageMagick)]** e navegue até a guia **[!UICONTROL Argumentos]**. Na lista **[!UICONTROL Tipos MIME]**, adicione os tipos MIME que você deseja que a Biblioteca de Transcodificação de Imagens processe. Por exemplo, se você ignorou o tipo MIME `image/tiff` na etapa acima, adicione `image/jpeg` à lista **[!UICONTROL Tipos MIME]**.

1. Remova os comandos padrão, se houver.

1. Alterne o painel lateral e, na lista de etapas, adicione **[!UICONTROL SWitchEngine Handler]**.

1. Adicione comandos ao [!UICONTROL Manipulador do SwitchEngine] com base em seus requisitos personalizados. Ajuste os parâmetros dos comandos especificados para atender aos requisitos. Por exemplo, se você deseja preservar o perfil de cores da imagem do JPEG, adicione os seguintes comandos à lista **[!UICONTROL Comandos]**:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (Opcional) Gere miniaturas de uma representação intermediária usando um único comando. A representação intermediária atua como origem para gerar representações estáticas e da Web. Este método é mais rápido que o método anterior. No entanto, não é possível aplicar parâmetros personalizados a miniaturas usando esse método.

   ![chlimage](assets/chlimage_1-200.png)

1. Para gerar representações da Web, configure parâmetros na guia **[!UICONTROL Imagem Habilitada para Web]**.

1. Sincronize o modelo de fluxo de trabalho atualizado do [!UICONTROL Ativo de atualização do DAM]. Salve o workflow.

Para verificar a configuração, carregue uma imagem de TIFF e monitore o arquivo error.log. Você observará `INFO` mensagens com menções de `SwitchEngineHandlingProcess execute: executing command line`. Os logs mencionam as representações geradas. Após a conclusão do fluxo de trabalho, você poderá exibir as novas representações em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Artigo sobre tipos MIME suportados](assets-formats.md#supported-image-transcoding-library)
