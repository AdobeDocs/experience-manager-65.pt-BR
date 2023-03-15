---
title: Introdução ao AEM Headless
description: Nesta parte da Jornada do desenvolvedor headless do AEM, saiba mais sobre pré-requisitos do AEM headless.
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 100%

---

# Introdução ao AEM Headless {#getting-started}

Nesta parte da [Jornada do desenvolvedor headless do AEM,](overview.md) saiba mais sobre o que é necessário para iniciar seu próprio projeto com o AEM Headless.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Saiba mais sobre o desenvolvimento do CMS headless](learn-about.md), você aprendeu a teoria básica do que é um CMS headless e agora deve:

* Entender os conceitos básicos e a terminologia da entrega de conteúdo headless
* Entender por que e quando a tecnologia headless é necessária
* Saber em nível avançado como os conceitos headless são usados e como eles se relacionam

Este artigo se baseia nesses fundamentos para que você entenda como usar o AEM para implementar uma solução headless.

## Objetivo {#objective}

Este documento ajuda você a entender o AEM headless no contexto de seu próprio projeto. Depois de ler esse documento, você deverá:

* Entender os fundamentos dos recursos headless do AEM.
* Conhecer os pré-requisitos para usar recursos headless do AEM.
* Entender os níveis de integração headless do AEM.
* Poder definir seu projeto em termos de escopo.

## Noções básicas do AEM {#aem-basics}

Antes de definir seu projeto headless no AEM, é importante entender alguns conceitos básicos do AEM.

### Instância do autor {#author}

