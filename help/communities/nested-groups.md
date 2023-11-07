---
title: Criação de grupos aninhados
description: Saiba como criar grupos aninhados para um site do Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 4%

---

# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor do AEM, na navegação global:

* Selecionar **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Selecionar **[!UICONTROL pasta de engajamento]** para abri-lo.
* Selecione o cartão para o **[!UICONTROL Tutorial de introdução]** Site em inglês.

   * Selecione a imagem do cartão.
   * Fazer *não* selecione um ícone.

O resultado é alcançar o objetivo [Console de grupos](/help/communities/groups.md):

![create-group](assets/create-group.png)

A função de grupos é exibida como uma pasta na qual as instâncias dos grupos são criadas. Para abri-lo, selecione a pasta Grupos. O grupo criado em Publicar está visível.

![create-new-group](assets/create-new-group.png)

## Criar grupo principal de artes {#create-main-arts-group}

Este grupo pode ser criado porque a estrutura do site para participação inclui a função de um grupo. A configuração da função no repositório do site `Reference Template` O padrão é permitir a seleção de qualquer modelo de grupo ativado. Assim, o modelo escolhido para esse novo grupo é o `Reference Group`.

Esses consoles são semelhantes ao console Sites de comunidades.

* Selecionar **[!UICONTROL Criar grupo]**

* **Modelo de grupo da comunidade**:

   * **[!UICONTROL Título do grupo da comunidade]**: Artes
   * **[!UICONTROL Descrição do grupo da comunidade]**: um grupo principal para vários grupos de artes
   * **[!UICONTROL Raiz do grupo da comunidade]**: *deixar como padrão*
   * **[!UICONTROL Idiomas adicionais disponíveis do Grupo da comunidade]**: use o menu suspenso para selecionar os idiomas disponíveis do grupo da comunidade. O menu exibe todos os idiomas nos quais o site pai da comunidade é criado. Os usuários podem selecionar entre esses idiomas para criar grupos em vários locais nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites de comunidade.
   * **[!UICONTROL Nome do grupo da comunidade]**: artes
   * **[!UICONTROL Modelo]**: menu suspenso para selecionar `Reference Group`
   * Selecione **[!UICONTROL Próximo]**

![Grupos de comunidades aninhados](assets/parent-to-nestedgroup.png)

Prossiga pelos outros painéis com estas configurações:

* **[!UICONTROL Design]**

   * Alterar o design ou permitir o design do site pai padrão.
   * Selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Configurações]**

   * **[!UICONTROL Moderação]**

      * Deixar em branco (herdar do site pai).

   * **[!UICONTROL Associação]**

      * Usar padrão `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`

      * **[!UICONTROL Selecione Próximo]**.

* Selecione **[!UICONTROL Criar]**.

### Aninhamento de grupos no grupo de artes {#nesting-groups-within-arts-group}

A variável `groups` A pasta agora contém dois grupos (atualize a página).

![Aninhamento dos grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de criar grupos aninhados no `arts` grupo, passe o mouse sobre a variável `arts` e selecione o ícone publicar para publicá-lo.

![site de publicação](assets/publish-site.png)

Aguarde a confirmação de que o grupo foi publicado.

![publicado pelo grupo](assets/group-published.png)

A variável `arts` O grupo também deve conter uma `groups` pasta, mas uma que esteja vazia e na qual novos grupos podem ser criados. Navegue até a pasta do grupo de artes e crie três grupos aninhados, cada um com uma configuração de associação diferente:

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

1. **[!UICONTROL História]**

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: selecione `Restricted Membership`, um grupo secreto, visível apenas para membros convidados. Como exemplo, convide [usuário de demonstração](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Atualize a página para que você possa ver todos os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados do console Sites de comunidades:

* Selecione o **[!UICONTROL pasta de engajamento]**
* Selecionar **[!UICONTROL Cartão Tutorial de introdução]**
* Selecione o **[!UICONTROL Grupos]** pasta
* Selecionar **[!UICONTROL cartão arts]**
* Selecione o **[!UICONTROL Grupos]** pasta

![create-new-group2](assets/create-new-group2.png)

## Publicar grupos {#publishing-groups}

![site de publicação](assets/publish-site.png)

Depois de publicar o site principal da comunidade:

* Publicar cada grupo individualmente:

   * Aguardando confirmação de que o grupo foi publicado.

* Publique o grupo pai antes de publicar qualquer grupo aninhado em:

   * Todos os grupos devem ser publicados de cima para baixo.

![publicado pelo grupo](assets/group-published.png)

## Experiência na publicação {#experience-on-publish}

É possível experimentar os diferentes grupos quando conectado, por exemplo, com a [usuários de demonstração](/help/communities/tutorials.md#demo-users) usado para:

* Membro do grupo Arte/Histórico: `emily.andrews@mailinator.com/password`
   * O grupo restrito (secreto), artes/história, está visível:
   * É possível ver grupos opcionais (públicos).
   * Capaz de ingressar em grupos restritos (abertos).

* Gerente de grupo: `aaron.mcdonald@mailinator.com/password`

   * É possível ver grupos opcionais (públicos).
   * Capaz de ingressar em grupos restritos (abertos).
   * Não é possível ver os grupos restritos (secretos).

Acesse as comunidades [Consoles Membros e grupos](/help/communities/members.md) em autor para adicionar outros usuários a vários grupos de membros que correspondem aos grupos da comunidade.
