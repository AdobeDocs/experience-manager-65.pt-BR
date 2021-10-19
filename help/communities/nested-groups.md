---
title: Criação de grupos aninhados
seo-title: Authoring Nested Groups
description: Criar grupos aninhados
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

---

# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor do AEM, na navegação global:

* Selecionar **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.
* Selecionar **[!UICONTROL pasta de engajamento]** para abri-lo.
* Selecione o cartão para o **[!UICONTROL Tutorial de introdução]** Site em inglês.

   * Selecione a imagem do cartão.
   * Do *not* selecione um ícone.

O resultado é alcançar a variável [Console Grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

A função groups será exibida como uma pasta na qual instâncias de grupos são criadas. Selecione a pasta Grupos para abri-la. O grupo criado na publicação está visível.

![create-new-group](assets/create-new-group.png)

## Criar grupo principal de artes {#create-main-arts-group}

Esse grupo pode ser criado porque a estrutura do site para engajamento inclui uma função de grupos. A configuração da função no `Reference Template` O padrão é permitir a seleção de qualquer modelo de grupo habilitado. Assim, o modelo escolhido para esse novo grupo é o `Reference Group`.

Esses consoles são semelhantes ao console Sites das Comunidades .

* Selecionar **[!UICONTROL Criar grupo]**

* **Modelo de grupo da comunidade**:

   * **[!UICONTROL Título do grupo da comunidade]**: Artes
   * **[!UICONTROL Descrição do grupo da comunidade]**: Um grupo pai para vários grupos de artes
   * **[!UICONTROL Raiz do grupo da comunidade]**: *deixar como padrão*
   * **[!UICONTROL Idioma(s) adicional(is) disponível(is) do grupo comunitário]**: use o menu suspenso para selecionar os idiomas disponíveis do grupo da comunidade. O menu exibe todos os idiomas nos quais o site da comunidade pai é criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.
   * **[!UICONTROL Nome do grupo da comunidade]**: artes
   * **[!UICONTROL Modelo]**: menu suspenso a ser selecionado `Reference Group`
   * Selecione **[!UICONTROL Próximo]**

![Grupos de comunidades aninhadas](assets/parent-to-nestedgroup.png)

Continue nos outros painéis com estas configurações:

* **[!UICONTROL Design]**

   * Altere o design ou permita o design padrão do site pai.
   * Selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Configurações]**

   * **[!UICONTROL Moderação]**

      * Deixe em branco (herdar do site pai).
   * **[!UICONTROL Associação]**

      * Usar padrão `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Selecione Próximo]**.



* Selecione **[!UICONTROL Criar]**.

### Aninhamento de grupos no grupo Artes {#nesting-groups-within-arts-group}

O `groups` agora contém dois grupos (atualize a página).

![Aninhamento dos grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de criar grupos aninhados na `arts` , passe o mouse sobre `arts` e selecione o ícone publicar para publicá-lo.

![publicar site](assets/publish-site.png)

Aguarde a confirmação de que o grupo foi publicado.

![publicado em grupo](assets/group-published.png)

O `arts` grupo também deve conter um `groups` , mas uma que está vazia e na qual novos grupos podem ser criados. Navegue até a pasta do grupo artístico e crie 3 grupos aninhados, cada um com uma configuração de associação diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nome: `visual`
   * Modelo: `Reference Group`
   * Associação: select `Optional Membership`, um grupo público, aberto a todos os membros.

1. **[!UICONTROL Auditório]**

   * Título: `Auditory Arts`
   * Nome: `auditory`
   * Modelo: `Reference Group`
   * Associação: select `Required Membership`, um grupo aberto, disponível para os membros aderirem.

1. **[!UICONTROL História]**

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: select `Restricted Membership`, um grupo secreto, visível somente para membros convidados. Como exemplo, convide [usuário de demonstração](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Atualize a página para ver todos os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados no console Sites das Comunidades:

* Selecionar **[!UICONTROL pasta de engajamento]**
* Selecionar **[!UICONTROL Introdução ao cartão tutorial]**
* Selecionar **[!UICONTROL Grupos]** pasta
* Selecionar **[!UICONTROL cartão de artes]**
* Selecionar **[!UICONTROL Grupos]** pasta

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicação {#publishing-groups}

![publicar site](assets/publish-site.png)

Depois de publicar o site principal da comunidade:

* Publicar cada grupo individualmente:

   * Aguardando confirmação de que o grupo foi publicado.

* Publicar grupo pai antes de publicar qualquer grupo aninhado em:

   * Todos os grupos devem ser publicados de cima para baixo.

![publicado em grupo](assets/group-published.png)

## Experiência na publicação {#experience-on-publish}

É possível experimentar os diferentes grupos quando ele está conectado, por exemplo, com a variável [usuários de demonstração](/help/communities/tutorials.md#demo-users) utilizado para:

* Membro do grupo Arte/História: emily.andrews@mailinator.com/password
   * O grupo restrito (secreto), artes/história, é visível:
   * Pode ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).

* Gerente de grupo: aaron.mcdonald@mailinator.com/password

   * Pode ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).
   * Não é possível ver grupos restritos (secretos).

Acesse as Comunidades [Consoles Membros e grupos](/help/communities/members.md) em autor para adicionar outros usuários a vários grupos de membros que correspondem aos grupos da comunidade.
