---
title: Consoles de gerenciamento de membros e grupos
seo-title: Consoles de gerenciamento de membros e grupos
description: Como acessar os consoles Gerenciamento de membros e grupos
seo-description: Como acessar os consoles Gerenciamento de membros e grupos
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# Consoles de gerenciamento de membros e grupos {#members-groups-management-consoles}

## Visão geral {#overview}

Os recursos do AEM Communities geralmente exigem que os visitantes do site sejam registrados e conectados antes de participar de uma comunidade no ambiente de publicação. O registro do usuário só precisa existir no ambiente publish e eles são comumente chamados de *membros* para diferenciá-los dos *usuários* registrados no ambiente author.

### Membros (usuários) na publicação {#members-users-on-publish}

Usando os consoles Membros e Grupos das Comunidades, os membros e grupos de membros registrados no ambiente *publish* podem ser criados e gerenciados a partir do ambiente do *autor* . Isso só é possível quando o serviço [de](deploy-communities.md#tunnel-service-on-author) túnel está ativado.

### Usuários no autor {#users-on-author}

Para gerenciar usuários e grupos registrados no ambiente do *autor* , é necessário usar o console de segurança da plataforma:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**.

>[!NOTE]
>
>Com conteúdo de amostra implantado e ativado, muitos usuários de amostra existem nos ambientes de autor e publicação. Esses usuários não estarão presentes ao executar com [nosamplecontent runmode](../../help/sites-administering/production-ready.md).


## Console de membros {#members-console}

No ambiente author, para acessar o console Membros para gerenciar membros registrados no ambiente publish:

* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Membros]**

