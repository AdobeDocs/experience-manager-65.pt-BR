---
title: Introdução à [!DNL Adobe Experience Manager Assets].
description: Saiba o que é gerenciamento de ativos digitais, seus casos de uso e [!DNL Adobe Experience Manager Asset] ofertas.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 41%

---


# Sobre [!DNL Adobe Experience Manager Assets] uma solução DAM {#administering-assets}

[!DNL Assets] é uma ferramenta Digital Asset Management (DAM) que faz parte integrante da [!DNL Experience Manager] plataforma e permite que sua empresa gerencie e distribua ativos digitais. Os usuários em uma organização podem gerenciar, armazenar e acessar diversos tipos de ativos digitais, como imagens, vídeos, documentos, clipes de áudio, arquivos 3D e mídias avançadas para uso na Web, na impressão e para distribuição digital.

## O que é o Gerenciamento de ativos digitais? {#what-is-digital-asset-management}

[!DNL Assets]O oferece compartilhamento e distribuição dos principais ativos digitais de uma organização para toda a empresa. Os usuários em uma organização podem armazenar, gerenciar e acessar ativos digitais como imagens, gráficos, áudio, vídeo e documentos por uma interface da Web (ou uma pasta CIFS ou WebDAV).

[!DNL Assets] o recurso de [!DNL Experience Manager] permite fazer o seguinte:

* Adicionar e compartilhar imagens, documentos, arquivos de áudio e vídeo em vários formatos de arquivos.
* Gerencie ativos agrupando-os por tags, lightbox ou stars (seus favoritos). Adicionar anotações a ativos.
* Encontrar ativos pesquisando por nomes de arquivos, o texto completo de documentos e pesquisando por datas, tipo de documento e marcas.
* Adicionar ou editar informações de metadados para ativos. O controle de versão de metadados ocorre automaticamente juntamente com o ativo correspondente. Você pode importar ou exportar metadados de ativos.
* Executar funções de edição de imagens como redimensionamento e adição de filtros de imagem. Importar e exportar vários ativos digitais simultaneamente usando uma pasta WebDAV ou CIFS.
* Usar fluxos de trabalho e notificações para habilitar o processamento conjunto e o download de qualquer conjunto de ativos e gerenciar direitos de acesso a ativos.

### [!DNL Experience Manager Assets] é integrado com [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] integra-se completamente com [!DNL Sites] e funciona perfeitamente em todos os casos de uso. Por exemplo, ao criar páginas da Web, os [!DNL Sites] autores podem encontrar e usar os ativos digitais por meio do Localizador de conteúdo. A interface do usuário de [!DNL Assets] é a mesma que a de [!DNL Sites]. Consulte a [visão geral dos Sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

A interface básica do usuário é a mesma da interface do usuário [!DNL Sites]. Consulte [Visão geral dos sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

### Gerenciamento de ativos digitais versus componente de imagem {#digital-asset-management-versus-image-component}

Ao determinar se uma imagem deve ser colocada no repositório DAM ou usar o componente de imagem, considere o ciclo de vida da imagem:

* Se a imagem tiver o mesmo ciclo de vida que a página, use o Componente de imagem.
* Se a imagem tiver um ciclo de vida separado, por exemplo, se você usar a imagem duas vezes ou fora do WCM, use o [!DNL Assets].

## O que são ativos digitais? {#what-are-digital-assets}

Um ativo é um documento digital, imagem, vídeo ou áudio (ou parte dele) que pode ter várias representações e subativos (por exemplo, camadas em um arquivo do Photoshop, slides em um arquivo do PowerPoint, páginas em um pdf, arquivos em um ZIP).

Um ativo é essencialmente um binário com metadados, além de representações e subativos. Consulte o [Guia de desempenho de DAM](/help/sites-deploying/assets-performance-sizing.md) para obter informações detalhadas.

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] deployment.

### [!DNL Experience Manager Assets] terminologia {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], you need to understand the following terminology:

* **Coleção**: Uma coleção de ativos, com base na localização física (pasta), nas propriedades comuns (pasta de pesquisa salva) ou na seleção do usuário (pastas lightbox).

* **Os metadados** [!DNL Assets] têm metadados; por exemplo, autor, data de expiração, Informações do DRM (Digital Rights Management) e assim por diante. O acesso aos metadados é controlado. [!DNL Assets]O é compatível com os seguintes esquemas comuns dos metadados padrão:

   * Dublin Core: inclui criador, descrição, data, assunto e assim por diante.
   * IPTC: inclui evento, modelo, local e assim por diante.
   * WCM: incluindo as propriedades da página, Tempo  ligado e Tempo [!UICONTROL desligado]e assim por diante.

* **Marcação**: [!DNL Assets] pode ser marcado e classificado. Consulte [organizar ativos](/help/assets/organize-assets.md).

* **Representações**: Uma representação é a representação binária de um ativo. [!DNL Assets] sempre tem uma representação principal - a do arquivo carregado. Eles podem ter qualquer número de representações adicionais que são criadas, por exemplo, por etapas de fluxo de trabalho personalizadas ou quando um ativo é carregado. As representações podem ter tamanhos diferentes, com uma resolução diferente, com uma marca d&#39;água adicionada ou alguma outra característica alterada.

* **Versões**: O controle de versão cria um instantâneo de ativos digitais em um ponto específico no tempo. Você pode restaurar ativos para versões anteriores. See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **Sub-ativos**: Subativos são ativos que compõem um ativo, por exemplo, camadas em um [!DNL Adobe Photoshop] arquivo ou páginas em um arquivo PDF. In [!DNL Assets], you can manage sub-assets as you would assets.

### How to work with assets {#how-to-work-with-assets}

Uma ação é executada em um ativo ou em uma coleção. As ações podem criar ou modificar ativos, coleções e execuções. Muitas das ações básicas executadas em ativos - carregar, excluir, atualizar, salvar subativos - acionam workflows pré-configurados. These are automatically turned on in [!DNL Assets] and are described in detail in [!DNL Assets] media handlers.

As tarefas que você pode executar com esses workflows pré-configurados:

* Salve o ativo no repositório ou exclua-o do repositório.
* Extrair e salvar metadados para o ativo; os itens de metadados individuais são salvos como XMP.
* Gerar representações e miniaturas para o ativo; incluindo o redimensionamento automático e a colheita, quando necessário.
* Transcodifique o ativo, se necessário. Por exemplo, um vídeo para uso na Web e em dispositivos móveis é transcodificado com 24 quadros por segundo, e o vídeo para download com 30 quadros por segundo. O áudio para uso em dispositivos móveis e na Web é transcodificado com 128 Kbps, o áudio para download com 192 Kbps.

E claro, é possível aplicar fluxos de trabalho manualmente. Consulte [Manipuladores de mídia do Assets](/help/assets/media-handlers.md) para obter uma lista de fluxos de trabalho padrão.

## [!DNL Experience Manager Assets] e [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

Consulte [Ativos e MediaLibrary](/help/assets/medialibrary.md) para obter informações sobre as diferenças.
