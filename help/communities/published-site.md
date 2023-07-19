---
title: Experimente o site publicado
seo-title: Experience the Published Site
description: Navegar até um site publicado
seo-description: Browse to a published site
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# Experimente o site publicado {#experience-the-published-site}

## Navegar até o novo site em Publicar {#browse-to-new-site-on-publish}

Agora que o site de comunidades recém-criado foi publicado, navegue até o URL exibido ao criar o site, mas no servidor de publicação, por exemplo:

* URL do autor = https://localhost:4502/content/sites/engage/en.html
* URL de publicação = https://localhost:4503/content/sites/engage/en.html

Para minimizar a confusão sobre qual membro está conectado no autor e na publicação, é recomendável usar navegadores diferentes para cada instância.

Ao chegar ao site publicado pela primeira vez, normalmente o visitante do site ainda não estava conectado e era anônimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## Visitante anônimo do site {#anonymous-site-visitor}

Um visitante anônimo do site vê o seguinte na interface do usuário:

* Título do site (Tutorial de introdução)
* Nenhum link de perfil
* Nenhum link de mensagem
* Nenhum link de notificações
* Campo Pesquisa
* Link de login
* O banner da marca
* Links de menu para os componentes incluídos no Modelo de site de referência.

Se selecionar vários links, você os verá no modo somente leitura.

### Impedir acesso anônimo no JCR {#prevent-anonymous-access-on-jcr}

Uma limitação conhecida expõe o conteúdo do site da comunidade para visitantes anônimos por meio do conteúdo jcr e json, embora **permitir acesso anônimo** O está desativado para o conteúdo do site. No entanto, esse comportamento pode ser controlado usando Restrições de Sling como solução alternativa.

Para proteger o conteúdo do site da comunidade do acesso de usuários anônimos por meio de conteúdo jcr e json, siga estas etapas:

1. Na instância do AEM Author, acesse https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Não vá para o site localizado.

1. Ir para **Propriedades da página**.

   ![page-properties](assets/page-properties.png)

1. Ir para **Avançado** guia.

1. Ativar **Requisitos de autenticação**.

   ![autenticação de site](assets/site-authentication.png)

1. Adicione o caminho da página de logon. Por exemplo, **/content/..../GetStarted**.
1. Publique a página.

## Membro de comunidade confiável {#trusted-community-member}