>[!CAUTION]
>
>Não será possível usar o console Membros se o serviço [de](deploy-communities.md#tunnel-service-on-author) túnel não estiver ativado.


![chlimage_1-119](assets/chlimage_1-119.png)

### Pesquisar {#search-features}

Selecione o ícone do painel lateral no lado esquerdo do cabeçalho para `Members` alternar entre abrir o painel lateral de pesquisa.

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

Selecione o ícone de pesquisa no lado esquerdo do cabeçalho para `Members` alternar o painel lateral de pesquisa fechado.

### Estatísticas dos Estados-Membros {#member-statistics}

As colunas que exibem `Views`, `Posts`e `Follows` são atualizadas quando o usuário é membro de um ou mais sites da comunidade com o Adobe Analytics `Likes` ativado [](sites-console.md#analytics).

### Exportar CSV {#export-csv}

A seleção do `Export CSV` link resulta no download de todos os membros como uma lista de valores separados por vírgula, adequados para importação em uma planilha.

Os cabeçalhos de coluna são

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Criar novo membro {#create-new-member}

Selecione `Create Member` para criar um usuário no ambiente de publicação.

![chlimage_1-122](assets/chlimage_1-122.png)

### GERAL - Detalhes dos membros {#general-member-details}

A maioria dos campos são opcionais, os membros podem preencher posteriormente seus perfis.

* **[!UICONTROL ID]**

(*Obrigatório*) A ID de autorização é a ID de logon do membro.
Por padrão, a ID é definida como o valor do endereço de email necessário.
*Depois de criada, a ID não pode ser modificada*.

* **[!UICONTROL Endereço de email]**

(*Obrigatório*) O endereço de email do membro.
O membro pode alterar seu endereço de email ao atualizar seu perfil.Se o padrão da ID for o endereço de email, a ID *não* será alterada quando o endereço de email for alterado.

* **[!UICONTROL Senha]**

   (*Obrigatório*) A senha de logon.

* **[!UICONTROL Digite a senha novamente]**

   (*Obrigatório*) Digite novamente a senha para verificação.

* **[!UICONTROL Adicionar membro aos Sites]**

   (*Opcional*) Selecione entre os sites da comunidade existente para adicionar o membro ao grupo de membros do site da comunidade.

* **[!UICONTROL Adicionar membro aos grupos]**

   (*Opcional*) Selecione dentre os grupos de membros existentes para adicionar o membro a esse grupo.

* Selecione **[!UICONTROL Salvar]**

### GERAL - Configurações de conta {#general-account-settings}

Em Configurações de conta, um administrador da comunidade pode:

* **[!UICONTROL Status]**
   * BanidoUm membro não pode fazer logon, impedindo que ele visualize páginas ou participe de atividades que exigem o logon. Eles ainda podem visitar anonimamente um site aberto da comunidade.

   * Não banidoUm membro tem acesso total ao site da comunidade.
   O padrão é `Not Banned`.

* **[!UICONTROL Limites de contribuição]**

   Se marcada, a capacidade do membro de publicar conteúdo é limitada.
O padrão depende da configuração dos limites de contribuição.
Consulte Limites [de contribuição do](limits.md)membro.

* **[!UICONTROL Alterar senha]**

   Um link que está presente ao modificar um membro existente. Fornece a capacidade de um administrador da comunidade redefinir uma senha para um membro.

### GERAL - Foto {#general-photo}

Para fornecer um avatar para o membro, comece selecionando **[!UICONTROL Carregar imagem]** e escolha uma imagem do tipo .jpg, .png, .tif ou .gif. O tamanho preferencial para uma imagem é 240 x 240 pixels a 72 dpi.

### GENERAL - Add Member to Sites {#general-add-member-to-sites}

O membro pode ser adicionado a um ou mais grupos de membros do site da comunidade. Comece inserindo o texto na caixa de texto.

### GENERAL - Add Member to Groups {#general-add-member-to-groups}

O membro pode ser acrescentado a um ou mais grupos de membros. Comece inserindo o texto na caixa de texto.

### Guia BADGES {#badges-tab}

O `BADGES` painel fornece a capacidade de atribuir manualmente os emblemas e de revogá-los. Os emblemas podem ser para funções atribuídas, bem como emblemas normalmente recebidos.

Consulte também [Pontuação e Distinções](implementing-scoring.md).

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL Adicionar emblemas]**
   * Comece digitando para selecionar entre os símbolos [](badges.md)disponíveis. Quando um crachá for selecionado, escolha cada site ou todos os sites nos quais o crachá deve ser exibido junto com o avatar do membro.
   * Vários símbolos e sites podem ser escolhidos.
* **[!UICONTROL Remover emblemas]**
   * Selecione o ícone da lixeira ao lado do crachá para removê-lo.

## Console de grupos {#groups-console}

O console Grupos, disponível no ambiente do autor, permite a criação e o gerenciamento de grupos de membros registrados no ambiente de publicação. É particularmente útil para:
* [Grupos de membros privilegiados](users.md#privilegedmembersgroups)
* Atribuição dos recursos de [ativação baseada em grupos](resources.md)

Para acessar o console Grupos:
* Na navegação global, selecione **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Grupos]**.

>[!CAUTION]
>
>Não será possível usar o console Grupos se o serviço [de](deploy-communities.md#tunnel-service-on-author) túnel não estiver ativado.


### Criar novo grupo {#create-new-group}

Selecione `Add Group` para criar um grupo no ambiente de publicação.

![chlimage_1-124](assets/chlimage_1-124.png)

Os campos necessários para criar um novo grupo de membros do lado da publicação são:

* **[!UICONTROL ID]**

   (*Obrigatório*) A ID exclusiva do grupo.

   *Depois de criada, a ID não pode ser modificada.*

* **[!UICONTROL Nome]**

   (*Opcional*) O nome de exibição do grupo.

   O valor padrão é a ID.

* **[!UICONTROL Descrição]**

   (*Opcional*) Uma descrição do objetivo e das permissões do grupo.

* **[!UICONTROL Adicionar membros ao grupo]**

   (*Opcional*) Selecione os membros do lado da publicação a serem incluídos como membros iniciais do grupo.

* Selecione **[!UICONTROL Salvar]**

## Administradores autorizados {#authorized-administrators}

Ao trabalhar com membros no console de membros das Comunidades, é necessário fazer logon como um usuário com as permissões apropriadas e configurar corretamente o agente de replicação usado pelo serviço [de](deploy-communities.md#tunnel-service-on-author) túnel.

Se não estiver conectado como `admin`, o usuário conectado deve ser membro do grupo de `administrators` usuários.

Consulte também Agentes [de Replicação no Autor](deploy-communities.md#replication-agents-on-author).
