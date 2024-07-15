---
title: Introdução ao  [!DNL Adobe Experience Manager Assets]
description: Crie, gerencie, processe e distribua ativos digitais no Experience Manager. Esses guias descrevem práticas recomendadas, recursos de acessibilidade e como usar ativos do AEM 6.5.
hide: true
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 347828d5bf3da01685f19fb43609505b24126c63
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 4%

---


# Cerca de [!DNL Adobe Experience Manager Assets] como uma solução DAM {#administering-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/overview) |
| AEM 6.5 | Este artigo |

O AEM [!DNL Assets] é uma ferramenta de Gerenciamento de Ativos Digitais (DAM) que faz parte da plataforma [!DNL Experience Manager] e permite que sua empresa gerencie e distribua ativos digitais. Os usuários em uma organização podem gerenciar, armazenar e acessar vários tipos de ativos digitais, como imagens, vídeos, documentos, clipes de áudio, arquivos 3D e mídia avançada para uso na Web, em impressão e para distribuição digital.

## O que é o Gerenciamento de ativos digitais? {#what-is-digital-asset-management}

O [!DNL Assets] fornece compartilhamento e distribuição em toda a empresa dos principais ativos digitais de uma organização. Os usuários em uma organização podem armazenar, gerenciar e acessar ativos digitais como imagens, gráficos, áudio, vídeo e documentos por meio de uma interface da Web (ou uma pasta CIF ou WebDAV).

A funcionalidade [!DNL Assets] de [!DNL Experience Manager] permite que você faça o seguinte:

* Adicione e compartilhe imagens, documentos, arquivos de áudio e arquivos de vídeo em vários formatos de arquivo.
* Gerencie ativos agrupando-os por tags, lightbox ou estrelas (seus favoritos). Adicionar anotações aos ativos.
* Localize ativos pesquisando nomes de arquivos, texto completo de documentos e pesquisando datas, tipo de documento e tags.
* Adicione ou edite informações de metadados para ativos. Os metadados são versionados automaticamente junto com o ativo correspondente. É possível importar ou exportar metadados de ativos.
* Execute funções de edição de imagens, como dimensionamento e adição de filtros de imagem. Importe e exporte vários ativos digitais simultaneamente usando uma pasta WebDAV ou CIF.
* Use fluxos de trabalho e notificações para permitir o processamento e o download em conjunto de qualquer conjunto de ativos e gerenciar direitos de acesso a ativos.

### [!DNL Experience Manager Assets] está integrado com [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

