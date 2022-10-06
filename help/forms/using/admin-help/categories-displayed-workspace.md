---
title: Gerenciamento das categorias exibidas no Workspace
seo-title: Managing the categories displayed in Workspace
description: No Workspace, os processos que um usuário pode iniciar são exibidos em categorias no painel de navegação esquerdo. Saiba como gerenciar essas categorias exibidas no Workspace.
seo-description: In Workspace, the processes that a user can start are displayed in categories in the left navigation pane. Learn how you can manage these categories displayed in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Gerenciamento das categorias exibidas no Workspace {#managing-the-categories-displayed-in-workspace}

No Workspace, os processos que um usuário pode iniciar são exibidos em categorias no painel de navegação esquerdo. Você pode configurar as categorias no console de administração ou os designers de processos podem configurá-las no Workbench. Quando os designers de processos criam processos, eles os atribuem a categorias.

Ao especificar nomes de categoria, crie-os para que eles apareçam corretamente no painel de navegação do Workspace. Por padrão, o painel de navegação esquerdo tem uma largura fixa de 210 pixels, que é de aproximadamente 24 caracteres. Se o nome da categoria especificado for muito longo para se ajustar à largura fixa do painel de navegação esquerdo, ele será truncado. O nome completo aparece somente quando o ponteiro do mouse está pausado sobre ele. Tente evitar nomes de categoria que serão truncados. Os exemplos a seguir ilustram os nomes de categoria que se encaixam e aqueles que estão truncados:

**Nome da categoria que se encaixa:** Participação e saída

**Nome da categoria truncado:** Participação e licença (Estados Unidos)

No Workspace, os processos em uma categoria normalmente são exibidos como cartões na página Iniciar processo . Em geral, seis cartões podem ser exibidos na tela de uma categoria antes que o usuário precise rolar para exibir os cartões restantes. Como a rolagem dificulta a localização de um processo, considere limitar cada categoria a seis processos ou, dependendo da resolução, limitar o número de processos que podem ser exibidos na tela sem a necessidade de rolagem.

Se você estiver usando o MySQL como o banco de dados de formulários AEM, o Console de Administração não poderá diferenciar dois nomes de categoria que diferem apenas no uso de caracteres estendidos. Por exemplo, se você criar uma categoria chamada abcde e uma categoria chamada âbcdè, elas serão consideradas iguais.

## Adicionar uma categoria {#add-a-category}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Clique em Adicionar. Se desejar adicionar uma subcategoria, selecione uma categoria e clique em Adicionar.
1. Na caixa Nome, digite um nome para a categoria e, na caixa Descrição, digite uma descrição da categoria.
1. Clique em Adicionar. A categoria é exibida na página Gerenciamento de categorias .

   ***observação **: É possível adicionar até cinco níveis de hierarquia ao criar categorias.*

## Editar uma categoria {#edit-a-category}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Selecione a categoria que deseja editar e clique em Editar. Como alternativa, você pode clicar duas vezes em uma categoria para editar.
1. Edite o nome da categoria na caixa Nome.

## Remover uma categoria {#remove-a-category}

Você pode remover apenas as categorias que não estão em uso.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Na página Gerenciamento de categorias , marque a caixa de seleção da categoria a ser removida e clique em Remover. A categoria não é mais exibida.
