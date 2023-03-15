---
title: Caminho para sua primeira experiência usando o AEM Headless
description: Nesta parte da jornada de desenvolvedor do AEM Headless, você entenderá as etapas para implementar sua primeira experiência headless no AEM, incluindo considerações de planejamento e práticas recomendadas para facilitar ao máximo o seu percurso.
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 99%

---

# Caminho para sua primeira experiência usando o AEM Headless {#path-to-first-experience}

Nesta parte da [jornada de desenvolvedor do AEM Headless,](overview.md) você entenderá as etapas para implementar sua primeira experiência headless no AEM, incluindo considerações de planejamento e práticas recomendadas para facilitar ao máximo o seu percurso.

## A história até agora {#story-so-far}

No documento anterior da jornada do AEM Headless, [Introdução ao AEM Headless ](getting-started.md), você aprendeu a teoria básica sobre o que é um CMS headless. Agora você deve:

* Entender os fundamentos dos recursos headless do AEM.
* Conhecer os pré-requisitos para usar recursos headless do AEM.
* Entender os níveis de integração headless do AEM.
* Poder definir seu projeto em termos de escopo.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto do AEM Headless.

## Objetivo {#objective}

Este documento ajuda você a entender as etapas necessárias para implementar seu primeiro projeto. Após ler esse documento, você deve:

* Entenda considerações importantes sobre o planejamento para criar seu conteúdo.
* Entenda as etapas para implementar o headless no AEM.
* Saiba quais ferramentas e configurações do AEM são necessárias.
* Conhecer as práticas recomendadas para simplificar a sua jornada headless, manter a eficiência na geração de conteúdo e garantir que o conteúdo seja entregue rapidamente.

## Requisitos {#requirements}

Antes de continuar com este documento, verifique se você analisou o documento anterior da jornada do desenvolvedor do AEM Headless, [Introdução ao AEM Headless ](getting-started.md), e certifique-se de que você:

* Satisfaz os requisitos listados.
* Considerou sua própria definição de projeto, incluindo escopo, funções e desempenho.

## Planejamento para o sucesso {#planning-for-success}

Para iniciar seu primeiro projeto headless do AEM, é necessário garantir que você tenha um modelo de conteúdo compatível com a personalização e as atualizações que deseja fazer em todos os canais.

Fora do AEM, também é necessário garantir que você tenha configurado um ambiente de desenvolvimento apropriado se estiver criando um aplicativo do lado do cliente, para que você possa testar o cliente em relação às chamadas de API para o AEM.

### Definição de modelos de conteúdo e APIs {#defining-models}

Você deseja oferecer uma experiência consistente e gerenciar campanhas personalizadas em todos os canais, para que possa visualizar cada canal e superfície individualmente como sua própria estrutura de conteúdo distinta para entrega. No entanto, ter cada canal com seu próprio modelo de conteúdo é algo muito difícil de se manter.

Em vez disso, você deve considerar como o conteúdo em diferentes superfícies está relacionado com base no princípio de organização, como hierarquias de marca e produto, categorias de mercadorias ou superfícies, ou etapas na jornada do cliente. Por exemplo, se você tiver um conjunto de superfícies compatíveis com uma marca específica de carros que você fabrica, talvez queira começar com um modelo de conteúdo para informações gerais que sejam relevantes para o carro inteiro, e então utilizar alguns elementos mais específicos, como o conteúdo necessário para quando o carro estiver dando partida ou quando houver problemas de manutenção. Tal modelo imporá a herança do conteúdo geral da marca de carro e permitirá mudanças com base no contexto específico necessário. Isso também ajuda na gestão de futuras atualizações desse conteúdo, pois é possível impor o controle com base em funções, como o profissional de marketing geral ou o gerente de produto da marca de carro, em comparação com um autor responsável pela experiência de “dar a partida no carro”.

Depois de ter o modelo de conteúdo e uma visão nítida dos vários clientes aos quais o conteúdo precisa ser exibido, é necessário garantir que as APIs GraphQL que permitem o acesso a vários modelos de conteúdo sejam publicadas para todos os clientes que precisam desse conteúdo. Há diferentes opções para se acessar um determinado conteúdo. Você pode solicitar um conteúdo específico que seja estático, o que permite o armazenamento em cache do conteúdo e melhor desempenho. Você também pode solicitar um conteúdo gerado dinamicamente, o que exigirá mais processamento. Certifique-se de que os clientes estejam utilizando as APIs que sejam mais eficientes para suas necessidades empresariais.

## Entender os ambientes {#understanding-environments}

No AEM há três tipos de ambientes: desenvolvimento, preparo e produção.

