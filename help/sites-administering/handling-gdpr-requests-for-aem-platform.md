---
title: Lidar com solicitações do GDPR para o Adobe Experience Manager Foundation
description: Lidar com solicitações do GDPR para o Adobe Experience Manager Foundation
contentOwner: sarchiz
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 40%

---

# Lidar com solicitações do GDPR para a base do Adobe Experience Manager (AEM){#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR, CCPA e assim por diante.

## Suporte ao GDPR da Fundação AEM {#aem-foundation-gdpr-support}

No nível da Fundação AEM, os Dados Pessoais armazenados são o Perfil do Usuário. Portanto, as informações neste artigo abordam principalmente como acessar e excluir perfis de usuário, atendendo às solicitações de Acesso e Exclusão do GDPR, respectivamente.

## Acessar um perfil de usuário {#accessing-a-user-profile}

### Etapas manuais {#manual-steps}

1. Abra o console Administração do usuário, navegando até **[!UICONTROL Configurações - Segurança - Usuários]** ou navegando diretamente para `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. Em seguida, pesquise pelo usuário em questão digitando o nome na barra de pesquisa na parte superior da página:

   ![usersearch](assets/usersearch.png)

1. Por fim, clique para abrir o perfil do usuário, e verifique na guia **[!UICONTROL Detalhes]**.

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP {#http-api}

Como mencionado, a Adobe fornece APIs para acessar dados do usuário, a fim de facilitar a automação. Há vários tipos de APIs que você pode usar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

*Descobrir a página inicial do usuário:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Recuperando dados do usuário*

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desativar um usuário e excluir os perfis associados {#disabling-a-user-and-deleting-the-associated-profiles}

### Desativar usuário {#disable-user}

1. Abra o console Administração do usuário e procure o usuário em questão, conforme descrito acima.
1. Passe o mouse sobre o usuário e clique no ícone de seleção. O perfil fica cinza, indicando que está selecionado.

1. Pressione o botão Desativar no menu superior para desativar o usuário:

   ![userdisable](assets/userdisable.png)

1. Por fim, confirme a ação:

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   A interface do usuário indica que o usuário é desativado ao esmaecer e adicionar um bloqueio ao cartão de perfil:

   ![disableduser](assets/disableduser.png)

### Excluir informações do perfil do usuário {#delete-user-profile-information}

1. Efetue logon no CRXDE Lite e procure pelo `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Abra o nó do usuário localizado em `[!UICONTROL /home/users]` por padrão:

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Excluir nós de perfil e todos os seus filhos. Há dois formatos para os nós de perfil, dependendo da versão do AEM:

   1. O perfil privado padrão em `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, para novos perfis criados usando o AEM 6.5.

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP {#http-api-1}

Os procedimentos a seguir usam o `curl` de linha de comando para ilustrar como desativar o usuário com a tag **[!UICONTROL cavery]** `userId` e excluir perfis de `cavery` que estão disponíveis no local padrão.

* *Descobrir a página inicial do usuário*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Desabilitar o usuário*

Usando o caminho do nó da propriedade home da carga JSON retornada do comando acima:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Exclusão de perfis de usuário*

Usando o caminho do nó da propriedade página inicial do conteúdo JSON retornada a partir do comando de descoberta de conta e os locais de nós de perfil conhecidos e prontos para uso:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
