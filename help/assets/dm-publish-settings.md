---
title: Configurar a publicação do Dynamic Media
description: Saiba como configurar a Publicação no Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: e3067a17153864babaf0243c4c3f6cf9cd8d30bc
workflow-type: tm+mt
source-wordcount: '3098'
ht-degree: 2%

---


# Configurar a publicação do Dynamic Media

>[!IMPORTANT]
>
>A Configuração de publicação do Dynamic Media só estará disponível se:
>
>* Você está executando o Dynamic Media no modo Scene7.
>* Você tem um *existente* **[!UICONTROL Configuração do Dynamic Media]** (em **[!UICONTROL Cloud Services]**) no Adobe Experience Manager 6.5 ou no Experience Manager as a Cloud Service.
>* Você é um administrador de sistema do Experience Manager com privilégios de administrador.



As configurações da página Configuração de publicação do Dynamic Media determinam como os ativos são entregues por padrão dos servidores do Adobe Dynamic Media para sites ou aplicativos da Web. Se nenhuma configuração for especificada, o servidor Adobe Dynamic Media fornece um ativo de acordo com uma configuração padrão em uma página Publicar configuração . Por exemplo, uma solicitação para fornecer uma imagem que não inclua um atributo de resolução gera uma imagem com a configuração de Resolução de objeto padrão na página Servidor de imagem.

Os administradores podem alterar as configurações padrão nas páginas Servidor de imagem, Renderizador de imagem e Vinheta para estabelecer configurações padrão para o fornecimento de ativos dos servidores.

>[!NOTE]
>
>A Configuração de publicação do Dynamic Media deve ser usada por desenvolvedores e programadores de sites experientes. O Adobe Dynamic Media parte do princípio de que os usuários que alteram qualquer um desses padrões publicam configurações estão familiarizados com o Adobe Dynamic Media, padrões e convenções de protocolo HTTP e tecnologia básica de geração de imagens.