Os ambientes de desenvolvimento (você pode ter vários) são um local seguro para experimentar e tentar novas ideias. Durante a fase inicial do projeto, a Adobe recomenda o uso dos ambientes de desenvolvimento para experimentar variações de modelos de conteúdo e ver quais fornecem o resultado pretendido para as superfícies.

O ambiente de preparo para projetos headless é usado para validar novas versões de produtos do AEM antes de serem implantados na produção. Mantenha uma lista atualizada dos modelos de conteúdo de produção disponíveis lá e utilize um subconjunto do conteúdo, para que você possa renderizar arquivos JSON e comparar se eles ainda fornecem o mesmo resultado, à medida que novas alterações são feitas por você ou por uma nova versão do AEM

A produção é onde os autores de conteúdo criam e gerenciam seu conteúdo real. As mudanças de modelo na produção devem ser realizadas com cuidado e tendo em mente a compatibilidade com versões anteriores.

Durante o estágio de desenvolvimento, é recomendável trabalhar com um ambiente de desenvolvimento e preparo. À medida que você migra para o teste de desempenho, desejará migrar para o ambiente de produção.

### Cooperação de desenvolvedores e autores de conteúdo {#cooperation}

Os desenvolvedores precisam de um ambiente de desenvolvimento do AEM configurado com os modelos de conteúdo preenchidos. O desenvolvedor cria o cliente que consumirá conteúdo do AEM Headless enquanto os autores de conteúdo ainda estão criando o conteúdo. É por isso que as definições de API são realmente importantes. Ao utilizar o SDK do AEM, o desenvolvedor pode criar um gancho de teste para que os testes de unidade e do cliente possam ser gerados, permitindo que o cliente renderize corretamente o conteúdo.

Os autores de conteúdo criam conteúdo com base nos modelos de conteúdo que foram definidos no ambiente de preparo. Usando a ferramenta de criação de fragmento de conteúdo, o autor criaria um novo fragmento de conteúdo ou editaria um já existente. Antes de publicá-lo, o autor pode visualizar como será a aparência no cliente, trabalhando com o desenvolvedor para mover o modelo de conteúdo para o desenvolvimento ou configurar um ambiente de desenvolvedor apenas para que os autores visualizem a aparência dele no cliente.

## Configurar {#setup}

