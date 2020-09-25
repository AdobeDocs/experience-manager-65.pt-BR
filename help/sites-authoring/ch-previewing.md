---
title: Visualização de páginas usando dados do ContextHub
seo-title: Visualização de páginas usando dados do ContextHub
description: A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub, permite alterar esses dados e é útil para visualizar o conteúdo
seo-description: A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub, permite alterar esses dados e é útil para visualizar o conteúdo
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 93%

---


# Visualização de páginas usando dados do ContextHub{#previewing-pages-using-contexthub-data}

A barra de ferramentas do [ContextHub](/help/sites-developing/contexthub.md) exibe os dados dos armazenamentos do ContextHub e permite alterar esses dados. A barra de ferramentas ContextHub é útil para visualizar o conteúdo que é determinado pelos dados em um armazenamento ContextHub.

A barra de ferramentas consiste em uma série de modos de interface que contêm um ou mais módulos de interface.

* Os modos de interface do usuário são ícones que aparecem no lado esquerdo da barra de ferramentas. Quando você clica ou toca em um ícone, a barra de ferramentas revela os módulos de interface do usuário que ele contém.
* Módulos de interface do usuário exibem dados de um ou mais armazenamentos do ContextHub. Alguns módulos de interface do usuário também permitem manipular os dados do armazenamento.

O ContextHub instala vários modos e módulos de interface do usuário. Seu administrador pode ter [configurado o ContextHub](/help/sites-developing/ch-configuring.md) para exibir opções diferentes.

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## Revelar a barra de ferramentas do ContextHub {#revealing-the-contexthub-toolbar}

A barra de ferramentas do ContextHub está disponível no modo de Visualização. A barra de ferramentas está disponível somente nas instâncias do autor e somente se o administrador a tiver ativado.

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. Com a página aberta para edição, clique ou toque em Visualizar na barra de ferramentas.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Para exibir a barra de ferramentas, clique ou toque no ícone ContextHub.

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## Recursos do módulo da interface {#ui-module-features}

Cada módulo de interface fornece um conjunto diferente de recursos, mas os tipos de recursos a seguir são os mais comuns. Como os módulos de interface podem ser estendidos, o desenvolvedor pode implementar outros recursos, conforme necessário.

### Conteúdo da barra de ferramentas {#toolbar-content}

Os módulos de interface podem exibir dados de um ou mais armazenamentos do ContextHub na barra de ferramentas. Os módulos de interface usam um ícone e um título para se identificar.

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### Conteúdo pop-up {#popup-content}

Alguns módulos de interface exibem uma sobreposição de pop-up quando clicados ou tocados. Normalmente, o pop-up contém mais informações do que o que aparece na barra de ferramentas.

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### Formulários pop-up {#popup-forms}

A sobreposição de pop-up de um módulo pode incluir elementos de formulário que permitem alterar os dados no armazenamento do ContextHub. Se o conteúdo da página for determinado pelos dados do armazenamento, será possível usar o formulário e observar as alterações no conteúdo da página.

### Modo de tela cheia {#fullscreen-mode}

As sobreposições de pop-up podem incluir um ícone que você clica ou toca para expandir o conteúdo do pop-up a toda a janela do navegador ou a tela.

![](do-not-localize/chlimage_1-18.png)

