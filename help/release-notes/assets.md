---
title: Notas de versão de [!DNL Adobe Experience Manager Assets] 6.5.
description: Os novos recursos e melhorias para [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 39%

---


# [!DNL Adobe Experience Manager Assets] notas de versão  {#aem-assets-release-notes}

Estes são os principais recursos e destaques da versão [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].

## Integração com [!DNL Adobe Creative Cloud] e workflows criativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]O oferece várias maneiras de se integrar à e compartilhar ativos para uso em fluxos de trabalho nos quais as equipes criativas e de marketing ou empresas colaboram ativamente. [!DNL Adobe Creative Cloud] [!DNL Experience Manager]O 6.5 continua a melhorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Leia para conhecer os recursos e integrações específicos do [!DNL Experience Manager] 6.5 que você pode aproveitar para melhor suportar seus casos de uso de velocidade de conteúdo.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece a colaboração entre criativos e profissionais de marketing no processo de criação de conteúdo. Os profissionais de criação podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem deixar os aplicativos com os quais estão mais familiarizados. Os profissionais de criação podem navegar, pesquisar, fazer check-out e fazer check-in de ativos sem problemas usando o painel no aplicativo nos aplicativos [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] faz parte da  [Creative Cloud para ](https://www.adobe.com/br/creativecloud/business/enterprise.html) oferta empresarial. Para obter mais informações sobre ele, incluindo a configuração necessária da implantação [!DNL Experience Manager], consulte [Link do ativo do Adobe](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

![Pesquisar ativos no Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integração  {#stock}

Sua organização pode usar seu [!DNL Adobe Stock] plano corporativo em [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing. Você pode encontrar, pré-visualização e licenciar rapidamente ativos [!DNL Adobe Stock] que são salvos no Experience Manager, usando os poderosos recursos de DAM de [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

Para obter mais informações, consulte [Usar ativos do Adobe Stock em Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Imagem e licença do Pré-visualização Adobe Stock de dentro dos Experience Manager Assets](assets/stock_image_preview_license_options.png)

*Figura: Pré-visualização de  [!DNL Adobe Stock] imagem e licença de dentro  [!DNL Experience Manager Assets].*

![Pesquise e filtre as imagens licenciadas do Adobe Stock no Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Pesquise e filtre as  [!DNL Adobe Stock] imagens licenciadas em  [!DNL Experience Manager].*

### Referências dinâmicas em [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] usados em  [!DNL Adobe InDesign] arquivos são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados se moverem no repositório. Para obter mais informações, consulte [como gerenciar ativos compostos](/help/assets/managing-linked-subassets.md).

## Recursos do Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] ajuda você a adquirir com facilidade, controlar efetivamente e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários corporativos internos entre dispositivos. Ele ajuda a melhorar a eficiência de compartilhamento de ativos, acelera o tempo de marketing de ativos e elimina o risco de uso que não está em conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Connected Assets {#connectedassets}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de site e os ativos digitais necessários residem em silos diferentes.

[!DNL Experience Manager Sites]O oferece recursos para criar páginas da Web e o é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites.[!DNL Experience Manager Assets] [!DNL Experience Manager] agora suporta o caso de uso acima, integrando  [!DNL Sites] e  [!DNL Assets]. Consulte [como configurar e usar o recurso Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arraste um ativo de uma  [!DNL Experience Manager] implantação em uma  [!DNL Sites] página de uma  [!DNL Experience Manager] implantação diferente](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arraste um ativo de uma  [!DNL Experience Manager] implantação em uma  [!DNL Sites] página em uma  [!DNL Experience Manager] implantação diferente.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] fornece criação aprimorada de rich media e delivery  [!DNL Experience Manager Assets] para impulsionar experiências de ponta que são imersivas e personalizadas. Ao fazer upload de um único ativo principal de alta qualidade e usar nossos visualizadores e renderização em nuvem avançada, você pode fornecer qualquer combinação de execuções dinamicamente para suportar a estratégia de mídia de sua organização.

Para obter mais detalhes sobre os novos recursos [!DNL Dynamic Media], consulte [Notas de versão do Dynamic Media](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Suporte a vídeo 360 {#video-support}

Gerencie seus arquivos de 360 vídeos diretamente em [!DNL Experience Manager] usando os visualizadores de ponta para fornecer experiências de VR a desktops, dispositivos móveis e fones de ouvido VR. Para obter mais informações, consulte [Usar vídeo 360](/help/assets/360-video.md).

### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter instruções adicionais, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Aprimoramentos de acessibilidade {#accessibility-enhancements}

[!DNL Dynamic Media] os visualizadores agora suportam recursos de acessibilidade aprimorados, como suporte a Aria, leitores de tela e texto alternativo. Para obter detalhes adicionais, consulte [Notas de versão dos visualizadores do Dynamic Media](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

## Aprimoramento da experiência de pesquisa {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir de 6.5, os profissionais de marketing podem descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada contra o filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos em Experience Manager](../assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Veja o número de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.*

## Aprimoramento da usabilidade {#usability-enhancement}

Agora você pode selecionar todos os ativos carregados em uma pasta ou de um resultado de pesquisa de uma vez. Isso ajuda a gerenciar vários ativos rapidamente. A caixa de seleção seleciona todos os ativos que se encaixam no cenário, digamos um resultado de pesquisa e não apenas os ativos que estão visíveis na interface [!DNL Experience Manager].

![Use a opção Selecionar tudo para selecionar todos os ativos carregados em um clique.](assets/select-all-in-aem-assets.gif)

*Figura: Use a opção Selecionar tudo para selecionar todos os ativos carregados em um clique.*

## Aprimoramentos de metadados {#metadata-enhancements}

[!DNL Assets] permite criar schemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma nova pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/metadata-config.md#folder-metadata-schema).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [metadados em cascata](/help/assets/metadata-schemas.md#cascading-metadata).

## Aprimoramentos de relatórios {#reporting-enhancements}

Os Fragmentos de conteúdo e compartilhamentos de link estão incluídos no relatório baixado agora. Para obter mais informações, consulte [Relatórios de ativos](/help/assets/asset-reports.md).
