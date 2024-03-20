---
title: Utilização de Edge Delivery Services
description: Utilização de Edge Delivery Services
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
solution: Experience Manager, Experience Manager Assets
feature: Edge Delivery Services
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---

# Utilização de Edge Delivery Services {#usingedge}

Com o Edge Delivery, você pode criar ambientes de desenvolvimento rápidos em que os autores podem atualizar e publicar conteúdo rapidamente, e novos sites podem ser iniciados rapidamente. Para isso, você pode trabalhar com várias fontes de conteúdo no mesmo site e a publicação será contínua e simplificada, independentemente da fonte escolhida. Dessa forma, leva apenas alguns segundos para ir da edição ao conteúdo ativo na Internet.

## Criação   {#authoring-edge}

Com o Edge Delivery, a criação é fácil, rápida e flexível. Você pode seguir dois caminhos diferentes para a criação no contexto de Edge Delivery Services:

* Criação baseada em documentos (como o Microsoft Word ou o Google Docs) - [Consulte este link para obter mais detalhes](https://www.hlx.live/docs/authoring).
* Editor de páginas/Editor universal - Entre em contato com o representante de vendas da Adobe.

Se houver criação baseada em documentos, você poderá trabalhar com várias fontes, como o Microsoft Word e a Documentação do Google. Os documentos dessas fontes se tornam páginas do site. Cabeçalhos, listas, imagens, elementos de fonte, vídeos podem ser transferidos da fonte inicial para o seu site. Você pode adicionar metadados para fins de SEO ou usar blocos para trabalhar com conteúdo estruturado e adicionar funcionalidades.

## Publicação {#publishing-edge}

Com o Edge Delivery, a publicação de conteúdo é contínua, independentemente da sua fonte de conteúdo. O processo é o seguinte: você usa o [extensão sidekick](#using-sidekick) para acionar o mecanismo de publicação, e seu conteúdo estará disponível ao vivo no site em alguns segundos.

## Edge Delivery Services e GitHub {#github-edge}

O Edge Delivery usa o GitHub para que os clientes possam gerenciar e implantar o código diretamente do repositório do GitHub. Por exemplo, você pode escrever conteúdo no Google Docs ou no Microsoft Word e desenvolver a funcionalidade do site usando CSS e JavaScript no GitHub. Os sites são criados automaticamente para cada uma de suas ramificações, da pré-visualização de conteúdo à produção. Todos os recursos que você coloca no repositório GitHub estão disponíveis no seu site sem um processo de criação.

## Uso do Sidekick {#using-sidekick}

O sidekick do AEM fornece uma barra de ferramentas com opções sensíveis ao contexto para que você possa editar, visualizar e publicar conteúdo facilmente. Depois [instalando](https://www.hlx.live/docs/sidekick-extension) A extensão AEM sidekick pode ser usada em ambientes de projeto ou ao editar conteúdo (por exemplo, em documentos do Google). Dependendo do ambiente, ele tem várias ações disponíveis, como Visualizar, Recarregar, Editar e Publicar. Você também pode alternar ambientes ao usar o sidekick que vai de pré-visualização a produção e vice-versa.

**Para publicar**, abra o sidekick em uma página de visualização e use a ação Publicar. Depois de clicar em Publicar, a versão de visualização atual da página estará disponível em ambientes ativos e de produção.

## Integrar o AEM Assets com a criação baseada em documentos {#integrate-assets-edge}

O Edge Delivery permite usar imagens disponíveis em repositórios do AEM Assets ao criar documentos no Microsoft Word ou Google Docs.

As opções para usar imagens nos documentos estão disponíveis somente após [configuração do plug-in do AEM Assets sidekick](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

O plug-in sidekick para AEM Assets oferece acesso a:

* AEM Assets as a Cloud Service

* AEM Assets Essentials

Depois de configurar o plug-in do AEM Assets sidekick, você pode [comece a usar imagens nos documentos do Google Docs ou do Microsoft Word](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Leitura adicional {#further-reading}

Para obter mais detalhes, consulte as seguintes páginas:

* Para obter detalhes sobre como começar a usar o Edge Delivery, consulte o [Build](https://www.hlx.live/docs/#build) seção da documentação de entrega do Edge.
* Para entender como criar e publicar conteúdo usando o Edge Delivery, consulte [Publicar seção](https://www.hlx.live/docs/authoring).
* Para entender como usar a extensão sidekick, consulte [Usar o sidekick](https://www.hlx.live/docs/sidekick) página.
* Para criação no AEM, consulte [Página Conceitos de criação](/help/sites-authoring/author.md))
