---
title: Gerenciar contas de usuário convidadas e locais
seo-title: Managing invited and local user accounts
description: Usando a segurança de documentos, você pode pesquisar, exibir, editar, bloquear, desbloquear e excluir contas de usuários convidadas e locais.
seo-description: Using document security, you can search for, view, edit, lock, unlock, and delete invited and local user accounts.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# Gerenciar contas de usuário convidadas e locais {#managing-invited-and-local-user-accounts}

Use a página Usuários Convidados e Locais para gerenciar seus usuários convidados e locais. Esta página é exibida somente se os seguintes requisitos forem atendidos:

* Você é um administrador que recebe a função Gerenciar usuários convidados e locais de segurança de documentos e a função Usuário do console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* O registro de usuário convidado está habilitado. (Consulte [Configurando o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

A página Usuários Convidados e Locais contém duas guias que podem ser usadas para pesquisar, exibir, editar, bloquear, desbloquear e excluir contas de usuários convidados e locais.

Você também pode enviar emails de registro manualmente para os usuários convidados. Você pode fazer isso, por exemplo, se o período de registro que o email autorizou terminar e o usuário não puder usar o URL para se registrar. Nesse caso, você pode reenviar um email de registro para o usuário convidado. Quando o usuário convidado registra e ativa a conta, o usuário se torna um usuário local.

>[!NOTE]
>
>Os usuários convidados também podem ser adicionados diretamente pelo diretório LDAP que documenta referências de segurança, ou quando um usuário ou administrador convida um novo usuário ao criar ou editar uma política, iniciando, portanto, um email de convite de registro. Os usuários poderão adicionar novos usuários convidados às políticas se você habilitar a opção Habilitar Registro de Usuário Convidado na página Registro de Usuário Convidado.

## Adicionar um usuário convidado {#add-an-invited-user}

É possível adicionar uma ou mais contas de usuário convidadas à segurança de documentos de cada vez. Para adicionar uma conta de usuário convidado, é necessário o endereço de email do usuário. Quando você adiciona um usuário, a segurança de documentos envia um email de registro convidando o usuário a se registrar.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e, em seguida, clique em Convidar novo usuário.
1. Digite os endereços de email dos usuários que deseja convidar. Insira vários endereços em uma linha, separados por vírgula.

   A mensagem que você criou ao habilitar o registro de usuário convidado é enviada aos usuários. (Consulte [Configurando o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Clique em OK.

## Exibir informações sobre um usuário local {#view-information-about-a-local-user}

Você pode exibir informações sobre usuários locais, incluindo nome, endereço de email, organização, status de registro e domínio.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e, em seguida, clique em Convidar novo usuário.
1. Clique na guia Usuários Locais e, na página Gerenciar Usuários Locais, clique no endereço de email do usuário que deseja exibir.

   Os detalhes do usuário são exibidos, e você pode redefinir a senha do usuário e desativar a conta.

## Enviar um email para um usuário externo não registrado {#send-an-email-to-an-unregistered-external-user}

Quando você adiciona um usuário convidado, a segurança de documentos envia automaticamente uma solicitação de email de registro. Você também pode gerar manualmente um email de registro para enviar a um usuário convidado que ainda não se registrou. Você pode fazer isso, por exemplo, para enviar um novo convite se o email de registro de um usuário convidado expirar.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais.
1. Na lista de usuários, marque a caixa de seleção para cada usuário para enviar um email de registro e clique em Reenviar email de convite.
1. Revise a lista de usuários selecionados e clique em OK.

## Redefinir uma senha de usuário local {#reset-a-local-user-password}

Você pode redefinir senhas para usuários convidados ativados que se registraram com a segurança de documentos, mas esqueceram a senha. Ao redefinir uma senha, é gerado um email contendo uma senha nova e temporária para o usuário.

Quando você ativou o processo de registro de usuário convidado, criou uma mensagem de email que será enviada aos usuários solicitando que eles redefinam suas senhas. (Consulte [Configurando o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e clique na guia Usuários locais.
1. Na lista de usuários, selecione o usuário apropriado.
1. Na página Gerenciar usuário local, clique em Redefinir senha e em OK. Um email de redefinição de senha contendo a nova senha é enviado ao usuário.

## Ativar ou desativar uma conta de usuário {#enable-or-disable-a-user-account}

Você pode desativar as contas de usuário locais para impedir temporariamente que um usuário faça logon na segurança de documentos. Quando você desativa a conta, o usuário não pode usar documentos protegidos por política nem criar ou aplicar políticas.

Você pode ativar uma conta de usuário local que esteja desativada no momento. Não é possível habilitar uma conta de usuário convidado que esteja listada como registrada. O status registered indica que o usuário convidado está registrado, mas ainda não ativou a conta usando o link no email de ativação.

**Restringir uma conta de usuário**

1. No Administration Console, clique em Serviços > segurança de documentos > Usuários Convidados e Locais e clique na guia Usuários Locais.
1. Na lista de usuários, selecione o usuário apropriado.
1. Na página Detalhes do usuário local, clique em Desativar conta.

**Restaurar uma conta de usuário**

1. Clique em Usuários Convidados e Locais e clique na guia Usuários Locais.
1. Na lista de usuários, selecione o usuário apropriado.
1. Na página Detalhes do usuário local, clique em Ativar conta.

## Remover uma conta de usuário convidado {#remove-an-invited-user-account}

Você pode excluir contas de usuário convidadas da segurança de documentos. Você pode excluir uma conta, por exemplo, quando um usuário altera as informações de sua conta de email pessoal.

Se você deletar uma conta de usuário, somente você ou outro administrador poderá restabelecer a conta selecionando a opção Adicionar Usuário Convidado na página Usuários Convidados. Os usuários não podem adicionar a conta de usuário excluída a uma política e nenhum processo de convite pode ser iniciado por esse método.

>[!NOTE]
>
>Os usuários convidados que foram excluídos por meio da interface de Gerenciamento de usuários de formulários AEM não podem ser convidados novamente até que sejam excluídos novamente usando o procedimento a seguir.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e clique na guia Usuários convidados.
1. Marque a caixa de seleção ao lado de um ou mais usuários, clique em Excluir e em OK.

## Procurar uma conta de usuário convidado {#search-for-an-invited-user-account}

Você pode pesquisar contas de usuário convidadas usando um endereço de email.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais.
1. Na caixa Localizar email, digite o endereço de email do usuário e clique em Localizar.

## Procurar uma conta de usuário local {#search-for-a-local-user-account}

Você pode pesquisar um usuário local usando o endereço de email ou o nome e o domínio do usuário.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e clique na guia Usuários locais.
1. Digite os critérios de pesquisa na caixa Localizar, selecione Nome ou Email e clique em Localizar.

## Remover uma conta de usuário local {#remove-a-local-user-account}

Você pode excluir contas de usuário locais da segurança de documentos. Você pode excluir contas, por exemplo, quando os usuários alteram as informações de suas contas de email pessoais.

1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais e clique na guia Usuários locais.
1. Marque a caixa de seleção ao lado de um ou mais usuários, clique em Excluir e em OK.

## Classificar a lista de usuários {#sort-the-user-list}

É possível encontrar usuários mais facilmente classificando a lista de usuários por cabeçalho de coluna. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna é usada atualmente para classificar:

* Um triângulo apontando para cima indica a ordem crescente.
* Um triângulo para baixo indica ordem decrescente.

   1. No console de administração, clique em Serviços > Segurança de documentos > Usuários convidados e locais.
   1. Para classificar usuários convidados, clique na guia Usuários Convidados e clique no cabeçalho de coluna apropriado.
   1. Para classificar usuários locais, clique na guia Usuários Locais e clique no cabeçalho de coluna apropriado.
