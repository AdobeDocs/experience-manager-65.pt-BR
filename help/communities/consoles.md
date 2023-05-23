---
title: Consoles das comunidades
seo-title: Communities Consoles
description: Explicação dos Consoles da comunidade
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%

---

# Consoles das comunidades {#communities-consoles}

Os consoles AEM Communities, disponíveis no ambiente de criação no painel de navegação global, fornecem acesso a tarefas administrativas como:

* [Criação de um site da comunidade](sites-console.md)
* Adicionando [grupos](groups.md) aninhado no site
* Gerenciamento [modelos de site da comunidade](sites.md)
* Gerenciamento [membros da comunidade](members.md)
* [Moderando](moderate-ugc.md) conteúdo gerado pelo usuário (UGC)
* Criar [selos personalizados](badges.md)
* Configuração do [armazenamento padrão para UGC](srp-config.md)

Quando [Armazenamento UGC](working-with-srp.md) é configurado para ser um armazenamento comum compartilhado pelos ambientes do autor e de publicação, o [console de moderação](moderation.md), disponível nos ambientes autor e publicação, opera em uma instância solitária do UGC.

No ambiente do autor, após fazer logon com privilégios de administrador, a variável `Communities` Os consoles estão disponíveis nos consoles navegação e ferramentas.

>[!NOTE]
>
>No ambiente de publicação, uma variável [site da comunidade](sites-console.md) exibirá uma `Administration` item de menu quando o membro conectado tem privilégios apropriados.

## Painel de navegação global {#global-navigation-panel}

Selecione o `Adobe Experience Manager` no canto superior esquerdo para abrir o painel de navegação global e acessar dois ícones:

* [Console de navegação](#navigation-console)
* [Console Ferramentas](tools.md)

## Console de navegação {#navigation-console}

Para acessar os vários consoles Comunidades, na navegação global, selecione **navegação, Communities**.

![comunidades](assets/communities.png)

* [Sites](sites-console.md)

   O console Sites pode ser acessado no ambiente de criação para criar e gerenciar sites da comunidade e seus [grupos](groups.md).

* [Moderação](moderation.md)

   O console de Moderação serve para a moderação em massa de UGC e no ambiente do autor. Um console de moderação em massa semelhante está acessível no ambiente de publicação para membros da comunidade com a função de [moderador da comunidade](users.md#publishenvironmentusersandgroups) para um ou mais sites da comunidade.

* [Membros, Grupos](members.md)

   Os consoles Membros e grupos são para gerenciar membros da comunidade e grupos de membros que existem no ambiente de publicação do ambiente de autor.

* [Relatórios](reports.md)

   O console Relatórios é onde os relatórios sobre atribuições, visualizações de página e conteúdo publicado (UGC) podem ser gerados quando um site da comunidade tiver [Adobe Analytics habilitado](sites-console.md#analytics). O console só está disponível no ambiente do autor.

## Console de ferramentas {#tools-console}

Para acessar o [Ferramentas das comunidades](tools.md) (antigo console de administração), da navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]**
