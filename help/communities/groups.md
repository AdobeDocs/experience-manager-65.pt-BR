---
title: Console de grupos da comunidade
seo-title: Console de grupos da comunidade
description: O console Grupos permite que você crie grupos da Comunidade
seo-description: O console Grupos permite que você crie grupos da Comunidade
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Console de grupos da comunidade {#community-groups-console}

O console Grupos fornece acesso à criação de grupos da comunidade quando a estrutura [de](/help/communities/sites-console.md#step1) modelo de um site da comunidade inclui a função [de](/help/communities/functions.md#groups-function)grupos.

* O AEM Communities suporta o aninhamento de grupos em outros grupos. O aninhamento de grupo é possível quando a [estrutura do novo grupo](/help/communities/tools-groups.md) contém a função de grupos.
* Somente para o ambiente do autor, há um assistente de criação de grupo semelhante ao assistente de criação de site.
* Se os membros podem ou não criar grupos no ambiente de publicação, é possível configurá-los ao adicionar uma função Grupos a uma estrutura de site da comunidade ou de grupo da comunidade.

Dos três modelos de grupo incluídos, somente o `Reference Group` modelo inclui uma função de grupos em sua estrutura.

As diferentes facetas dos grupos comunitários são:

* **Criação**: novo grupo pode ser criado no autor e, opcionalmente, na instância de publicação.
* **Controle**: grupo pode ser aberto ou secreto.
* **Aninhamento**: grupo pode conter zero ou mais grupos.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>Esse console Grupos, que pode ser acessado somente pelo console Sites das Comunidades, não deve ser confundido com o console [](/help/communities/members.md) Grupos de membros para gerenciar grupos de membros.
>
>Os grupos de membros são grupos de usuários registrados no ambiente publish e acessados a partir do ambiente autor usando o serviço [de](/help/communities/deploy-communities.md#tunnel-service-on-author)túnel.


## Criação do grupo {#group-creation}

Para acessar o console Grupos:

* No autor, faça logon com privilégios de administrador.
* Da navegação global: **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.
* Selecione uma pasta de site da comunidade existente para abri-la.
* Selecione uma instância de um site da comunidade dentro da pasta.

   * A estrutura do site da comunidade deve incluir uma função de grupos.
   * Essas capturas de tela são do tutorial Introdução depois de [criar grupos na publicação](/help/communities/published-site.md).

* Selecione a pasta **** Grupos para abri-la.

   Quando abertos, todos os grupos existentes, sejam criados em autor ou publicação, serão exibidos.

   Desse console Grupos, é possível criar novos grupos.

   ![chlimage_1-200](assets/chlimage_1-200.png)

* Selecione o botão **Criar grupo** .

### Etapa 1: Modelo de grupo da comunidade {#step-community-group-template}

![Grupos comunitários multilíngues](assets/multi-lingual-group.png)

* **Título do grupo da comunidade**

   Um título de exibição para o grupo.
O título aparece no site publicado do grupo.

* **Descrição do grupo da comunidade**

   Uma descrição do grupo.

* **Raiz do grupo da comunidade**

   O caminho raiz para o grupo.
A raiz padrão é o site pai, mas a raiz pode ser movida para qualquer local dentro do site. Não é recomendado alterá-la.

* **Menu Adicionais de Idiomas do Grupo da Comunidade Disponíveis**

   Use a lista suspensa para selecionar os idiomas do grupo da comunidade disponíveis. O menu exibe todos os idiomas nos quais o site da comunidade pai foi criado. Os usuários podem selecionar entre esses idiomas para criar grupos em várias localidades nesta única etapa. O mesmo grupo é criado em vários idiomas especificados no console Grupos dos respectivos sites da comunidade.

* **Nome do grupo da comunidade**

   O nome da página raiz do grupo que aparece no URL.

   * Verifique o nome com o Duplo, pois ele não é facilmente alterado após a criação do grupo.
   * O URL base será exibido abaixo do `Community Group Name`.
   * Para um URL válido, acrescente &quot;.html&quot;
      *por exemplo*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Menu Modelo** de grupo da comunidade

   Use o menu suspenso para escolher um modelo [de grupo da](/help/communities/tools.md)comunidade disponível.

### Etapa 2: Design {#step-design}

### COMMUNITY GROUP THEME {#community-group-theme}

A estrutura usa o [Twitter Bootstrap](https://twitterbootstrap.org/) para trazer um design responsivo e flexível ao site. Um dos muitos temas Bootstrap pré-carregados pode ser selecionado para criar o estilo do modelo de grupo da comunidade selecionado, ou um tema Bootstrap pode ser carregado.

Quando selecionado, o tema será sobreposto com uma marca de seleção azul opaca.

É possível selecionar um tema diferente do tema do site pai.

Depois que o site da comunidade é publicado, é possível [editar as propriedades](#modifyinggroupproperties) e selecionar um tema diferente.

### COMMUNITY GROUP BRANDING {#community-group-branding}

![chlimage_1-201](assets/chlimage_1-201.png)

A marca do site da comunidade é uma imagem exibida como um cabeçalho na parte superior de cada página. É possível exibir um banner para o grupo que difere das outras páginas do site.

A imagem deve ser dimensionada para ser tão larga quanto a exibição esperada da página no navegador e 120 pixels de altura.

Ao criar ou selecionar uma imagem, lembre-se:

* A altura da imagem será recortada para 120 pixels medidos a partir da borda superior da imagem
* A imagem é fixada na borda esquerda da janela do navegador
* Não há redimensionamento da imagem, de modo que, quando a largura da imagem for:

   * Menor que a largura do navegador, a imagem será repetida horizontalmente.
   * Maior que a largura do navegador, a imagem parece estar cortada.

### Etapa 3: Configurações {#step-settings}

**MODERAÇÃO**

![selecionar funções de membro do grupo da comunidade](assets/group-admin.png)

**Moderadores do grupo da comunidade**

Por padrão, a lista de moderadores do site da comunidade pai é herdada.

É possível adicionar moderadores específicos ao grupo. Procurar membros (do ambiente de publicação) para adicioná-los como moderadores

**Agrupar administradores**

Por padrão, o administrador principal do site da comunidade também é o administrador para grupos.

No entanto, é possível atribuir administradores de grupos independentes. Os administradores de grupo podem gerenciar seus grupos (por exemplo, G1) e criar um subgrupo aninhado em G1. Eles podem atribuir administradores diferentes para o subgrupo.

Um usuário U1, portanto, pode ser um administrador em um grupo G1 e um usuário comum em seu grupo aninhado G2.

**ASSOCIAÇÃO**

A configuração de associação permite a seleção de uma das três maneiras de proteger um grupo da comunidade.

![chlimage_1-202](assets/chlimage_1-202.png)

* **Associação opcional**

   Se selecionado, o grupo da comunidade é um grupo público. Os membros do site podem participar do grupo e publicar sem ingressar explicitamente no grupo. O padrão está selecionado.

* **Associação necessária**

   Se selecionado, o grupo da comunidade é um grupo aberto. Os membros do site da comunidade podem visualização o conteúdo do grupo, mas precisam ingressar no grupo para publicar o conteúdo. Os membros ingressam selecionando o `Join` botão no ambiente de publicação. O padrão não está selecionado.

* **Associação restrita**

   Se selecionado, o grupo da comunidade é um grupo secreto. Os membros da Comunidade devem ser expressamente convidados. Os membros convidados são inseridos na caixa de pesquisa. Os membros podem ser adicionados posteriormente usando os consoles [Membros e Grupos](/help/communities/members.md) do ambiente do autor. O padrão não está selecionado.

**MINIATURA**

![chlimage_1-203](assets/chlimage_1-203.png)

A miniatura é uma imagem a ser exibida para o grupo no autor e na publicação.

O tamanho ideal para uma imagem de grupo é de 170 x 90 pixels em um formato de imagem compatível (como JPG ou PNG).

Se nenhuma imagem for adicionada, uma imagem padrão será exibida.

![chlimage_1-204](assets/chlimage_1-204.png)

### Etapa 4: Criar grupo {#step-create-group}

![chlimage_1-205](assets/chlimage_1-205.png)

Se algum ajuste for necessário, use o botão **Voltar **para fazer isso.

Quando **Criar** é selecionado e iniciado, o processo de criação do grupo não pode ser interrompido.

Quando o processo é concluído, o cartão do novo site da subcomunidade (grupo) é exibido no console Grupos de sites das Comunidades, a partir do qual os autores podem adicionar conteúdo de página ou os administradores podem modificar as propriedades do site.

![criar grupo da comunidade](assets/create-community-groups.png)

>[!NOTE]
>
>O grupo é criado em todos os idiomas, conforme especificado na [Etapa 1: Modelo](/help/communities/groups.md#step-community-group-template) de grupo da comunidade em Idiomas adicionais de grupo da comunidade disponíveis, no console Grupos da comunidade dos respectivos sites da comunidade.


## Conteúdo do grupo de autores {#author-group-content}

![chlimage_1-206](assets/chlimage_1-206.png)

O conteúdo da página de um grupo pode ser criado com as mesmas ferramentas de qualquer outra página do AEM. Para abrir o grupo para criação, selecione o ícone Abrir site que aparece ao passar o mouse sobre o cartão de grupo.

## Modificar propriedades do grupo {#modify-group-properties}

As propriedades de um site da subcomunidade existente, especificadas durante o processo de criação do grupo da comunidade, podem ser modificadas selecionando o ícone Editar site que aparece ao passar o mouse sobre o cartão do grupo:

![chlimage_1-207](assets/chlimage_1-207.png)

Os detalhes das seguintes propriedades correspondem às descrições fornecidas na seção Criação de [grupo](#group-creation) . Qualquer grupo aninhado pode ser modificado, independentemente de ser criado no ambiente de publicação ou no ambiente do autor.

![chlimage_1-208](assets/chlimage_1-208.png)

### Modificar básico {#modify-basic}

O painel BASIC permite a modificação de

* Título do grupo da comunidade
* Descrição do grupo da comunidade

O Nome do Grupo da Comunidade não pode ser alterado.

A escolha de um modelo de grupo da comunidade diferente não afetaria um site de grupo da comunidade já que nenhuma conexão permanece entre modelos e sites.

Em vez disso, a [ESTRUTURA](#modify-structure) da subcomunidade pode ser modificada.

### Modificar estrutura {#modify-structure}

O painel ESTRUTURA permite a modificação da estrutura criada inicialmente a partir do modelo de grupo da comunidade selecionado ao criar o site da subcomunidade a partir do ambiente do autor ou da publicação. No painel, é possível:

* Arraste e solte funções [adicionais da](/help/communities/functions.md) comunidade na estrutura do site.
* Em uma instância de uma função da comunidade na estrutura do site:

   * **`Gear icon`**
Edite as configurações, incluindo o título de exibição e o nome do URL*e os grupos [de membros](/help/communities/users.md#privilegedmembersgroups)privilegiados.

   * **`Trashcan icon`**
Remover (excluir) funções da estrutura do site.

   * **`Grid icon`**
Modifique a ordem das funções, conforme exibido na barra de navegação de nível superior do site.

>[!CAUTION]
>
>Embora o título de exibição possa ser alterado sem efeitos colaterais, não é recomendável editar o nome do URL de uma função da comunidade pertencente a um site da comunidade.
>
>Por exemplo, renomear o URL não moverá o UGC existente, com o efeito de &#39;perder&#39; o UGC.


>[!CAUTION]
>
>A função groups não deve *ser a *primeira nem a única* função na estrutura do site.
>
>Qualquer outra função, como a função [de](/help/communities/functions.md#page-function)página, deve ser incluída e listada primeiro.


**Exemplo: Adicionando uma função de calendário a uma estrutura subcomunitária (grupo)**

![chlimage_1-209](assets/chlimage_1-209.png)

### Modificar design {#modify-design}

O painel DESIGN permite a modificação do tema:

* [Tema do grupo da comunidade](#community-group-theme)
* [Marca de grupo da comunidade](#community-group-branding)

   * Role até a parte inferior do painel para alterar a imagem da marca.

### Modificar configurações {#modify-settings}

O painel CONFIGURAÇÕES permite adicionar [moderadores](#moderation)da comunidade.

### Modificar associação {#modify-membership}

O painel [ASSOCIAÇÃO](#membership) é apenas informativo. Não é possível alterar o tipo de associação estabelecida, quer seja opcional, obrigatória ou restrita.

### Modificar miniatura {#modify-thumbnail}

O painel [MINIATURA](#thumbnail) permite que uma imagem seja carregada para representar o grupo da comunidade aos visitantes do site no ambiente de publicação, bem como no console Grupos do site das Comunidades no ambiente do autor.

## Publicar o grupo {#publish-the-group}

![chlimage_1-210](assets/chlimage_1-210.png)

Depois que um grupo da comunidade é recém-criado ou modificado, é possível publicar (ativar) o grupo selecionando o `Publish Site` ícone.

Depois que o grupo for publicado com êxito, uma mensagem será exibida:

![chlimage_1-211](assets/chlimage_1-211.png)

>[!CAUTION]
>
>O site da comunidade pai e os grupos pai já deveriam ter sido publicados.
>
>O site da comunidade e os grupos aninhados devem ser publicados de cima para baixo.


## Excluir o grupo {#delete-the-group}

![ícone excluir]()

Exclua um grupo do console Grupos da comunidade selecionando o ícone Excluir grupo, que aparece ao passar o mouse sobre o grupo.

Isso remove todos os itens associados ao grupo, por exemplo, todo o conteúdo do grupo é permanentemente excluído e as associações de usuários são removidas do sistema.
