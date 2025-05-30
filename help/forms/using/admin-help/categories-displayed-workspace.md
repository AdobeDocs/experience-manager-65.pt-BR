---
title: Gerenciamento das categorias exibidas no Workspace
description: No Workspace, os processos que um usuário pode iniciar são exibidos em categorias no painel de navegação esquerdo. Saiba como gerenciar essas categorias exibidas no Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Gerenciamento das categorias exibidas no Workspace {#managing-the-categories-displayed-in-workspace}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

No Workspace, os processos que um usuário pode iniciar são exibidos em categorias no painel de navegação esquerdo. Você pode configurar as categorias no console de administração ou os designers de processo podem configurá-las no Workbench. Quando os projetistas de processos criam processos, eles os atribuem a categorias.

Ao especificar nomes de categoria, crie-os para que eles apareçam corretamente no painel de navegação do Workspace. Por padrão, o painel de navegação esquerdo tem uma largura fixa de 210 pixels, que é de aproximadamente 24 caracteres. Se o nome da categoria especificado for muito longo para caber dentro da largura fixa do painel de navegação esquerdo, ele será truncado. O nome completo aparece somente quando o ponteiro do mouse está pausado sobre ele. Tente evitar nomes de categoria que serão truncados. Os exemplos a seguir ilustram nomes de categoria que se encaixam e aqueles que estão truncados:

**Nome da categoria que se encaixa:** Presença e Saída

**Nome da categoria truncado:** Presença e Saída (Estados Unidos)

No Workspace, os processos em uma categoria normalmente são exibidos como cartões na página Iniciar processo. Em geral, seis cartões podem ser exibidos na tela para uma categoria antes que o usuário precise rolar a tela para visualizar os cartões restantes. Como a rolagem dificulta a localização de um processo, limite cada categoria a seis processos ou, dependendo da sua resolução, limite o número de processos que podem ser exibidos na tela sem a necessidade de rolagem.

Se você estiver usando o MySQL como banco de dados do AEM Forms, o Console de Administração não poderá diferenciar entre dois nomes de categoria que diferem somente no uso de caracteres estendidos. Por exemplo, se você criar uma categoria chamada abcde e uma chamada âbcdè, elas serão consideradas iguais.

## Adicionar uma categoria {#add-a-category}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Clique em Adicionar. Se desejar adicionar uma subcategoria, selecione uma categoria e clique em Adicionar.
1. Na caixa Nome, digite um nome para a categoria e, na caixa Descrição, digite uma descrição da categoria.
1. Clique em Adicionar. A categoria é exibida na página Gerenciamento de categorias.

   ***observação &#x200B;**: você pode adicionar até cinco níveis de hierarquia ao criar categorias.*

## Editar uma categoria {#edit-a-category}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Selecione a categoria que deseja editar e clique em Editar. Como alternativa, clique duas vezes em uma categoria para editá-la.
1. Edite o nome da categoria na caixa Nome.

## Remover uma categoria {#remove-a-category}

Você pode remover apenas as categorias que não estão em uso.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de categorias.
1. Na página Gerenciamento de categorias, marque a caixa de seleção da categoria a ser removida e clique em Remover. A categoria não é mais exibida.
