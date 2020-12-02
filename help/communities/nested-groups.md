---
title: Criação de grupos aninhados
seo-title: Criação de grupos aninhados
description: Criar grupos aninhados
seo-description: Criar grupos aninhados
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 5%

---


# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor de AEM, na navegação global:

* Selecione **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Selecione **[!UICONTROL engajar pasta]** para abri-la.
* Selecione o cartão para o **[!UICONTROL Tutorial de introdução]** site em inglês.

   * Selecione a imagem do cartão.
   * Selecione *e não* um ícone.

O resultado é alcançar o [console Grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

A função groups será exibida como uma pasta na qual as instâncias de grupos são criadas. Selecione a pasta Grupos para abri-la. O grupo criado na publicação está visível.

![create-new-group](assets/create-new-group.png)

## Criar grupo Artes Principais {#create-main-arts-group}

Esse grupo pode ser criado porque a estrutura do site para engajamento inclui uma função de grupos. A configuração da função em `Reference Template` do site permite a seleção de qualquer modelo de grupo ativado. Portanto, o modelo escolhido para esse novo grupo é `Reference Group`.

Esses consoles são semelhantes ao console Sites das Comunidades.

* Selecione **[!UICONTROL Criar grupo]**.

* **Modelo de grupo da comunidade**:

   * **[!UICONTROL Título]** do grupo da comunidade: Artes.
   * **[!UICONTROL Descrição]** do grupo da comunidade: Um grupo pai para vários grupos artísticos.
   * **[!UICONTROL Raiz]** do grupo da comunidade:  *deixe como padrão*.
   * **[!UICONTROL Idioma(s) adicional(is)]** disponível(is) do grupo comunitário: use o menu suspenso para selecionar os idiomas do grupo da comunidade disponíveis. O menu exibe todos os idiomas nos quais o site da comunidade pai foi criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.
   * **[!UICONTROL Nome]** do grupo da comunidade: artes.
   * **[!UICONTROL Modelo]**: menu suspenso para selecionar  `Reference Group.`
   * Selecione **[!UICONTROL Próximo]**.

![Grupos de comunidade aninhados](assets/parent-to-nestedgroup.png)

Continue pelos outros painéis com estas configurações:

* **[!UICONTROL Design]**

   * Altere o design ou permita o design padrão do site pai.
   * Selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Configurações]**

   * **[!UICONTROL Moderação]**

      * Deixe vazio (herde do site pai).
   * **[!UICONTROL Associação]**

      * Usar padrão `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Selecione Próximo]**.



* Selecione **[!UICONTROL Criar]**.

### Aninhando grupos no grupo Arts {#nesting-groups-within-arts-group}

A pasta `groups` agora contém dois grupos (atualize a página).

![Aninhamento dos grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de criar grupos aninhados no grupo `arts`, passe o mouse sobre o cartão `arts` e selecione o ícone de publicação para publicá-lo.

![site de publicação](assets/publish-site.png)

Aguarde a confirmação de que o grupo foi publicado.

![publicado em grupo](assets/group-published.png)

O grupo `arts` também deve conter uma pasta `groups`, mas que esteja vazia e na qual novos grupos possam ser criados. Navegue até a pasta do grupo artístico e crie 3 grupos aninhados, cada um com uma configuração de associação diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nome: `visual`
   * Modelo: `Reference Group`
   * Associação: selecione `Optional Membership`, um grupo público, aberto para todos os membros.

1. **[!UICONTROL Auditoria]**

   * Título: `Auditory Arts`
   * Nome: `auditory`
   * Modelo: `Reference Group`
   * Associação: selecione `Required Membership`, um grupo aberto, disponível para os membros participarem.

1. **[!UICONTROL História]**

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: selecione `Restricted Membership`, um grupo secreto, visível apenas para os membros convidados. Por exemplo, convide [usuário de demonstração](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Atualize a página para ver os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados no console Sites das Comunidades:

* Selecione **[!UICONTROL pasta de participação]**
* Selecione **[!UICONTROL Cartão de Tutorial de Introdução]**
* Selecionar a pasta **[!UICONTROL Grupos]**
* Selecione **[!UICONTROL cartão de artes]**
* Selecionar a pasta **[!UICONTROL Grupos]**

![create-new-group2](assets/create-new-group2.png)

## Grupos de publicação {#publishing-groups}

![site de publicação](assets/publish-site.png)

Depois de publicar o site da comunidade principal:

* Publique cada grupo individualmente:

   * Aguardando confirmação de que o grupo foi publicado.

* Publicar grupo pai antes de publicar quaisquer grupos aninhados em:

   * Todos os grupos devem ser publicados de cima para baixo.

![publicado em grupo](assets/group-published.png)

## Experiência em Publicar {#experience-on-publish}

É possível experimentar os diferentes grupos ao fazer logon, por exemplo, com os [usuários de demonstração](/help/communities/tutorials.md#demo-users) usados para:

* Membro do grupo Arte/Histórico: emily.andrews@mailinator.com/senha
   * O grupo restrito (secreto), artes/história, é visível:
   * Podem ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).

* Gerente de grupo: aaron.mcdonald@mailinator.com/senha

   * Podem ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).
   * Não é possível ver grupos restritos (secretos).

Acesse os consoles Comunidades [Membros e grupos](/help/communities/members.md) no autor para adicionar outros usuários a vários grupos de membros que correspondam aos grupos da comunidade.

