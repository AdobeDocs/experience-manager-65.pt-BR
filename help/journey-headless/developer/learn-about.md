---
title: Saiba mais sobre o desenvolvimento sem periféricos do CMS
description: Nesta parte da Jornada de desenvolvedores sem periféricos AEM, saiba mais sobre a tecnologia sem periféricos e por que usá-la.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Saiba mais sobre o desenvolvimento sem periféricos do CMS {#learn-about}

Nesta parte do [AEM Jornada de desenvolvedor sem periféricos,](overview.md) saiba mais sobre tecnologia sem interface e por que usá-la.

## Objetivo {#objective}

Este documento ajuda você a entender a entrega de conteúdo sem periféricos e por que ele deve ser usado. Depois de ler, você deve:

* Entenda os conceitos básicos e a terminologia da entrega de conteúdo sem periféricos
* Entenda por que e quando o headless é necessário
* Saiba em alto nível como os conceitos sem interface são usados e como eles se relacionam

## Entrega de conteúdo em pilha completa {#full-stack}

Desde o aumento dos sistemas de gerenciamento de conteúdo (CMSs) fáceis de usar e em larga escala, as organizações os aproveitaram como um local central para gerenciar mensagens, identidade visual e comunicações. Usar o CMS como ponto central para administrar experiências melhorou a eficiência, eliminando a necessidade de duplicar tarefas em sistemas diferentes.

![O CMS clássico de pilha completa](assets/full-stack.png)

Em um CMS de pilha completa, toda a funcionalidade de manipulação de conteúdo está no CMS. Os recursos do sistema constituem componentes diferentes da pilha do CMS. A solução de pilha completa tem muitas vantagens.

* Você tem um sistema para manter.
* O conteúdo é gerenciado centralmente.
* Todos os serviços do sistema estão integrados.
* A criação de conteúdo é contínua.

Portanto, se quiser adicionar um novo canal ou suportar novos tipos de experiências, poderá inserir um (ou mais) novo componente na sua pilha e terá apenas um local para fazer as alterações.

![Adicionar um novo canal à pilha](assets/adding-channel.png)

A complexidade das dependências na pilha rapidamente se torna aparente, pois você vê que outros itens na pilha podem precisar ser ajustados para acomodar as alterações.

## Limites da entrega em pilha completa {#limits}

A abordagem de pilha completa cria inerentemente um silo em que todas as experiências acabam em um sistema. As alterações ou adições a um componente do silo exigem alterações em outros componentes que podem fazer mudanças demoradas e caras.

Isto é particularmente verdade no que respeita ao sistema de apresentação, que, nas configurações tradicionais, está frequentemente vinculado ao SCC. Qualquer novo canal geralmente significa uma atualização do sistema de apresentação, que pode afetar todos os outros canais.

![A complexidade aumenta à medida que os canais são adicionados a uma pilha](assets/presentation-complexity.png)

As limitações desse silo natural podem se tornar evidentes à medida que você se esforça para coordenar as alterações em todos os componentes da pilha.

Os usuários esperam engajamento independentemente da plataforma ou do ponto de contato, o que requer agilidade na maneira como você apresenta suas experiências.  Essa abordagem multicanal é o padrão das experiências digitais e uma abordagem de pilha completa pode, em determinadas circunstâncias, se revelar inflexível.

## A Cabeça em Sem Cabeça {#the-head}

O cabeçalho de qualquer sistema é geralmente o renderizador de saída desse sistema, normalmente na forma de uma GUI ou outro resultado gráfico.

Um servidor sem periféricos, por exemplo, provavelmente está sentado em um rack em uma sala de servidor em algum lugar e não tem monitor conectado. Para acessá-lo, você precisa se conectar remotamente a ele. Nesse caso, o monitor é o cabeçalho à medida que resolve a renderização da saída do servidor. Como consumidor do serviço, forneça seu próprio cabeçalho (o monitor) ao se conectar remotamente a ele.

Quando falamos de um CMS sem interface, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, apenas entregando a variável **conteúdo** de forma padronizada, um CMS sem periféricos omita a renderização final de output, deixando o **apresentação** do conteúdo para o serviço de consumo.

![CMS sem periféricos](assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, um webshop, experiências móveis, aplicativos web progressivos (PWA), etc., absorvem conteúdo do CMS sem cabeçalho e fornecem sua própria renderização. Eles cuidam de fornecer suas próprias cabeças para o seu conteúdo.

Omitir a cabeça simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Desvinculação {#decoupling}

A entrega sem interface é possível ao expor um conjunto de APIs (Application Programming Interfaces, interfaces de programação de aplicativos) robustas e flexíveis que todas as suas experiências podem aproveitar. A API serve como um idioma comum entre os serviços, vinculando-os no nível de conteúdo por meio de uma entrega de conteúdo padronizada, mas permitindo a flexibilidade para implementar suas próprias soluções.

Headless é um exemplo de dissociação do conteúdo de sua apresentação. Ou, em um sentido mais genérico, dissociar o front-end do back-end da sua pilha de serviço. Em uma configuração sem cabeçalho, o sistema de apresentação (o cabeçalho) é dissociado do gerenciamento de conteúdo (a cauda). Os dois só interagem por meio de chamadas de API.

Essa dissociação significa que cada serviço de consumo (front-end) pode criar sua experiência com base no mesmo conteúdo fornecido sobre as APIs, garantindo a reutilização e a consistência do conteúdo. Os serviços de consumo podem, então, implementar seus próprios sistemas de apresentação, permitindo que a pilha de gerenciamento de conteúdo (o back-end) seja facilmente dimensionada horizontalmente.

## Subvenções Tecnológicas {#technology}

Uma abordagem sem interface permite construir uma pilha de tecnologia que se adapte fácil e rapidamente às futuras demandas de experiência digital.

As APIs para CMSs no passado normalmente eram baseadas em REST. A transferência de estado de representação (REST) fornece recursos como texto sem estado. Isso permite que os recursos sejam lidos e modificados com um conjunto predefinido de operações. O REST permitiu uma grande interoperabilidade entre serviços na Web, garantindo a representação sem estado do conteúdo.

Ainda há necessidade de REST APIs robustas. No entanto, as solicitações REST podem ser grandes e detalhadas. Se você tiver vários consumidores fazendo chamadas REST para todos os seus canais, esses compostos de verbosidade e o desempenho podem ser afetados.

A entrega de conteúdo headless geralmente usa APIs GraphQL. GraphQL permite uma transferência sem estado semelhante, mas permite consultas mais direcionadas, reduzindo o número total de consultas necessárias e melhorando o desempenho. É comum ver soluções que usam uma combinação de REST e GraphQL, escolhendo essencialmente a melhor ferramenta para o trabalho em mãos.

Independentemente da API escolhida, ao definir um sistema sem periféricos com base em APIs comuns, você pode aproveitar o navegador mais recente e outras tecnologias da Web, como aplicativos da Web progressivos (PWA). As APIs criam uma interface padrão que é facilmente extensível e adaptável.

Normalmente, o conteúdo é renderizado no lado do cliente. Isso normalmente significa que alguém chama seu conteúdo em um dispositivo móvel, seu CMS entrega o conteúdo e, em seguida, o dispositivo móvel (o cliente) é responsável pela renderização do conteúdo que você disponibilizou. Se o dispositivo estiver antigo ou lento, sua experiência digital também estará lenta.

A dissociação do conteúdo da apresentação significa que pode haver mais controle sobre essas preocupações de desempenho do lado do cliente. A renderização do lado do servidor (SSR) transfere a responsabilidade de renderizar o conteúdo do navegador do cliente para o servidor. Isso permite que você, como provedor do conteúdo, ofereça um nível de desempenho garantido para o seu público-alvo, se isso for necessário.

## Desafios organizacionais {#organization}

O headless abre um mundo de flexibilidade para fornecer suas experiências digitais. Mas esta flexibilidade pode também apresentar o seu próprio desafio.

Ter muitos canais diferentes pode significar que cada um tem seus próprios sistemas de apresentação. Mesmo que todos consumam o mesmo conteúdo por meio das mesmas APIs, a experiência pode ser diferente por causa das diferentes apresentações. Deve ser dada atenção e preocupação a assegurar a coerência da experiência do cliente.

Ao implementar sistemas de design cuidadosos, compartilhar bibliotecas de padrões e aproveitar componentes de design reutilizáveis, bem como estruturas estabelecidas e abertas do lado do cliente, experiências consistentes podem ser asseguradas, mas isso deve ser planejado.

## O futuro é imprudente e o futuro é agora {#future}

As experiências digitais continuarão a definir como as marcas interagem com os clientes. O que é empolgante sobre o design sem interface é a flexibilidade que ele nos dá para responder às expectativas do cliente em evolução.

É impossível prever o futuro, mas sem cabeça dá-nos a agilidade de reagir ao que o futuro traz.

## AEM e sem cabeça {#aem-and-headless}

À medida que você prossegue com essa jornada do desenvolvedor, aprenderá como o AEM suporta a entrega sem periféricos junto com seus recursos de entrega em pilha completa.

Como líder do setor em gerenciamento de experiência digital, o Adobe percebe que a solução ideal para os desafios do mundo real que os criadores de experiências enfrentam raramente é uma escolha binária. É por isso que AEM suporta não apenas ambos os modelos, mas também permite exclusivamente a combinação híbrida perfeita dos dois, misturando as vantagens da pilha completa e sem interface, para ajudá-lo a atender melhor os consumidores de seu conteúdo, onde quer que estejam.

Essa jornada se concentra no modelo sem periféricos de entrega de conteúdo. No entanto, uma vez que você tenha esse conhecimento fundamental, poderá explorar ainda mais o potencial de ambos os modelos.

## O que vem a seguir {#what-is-next}

Obrigado por começar a sua jornada AEM sem cabeça! Agora que você leu este documento, deve:

* Entenda os conceitos básicos e a terminologia da entrega de conteúdo sem periféricos.
* Entenda por que e quando o headless é necessário.
* Saiba em alto nível como os conceitos sem interface são usados e como eles se relacionam.

Aproveite esse conhecimento e prossiga com sua jornada sem periféricos AEM ao próximo revisar o documento [Introdução ao AEM Headless](getting-started.md) onde você aprenderá a configurar as ferramentas necessárias e a começar a pensar em como o AEM aborda a entrega de conteúdo sem periféricos e seus pré-requisitos.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de desenvolvimento sem periféricos revisando o documento [Introdução ao AEM Headless](getting-started.md), a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada sem periféricos.

<!-- HM-Links
* [An Introduction to the Architecture of Adobe Experience Manager as a Cloud Service](/help/overview/architecture.md) - Understand AEM as a Cloud Service's structure
-->

* [AEM Tutorials sem cabeça](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Use esses tutoriais práticos para explorar como usar as várias opções para fornecer conteúdo a endpoints sem interface com o AEM e escolha o que é certo para você.
