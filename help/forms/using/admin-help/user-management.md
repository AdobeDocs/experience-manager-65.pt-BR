---
title: Gerenciamento de usuários
seo-title: Gerenciamento de usuários
description: O Gerenciamento de usuários permite ativar o SSO entre os módulos de formulários AEM e os aplicativos protegidos pelo Netegrity SiteMinder usando o SAML. Este documento fornece mais informações sobre o Gerenciamento de usuários.
seo-description: O Gerenciamento de usuários permite ativar o SSO entre os módulos de formulários AEM e os aplicativos protegidos pelo Netegrity SiteMinder usando o SAML. Este documento fornece mais informações sobre o Gerenciamento de usuários.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gerenciamento de usuários {#user-management}

O Gerenciamento de usuários permite ativar o logon único (SSO) entre os módulos de formulários AEM e os aplicativos protegidos pelo Netegrity SiteMinder usando o SAML (Security Assertion Markup Language). Quando o SSO é implementado, as páginas de logon de usuário dos formulários AEM não são obrigatórias e não são exibidas se o usuário já estiver autenticado pelo portal da empresa.

Para obter informações sobre como melhorar o desempenho do banco de dados e sincronização de diretório para o DB2, consulte o banco de dados [IBM DB2: Execução de comandos para manutenção](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)regular.

## Configuração do Gerenciamento de usuários para um servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se você tiver um servidor LDAP habilitado para SSL, configure o Gerenciamento de usuários para trabalhar com ele. (Consulte [Configurar o Gerenciamento de usuários para um servidor](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)LDAP habilitado para SSL.)

## Configurar privilégios de usuário para uso com o Document Security {#setting-user-privileges-for-use-with-document-security}

Crie um usuário administrador que tenha os privilégios apropriados para criar usuários e grupos. Se o ambiente de formulários do AEM incluir o Document Security, conceda o privilégio de gerenciar usuários convidados e locais a um usuário que será o administrador desses usuários. Atribua também a função Usuário do console de administração para fornecer ao usuário acesso ao console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Para exibir usuários e grupos em domínios selecionados durante pesquisas de usuários de políticas, um superadministrador ou administrador de conjuntos de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista de usuários e grupos visível para cada conjunto de políticas criado.

A lista de usuários e grupos visíveis é visível para o coordenador do conjunto de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos a serem adicionados às políticas. Se essa tarefa não for executada, o coordenador do conjunto de políticas não encontrará usuários ou grupos para adicionar à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas.

>[!NOTE]
>
> A criação de domínios deve ser feita antes que qualquer política possa ser criada.

### Definir usuários e grupos visíveis {#set-visible-users-and-groups}

Depois de instalar e configurar seu ambiente de formulários AEM com o Document Security, configure todos os domínios apropriados no Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Document Security> Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Selecione Conjunto de políticas global e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.
1. Navegue até Serviços > segurança do documento > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.

## Restrições do usuário administrador {#administrator-user-restrictions}

Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas da Web podem existir fora de um firewall, permitir tarefas de nível administrativo pode representar um risco à segurança. Somente os usuários que tiverem privilégios de Administrador ou Usuário do Workspace poderão acessar as páginas da Web do usuário final.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão de formulários do AEM.

