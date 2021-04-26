---
title: Implementação de referência We.Retail
seo-title: Implementação de referência We.Retail
description: We.Retail é uma pré-visualização de tecnologia de uma implementação de referência que ilustra a maneira recomendada de configurar uma presença online com o AEM
seo-description: We.Retail é uma pré-visualização de tecnologia de uma implementação de referência que ilustra a maneira recomendada de configurar uma presença online com o AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 12%

---

# Implementação de referência We.Retail{#we-retail-reference-implementation}

## Introdução {#introduction}

We.Retail é uma implementação de referência e um conteúdo de amostra que ilustra a maneira recomendada de configurar uma presença online com o Adobe Experience Manager.

We.Retail utiliza as tecnologias de AEM mais recentes, como HTL, layouts responsivos, modelos editáveis, componentes principais e muito mais.

Embora ilustre um negócio de varejo, a maneira como o site é configurado pode ser aplicada a qualquer segmento vertical, e somente o catálogo de produtos e os recursos do carrinho são específicos do varejo.

## Recursos {#features}

Como AEM implementação de referência padrão, o We.Retail exibe alguns dos recursos mais avançados do AEM.

| **Recurso** | **Descrição** | **Está interessado?** |
|---|---|---|
| [Estrutura de site globalizada](/help/sites-administering/tc-bp.md) | We.Retail inclui matrizes de idioma que são copiadas em tempo real em sites específicos do país. | [Experimente!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Layout responsivo](/help/sites-authoring/responsive-layout.md) | Todas as páginas apresentam layout responsivo para se adaptarem dinamicamente à tela e ao tamanho do dispositivo. | [Experimente!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modelos editáveis](/help/sites-developing/page-templates-editable.md) | Todas as páginas são baseadas em modelos editáveis, permitindo que não desenvolvedores adaptem e personalizem os modelos. | [Experimente!](/help/sites-developing/we-retail-editable-templates.md) |
| [Linguagem de modelo HTML](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) | Todos os componentes são baseados em HTL |  |
| [Recursos do eCommerce](/help/commerce/cif-classic/developing/ecommerce.md) | Apresenta um catálogo de produtos |  |
| [Sites das comunidades](/help/communities/overview.md) | Permitindo que visitantes se juntem a discussões da comunidade, leiam blogs e muito mais |  |
| [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) | Todos os componentes se baseiam nos novos componentes principais e são mais utilizáveis e configuráveis pelo usuário, prontos para uso | [Experimente!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) | A seção Experiências We.Retail mostra o poder da reutilização do conteúdo por meio de fragmentos de conteúdo. | [Experimente-os!](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md) | Um Fragmento de experiência é um grupo de um ou mais componentes, incluindo o conteúdo e o layout que podem ser referenciados nas páginas. | [Experimente-os!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introdução {#getting-started}

We.Retail é fornecido como AEM conteúdo de amostra. Para usar, basta [iniciar AEM como você normalmente usaria](/help/sites-deploying/deploy.md#getting-started), certificando-se de que o conteúdo de amostra não esteja desativado.

>[!CAUTION]
>
>We.Retail não deve ser instalado em instâncias de produção. As instâncias de produção devem ser iniciadas em `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>O We.Retail é baseado na tecnologia de AEM mais recente e, portanto, não oferece suporte à [criação da interface clássica](/help/sites-classic-ui-authoring/home.md).

### Versão mais recente {#latest-version}

Embora o We.Retail seja distribuído com a versão do AEM, as atualizações do conteúdo e de seus recursos podem ser feitas após o lançamento. Portanto, é possível [baixar a versão mais recente do GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) e depois [fazer upload](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [instalá-la](/help/sites-administering/package-manager.md#installing-packages) como um pacote na sua instância de AEM.

### Primeiras etapas {#first-steps}

1. Quando AEM for iniciado (e/ou We.Retail estiver instalado), o site **We.Retail** estará disponível no [console de sites](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por exemplo, a página a seguir pode ser aberta e deve ser exibida conforme mostrado no [apêndice](#appendix) abaixo:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail e Geometrixx {#we-retail-geometrixx}

O Geometrixx e suas muitas encarnações serviram como conteúdo de amostra em versões anteriores do AEM. Desde a versão 6.3, We.Retail é o conteúdo de amostra fornecido com o AEM e serve como a nova implementação de referência padrão.

We.Retail é tecnicamente mais robusta e utiliza a tecnologia de AEM mais recente para ser mais flexível e escalável, além de demonstrar os recursos mais recentes do produto.

### Comparação de recursos {#feature-comparison}

A tabela a seguir fornece uma visão geral dos principais recursos disponíveis no We.Retail em comparação ao Geometrixx.

* **** Disponível: exemplos do recurso são encontrados no conteúdo de amostra.
* **Não** disponível significa que exemplos do recurso não estão disponíveis no conteúdo de amostra, mas não significa que o recurso em si não esteja disponível.

| **Recurso** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estrutura de site globalizada | Mestres de idioma copiados em tempo real em sites específicos de país | Não disponível |
| Fragmentos de conteúdo | Disponível | Não disponível |
| Fragmentos de experiência | Disponível | Não disponível |
| Layout responsivo   | Para todas as páginas | Somente Geometrixx Media |
| Modelos editáveis | Para todas as páginas | Não disponível |
| HTL | Todos os componentes | Limitado |
| Direcionar | Para todas as páginas | Somente Geometrixx Outdoors |
| Screens | Disponível | Não disponível |
| Móvel | Não disponível | Disponível |
| Manuscritos | Não disponível | Disponível |
| Carrossel, download, componentes de gráfico | Não disponível | Disponível |
| Controle de coluna | Substituído pelo contêiner de layout | Disponível |
| Forms | Não disponível | Disponível |
| Campaign | Nenhuma amostra de email | Disponível |

>[!NOTE]
>
>Esta lista esforça-se por ser completa, mas não deve ser considerada exaustiva.

## Contribuir {#contribute}

O We.Retail foi lançado como um projeto de código aberto e a versão mais recente do código-fonte pode ser baixada do GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sample-we-retail no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

A versão mais recente também pode ser [baixada diretamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) como um pacote instalável.

Se encontrar problemas, registre [problemas do GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Sinta-se à vontade para bifurcar ou contribuir com [solicitações de pull](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Visualizar {#preview}

Visualização da página de boas-vindas We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