**Para configurar a Configuração de publicação do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, selecione o ícone Ferramentas e vá para **[!UICONTROL Ativos]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagens , defina o Servidor de imagens - contexto de publicação e use as cinco guias para definir as configurações de publicação padrão.

   * [Servidor de imagem](#image-server)
   * [Segurança](#security-tab) guia
   * [Gerenciamento de catálogo](#catalog-management-tab) guia
   * [Atributos da solicitação](#request-attributes-tab) guia
   * [Atributos de miniatura comuns](#common-thumbnail-attributes-tab) guia
   * [Atributos do gerenciamento de cores](#color-management-attributes-tab) guia

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

## Servidor de imagem {#image-server}

A página Servidor de imagens estabelece as configurações padrão para o fornecimento de imagens de servidores de imagens. As configurações estão disponíveis em cinco categorias

| Contexto de publicação | Descrição |
| --- | --- |
| Serviço de imagem | Especifica o contexto das configurações de publicação. |
| Servidor de imagens de teste | Especifica o contexto para testar as configurações de publicação.<br>Consulte [Testar ativos antes de torná-los públicos](#test-assets-before-making-public). |

### Guia Segurança {#security-tab}

**[!UICONTROL Endereço do cliente]** - Permite especificar um ou mais endereços IP ou intervalos de endereço IP. Quando especificado, as solicitações para este catálogo de imagem que se origina de um cliente em um endereço IP não listado são rejeitadas. Essa regra se aplica à entrega de imagens e imagens renderizadas.

### Guia Gerenciamento de catálogo {#catalog-management-tab}

**[!UICONTROL Caminho do arquivo de definição do conjunto de regras]** - Especifica o arquivo que contém as definições do conjunto de regras para o catálogo de imagens.

Consulte também [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) no Guia de referência de visualizadores do Dynamic Media.

### Guia Atributos da solicitação {#request-attributes-tab}

Essas configurações pertencem à aparência padrão das imagens.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Limite de tamanho da imagem de resposta]** | Obrigatório.<br>Especifica a largura e a altura máximas da imagem de resposta que são retornadas ao cliente. O servidor retornará um erro se uma solicitação causar uma imagem de resposta cuja largura, altura ou ambos forem maiores que essa configuração.<br>Consulte também [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de solicitação de ofuscação]** | Ative se desejar que a codificação base64 seja aplicada a solicitações válidas.<br>Consulte também [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de bloqueio de solicitação]** | Ative se desejar que um simples bloqueio de hash seja incluído em solicitações.<br>Consulte também [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de solicitação padrão]** |  |
| **[!UICONTROL Sufixo do arquivo de imagem padrão]** | Obrigatório.<br>Extensão padrão do arquivo de dados que é anexada aos valores dos campos Caminho e Máscara do catálogo se o caminho não incluir um sufixo de arquivo.<br>Consulte também [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Nome da face da fonte padrão]** | Especifica qual fonte é usada se nenhuma fonte for fornecida por uma solicitação de camada de texto. Se especificado, deve ser um valor de nome de fonte válido no mapa de fonte deste catálogo de imagem ou no mapa de fontes do catálogo padrão.<br>Consulte também [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Imagem padrão]** | Fornece uma imagem padrão a ser retornada em resposta a uma solicitação na qual a imagem solicitada não é encontrada.<br>Consulte também [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de imagem padrão]** | Quando a caixa de controle deslizante estiver ativada (controle deslizante à direita), a variável **[!UICONTROL Imagem padrão]** substitui cada camada ausente na imagem de origem pela imagem padrão e retorna o composto como de costume. Quando a caixa de controle deslizante está desativada (controle deslizante à esquerda), a imagem padrão substitui toda a imagem composta, mesmo que a imagem ausente seja apenas uma das várias camadas.<br>Consulte também [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tamanho de exibição padrão]** | Obrigatório.<br>O servidor restringe as imagens de resposta a não serem maiores que essa largura e altura, se a solicitação não especificar o tamanho de exibição explicitamente usando `wid=`, `hei=`ou `scl=`.<br>Consulte também [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tamanho padrão da miniatura]** | Obrigatório.<br>Usado em vez do atributo **[!UICONTROL Tamanho de exibição padrão]** para solicitações de miniatura (`req=tmb`). O servidor restringe as imagens de resposta para não serem maiores que essa largura e altura, se houver uma solicitação em miniatura (`req=tmb`) não especifica o tamanho explicitamente usando `wid=`, `hei=`ou `scl=`.<br>Consulte também [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Cor de fundo padrão]** | Especifica o valor RGB usado para preencher qualquer área de uma imagem de resposta que não contenha dados de imagem reais.<br>Consulte também [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de codificação de JPEG]** |  |
| **[!UICONTROL Qualidade]** | Especifica os atributos padrão para imagens JPEG reply. O **[!UICONTROL Qualidade]** é definido no intervalo de 1 - 100.<br>Consulte também [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Diminuição da resolução cromática]** | Ative ou desative a redução cromaticamente da amostragem que é empregada por codificadores JPEG. |
| **[!UICONTROL Modo de reamostragem padrão]** | Especifica a reamostragem e os atributos de interpolação padrão a serem usados para dimensionar dados de imagem. Use quando `resMode` não é especificado em uma solicitação.<br>Consulte também [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) no Guia de referência de visualizadores do Dynamic Media. |

### Guia Atributos de miniatura comuns {#common-thumbnail-attributes-tab}

Essas configurações pertencem à aparência padrão e ao alinhamento de imagens em miniatura.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Cor de fundo padrão para miniatura]** | Especifica o valor de RGB usado para preencher a área de uma imagem em miniatura de saída que não contém dados de imagem reais. Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]** ou **[!UICONTROL Textura]**.<br>Consulte também [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento horizontal]** | Especifica o alinhamento horizontal da imagem em miniatura no retângulo de imagem de resposta especificado por `wid=` e `hei=` valores.<br>Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos horizontais para escolher: **[!UICONTROL Alinhamento central]**, **[!UICONTROL Alinhamento à esquerda]** e **[!UICONTROL Alinhamento à direita]**.<br>Consulte também [MiniaturaAlinhar](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento vertical]** | Especifica o alinhamento vertical da imagem em miniatura no retângulo de imagem de resposta especificado por `wid=` e `hei=` valores. Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos verticais a serem escolhidos: **[!UICONTROL Alinhamento superior]**, **[!UICONTROL Alinhamento central]** e **[!UICONTROL Alinhamento inferior]**.<br>Consulte também [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tempo de funcionamento padrão do cache]** | Fornece um intervalo de expiração padrão em horas, caso um registro de catálogo específico não contenha um valor de Expiração de catálogo válido. Defina como `-1` para marcar como nunca expirar. <br>Consulte também [Expiração](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tipo de miniatura padrão]** | Fornece um padrão para o tipo de miniatura caso um registro de catálogo específico não contenha um valor ThumbType de catálogo válido. Usado somente para solicitações de miniatura (`req=tmb`).<br>Há três tipos de miniaturas para escolher: **[!UICONTROL Cortar]**, **[!UICONTROL Ajustar]** e **[!UICONTROL Textura]**.<br>Consulte também [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Resolução padrão de miniatura]** | Fornece um padrão para a resolução de objeto de miniatura caso um registro de catálogo específico não contenha um valor de ThumbRes de catálogo válido. Usado somente para solicitações de miniatura (`req=tmb`) e quando a variável **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Textura]**.<br>Consulte também [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) no Guia de referência de visualizadores do Dynamic Media. |

### Guia Atributos de gerenciamento de cores {#color-management-attributes-tab}

Essas configurações determinam quais perfis de cores ICC são usados para imagens.

**Propósito de renderização da conversão de cores**
Um propósito de renderização de conversão de cores permite a substituição da intenção de renderização padrão dos perfis de trabalho para determinar como as cores de origem são ajustadas. Usado quando:

1. Um dos perfis ICC padrão é o espaço de cores de destino de uma conversão de cores.
1. Um dispositivo de saída (impressora ou monitor) é caracterizado por esse perfil.
1. E o propósito de renderização especificado é válido para este perfil.

Diferentes intenções de renderização usam regras diferentes para determinar como as cores de origem são ajustadas.

Consulte também [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) no Guia de referência de visualizadores do Dynamic Media.

>[!NOTE]
>
>Em geral, é melhor usar o propósito de renderização padrão para a configuração de cor selecionada, que foi testada pelo Adobe para atender aos padrões do setor. Por exemplo, se você escolher uma configuração de cor para América do Norte ou Europa, o objetivo padrão de renderização da conversão de cores será **[!UICONTROL Colormétrica relativa]**. Se você escolher uma configuração de cor para o Japão, o objetivo padrão de renderização da conversão de cores será **[!UICONTROL Perceptivo]**.

| Configuração | Características |
| --- | --- |
| **[!UICONTROL Espaço de cores padrão CMYK]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados CMYK. If **[!UICONTROL Nenhum especificado]** for escolhida, o gerenciamento de cores será desativado para esse catálogo de imagens quando as imagens de origem CMYK estiverem envolvidas. Todos os espaços de trabalho CMYK dependem do dispositivo, o que significa que eles são baseados em combinações reais de tinta e papel. Os Adobe dos espaços de trabalho CMYK são fornecidos com base em condições de impressão comercial padrão.<br> Consulte também [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Espaço de cores padrão de escala de cinza]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados em escala de cinza. If **[!UICONTROL Nenhum especificado]** for escolhido, o gerenciamento de cores será desativado para esse catálogo de imagens quando imagens de origem em escala cinza forem envolvidas.<br>Consulte também [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL RGB espaço de cores padrão]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados de RGB. If **[!UICONTROL Nenhum especificado]** for escolhido, o gerenciamento de cores será desativado para esse catálogo de imagens quando as imagens de RGB forem envolvidas. Em geral, é melhor escolher **[!UICONTROL Adobe RGB]** ou **[!UICONTROL sRGB]**, em vez do perfil de um dispositivo específico (como um perfil de monitor). **[!UICONTROL sRGB]** O é recomendado ao preparar imagens para a Web ou dispositivos móveis, pois define o espaço de cores do monitor padrão usado para exibir imagens na Web. **[!UICONTROL sRGB]** O também é uma boa escolha para trabalhar com imagens de câmeras digitais de nível de consumidor, pois a maioria dessas câmeras usa o sRGB como espaço de cores padrão.<br>Consulte também [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Objetivo de renderização da conversão de cores]** | **[!UICONTROL Perceptivo]** - Tem como objetivo preservar a relação visual entre as cores para que seja percebida como natural para o olho humano, mesmo que os próprios valores de cor possam mudar. Essa intenção é adequada para imagens fotográficas com muitas cores fora do gamut. Essa configuração é o propósito de renderização padrão para o setor de impressão japonês. |
|  | **[!UICONTROL Colorimétrica relativa]** - Compara o realce extremo do espaço de cores de origem com o do espaço de cores de destino e alterna todas as cores de acordo. As cores fora do gamut são transferidas para a cor reprodutível mais próxima no espaço de cores de destino. Colorimétrica relativa preserva mais das cores originais em uma imagem do que Perceptual. Essa configuração é o propósito de renderização padrão para impressão na América do Norte e na Europa. |
|  | **[!UICONTROL Saturação]** - Tenta produzir cores vivas em uma imagem, em detrimento da precisão das cores. Esse propósito de renderização é adequado para gráficos comerciais, como gráficos ou gráficos, em que cores saturadas brilhantes são mais importantes do que a relação exata entre cores. |
|  | **[!UICONTROL Colorimétrica absoluta]** - Deixa inalteradas as cores que estão dentro da gama de destino. As cores fora do gamut são cortadas. Não é executado o dimensionamento de cores para o ponto branco de destino. Essa intenção tem como objetivo manter a precisão da cor em detrimento da preservação das relações entre cores e é adequada para a prova para simular a saída de um determinado dispositivo. Essa intenção é útil para visualizar como a cor do papel afeta as cores impressas. |

## Testar ativos antes de torná-los públicos {#test-assets-before-making-public}

O Teste Seguro ajuda você a definir um ambiente de teste seguro e criar uma solução empresarial para negócios robusta, com base em um conjunto configurável de endereços IP e intervalos. Essa funcionalidade permite que você corresponda suas implantações do Adobe Dynamic Media à arquitetura do seu sistema de negócios e de gerenciamento de conteúdo.

Com o Teste Seguro, você pode visualizar a versão de preparo do site com conteúdo não publicado.

Se desejar, crie um ambiente de preparo em vez de tornar os ativos disponíveis publicamente pelos seguintes motivos:

* Visualizar sites antes do lançamento público (site de preparo).
* Adicione ativos que exigem acesso restrito, como eCatalogs que mostrem preços em uma aplicação Web B2B.
* Use os ativos por trás de um firewall como parte do sistema de gerenciamento de informações do produto, do aplicativo de atendimento ao cliente, do site de treinamento e assim por diante.

>[!NOTE]
>
>O Teste Seguro não afeta o acesso ao Adobe Dynamic Media Classic. A segurança do Adobe Dynamic Media Classic permanece consistente e requer as credenciais usuais para acesso ao Adobe Dynamic Media Classic e serviços da Web relacionados.

### Como o teste seguro funciona {#how-test-assets-works}

A maioria das corporações mantém a Internet por trás de um firewall. O acesso à Internet é possível através de determinadas rotas e geralmente através de uma gama limitada de endereços IP públicos.

Na sua rede corporativa, você pode descobrir seu endereço IP público usando sites como [https://www.whatismyip.com](https://www.whatismyip.com/) ou solicite essas informações à sua organização de TI corporativa.

Com o Teste Seguro, o Adobe Dynamic Media estabelece um Servidor de Imagem dedicado para ambientes de preparo ou aplicativos internos. Qualquer solicitação para este servidor verifica o endereço IP de origem. Se a solicitação recebida não estiver na lista aprovada de endereços IP, uma resposta de falha será retornada. O Administrador da empresa do Adobe Dynamic Media configura a lista aprovada de endereços IP para o ambiente de Teste Seguro da empresa.

Como a localização da solicitação original deve ser confirmada, o tráfego do serviço de Teste Seguro não é roteado por meio de uma rede de distribuição de conteúdo como o tráfego público do Dynamic Media Image Server. As solicitações para o serviço de teste seguro têm uma latência ligeiramente maior em comparação com os servidores públicos de imagem da Dynamic Media.

Os ativos não publicados ficam imediatamente disponíveis nos serviços de Teste Seguro, sem a necessidade de publicar. Dessa forma, é possível executar uma visualização antes que os ativos sejam publicados em seu servidor de imagens aberto ao público.

>[!NOTE]
>
>Os serviços de Teste Seguro usam o Servidor de Catálogo configurado com um contexto de publicação interno. Portanto, se sua empresa estiver configurada para publicar no Teste seguro, todos os ativos carregados no Adobe Dynamic Media imediatamente se tornarão disponíveis nos serviços de Teste seguro. Essa funcionalidade é verdadeira independentemente de os ativos serem marcados para publicação no upload.

Os serviços de Teste Seguro atualmente oferecem suporte aos seguintes tipos de ativos e funcionalidades:

* Imagens.
* Vinhetas (Solicitações do Servidor de Renderização).
* Solicitações do Servidor de Renderização (suportadas, mas devem ser solicitadas explicitamente pelo cliente).
* Conjuntos, incluindo conjuntos de imagens, eCatalog, conjuntos de renderização e conjuntos de mídia.
* Visualizadores de mídia avançada do Adobe Standard Dynamic Media.
* Adobe Dynamic Media OnDemand JSP pages.
* Conteúdo estático, como arquivos PDF e vídeos fornecidos progressivamente.
* streaming de vídeo HTTP.
* Transmissão contínua de vídeo.

Os seguintes tipos de ativos e funcionalidades não são suportados no momento:

* Pesquisa de informações ou eCatalog do Adobe Dynamic Media Classic
* Transmissão de vídeo RTMP
* Web-to-print
* Serviços UGC (Conteúdo gerado pelo usuário)

>[!IMPORTANT]
>
>O suporte para ativos de imagem vetorial UGC novos ou existentes no Adobe Dynamic Media terminou em 30 de setembro de 2021.

### Testar o serviço de teste seguro {#test-secure-testing-service}

Para garantir que o serviço de Teste Seguro funcione conforme o esperado, faça o seguinte:

#### Prepare sua conta

1. Entre em contato com o Atendimento ao cliente do Adobe e solicite que ele ative o Teste seguro em sua conta.
1. No Adobe Experience Manager, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagem , no **[!UICONTROL Publicar contexto]** , selecione **[!UICONTROL Testar o fornecimento de imagem]**.
1. Selecione o **[!UICONTROL Segurança]** guia .
1. Para o **[!UICONTROL Endereço do cliente]** filtro, selecione **[!UICONTROL Adicionar]**.
1. No **[!UICONTROL Endereço IP]** digite um endereço IP.
1. No **[!UICONTROL Máscara]** digite uma máscara de rede.

   >[!NOTE]
   >
   >Se você adicionar mais de um endereço IP e uma máscara de rede, ela permitirá *all* Endereços IP para fazer chamadas de ativos e todos aparecem.

1. Faça uma das seguintes opções:

   * Para adicionar mais endereços IP, repita as três etapas anteriores.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página Servidor de imagem, selecione **[!UICONTROL Salvar]**.
1. Faça upload das imagens desejadas para sua conta do Adobe Dynamic Media.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Certifique-se de que algumas imagens estejam marcadas para publicação e outras não estejam marcadas e envie o trabalho de publicação.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine o nome do seu serviço de Teste Seguro acessando **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração geral do Dynamic Media]**.
1. No **[!UICONTROL Servidor]** , localize o nome do servidor à direita de **[!UICONTROL Nome do servidor publicado]**.

Entre em contato com o Adobe Care se o nome do servidor estiver ausente ou se o URL para o servidor não funcionar.

#### Preparar variações do site

Você precisa de duas variações de um site que vincula os ativos publicados e não publicados:

* Versão pública - Vincule ativos usando a sintaxe de URL tradicional do Adobe Dynamic Media.
* Versão de armazenamento temporário - Vincule ativos usando a mesma sintaxe, mas com o nome do site Teste seguro .

#### Executar os testes

Execute os seguintes testes:

1. Verifique se os ativos estão visíveis na rede corporativa.

   Na rede corporativa identificada pelo intervalo de endereços IP definido anteriormente, a versão de preparo do site exibe todas as imagens, independentemente de serem ou não marcadas para publicação. Dessa forma, é possível testar sem disponibilizar acidentalmente as imagens antes de visualizar a aprovação ou o lançamento do produto.

   Confirme se a versão pública do seu site mostra os ativos publicados como anteriormente tinham experiência com o Adobe Dynamic Media.

1. De fora da rede corporativa, verifique se os ativos não publicados (ou seja, não marcados para publicação) estão protegidos do acesso de terceiros.

   Acesse sua rede de fora (como de seu computador doméstico ou por uma conexão 4G/5G) e verifique se a versão pública do site mostra todos os ativos publicados, mas nenhum do conteúdo não publicado.

   Confirme se a versão de armazenamento temporário não mostra nenhum ativo porque você está acessando o serviço de Teste Seguro a partir de um endereço IP não aprovado.



