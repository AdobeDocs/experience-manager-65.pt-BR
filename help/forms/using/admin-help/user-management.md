---
title: Gerenciamento de usuários
seo-title: User Management
description: O Gerenciamento de usuários permite habilitar o SSO entre AEM módulos de formulários e aplicativos protegidos pelo Netegrity SiteMinder usando o SAML. Este documento fornece mais informações sobre o Gerenciamento de usuários.
seo-description: User Management allows you to enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Gerenciamento de usuários {#user-management}

O Gerenciamento de usuários permite habilitar o logon único (SSO) entre os módulos de formulários AEM e os aplicativos protegidos pelo Netegrity SiteMinder usando o SAML (Security Assertion Markup Language). Quando o SSO é implementado, as páginas de logon do usuário dos formulários AEM não são necessárias e não são exibidas se o usuário já estiver autenticado no portal da empresa.

Para obter informações sobre como melhorar o desempenho de sincronização de banco de dados e diretório para DB2, consulte [Banco de dados IBM DB2: Executando comandos para manutenção regular](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurando o Gerenciamento de Usuários para um servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se você tiver um servidor LDAP habilitado para SSL, configure o Gerenciamento de usuários para funcionar com ele. (Consulte [Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Definindo privilégios de usuário para uso com a Segurança de documento {#setting-user-privileges-for-use-with-document-security}

Crie um usuário administrador que tenha os privilégios apropriados para criar usuários e grupos. Se o seu ambiente de AEM forms incluir a Segurança de documentos, conceda o privilégio de gerenciar usuários convidados e locais para um usuário que será o administrador desses usuários. Atribua também a função Usuário do console de administração para fornecer ao usuário acesso ao console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Para visualizar usuários e grupos em domínios selecionados durante pesquisas de política do usuário, um superadministrador ou administrador de conjunto de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista de usuários e grupos visível para cada conjunto de políticas criado.

A lista de usuários e grupos visível é visível para o coordenador do conjunto de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos para adicionar às políticas. Se esta tarefa não for executada, o coordenador do conjunto de políticas não encontrará usuários ou grupos para adicionar à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas.

>[!NOTE]
>
>A criação de domínios deve ser feita antes que qualquer política possa ser criada.

### Definir usuários e grupos visíveis {#set-visible-users-and-groups}

Depois de instalar e configurar o ambiente de formulários AEM com a Segurança de documentos, configure todos os domínios apropriados no Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Segurança de documentos > Políticas e, em seguida, clique na guia Conjuntos de políticas .
1. Selecione Conjunto de políticas global e clique na guia Usuários e grupos visíveis .
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.
1. Navegue até Serviços > segurança do documento > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis .
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.

## Restrições do usuário administrador {#administrator-user-restrictions}

Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas da Web podem existir fora de um firewall, permitir tarefas de nível administrativo pode representar um risco à segurança. Somente os usuários que têm os privilégios de Administrador do Workspace ou Usuário do Workspace podem acessar as páginas da Web do usuário final.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.
