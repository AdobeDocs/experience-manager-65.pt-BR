---
title: Gerenciamento de contas de usuário convidadas e locais
seo-title: Gerenciamento de contas de usuário convidadas e locais
description: Usando a segurança do documento, você pode procurar, visualização, editar, bloquear, desbloquear e excluir contas de usuário convidadas e locais.
seo-description: Usando a segurança do documento, você pode procurar, visualização, editar, bloquear, desbloquear e excluir contas de usuário convidadas e locais.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---


# Gerenciamento de contas de usuário convidadas e locais {#managing-invited-and-local-user-accounts}

Use a página Usuários convidados e locais para gerenciar seus usuários convidados e locais. Esta página é exibida somente se os seguintes requisitos forem atendidos:

* Você é um administrador ao qual é atribuída a função Gerenciamento de segurança do documento Convidado e Usuários locais e a função Usuário do console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* O registro de usuário convidado está ativado. (Consulte [Configurar o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

A página Usuários convidados e locais contém duas guias que podem ser usadas para pesquisar, visualização, editar, bloquear, desbloquear e excluir contas de usuários convidados e locais.

Você também pode enviar emails de inscrição manualmente para os usuários convidados. Você pode desejar fazer isso, por exemplo, se o período de registro no qual o email autorizado termina e o usuário não puder usar o URL para registro. Nesse caso, você pode reenviar um e-mail de registro para o usuário convidado. Quando o usuário convidado se registra e ativa a conta, o usuário se torna um usuário local.

>[!NOTE]
>
>Os usuários convidados também podem ser adicionados diretamente por meio do diretório LDAP que faz referência à segurança do documento, ou quando um usuário ou administrador convida um novo usuário ao criar ou editar uma política, iniciando, portanto, um email de convite de registro. Os usuários poderão adicionar novos usuários convidados a políticas se você ativar a opção Habilitar inscrição de usuários convidados na página Inscrição de usuários convidados.

## Adicionar um usuário convidado {#add-an-invited-user}

Você pode adicionar uma ou mais contas de usuário convidadas à segurança do documento de cada vez. Para adicionar uma conta de usuário convidada, você precisa do endereço de email do usuário. Quando você adiciona um usuário, a segurança do documento envia um email de inscrição convidando o usuário a se registrar.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique em Convidar novo usuário.
1. Digite os endereços de email dos usuários que deseja convidar. Insira vários endereços em uma linha, separados por vírgula.

   A mensagem que você criou ao ativar o registro de usuário convidado é enviada aos usuários. (Consulte [Configurar o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Clique em OK.

## Informações de visualização sobre um usuário local {#view-information-about-a-local-user}

Você pode visualização informações sobre usuários locais, incluindo nome, endereço de email, organização, status de registro e domínio.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique em Convidar novo usuário.
1. Clique na guia Usuários locais e, na página Gerenciar usuários locais, clique no endereço de email do usuário que deseja visualização.

   Os detalhes do usuário são exibidos e você pode redefinir a senha do usuário e desativar a conta.

## Enviar um email para um usuário externo não registrado {#send-an-email-to-an-unregistered-external-user}

Quando você adiciona um usuário convidado, a segurança do documento envia automaticamente ao usuário uma solicitação de e-mail de registro. Você também pode gerar manualmente um email de inscrição para enviar a um usuário convidado que ainda não se registrou. Você pode desejar fazer isso, por exemplo, para enviar um novo convite se o email de inscrição de um usuário convidado expirar.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais.
1. Na lista do usuário, marque a caixa de seleção para cada usuário para enviar um e-mail de inscrição e clique em Reenviar e-mail de convite.
1. Revise a lista de usuários selecionados e clique em OK.

## Redefinir uma senha de usuário local {#reset-a-local-user-password}

Você pode redefinir senhas para usuários convidados ativados que se registraram com segurança de documento, mas esqueceram sua senha. Quando você redefine uma senha, um email é gerado que contém uma nova senha temporária para o usuário.

Quando você ativou o processo de registro do usuário convidado, criou uma mensagem de email que será enviada aos usuários solicitando que redefinam suas senhas. (Consulte [Configurar o registro de usuário convidado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique na guia Usuários locais.
1. Na lista do usuário, selecione o usuário apropriado.
1. Na página Gerenciar usuário local, clique em Redefinir senha e clique em OK. Um email de redefinição de senha contendo a nova senha é enviado ao usuário.

## Habilitar ou desabilitar uma conta de usuário {#enable-or-disable-a-user-account}

Você pode desativar as contas de usuário locais para restringir temporariamente o logon de um usuário à segurança do documento. Quando você desativa a conta, o usuário não pode usar documentos protegidos por política ou criar ou aplicar políticas.

Você pode ativar uma conta de usuário local que esteja desabilitada no momento. Não é possível ativar uma conta de usuário convidada que esteja listada como registrada. O status registrado indica que o usuário convidado está registrado, mas ainda não ativou a conta usando o link no email de ativação.

**Restringir uma conta de usuário**

1. No Console de administração, clique em Serviços > Segurança do documento > Usuários convidados e locais e clique na guia Usuários locais.
1. Na lista do usuário, selecione o usuário apropriado.
1. Na página Detalhes do usuário local, clique em Desativar conta.

**Reinstalar uma conta de usuário**

1. Clique em Usuários convidados e locais e clique na guia Usuários locais.
1. Na lista do usuário, selecione o usuário apropriado.
1. Na página Detalhes do usuário local, clique em Ativar conta.

## Remover uma conta de usuário convidada {#remove-an-invited-user-account}

Você pode excluir contas de usuário convidadas da segurança do documento. Você pode querer excluir uma conta, por exemplo, quando um usuário altera suas informações pessoais de conta de email.

Se você excluir uma conta de usuário, somente você ou outro administrador poderá reinstalar a conta selecionando a opção Adicionar usuário convidado na página Usuários convidados. Os usuários não podem adicionar a conta de usuário excluída a uma política, e nenhum processo de convite pode ser iniciado por esse método.

>[!NOTE]
>
>Os usuários convidados que foram excluídos por meio da interface de Gerenciamento de usuários de formulários AEM não poderão ser convidados novamente até que tenham sido excluídos novamente usando o procedimento a seguir.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique na guia Usuários convidados.
1. Marque a caixa de seleção ao lado de um ou mais usuários, clique em Excluir e, em seguida, clique em OK.

## Procurar uma conta de usuário convidada {#search-for-an-invited-user-account}

Você pode procurar contas de usuário convidadas usando um endereço de email.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais.
1. Na caixa Localizar email, digite o endereço de email do usuário e clique em Localizar.

## Procurar uma conta de usuário local {#search-for-a-local-user-account}

Você pode procurar um usuário local usando o endereço de email ou o nome e o domínio do usuário.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique na guia Usuários locais.
1. Digite os critérios de pesquisa na caixa Localizar, selecione Nome ou Email e clique em Localizar.

## Remover uma conta de usuário local {#remove-a-local-user-account}

Você pode excluir contas de usuário locais da segurança do documento. Você pode desejar excluir contas, por exemplo, quando os usuários alterarem suas informações pessoais de conta de email.

1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais e clique na guia Usuários locais.
1. Marque a caixa de seleção ao lado de um ou mais usuários, clique em Excluir e, em seguida, clique em OK.

## Classificar a lista do usuário {#sort-the-user-list}

Você pode encontrar usuários mais facilmente classificando a lista do usuário por cabeçalho de coluna. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna é usada atualmente para classificar:

* Um triângulo apontando para cima indica ordem crescente.
* Um triângulo apontando para baixo indica uma ordem decrescente.

   1. No console de administração, clique em Serviços > Segurança do Documento > Usuários convidados e locais.
   1. Para classificar usuários convidados, clique na guia Usuários convidados e no cabeçalho da coluna apropriada.
   1. Para classificar usuários locais, clique na guia Usuários locais e clique no cabeçalho da coluna apropriada.

