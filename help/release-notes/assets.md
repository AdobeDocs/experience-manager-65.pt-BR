---
title: Notas de versão do Adobe Experience Manager Assets
description: Novos recursos e melhorias do Adobe Experience Manager 6.5 Assets.
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 40%

---


# Notas de versão do Adobe Experience Manager Assets {#aem-assets-release-notes}

Estes são os principais recursos e destaques da versão dos ativos Adobe Experience Manager 6.5.

## Integration with [!DNL Adobe Creative Cloud] and creative workflows {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]O oferece várias maneiras de se integrar à e compartilhar ativos para uso em fluxos de trabalho nos quais as equipes criativas e de marketing ou empresas colaboram ativamente. [!DNL Adobe Creative Cloud] [!DNL Experience Manager]O 6.5 continua a melhorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Read on to know the specific capabilities and integrations of [!DNL Experience Manager] 6.5 that you can leverage to best support your content velocity use cases.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece a colaboração entre criativos e profissionais de marketing no processo de criação de conteúdo. Creatives can access content stored in [!DNL Experience Manager Assets], without leaving the apps that they are most familiar with. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign] apps.

[!DNL Adobe Asset Link] faz parte da oferta da [Creative Cloud para empresas](https://www.adobe.com/br/creativecloud/business/enterprise.html) . For more information about it, including necessary configuration of your [!DNL Experience Manager] deployment, see [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

![Pesquisar ativos no Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integração {#stock}

Your organization can use its [!DNL Adobe Stock] enterprise plan within [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for your creative and marketing projects. You can quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in Experience Manager, using the powerful DAM capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

For more info, see [Use Adobe Stock assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Pré-visualização da imagem e da licença do Adobe Stock nos Ativos da Experience Manager](assets/stock_image_preview_license_options.png)

*Figura: imagem de Pré-visualização[!DNL Adobe Stock]e licença de dentro[!DNL Experience Manager Assets].*

![Pesquise e filtre as imagens licenciadas do Adobe Stock no Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Pesquise e filtre as[!DNL Adobe Stock]imagens licenciadas em[!DNL Experience Manager].*

### Dynamic references in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] usados em [!DNL Adobe InDesign] arquivos são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados se moverem no repositório. Para obter mais informações, consulte [como gerenciar ativos](/help/assets/managing-linked-subassets.md)compostos.

## Recursos do Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] ajuda você a adquirir com facilidade, controlar efetivamente e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários corporativos internos entre dispositivos. Ele ajuda a melhorar a eficiência de compartilhamento de ativos, acelera o tempo de marketing de ativos e elimina o risco de uso que não está em conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Connected Assets {#connectedassets}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de site e os ativos digitais necessários residem em silos diferentes.

[!DNL Experience Manager Sites]O oferece recursos para criar páginas da Web e o é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites.[!DNL Experience Manager Assets] [!DNL Experience Manager] agora suporta o caso de uso acima, integrando [!DNL Sites] e [!DNL Assets]. Consulte [como configurar e usar o recurso](/help/assets/use-assets-across-connected-assets-instances.md)Ativos conectados.

![Arraste um ativo de uma [!DNL Experience Manager] implantação em uma [!DNL Sites] página de uma implantação diferente [!DNL Experience Manager]](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arraste um ativo de uma[!DNL Experience Manager]implantação em uma[!DNL Sites]página em uma[!DNL Experience Manager]implantação diferente.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] fornece criação aprimorada de rich media e delivery [!DNL Experience Manager Assets] para impulsionar experiências de ponta que são imersivas e personalizadas. Ao fazer upload de um único ativo principal de alta qualidade e usar nossos visualizadores e renderização em nuvem avançada, você pode fornecer qualquer combinação de execuções dinamicamente para suportar a estratégia de mídia de sua organização.

For more details on new [!DNL Dynamic Media] features see [Dynamic Media Release Notes](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Suporte para vídeo 360 {#video-support}

Manage your 360-video files directly in [!DNL Experience Manager] using the cutting edge viewers to deliver VR-experiences to desktops, mobile and VR-headsets. Para obter mais informações, consulte [Usar vídeo 360](/help/assets/360-video.md).

### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter instruções adicionais, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Aprimoramentos de acessibilidade {#accessibility-enhancements}

[!DNL Dynamic Media] os visualizadores agora suportam recursos de acessibilidade aprimorados, como suporte a Aria, leitores de tela e texto alternativo. Para obter detalhes adicionais, consulte [Notas de versão dos visualizadores do Dynamic Media](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

## Aprimoramento da experiência de pesquisa {#search-experience-enhancement}

[!DNL Experience Manager] A partir de 6.5, os profissionais de marketing podem descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada contra o filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos no Experience Manager](../assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Veja o número de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.*

## Aprimoramento da usabilidade {#usability-enhancement}

Agora você pode selecionar todos os ativos carregados em uma pasta ou de um resultado de pesquisa de uma vez. Isso ajuda a gerenciar vários ativos rapidamente. The check box selects all the assets that fits the scenario, say a search result and not just the assets that are visible in the [!DNL Experience Manager] interface.

![Use a opção Selecionar tudo para selecionar todos os ativos carregados em um clique.](assets/select-all-in-aem-assets.gif)

*Figura: Use a opção Selecionar tudo para selecionar todos os ativos carregados em um clique.*

## Aprimoramentos de metadados {#metadata-enhancements}

[!DNL Assets] permite criar schemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma nova pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/folder-metadata-schema.md).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [Metadados em cascata](/help/assets/cascading-metadata.md).

## Aprimoramentos de relatórios {#reporting-enhancements}

Os Fragmentos de conteúdo e compartilhamentos de link estão incluídos no relatório baixado agora. Para obter mais informações, consulte [Relatórios de ativos](/help/assets/asset-reports.md).
