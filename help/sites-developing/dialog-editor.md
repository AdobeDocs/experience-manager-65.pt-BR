---
title: Editor de caixa de diálogo
seo-title: Dialog Editor
description: O editor de caixas de diálogo fornece uma interface gráfica para criar e editar facilmente caixas de diálogo e scaffoles
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Editor de caixa de diálogo{#dialog-editor}

O editor de caixas de diálogo fornece uma interface gráfica para criar e editar facilmente caixas de diálogo e scaffolds.

Para ver como funciona, vá para o CRXDE Lite, abra a árvore do explorador para `/libs/foundation/components/chart` e clique duas vezes no nó `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

O nó da caixa de diálogo será aberto na **editor de caixas de diálogo**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Visão geral da interface do usuário {#user-interface-overview}

A interface do editor de caixas de diálogo é composta por quatro painéis:

* O **paleta**, no canto superior esquerdo. Esse painel contém os widgets disponíveis para criar uma caixa de diálogo, como painéis de guias, campos de texto, listas de seleção e botões. É possível expandir as diferentes categorias dentro da paleta clicando na barra de divisores desejada.
* O **estrutura** no canto inferior esquerdo. Este painel mostra a estrutura hierárquica dos nós que compõem a definição da caixa de diálogo. Você pode ver a mesma estrutura expandindo o nó da caixa de diálogo no CRXDE Lite ou no CRX Content Explorer.
* O **renderizar** no centro da janela. Este painel mostra como a definição da caixa de diálogo definida no painel de estrutura será renderizada como uma caixa de diálogo real.
* O **propriedades** painel. Este painel mostra as propriedades do nó atualmente realçadas no painel de estrutura.

### Uso do Editor de caixa de diálogo {#using-the-dialog-editor}

Para criar uma caixa de diálogo, o usuário arrasta e solta elementos da paleta no painel de estrutura na posição dentro da hierarquia de definição da caixa de diálogo.

Depois que a estrutura desejada é concluída, o usuário clica em **Salvar** na parte superior do painel de renderização.

>[!CAUTION]
>
>Observe que o editor de caixas de diálogo se destina à criação de caixas de diálogo relativamente simples e pode não ser capaz de editar definições de caixas de diálogo mais complexas. Nos casos em que o editor de caixas de diálogo não permite a edição de uma estrutura de diálogo, a definição da caixa de diálogo deve ser criada e/ou editada manualmente ao editar diretamente a estrutura do nó usando, por exemplo, o CRXDE Lite ou o CRX Content Explorer.

### Criação de uma nova caixa de diálogo {#creating-a-new-dialog}

Para criar uma nova caixa de diálogo, você precisa selecionar o componente desejado, clique em **Criar...** e depois **Criar caixa de diálogo...**.

Insira os detalhes necessários e clique em **Salvar tudo** - agora é possível clicar duas vezes na caixa de diálogo para abri-la com o editor.

### Uso do Editor de caixa de diálogo para scaffolds {#using-the-dialog-editor-for-scaffolds}

Um scaffold é uma página especial contendo um formulário que pode ser preenchido e enviado em uma etapa. Isso permite criar uma página rapidamente usando o conteúdo inserido.

O formulário que compõe um scaffold é definido por uma definição de diálogo, como uma caixa de diálogo normal, embora ele apareça na página de scaffolding em um formulário diferente. Como as definições de diálogo são usadas para definir scaffolds, os scaffolds podem ser projetados usando o editor de caixas de diálogo. Observe que, ao usar o editor de caixa de diálogo dessa maneira, o painel de renderização ainda exibirá a definição da caixa de diálogo na forma de uma caixa de diálogo e não como um scaffold.

Consulte [Andaime](/help/sites-authoring/scaffolding.md) para obter mais informações sobre como usar o editor de caixas de diálogo para criar scaffolds.
