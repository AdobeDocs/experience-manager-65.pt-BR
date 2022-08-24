---
title: Provisionamento de usuário em tempo real
seo-title: Just-in-time user provisioning
description: Use o provisionamento just-in-time para adicionar usuários ao Gerenciamento de usuários após a autenticação bem-sucedida e atribuir dinamicamente funções e grupos relevantes ao novo usuário.
seo-description: Use just-in-time provisioning to add users to User Management after successfull authentication and dynamically assign relevant roles and groups to the new user.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Provisionamento de usuário em tempo real {#just-in-time-user-provisioning}

AEM formulários oferecem suporte ao provisionamento just-in-time de usuários que ainda não existem no Gerenciamento de usuários. Com o provisionamento just-in-time, os usuários são adicionados automaticamente ao Gerenciamento de usuários depois que suas credenciais são autenticadas com êxito. Além disso, funções e grupos relevantes são atribuídos dinamicamente ao novo usuário.

## Necessidade de provisionamento de usuário em tempo real {#need-for-just-in-time-user-provisioning}

A autenticação tradicional funciona assim:

1. Quando um usuário tenta fazer logon em AEM formulários, o Gerenciamento de usuários transmite as credenciais do usuário sequencialmente para todos os provedores de autenticação disponíveis. (As credenciais de logon incluem uma combinação de nome de usuário/senha, tíquete Kerberos, assinatura PKCS7 e assim por diante.)
1. O provedor de autenticação valida as credenciais.
1. O provedor de autenticação verifica se o usuário existe no banco de dados do Gerenciamento de usuários. Os seguintes resultados são possíveis:

   **Existe:** Se o usuário estiver atual e desbloqueado, o Gerenciamento de usuários retornará a autenticação bem-sucedida. No entanto, se o usuário não for atual ou estiver bloqueado, o Gerenciamento de usuários retornará a falha de autenticação.

   **Não existe:** O Gerenciamento de usuários retorna a falha de autenticação.

   **Inválido:** O Gerenciamento de usuários retorna a falha de autenticação.

1. O resultado retornado pelo provedor de autenticação é avaliado. Se o provedor de autenticação retornar a autenticação bem-sucedido, o usuário poderá fazer logon. Caso contrário, o Gerenciamento de usuários verificará o próximo provedor de autenticação (etapas 2 a 3).
1. A falha de autenticação é retornada se nenhum provedor de autenticação disponível validar as credenciais do usuário.

Quando o provisionamento just-in-time é implementado, um novo usuário é criado dinamicamente no Gerenciamento de usuários se um dos provedores de autenticação validar as credenciais do usuário. (Após a etapa 3 do procedimento de autenticação tradicional, acima).

## Implemente o provisionamento do usuário just-in-time {#implement-just-in-time-user-provisioning}

### APIs para provisionamento just-in-time {#apis-for-just-in-time-provisioning}

Os AEM forms fornecem as seguintes APIs para o provisionamento just-in-time:

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Considerações ao criar um domínio ativado apenas no tempo {#considerations-while-creating-a-just-in-time-enabled-domain}

* Ao criar um `IdentityCreator` para um domínio híbrido, verifique se uma senha de teste está especificada para o usuário local. Não deixe este campo de senha vazio.
* Recomendação: Use `DomainSpecificAuthentication` para validar as credenciais do usuário em relação a um domínio específico.

### Criar um domínio ativado apenas no tempo {#create-a-just-in-time-enabled-domain}

1. Escreva um DSC implementando as APIs na seção &quot;APIs para provisionamento just-in-time&quot;.
1. Implante o DSC no servidor de formulários.
1. Crie um domínio ativado apenas no tempo:

   * No Console de Administração, clique em Configurações > Gerenciamento de Usuário > Gerenciamento de Domínio > Novo Domínio Enterprise.
   * Configure o domínio e selecione Habilitar provisionamento Exatamente no Tempo. <!--Fix broken link (See Setting up and managing domains).-->
   * Adicionar provedores de autenticação. Ao adicionar provedores de autenticação, na tela Nova Autenticação, selecione um Criador de Identidade e Provedor de Atribuição registrado.

1. Salve o novo domínio.

## Por trás das cenas {#behind-the-scenes}

Suponha que um usuário esteja tentando fazer logon em AEM formulários e que um provedor de autenticação aceite suas credenciais de usuário. Se o usuário ainda não existir no banco de dados do Gerenciamento de usuários, a verificação de identidade do usuário falhará. AEM formulários agora executa as seguintes ações:

1. Crie um `UserProvisioningBO` com os dados de autenticação e coloque-os em um mapa de credenciais.
1. Com base nas informações de domínio retornadas por `UserProvisioningBO`, buscar e invocar o `IdentityCreator` e `AssignmentProvider` para o domínio .
1. Invocar `IdentityCreator`. Se retornar um bem-sucedido `AuthResponse`, extrair `UserInfo` no mapa de credenciais. Passe para o `AssignmentProvider` para atribuição de grupo/função e qualquer outro pós-processamento depois que o usuário é criado.
1. Se o usuário for criado com sucesso, retorne a tentativa de logon pelo usuário como bem-sucedido.
1. Para domínios híbridos, extraia informações do usuário dos dados de autenticação fornecidos ao provedor de autenticação. Se essas informações forem buscadas com sucesso, crie o usuário dinamicamente.

>[!NOTE]
>
>O recurso de provisionamento just-in-time é fornecido com uma implementação padrão de `IdentityCreator` que você pode usar para criar usuários dinamicamente. Os usuários são criados com as informações associadas aos diretórios no domínio.
