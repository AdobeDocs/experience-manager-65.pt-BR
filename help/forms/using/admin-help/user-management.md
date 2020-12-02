---
title: Gerenciamento de usuários
seo-title: Gerenciamento de usuários
description: O Gerenciamento de usuários permite ativar o SSO entre AEM módulos de formulários e aplicativos protegidos pelo Netegrity SiteMinder usando SAML. Este documento fornece mais informações sobre o Gerenciamento de usuários.
seo-description: O Gerenciamento de usuários permite ativar o SSO entre AEM módulos de formulários e aplicativos protegidos pelo Netegrity SiteMinder usando SAML. Este documento fornece mais informações sobre o Gerenciamento de usuários.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# Gerenciamento de usuários {#user-management}

O Gerenciamento de usuários permite ativar o logon único (SSO) entre AEM módulos de formulários e aplicativos protegidos pelo Netegrity SiteMinder usando o SAML (Security Assertion Markup Language). Quando o SSO é implementado, as páginas de logon do usuário dos formulários AEM não são obrigatórias e não são exibidas se o usuário já estiver autenticado pelo portal de empresa.

Para obter informações sobre como melhorar o desempenho do banco de dados e sincronização de diretório para DB2, consulte [banco de dados IBM DB2: Execução de comandos para manutenção regular](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurando o Gerenciamento de usuários para um servidor LDAP habilitado para SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se você tiver um servidor LDAP habilitado para SSL, configure o Gerenciamento de usuários para trabalhar com ele. (Consulte [Configurar o Gerenciamento de Usuário para um servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Configuração de privilégios de usuário para uso com o Documento Security {#setting-user-privileges-for-use-with-document-security}

Crie um usuário administrador que tenha os privilégios apropriados para criar usuários e grupos. Se o seu ambiente de formulários AEM incluir a Segurança do Documento, conceda o privilégio de gerenciar usuários convidados e locais a um usuário que será o administrador desses usuários. Atribua também a função Usuário do console de administração para fornecer ao usuário acesso ao console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Para visualização de usuários e grupos em domínios selecionados durante pesquisas de usuários de políticas, um superadministrador ou administrador de conjuntos de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista visível do usuário e grupo para cada conjunto de políticas criado.

A lista visível de usuário e grupo está visível para o coordenador do conjunto de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos para adicionar às políticas. Se essa tarefa não for executada, o coordenador do conjunto de políticas não encontrará nenhum usuário ou grupo a ser adicionado à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas.

>[!NOTE]
>
>A criação de domínios deve ser feita antes que qualquer política possa ser criada.

### Definir usuários e grupos visíveis {#set-visible-users-and-groups}

Depois de instalar e configurar o ambiente de formulários AEM com a Segurança do Documento, configure todos os domínios apropriados no Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Segurança do Documento > Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Selecione Conjunto de políticas global e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.
1. Navegue até Serviços > Segurança do documento > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.

## Restrições de usuário do administrador {#administrator-user-restrictions}

Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas da Web podem existir fora de um firewall, permitir tarefas de nível administrativo pode representar um risco à segurança. Somente os usuários que tiverem privilégios de Administrador ou Usuário do Workspace poderão acessar as páginas da Web do usuário final.

>[!NOTE]
>
>O Flex Workspace está obsoleto para AEM versão de formulários.

