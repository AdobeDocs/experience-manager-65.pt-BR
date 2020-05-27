---
title: Sobre os ativos Adobe Experience Manager
description: Saiba o que é gerenciamento de ativos digitais, seus casos de uso e a oferta de ativos do Experience Manager da Adobe
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 55%

---


# Administrar ativos {#administering-assets}

O Assets é uma ferramenta de Gerenciamento de ativos digitais (DAM) totalmente integrada à plataforma Experience Manager e permite que sua empresa compartilhe e distribua ativos digitais. Os usuários em uma organização podem armazenar, gerenciar e acessar imagens, vídeos, documentos, clipes de áudio e mídias avançadas como arquivos Flash para uso na Web, em impressões e para distribuição digital.

## O que é o Gerenciamento de ativos digitais? {#what-is-digital-asset-management}

O Assets oferece compartilhamento e distribuição dos principais ativos digitais de uma organização para toda a empresa. Os usuários em uma organização podem armazenar, gerenciar e acessar ativos digitais como imagens, gráficos, áudio, vídeo e documentos por uma interface da Web (ou uma pasta CIFS ou WebDAV).

Bem integrado ao Experience Manager, o recurso Ativos permite fazer o seguinte:

* Adicionar e compartilhar imagens, documentos, arquivos de áudio e vídeo em vários formatos de arquivos.
* Gerencie ativos agrupando-os por tags, lightbox ou stars (seus favoritos). Adicionar anotações a ativos.
* Encontrar ativos pesquisando por nomes de arquivos, o texto completo de documentos e pesquisando por datas, tipo de documento e marcas.
* Adicionar ou editar informações de metadados para ativos. O controle de versão de metadados ocorre automaticamente juntamente com o ativo correspondente. Você pode importar ou exportar metadados de ativos.
* Executar funções de edição de imagens como redimensionamento e adição de filtros de imagem. Importar e exportar vários ativos digitais simultaneamente usando uma pasta WebDAV ou CIFS.
* Usar fluxos de trabalho e notificações para habilitar o processamento conjunto e o download de qualquer conjunto de ativos e gerenciar direitos de acesso a ativos.

### Os ativos do Experience Manager são integrados aos Sites do Experience Manager {#aem-assets-fully-integrated-in-cq-wcm}

Os ativos são totalmente integrados aos Sites e a funcionalidade está disponível usando o ícone DAM. Os ativos digitais gerenciados no repositório do Assets podem ser acessados pelo localizador de conteúdo ao criar páginas da Web.

A interface básica do usuário é a mesma do Sites. Consulte [Visão geral dos sites](/help/sites-authoring/page-authoring.md) para obter detalhes completos.

### Gerenciamento de ativos digitais versus componente de imagem {#digital-asset-management-versus-image-component}

Ao determinar se uma imagem deve ser colocada no repositório DAM ou usar o componente de imagem, considere o ciclo de vida da imagem:

* Se a imagem tiver o mesmo ciclo de vida que a página, use o Componente de imagem.
* Se a imagem tiver um ciclo de vida separado, por exemplo, se você usar a imagem duas vezes ou fora do WCM, use o Assets.

## O que são ativos digitais? {#what-are-digital-assets}

Um ativo é um documento digital, imagem, vídeo ou áudio (ou parte dele) que pode ter várias representações e subativos (por exemplo, camadas em um arquivo do Photoshop, slides em um arquivo do PowerPoint, páginas em um pdf, arquivos em um ZIP).

Um ativo é essencialmente um binário com metadados, além de representações e subativos. Consulte o [Guia de desempenho de DAM](/help/sites-deploying/assets-performance-sizing.md) para obter informações detalhadas.

>[!CAUTION]
>
>Fazer upload e/ou editar um grande volume de ativos (especialmente imagens) pode afetar o desempenho da sua instância do Experience Manager.

### Terminologia do Experience Manager Assets {#aem-assets-terminology}

Ao trabalhar com ativos digitais no Experience Manager, é necessário compreender a seguinte terminologia:

* **Coleção** Uma coleção de ativos, com base na localização física (pasta), nas propriedades comuns (pasta de pesquisa salva) ou na seleção do usuário (pastas lightbox).

* **Os ativos de metadados** têm metadados; por exemplo, autor, data de expiração, Informações do DRM (Digital Rights Management) e assim por diante. O acesso aos metadados é controlado. O Assets é compatível com os seguintes esquemas comuns dos metadados padrão:

   * Dublin Core: inclui criador, descrição, data, assunto e assim por diante.
   * IPTC: inclui evento, modelo, local e assim por diante.
   * WCM: incluindo as propriedades da página, Tempo  ligado e Tempo [!UICONTROL desligado]e assim por diante.

* **Os ativos de marcação** podem ser marcados e classificados. Consulte Uso de tags e Administração de tags.

* **Representações** Uma representação é a representação binária de um ativo. Os ativos sempre possuem uma representação primária: a do arquivo enviado. Eles podem ter qualquer número de representações adicionais que são criadas, por exemplo, por etapas de fluxo de trabalho personalizadas ou quando um ativo é carregado. As representações podem ter tamanhos diferentes, com uma resolução diferente, com uma marca d&#39;água adicionada ou alguma outra característica alterada.

* **O controle de versão** cria um instantâneo de ativos digitais em um ponto específico no tempo. Você pode restaurar ativos para versões anteriores. See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **Sub-ativos** Sub-ativos são ativos que compõem um ativo, por exemplo, camadas em um arquivo do Adobe Photoshop ou páginas em um arquivo PDF. No Assets, é possível gerenciar subativos como se fossem ativos.

### How to work with assets {#how-to-work-with-assets}

Uma ação é executada em um ativo ou em uma coleção. As ações podem criar ou modificar ativos, coleções e execuções. Muitas das ações básicas executadas em ativos - carregar, excluir, atualizar, salvar subativos - acionam workflows pré-configurados. Esses são ativados automaticamente no Assets e descritos detalhadamente nos manipuladores de mídia do Assets.

As tarefas que você pode executar com esses workflows pré-configurados:

* salvam o ativo no ou excluem o ativo do repositório.
* extraem e salvam metadados para o ativo; os itens individuais são salvos como metadados XMP.
* criam execuções e miniaturas para o ativo; incluindo o redimensionamento automático e recorte onde necessário.
* transcodificação do ativo, se necessário. Por exemplo, um vídeo para uso na Web e em dispositivos móveis é transcodificado com 24 quadros por segundo, e o vídeo para download com 30 quadros por segundo. Um áudio para uso na Web e em dispositivos móveis é transcodificado com 128 kbps, e o áudio para download com 192 kbps.

E claro, é possível aplicar fluxos de trabalho manualmente. Consulte [Manipuladores de mídia do Assets](/help/assets/media-handlers.md) para obter uma lista de fluxos de trabalho padrão.

## Ativos do Experience Manager e MediaLibrary {#cq-dam-vs-cq-medialibrary}

Consulte [Ativos e MediaLibrary](/help/assets/medialibrary.md) para obter informações sobre as diferenças.
