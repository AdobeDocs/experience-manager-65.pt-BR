---
title: Introdução ao  [!DNL Adobe Experience Manager Assets]
description: Saiba o que é o gerenciamento de ativos digitais, seus casos de uso e [!DNL Adobe Experience Manager Asset] oferta.
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Sobre [!DNL Adobe Experience Manager Assets] como uma solução DAM {#administering-assets}

AEM [!DNL Assets] é uma ferramenta de Gerenciamento de ativos digitais (DAM) que faz parte da [!DNL Experience Manager] e permite que sua empresa gerencie e distribua ativos digitais. Os usuários em uma organização podem gerenciar, armazenar e acessar vários tipos de ativos digitais, como imagens, vídeos, documentos, clipes de áudio, arquivos 3D e mídia avançada para uso na Web, em impressão e para distribuição digital.

## O que é o Gerenciamento de ativos digitais? {#what-is-digital-asset-management}

[!DNL Assets] O oferece compartilhamento e distribuição em toda a empresa dos principais ativos digitais de uma organização. Os usuários em uma organização podem armazenar, gerenciar e acessar ativos digitais como imagens, gráficos, áudio, vídeo e documentos por meio de uma interface da Web (ou uma pasta CIFS ou WebDAV).

[!DNL Assets] capacidade de [!DNL Experience Manager] permite fazer o seguinte:

* Adicione e compartilhe imagens, documentos, arquivos de áudio e arquivos de vídeo em vários formatos de arquivo.
* Gerencie ativos agrupando-os por tags, lightbox ou estrelas (seus favoritos). Adicionar anotações aos ativos.
* Localize ativos pesquisando nomes de arquivos, texto completo de documentos e pesquisando datas, tipo de documento e tags.
* Adicione ou edite informações de metadados para ativos. Os metadados são versionados automaticamente junto com o ativo correspondente. É possível importar ou exportar metadados de ativos.
* Execute funções de edição de imagens, como dimensionamento e adição de filtros de imagem. Importe e exporte vários ativos digitais simultaneamente usando uma pasta WebDAV ou CIFS.
* Use fluxos de trabalho e notificações para permitir o processamento e o download em conjunto de qualquer conjunto de ativos e gerenciar direitos de acesso a ativos.

### [!DNL Experience Manager Assets] está integrado com [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] integra-se completamente ao [!DNL Sites] e funciona perfeitamente para todos os casos de uso. Por exemplo, ao criar páginas da Web, a variável [!DNL Sites] os autores podem encontrar e usar os ativos digitais por meio do Localizador de conteúdo. A interface de usuário do [!DNL Assets] é igual ao de [!DNL Sites]. Consulte uma [visão geral do Sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

A interface básica do usuário é a mesma do [!DNL Sites]. Consulte [Visão Geral dos Sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

### Gerenciamento de ativos digitais versus componente de imagem {#digital-asset-management-versus-image-component}

Ao determinar se uma imagem deve ser colocada no repositório DAM ou usar um componente de imagem, considere o ciclo de vida da imagem:

* Se a imagem tiver o mesmo ciclo de vida da página, use o componente de Imagem.
* Se a imagem tiver um ciclo de vida separado, por exemplo, se você usar a imagem duas vezes ou fora do WCM, use [!DNL Assets].

## O que são ativos digitais? {#what-are-digital-assets}

Um ativo é um documento digital, imagem, vídeo ou áudio (ou parte dele) que pode ter várias representações. Ele também pode ter subativos, por exemplo, camadas em um arquivo Photoshop, slides em um arquivo PowerPoint, páginas em um pdf, arquivos em um ZIP.

Um ativo é essencialmente um binário mais metadados mais representações mais subativos. Consulte a [Guia de desempenho do DAM](/help/sites-deploying/assets-performance-sizing.md) para obter informações detalhadas.

>[!CAUTION]
>
>Fazer upload e/ou editar um grande volume de ativos (principalmente imagens) pode afetar o desempenho do [!DNL Experience Manager] implantação.

### [!DNL Experience Manager Assets] terminologia {#aem-assets-terminology}

Ao trabalhar com ativos digitais no [!DNL Experience Manager], será útil se você entender a seguinte terminologia:

* **Coleção**: uma coleção de ativos, com base no local físico (pasta), nas propriedades comuns (pasta de pesquisa salva) ou na seleção de usuários (pastas lightbox).

* **Metadados** [!DNL Assets] ter metadados; por exemplo, autor, data de expiração e Informações de DRM (Digital Rights Management). Os metadados estão sob controle de acesso. [!DNL Assets] O é compatível com os seguintes vários esquemas de metadados comuns prontos para uso:

   * Dublin Core: incluindo autor, descrição, data, assunto e assim por diante.
   * IPTC: incluindo evento, modelo, localização, etc.
   * WCM: inclusão das propriedades da página, [!UICONTROL No Prazo] e [!UICONTROL Tempo desligado]e assim por diante.

* **Marcação**: [!DNL Assets] podem ser marcadas e classificadas. Consulte [organização de ativos](/help/assets/organize-assets.md).

* **Representações**: uma representação é a representação binária de um ativo. [!DNL Assets] sempre tem uma representação primária, que é a do arquivo carregado. Elas podem ter qualquer número de representações adicionais criadas, por exemplo, por etapas de fluxo de trabalho personalizadas ou quando um ativo é carregado. As representações podem ser de um tamanho diferente, com uma resolução diferente, com uma marca d&#39;água adicionada ou alguma outra característica alterada.

* **Versões**: o controle de versão cria um instantâneo dos ativos digitais em um ponto específico do tempo. Você pode restaurar ativos para versões anteriores. Consulte [controle de versão em [!DNL Assets]](manage-assets.md#asset-versioning).

* **Subativos**: os subativos são ativos que compõem um ativo, por exemplo, camadas em um [!DNL Adobe Photoshop] arquivo ou páginas em um arquivo PDF. Entrada [!DNL Assets], é possível gerenciar os subativos da mesma maneira que os ativos.

### Como trabalhar com ativos digitais {#how-to-work-with-assets}

Execute uma ação em um ativo ou coleção. As ações podem criar ou modificar ativos, coleções e representações. Muitas das ações básicas que você executa em ativos - carregar, excluir, atualizar, salvar subativos - acionam fluxos de trabalho pré-configurados. Elas são ativadas automaticamente no [!DNL Assets] e são descritos em detalhes no [!DNL Assets] manipuladores de mídia.

As tarefas que você pode executar com esses workflows pré-configurados:

* Salve o ativo no repositório ou exclua o ativo dele.
* Extrair e salvar metadados para o ativo; os itens de metadados individuais são salvos como XMP.
* Gerar representações e miniaturas para o ativo; incluindo redimensionamento e recorte automáticos quando necessário.
* Transcodifique o ativo onde necessário. Por exemplo, o vídeo para uso em dispositivos móveis e na Web é transcodificado com 24 quadros por segundo, baixe o vídeo com 30 quadros por segundo. O áudio para uso móvel e na Web é transcodificado com 128 Kbps, o áudio para download com 192 Kbps.

Também é possível aplicar workflows manualmente. Consulte [Manipuladores de mídia de ativos](media-handlers.md)para obter uma lista de workflows padrão.

## [!DNL Experience Manager Assets] e [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consulte [Assets e Media Library](medialibrary.md) para obter informações sobre as diferenças.

>[!MORELIKETHIS]
>
>* [Introdução em vídeo - Experience Manager Assets como um DAM moderno](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Entender os conceitos de metadados](/help/assets/metadata-concepts.md)
