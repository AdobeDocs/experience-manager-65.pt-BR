---
title: Visualização de páginas usando dados do ContextHub
description: A barra de ferramentas do ContextHub exibe os dados dos armazenamentos do ContextHub, permite alterar esses dados e é útil para visualizar o conteúdo
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 24%

---

# Visualização de páginas usando dados do ContextHub{#previewing-pages-using-contexthub-data}

A barra de ferramentas [ContextHub](/help/sites-developing/contexthub.md) exibe os dados dos armazenamentos do ContextHub e permite alterar esses dados. A barra de ferramentas do ContextHub é útil para visualizar o conteúdo determinado pelos dados em um armazenamento do ContextHub.

A barra de ferramentas consiste em uma série de modos de interface que contêm um ou mais módulos de interface.

* Os modos da interface são ícones exibidos no lado esquerdo da barra de ferramentas. Ao clicar em um ícone, a barra de ferramentas revela os módulos de interface do usuário que ela contém.
* Os módulos de interface exibem dados de um ou mais armazenamentos do ContextHub. Alguns módulos de interface também permitem manipular dados de armazenamento.

O ContextHub instala vários modos de interface e módulos de interface do usuário. O administrador pode ter [configurado o ContextHub](/help/sites-developing/ch-configuring.md) para exibir outros.

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## Revelação da barra de ferramentas do ContextHub {#revealing-the-contexthub-toolbar}

A barra de ferramentas do ContextHub está disponível no modo Visualização. A barra de ferramentas está disponível somente nas instâncias do autor e somente se o administrador a tiver ativado.

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. Com a página aberta para edição, clique em Visualizar na barra de ferramentas.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Para exibir a barra de ferramentas, clique no ícone do ContextHub.

   ![Context Hub](do-not-localize/screen_shot_2018-03-23at093621.png)

## Recursos do módulo de UI {#ui-module-features}

Cada módulo de interface do usuário fornece um conjunto diferente de recursos, mas os seguintes tipos de recursos são comuns. Como os módulos de interface do usuário são extensíveis, o desenvolvedor pode implementar outros recursos conforme necessário.

### Conteúdo da barra de ferramentas {#toolbar-content}

Os módulos de interface podem exibir dados de um ou mais armazenamentos do ContextHub na barra de ferramentas. Os módulos de interface usam um ícone e um título para se identificarem.

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### Conteúdo pop-up {#popup-content}

Alguns módulos de interface exibem um pop-up sobreposto quando clicados ou tocados. Normalmente, o pop-up contém mais informações do que o que aparece na barra de ferramentas.

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### Forms pop-up {#popup-forms}

A sobreposição pop-up de um módulo pode incluir elementos de formulário que permitem alterar os dados no armazenamento do ContextHub. Se o conteúdo da página for determinado pelos dados de armazenamento, é possível usar o formulário e observar as alterações no conteúdo da página.

### Modo de tela inteira {#fullscreen-mode}

As sobreposições de pop-up podem incluir um ícone no qual você clica para expandir o conteúdo de pop-up para cobrir toda a janela ou tela do navegador.

![Tela inteira](do-not-localize/chlimage_1-18.png)
