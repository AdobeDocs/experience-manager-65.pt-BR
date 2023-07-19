---
title: Editor de caixa de diálogo
seo-title: Dialog Editor
description: O editor de diálogo fornece uma interface gráfica para criar e editar facilmente caixas de diálogo e scaffolds
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Editor de caixa de diálogo{#dialog-editor}

O editor de diálogo fornece uma interface gráfica para criar e editar facilmente caixas de diálogo e scaffolds.

Para ver como funciona, acesse o CRXDE Lite, abra a árvore do explorador para `/libs/foundation/components/chart` e clique duas vezes no nó `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

O nó da caixa de diálogo será aberto no **editor de diálogo**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Visão geral da interface do usuário {#user-interface-overview}

A interface do editor de caixa de diálogo é composta de quatro painéis:

* A variável **paleta**, no canto superior esquerdo. Este painel mantém os elementos disponíveis para criar uma caixa de diálogo, como painéis de abas, campos de texto, listas de seleção e botões. É possível expandir as diferentes categorias na paleta clicando na barra divisória desejada.
* A variável **estrutura** no canto inferior esquerdo. Este painel mostra a estrutura hierárquica dos nós que compõem a definição da caixa de diálogo. Você pode ver a mesma estrutura expandindo o nó da caixa de diálogo no CRXDE Lite ou no CRX Content Explorer.
* A variável **renderizar** no centro da janela. Esse painel mostra como a definição da caixa de diálogo definida no painel de estrutura será renderizada como uma caixa de diálogo real.
* A variável **propriedades** painel. Esse painel mostra as propriedades do nó atualmente destacado no painel de estrutura.

### Usando o Editor de diálogo {#using-the-dialog-editor}

Para criar uma caixa de diálogo, o usuário arrasta e solta elementos da paleta para o painel de estrutura na posição dentro da hierarquia de definição da caixa de diálogo.

Quando a estrutura desejada for concluída, o usuário clica em **Salvar**, na parte superior do painel de renderização.

>[!CAUTION]
>
>Observe que o editor de caixa de diálogo é destinado à criação de caixas de diálogo relativamente simples e pode não ser capaz de editar definições de caixa de diálogo mais complexas. Nos casos em que o editor de diálogo não permite a edição de uma estrutura de diálogo, a definição da caixa de diálogo deve ser criada e/ou editada manualmente editando diretamente a estrutura do nó usando, por exemplo, o CRXDE Lite ou o CRX Content Explorer.

### Criando uma nova caixa de diálogo {#creating-a-new-dialog}

Para criar uma nova caixa de diálogo, é necessário selecionar o componente desejado, clique em **Criar...** e depois **Criar caixa de diálogo...**.

Insira os detalhes necessários e clique em **Salvar tudo** - agora é possível clicar duas vezes na caixa de diálogo para abri-la com o editor.

### Usando o Editor de diálogo para scaffolds {#using-the-dialog-editor-for-scaffolds}

Um scaffold é uma página especial que contém um formulário que pode ser preenchido e enviado em uma etapa. Isso permite criar rapidamente uma página usando o conteúdo inserido.

O formulário que compõe um scaffolding é definido por uma definição de caixa de diálogo, como uma caixa de diálogo normal, embora apareça na página de scaffolding em um formulário diferente. Como as definições de caixa de diálogo são usadas para definir scaffolds, os scaffolds podem ser criados usando o editor de caixa de diálogo. Observe que ao usar o editor de diálogo dessa maneira, o painel de renderização ainda exibirá a definição do diálogo no formato de uma caixa de diálogo, não como um scaffold.

Consulte [Andaime](/help/sites-authoring/scaffolding.md) para obter mais informações sobre como usar o editor de diálogo para criar scaffolds.
