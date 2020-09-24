---
title: Práticas recomendadas de tradução
seo-title: Práticas recomendadas de tradução
description: Descubra as práticas recomendadas compiladas pelas equipes de engenharia de Adobe e consultoria para ajudá-lo a se familiarizar com os projetos de tradução.
seo-description: Descubra as práticas recomendadas compiladas pelas equipes de engenharia de Adobe e consultoria para ajudá-lo a se familiarizar com os projetos de tradução.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Translation Best Practices{#translation-best-practices}

## Geral {#general}

Criar ou expandir uma presença global na Web pode ser um processo complexo, mas com boas AEM de previsão e planejamento pode simplificar seus esforços e suportar suas metas globais de negócios.

* **Planeje a expansão** global antes de implementar seu primeiro site. A adaptação de um site existente para cobertura global quando o site foi implementado em breve é normalmente mais difícil do que o planejamento para expansão global no início:

   * Avalie o estado atual da maturidade localização de sua organização. Determine se você tem **ferramentas**, **processos** e **recursos** em vigor para suportar a expansão global.
   * Esteja ciente dos regulamentos **** globais e das preferências **linguísticas** regionais. Crie estruturas e processos de conteúdo flexíveis que possam acomodar um ambiente empresarial global em constante mudança.

* Determine um modelo de **governança** que suporte seus negócios globais e use mecanismos AEM como MSM e permissões de usuário para impor seu modelo escolhido. Por exemplo, determine se o conteúdo será criado centralmente e &quot;enviado&quot; ou &quot;puxado&quot; para regiões/países. Determine qual conteúdo pode ser desbloqueado e alterado nas regiões geográficas. Determine quem é responsável por iniciar e gerenciar traduções.
* Se os recursos permitirem, é melhor gerenciar a atividade de tradução de uma equipe central, que pode desenvolver conhecimento sobre as ferramentas, os processos e os relacionamentos dos fornecedores necessários.
* **Planeje**, **protótipo** e **teste** sua estrutura e processos globais para garantir que eles suportem os negócios e que você tenha o suporte necessário das partes interessadas nas regiões geográficas.

## Estrutura do site  {#site-structure}

* Ao projetar a estrutura do site, faça o start examinando o conteúdo e determine onde e em qual conteúdo de idioma é criado. Esse local deve ser o nível superior do site.
* A prática recomendada é uma estrutura **baseada em** idiomas com até três níveis entre a criação de nível superior e os sites de países.
* Use uma convenção de nomenclatura de idioma/site de país que siga os padrões **do** W3C.
* Determine como o conteúdo é distribuído por regiões e países. Considere quais países compartilham idiomas. É recomendável criar mestres de idioma, uma camada de páginas não ativadas, onde o conteúdo traduzido pode ser revisado e modificado e então enviado ou direcionado para um site de um país que compartilha esse idioma.
* Há duas abordagens para a criação de mestres em linguagem: usando cópias de idioma e usando MSM/live copies.

   * A abordagem de cópia de idioma é a utilizada AEM estrutura de integração de tradução pronta para uso, e portanto é a maneira mais fácil de começar. A estrutura fornece uma interface de usuário que facilita inicialmente a propagação e tradução de alterações de conteúdo do idioma principal (por exemplo, inglês) principal para os mestres de idioma. No entanto, à medida que o projeto cresce, a automação do fluxo de trabalho se torna cada vez mais necessária para gerenciar a tradução do número crescente de páginas e/ou idiomas.
   * A abordagem MSM/live copy pode ser uma alternativa para casos de uso avançados, em que os sites são maiores e mais complexos. É necessário um controle forte e uma automação de fluxo de trabalho do start para lidar com as complexas relações de herança entre os mestres em inglês e idioma, e para reduzir o risco de substituir as traduções existentes. Esse manuseio pode ser feito com a ajuda de alguns conectores de tradução. Consulte [MSM e Sites](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) multilíngues para obter mais informações.

* Se o seu idioma principal tem variações globais, uma opção é usar o MSM para criar uma cópia ao vivo do principal global para usar para tradução. Por exemplo, se a criação global for executada em um principal inglês dos EUA, crie um inglês internacional principal como uma cópia ao vivo e base para a tradução para outros idiomas.
* Use a MSM para criar sites de países a partir de mestres de idiomas traduzidos e para distribuir conteúdo para sites que compartilham o mesmo idioma. Por exemplo, a língua francesa principal pode ser distribuída para os sites da França, Bélgica e Suíça.
* Planeje, protótipo e teste primeiro, antes de iniciar a implementação.

## Processos e métodos de tradução {#translation-processes-and-methods}

* Envolva um provedor de serviço de **localização (LSP)** com experiência em tradução e atividades relacionadas. Os LSPs podem ajudar a ampliar sua empresa global fornecendo uma ampla gama de recursos e tecnologias para melhorar a eficiência e economizar custos de tradução:

   * Alguns LSPs são provedores de serviços e tecnologia. Há também provedores independentes de tecnologia que permitem que muitos LSPs participem de suas plataformas de tradução.
   * A Estrutura **de Tradução** AEM apoia a integração com uma variedade de provedores de tecnologia de tradução para tradução automática e humana.
   * Saiba como [integrar conectores LSP no seu sistema](/help/sites-administering/translation.md) de AEM para automatizar a tradução de conteúdo, ou como criar, exportar e importar manualmente os Projetos de tradução para teste e nos casos em que não há LSP ou provedor de tecnologia de tradução.

* Escolha um método **de** tradução mais adequado ao conteúdo.

   * **A tradução** humana é mais adequada para o conteúdo em que as expectativas de mensagens e qualidade são altas e o conteúdo permanecerá disponível por algum tempo no site, como as páginas de marketing.
   * **A tradução** automática pode ser uma boa escolha para volumes em massa de tradução quando o tempo de publicação é crítico, as expectativas de qualidade estão diminuídas ou os custos de tradução humana são proibitivos. A base de conhecimento de suporte e o conteúdo gerado pelo usuário geralmente são traduzidos por computador.

* Confie na experiência de provedores de serviço de localização, consultoria de Adobe e integradores de sistemas para planejar, criar protótipos e testar sua estrutura de site multilíngue.

