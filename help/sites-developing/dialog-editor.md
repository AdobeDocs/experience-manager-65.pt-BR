---
title: Editor de diálogo
seo-title: Editor de diálogo
description: O editor de diálogo fornece uma interface gráfica para fácil criação e edição de caixas de diálogo e andaimes
seo-description: O editor de diálogo fornece uma interface gráfica para fácil criação e edição de caixas de diálogo e andaimes
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Editor de diálogo{#dialog-editor}

O editor de diálogo fornece uma interface gráfica para fácil criação e edição de caixas de diálogo e andaimes.

Para ver como funciona, vá para CRXDE Lite, abra a árvore do explorador para `/libs/foundation/components/chart` e clique do duplo no nó `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

O nó de diálogo será aberto no **editor de diálogo**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Visão Geral da Interface do Usuário {#user-interface-overview}

A interface do editor de diálogo é composta de quatro painéis:

* A paleta ****, no canto superior esquerdo. Esse painel contém os widgets disponíveis para criar uma caixa de diálogo, como painéis de guia, campos de texto, listas de seleção e botões. É possível expandir as diferentes categorias dentro da paleta clicando na barra divisória desejada.
* O painel **structure**, no canto inferior esquerdo. Este painel mostra a estrutura hierárquica dos nós que compõem a definição da caixa de diálogo. Você pode ver a mesma estrutura expandindo o nó de diálogo no CRXDE Lite ou no CRX Content Explorer.
* O painel **renderizar**, no centro da janela. Este painel mostra como a definição da caixa de diálogo definida no painel de estrutura será renderizada como uma caixa de diálogo real.
* O painel **propriedades**. Este painel mostra as propriedades do nó atualmente realçado no painel de estrutura.

### Usando o Editor de Diálogo {#using-the-dialog-editor}

Para criar uma caixa de diálogo, o usuário arrasta e solta elementos da paleta para o painel de estrutura na posição dentro da hierarquia de definição da caixa de diálogo.

Depois que a estrutura desejada é concluída, o usuário clica em **Salvar**, na parte superior do painel de renderização.

>[!CAUTION]
>
>Observe que o editor de diálogo se destina à criação de diálogos relativamente simples e pode não ser capaz de editar definições de diálogo mais complexas. Nos casos em que o editor de diálogo não permite a edição de uma estrutura de diálogo, a definição da caixa de diálogo deve ser criada e/ou editada manualmente, editando diretamente a estrutura do nó usando, por exemplo, o CRXDE Lite ou o CRX Content Explorer.

### Criando uma Nova Caixa de Diálogo {#creating-a-new-dialog}

Para criar uma nova caixa de diálogo, é necessário selecionar o componente desejado, clique em **Criar...** e, em seguida, **Criar caixa de diálogo...**.

Digite os detalhes necessários e clique em **Salvar tudo** - agora você pode clicar com o duplo na caixa de diálogo para abri-la com o editor.

### Usando o Editor de Diálogo para Scaffolds {#using-the-dialog-editor-for-scaffolds}

Um suporte é uma página especial que contém um formulário que pode ser preenchido e enviado em uma etapa. Isso permite que você crie rapidamente uma página usando o conteúdo inserido.

O formulário que compõe um suporte é definido por uma definição de diálogo, como um diálogo normal, embora apareça na página de andaime em um formato diferente. Como as definições de diálogo são usadas para definir andaimes, os andaimes podem ser projetados usando o editor de diálogo. Observe que ao usar o editor de diálogo dessa maneira, o painel de renderização ainda exibirá a definição da caixa de diálogo na forma de uma caixa de diálogo e não como um suporte.

Consulte [Andaime](/help/sites-authoring/scaffolding.md) para obter mais informações sobre como usar o editor de diálogo para criar andaimes.
