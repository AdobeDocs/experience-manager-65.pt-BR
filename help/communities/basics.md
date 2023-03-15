---
title: Noções básicas sobre componentes do Communities
seo-title: Communities Components Basics
description: Adicionar recursos do Communities ao AEM sites no modo de edição e configurar componentes
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# Noções básicas sobre componentes do Communities {#communities-components-basics}

## Visão geral {#overview}

A seção de criação da documentação descreve como adicionar recursos do Communities aos sites AEM no modo de edição do autor, bem como descrever as configurações de componentes.

Os componentes podem ser explorados usando uma instância AEM e o [Guia de componentes da comunidade](components-guide.md).

## Acesso aos componentes das comunidades {#accessing-communities-components}

Ao criar o conteúdo da página, se o modelo subjacente permitir alterações no design da página, é possível habilitar componentes que ainda não estão disponíveis no navegador de componentes como parte do design do site.

Os componentes disponíveis das Comunidades são listados [here](author-communities.md#available-communities-components).

>[!NOTE]
>
>Para obter informações gerais sobre criação, visualize o [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com AEM, visualize a documentação em [tratamento básico](../../help/sites-authoring/basic-handling.md).

### Entrando no modo de design {#entering-design-mode}

Se uma **Comunidades** não for encontrado no navegador de componentes (sidekick), será necessário inserir `Design Mode` para adicionar outros componentes do Communities. [Bibliotecas obrigatórias do lado do cliente](#required-clientlibs) (clientlibs) também pode precisar ser adicionada.

Para obter detalhes, consulte [Configuração de componentes no modo de design](../../help/sites-authoring/default-components-designmode.md).

A seguir estão imagens de selecionar alguns componentes do Communities e exibi-los no navegador de componentes:

![design de componentes](assets/component-design.png)

Os componentes selecionados agora estão disponíveis no navegador de componentes:

![component-design1](assets/component-design1.png)

## Clientlibs necessários {#required-clientlibs}

[Bibliotecas do lado do cliente](../../help/sites-developing/clientlibs.md) (clientlibs) são necessários para o funcionamento correto (JavaScript) e o estilo (CSS) de um componente.

Ao adicionar um componente Comunidades a uma página, se o resultado for um erro ou uma aparência inesperada, a primeira coisa a tentar é adicionar as clientlibs necessárias para o componente Comunidades. Para obter detalhes, consulte [Clientlibs para componentes do Communities](clientlibs.md).

### Exemplo: Análises inicialmente colocadas sem bibliotecas de clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... E com bibliotecas de clientes {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Marcação com tags {#tagging}

Muitos recursos das Comunidades podem ser configurados para permitir que os membros marquem o conteúdo inserido (publicado) no ambiente de publicação.

Se a marcação for permitida, a configuração do site da comunidade poderá ser definida para limitar os namespaces apresentados aos membros no ambiente de publicação. Consulte a [Console de sites da comunidade](sites-console.md#tagging).

Recursos que permitem marcação: [blog](blog-feature.md), [calendário](calendar.md), [biblioteca de arquivos](file-library.md), [fórum](forum.md)

Recursos que usam tags: [catálogo](catalog.md), [pesquisa](search.md), [nuvem de tags sociais](tagcloud.md)

Para obter informações de criação:

* [Uso de tags](../../help/sites-authoring/tags.md)

Para informações administrativas:

* Criação de namespaces de tags (taxonomia): [Administração de tags](../../help/sites-administering/tags.md)
* Configuração do site da comunidade: see [MARCAÇÃO](sites-console.md#tagging)
* [Marcação de conteúdo gerado pelo usuário](../../help/sites-authoring/tags.md)
* [Marcar recursos de ativação](tag-resources.md)

Para informações do desenvolvedor:

* [Estrutura de marcação do AEM](../../help/sites-developing/framework.md)
* [Princípios básicos de marcação](tag.md)
