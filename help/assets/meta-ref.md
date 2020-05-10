---
title: Referência dos esquemas de metadados
description: 'Saiba mais sobre as convenções padrão para descrever metadados de ativos, incluindo Dublin Core, IPTC e outros schemas de metadados. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 2%

---


# Referência dos esquemas de metadados {#metadata-schemata-reference}

A referência a seguir inclui informações sobre esquemas de metadados específicos (em ordem alfabética), bem como uma lista de propriedades e suas definições.

## Dublin Core {#dublin-core}

Os metadados do Dublin Core fornecem um conjunto padronizado de convenções para descrever ativos para facilitar sua localização. Nos ativos AEM, o Dublin Core descreve os ativos digitais, incluindo vídeo, som, imagens e documentos.

O conjunto simples de elementos de metadados principais de Dublin (DCMES) contém 15 elementos de metadados, conforme listados na tabela a seguir. Cada elemento de Dublin Core é opcional e pode ser repetido. Você pode adicionar ou excluir informações de metadados do Dublin Core como faria para metadados específicos de tipos de mídia.

Além do DCMES, existem outros elementos de metadados criados pela iniciativa Dublin Core. Para mais informações, consultar a iniciativa [](https://dublincore.org/) Dublin Core.

| Propriedade | Descrição |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contribuinte | A pessoa ou empresa responsável por contribuir para o conteúdo. |
| cobertura | A localização geográfica ou o período de tempo que o ativo cobre. |
| criadora | A pessoa ou empresa responsável pela criação do conteúdo. |
| date | Data ou período associado ao ativo. |
| descrição | Mais informações sobre o ativo. |
| format | O formato de arquivo, a mídia física ou as dimensões do ativo. O AEM usa `dc:format` para indicar o tipo MIME do ativo. |
| identifier | Uma referência exclusiva ao ativo. |
| language | O idioma do ativo (por exemplo, en para inglês). |
| editor | A pessoa ou empresa responsável por disponibilizar o ativo. |
| relation | Um ativo relacionado. |
| direitos | Informações sobre quem tem os direitos a este ativo. |
| source | Um ativo relacionado do qual o ativo é derivado. |
| assunto | O tópico do ativo. |
| título | Um nome para o ativo. |
| tipo | A natureza ou o gênero do ativo. |

## IPTC {#iptc}

O International Press Telecommunications Council (IPTC) é um consórcio de agências de notícias ao redor do mundo - um de seus objetivos é desenvolver e manter padrões técnicos. O IPTC definiu um conjunto de padrões de metadados de fotos para imagens que são aceitos quase universalmente pelos fotógrafos. Esses padrões de metadados faziam parte do padrão mais amplo conhecido como IPTC Information Interchange Model (IIM), criado nos anos 90.

Embora as informações do cabeçalho IPTC tenham sido substituídas principalmente por XMP, um schema principal IPTC e um schema de extensão estão disponíveis para XMP. Em programas de imagem, as propriedades XMP e IPTC são sincronizadas.
