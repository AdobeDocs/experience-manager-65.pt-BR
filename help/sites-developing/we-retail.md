---
title: Implementação de referência do We.Retail
seo-title: We.Retail Reference Implementation
description: We.Retail é uma visualização de tecnologia de uma implementação de referência que ilustra a maneira recomendada de configurar uma presença online com AEM
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 9%

---

# Implementação de referência do We.Retail{#we-retail-reference-implementation}

## Introdução {#introduction}

We.Retail é uma implementação de referência e conteúdo de amostra que ilustra a maneira recomendada de configurar uma presença online com o Adobe Experience Manager.

O We.Retail usa as tecnologias AEM mais recentes, como HTL, layouts responsivos, modelos editáveis, componentes principais e muito mais.

Embora ele ilustre um vertical de varejo, a forma como o site é configurado pode ser aplicada a qualquer vertical e somente os recursos do catálogo de produtos e do carrinho são específicos do varejo.

## Recursos {#features}

Como implementação de referência padrão do AEM, o We.Retail apresenta alguns dos recursos mais eficientes do AEM.

| **Destaque** | **Descrição** | **Interessado?** |
|---|---|---|
| [Estrutura do site globalizada](/help/sites-administering/tc-bp.md) | O We.Retail inclui matrizes de idioma que são copiadas em tempo real para sites específicos de cada país. | [Experimente!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Layout responsivo](/help/sites-authoring/responsive-layout.md) | Todas as páginas apresentam layout responsivo para adaptar dinamicamente à tela e ao tamanho do dispositivo. | [Experimente!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modelos editáveis](/help/sites-developing/page-templates-editable.md) | Todas as páginas são baseadas em modelos editáveis, permitindo que não desenvolvedores adaptem e personalizem os modelos. | [Experimente!](/help/sites-developing/we-retail-editable-templates.md) |
| [Linguagem de modelo HTML ](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) | Todos os componentes são baseados em HTL |  |
| [Recursos de comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md) | Apresenta um catálogo de produtos |  |
| [Sites de comunidades](/help/communities/overview.md) | Permitir que visitantes participem de discussões da comunidade, leiam blogs e muito mais |  |
| [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) | Todos os componentes são baseados nos novos componentes principais e são mais utilizáveis e configuráveis pelo usuário, prontos para uso | [Experimente!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) | A seção Experiências do We.Retail mostra o poder da reutilização de conteúdo por meio de fragmentos de conteúdo. | [Experimente-os!](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md) | Um Fragmento de experiência é um grupo de um ou mais componentes, incluindo conteúdo e layout, que podem ser referenciados nas páginas. | [Experimente-os!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introdução {#getting-started}

O We.Retail é fornecido como conteúdo de amostra de AEM. Para utilizar, basta [comece com o AEM normalmente](/help/sites-deploying/deploy.md#getting-started), certificando-se de que o conteúdo de amostra não esteja desativado.

>[!CAUTION]
>
>O We.Retail não deve ser instalado em instâncias de produção. As instâncias de Produção devem ser iniciadas em `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>O We.Retail é baseado na tecnologia AEM mais recente e, portanto, não é compatível [criação da interface clássica](/help/sites-classic-ui-authoring/home.md).

### Versão mais recente {#latest-version}

Embora o We.Retail seja distribuído com a versão do AEM, as atualizações do conteúdo e de seus recursos podem ser feitas após o lançamento. Por conseguinte, é [baixe a versão mais recente do GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) e depois [upload](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [instalar](/help/sites-administering/package-manager.md#installing-packages) como um pacote na sua instância do AEM.

### Primeiras etapas {#first-steps}

1. Depois que o AEM for iniciado (e/ou que o We.Retail estiver instalado), o site **We.Retail** está disponível no [console de sites](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por exemplo, a página a seguir pode ser aberta e deve parecer como exibida na [apêndice](#appendix) abaixo:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail e Geometrixx {#we-retail-geometrixx}

O Geometrixx e suas muitas encarnações serviram como conteúdo de amostra em versões anteriores do AEM. Desde a versão 6.3, We.Retail é o conteúdo de amostra entregue com AEM e serve como a nova implementação de referência padrão.

O We.Retail é tecnicamente mais robusto e explora a mais recente tecnologia AEM para ser mais flexível e escalável, além de demonstrar os recursos mais recentes do produto.

### Comparação de recursos {#feature-comparison}

A tabela a seguir fornece uma visão geral dos principais recursos disponíveis no We.Retail em comparação ao Geometrixx.

* **Disponível** significa que exemplos do recurso são encontrados no conteúdo de amostra.
* **Não disponível** significa que exemplos do recurso não estão disponíveis no conteúdo de amostra, mas não significa que o recurso em si não esteja.

| **Destaque** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estrutura do site globalizada | Idiomas principais copiados para sites específicos do país | Não disponível |
| Fragmentos de conteúdo | Disponível | Não disponível |
| Fragmentos de experiência | Disponível | Não disponível |
| Layout responsivo | Para todas as páginas | Somente Geometrixx Media |
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
>Essa lista se esforça para ser completa, mas não deve ser considerada exaustiva.

## Contribute {#contribute}

O We.Retail foi lançado como um projeto de código aberto e a versão mais recente do código-fonte pode ser baixada do GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sample-we-retail no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

A versão mais recente também pode ser [baixado diretamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) como um pacote instalável.

Se você encontrar problemas, registre [Problemas do GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Fique à vontade para bifurcar ou contribuir [pull requests](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Visualizar {#preview}

Pré-visualização da página de boas-vindas do We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
