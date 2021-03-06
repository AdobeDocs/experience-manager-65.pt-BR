---
title: Componentes básicos das comunidades
seo-title: Componentes básicos das comunidades
description: Adicionar recursos de Comunidades a sites AEM no modo de edição e configurar componentes
seo-description: Adicionar recursos de Comunidades a sites AEM no modo de edição e configurar componentes
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# Componentes básicos das comunidades {#communities-components-basics}

## Visão geral {#overview}

A seção de criação da documentação descreve como adicionar recursos de Comunidades a sites AEM no modo de edição do autor, bem como descrever configurações de componentes.

Os componentes podem ser explorados usando uma instância AEM e o guia interativo [Componentes da comunidade](components-guide.md).

## Acessar componentes das comunidades {#accessing-communities-components}

Ao criar o conteúdo da página, se o modelo subjacente permitir alterações no design da página, é possível ativar os componentes que ainda não estão disponíveis no navegador de componentes como parte do design do site.

Os componentes de Comunidades disponíveis estão listados [aqui](author-communities.md#available-communities-components).

>[!NOTE]
>
>Para obter informações gerais de criação, visualização o guia rápido [para criar páginas](../../help/sites-authoring/qg-page-authoring.md).
>
>Se não estiver familiarizado com o AEM, visualização a documentação em [manuseio básico](../../help/sites-authoring/basic-handling.md).

### Entrando no Modo de Design {#entering-design-mode}

Se um componente **Communities** não for encontrado no navegador de componentes (sidekick), será necessário digitar `Design Mode` para adicionar outros componentes do Communities. [As bibliotecas](#required-clientlibs)  obrigatórias do cliente (clientlibs) também podem precisar ser adicionadas.

Para obter detalhes, consulte [Configuração de componentes no Modo Design](../../help/sites-authoring/default-components-designmode.md).

Veja a seguir as imagens de seleção de alguns componentes das Comunidades e sua visualização no navegador de componentes:

![concepção de componentes](assets/component-design.png)

Os componentes selecionados agora estão disponíveis no navegador de componentes:

![componente-design1](assets/component-design1.png)

## Clientlibs necessários {#required-clientlibs}

[As bibliotecas](../../help/sites-developing/clientlibs.md)  do cliente (clientlibs) são necessárias para o funcionamento correto (JavaScript) e o estilo (CSS) de um componente.

Ao adicionar um componente Comunidades a uma página, se o resultado for um erro ou uma aparência inesperada, a primeira coisa a tentar é adicionar os clientlibs necessários para o componente Comunidades. Para obter detalhes, consulte [Clientlibs for Communities Components](clientlibs.md).

### Exemplo: Análises inicialmente colocadas sem bibliotecas de clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... E com bibliotecas de clientes {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Marcação com tags {#tagging}

Vários recursos das Comunidades podem ser configurados para permitir que os membros marquem o conteúdo inserido (publicado) no ambiente de publicação.

Se a marcação for permitida, a configuração do site da comunidade pode ser definida para limitar as namespaces apresentadas aos membros no ambiente de publicação. Consulte o [console Sites da comunidade](sites-console.md#tagging).

Recursos que permitem marcação: [blog](blog-feature.md), [calendário](calendar.md), [biblioteca de ficheiros](file-library.md), [fórum](forum.md)

Recursos que usam tags: [catálogo](catalog.md), [pesquisa](search.md), [nuvem de etiqueta social](tagcloud.md)

Para obter informações de criação:

* [Uso de tags](../../help/sites-authoring/tags.md)

Para informações administrativas:

* Criando namespaces de tags (taxonomia): [Administração de tags](../../help/sites-administering/tags.md)
* Configuração do site da comunidade: consulte [TAGGGING](sites-console.md#tagging)
* [Marcação de conteúdo gerado pelo usuário](../../help/sites-authoring/tags.md)
* [Marcação de recursos de ativação](tag-resources.md)

Para obter informações sobre desenvolvedores:

* [Estrutura de marcação AEM](../../help/sites-developing/framework.md)
* [Essenciais da marcação](tag.md)

