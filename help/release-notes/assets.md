---
title: Notas de versão do AEM Assets
description: Novos recursos e melhorias do Adobe Experience Manager 6.5 Assets.
uuid: f785029d-e0fd-494f-b215-7b4caca4e806
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 1ab34a42-2f0e-4b05-a7b6-2fc8dca07ef5
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# Notas de versão do AEM Assets{#aem-assets-release-notes}

Aqui estão os principais recursos e destaques do lançamento do dos ativos do AEM 6.5 Assets.

## Integração com a Adobe Creative Cloud e fluxos de trabalho criativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

O AEM oferece várias maneiras de se integrar à Adobe Creative Cloud e compartilhar ativos para uso em fluxos de trabalho nos quais as equipes criativas e de marketing ou empresas colaboram ativamente. O AEM 6.5 continua a melhorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Leia para conhecer as funcionalidades e integrações específicas do AEM 6.5 que você pode aproveitar para oferecer um melhor suporte aos casos de uso de velocidade do seu conteúdo.

### Adobe Asset Link {#aal}

O Adobe Asset Link reforça a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. Os criadores podem acessar o conteúdo armazenado no Adobe Experience Manager Assets (AEM Assets), sem deixar os aplicativos que estão mais familiarizados. Elas podem navegar com facilidade, pesquisar, experimentar e verificar ativos usando o painel no aplicativo do Photoshop, Illustrator e InDesign.

O Adobe Asset Link faz farte das ofertas da [Creative Cloud for enterprise](https://www.adobe.com/creativecloud/business/enterprise.html). Para obter mais informações sobre, incluindo a configuração necessária de sua implantação AEM, consulte [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

![Pesquisa de ativos no Photoshop](assets/asset_search_photoshop.png)

### Integração com o Adobe Stock {#stock}

Sua organização pode usar seu plano empresarial do Adobe Stock nos ativos AEM para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing. Você pode encontrar, visualizar e licenciar rapidamente os ativos do Adobe Stock salvos no AEM, usando as poderosas funcionalidades do DAM do AEM.

O serviço do Adobe Stock fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

Para obter mais informações, consulte [Usar ativos do Adobe Stock no AEM Assets](/help/assets/aem-assets-adobe-stock.md).

![Visualize a imagem e a licença do Adobe Stock a partir do AEM Assets](assets/stock_image_preview_license_options.png)

Visualize a imagem e a licença do Adobe Stock a partir do AEM Assets

![Pesquise e filtre as imagens licenciadas do Adobe Stock no AEM](assets/aem-search-filters2.jpg)

Pesquise e filtre as imagens licenciadas do Adobe Stock no AEM

### Dynamic references in Adobe InDesign {#dynamic-references-in-indesign}

O AEM Assets usado nos arquivos do Adobe InDesign são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados se moverem na hierarquia JCR. Para obter mais informações, consulte [Gerenciamento de ativos compostos](/help/assets/managing-linked-subassets.md).

## Recursos do Brand Portal {#brand-portal-capabilities}

AEM Assets Brand Portal ajuda você a adquirir com facilidade, controlar efetivamente e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários corporativos internos entre dispositivos. Ele ajuda a melhorar a eficiência de compartilhamento de ativos, acelera o tempo de marketing de ativos e elimina o risco de uso que não está em conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Connected Assets {#connectedassets}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de site e os ativos digitais necessários residem em silos diferentes.

O AEM Sites oferece recursos para criar páginas da Web e o AEM Assets é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites. O AEM agora dá suporte ao caso de uso acima integrando o AEM Sites e o AEM Assets.

Para obter mais informações, consulte [Usar ativos de um ativo conectado](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastar e soltar ativos de DAM de uma ocorrência do AEM na página Sites em uma ocorrência diferente do AEM](assets/connected-assets-drag-and-drop-only.gif)

Arrastar e soltar ativos de DAM de uma ocorrência do AEM na página Sites em uma ocorrência diferente do AEM

## Dynamic Media {#dynamic-media}

O Dynamic Media oferece a criação avançada de mídia avançada e entrega no AEM Assets para conduzir experiências de ponta que são imersivas e personalizadas. Ao fazer upload de um único ativo mestre de alta qualidade e usar nossa renderização avançada de nuvem e os visualizadores, você pode oferecer qualquer combinação de representações rapidamente para dar suporte à estratégia de mídia da sua organização.

Para obter mais detalhes sobre os novos recursos do Dynamic Media, consulte [Notas de versão do Dynamic Media](https://marketing.adobe.com/resources/help/en_US/s7/release_notes/).

### Suporte para vídeo 360 {#video-support}

Gerencie seus arquivos de vídeo 360 diretamente no AEM usando os visualizadores de ponta do Dynamic Media para oferecer experiências VR a desktops, dispositivos móveis e headsets de VR. Para obter mais informações, consulte [Usar vídeo 360](/help/assets/360-video.md).

### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter instruções adicionais, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Aprimoramentos de acessibilidade {#accessibility-enhancements}

Os visualizadores do Dynamic Media agora incluem suporte para recursos aprimorados de acessibilidade, como suporte Aria, leitores de tela e texto alternativo. Para obter detalhes adicionais, consulte [Notas de versão dos visualizadores do Dynamic Media](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html).

## Aprimoramento da experiência de pesquisa {#search-experience-enhancement}

A partir do AEM 6.5, os profissionais de marketing podem descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada contra o filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos no AEM](../assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa.

## Aprimoramento da usabilidade {#usability-enhancement}

Agora você pode selecionar todos os ativos em uma pasta ou a partir de um resultado de pesquisa de uma só vez. Isso ajuda a gerenciar vários ativos rapidamente. A caixa de seleção seleciona todos os ativos que se ajustam ao cenário, digamos, um resultado de pesquisa e não apenas os ativos visíveis na interface do AEM.

![Use a opção Selecionar tudo para selecionar todos os ativos em um clique.](assets/select-all-in-aem-assets.gif)

Use a opção Selecionar tudo para selecionar todos os ativos em um clique.

## Aprimoramentos de metadados {#metadata-enhancements}

Os ativos permitem criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma nova pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/folder-metadata-schema.md).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [Metadados em cascata](/help/assets/cascading-metadata.md).

## Aprimoramentos de relatórios {#reporting-enhancements}

Os fragmentos de conteúdo e compartilhamentos de link agora estão incluídos no relatório de Ativos baixados. Para obter mais informações, consulte [Relatórios de ativos](/help/assets/asset-reports.md).
