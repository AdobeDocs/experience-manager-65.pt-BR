---
title: Práticas recomendadas de tradução
seo-title: Translation Best Practices
description: Encontre as práticas recomendadas compiladas pelas equipes de engenharia e consultoria de Adobe para ajudá-lo a trabalhar com projetos de tradução.
seo-description: Find best practices compiled by Adobe engineering and consulting teams to help you get up and running with translation projects.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
feature: Language Copy
exl-id: 01a81c4b-cb30-4f7e-b281-7194ebb5fc70
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 97%

---

# Práticas recomendadas de tradução{#translation-best-practices}

## Geral {#general}

Criar ou expandir uma presença global na Web pode ser um processo complexo, mas com boa antecipação e planejamento, o AEM pode simplificar seus esforços e apoiar suas metas globais de negócios.

* **Crie um plano de expansão global** antes de implementar seu primeiro site. Adaptar um site existente para cobertura global depois de ele ter sido implementado em curto prazo normalmente é mais difícil do que planejar sua expansão global desde o início:

   * Avalie o estado atual da maturidade de localização da sua organização. Determine se você tem **ferramentas**, **processos** e **recursos** disponíveis para realizar a expansão global.
   * Esteja ciente dos **regulamentos globais** e **preferências regionais de idioma**. Crie estruturas e processos de conteúdo flexíveis, que possam acomodar um ambiente de negócios global em constante mudança.

* Defina um modelo de **governança** compatível com seus negócios globais e use mecanismos do AEM, como o MSM e as permissões de usuário, para aplicar o modelo escolhido. Por exemplo, determine se o conteúdo será criado centralmente e “enviado” ou “extraído” para regiões/países. Determine qual conteúdo pode ser desbloqueado e alterado nas regiões geográficas. Determine quem é responsável por iniciar e gerenciar as traduções.
* Se os recursos permitirem, é melhor gerenciar a atividade de tradução a partir de uma equipe central que pode desenvolver conhecimento especializado nas ferramentas, processos e relacionamentos de fornecedores necessários.
* **Planeje**, **crie um protótipo** e **teste** sua estrutura e processos globais para garantir que eles possam sustentar os negócios e que você tenha o suporte necessário das partes interessadas nas regiões geográficas.

## Estrutura do site  {#site-structure}

* Ao projetar a estrutura do site, comece examinando o conteúdo e determine onde e em qual idioma o conteúdo será criado. Esse local deve ser o nível superior do site.
* A prática recomendada é uma **estrutura baseada em idiomas** com até três níveis entre a criação de nível superior e os sites de países.
* Use uma convenção de nomenclatura de site de idioma/país que siga os **padrões W3C**.
* Determine como o conteúdo será distribuído por regiões e países. Considere quais países compartilham idiomas. É recomendável criar matrizes de idioma, uma camada de páginas não ativadas em que o conteúdo traduzido pode ser revisado, modificado e depois enviado ou extraído para um site de país que compartilha esse idioma.
* Há duas abordagens para a criação de matrizes de idioma: usar cópias de idioma ou usar o MSM e as Live Copies.

   * A abordagem de cópia de idioma é a utilizada pela estrutura de integração de tradução pronta para uso do AEM e, portanto, é a maneira mais fácil de começar. A estrutura fornece uma interface que inicialmente facilita a propagação e tradução de alterações de conteúdo da matriz de idioma principal (por exemplo, inglês) para as matrizes de outros idiomas. No entanto, à medida que o projeto cresce, a automação do fluxo de trabalho torna-se cada vez mais necessária para gerenciar a tradução do crescente número de páginas e/ou idiomas.
   * A abordagem do MSM/Live Copy pode ser uma alternativa para casos de uso avançados, em que os sites são maiores e mais complexos. Uma governança forte e a automação do fluxo de trabalho são necessárias desde o início para lidar com os complexos relacionamentos de herança entre as matrizes em inglês e de outros idiomas, além de reduzir o risco de sobrepor traduções existentes. Esse manuseio pode ser realizado com a ajuda de alguns conectores de tradução. Consulte [MSM e sites multilíngues](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) para obter mais informações.

* Se sua matriz de idioma tiver variações globais, uma opção seria usar o MSM para criar uma Live Copy a partir da matriz global para usar na tradução. Por exemplo, se a criação global for realizada em uma matriz de inglês dos EUA, crie uma matriz de inglês internacional como uma Live Copy e como base de tradução para outros idiomas.
* Use o MSM para criar sites de países a partir das matrizes de idioma traduzidas e implantar conteúdo em sites que compartilhem o mesmo idioma. Por exemplo, a matriz de idioma francês pode ser distribuída para sites da França, Bélgica e Suíça.
* Planeje, crie um protótipo e teste antes de iniciar a implementação.

## Processos e métodos de tradução {#translation-processes-and-methods}

* Envolva um **provedor de serviços de localização (LSP)** que tenha conhecimento especializado em tradução e atividades de localização relacionadas. Os LSPs podem ajudar a ampliar seus negócios globais, fornecendo uma ampla variedade de recursos e tecnologias para melhorar a eficiência e economizar com custos de tradução:

   * Alguns LSPs são provedores de serviços e tecnologia. Há também provedores independentes de tecnologia que permitem que muitos LSPs participem de suas plataformas de tradução.
   * A **estrutura de tradução do AEM** permite a integração com vários provedores de tecnologia de tradução, para tradução automática e tradução humana.
   * Saiba como [integrar conectores de LSPs ao seu sistema do AEM](/help/sites-administering/translation.md) para automatizar a tradução de conteúdo ou como criar, exportar e importar manualmente projetos de tradução para testes e casos em que não há um LSP ou provedor de tecnologia de tradução disponível.

* Escolha um **método de tradução** que melhor se adapta ao conteúdo.

   * A **tradução humana** é mais adequada para conteúdo em que as expectativas de mensagens e qualidade são altas e quando o conteúdo permanecerá por algum tempo no site, como em páginas de marketing.
   * A **tradução automática** pode ser uma boa escolha para grandes volumes de tradução em que o tempo de publicação seja crítico, as expectativas de qualidade sejam menores ou os custos de tradução humana sejam proibitivos. A knowledge base de suporte e conteúdos gerados pelo usuário geralmente são traduzidos automaticamente

* Conte com a experiência de provedores de serviços de localização, da Adobe Consulting e dos integradores de sistemas para planejar, criar um protótipo e testar a estrutura multilíngue do site.