Em sua forma mais simples, o AEM consiste em uma instância de autor e uma [instância de publicação](#publish) que trabalham em conjunto para criar, gerenciar e publicar seu conteúdo.

O conteúdo começa na instância do autor. É aqui que os autores de conteúdo criam o conteúdo. O ambiente de criação oferece várias ferramentas para que os autores criem, organizem e reutilizem o conteúdo.

### Instância de publicação {#publish}

Depois que o conteúdo é criado na instância do autor, ele deve ser publicado para estar disponível a outros serviços para consumo. Uma instância de publicação contém todo o conteúdo que foi publicado.

### Replicação {#replication}

Replicação é o ato de transferir conteúdo da instância do autor para a instância de publicação. Isso é feito automaticamente pelo AEM quando um autor ou outro usuário com direitos apropriados publica conteúdo.

### Resumo das noções básicas do AEM {#aem-basics-summary}

No nível mais simples, a criação de experiências digitais no AEM requer as seguintes etapas:

1. Os autores de conteúdo criam o conteúdo headless na instância do autor.
1. Quando esse conteúdo estiver pronto, ele será replicado para a instância de publicação.
1. As APIs podem ser chamadas para recuperar esse conteúdo.

O AEM headless desenvolve essa base técnica, oferecendo ferramentas eficientes para gerenciar conteúdo headless que é [descrito na próxima seção.](#aem-headless-basics)

## Noções básicas do AEM Headless {#aem-headless-basics}

Os recursos headless do AEM são baseados em alguns recursos principais. Eles são explicados em detalhes em partes posteriores da jornada. É importante agora apenas saber o básico do que eles fazem e como são chamados.

### Modelos de fragmentos do conteúdo {#content-fragment-models}

Os Modelos de fragmento de conteúdo definem a estrutura dos dados e do conteúdo que você irá criar e gerenciar no AEM. Eles servem como uma espécie de andaime para o conteúdo. Ao optar por criar o conteúdo, os autores escolherão entre os Modelos de fragmento de conteúdo definidos, que os orientarão na criação do conteúdo.

### Fragmentos de conteúdo {#content-fragments}

Os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem que você deixe o conteúdo pronto para uso em vários locais e em vários canais.

Fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

### APIs GraphQL e REST {#apis}

Para modificar o conteúdo de forma headless, o AEM oferece duas APIs robustas.

* A API GraphQL permite criar solicitações para acessar e fornecer Fragmentos de conteúdo.
* A API REST do Assets permite criar e modificar Fragmentos de conteúdo (e outros ativos).

Você aprenderá sobre essas APIs e como usá-las em uma parte posterior da jornada headless do AEM. Ou consulte a seção [recursos adicionais](#additional-resources) para obter a documentação adicional.

## Níveis de integração headless {#integration-levels}

O AEM oferece suporte aos modelos headless completo e tradicional de pilha completa ou headful de um CMS. No entanto, o AEM oferece não apenas essas duas opções exclusivas, mas também a capacidade de oferecer suporte a modelos híbridos que combinam as vantagens de ambos, oferecendo flexibilidade exclusiva para seu projeto headless.

Para garantir a compreensão dos conceitos headless, esta Jornada do desenvolvedor headless do AEM concentra-se no modelo headless puro para colocá-lo em funcionamento o mais rápido possível, sem codificação no AEM.

No entanto, você deve estar ciente das possibilidades híbridas adicionais abertas a você depois de entender os recursos headless do AEM. Esses casos são descritos abaixo para sua percepção. No final da jornada, você será apresentado a esses conceitos com mais detalhes caso essa flexibilidade seja necessária para o seu projeto.

### Você já tem um consumo externo de conteúdo headless, como um aplicativo de página única (SPA). {#already-have-a-spa}

Vamos supor que seu requisito básico seja no mínimo fornecer conteúdo do AEM para um serviço externo já existente.

#### Nível 1: Integração de fragmentos de conteúdo - Modelo headless tradicional {#level-1}

Esse nível de integração é o modelo headless tradicional e permite que os autores de conteúdo criem conteúdo no AEM e o entreguem de forma headless a qualquer número de serviços externos usando o GraphQL ou que editem de serviços externos usando a API de ativos. Nenhuma codificação é necessária no AEM.

Neste modelo, o AEM é usado apenas para criar e distribuir o conteúdo usando os Fragmentos de conteúdo do AEM. A renderização e a interação com o conteúdo são delegadas ao aplicativo externo consumidor, geralmente um aplicativo de página única (SPA).

#### Nível 2: Incorporação do SPA no AEM - Modelo híbrido {#level-2}

Esse nível de integração baseia-se no primeiro nível, mas também permite que o aplicativo externo (SPA) seja incorporado no AEM para que os autores de conteúdo possam visualizar o conteúdo no contexto do aplicativo externo dentro do AEM. O aplicativo também pode oferecer suporte à edição limitada do aplicativo externo dentro do AEM.

Esse nível tem a vantagem de permitir que os autores de conteúdo criem conteúdo de forma flexível no AEM de uma maneira headful, com o conteúdo apresentado em contexto com um SPA externo incorporado, enquanto ainda entregam o conteúdo de forma headless.

#### Nível 3: SPA incorporado e totalmente ativado no AEM - Modelo híbrido {#level-3}

Esse nível de integração baseia-se no nível dois, permitindo que a maioria do conteúdo no SPA externo seja editável no AEM.

### Você ainda não tem um consumidor externo do conteúdo headless, como um aplicativo de página única (SPA). {#do-not-have-a-spa}

Se o objetivo for criar um novo SPA que consuma de forma headless conteúdo do AEM, você pode usar recursos como os Fragmentos de conteúdo para gerenciar seu conteúdo headless e também criar um SPA com estrutura de edição de SPA do AEM.

Usando o Editor de SPA, o SPA não apenas consome conteúdo do AEM, como também é totalmente editável dentro do AEM pelos autores de conteúdo, proporcionando a flexibilidade da entrega headless e da edição no contexto dentro do AEM.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar o seu projeto do AEM headless.

### Conhecimento {#knowledge}

* GraphQL
* Experiência de desenvolvimento na criação de SPAs com estruturas React ou Angular
* Habilidades básicas do AEM para criar fragmentos de conteúdo e usar o editor

### Ferramentas {#tools}

* Acesso à sandbox para testar a implantação do seu projeto
* Instância de desenvolvimento local para modelagem e teste de dados
* SPA externo já existente ou outro consumidor do seu conteúdo AEM headless

## Definindo o seu projeto {#defining-your-project}

Para qualquer projeto bem-sucedido, é importante definir claramente não apenas os requisitos do projeto, mas também as funções e responsabilidades.

### Escopo {#scope}

É importante ter um escopo claramente definido para o projeto. O escopo informa os critérios de aceitação e permite que você estabeleça uma definição de concluído.

A primeira pergunta que você deve fazer é “O que estou tentando alcançar com AEM Headless?” A resposta deve ser, no geral, que você tem ou terá no futuro um aplicativo de experiência que você criou com suas próprias ferramentas de desenvolvimento e não com o AEM. Esse aplicativo de experiência pode ser um aplicativo móvel, um site ou qualquer outro aplicativo de experiência voltado para o cliente final. O objetivo de usar o AEM Headless é alimentar seu aplicativo de experiência com conteúdo criado, armazenado e gerenciado no AEM com APIs de última geração que chamariam o AEM Headless para buscar conteúdo ou até mesmo conteúdo totalmente CRUD diretamente do seu aplicativo de experiência. Se isto não é o que você pretende fazer, então você provavelmente deve [voltar para a documentação do AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) e encontrar a seção que melhor se adapta ao que você deseja realizar.

### Funções e responsabilidades {#roles-responsibilities}

As funções de qualquer projeto individual variam, mas as funções importantes a serem consideradas no conteúdo do desenvolvimento headless do AEM são:

* [Administrador](#administrator)
* [Autor de conteúdo](#content-author)
* [Arquiteto de conteúdo](#content-architect)
* [Desenvolvedor](#developer)

#### Administrador {#administrator}

O administrador é responsável pelas definições básicas e a configuração do sistema. Por exemplo, o administrador configura sua organização no sistema de gerenciamento de usuários da Adobe, referido ao Identity Management System (IMS). O administrador é o primeiro usuário da organização a receber um convite por email da Adobe depois que sua organização tiver sido criada pela Adobe no IMS. O administrador tem a capacidade de fazer logon no IMS e adicionar usuários de outros perfis.

Depois que os usuários são configurados pelo administrador, eles recebem as permissões para acessar todos os recursos do AEM para realizar seu trabalho como colaboradores na entrega do aplicativo de experiência usando o AEM Headless.

O administrador deve ser o usuário que configura o AEM e prepara o ambiente de tempo de execução para habilitar os [autores de conteúdo](#content-author) para criar e atualizar conteúdo e [desenvolvedores](#developer) para usar as APIs que buscam ou modificam o conteúdo para seus aplicativos de experiência.

#### Autor de conteúdo {#content-author}

Os autores de conteúdo criam e gerenciam o conteúdo que é entregue de forma headless pelo AEM. Os autores de conteúdo usam recursos do AEM como Fragmentos de conteúdo e o console de Ativos para gerenciar seu conteúdo.

Os autores de conteúdo devem ter em mente as seguintes práticas recomendadas:

#### Planejamento para a tradução {#translation}

Planeje a tradução bem no início do projeto. Considere o “especialista em tradução” como um perfil separado, cuja responsabilidade é definir qual conteúdo deve ser traduzido e qual não, além de qual conteúdo traduzido poderá ser modificado pelos produtores de conteúdo regionais ou locais.

Crie um plano sobre qual tradução de conteúdo você precisa.

* Você precisa só de línguas diferentes ou também de uma linguagem que se adapte em especificidades regionais?
* Você precisa que o conteúdo de mídia avançada, como imagens e vídeos, sejam diferentes para locais diferentes?

Seja claro sobre o fluxo de trabalho de atualização de conteúdo. Qual é o processo de aprovação que o sistema deve oferecer suporte? Os fluxos de trabalho do AEM podem ser aproveitados para automatizar esse processo?

Observe que a [hierarquia de conteúdo](#content-hierarchy) pode ser aproveitada para facilitar a tradução.

Consulte a seção [recursos adicionais](#additional-resources) para obter a documentação adicional sobre fluxos de trabalho do AEM e ferramentas de tradução, incluindo links para a Jornada de tradução headless do AEM.

##### Aproveitar a hierarquia de conteúdo {#content-hierarchy}

A hierarquia de pastas pode atender a duas principais preocupações com relação à gestão de conteúdo:

* [Tradução](#translation): o AEM gerencia a tradução de conteúdo mantendo cópias do conteúdo em pastas específicas da localidade.
* Organização: as pastas são usadas para definir uma hierarquia de conteúdo necessária para suportar as necessidades de tradução, bem como para gerenciar logicamente os Fragmentos de conteúdo.

O AEM permite uma estrutura de conteúdo flexível e uma hierarquia pode ser arbitrariamente grande. No entanto, é importante perceber que qualquer alteração na estrutura de pastas pode ter consequências não intencionais para consultas existentes que [dependem do caminho do conteúdo.](#developer) Portanto, uma hierarquia bem definida, claramente definida previamente, pode ser útil para os autores de conteúdo.

As pastas também podem ser restritas para permitir apenas determinados tipos de conteúdo (com base nos Modelos de fragmento de conteúdo). É recomendável sempre especificar explicitamente quais modelos são permitidos para todas as pastas na hierarquia. Especificação do conteúdo permitido para uma determinada pasta:

* Impede que os autores de conteúdo criem conteúdo que não pertence à pasta.
* Otimiza o processo de criação de conteúdo filtrando os tipos de conteúdo permitidos na pasta durante a criação para mostrar apenas tipos válidos de conteúdo.

Ao criar uma estrutura de conteúdo apropriada, torna-se mais fácil coordenar a criação de conteúdo headless em todos os canais para maximizar a reutilização do conteúdo. O aproveitamento do conteúdo em vários canais melhora muito a eficiência da produção de conteúdo e o gerenciamento de alterações.

##### Estabeleça boas convenções de nomenclatura {#naming-conventions}

Os nomes dos Fragmentos de conteúdo devem ser descritivos para os autores de conteúdo. O AEM lida de forma transparente com o escape e/ou truncamento dos nomes usados nas IDs no nível do repositório. Portanto, os nomes lógicos fornecidos pelos autores de conteúdo devem sempre ser legíveis e representar o conteúdo.

* Nome incorreto: `cta_btn_1`
* Nome correto: `Call To Action Button`

Consulte a seção [recursos adicionais](#additional-resources) para obter documentação adicional sobre convenções de nomenclatura da página do AEM.

##### Não estenda o aninhamento de conteúdo {#content-nesting}

[Fragmentos de conteúdo](#content-fragments) são usados no AEM para criar conteúdo headless. O AEM aceita até dez níveis de aninhamento de conteúdo para Fragmentos de conteúdo. No entanto, é importante ter em mente que o AEM deve resolver iterativamente cada referência definida no Fragmento de conteúdo principal e verificar se há referências filho em todos os irmãos. Essas operações podem aumentar rapidamente e se tornar uma preocupação de desempenho.

Como regra geral, as referências do Fragmento de conteúdo não devem ser aninhadas além de cinco níveis.

#### Arquiteto de conteúdo {#content-architect}

Os arquitetos de conteúdo analisam os requisitos para os dados que devem ser entregues de forma headless e definem a estrutura desses dados. Essas estruturas são chamadas de [Modelos de fragmentos de conteúdo](#content-fragment-models) no AEM. Os Modelos de fragmentos de conteúdo são usados como a base dos Fragmentos de conteúdo criados pelos autores do conteúdo.

Uma abordagem útil ao definir Modelos de fragmento de conteúdo é criar modelos que mapeiam para os componentes da UX dos aplicativos que consomem o conteúdo.

Como os autores de conteúdo interagem com os modelos continuamente à medida que criam novo conteúdo, o alinhamento dos modelos à UX os ajuda a visualizar a experiência digital resultante. Levando esse alinhamento um passo além, você pode atribuir ícones aos Modelos de fragmento de conteúdo que representam o elemento de UX para que os autores possam intuitivamente selecionar o modelo correto com base em dicas visuais.

#### Desenvolvedor {#developer}

Os desenvolvedores são responsáveis por unir o conteúdo que está sendo criado de forma headless no AEM ao consumidor desse conteúdo, que geralmente pode ser um aplicativo de página única (SPA), um aplicativo Web progressivo (PWA), uma loja virtual ou outro serviço externo ao AEM.

O GraphQL é como se fosse a “cola” entre o AEM e os consumidores de conteúdo headless. O GraphQL é o idioma que consulta o AEM para o conteúdo necessário.

Os desenvolvedores devem ter em mente algumas recomendações básicas ao planejar suas consultas:

* As consultas não devem depender de um caminho fixo (`ByPath`) para recuperar Fragmentos de conteúdo.
   * [Os autores de conteúdo têm controle total sobre a hierarquia do fragmento de conteúdo](#content-hierarchy) e podem fazer alterações que interromperiam essa consulta.
   * Em vez disso, as consultas devem optar por referências de modelo de fragmento de conteúdo com parâmetros de consulta dinâmicos para filtrar os resultados para gerar o conteúdo desejado.
* Para obter o melhor desempenho da consulta, sempre use consultas persistentes no AEM. Elas serão discutidas posteriormente na jornada.
* O GraphQL é declarativo seguindo o lema “Peça exatamente o que você precisa, e obtenha exatamente o que você pediu.” Isso significa que ao criar consultas do GraphQL, sempre evite consultas do tipo `select *` que você pode criar em um banco de dados relacional.

Para uma [implementação headless típica usando o AEM,](#level-1) o desenvolvedor não precisa ter conhecimento de codificação do AEM.

### Requisitos de desempenho {#performance-requirements}

Para que qualquer projeto seja um sucesso, o desempenho deve ser considerado antes que qualquer conteúdo seja criado.

Você deve entender suas expectativas de usuários/visitantes e projetar para isso. Defina objetivos de nível de serviço (SLOs) e os meça para entender se você atende às expectativas de seus usuários.

#### Padrões de tráfego {#traffic-patterns}

Para entender tráfego e os padrões de tráfego, comece reunindo o que você sabe do passado e projete para o crescimento esperado nos próximos anos. Algumas das variáveis mais importantes a serem consideradas:

* Quantas chamadas de API por hora/dia/mês você espera e há potencial para picos e sazonalidade?
* Quantos autores de conteúdo diferentes existem?
* Quantos autores de conteúdo você supõe que trabalharão simultaneamente?
* Qual é a frequência das atualizações de conteúdo?
* Quantos modelos de conteúdo são necessários?
* Quantas instâncias de modelos são necessárias?

#### Frequência das atualizações {#update-frequency}

Frequentemente, diferentes seções de experiências têm frequências diferentes de atualizações de conteúdo. Entender isso é importante para ajustar as configurações de CDN e cache. Isso também é importante para o [Arquitetos de conteúdo](#content-architects) conforme criam modelos para representar seu conteúdo. Considere:

* Alguns tipos de conteúdo devem expirar após um determinado período?
* Há elementos que são específicos do usuário e, portanto, não podem ser armazenados em cache?

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Entender os fundamentos dos recursos headless do AEM.
* Conhecer os pré-requisitos para usar recursos headless do AEM.
* Entender os níveis de integração headless do AEM.
* Poder definir seu projeto em termos de escopo.

Você deve continuar sua jornada headless no AEM revisando o documento a seguir: [Caminho para Sua Primeira Experiência Usando AEM Headless](path-to-first-experience.md) onde aprenderá a configurar as ferramentas necessárias e como começar a pensar em modelar seus dados no AEM.

## Recursos adicionais {#additional-resources}

Mesmo sendo recomendado que você siga para a próxima parte da jornada de desenvolvimento headless revisando o documento [Caminho para Sua Primeira Experiência usando AEM Headless,](path-to-first-experience.md) a seguir estão alguns recursos adicionais e opcionais que fazem uma análise mais profunda sobre alguns conceitos mencionados neste documento, mas eles não são requisitos para continuar na jornada headless.

* [Jornada de Tradução AEM Headless](/help/journey-headless/translation/overview.md) - Essa jornada de documentação oferece uma ampla compreensão da tecnologia headless, como o AEM fornece conteúdo headless e como você pode traduzi-lo.
* [Tutoriais AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - Use esses tutoriais práticos para explorar como utilizar as várias opções para fornecer conteúdo a endpoints headless com o AEM e escolha o que é certo para você.
* [Gerenciamento de Conteúdo Headless Usando APIs GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=pt-BR#courses) - Siga este curso para obter uma visão geral da API GraphQL implementada no AEM. Autenticação via AdobeID é necessária.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Este projeto do GitHub inclui aplicativos exemplificativos que destacam APIs GraphQL do AEM.
* [Conceitos de Criação](/help/sites-authoring/author.md) - Documentação técnica do ambiente de criação do AEM, incluindo detalhes sobre a configuração de publicação do autor
* [Publicar Páginas](/help/sites-authoring/publishing-pages.md) - Documentação técnica para publicação de conteúdo no AEM
* [Convenções de Nomenclatura](/help/sites-developing/naming-conventions.md) - Documentação técnica das restrições de nomenclatura de página no AEM
* [Gerenciador de Vários Sites e Tradução](/help/sites-administering/msm-and-translation.md) - Documentação técnica sobre os recursos avançados de tradução do AEM
* [Fluxos de trabalho AEM](/help/sites-authoring/workflows.md) - Documentação técnica sobre como automatizar fluxos de trabalho no AEM
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) - Documentação técnica dos Fragmentos de Conteúdo.
* [Modelos de Fragmentos de Conteúdo](/help/assets/content-fragments/content-fragments-models.md) - Documentação técnica dos Modelos de Fragmento de Conteúdo.
* [Documentação Técnica do GraphQL](https://graphql.org) - A definição do GraphQL (link externo)
* [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Documentação técnica que explica como criar solicitações para acessar e fornecer Fragmentos de Conteúdo
* [API REST do Assets](/help/assets/assets-api-content-fragments.md) - Documentação técnica que explica como criar e modificar Fragmentos de Conteúdo (e outros ativos)
* [Consultas Persistentes](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) - Documentação técnica sobre consultas persistentes no AEM
* [Headful e Headless no AEM](/help/sites-developing/headful-headless.md) - Uma discussão completa dos níveis de integração headless disponíveis no AEM
