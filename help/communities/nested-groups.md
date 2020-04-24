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
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor de AEM, na navegação global:

* Selecione **[!UICONTROL Comunidades] > **[!UICONTROL Sites]**.
* Selecione **[!UICONTROL engajar pasta]** para abri-la.
* Selecione o cartão para o site **[!UICONTROL Introdução ao tutorial]** em inglês.

   * Selecione a imagem do cartão.
   * Não *selecione* um ícone.

O resultado é alcançar o console [](/help/communities/groups.md)Grupos:

![chlimage_1-91](assets/chlimage_1-91.png)

A função groups será exibida como uma pasta na qual as instâncias de grupos são criadas. Selecione a pasta Grupos para abri-la. O grupo criado na publicação está visível.

![chlimage_1-92](assets/chlimage_1-92.png)

## Criar grupo de artes principais {#create-main-arts-group}

Esse grupo pode ser criado porque a estrutura do site para engajamento inclui uma função de grupos. A configuração da função no padrão do site `Reference Template` permite a seleção de qualquer modelo de grupo habilitado. Assim, o modelo escolhido para esse novo grupo é o `Reference Group`.

Esses consoles são semelhantes ao console Sites das Comunidades.

* Selecione **[!UICONTROL Criar grupo]**.

* **Modelo de grupo da comunidade**:

   * **[!UICONTROL Título]** do grupo da comunidade: Artes.
   * **[!UICONTROL Descrição]** do grupo da comunidade: Um grupo pai para vários grupos artísticos.
   * **[!UICONTROL Raiz]** do grupo da comunidade: *deixe como padrão*.
   * **[!UICONTROL Idioma(s) adicional(is)]** disponível(is) do grupo comunitário: use o menu suspenso para selecionar os idiomas do grupo da comunidade disponíveis. O menu exibe todos os idiomas nos quais o site da comunidade pai foi criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.
   * **[!UICONTROL Nome]** do grupo da comunidade: artes.
   * **[!UICONTROL Modelo]**: menu suspenso para selecionar `Reference Group.`
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

      * Use default `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Selecione Próximo]**.



* Selecione **[!UICONTROL Criar]**.

### Aninhamento de grupos no grupo Artes {#nesting-groups-within-arts-group}

A `groups` pasta agora contém dois grupos (atualize a página).

![Aninhamento dos grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de criar grupos aninhados dentro do `arts` grupo, passe o mouse sobre o `arts` cartão e selecione o ícone de publicação para publicá-lo.

![chlimage_1-93](assets/chlimage_1-93.png)

Aguarde a confirmação de que o grupo foi publicado.

![chlimage_1-94](assets/chlimage_1-94.png)

O `arts` grupo também deve conter uma `groups` pasta, mas que esteja vazia e na qual novos grupos possam ser criados. Navegue até a pasta do grupo artístico e crie 3 grupos aninhados, cada um com uma configuração de associação diferente:

1. **[!UICONTROL Visual]**

   * Título: `Visual Arts`
   * Nome: `visual`
   * Modelo: `Reference Group`
   * Associação: selecione `Optional Membership`, um grupo público, abrir para todos os membros.

1. **[!UICONTROL Auditoria]**

   * Título: `Auditory Arts`
   * Nome: `auditory`
   * Modelo: `Reference Group`
   * Associação: selecione `Required Membership`, um grupo aberto, disponível para os membros ingressarem.

1. **[!UICONTROL História]**

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: selecione `Restricted Membership`, um grupo secreto, visível somente para membros convidados. Como exemplo, convide um usuário [de](/help/communities/tutorials.md#demo-users) demonstração `emily.andrews@mailinator.com`.

Atualize a página para ver os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados no console Sites das Comunidades:

* Selecionar pasta **[!UICONTROL de participação]**
* Selecione o cartão Tutorial de **[!UICONTROL Introdução]**
* Selecionar pasta **[!UICONTROL Grupos]**
* Selecionar cartão **[!UICONTROL artístico]**
* Selecionar pasta **[!UICONTROL Grupos]**

![chlimage_1-95](assets/chlimage_1-95.png)

## Grupos de publicação {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Depois de publicar o site da comunidade principal:

* Publique cada grupo individualmente:

   * Aguardando confirmação de que o grupo foi publicado.

* Publicar grupo pai antes de publicar quaisquer grupos aninhados em:

   * Todos os grupos devem ser publicados de cima para baixo.

![chlimage_1-97](assets/chlimage_1-97.png)

## Experiência de publicação {#experience-on-publish}

É possível experimentar os diferentes grupos ao fazer logon, por exemplo, com os usuários [da](/help/communities/tutorials.md#demo-users) demonstração usados para:

* Membro do grupo Arte/Histórico: emily.andrews@mailinator.com/senha
   * O grupo restrito (secreto), artes/história, é visível:
   * Podem ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).

* Gerente de grupo: aaron.mcdonald@mailinator.com/senha

   * Podem ver grupos opcionais (públicos).
   * Pode ingressar em grupos restritos (abertos).
   * Não é possível ver grupos restritos (secretos).

Acesse os consoles [](/help/communities/members.md) Membros e Grupos das Comunidades no autor para adicionar outros usuários a vários grupos de membros que correspondam aos grupos da comunidade.

