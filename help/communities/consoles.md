---
title: Consoles de comunidades
seo-title: Communities Consoles
description: Explicação dos Consoles da Comunidade
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# Consoles de comunidades {#communities-consoles}

Os consoles AEM Communities, disponíveis no ambiente de criação no painel de navegação global, fornecem acesso a tarefas administrativas como:

* [Criação de um site da comunidade](sites-console.md)
* Adição de [grupos](groups.md) aninhado dentro do site
* Gerenciamento [modelos de site da comunidade](sites.md)
* Gerenciamento [membros da comunidade](members.md)
* [Moderação](moderate-ugc.md) conteúdo gerado pelo usuário (UGC)
* Criar [etiquetas personalizadas](badges.md)
* Configurar a [armazenamento padrão para UGC](srp-config.md)

When [Armazenamento UGC](working-with-srp.md) está configurada para ser um armazenamento comum compartilhado pelos ambientes de criação e publicação, a variável [console de moderação](moderation.md), disponível em ambientes do autor e de publicação, opera em uma instância solitária do UGC.

No ambiente de criação, depois de fazer logon com privilégios de administrador, a variável `Communities` os consoles estão disponíveis nos consoles navegação e ferramentas.

>[!NOTE]
>
>No ambiente de publicação, uma [site da comunidade](sites-console.md) exibirá uma `Administration` item de menu quando o membro conectado tiver privilégios adequados.

## Painel Navegação global {#global-navigation-panel}

Selecione o `Adobe Experience Manager` ícone no canto superior esquerdo para abrir o painel de navegação global e acessar dois ícones:

* [Console de navegação](#navigation-console)
* [Console Ferramentas](tools.md)

## Console de navegação {#navigation-console}

Para acessar os vários consoles Comunidades, na navegação global, selecione **navegação, comunidades**.

![comunidades](assets/communities.png)

* [Sites](sites-console.md)

   O console Sites é acessível no ambiente de criação com o objetivo de criar e gerenciar sites da comunidade e seus [grupos](groups.md).

* [Moderação](moderation.md)

   O console Moderação é para moderação em massa do UGC e no ambiente de criação. Um console de moderação em massa semelhante pode ser acessado no ambiente de publicação para membros da comunidade aos quais foi atribuída a função de [moderador da comunidade](users.md#publishenvironmentusersandgroups) para um ou mais sites da comunidade.

* [Membros, Grupos](members.md)

   Os consoles Membros e Grupos são para gerenciar membros da comunidade e grupos de membros que existem no ambiente de publicação a partir do ambiente de criação.

* [Relatórios](reports.md)

   O console Relatórios é onde os relatórios sobre atribuições, exibições de página e conteúdo publicado (UGC) podem ser gerados quando um site da comunidade [Adobe Analytics habilitado](sites-console.md#analytics). O console só está disponível no ambiente do autor.

* [Recursos](resources.md)

   O console Recursos é onde [gerentes de capacitação](enablement.md#communitymanagers) criar, gerenciar e atribuir recursos aos membros de um [site da comunidade de ativação](overview.md#enablement-community). O console só está disponível no ambiente do autor.

## Console Ferramentas {#tools-console}

Para acessar [Ferramentas do Communities](tools.md) (antigo console de administração), da navegação global: **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]**
