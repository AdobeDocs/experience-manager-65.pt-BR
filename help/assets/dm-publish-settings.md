---
title: Configurar definição de publicação do Dynamic Media para o servidor de imagem
description: Saiba como configurar a configuração de publicação do Dynamic Media para o servidor de imagens para publicar ativos. Você também pode testar seus ativos antes de torná-los públicos.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:46:26.981Z'
TQID: 'https://experienceleague.adobe.com/DfSAGGSoBR-9TOXKA89X3U4VReVbP-Ej70vUK1Zfczk'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 3751
ht-degree: 0%

---

# Configurar definição de publicação do Dynamic Media para o servidor de imagem

As opções de Configuração de publicação do Dynamic Media estão disponíveis somente se o seguinte for verdadeiro:

* Você está executando o Dynamic Media no modo Scene7. Consulte [Habilitar Dynamic Media no modo Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Você tem uma *Configuração existente* do **[!UICONTROL Dynamic Media]** (no **[!UICONTROL Cloud Services]**) no Adobe Experience Manager 6.5.11 ou superior. Consulte [Criar uma configuração de Dynamic Media no Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Você é um administrador de sistema da Experience Manager com privilégios de administrador.

Desenvolvedores e programadores de sites experientes devem usar a Configuração de publicação do Dynamic Media. O Adobe Dynamic Media recomenda que os usuários que alteram as configurações de publicação estejam familiarizados com o Adobe Dynamic Media, padrões e convenções de protocolo HTTP e tecnologia básica de geração de imagens.

A página Configuração de publicação do Dynamic Media estabelece configurações padrão que determinam como os ativos são entregues dos servidores do Adobe Dynamic Media para sites ou aplicativos. Se nenhuma configuração for especificada, o servidor do Adobe Dynamic Media fornecerá um ativo de acordo com uma configuração padrão definida na página Configuração de publicação do Dynamic Media.

Consulte também [Opcional - Configuração do Dynamic Media - Configurações do modo Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) para obter mais tarefas de configuração opcionais.

>[!NOTE]
>
>Atualização do Dynamic Media Classic para o Dynamic Media no Adobe Experience Manager? As páginas [Configurações gerais](/help/assets/dm-general-settings.md) e Configuração de publicação no Dynamic Media são preenchidas previamente com os valores obtidos da sua conta do Dynamic Media Classic. As exceções são todos os valores listados na área **[!UICONTROL Opções de carregamento padrão]** da página Configurações Gerais. Esses valores já estão no Experience Manager. Dessa forma, todas as alterações feitas em **[!UICONTROL Opções de carregamento padrão]**, em qualquer uma das cinco guias, por meio da interface do usuário do Experience Manager, serão refletidas no Dynamic Media, não no Dynamic Media Classic. Todas as outras configurações e valores na página [Configurações gerais](/help/assets/dm-general-settings.md) e na página Configuração de publicação são mantidos entre o Dynamic Media Classic e o Dynamic Media no Experience Manager.

**Para configurar o Servidor de Imagens da Instalação de Publicação do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, clique no ícone Ferramentas e vá para **[!UICONTROL Assets]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagens, na lista suspensa, escolha o contexto de publicação para estabelecer as configurações padrão para fornecer imagens dos Servidores de imagens.

| Publicar contexto | Descrição |
| --- | --- |
| Serviço de imagem | Especifica o contexto das configurações de publicação. |
| Servidor de imagens de teste | Especifica o contexto para testar as configurações de publicação.<br>Somente para novas contas do Dynamic Media, o campo **[!UICONTROL Endereço do cliente]** padrão é definido como `127.0.0.1` automaticamente.<br>Consulte [Testar ativos antes de torná-los públicos](#test-assets-before-making-public). |

1. Use as cinco guias para definir as configurações padrão de contexto de publicação.

   * Guia [Segurança](#security-tab)
   * Guia [Gerenciamento de catálogo](#catalog-management-tab)
   * Guia [Atributos da solicitação](#request-attributes-tab)
   * Guia [Atributos de miniatura comuns](#common-thumbnail-attributes-tab)
   * Guia [Atributos de gerenciamento de cores](#color-management-attributes-tab)

   ![Página de configuração de publicação do Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Página de configuração de publicação do Dynamic Media, com a guia **[!UICONTROL Atributos da solicitação]**&#x200B;selecionada.*<br><br>

1. Quando terminar, próximo ao canto superior direito da página, clique em **[!UICONTROL Salvar]**.

## Guia Segurança {#security-tab}

>[!NOTE]
>
>Não há suporte para as configurações de segurança para o contexto de publicação do *Servidor de Imagens*.

Quando o *Servidor de imagens de teste* estiver definido como contexto de publicação, você poderá definir a seguinte configuração de segurança:

**[!UICONTROL Endereço do cliente]** - Permite especificar um ou mais endereços IP ou intervalos de endereços IP. Quando especificado, as solicitações para este catálogo de imagens originadas de um cliente em um endereço IP não listado são rejeitadas. Essa regra se aplica à entrega de imagens e imagens renderizadas.

![Guia Segurança &#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*A guia Segurança mostrando o campo &quot;permitir&quot; IP.*

## Guia Gerenciamento de catálogo {#catalog-management-tab}

**[!UICONTROL Caminho do arquivo de definição do conjunto de regras]** - Especifica o arquivo que contém as definições do conjunto de regras para o catálogo de imagens.

Consulte também o parâmetro [RuleSetFile](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile) no Guia de Referência de Visualizadores do Dynamic Media.

>[!NOTE]
>
>Se sua conta do Dynamic Media Classic tiver um **[!UICONTROL Caminho do arquivo de definição do conjunto de regras]** selecionado em **[!UICONTROL Configuração]** > **[!UICONTROL Aplicativo]** > **[!UICONTROL Configuração de publicação]**, o Experience Manager buscará o arquivo. Sua conta do Dynamic Media recupera o arquivo da Dynamic Media Classic. O arquivo é então armazenado e disponibilizado nesse campo, quando você abre a página **[!UICONTROL Configuração de publicação do Dynamic Media]** pela primeira vez.

## Guia Atributos da solicitação {#request-attributes-tab}

Essas configurações pertencem à aparência padrão das imagens.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Limite de tamanho da imagem de resposta]** | Obrigatório.<br>Somente para novas contas do Dynamic Media, os limites de tamanho padrão são definidos automaticamente como Largura: `3000` e Altura: `3000` para o **[!UICONTROL Servidor de imagens]** e o **[!UICONTROL Servidor de imagens de teste]**.<br>Especifica a largura e a altura máximas da imagem de resposta que são retornadas ao cliente. O servidor retornará um erro se uma solicitação fizer com que uma imagem de resposta cuja largura, altura ou ambos sejam maiores que essa configuração.<br>Consulte também o parâmetro [MaxPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Solicitar modo de ofuscação]** | Ative se quiser que a codificação base64 seja aplicada a solicitações válidas.<br>Consulte também o parâmetro [RequestObfuscation](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Solicitar modo de bloqueio]** | Ative se quiser que um bloqueio com hash simples seja incluído em solicitações.<br>Consulte também o parâmetro [RequestLock](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de solicitação padrão]** | |
| **[!UICONTROL Sufixo de arquivo de imagem padrão]** | Obrigatório.<br>A extensão de arquivo de dados padrão que é anexada aos valores de campo Caminho do catálogo e MaskPath se o caminho não incluir um sufixo de arquivo.<br>Consulte também o parâmetro [DefaultExt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Nome padrão da fonte]** | Especifica qual fonte será usada se nenhuma fonte for fornecida por uma solicitação de camada de texto. Se especificado, deve ser um valor de nome de fonte válido no mapa de fontes deste catálogo de imagens ou no mapa de fontes do catálogo padrão.<br>Consulte também o parâmetro [DefaultFont](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Imagem padrão]** | Uma imagem padrão é retornada em resposta a uma solicitação em que a imagem solicitada não é encontrada.<br>Consulte também o parâmetro [DefaultImage](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage) no Guia de Referência de Visualizadores do Dynamic Media.<br>**OBSERVAÇÃO**: se a sua conta do Dynamic Media Classic tiver uma **[!UICONTROL Imagem padrão]** selecionada em **[!UICONTROL Configuração]** > **[!UICONTROL Aplicativo]** > **[!UICONTROL Configuração de publicação]**, no grupo **[!UICONTROL Atributos de Solicitação Padrão]**, a Experience Manager buscará o arquivo. O arquivo é então armazenado e disponibilizado nesse campo quando você abre a página **[!UICONTROL Configuração de publicação do Dynamic Media]** pela primeira vez. |
| **[!UICONTROL Modo de imagem padrão]** | Quando a caixa deslizante está habilitada (controle deslizante à direita), a **[!UICONTROL Imagem padrão]** substitui cada camada ausente na imagem de origem pela imagem padrão e retorna o composto como de costume. Quando a caixa do controle deslizante está desativada (controle deslizante à esquerda), a imagem padrão substitui toda a imagem composta, mesmo que a imagem ausente seja apenas uma das várias camadas.<br>Consulte também o parâmetro [DefaultImageMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Tamanho de exibição padrão]** | Obrigatório.<br>Somente para novas contas do Dynamic Media, os tamanhos de exibição padrão são definidos automaticamente como Largura: `1280` e Altura: `1280` para **[!UICONTROL Servidor de imagens]** e **[!UICONTROL Servidor de imagens de teste]**.<br>As restrições do servidor respondem que as imagens não são maiores que essa largura e altura, se a solicitação não especificar explicitamente o tamanho de exibição usando `wid=`, `hei=` ou `scl=`.<br>Consulte também o parâmetro [DefaultPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix) no Guia de Referência do Dynamic Media Viewers. |
| **[!UICONTROL Tamanho padrão da miniatura]** | Obrigatório.<br>Usado em vez do atributo **[!UICONTROL Tamanho de exibição padrão]** para solicitações de miniatura (`req=tmb`). As restrições do servidor respondem que as imagens não são maiores que essa largura e altura se uma solicitação de miniatura (`req=tmb`) não especificar explicitamente o tamanho usando `wid=`, `hei=` ou `scl=`.<br>Consulte também o parâmetro [DefaultThumbPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Cor de fundo padrão]** | Especifica o valor de RGB usado para preencher qualquer área de uma imagem de resposta que não contenha dados reais da imagem.<br>Consulte também o parâmetro [BkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de Codificação do JPEG]** |  |
| **[!UICONTROL Qualidade]** | <br>Especifica os atributos padrão para imagens de resposta do JPEG.<br>Somente para novas contas do Dynamic Media, os valores padrão **[!UICONTROL Qualidade]** são definidos automaticamente como `80` para **[!UICONTROL Servidor de imagens]** e **[!UICONTROL Servidor de imagens de teste]**.<br>Esse campo é definido no intervalo de 1 a 100.<br>Consulte também o parâmetro [JpegQuality](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Redução de resolução cromática]** | Ative ou desative a redução de resolução cromática usada pelos codificadores do JPEG. |
| **[!UICONTROL Modo de reamostragem padrão]** | Especifica os atributos padrão de reamostragem e interpolação a serem usados para dimensionar dados de imagem. Use quando `resMode` não estiver especificado em uma solicitação.<br>Somente para novas contas do Dynamic Media, os modos de reamostragem padrão são automaticamente definidos como `Sharp2` para **[!UICONTROL Servidor de Imagens]** e **[!UICONTROL Servidor de Imagens de Teste]**.<br>Consulte também o parâmetro [ResMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode) no Guia de Referência do Dynamic Media Viewers. |

## Guia Atributos de miniatura comuns {#common-thumbnail-attributes-tab}

Essas configurações pertencem à aparência e ao alinhamento padrão das imagens em miniatura.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Cor de fundo padrão da miniatura]** | Especifica o valor de RGB usado para preencher a área de uma imagem em miniatura de saída que não contém dados de imagem reais. Usado apenas para solicitações de miniatura (`req=tmb`) e quando a configuração **[!UICONTROL Tipo de Miniatura Padrão]** está definida como **[!UICONTROL Ajuste]** ou **[!UICONTROL Textura]**.<br>Consulte também o parâmetro [ThumbBkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento horizontal]** | Especifica o alinhamento horizontal da imagem de miniatura no retângulo da imagem de resposta especificado pelos valores `wid=` e `hei=`.<br>Usado apenas para solicitações de miniatura (`req=tmb`) e quando a configuração **[!UICONTROL Tipo de Miniatura Padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos horizontais para escolher: **[!UICONTROL Alinhamento central]**, **[!UICONTROL Alinhamento esquerdo]** e **[!UICONTROL Alinhamento direito]**.<br>Consulte também o parâmetro [ThumbHorizAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento vertical]** | Especifica o alinhamento vertical da imagem de miniatura no retângulo da imagem de resposta especificado pelos valores `wid=` e `hei=`. Usado apenas para solicitações de miniatura (`req=tmb`) e quando a configuração **[!UICONTROL Tipo de Miniatura Padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos verticais para escolher: **[!UICONTROL Alinhamento superior]**, **[!UICONTROL Alinhamento central]** e **[!UICONTROL Alinhamento inferior]**.<br>Consulte também o parâmetro [ThumbVertAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Tempo de funcionamento padrão do cache]** | Um intervalo de expiração padrão é fornecido em horas, caso um determinado registro de catálogo não contenha um valor de Expiração de catálogo válido. Defina como `-1` para marcar como nunca expirar. <br>Consulte também o parâmetro [Expiration](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Tipo de miniatura padrão]** | Um padrão para o tipo de miniatura é fornecido caso um determinado registro de catálogo não contenha um valor ThumbType de catálogo válido. Usado apenas para solicitações de miniatura (`req=tmb`).<br>Há três tipos de miniaturas para escolher: **[!UICONTROL Cortar]**, **[!UICONTROL Ajustar]** e **[!UICONTROL Textura]**.<br>Consulte também o parâmetro [ThumbType](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Resolução de miniatura padrão]** | Um padrão para a resolução do objeto de miniatura é fornecido caso um determinado registro de catálogo não contenha um valor ThumbRes de catálogo válido. Usado apenas para solicitações de miniatura (`req=tmb`) e quando a configuração **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Textura]**.<br>Consulte também o parâmetro [ThumbRes](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres) no Guia de Referência de Visualizadores do Dynamic Media. |

## Guia Atributos de gerenciamento de cores {#color-management-attributes-tab}

Essas configurações determinam quais perfis de cores ICC são usados para imagens.

**Tentativa de renderização da conversão de cor**
A tentativa de renderização da conversão de cores permite substituir a tentativa de renderização padrão dos perfis de trabalho para determinar como as cores de origem são ajustadas. Usado quando:

1. Um dos perfis ICC padrão é o espaço de cores de destino de uma conversão de cores.
1. Esse perfil caracteriza um dispositivo de saída, como uma impressora ou um monitor.
1. E a tentativa de renderização especificada é válida para esse perfil.

Diferentes intenções de renderização usam regras diferentes para determinar como as cores de origem são ajustadas.

Consulte também o parâmetro [IccRenderIntent](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent) no Guia de Referência de Visualizadores do Dynamic Media.

>[!NOTE]
>
>Em geral, use a tentativa de renderização padrão para a configuração de cor selecionada, que a Adobe testou para atender aos padrões do setor. Por exemplo, se você escolher uma configuração de cor para a América do Norte ou Europa, a tentativa de renderização de conversão de cor padrão será a **[!UICONTROL Colorimétrica relativa]**. Se você escolher uma configuração de cor para o Japão, a tentativa de renderização de conversão de cor padrão é **[!UICONTROL Perceptivo]**.

| Configuração | Características |
| --- | --- |
| **[!UICONTROL Espaço de cor padrão CMYK]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados CMYK. Se **[!UICONTROL Nenhum Especificado]** for escolhido, o gerenciamento de cores será desabilitado para este catálogo de imagens quando as imagens de origem CMYK estiverem envolvidas. Todos os espaços de trabalho CMYK dependem de dispositivos, o que significa que eles se baseiam em combinações reais de tinta e papel. Os espaços de trabalho CMYK que a Adobe fornece são baseados nas condições de impressão comercial padrão.<br> Consulte também o parâmetro [IccProfileCMYK](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Espaço de cor padrão de escala de cinza]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados em tons de cinza. Se **[!UICONTROL Nenhum especificado]** for escolhido, o gerenciamento de cores será desabilitado para este catálogo de imagens quando imagens de origem em tons de cinza estiverem envolvidas.<br>Consulte também o parâmetro [IccProfileGray](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Espaço de cores padrão do RGB]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados do RGB. Se **[!UICONTROL Nenhum Especificado]** for escolhido, o gerenciamento de cores será desabilitado para este catálogo de imagens quando as imagens de origem RGB estiverem envolvidas. Em geral, é melhor escolher o **[!UICONTROL Adobe RGB]** ou o **[!UICONTROL sRGB]**, em vez do perfil de um dispositivo específico (como um perfil de monitor). O **[!UICONTROL sRGB]** é recomendado quando você prepara imagens para a Web ou dispositivos móveis, pois ele define o espaço de cores do monitor padrão usado para exibir imagens na Web. O **[!UICONTROL sRGB]** também é uma boa opção quando você trabalha com imagens de câmeras digitais de nível de consumidor, pois a maioria dessas câmeras usa o sRGB como espaço de cores padrão.<br>Consulte também o parâmetro [IccProfileRBG](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb) no Guia de Referência de Visualizadores do Dynamic Media. |
| **[!UICONTROL Tentativa de renderização da conversão de cores]** | **[!UICONTROL Perceptivo]** - Tem como objetivo preservar a relação visual entre as cores para que seja percebida como natural para o olho humano, mesmo que os próprios valores das cores possam mudar. Esse propósito é adequado para imagens fotográficas com muitas cores fora do gamut. Esta configuração é o propósito de renderização padrão para a indústria de impressão japonesa. |
|  | **[!UICONTROL Colorimétrica Relativa]** - Compara o realce extremo do espaço de cores de origem com o do espaço de cores de destino e desloca todas as cores de acordo. As cores fora do gamut são deslocadas para a cor reproduzível mais próxima no espaço de cores de destino. A Colorimétrica relativa preserva mais das cores originais em uma imagem do que a Perceptual. Esta configuração é a tentativa de renderização padrão para impressão na América do Norte e Europa. |
|  | **[!UICONTROL Saturação]** - Tenta produzir cores vívidas em uma imagem em detrimento da precisão das cores. Esse propósito de renderização é adequado para gráficos de negócios como gráficos ou tabelas, em que as cores saturadas brilhantes são mais importantes do que a relação exata entre as cores. |
|  | **[!UICONTROL Colorimétrica Absoluta]** - Deixa as cores que se enquadram no gamut de destino inalteradas. As cores fora do gamut são cortadas. Não é feito o dimensionamento de cores para o ponto branco de destino. Essa intenção tem como objetivo manter a precisão das cores em detrimento da preservação das relações entre as cores e é adequada para provas para simular a saída de um dispositivo específico. Esse propósito é útil para visualizar como a cor do papel afeta as cores impressas. |

## Testar ativos antes de torná-los públicos {#test-assets-before-making-public}

O Secure Testing ajuda você a definir um ambiente de teste seguro e criar uma solução robusta de business-to-business, com base em um conjunto configurável de endereços IP e intervalos. Essa funcionalidade permite que você associe suas implantações do Adobe Dynamic Media à arquitetura do sistema de gerenciamento de conteúdo e de negócios.

Com o Teste seguro, é possível visualizar a versão de preparo do site com conteúdo não publicado.

Se desejar, crie um ambiente de preparo em vez de disponibilizar os ativos publicamente pelos seguintes motivos:

* Visualizar sites antes do lançamento público (site de preparo).
* Atenda a ativos que exigem acesso restrito, como eCatalogs que mostram preços em um aplicativo web B2B.
* Use ativos protegidos por um firewall como parte de um sistema de gerenciamento de informações de produtos, aplicativo de atendimento ao cliente, local de treinamento etc.

>[!NOTE]
>
>O teste seguro não afeta o acesso ao Adobe Dynamic Media Classic. A segurança do Adobe Dynamic Media Classic permanece consistente e requer as credenciais normais para acessar o Adobe Dynamic Media Classic e os serviços da Web relacionados.

### Como funciona o teste seguro {#how-test-assets-works}

A maioria das corporações usa a Internet com um firewall. O acesso à Internet é possível por meio de determinadas rotas e, normalmente, por meio de um intervalo limitado de endereços IP públicos.

Na rede corporativa, você pode descobrir seu endereço IP público usando sites como o [https://www.whatismyip.com](https://www.whatismyip.com/) ou solicitar essas informações à organização de TI corporativa.

Com testes seguros, o Adobe Dynamic Media estabelece um servidor de imagens dedicado para ambientes de preparo ou aplicativos internos. Qualquer solicitação a esse servidor verifica o endereço IP de origem. Se a solicitação recebida não estiver na lista aprovada de endereços IP, uma resposta de falha será retornada. O Administrador da empresa Adobe Dynamic Media configura a lista aprovada de endereços IP para o ambiente de teste seguro da empresa.

Como a localização da solicitação original deve ser confirmada, o tráfego do serviço de Teste seguro não é roteado por uma rede de distribuição de conteúdo, como o tráfego público do servidor de imagens do Dynamic Media. As solicitações para o serviço de Teste seguro têm uma latência um pouco maior em comparação aos servidores públicos de imagem do Dynamic Media.

Os ativos não publicados estão imediatamente disponíveis nos serviços de teste seguro, sem a necessidade de publicar. Dessa forma, é possível executar uma pré-visualização antes que os ativos sejam publicados no Servidor de imagens voltado para o público.

>[!NOTE]
>
>Os serviços de teste seguro usam o Servidor de catálogo configurado com um contexto de publicação interno. Portanto, se sua empresa estiver configurada para publicar no Teste de segurança, todos os ativos carregados no Adobe Dynamic Media ficarão disponíveis imediatamente nos serviços de Teste de segurança. Essa funcionalidade é verdadeira independentemente de os ativos estarem marcados para publicação durante o upload.

Atualmente, os serviços de teste seguro são compatíveis com os seguintes tipos de ativos e funcionalidades:

* Imagens.
* Vinhetas (solicitações do Servidor de Renderização).
* Os clientes devem solicitar explicitamente o suporte ao Servidor de renderização, que está disponível.
* Conjuntos, incluindo conjuntos de imagens, eCatalog, conjuntos de renderização e conjuntos de mídia.
* Visualizadores padrão do Adobe Dynamic Media.
* Páginas JSP do Adobe Dynamic Media OnDemand.
* Conteúdo estático, como arquivos PDF e vídeos progressivamente disponibilizados.
* Transmissão de vídeo HTTP.
* Transmissão de vídeo progressiva.

Os seguintes tipos de ativos e funcionalidades não são compatíveis no momento:

* Pesquisa no Adobe Dynamic Media Classic Info ou eCatalog
* Transmissão contínua de vídeo RTMP
* Web para impressão
* Serviços UGC (User-Generated Content, conteúdo gerado pelo usuário)

  >[!IMPORTANT]
  >
  >A partir de 1 de maio de 2023, os ativos UGC no Dynamic Media estarão disponíveis para uso por até 60 dias a partir da data do upload. Após 60 dias, os ativos são removidos.

  >[!NOTE]
  >
  >O suporte a ativos de imagem vetorial UGC novos ou existentes no Adobe Dynamic Media terminou em 30 de setembro de 2021.

### Testar o serviço de teste seguro {#test-secure-testing-service}

Para garantir que o serviço de teste seguro funcione conforme o esperado, faça o seguinte:

#### Preparar sua conta

1. Entre em contato com o Atendimento ao cliente da Adobe e solicite que ele ative o Teste seguro em sua conta.
1. No Adobe Experience Manager, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagens, na lista suspensa **[!UICONTROL Contexto de publicação]**, selecione **[!UICONTROL Servidor de imagens de teste]**.
1. Selecione a guia **[!UICONTROL Segurança]**.
1. Para o filtro **[!UICONTROL Endereço do cliente]**, selecione **[!UICONTROL Adicionar]**.
1. No campo **[!UICONTROL Endereço IP]**, digite um endereço IP.
1. No campo **[!UICONTROL Máscara]**, digite uma máscara de rede.

   >[!NOTE]
   >
   >Se você adicionar mais de um endereço IP e uma máscara de rede, isso permitirá que *todos* endereços IP façam chamadas de ativos, e todos eles serão exibidos.

1. Siga uma das seguintes opções:

   * Para adicionar mais endereços IP, repita as três etapas anteriores.
   * Continue com a próxima etapa.

1. No canto superior direito da página Servidor de imagens, selecione **[!UICONTROL Salvar]**.
1. Faça upload das imagens desejadas para sua conta do Adobe Dynamic Media.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Verifique se algumas imagens estão marcadas para publicação e outras estão desmarcadas e envie o trabalho de publicação.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine o nome do seu serviço de Teste Seguro em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuração Geral do Dynamic Media]**.
1. Na página **[!UICONTROL Servidor]**, localize o nome do servidor à direita de **[!UICONTROL Nome do Servidor Publicado]**.

Entre em contato com o Adobe Care se o nome do servidor estiver ausente ou se o URL para o servidor não funcionar.

#### Preparar variações de site

Você precisa de duas variações de um site que vincula os ativos publicados e não publicados:

* Versão pública - Vincule ativos usando a sintaxe tradicional de URL do Adobe Dynamic Media.
* Versão de preparo - Vincule ativos usando a mesma sintaxe, mas com o nome do site de teste seguro.

#### Executar os testes

Execute os seguintes testes:

1. Verifique se os ativos estão visíveis na rede corporativa.

   Dentro da rede corporativa identificada pelo intervalo de endereços IP definido anteriormente, a versão de preparo do site exibe todas as imagens, marcadas para publicação ou não. Dessa forma, você pode testar sem disponibilizar acidentalmente as imagens antes da aprovação de visualização ou do lançamento do produto.

   Confirme se a versão pública do site mostra os ativos publicados conforme anteriormente visto no Adobe Dynamic Media.

1. De fora da rede corporativa, verifique se os ativos não publicados (ou seja, desmarcados para publicação) estão protegidos do acesso de terceiros.

   Acesse sua rede de fora (como de seu computador doméstico ou por uma conexão 4G/5G) e verifique se a versão pública do site mostra todos os ativos publicados, mas nenhum conteúdo não publicado.

   Confirme se a versão de preparo não mostra nenhum ativo porque você está acessando o serviço de Teste seguro de um endereço IP não aprovado.
