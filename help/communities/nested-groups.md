---
title: Criação de grupos aninhados
description: Saiba como criar grupos aninhados para um site do Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor do AEM, na navegação global:

* Selecione **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.
* Selecione **[!UICONTROL engajar pasta]** para abri-la.
* Selecione o cartão para o site em inglês **[!UICONTROL Tutorial de introdução]**.

   * Selecione a imagem do cartão.
   * *não* selecione um ícone.

O resultado é alcançar o [console Grupos](/help/communities/groups.md):

![criar-grupo](assets/create-group.png)

A função de grupos é exibida como uma pasta na qual as instâncias dos grupos são criadas. Para abri-lo, selecione a pasta Grupos. O grupo criado no Publish está visível.

![criar-novo-grupo](assets/create-new-group.png)

## Criar grupo principal de artes {#create-main-arts-group}

Este grupo pode ser criado porque a estrutura do site para participação inclui a função de um grupo. A configuração da função no `Reference Template` do site é padronizada para permitir a seleção de qualquer modelo de grupo habilitado. Assim, o modelo escolhido para este novo grupo é o `Reference Group`.

Esses consoles são semelhantes ao console Sites de comunidades.

* Selecionar **[!UICONTROL Criar Grupo]**

* **Modelo do grupo da comunidade**:

   * **[!UICONTROL Título do Grupo da Comunidade]**: Artes
   * **[!UICONTROL Descrição do grupo da comunidade]**: um grupo pai para vários grupos de artes
   * **[!UICONTROL Raiz do grupo da comunidade]**: *deixar como padrão*
   * **[!UICONTROL Idioma(s) adicional(is) disponível(is) do grupo da comunidade]**: use o menu suspenso para selecionar os idiomas disponíveis do grupo da comunidade. O menu exibe todos os idiomas nos quais o site pai da comunidade é criado. Os usuários podem selecionar entre esses idiomas para criar grupos em vários locais nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites de comunidade.
   * **[!UICONTROL Nome do Grupo da Comunidade]**: artes
   * **[!UICONTROL Modelo]**: menu suspenso para selecionar `Reference Group`
   * Selecionar **[!UICONTROL Próximo]**

![Grupos de comunidades aninhados](assets/parent-to-nestedgroup.png)

Prossiga pelos outros painéis com estas configurações:

* **[!UICONTROL Design]**

   * Alterar o design ou permitir o design do site pai padrão.
   * Selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Configurações]**

   * **[!UICONTROL Moderação]**

      * Deixar em branco (herdar do site pai).

   * **[!UICONTROL Associação]**

      * Usar o padrão `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`

      * **[!UICONTROL Selecione Próximo]**.

* Selecione **[!UICONTROL Criar]**.

### Aninhamento de grupos no grupo de artes {#nesting-groups-within-arts-group}

A pasta `groups` agora contém dois grupos (atualize a página).

![Aninhamento de grupos](assets/create-community-group.png)

#### Grupo Publish {#publish-group}

Antes de criar grupos aninhados no grupo `arts`, passe o mouse sobre o cartão `arts` e selecione o ícone de publicação para publicá-lo.

![publicar-site](assets/publish-site.png)

Aguarde a confirmação de que o grupo foi publicado.

![grupo-publicado](assets/group-published.png)

O grupo `arts` também deve conter uma pasta `groups`, mas que esteja vazia e na qual novos grupos possam ser criados. Navegue até a pasta do grupo de artes e crie três grupos aninhados, cada um com uma configuração de associação diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nome: `visual`
   * Modelo: `Reference Group`
   * Associação: selecione `Optional Membership`, um grupo público, aberto a todos os membros.

1. **[!UICONTROL Auditório]**

   * Título: `Auditory Arts`
   * Nome: `auditory`
   * Modelo: `Reference Group`
   * Associação: selecione `Required Membership`, um grupo aberto, disponível para membros participarem.

1. **[!UICONTROL Histórico]**

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: selecione `Restricted Membership`, um grupo secreto, visível apenas para membros convidados. Como exemplo, convide [usuário de demonstração](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Atualize a página para que você possa ver todos os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados do console Sites de comunidades:

* Selecione a **[!UICONTROL pasta de participação]**
* Selecione o **[!UICONTROL cartão Tutorial de introdução]**
* Selecione a pasta **[!UICONTROL Grupos]**
* Selecione o **[!UICONTROL cartão de artes]**
* Selecione a pasta **[!UICONTROL Grupos]**

![criar-novo-grupo2](assets/create-new-group2.png)

## Publicar grupos {#publishing-groups}

![publicar-site](assets/publish-site.png)

Depois de publicar o site principal da comunidade:

* Publish cada grupo individualmente:

   * Aguardando confirmação de que o grupo foi publicado.

* Publish o grupo pai antes de publicar quaisquer grupos aninhados em:

   * Todos os grupos devem ser publicados de cima para baixo.

![grupo-publicado](assets/group-published.png)

## Experiência no Publish {#experience-on-publish}

É possível experimentar os diferentes grupos quando conectado, por exemplo, com os [usuários de demonstração](/help/communities/tutorials.md#demo-users) usados para:

* Membro do grupo Art/History: `emily.andrews@mailinator.com/password`
   * O grupo restrito (secreto), artes/história, está visível:
   * É possível ver grupos opcionais (públicos).
   * Capaz de ingressar em grupos restritos (abertos).

* Gerenciador de grupo: `aaron.mcdonald@mailinator.com/password`

   * É possível ver grupos opcionais (públicos).
   * Capaz de ingressar em grupos restritos (abertos).
   * Não é possível ver os grupos restritos (secretos).

Acesse os [consoles Membros e Grupos](/help/communities/members.md) das Comunidades no autor para adicionar outros usuários a vários grupos de membros que correspondam aos grupos da comunidade.