Antes de começar a usar o headless no AEM, você precisa garantir que todos os recursos necessários estejam habilitados. Esta seção descreve o que é necessário. As etapas serão mais detalhadas posteriormente na [Jornada do desenvolvedor do AEM Headless.](#overview.md)

Também é possível consultar os [recursos adicionais](#additional-resources) para obter mais informações sobre tópicos individuais.

### Configuração {#configuration}

1. Habilitar fragmentos de conteúdo
1. Habilitar GraphQL
1. Configurar o SDK Headless

## Implementar seu primeiro aplicativo headless do AEM

Esta é uma visão geral do que é necessário para implementar seu primeiro aplicativo headless usando o AEM para distribuir o seu conteúdo. Como executar essas etapas será descrito mais detalhadamente em partes posteriores da jornada do desenvolvedor headless.

1. Criar modelos de fragmentos de conteúdo
1. Criar fragmentos de conteúdo
1. Consultar conteúdo com o GraphQL

## Práticas recomendadas     {#best-practices}

Um projeto headless não é bem-sucedido apenas devido à tecnologia implementada, mas também por conta do bom planejamento e governança do projeto. Veja a seguir uma série de práticas recomendadas que autores de conteúdo e desenvolvedores devem manter em mente ao planejar seu projeto.

### Organizar seu conteúdo {#organizing-content}

* Torne sua estrutura tão complexa quanto necessário, mas, ao mesmo tempo, tão simples quanto possível. Estruturas de conteúdo mais simples ajudam a facilitar a governança de conteúdo e melhorar o desempenho do sistema.
* Priorize a reutilização de conteúdo em sua estratégia. Crie submodelos e referências de conteúdo que podem ser reutilizados em vários modelos e canais de nível superior.
* Torne as estruturas de conteúdo o mais autoexplicativas possível, para que os autores de conteúdo possam aprender e se adaptar rapidamente às tarefas de criação.
* Se você tiver restrições de acesso, tente alinhar seu modelo de conteúdo aos requisitos de acesso.
* Quando você tem requisitos de acesso, eles devem orientar sua hierarquia de conteúdo. Agrupe os conteúdos que são editados pelo mesmo grupo de pessoas.
* Agrupe os conteúdos semelhantes em uma pasta.
   * É mais provável que um autor de conteúdo copie e cole um conteúdo já existente para criar novo conteúdo. Portanto, realizar esse processo na mesma pasta o torna mais eficiente.
   * O AEM possibilita que os modelos permitidos sejam definidos por pasta, para que o botão **Criar novo** só mostre os modelos compatíveis com esse local.
* A criação de novos fragmentos de conteúdo no editor de fragmento de conteúdo em linha pode ser simplificada se a pasta raiz estiver definida no modelo. Então o profissional não precisa escolher um local, apenas fornecer um nome, para iniciar a edição da nova referência.

### Criar conteúdo {#authoring}

* Para versões específicas de um canal do seu conteúdo, considere usar variações de fragmento de conteúdo. As variações são sincronizadas com o conteúdo principal para simplificar o gerenciamento de alterações de conteúdo.
* Convide outros produtores de conteúdo para revisar o conteúdo e fornecer feedback com anotações e comentários, que estão disponíveis no editor de fragmento de conteúdo e globalmente através de fragmentos no Admin Console de fragmentos de conteúdo.
* Mantenha as coisas em movimento com o menor número possível de elementos obrigatórios. Os elementos obrigatórios podem bloquear o fluxo de trabalho.

### Criação de conteúdo global {#localization}

* Estabeleça as regras e a governança para a tradução do conteúdo. Para reduzir a carga do sistema, estabeleça a tradução como um processo assíncrono que pode ser executado em intervalos maiores. Reserve um tempo para o controle de qualidade da localização e a correção de erros.
* Aproveite todos os recursos fornecidos pelo seu sistema de tecnologia de tradução que podem ser integrados no AEM, como a memória de tradução.
* Decida se os conteúdos de mídia avançada, como imagens e vídeos, precisam de localização.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Entenda considerações importantes sobre o planejamento para criar seu conteúdo.
* Entenda as etapas para implementar o headless no AEM.
* Saiba quais ferramentas e configurações do AEM são necessárias.
* Conhecer as práticas recomendadas para simplificar a sua jornada headless, manter a eficiência na geração de conteúdo e garantir que o conteúdo seja entregue rapidamente.

Queremos que você se baseie nesse conhecimento fundamental para entender toda a eficiência e flexibilidade do AEM Headless, aproveitando-as em seus próprios projetos. Para fazer isso, você tem algumas opções.

### Escolha sua própria aventura {#choose-your-path}

Não importa qual o seu estilo de aprendizagem, a Adobe quer que você tenha sucesso à medida que inicia seu projeto do AEM Headless.

* Se preferir continuar a **aprender mais sobre os conceitos headless e tecnologias headless do AEM**, você deve continuar sua jornada headless do AEM revisando o documento [Como modelar seu conteúdo como modelos de conteúdo do AEM](model-your-content.md), onde você aprenderá a modelar sua estrutura de conteúdo no AEM.
* Se preferir **aprender na prática**, você pode pular para a [Introdução ao tutorial prático do AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR), onde você participará diretamente do desenvolvimento headless do AEM implementando um projeto simples para expor conteúdo headless do AEM.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de desenvolvimento headless revisando o documento [Como modelar seu conteúdo como Modelos de conteúdo do AEM,](model-your-content.md) veja a seguir alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas que não são necessários para continuar na jornada headless.

* [Jornada de tradução headless do AEM](/help/journey-headless/translation/overview.md) - Essa jornada de documentação oferece uma ampla compreensão da tecnologia headless, como o AEM fornece conteúdo headless e como você pode traduzi-lo.
* [Desenvolvimento headless para o AEM Sites ](/help/sites-developing/headless/introduction.md) - Uma introdução rápida para orientar o desenvolvedor headless do AEM com os recursos necessários
* [Tutoriais AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - Use esses tutoriais práticos para explorar como utilizar as várias opções para fornecer conteúdo a endpoints headless com o AEM e escolha o que é certo para você.
* [Gerenciamento de Conteúdo Headless Usando APIs GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=pt-BR#courses) - Siga este curso para obter uma visão geral da API GraphQL implementada no AEM. Autenticação via AdobeID é necessária.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Este projeto do GitHub inclui aplicativos exemplificativos que destacam APIs GraphQL do AEM.
* [Guia de introdução sem cabeçalho](/help/sites-developing/headless/introduction.md#getting-started) - Uma rápida introdução AEM recursos sem periféricos para usuários já com conhecimento de AEM.
* [Criar modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) - Documentação técnica sobre Modelos de fragmento de conteúdo
* [Criar fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) - Documentação técnica sobre Fragmentos de conteúdo
* [Consultar conteúdo com GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Documentação técnica sobre a API GraphQL