O [!DNL Assets] integra-se completamente ao [!DNL Sites] e funciona perfeitamente para todos os casos de uso. Por exemplo, ao criar páginas da Web, os autores do [!DNL Sites] podem localizar e usar os ativos digitais por meio do Localizador de conteúdo. A interface de usuário de [!DNL Assets] é a mesma de [!DNL Sites]. Consulte uma [visão geral do Sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

A interface de usuário básica é a mesma de [!DNL Sites]. Consulte [Visão geral dos sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

### Gerenciamento de ativos digitais versus componente de imagem {#digital-asset-management-versus-image-component}

Ao determinar se uma imagem deve ser colocada no repositório DAM ou usar um componente de imagem, considere o ciclo de vida da imagem:

* Se a imagem tiver o mesmo ciclo de vida da página, use o componente de Imagem.
* Se a imagem tiver um ciclo de vida separado, por exemplo, se você usar a imagem duas vezes ou fora do WCM, use [!DNL Assets].

## O que são ativos digitais? {#what-are-digital-assets}

Um ativo é um documento digital, imagem, vídeo ou áudio (ou parte dele) que pode ter várias representações. Ele também pode ter subativos, por exemplo, camadas em um arquivo Photoshop, slides em um arquivo PowerPoint, páginas em um pdf, arquivos em um ZIP.

Um ativo é essencialmente um binário mais metadados mais representações mais subativos. Consulte o [Guia de desempenho do DAM](/help/sites-deploying/assets-performance-sizing.md) para obter informações detalhadas.

>[!CAUTION]
>
>Carregar e/ou editar um grande volume de ativos (principalmente imagens) pode afetar o desempenho da implantação do [!DNL Experience Manager].

### Terminologia do [!DNL Experience Manager Assets] {#aem-assets-terminology}

Ao trabalhar com ativos digitais no [!DNL Experience Manager], é útil compreender a seguinte terminologia:

* **Coleção**: uma coleção de ativos baseada no local físico (pasta), propriedades comuns (pasta de pesquisa salva) ou seleção de usuário (pastas lightbox).

* **Os metadados** [!DNL Assets] têm metadados; por exemplo, autor, data de expiração e Informações DRM (Digital Rights Management). Os metadados estão sob controle de acesso. [!DNL Assets] oferece suporte aos seguintes vários esquemas de metadados comuns prontos para uso:

   * Dublin Core: incluindo autor, descrição, data, assunto e assim por diante.
   * IPTC: incluindo evento, modelo, localização, etc.
   * WCM: incluindo propriedades de página, [!UICONTROL Momento da ativação] e [!UICONTROL Momento da desativação], e assim por diante.

* **Marcação**: [!DNL Assets] pode ser marcada e classificada. Consulte [organização de ativos](/help/assets/organize-assets.md).

* **Representações**: uma representação é a representação binária de um ativo. [!DNL Assets] sempre tem uma representação primária - a do arquivo carregado. Elas podem ter qualquer número de representações adicionais criadas, por exemplo, por etapas personalizadas de fluxo de trabalho ou quando um ativo é carregado. As representações podem ser de um tamanho diferente, com uma resolução diferente, com uma marca d&#39;água adicionada ou alguma outra característica alterada.

* **Versões**: o controle de versão cria um instantâneo de ativos digitais em um ponto específico no tempo. Você pode restaurar ativos para versões anteriores. Consulte [controle de versão em [!DNL Assets]](manage-assets.md#asset-versioning).

* **Subativos**: os subativos são ativos que compõem um ativo, por exemplo, camadas em um arquivo [!DNL Adobe Photoshop] ou páginas em um arquivo PDF. Em [!DNL Assets], é possível gerenciar ativos secundários da mesma maneira que você faria com os ativos.

### Como trabalhar com ativos digitais {#how-to-work-with-assets}

Execute uma ação em um ativo ou coleção. As ações podem criar ou modificar ativos, coleções e representações. Muitas das ações básicas que você executa em ativos - carregar, excluir, atualizar, salvar subativos - acionam fluxos de trabalho pré-configurados. Eles são ativados automaticamente em [!DNL Assets] e são descritos detalhadamente em [!DNL Assets] manipuladores de mídia.

As tarefas que você pode executar com esses workflows pré-configurados:

* Salve o ativo no repositório ou exclua o ativo dele.
* Extrair e salvar metadados para o ativo; os itens de metadados individuais são salvos como XMP.
* Gerar representações e miniaturas para o ativo; incluindo redimensionamento e recorte automáticos quando necessário.
* Transcodifique o ativo onde necessário. Por exemplo, o vídeo para uso em dispositivos móveis e na Web é transcodificado com 24 quadros por segundo, baixe o vídeo com 30 quadros por segundo. O áudio para uso móvel e na Web é transcodificado com 128 Kbps, o áudio para download com 192 Kbps.

Também é possível aplicar workflows manualmente. Consulte [Assets Media Handlers](media-handlers.md)para obter uma lista de fluxos de trabalho padrão.

## [!DNL Experience Manager Assets] e [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consulte [Assets e Media Library](medialibrary.md) para obter informações sobre as diferenças.

>[!MORELIKETHIS]
>
>* [Introdução ao vídeo - Experience Manager Assets como um DAM moderno](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Compreender os conceitos de metadados](/help/assets/metadata-concepts.md)
