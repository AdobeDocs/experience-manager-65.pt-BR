---
title: Consoles de gerenciamento de membros e grupos
description: Como acessar os consoles de Gerenciamento de Membros e Grupos
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Consoles de gerenciamento de membros e grupos {#members-groups-management-consoles}

## Visão geral {#overview}

Os recursos do AEM Communities geralmente exigem que os visitantes do site sejam registrados e conectados antes de participar de uma comunidade no ambiente de publicação. O registro do usuário só precisa existir no ambiente de publicação, e eles são comumente chamados de *membros* para diferenciá-los de *usuários* registrados no ambiente de criação.

### Membros (usuários) no Publish {#members-users-on-publish}

Usando os consoles Membros e Grupos de Comunidades, membros e grupos de membros registrados no ambiente *publicar* podem ser criados e gerenciados no ambiente *autor*. Isso só é possível quando o [serviço de túnel](deploy-communities.md#tunnel-service-on-author) está habilitado.

### Usuários no autor {#users-on-author}

Para gerenciar usuários e grupos registrados no ambiente *autor*, é necessário usar o console de segurança da plataforma:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**.

>[!NOTE]
>
>Com conteúdos de amostra implantados e ativados, muitos usuários de amostra existem nos ambientes do autor e de publicação. Estes usuários não estarão presentes durante a execução com o [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console de membros {#members-console}

No ambiente de criação, para acessar o console Membros para gerenciar membros registrados no ambiente de publicação:

* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Membros]**

>[!CAUTION]
>
>Não será possível usar o console Membros se o [serviço de túnel](deploy-communities.md#tunnel-service-on-author) não estiver habilitado.

![O console do membro](assets/member-console1.png)

### Pesquisar {#search-features}

Selecione o ícone do painel lateral no lado esquerdo do cabeçalho do `Members` para alternar e abrir o painel lateral de pesquisa.

![Ícone do painel lateral de pesquisa.](assets/leftpanel-icon.png)


![Opções de filtro para o console do membro](assets/member-console2.png)

Selecione o ícone de pesquisa no lado esquerdo do cabeçalho do `Members` para alternar o painel lateral de pesquisa fechado.

### Estatísticas de Membros {#member-statistics}

As colunas que exibem `Views`, `Posts`, `Follows` e `Likes` são atualizadas quando o usuário é membro de um ou mais sites da comunidade com o Adobe Analytics [habilitado](sites-console.md#analytics).

### Exportar CSV {#export-csv}

A seleção do link `Export CSV` resulta no download de todos os membros como uma lista de valores separados por vírgula, adequada para importação em uma planilha.

Os cabeçalhos de coluna são

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Criar novo membro {#create-new-member}

Selecione `Create Member` para criar um usuário no ambiente de publicação.

![A janela Criar novo membro](assets/create-member1.png)

### GERAL - Detalhes do membro {#general-member-details}

A maioria dos campos são campos opcionais que o membro pode preencher posteriormente em seu perfil.

* **[!UICONTROL ID]**

(*Obrigatório*) A ID autorizável é a ID de entrada do membro.
Por padrão, a ID é definida como o valor do endereço de email necessário.
*Uma vez criada, a ID não pode ser modificada*.

* **[!UICONTROL Endereço de email]**

(*Obrigatório*) O endereço de email do membro.
O membro pode alterar seu endereço de e-mail ao atualizar seu perfil.
Se a ID tiver assumido como padrão o endereço de email, a ID *não* será alterada quando o endereço de email for alterado.

* **[!UICONTROL Senha]**

  (*Obrigatório*) A senha de entrada.

* **[!UICONTROL Senha do Retype]**

  (*Obrigatório*) Digite novamente a senha para verificação.

* **[!UICONTROL Adicionar membro aos sites]**

  (*Opcional*) Selecione um dos sites existentes da comunidade para adicionar o membro ao grupo de membros do site da comunidade.

* **[!UICONTROL Adicionar membro a grupos]**

  (*Opcional*) Selecione dentre os grupos de membros existentes para adicionar o membro a esse grupo.

* Selecione **[!UICONTROL Salvar]**

### GERAL - Configurações da conta {#general-account-settings}

Nas Configurações da conta, é possível para um administrador da comunidade:

* **[!UICONTROL Status]**
   * Proibido
Um membro não pode fazer logon, impedindo-o de exibir páginas ou participar de atividades que exigem logon. Eles ainda podem visitar anonimamente um site da comunidade aberto.

   * Não proibido
Um membro tem acesso total ao site da comunidade.

  O padrão é `Not Banned`.

* **[!UICONTROL Limites de contribuição]**

  Se marcada, a capacidade do membro de publicar conteúdo é limitada.
O padrão depende da configuração dos limites de contribuição.
Consulte [Limites de contribuição de membros](limits.md).

* **[!UICONTROL Alterar senha]**

  Um link que está presente ao modificar um membro existente. Fornece a capacidade de um administrador da comunidade redefinir uma senha para um membro.

### GERAL - Foto {#general-photo}

Para fornecer um avatar para o membro, comece selecionando **[!UICONTROL Fazer upload da imagem]** e escolha uma imagem do tipo .jpg, .png, .tif ou .gif. O tamanho preferido para uma imagem é 240 x 240 pixels a 72 dpi.

### GERAL - Adicionar membro aos sites {#general-add-member-to-sites}

O membro pode ser adicionado a um ou mais grupos de membros de sites da comunidade. Comece inserindo texto na caixa de texto.

### GERAL - Adicionar membro aos grupos {#general-add-member-to-groups}

O membro pode ser adicionado a um ou mais grupos de membros. Comece inserindo texto na caixa de texto.

### Guia SELOS {#badges-tab}

O painel `BADGES` fornece a capacidade de atribuir selos manualmente e revogá-los. As medalhas podem ser para funções atribuídas e medalhas normalmente obtidas.

Consulte também [Pontuação e medalhas](implementing-scoring.md).

![A janela Editar Configurações de Associação](assets/create-member2.png)

* **[!UICONTROL Adicionar medalhas]**
   * Comece a digitar para selecionar entre [selos disponíveis](badges.md). Depois que um selo é selecionado, escolha cada site ou todos os sites, nos quais o selo deve ser exibido junto com o avatar do membro.
   * Vários selos e sites podem ser escolhidos.
* **[!UICONTROL Remover medalhas]**
   * Selecione o ícone da lixeira ao lado de um selo para removê-lo.

## Console de grupos {#groups-console}

O console Grupos, disponível no ambiente de criação, permite a criação e o gerenciamento de grupos de membros registrados no ambiente de publicação. É particularmente útil para [Grupos de membros privilegiados](users.md#privilegedmembersgroups).

Para acessar o console Grupos:
* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Grupos]**.

>[!CAUTION]
>
>Não será possível usar o console Grupos se o [serviço de túnel](deploy-communities.md#tunnel-service-on-author) não estiver habilitado.

### Criar novo grupo {#create-new-group}

Selecione `Add Group` para criar um grupo no ambiente de publicação.

![A janela Criar novo grupo](assets/group-console1.png)

Os campos obrigatórios para criar um grupo de membros do lado da publicação são:

* **[!UICONTROL ID]**

  (*Obrigatório*) A ID exclusiva do grupo.

  *Uma vez criada, a ID não pode ser modificada.*

* **[!UICONTROL Nome]**

  (*Opcional*) O nome para exibição do grupo.

  O valor padrão é a ID.

* **[!UICONTROL Descrição]**

  (*Opcional*) Uma descrição da finalidade e das permissões do grupo.

* **[!UICONTROL Adicionar Membros Ao Grupo]**

  (*Opcional*) Selecione membros do lado da publicação a serem incluídos como membros iniciais do grupo.

* Selecione **[!UICONTROL Salvar]**

## Administradores autorizados {#authorized-administrators}

Ao trabalhar com membros no console Membros das Comunidades, é necessário entrar como um usuário com permissões apropriadas e que o agente de replicação usado pelo [serviço de túnel](deploy-communities.md#tunnel-service-on-author) esteja configurado corretamente.

Se não estiver conectado como `admin`, o usuário conectado deverá ser membro do grupo de usuários `administrators`.

Consulte também [Agentes de replicação no Author](deploy-communities.md#replication-agents-on-author).
