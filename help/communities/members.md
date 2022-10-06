---
title: Consoles de gerenciamento de membros e grupos
seo-title: Members & Groups Management Consoles
description: Como acessar os consoles Gerenciamento de membros e grupos
seo-description: How to access Members and Groups Management consoles
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 4%

---

# Consoles de gerenciamento de membros e grupos {#members-groups-management-consoles}

## Visão geral {#overview}

Os recursos do AEM Communities geralmente exigem que os visitantes do site sejam registrados e conectados antes de participar de uma comunidade no ambiente de publicação. O registro de usuários só precisa existir no ambiente de publicação e geralmente são chamados de *membros* para diferenciá-los de *usuários* registrado no ambiente do autor.

### Membros (usuários) na publicação {#members-users-on-publish}

Usando os consoles Membros e Grupos das Comunidades, membros e grupos de membros registrados no *publicar* pode ser criado e gerenciado a partir do *autor* ambiente. Isso só é possível quando a variável [serviço de túnel](deploy-communities.md#tunnel-service-on-author) estiver ativado.

### Usuários no autor {#users-on-author}

Para gerenciar usuários e grupos registrados na *autor* , é necessário para usar o console de segurança da plataforma:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**.

>[!NOTE]
>
>Com o conteúdo de amostra implantado e ativado, muitos usuários de amostra existem nos ambientes de autor e publicação. Esses usuários não estarão presentes ao executar com [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console de membros {#members-console}

No ambiente de criação, para acessar o console Membros para gerenciar membros registrados no ambiente de publicação:

* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Membros]**

>[!CAUTION]
>
>Não será possível usar o console Membros se a variável [serviço de túnel](deploy-communities.md#tunnel-service-on-author) não está ativado.

![membro-console1](assets/member-console1.png)

### Pesquisar {#search-features}

Selecione o ícone do painel lateral no lado esquerdo do `Members` para alternar, abra o painel lateral de pesquisa.

![](assets/leftpanel-icon.png)


![membro-console2](assets/member-console2.png)

Selecione o ícone de pesquisa no lado esquerdo do `Members` para ativar o painel lateral de pesquisa fechado.

### Estatísticas do Membro {#member-statistics}

As colunas exibindo `Views`, `Posts`, `Follows` e `Likes` são atualizados quando o usuário é membro de um ou mais sites da comunidade com o Adobe Analytics [ativado](sites-console.md#analytics).

### Exportar CSV {#export-csv}

Selecionar o `Export CSV` O link resulta no download de todos os membros como uma lista de valores separados por vírgula, adequados para importação em uma planilha.

Os cabeçalhos da coluna são

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Criar novo membro {#create-new-member}

Selecionar `Create Member` para criar um usuário no ambiente de publicação.

![create-member1](assets/create-member1.png)

### GERAL - Detalhes do Membro {#general-member-details}

A maioria dos campos são campos opcionais que o membro pode preencher posteriormente no perfil.

* **[!UICONTROL ID]**

(*Obrigatório*) A ID autorizável é a ID de logon do membro.
Por padrão, a ID é definida com o valor do endereço de email necessário.
*Depois de criada, a ID não pode ser modificada*.

* **[!UICONTROL Endereço de email]**

(*Obrigatório*) O endereço de email do membro.
O membro pode alterar seu endereço de email ao atualizar seu perfil.I Se a ID for padronizada para o endereço de email, a ID *not* alterar quando o endereço de email for alterado.

* **[!UICONTROL Senha]**

   (*Obrigatório*) A senha de logon.

* **[!UICONTROL Digite a senha novamente]**

   (*Obrigatório*) Digite novamente a senha para verificação.

* **[!UICONTROL Adicionar membro aos Sites]**

   (*Opcional*) Selecione entre sites da comunidade existentes para adicionar o membro ao grupo de membros do site da comunidade.

* **[!UICONTROL Adicionar membro aos grupos]**

   (*Opcional*) Selecione de grupos de membros existentes para adicionar o membro a esse grupo.

* Selecione **[!UICONTROL Salvar]**

### GERAL - Configurações de conta {#general-account-settings}

Em Configurações de conta, é possível para um administrador de comunidade:

* **[!UICONTROL Status]**
   * Proibido Um membro não consegue entrar, impedindo-o de visualizar páginas ou participar de atividades que exigem o logon. Eles ainda podem visitar anonimamente um site aberto da comunidade.

   * Não proibido Um membro tem acesso total ao site da comunidade.

   O padrão é `Not Banned`.

* **[!UICONTROL Limites de contribuição]**

   Se marcada, a capacidade do membro de publicar conteúdo é limitada.
O padrão depende da configuração dos limites de contribuição.
Consulte [Limites de contribuição dos membros](limits.md).

* **[!UICONTROL Alterar senha]**

   Um link que está presente ao modificar um membro existente. Fornece a capacidade de um administrador da comunidade redefinir uma senha para um membro.

### GERAL - Foto {#general-photo}

Para fornecer um avatar para o membro, comece selecionando **[!UICONTROL Carregar imagem]** e escolha uma imagem do tipo .jpg, .png, .tif ou .gif. O tamanho preferencial de uma imagem é 240 x 240 pixels a 72 dpi.

### GERAL - Adicionar Membro aos Sites {#general-add-member-to-sites}

O membro pode ser adicionado a um ou mais grupos de membros do site da comunidade. Comece inserindo texto na caixa de texto.

### GERAL - Adicionar Membro a Grupos {#general-add-member-to-groups}

O membro pode ser acrescentado a um ou mais grupos de membros. Comece inserindo texto na caixa de texto.

### Guia BADGES {#badges-tab}

O `BADGES` O painel oferece a capacidade de atribuir manualmente os emblemas e de revogá-los. Os emblemas podem ser para funções atribuídas, bem como emblemas normalmente ganhos.

Consulte também [Pontuação e emblemas](implementing-scoring.md).

![create-member2](assets/create-member2.png)

* **[!UICONTROL Adicionar emblemas]**
   * Começar a digitar para selecionar de [etiquetas disponíveis](badges.md). Depois que um selo for selecionado, escolha cada site, ou todos os sites, nos quais o selo deve ser exibido junto com o avatar do membro.
   * Vários emblemas e sites podem ser escolhidos.
* **[!UICONTROL Remover emblemas]**
   * Selecione o ícone da lixeira ao lado de um selo para removê-lo.

## Console Grupos {#groups-console}

O console Grupos , disponível no ambiente de criação, permite a criação e o gerenciamento de grupos de membros registrados no ambiente de publicação. É particularmente útil para:
* [Grupos de membros privilegiados](users.md#privilegedmembersgroups)
* Atribuição baseada em grupos de [recursos de habilitação](resources.md)

Para acessar o console Grupos :
* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Grupos]**.

>[!CAUTION]
>
>Não será possível usar o console Grupos se a variável [serviço de túnel](deploy-communities.md#tunnel-service-on-author) não está ativado.

### Criar novo grupo {#create-new-group}

Selecionar `Add Group` para criar um grupo no ambiente de publicação.

![group-console1](assets/group-console1.png)

Os campos necessários para criar um novo grupo de membros do lado da publicação são:

* **[!UICONTROL ID]**

   (*Obrigatório*) A ID exclusiva do grupo.

   *Depois de criada, a ID não pode ser modificada.*

* **[!UICONTROL Nome]**

   (*Opcional*) O nome de exibição do grupo.

   O valor padrão é a ID.

* **[!UICONTROL Descrição]**

   (*Opcional*) Uma descrição da finalidade e das permissões do grupo.

* **[!UICONTROL Adicionar membros ao grupo]**

   (*Opcional*) Selecione os membros do lado da publicação a serem incluídos como membros iniciais do grupo.

* Selecione **[!UICONTROL Salvar]**

## Administradores autorizados {#authorized-administrators}

Ao trabalhar com membros no console de membros das Comunidades, é necessário fazer logon como um usuário com as permissões apropriadas e para o agente de replicação usado pelo [serviço de túnel](deploy-communities.md#tunnel-service-on-author) para ser configurado corretamente.

Se não tiver feito logon como `admin`, o usuário conectado deve ser um membro do `administrators` grupo de usuários.

Consulte também [Agentes de Replicação no Autor](deploy-communities.md#replication-agents-on-author).
