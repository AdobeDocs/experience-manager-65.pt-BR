---
title: Operações do Granite - Administração de usuários e grupos
seo-title: Granite Operations - User and Group Administration
description: Saiba mais sobre a administração de usuários e grupos do Granite.
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 4%

---

# Operações do Granite - Administração de usuários e grupos{#granite-operations-user-and-group-administration}

Como o Granite incorpora a implementação do Repositório CRX da Especificação da API JCR, ele tem sua própria administração de usuários e grupos.

Estas contas são a base subjacente da [Contas AEM](/help/sites-administering/security.md) e qualquer alteração de conta feita com a administração do Granite será refletida se/quando as contas forem acessadas do [AEM console Usuários](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (por exemplo, `http://localhost:4502/useradmin`). No console Usuários do AEM, também é possível gerenciar os privilégios e outras AEM específicas.

Os consoles de administração de usuários e grupos do Granite estão disponíveis no **[Ferramentas](/help/sites-administering/tools-consoles.md)** console da interface otimizada para toque:

![chlimage_1-72](assets/chlimage_1-72a.png)

Como escolher **Usuários** ou **Grupos** no console Ferramentas , o console apropriado será aberto. Em ambos, você pode tomar uma ação usando a caixa de clique e, em seguida, as ações da barra de ferramentas ou abrindo os detalhes da conta através do link em **Nome**.

* [Administração do usuário](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   O **Usuários** listas de console:

   * o nome de usuário
   * o nome de logon do usuário (nome da conta)
   * qualquer título dado à conta

* [Administração de grupo](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   O **Grupos** listas de console:

   * o nome do grupo
   * a descrição do grupo
   * o número de usuários/grupos no grupo

## Administração do usuário {#user-administration}

### Adicionar um novo usuário {#adding-a-new-user}

1. Use o **Adicionar usuário** ícone :

   ![](do-not-localize/chlimage_1-1.png)

1. O **Criar usuário** o formulário será aberto:

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   Aqui você pode inserir os detalhes do usuário para a conta (a maioria é padrão e autoexplicativa):

   * **ID**

      Essa é a identificação exclusiva da conta de usuário. É obrigatório e não pode conter espaços.

   * **Endereço de email**
   * **Senha**

      Uma senha é obrigatória.

   * **Digite a senha novamente**

      Isso é obrigatório, pois é necessário para a confirmação da senha.

   * **Nome**
   * **Sobrenome**
   * **Número de telefone**
   * **Cargo**
   * **Rua**
   * **Móvel**
   * **Cidade**
   * **Código postal**
   * **País**
   * **Estado**
   * **Título**
   * **Sexo**
   * **Sobre**
   * **Configurações da conta**

      * **Status**
Você pode sinalizar a conta como 
**ative** ou **inativo**.
   * **Foto**

      Aqui você pode fazer upload de uma foto para usar como avatar.

      Tipos de arquivo aceitos: `.jpg .png .tif .gif`

      Tamanho preferencial: `240x240px`

   * **Adicionar usuário aos grupos**

      Use o menu suspenso de seleção para selecionar grupos dos quais o usuário deve ser membro. Depois de selecionado, use a **X** pelo nome a ser desmarcado antes de salvar.

   * **Grupos**

      Uma lista de grupos dos quais o usuário é membro no momento. Use o **X** pelo nome a ser desmarcado antes de salvar.


1. Ao definir o uso da conta do usuário, faça o seguinte:

   * **Cancelar** para suspender o registro.
   * **Salvar** para concluir o registro. A criação da conta de usuário será confirmada com uma mensagem.

### Editar um usuário existente {#editing-an-existing-user}

1. Acesse os detalhes do usuário no link sob o nome do usuário no console Usuários .

1. Agora você pode editar os detalhes como em [Adicionar um novo usuário](#adding-a-new-user).

1. Acesse os detalhes do usuário no link sob o nome do usuário no console Usuários .

1. Agora você pode editar os detalhes como em [Adicionar um novo usuário](#adding-a-new-user).

### Alterar a senha de um usuário existente {#changing-the-password-for-an-existing-user}

1. Acesse os detalhes do usuário no link sob o nome do usuário no console Usuários .

1. Agora você pode editar os detalhes como em [Adicionar um novo usuário](#adding-a-new-user). Em **Configurações da conta** há um link para **Alterar senha**.

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. O **Alterar senha** será aberta. Digite e digite novamente a nova senha, juntamente com a senha. Use **OK** para confirmar as alterações.

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   Uma mensagem confirmará que a senha foi alterada.

### Atribuição de grupo rápido {#quick-group-assignment}

1. Use a caixa de clique para sinalizar um ou mais usuários.
1. Use o **Grupos** ícone :

   ![](do-not-localize/chlimage_1-2.png)

   Para abrir o menu suspenso de seleção de grupo:

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. Na caixa de seleção, você pode selecionar ou desmarcar grupos aos quais a conta de usuário deve pertencer.

1. Quando você atribuiu ou não atribuiu os grupos, conforme necessário, use:

   * **Cancelar** para suspender as alterações
   * **Salvar** para confirmar as alterações

### Excluindo Detalhes do Usuário Existente {#deleting-existing-user-details}

1. Use a caixa de clique para sinalizar um ou mais usuários.
1. Use o **Excluir** ícone para excluir os detalhes do usuário:

   ![](do-not-localize/chlimage_1-3.png)

1. Você receberá uma solicitação para confirmar a exclusão e, em seguida, uma mensagem confirmará que a exclusão real ocorreu.

## Administração de grupo {#group-administration}

### Adicionar um novo grupo {#adding-a-new-group}

1. Use o ícone Adicionar grupo :

   ![](do-not-localize/chlimage_1-4.png)

1. O **Criar grupo** o formulário será aberto:

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   Aqui você pode inserir os detalhes do grupo:

   * **ID**

      Esse é um identificador exclusivo do grupo. Isso é obrigatório e não pode conter espaços.

   * **Nome**

      Um nome para o grupo; será exibido no console Grupos .

   * **Descrição**

      Uma descrição do grupo.

   * **Adicionar membros ao grupo**

      Use o menu suspenso de seleção para selecionar usuários a serem adicionados ao grupo. Depois de selecionado, use a **X** pelo nome a ser desmarcado antes de salvar.

   * **Membros do grupo**

      Uma lista de usuários no grupo. Use o **X** pelo nome a ser desmarcado antes de salvar.

1. Após definir o grupo, use:

   * **Cancelar** para suspender o registro.
   * **Salvar** para concluir o registro. A criação do grupo será confirmada com uma mensagem.

### Editar um grupo existente {#editing-an-existing-group}

1. Acesse os detalhes do grupo no link sob o nome do grupo no console Grupos .

1. Agora você pode editar e salvar os detalhes como em [Adicionar um novo grupo](#adding-a-new-group).

### Copiando um grupo existente {#copying-an-existing-group}

1. Use a caixa de clique para sinalizar um grupo.
1. Use o **Copiar** ícone para copiar os detalhes do grupo:

   ![](do-not-localize/chlimage_1-5.png)

1. O **Editar configurações de grupo** será aberto.

   A ID do grupo será a mesma do original, mas terá o prefixo `Copy of`. Você deve editar isso, pois a ID não pode conter espaços. Todos os outros detalhes serão iguais ao original.

   Agora você pode editar e salvar os detalhes como em [Adicionar um novo grupo](#adding-a-new-group).

### Excluindo um grupo existente {#deleting-an-existing-group}

1. Use a caixa de clique para sinalizar um ou mais grupos.
1. Use o **Excluir** ícone para excluir os detalhes do grupo:

   ![](do-not-localize/chlimage_1-6.png)

1. Você receberá uma solicitação para confirmar a exclusão e, em seguida, uma mensagem confirmará que a exclusão real ocorreu.
