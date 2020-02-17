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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Criação de grupos aninhados{#authoring-nested-groups}

## Criação de grupos no autor {#creating-groups-on-author}

Na instância do autor de AEM, na navegação global:

* Selecione** Comunidades, Sites.**
* Selecione **engajar pasta** para abri-la.
* Selecione o cartão para o site **Introdução ao tutorial** em inglês.

   * Selecione a imagem do cartão.
   * Não *selecione* um ícone.

O resultado é alcançar o console [](/help/communities/groups.md)Grupos:

![chlimage_1-91](assets/chlimage_1-91.png)

A função groups será exibida como uma pasta na qual as instâncias de grupos são criadas. Selecione a pasta Grupos para abri-la. O grupo criado na publicação está visível.

![chlimage_1-92](assets/chlimage_1-92.png)

## Criar grupo de artes principais {#create-main-arts-group}

Esse grupo pode ser criado porque a estrutura do site para engajamento inclui uma função de grupos. A configuração da função no padrão do site `Reference Template` permite a seleção de qualquer modelo de grupo habilitado. Assim, o modelo escolhido para esse novo grupo é o `Reference Group`.

Esses consoles são semelhantes ao console Sites das Comunidades.

* Selecione **Criar grupo.**
* **Modelo de grupo da comunidade**:

   * Título do grupo da comunidade: Artes.
   * Descrição do grupo da comunidade: Um grupo pai para vários grupos artísticos.
   * Raiz do grupo da comunidade: *deixe como padrão.*
   * Idioma(s) adicional(is) disponível(is) do grupo comunitário: use o menu suspenso para selecionar os idiomas do grupo da comunidade disponíveis. O menu exibe todos os idiomas nos quais o site da comunidade pai foi criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.
   * Nome do grupo da comunidade: artes.
   * Modelo: menu suspenso para selecionar `Reference Group.`
   * `Select Next.`

![Grupos de comunidade aninhados](assets/parent-to-nestedgroup.png)

Continue pelos outros painéis com estas configurações:

* **Design**

   * Altere o design ou permita o design padrão do site pai.
   * Selecione **Próximo.**

* **Configurações**

   * **Moderação**

      * deixar vazio (herdar do site pai).
   * **Associação**

      * use default `Optional Membership.`
   * **Miniatura**

      * `*optional.*`
   * `Select Next.`




* Selecione **Criar.**

### Aninhamento de grupos no grupo Artes {#nesting-groups-within-arts-group}

A `groups` pasta agora contém dois grupos (atualize a página).

![Aninhamento dos grupos](assets/create-community-group.png)

#### Publicar grupo {#publish-group}

Antes de criar grupos aninhados dentro do `arts`grupo, passe o mouse sobre o `arts` cartão e selecione o ícone de publicação para publicá-lo.

![chlimage_1-93](assets/chlimage_1-93.png)

Aguarde a confirmação de que o grupo foi publicado.

![chlimage_1-94](assets/chlimage_1-94.png)

O `arts` grupo também deve conter uma `groups` pasta, mas que esteja vazia e na qual novos grupos possam ser criados. Navegue até a pasta do grupo artístico e crie 3 grupos aninhados, cada um com uma configuração de associação diferente:

1. Visual

   * Título: `Visual Arts`
   * Nome: `visual`
   * Modelo: `Reference Group`
   * Associação: selecionar `Optional Membership`um grupo público, abrir para todos os membros

1. Auditoria

   * Título: `Auditory Arts`
   * Nome: `auditory`
   * Modelo: `Reference Group`
   * Associação: selecionar `Required Membership`um grupo aberto, disponível para os membros participarem

1. História

   * Título: `Art History`
   * Nome: `history`
   * Modelo: `Reference Group`
   * Associação: selecionar `Restricted Membership`um grupo secreto, visível somente para membros convidados, como exemplo, convidar usuário [de](/help/communities/tutorials.md#demo-users) demonstração `emily.andrews@mailinator.com`

Atualize a página para ver os três grupos aninhados (subcomunidades).

Para navegar até os grupos aninhados no console Sites das Comunidades:

* selecionar pasta de participação
* selecione o cartão Tutorial de Introdução
* selecionar pasta Grupos
* selecionar cartão de artes
* selecionar pasta Grupos

![chlimage_1-95](assets/chlimage_1-95.png)

## Grupos de publicação {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Depois de publicar o site da comunidade principal:

* publicar cada grupo individualmente

   * aguardando confirmação de que o grupo foi publicado

* publicar grupo pai antes de publicar quaisquer grupos aninhados dentro de

   * todos os grupos devem ser publicados de cima para baixo.

![chlimage_1-97](assets/chlimage_1-97.png)

## Experiência de publicação {#experience-on-publish}

É possível experimentar os diferentes grupos ao fazer logon, por exemplo, com os usuários [da](/help/communities/tutorials.md#demo-users) demonstração usados para

* Membro do grupo Arte/Histórico: emily.andrews@mailinator.com/senha

   * o grupo restrito (secreto), artes/história, é visível
   * podem ver grupos opcionais (públicos)
   * pode ingressar em grupos restritos (abertos)

* Gerente de grupo: aaron.mcdonald@mailinator.com/senha

   * podem ver grupos opcionais (públicos)
   * pode ingressar em grupos restritos (abertos)
   * não é possível ver grupos restritos (secretos)

Acesse os consoles [](/help/communities/members.md) Membros e Grupos das Comunidades no autor para adicionar outros usuários a vários grupos de membros que correspondam aos grupos da comunidade.

