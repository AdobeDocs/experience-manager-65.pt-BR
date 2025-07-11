---
title: Introdução e visão geral
description: Entenda como usar e administrar o AEM Content and Commerce com artigos úteis sobre integrações e como começar a usar a vitrine do AEM.
thumbnail: introducing-aem-commerce.jpg
exl-id: 52dad8f9-1812-42a3-8106-92b23f8517cd
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 88%

---


# Content and Commerce {#content-commerce}

Com o Adobe Experience Manager Content and Commerce, as marcas podem dimensionar e inovar mais rapidamente para diferenciar as experiências comerciais e explorar o crescimento das compras online. O AEM Content and Commerce combina as experiências imersivas, omnicanais e personalizadas no Experience Manager com qualquer quantidade de soluções comerciais para trazer experiências diferenciadas para todas as partes da jornada de compras, reduzindo o tempo de retorno e aumentando a conversão.

## Como o Content and Commerce ajuda os clientes a terem sucesso

Com as expectativas cada vez maiores dos clientes em experiências comerciais online, as marcas são pressionadas a oferecer experiências diferenciadas e mais conteúdo com mais rapidez. No entanto, a implementação de uma plataforma de gerenciamento de conteúdo geralmente requer investimentos em tempo e orçamento pesados no desenvolvimento de elementos fundamentais, como componentes personalizados e ferramentas de criação, e acumula custos em manutenção e atualizações. A Experience Manager Sites oferece o Content and Commerce como um módulo complementar para o Experience Manager, que fornece componentes principais de comércio prontos para uso, ferramentas de criação e uma loja de referência para acelerar a ativação, permitir a colaboração contínua entre equipes e impulsionar a conversão.

As marcas podem integrar o Experience Manager com o Adobe Commerce (que faz parte da Adobe Experience Cloud), ou qualquer mecanismo de comércio de sua preferência. Com o Experience Manager Content and Commerce, as marcas podem:

* Expandir e inovar mais rápido
* Personalizar experiências para impulsionar a conversão
* Criar só uma vez e publicar em todos os locais
* Enriquecer e diferenciar as experiências para clientes
* Simplificar a criação com acesso a dados comerciais

## Introdução à Estrutura de Integração (CIF) do AEM Commerce {#cif-intro}

Como esses projetos têm de lidar com a complexidade da integração de uma solução comercial. Uma solução comercial pode ser qualquer coisa, desde uma solução comercial, como o Adobe Commerce, até um conjunto de serviços comerciais personalizados. A integração é altamente dependente dos casos de uso e do ecossistema. Ela costuma tocar em vários lugares e vem em vários tipos diferentes:

* Integração de um ecossistema complexo e dinâmico (por exemplo, catálogos de produtos)
* As necessidades da empresa de gerenciar o conteúdo do produto com seu próprio ciclo de vida de forma eficiente e omnicanal
* Criação de jornadas de compras complexas e personalizadas para várias pessoas
* Capacidade de adaptar e inovar rapidamente no back-end e no front-end
* Execução de uma infraestrutura E2E escalável e estável, criada para desempenho máximo (Promoções relâmpagos, Black Friday...). Isso inclui o gerenciamento de cache e pesquisa unificados.

Essa complexidade abre as portas para possíveis falhas, aumento de TCO, atrasos e redução da realização de valores. Essas razões levaram ao desenvolvimento da Estrutura de Integração do Commerce (CIF), um complemento do Experience Manager. A CIF amplia o Experience Manager com recursos de comércio e padroniza a integração com um mecanismo de comércio. O resultado é uma solução estável, escalável e duradoura com baixo TCO. Ela libera inovações técnicas e comerciais com ferramentas ágeis e recursos perfeitamente integrados para criar experiências comerciais atraentes.

![Elementos da CIF](./assets/CIF/CIF_Overview.png)

## A CIF oferece suporte aos clientes desde 2013 com sucesso

Com mais de 200 clientes, a CIF se estabeleceu como um ingrediente eficaz para um projeto de Content and Commerce bem-sucedido. Ela oferece valor para a TI e negócios hoje e no futuro. Projetos recentes de clientes descrevem a CIF como &quot;um grande acelerador e uma enorme economia de tempo com muito valor&quot;.

## Vantagens da CIF {#cif-benefits}

A CIF fornece componentes principais para o comércio prontos para uso que reduzem a necessidade de código personalizado, acelerando a comercialização das marcas. Todos os componentes principais são integrados de fábrica com a camada de dados do lado do cliente da Adobe para hidratar os perfis de clientes, como o perfil unificado. Esse perfil captura em detalhes o comportamento de um visitante, que pode ser usado para prever e personalizar a jornada do cliente em tempo real.

O complemento CIF traz o contexto do produto para o Experience Manager e fornece ferramentas de criação, como um console de produtos e seletores de produtos/categorias que capacitam o profissional de marketing a criar e fornecer experiências que podem ser compradas no Experience Manager sem depender do desenvolvedor. As vantagens incluem:

### Experiências

Ferramentas eficientes da CIF no AEM permitem que os criadores de conteúdo criem rapidamente experiências comerciais amplas e personalizadas de maneira escalável e independente da entrega para capitalizar as oportunidades de negócios.

![Elementos da CIF](./assets/CIF/CIF_Product_Experience_Management.png)

### Tempo de retorno (TTV)

Acelera o desenvolvimento de projetos com [Componentes principais do AEM](https://www.aemcomponents.dev/), [vitrine de referência do AEM Venia](https://github.com/adobe/aem-cif-guides-venia), [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) e padrões de integração para PWAs (Conteúdo headless e Commerce).

A CIF foi criada para inovação contínua com um complemento sempre atualizado, permitindo que os clientes acessem recursos novos e aprimorados.

### Integrações

Conecte seu ecossistema (por exemplo, uma solução comercial) com a Experience Cloud usando o [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), um PaaS sem servidor baseado em microsserviços e [Implementação de referência da CIF](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Padrões comprovados e práticas recomendadas

A CIF oferece suporte a clientes com esquemas de integração padronizados com base nas práticas recomendadas. Isso ajuda os clientes a terem sucesso atualmente e é flexível para crescer com o cliente e se adaptar a requisitos futuros:

* Elimina desafios típicos em integrações de catálogos de produtos que possam ocorrer. Exemplos:
   * Problemas de desempenho com um volume grande do catálogo ou sua complexidade
   * Sem acesso aos dados preparados
   * Necessidade de dados e experiências do produto em tempo real
* Uma maturidade digital crescente resulta na necessidade de gerenciamento de experiência. A CIF é fornecida com recursos de gerenciamento da experiência do produto que podem ser incorporados de forma incremental, sem esforço adicional da TI.
* Pronto para omnicanal: a CIF é compatível com diversas tecnologias touchpoint (lado do servidor, híbridas, lado do cliente) com padrões, aceleradores e componentes principais.