Essa experiência assume que [Aaron McDonald](/help/communities/tutorials.md#demo-users) foi atribuído às funções de [gerente e moderador da comunidade](/help/communities/create-site.md#roles). Caso contrário, retorne ao ambiente de criação para [modificar as configurações do site](/help/communities/sites-console.md#modifying-site-properties) e selecione Aaron McDonald como gerente da comunidade e moderador.

No canto superior direito, selecione `Log in`, e assine com o nome de usuário (aaron.mcdonald@mailinator.com) e a senha (senha). Observe a capacidade de fazer logon com credenciais do Twitter ou da Facebook.

![fazer logon](assets/login.png)

Depois de fazer logon como membro registrado da comunidade, observe os seguintes itens de menu para clicar e explorar seu site da comunidade:

* **Perfil** permite visualizar e editar o perfil.
* [Mensagens](/help/communities/configure-messaging.md) direciona você para a seção de mensagens diretas, onde é possível:

   1. Exibir as mensagens diretas recebidas (Caixa de entrada), enviadas (Itens enviados) e excluídas (Lixeira).
   1. Redija novas mensagens diretas para enviar a indivíduos e grupos.

* [Notificação](/help/communities/notifications.md) A opção direciona você para a seção notificações, onde é possível exibir os eventos de interesse e editar as configurações de notificação.
* [Administração](/help/communities/published-site.md#moderationlink) O direciona você para a página Moderação do AEM Communities, caso tenha privilégios de moderação.

![adminscreen](assets/adminscreen.png)

Observe que a página Calendário é a página inicial porque o Modelo de site de referência escolhido incluiu a função Calendário primeiro, seguido pela função Fluxo de atividades, função Fórum e assim por diante. Essa estrutura é visível do [Modelo do site](/help/communities/sites.md#edit-site-template) ou ao modificar propriedades do site no ambiente de criação:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Para obter mais informações sobre componentes e funções do Communities, visite:
>
>* [Componentes das comunidades](/help/communities/author-communities.md) (para autores)
>* [Fundamentos de componentes, funções e recursos](/help/communities/essentials.md) (para desenvolvedores)

### Link do fórum {#forum-link}

Exiba o recurso básico do fórum selecionando o link Fórum.

Os membros podem postar um novo tópico ou seguir um tópico.

Os visitantes do site podem visualizar publicações e classificá-las de várias maneiras.

![forumlink](assets/forumlink.png)

### Link Grupos {#groups-link}

Como Aaron é um administrador de grupo, selecionar o link Grupos permitirá que Aaron crie um novo grupo da comunidade selecionando um modelo de grupo, imagem, seja o grupo aberto ou secreto, e convidando membros.

Este é um exemplo em que um grupo é criado no ambiente de publicação.

Os grupos também podem ser criados no ambiente de criação e gerenciados no site da comunidade no ambiente de criação ([Console de grupos da comunidade](/help/communities/groups.md)). A experiência do [criação de grupos no autor](/help/communities/nested-groups.md) é o próximo neste tutorial.

![grouplink](assets/grouplink.png)

Criar um grupo de referência:

1. Selecionar **Novo grupo**
1. **Guia Configurações**

   * Nome do grupo : `Sports`
   * Descrição : `A parent group for various sporting groups`.
   * Nome do URL do grupo : `sports`
   * Selecionar `Open Group` (permitir a participação de qualquer membro da comunidade ao ingressar)

1. **Guia Modelo**

   * Selecionar `Reference Group` (contém uma função groups em sua estrutura para permitir grupos aninhados)

1. Selecionar **Criar grupo**

   ![creategroup](assets/creategroup.png)

Depois que um novo grupo for criado, **selecionar o novo grupo Esportes** para criar dois grupos (aninhados) dentro dele. Como uma estrutura de site não pode começar com a função groups, depois de abrir o grupo Sports, é necessário selecionar o link Groups:

![grouplink1](assets/grouplink1.png)

O segundo conjunto de links, começando com `Blog`, pertencer ao grupo selecionado no momento, a variável `Sports` grupo. Ao selecionar as opções de esportes&#39; `Groups` link, é possível aninhar dois grupos no grupo Esportes.

Como exemplo, adicione dois `new groups`.

* Um chamado `Baseball`

   * Deixe-o definido como `Open Group` (associação necessária).
   * Na guia Modelos, selecione `Conversational Group`.

* Um chamado `Gymnastics`

   * Alterar sua configuração para `Member Only Group` (associação restrita).
   * Na guia Modelos, selecione `Conversational Group`.

**Aviso**:

* Pode ser necessário atualizar a página antes que ambos os grupos sejam exibidos.
* Esse modelo não *não* incluir a função groups, portanto, não será possível fazer mais aninhamento de grupos.
* No autor, a variável [Console de grupos](/help/communities/groups.md) fornece uma terceira opção - uma `Public Group` (associação opcional).

Depois que ambos os grupos forem criados, selecione o grupo Beisebol, um grupo aberto e observe seus links:

`Discussions` `What's New` `Members`

Os links do grupo são exibidos abaixo dos links do site principal e resultam na seguinte exibição:

![grouplink2](assets/grouplink2.png)

Na criação - com privilégios administrativos, navegue até o [Console de grupos de comunidades](/help/communities/members.md) e adicione Weston McCall à `Community Engage Gymnastics <uid> Members` grupo.

Continuando a publicar, saia como Aaron McDonald e visualize os grupos no Sports Group como um visitante anônimo do site:

* Da home page
* Selecionar `Groups` link
* Selecionar `Sports` link
* Selecione o &#39;Esportes&#39; `Groups` link

Somente o grupo Beisebol estará visível.

Faça logon como Weston McCall (weston.mccall@dodgit.com / password) e navegue até o mesmo local. Observe que a Weston pode `Join` a abertura `Baseball` agrupar e `enter or Leave` o privado `Gymnastics` grupo.

![grouplink3](assets/grouplink3.png)

### Link da página da Web {#web-page-link}

Exiba a página da Web básica incluída no site selecionando o link Página da Web. As ferramentas de criação padrão do AEM podem ser usadas para adicionar conteúdo a esta página no ambiente de criação.

Por exemplo, vá para **autor** , abra a variável `engage` pasta na [Console de sites das comunidades](/help/communities/sites-console.md), selecione o **Abrir site** ícone para entrar no modo de edição do autor. Em seguida, selecione o modo de visualização para selecionar a `Web Page` e selecione o modo de edição para adicionar os componentes Título e Texto. Por último, publique novamente apenas a página ou todo o site.

![webpagelink](assets/webpagelink.png)

### Link de moderação {#moderationlink}

Quando o membro da comunidade tiver privilégios de moderação, o link Moderação ficará visível e sua seleção exibirá o conteúdo da comunidade publicado e permitirá que ele seja [moderado](/help/communities/moderate-ugc.md) de uma forma semelhante à [console de moderação](/help/communities/moderation.md) no ambiente de criação.

Use o botão Voltar do navegador para retornar ao site publicado. A maioria dos consoles não pode ser acessada a partir da navegação global no ambiente de publicação.

![moderationlink](assets/moderationlink.png)

## Autorregistro {#self-registration}

Depois de fazer logout, é possível criar um novo registro de usuário.

* Selecionar `Log In`
* Selecionar `Sign up for a new account`

![registro](assets/registration.png)

![inscrição](assets/signup.png)

Por padrão, o endereço de email é a ID de logon. Se estiver desmarcada, o visitante poderá inserir sua própria ID de logon (nome de usuário). O nome de usuário deve ser exclusivo no ambiente de publicação.

Depois de especificar o nome do usuário, email e senha, selecione `Sign Up` criará o usuário e permitirá que ele assine.

Depois de fazer logon, a primeira página apresentada é a delas `Profile` página, que eles podem personalizar.

![perfil](assets/profile.png)

Se o membro esquecer sua ID de logon, é possível recuperar o está usando seu endereço de email.

![forgotusername](assets/forgotusername.png)
