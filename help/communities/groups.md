---
title: Console de grupos da comunidade
seo-title: Console de grupos da comunidade
description: O console Grupos permite criar grupos da Comunidade
seo-description: O console Grupos permite criar grupos da Comunidade
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 2%

---


# Console de grupos da comunidade {#community-groups-console}

O console Grupos fornece acesso à criação de grupos da comunidade quando a [estrutura de modelo](/help/communities/sites-console.md#step1) de um site da comunidade inclui a [função de grupos](/help/communities/functions.md#groups-function).

* O AEM Communities suporta o aninhamento de grupos em outros grupos. O aninhamento de grupo é possível quando a estrutura [do novo grupo](/help/communities/tools-groups.md) contém a função de grupos.
* Somente para o ambiente de criação, há um assistente de criação de grupo semelhante ao assistente de criação de site.
* Se os membros podem ou não criar grupos no ambiente de publicação, é configurável ao adicionar uma função Grupos a uma estrutura de site da comunidade ou de grupo da comunidade.

Dos três modelos de grupo incluídos, somente o modelo `Reference Group` inclui uma função de grupos em sua estrutura.

As diferentes facetas dos grupos da comunidade são:

* **Criação**: o novo grupo pode ser criado no autor e, opcionalmente, na instância de publicação.
* **Controle**: pode ser aberto ou secreto.
* **Aninhamento**: pode conter zero ou mais grupos.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Esse console Grupos, acessível apenas no console Sites de Comunidades, não deve ser confundido com o [console Grupos](/help/communities/members.md) para gerenciar grupos de membros.
>
>Os grupos de membros são grupos de usuários registrados no ambiente de publicação e acessados do ambiente do autor usando o [serviço de túnel](/help/communities/deploy-communities.md#tunnel-service-on-author).

## Criação do grupo {#group-creation}

Para acessar o console Grupos :

* Ao criar, faça logon com privilégios de administrador.
* Na navegação global: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Selecione uma pasta de site da comunidade existente para abri-la.
* Selecione uma instância de um site da comunidade na pasta .

   * A estrutura do site da comunidade deve incluir uma função de grupos.
   * Essas capturas de tela são do tutorial Introdução após [criar grupos em publicar](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* Selecione a pasta **Groups** para abri-la.

   Quando abertas, todos os grupos existentes, sejam eles criados em autor ou publicação, serão exibidos.

   Nesse console Grupos é possível criar novos grupos.

   ![create-new-group](assets/create-new-group.png)

* Selecione o botão **Criar grupo**.

### Etapa 1: Modelo de grupo da comunidade {#step-community-group-template}

![Grupos da comunidade multilíngue](assets/multi-lingual-group.png)

* **Título do grupo da comunidade**

   Um título de exibição para o grupo.
O título aparece no site publicado do grupo.

* **Descrição do grupo da comunidade**

   Uma descrição do grupo.

* **Raiz do grupo da comunidade**

   O caminho raiz para o grupo.
A raiz padrão é o site principal, mas a raiz pode ser movida para qualquer local dentro do site. Não é recomendável alterá-la.

* **Menu de Idiomas adicionais disponíveis dos grupos da comunidade** 

   Use o menu suspenso para selecionar os idiomas de grupo da comunidade disponíveis. O menu exibe todos os idiomas nos quais o site da comunidade pai é criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.

* **Nome do grupo da comunidade**

   O nome da página raiz do grupo que aparece no URL.

   * Verifique novamente o nome, pois ele não é facilmente alterado depois que o grupo é criado.
   * O URL base será exibido abaixo de `Community Group Name`.
   * Para um URL válido, anexe &quot;.html&quot;
      *por exemplo*,  `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Menu de** modelo do grupo da comunidade

   Use o menu suspenso para escolher um [modelo de grupo da comunidade disponível](/help/communities/tools.md).

### Etapa 2: Design {#step-design}

### TEMA DO GRUPO COMUNITÁRIO {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

A estrutura usa [Bootstrap do Twitter](https://twitterbootstrap.org/) para trazer um design responsivo e flexível para o site. Um dos muitos temas de Bootstrap pré-carregados pode ser selecionado para criar o estilo do modelo de grupo da comunidade selecionado ou um tema de Bootstrap pode ser carregado.

Quando selecionado, o tema será sobreposto com uma marca de verificação azul opaca.

É possível selecionar um tema que difere do tema do site pai.

Depois que o site da comunidade é publicado, é possível [editar as propriedades](#modifyinggroupproperties) e selecionar um tema diferente.

### MARCA DO GRUPO DA COMUNIDADE {#community-group-branding}

![associação de marcas](assets/community-group-branding.png)

A marca do site da comunidade é uma imagem exibida como um cabeçalho na parte superior de cada página. É possível exibir um banner para o grupo que difere de outras páginas do site.

A imagem deve ser dimensionada para ser tão ampla quanto a exibição esperada da página no navegador e 120 pixels de altura.

Ao criar ou selecionar uma imagem, lembre-se:

* A altura da imagem será cortada para 120 pixels medidos a partir da borda superior da imagem
* A imagem é fixada na borda esquerda da janela do navegador
* Não há redimensionamento da imagem, de modo que, quando a largura da imagem for:

   * Menos que a largura do navegador, a imagem se repetirá horizontalmente.
   * Maior que a largura do navegador, a imagem aparecerá cortada.

### Etapa 3: Configurações {#step-settings}

**MODERAÇÃO**

![selecionar funções de membro do grupo da comunidade](assets/group-admin.png)

**Moderadores do grupo da comunidade**

Por padrão, a lista de moderadores do site da comunidade principal é herdada.

É possível adicionar moderadores específicos ao grupo. Pesquise membros (do ambiente de publicação) para adicioná-los como moderadores

**Agrupar administradores**

Por padrão, o administrador principal do site da comunidade também é o administrador de grupos.

No entanto, é possível atribuir administradores de grupos independentes. Os administradores de grupo podem gerenciar seu grupo (por exemplo, G1) e criar um subgrupo aninhado em G1. Eles podem atribuir administradores diferentes para o subgrupo.

Um usuário U1, portanto, pode ser um administrador em um grupo G1 e um usuário comum em seu grupo aninhado G2.

**ASSOCIAÇÃO**

A configuração de associação permite a seleção de uma das três maneiras de proteger um grupo da comunidade.

![comunidade-grupo-associação](assets/community-group-membership.png)

* **Associação opcional**

   Se selecionado, o grupo da comunidade é um grupo público. Os membros do site podem participar do grupo e publicar sem ingressar explicitamente no grupo. O padrão é selecionado.

* **Associação necessária**

   Se selecionado, o grupo da comunidade será um grupo aberto. Os membros do site da comunidade podem visualizar o conteúdo do grupo, mas precisam ingressar no grupo para publicar conteúdo. Os membros se associam selecionando o botão `Join` no ambiente de publicação. O padrão não está selecionado.

* **Associação restrita**

   Se selecionado, o grupo da comunidade é um grupo secreto. Os membros da Comunidade devem ser convidados explicitamente. Os membros convidados são inseridos na caixa de pesquisa. Os membros podem ser adicionados posteriormente usando o [console Membros e grupos](/help/communities/members.md) ambiente do autor. O padrão não está selecionado.

**MINIATURA**

![comunidade-grupo-miniatura](assets/community-group-thumbnail.png)

A miniatura é uma imagem a ser exibida para o grupo na criação e publicação.

O tamanho ideal para uma imagem de grupo é 170 x 90 pixels em um formato de imagem compatível (como JPG ou PNG).

Se nenhuma imagem for adicionada, uma imagem padrão será exibida.

![miniatura-imagem](assets/thumbnail-image.png)

### Etapa 4: Criar grupo {#step-create-group}

![comunidade-criar-grupo](assets/community-create-group.png)

Se algum ajuste for necessário, use o botão **Voltar** para fazer isso.

Depois que **Create** for selecionado e iniciado, o processo de criação do grupo não poderá ser interrompido.

Quando o processo é concluído, o cartão do novo site da subcomunidade (grupo) é exibido no console Grupos de sites das Comunidades , onde os autores podem adicionar conteúdo de página ou os administradores podem modificar as propriedades do site.

![criar grupo da comunidade](assets/create-community-groups.png)

>[!NOTE]
>
>O grupo é criado em todos os idiomas, conforme especificado em [Etapa 1: Modelo de grupo da comunidade](/help/communities/groups.md#step-community-group-template) em Idiomas de grupo da comunidade adicionais disponíveis, no console Grupos da comunidade dos respectivos sites da comunidade.

## Conteúdo do grupo de autores {#author-group-content}

![site aberto](assets/open-site.png)

O conteúdo da página de um grupo pode ser criado com as mesmas ferramentas que qualquer outra página AEM. Para abrir o grupo para criação, selecione o ícone Abrir site que aparece ao passar o mouse sobre o cartão de grupo.

## Modificar Propriedades do Grupo {#modify-group-properties}

As propriedades de um site de subcomunidade existente, especificadas durante o processo de criação do grupo da comunidade, podem ser modificadas ao selecionar o ícone Editar site, que aparece ao passar o mouse sobre o cartão de grupo:

![editar site](assets/edit-site.png)

Os detalhes das seguintes propriedades correspondem às descrições fornecidas na seção [Criação de grupo](#group-creation). Qualquer grupo aninhado pode ser modificado, seja ele criado no ambiente de publicação ou no ambiente de criação.

![comunidade-grupo-básico](assets/community-group-basic.png)

### Modificar Básico {#modify-basic}

O painel BÁSICO permite a modificação de

* Título do grupo da comunidade
* Descrição do grupo da comunidade

O Nome do Grupo da Comunidade não pode ser alterado.

A escolha de um modelo de grupo da comunidade diferente não teria efeito em um site de grupo da comunidade existente, pois nenhuma conexão permanece entre modelos e sites.

Em vez disso, o [STRUCTURE](#modify-structure) da subcomunidade pode ser modificado.

### Modificar estrutura {#modify-structure}

O painel ESTRUTURA permite a modificação da estrutura inicialmente criada a partir do modelo de grupo da comunidade selecionado ao criar o site da subcomunidade a partir do ambiente de criação ou publicação. No painel , é possível:

* Arraste e solte [funções da comunidade](/help/communities/functions.md) adicionais na estrutura do site.
* Em uma instância de uma função da comunidade na estrutura do site:

   * **`Gear icon`**
Edite as configurações, incluindo o título de exibição, o URL e os grupos de membros  [privilegiados](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Remover (excluir) funções da estrutura do site.

   * **`Grid icon`**
Modifique a ordem das funções, conforme exibido na barra de navegação de nível superior do site.

>[!CAUTION]
>
>Embora o título de exibição possa ser alterado sem efeitos colaterais, não é recomendável editar o nome do URL de uma função da comunidade pertencente a um site da comunidade.
>
>Por exemplo, renomear o URL não moverá o UGC existente, tendo o efeito de &#39;perder&#39; o UGC.

>[!CAUTION]
>
>A função de grupos deve *não* ser a *primeira nem a única* função na estrutura do site.
>
>Qualquer outra função, como [page function](/help/communities/functions.md#page-function), deve ser incluída e listada primeiro.

**Exemplo: Adicionar uma função de calendário a uma estrutura de subcomunidade (grupo)**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### Modificar Design {#modify-design}

O painel DESIGN permite a modificação do tema:

* [Tema do grupo da comunidade](#community-group-theme)
* [Marca de grupo da comunidade](#community-group-branding)

   * Role até a parte inferior do painel para alterar a imagem da marca.

### Modificar configurações {#modify-settings}

O painel CONFIGURAÇÕES permite a capacidade de adicionar [moderadores](#moderation) da comunidade.

### Modificar Associação {#modify-membership}

O painel [MEMBERSHIP](#membership) é apenas informativo. Não é possível alterar o tipo de membro do grupo estabelecido, seja ele opcional, obrigatório ou restrito.

### Modificar miniatura {#modify-thumbnail}

O painel [THUMBNAIL](#thumbnail) permite que uma imagem seja carregada para representar o grupo da comunidade para os visitantes do site no ambiente de publicação, bem como no console Grupos do site das Comunidades no ambiente do autor.

## Publicar o grupo {#publish-the-group}

![publicar site](assets/publish-site.png)

Após um grupo da comunidade ter sido criado ou modificado recentemente, é possível publicar (ativar) o grupo selecionando o ícone `Publish Site`.

Depois que o grupo for publicado com êxito, uma mensagem será exibida:

![publicado em grupo](assets/group-published.png)

>[!CAUTION]
>
>O site da comunidade pai e os grupos pai já deveriam ter sido publicados.
>
>O site da comunidade e os grupos aninhados devem ser publicados de cima para baixo.

## Excluir o grupo {#delete-the-group}

![ícone excluir](assets/deleteicon.png)

Exclua um grupo do console Grupos da comunidade selecionando o ícone Excluir grupo , que aparece ao passar o mouse sobre ele.

Isso remove todos os itens associados ao grupo, por exemplo, todo o conteúdo do grupo é excluído permanentemente e as associações de usuário são removidas do sistema.
