---
title: Notas de versão de  [!DNL Adobe Experience Manager Assets] 6.5.
description: Os novos recursos e aprimoramentos para [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].
exl-id: 6d9c9f09-ea42-43fb-98f7-12ce82d308bf
source-git-commit: 62544559020b0c0afd7bb31fb832b82ba3d47919
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 34%

---

# [!DNL Adobe Experience Manager Assets] notas de versão {#aem-assets-release-notes}

Aqui estão os principais recursos e destaques da versão [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].

## Integração com [!DNL Adobe Creative Cloud] e workflows criativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]O oferece várias maneiras de se integrar à e compartilhar ativos para uso em fluxos de trabalho nos quais as equipes criativas e de marketing ou empresas colaboram ativamente. [!DNL Adobe Creative Cloud] [!DNL Experience Manager]O 6.5 continua a melhorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Leia para conhecer os recursos e integrações específicos do [!DNL Experience Manager] 6.5 que você pode usar para melhor suportar seus casos de uso de velocidade do conteúdo.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. Os criadores podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem deixar os aplicativos com os quais estão mais familiarizados. Os criadores podem navegar, pesquisar, sair e fazer check-in com facilidade em ativos usando o painel no aplicativo em [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign] aplicativos.

[!DNL Adobe Asset Link] faz parte do  [Creative Cloud for ](https://www.adobe.com/br/creativecloud/business/enterprise.html) enterprise offer. Para obter mais informações sobre isso, incluindo a configuração necessária de sua implantação [!DNL Experience Manager], consulte [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

![Pesquisar ativos no Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integração {#stock}

Sua organização pode usar seu [!DNL Adobe Stock] plano corporativo dentro de [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing. Você pode encontrar, visualizar e licenciar rapidamente ativos [!DNL Adobe Stock] salvos no Experience Manager, usando os poderosos recursos do DAM de [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

Para obter mais informações, consulte [Usar ativos do Adobe Stock no Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Visualizar imagem e licença do Adobe Stock no Experience Manager Assets](assets/stock_image_preview_license_options.png)

*Figura: Visualize a  [!DNL Adobe Stock] imagem e a licença de dentro do  [!DNL Experience Manager Assets].*

![Pesquise e filtre as imagens licenciadas do Adobe Stock no Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Pesquise e filtre as  [!DNL Adobe Stock] imagens licenciadas em  [!DNL Experience Manager].*

### Referências dinâmicas em [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] usados em  [!DNL Adobe InDesign] arquivos são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados se moverem no repositório. Para obter mais informações, consulte [como gerenciar ativos compostos](/help/assets/managing-linked-subassets.md).

## Recursos do Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] ajuda você a adquirir com facilidade, controlar efetivamente e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários corporativos internos entre dispositivos. Ele ajuda a melhorar a eficiência de compartilhamento de ativos, acelera o tempo de marketing de ativos e elimina o risco de uso que não está em conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

## Connected Assets {#connectedassets}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de site e os ativos digitais necessários residem em silos diferentes.

[!DNL Experience Manager Sites]O oferece recursos para criar páginas da Web e o é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites.[!DNL Experience Manager Assets] [!DNL Experience Manager] O agora é compatível com o caso de uso acima, integrando  [!DNL Sites] e  [!DNL Assets]. Consulte [como configurar e usar o recurso Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

![Arraste um ativo de uma  [!DNL Experience Manager] implantação em uma  [!DNL Sites] página de uma  [!DNL Experience Manager] implantação diferente](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arraste um ativo de uma  [!DNL Experience Manager] implantação em uma  [!DNL Sites] página de uma  [!DNL Experience Manager] implantação diferente.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] O oferece criação avançada de mídia avançada e entrega  [!DNL Experience Manager Assets] para impulsionar experiências de ponta que são imersivas e personalizadas. Ao fazer upload de um único ativo principal de qualidade e usar a renderização avançada em nuvem e os visualizadores do Adobe, você pode fornecer qualquer combinação de representações dinamicamente para dar suporte à estratégia de mídia de sua organização.

Para obter mais detalhes sobre os novos recursos [!DNL Dynamic Media], consulte [Notas de versão do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Suporte para vídeo 360 {#video-support}

Gerencie seus arquivos de vídeo 360 diretamente em [!DNL Experience Manager] usando os visualizadores de ponta para fornecer experiências VR a desktops, dispositivos móveis e headsets VR. Para obter mais informações, consulte [Usando o vídeo 360](/help/assets/360-video.md).

### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter instruções adicionais, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Aprimoramentos de acessibilidade {#accessibility-enhancements}

[!DNL Dynamic Media] os visualizadores agora oferecem suporte para recursos de acessibilidade aprimorados, como suporte para Aria, leitores de tela e texto alternativo. Para obter detalhes adicionais, consulte [Guia de referência de visualizadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

## Aprimoramento da experiência de pesquisa {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir da versão 6.5, os profissionais de marketing podem descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada contra o filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos no Experience Manager](../assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Veja o número de ativos sem filtrar os resultados da pesquisa nos aspectos de pesquisa.*

## Aprimoramento da usabilidade {#usability-enhancement}

Agora é possível selecionar todos os ativos carregados em uma pasta ou de um resultado de pesquisa de uma só vez. Isso ajuda a gerenciar vários ativos rapidamente. A caixa de seleção seleciona todos os ativos que se encaixam no cenário, digamos um resultado de pesquisa, e não apenas os ativos que estão visíveis na interface [!DNL Experience Manager].

![Use a opção Selecionar tudo para selecionar todos os ativos carregados com um clique.](assets/select-all-in-aem-assets.gif)

*Figura: Use a opção Selecionar tudo para selecionar todos os ativos carregados com um clique.*

## Aprimoramentos de metadados {#metadata-enhancements}

[!DNL Assets] permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/metadata-config.md#folder-metadata-schema).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [metadados em cascata](/help/assets/metadata-schemas.md#cascading-metadata).

## Aprimoramentos de relatórios {#reporting-enhancements}

Os Fragmentos de conteúdo e compartilhamentos de link agora estão incluídos no relatório baixado. Para obter mais informações, consulte [Relatórios de ativos](/help/assets/asset-reports.md).
