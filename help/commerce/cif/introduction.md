---
title: Introdução e visão geral
description: Introdução e visão geral do conteúdo e comércio. A CIF (Experience Manager Integration Framework) é um padrão recomendado do Commerce Adobe para integrar e estender os serviços comerciais da Adobe Commerce e outras soluções comerciais de terceiros com o Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
exl-id: 52dad8f9-1812-42a3-8106-92b23f8517cd
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 3%

---

# Content and Commerce {#content-commerce}

Com o conteúdo e o comércio do Adobe Experience Manager, as marcas podem dimensionar e inovar mais rapidamente para diferenciar as experiências de comércio e capturar a aceleração dos gastos online. O AEM Content and Commerce combina as experiências imersivas, omnicanais e personalizadas no Experience Manager a qualquer quantidade de soluções comerciais para trazer experiências diferenciadas para todas as partes da jornada de compras, reduzindo o tempo de implantação e aumentando a conversão.

## Como o conteúdo e o comércio ajudam os clientes a terem sucesso

Com as expectativas cada vez maiores do cliente em experiências de comércio online, as marcas são pressionadas a oferecer experiências diferenciadas e mais conteúdo com mais rapidez. No entanto, a implementação de uma plataforma de gerenciamento de conteúdo geralmente requer investimentos em tempo e orçamento pesados no desenvolvimento de elementos fundamentais, como componentes personalizados e ferramentas de criação, e acumula custos em manutenção e upgrades. A Experience Manager Sites oferece conteúdo e comércio como um módulo complementar para o Experience Manager que fornece componentes principais de comércio prontos para uso, ferramentas de criação e uma loja de referência para acelerar o lançamento, permitir colaboração contínua entre equipes e gerar conversão.

As marcas podem integrar o Experience Manager com o Adobe Commerce, parte do Adobe Experience Cloud, bem como qualquer mecanismo de comércio preferido. Com o Experience Manager Content e Commerce, as marcas podem:

* Expanda e inove mais rapidamente
* Personalize experiências para impulsionar a conversão
* Criar uma vez e publicar em todos os locais
* Enriqueça e diferencie experiências para clientes
* Simplifique a criação com acesso a dados comerciais

## Introdução AEM Commerce Integration Framework (CIF) {#cif-intro}

Como esses projetos têm de lidar com a complexidade da integração de uma solução comercial. Uma solução comercial pode ser qualquer coisa, de uma solução comercial, como o Adobe Commerce, a um conjunto de serviços comerciais personalizados. A integração é altamente dependente dos casos de uso e do ecossistema. Ela costuma tocar em vários lugares e vem em vários sabores diferentes:

* Integração de um ecossistema complexo e dinâmico (por exemplo, catálogos de produtos)
* A empresa precisa gerenciar o conteúdo do produto com seu próprio ciclo de vida de forma eficiente e omnicanal
* Criação de jornadas de compras complexas e personalizadas para vários cabeçalhos
* Capacidade de adaptar e inovar rapidamente no back-end e no front-end
* Executando uma infraestrutura E2E escalável e estável, criada para desempenho máximo (Flash Sales, Black Friday, ...). Isso inclui pesquisa unificada e gerenciamento de cache.

Essa complexidade abre as portas para possíveis falhas, aumento de TCO, atrasos e redução da realização de valores. Essas razões levaram ao desenvolvimento da Commerce Integration Framework (CIF), que é um complemento do Experience Manager. A CIF amplia o Experience Manager com recursos de comércio e padroniza a integração com um mecanismo de comércio. O resultado é uma solução estável, escalável e à prova do futuro com menor TCO. Ele libera inovação técnica e comercial com ferramentas ágeis e recursos perfeitamente integrados para criar experiências comerciais atraentes.

![Elementos da CIF](./assets/CIF/CIF_Overview.png)

## A CIF oferece suporte aos clientes desde 2013 com sucesso

Com mais de 200 clientes, a CIF se estabeleceu como um ingrediente bem-sucedido para um projeto de conteúdo e comércio bem-sucedido. Isso oferece valor para TI e negócios hoje e no futuro. Projetos de clientes recentes descrevem a CIF como um &quot;grande acelerador e uma economia de tempo enorme com muito valor&quot;.

## Vantagens da CIF {#cif-benefits}

A CIF fornece componentes essenciais para o comércio prontos para uso que reduzem a necessidade de código personalizado, acelerando o tempo de comercialização de marcas. Todos os componentes principais são integrados imediatamente com a camada de dados do lado do cliente do Adobe para hidratar os perfis do cliente, como o perfil unificado. Esse perfil captura em detalhes o comportamento de um visitante, que pode ser usado para prever e personalizar a jornada do cliente em tempo real.

O complemento CIF traz o contexto do produto para o Experience Manager e fornece ferramentas de criação, como um console de produto e seletores de produto/categoria que capacitam o profissional de marketing a criar e fornecer experiências que podem ser compradas no Experience Manager sem depender do desenvolvedor. As vantagens incluem:

### Experiências

Ferramentas eficientes da CIF no AEM permitem que os criadores de conteúdo criem rapidamente experiências de comércio avançadas e personalizadas em uma maneira escalável e agnóstica de entrega para capitalizar as oportunidades de negócios.

![Elementos da CIF](./assets/CIF/CIF_Product_Experience_Management.png)

### Valor de tempo (TTV)

Acelera o desenvolvimento de projetos com [Componentes principais do AEM](https://www.aemcomponents.dev/), [Loja de referência Venia AEM](https://github.com/adobe/aem-cif-guides-venia), [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)e padrões de integração para PWA (conteúdo e comércio sem cabeçalho).

A CIF é criada para inovação contínua com um complemento sempre atualizado, permitindo que o cliente acesse recursos novos e aprimorados.

### Integrações

Conecte seu ecossistema (por exemplo, solução comercial) com o Experience Cloud usando  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), um PaaS sem servidor baseado em microsserviços e [Implementação de referência da CIF](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Padrões comprovados e práticas recomendadas

A CIF oferece suporte a clientes com padrões de integração padronizados com base nas práticas recomendadas. Isso ajuda os clientes a terem sucesso hoje e é flexível para crescer com o cliente e se adaptar a requisitos futuros:

* Elimina desafios típicos em integrações de catálogos de produtos que podem ocorrer. Exemplos:
   * Problemas de desempenho com maior volume ou complexidade de catálogo
   * Sem acesso aos dados preparados
   * Necessidade de dados e experiências do produto em tempo real
* Uma maturidade digital crescente resulta na necessidade de gerenciamento de experiência. A CIF é fornecida com recursos de gerenciamento da experiência do produto que podem ser incorporados de forma incremental, sem esforço adicional da TI.
* Pronto para omnicanal: A CIF é compatível com diversas tecnologias de pontos de contato (lado do servidor, híbridas, lado do cliente) com padrões, aceleradores e componentes principais.
