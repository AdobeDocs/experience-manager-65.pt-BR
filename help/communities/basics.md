---
title: Noções básicas sobre componentes das comunidades
seo-title: Communities Components Basics
description: Adicionar recursos das Comunidades a sites AEM no modo de edição e configurar componentes
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---

# Noções básicas sobre componentes das comunidades {#communities-components-basics}

## Visão geral {#overview}

A seção de criação da documentação descreve a adição de recursos das Comunidades a sites AEM no modo de edição do autor e a descrição das configurações de componentes.

Componentes podem ser explorados usando uma instância AEM e o mecanismo de [Guia de componentes da comunidade](components-guide.md).

## Acesso aos componentes das comunidades {#accessing-communities-components}

Ao criar conteúdo da página, se o modelo subjacente permitir alterações no design da página, será possível habilitar componentes que ainda não estejam disponíveis no navegador de componentes como parte do design do site.

Os componentes das Comunidades disponíveis estão listados [aqui](author-communities.md#available-communities-components).

>[!NOTE]
>
>Para obter informações gerais sobre criação, consulte [guia rápido para a criação de páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com o AEM, consulte a documentação em [manuseio básico](../../help/sites-authoring/basic-handling.md).

### Entrando no modo de design {#entering-design-mode}

Se um **Communities** componente não é encontrado no navegador de componentes (sidekick), será necessário inserir `Design Mode` para adicionar outros componentes do Communities. [Bibliotecas obrigatórias do lado do cliente](#required-clientlibs) (clientlibs) também pode precisar ser adicionado.

Para obter detalhes, consulte [Configuração de componentes no modo de design](../../help/sites-authoring/default-components-designmode.md).

A seguir estão imagens de como selecionar alguns componentes de Comunidades e visualizá-los no navegador de componentes:

![design de componente](assets/component-design.png)

Os componentes selecionados agora estão disponíveis no navegador de componentes:

![component-design1](assets/component-design1.png)

## Clientlibs Necessárias {#required-clientlibs}

[Bibliotecas do lado do cliente](../../help/sites-developing/clientlibs.md) (clientlibs) são necessários para o funcionamento adequado (JavaScript) e estilo (CSS) de um componente.

Ao adicionar um componente das Comunidades a uma página, se o resultado for um erro ou uma aparência inesperada, a primeira coisa a tentar é adicionar as clientlibs necessárias para o componente das Comunidades. Para obter detalhes, consulte [Clientlibs para componentes das comunidades](clientlibs.md).

### Exemplo: revisões inicialmente colocadas sem bibliotecas de clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### .. E com bibliotecas de clientes {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Marcação com tags {#tagging}

Muitos recursos do Communities podem ser configurados para permitir que os membros marquem o conteúdo inserido (publicado) no ambiente de publicação.

Se a marcação for permitida, a configuração do site da comunidade poderá ser definida para limitar os namespaces apresentados aos membros no ambiente de publicação. Consulte a [Console de sites da comunidade](sites-console.md#tagging).

Recursos que permitem marcação: [blog](blog-feature.md), [calendário](calendar.md), [biblioteca de arquivos](file-library.md), [fórum](forum.md)

Recursos que usam tags: [pesquisa](search.md), [nuvem de tags sociais](tagcloud.md)

Para obter informações sobre criação:

* [Uso de tags](../../help/sites-authoring/tags.md)

Para obter informações administrativas:

* Criação de namespaces de tag (taxonomia): [Administração de tags](../../help/sites-administering/tags.md)
* Configuração do site da comunidade: consulte [MARCAÇÃO](sites-console.md#tagging)
* [Marcação do conteúdo gerado pelo usuário](../../help/sites-authoring/tags.md)

Para obter informações do desenvolvedor:

* [Estrutura de marcação do AEM](../../help/sites-developing/framework.md)
* [Fundamentos de marcação](tag.md)
