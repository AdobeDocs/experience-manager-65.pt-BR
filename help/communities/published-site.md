---
title: Experimente o site publicado
description: Saiba como navegar até o URL exibido ao criar um site, mas no servidor de publicação.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Experimente o site publicado {#experience-the-published-site}

## Navegar até o novo site no Publish {#browse-to-new-site-on-publish}

Agora que o site de comunidades recém-criado foi publicado, navegue até o URL exibido ao criar o site, mas no servidor de publicação, por exemplo:

* URL do autor = https://localhost:4502/content/sites/engage/en.html
* URL do Publish = https://localhost:4503/content/sites/engage/en.html

Para minimizar a confusão sobre qual membro está conectado no autor e na publicação, é recomendável usar navegadores diferentes para cada instância.

Ao chegar ao site publicado pela primeira vez, em geral, o visitante do site ainda não estaria conectado e seria anônimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## Visitante anônimo do site {#anonymous-site-visitor}

Um visitante anônimo do site vê o seguinte na interface do usuário:

* Título do site (Tutorial de introdução)
* Nenhum link de perfil
* Nenhum link de mensagem
* Nenhum link de notificações
* Campo de pesquisa
* Link de login
* O banner da marca
* Links de menu para os componentes incluídos no Modelo de site de referência.

Se você selecionar vários links, descobrirá que eles estão no modo somente leitura.

### Impedir acesso anônimo no JCR {#prevent-anonymous-access-on-jcr}

Uma limitação conhecida expõe o conteúdo do site da comunidade para visitantes anônimos por meio de conteúdo jcr e json, embora o **permitir acesso anônimo** esteja desabilitado para o conteúdo do site. No entanto, esse comportamento pode ser controlado usando Restrições de Sling como solução alternativa.

Para proteger o conteúdo do site da comunidade do acesso de usuários anônimos por meio de conteúdo jcr e json, siga estas etapas:

1. Na instância do autor do AEM, acesse https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Não vá para o site localizado.

1. Ir para **Propriedades da Página**.

   ![propriedades-página](assets/page-properties.png)

1. Vá para a guia **Avançado**.

1. Habilitar **Requisito de Autenticação**.

   ![autenticação de site](assets/site-authentication.png)

1. Adicione o caminho da página de logon. Por exemplo, **/content/....../GetStarted**.
1. Publish na página.

## Membro de comunidade confiável {#trusted-community-member}

Esta experiência supõe que Aaron McDonald[&#128279;](/help/communities/tutorials.md#demo-users) recebeu as funções de [gerente e moderador da comunidade](/help/communities/create-site.md#roles).  Caso contrário, retorne ao ambiente de criação para [modificar as configurações do site](/help/communities/sites-console.md#modifying-site-properties) e selecione Aaron McDonald como gerente e moderador da comunidade.

No canto superior direito, selecione `Log in` e faça logon com nome de usuário (aaron.mcdonald@mailinator.com) e senha (senha). Observe a capacidade de fazer logon com as credenciais do Twitter ou da Facebook.

![logon](assets/login.png)

Depois de fazer logon como membro registrado da comunidade, observe os seguintes itens de menu para clicar e explorar seu site da comunidade:

* A opção **Perfil** permite exibir e editar seu perfil.
* A opção [Mensagens](/help/communities/configure-messaging.md) direciona você para a seção de mensagens diretas, onde você pode fazer o seguinte:

   1. Exibir as mensagens diretas recebidas (Caixa de entrada), enviadas (Itens enviados) e excluídas (Lixeira).
   1. Redija novas mensagens diretas para enviar a indivíduos e grupos.

* A opção [Notificações](/help/communities/notifications.md) direciona você para a seção de notificações, onde é possível exibir seus eventos de interesse e editar as configurações de notificação.
* A [Administração](/help/communities/published-site.md#moderationlink) direciona você para a Página de moderação do AEM Communities, caso tenha privilégios de moderação.

![adminscreen](assets/adminscreen.png)

Observe que a página Calendário é a página inicial porque o Modelo de site de referência escolhido incluiu a função Calendário primeiro, seguido pela função Fluxo de atividades, função Fórum e assim por diante. Esta estrutura é visível do console [Modelo de Site](/help/communities/sites.md#edit-site-template) ou ao modificar propriedades do site no ambiente de criação:

![modelo de site](assets/sitetemplate.png)

>[!NOTE]
>
>Para obter mais informações sobre componentes e funções do Communities, visite:
>
>* [Componentes das comunidades](/help/communities/author-communities.md) (para autores)
>* [Fundamentos de Componentes, Funções e Recursos](/help/communities/essentials.md) (para desenvolvedores)

### Link do fórum {#forum-link}

Exiba o recurso básico do fórum selecionando o link Fórum.

Os membros podem postar um novo tópico ou seguir um tópico.

Os visitantes do site podem visualizar publicações e classificá-las de várias maneiras.

![forumlink](assets/forumlink.png)

### Link Grupos {#groups-link}

Como Aaron é um administrador de grupo, a seleção do link Grupos permite que Aaron crie um grupo da comunidade selecionando um modelo de grupo, imagem, seja o grupo aberto ou secreto, e convidando membros.

Este é um exemplo em que um grupo é criado no ambiente de publicação.

Grupos também podem ser criados no ambiente de criação e gerenciados no site da comunidade no ambiente de criação ([console Grupos da comunidade](/help/communities/groups.md)). A experiência de [criar grupos no autor](/help/communities/nested-groups.md) é a próxima neste tutorial.

![grouplink](assets/grouplink.png)

Criar um grupo de referência:

1. Selecionar **Novo Grupo**
1. **Guia Configurações**

   * Nome do Grupo: `Sports`
   * Descrição: `A parent group for various sporting groups`.
   * Nome da URL do Grupo: `sports`
   * Selecionar `Open Group` (permitir que qualquer membro da comunidade participe ingressando)

1. **Guia Modelo**

   * Selecionar `Reference Group` (contém uma função de grupos em sua estrutura para permitir grupos aninhados)

1. Selecionar **Criar Grupo**

   ![criargrupoup](assets/creategroup.png)

Depois que o novo grupo for criado, **selecione o novo grupo de esportes** para criar dois grupos (aninhados) dentro dele. Como a estrutura de um site não pode começar com a função groups, depois de abrir o grupo Sports, é necessário selecionar o link Groups:

![grouplink1](assets/grouplink1.png)

O segundo conjunto de links, começando com `Blog`, pertence ao grupo atualmente selecionado, o grupo `Sports`. Ao selecionar o link `Groups` dos Esportes, é possível aninhar dois grupos no grupo Esportes.

Como exemplo, adicione dois `new groups`.

* Um chamado `Baseball`

   * Deixe-o definido como `Open Group` (associação necessária).
   * Na guia Modelos, selecione `Conversational Group`.

* Um chamado `Gymnastics`

   * Altere sua configuração para `Member Only Group` (associação restrita).
   * Na guia Modelos, selecione `Conversational Group`.

**Aviso**:

* Pode ser necessário atualizar a página antes que ambos os grupos sejam exibidos.
* Este modelo *não* inclui a função de grupos, portanto, não é possível fazer mais aninhamento de grupos.
* Na criação, o [console Grupos](/help/communities/groups.md) fornece uma terceira opção: um `Public Group` (associação opcional).

Depois que ambos os grupos forem criados, selecione o grupo Beisebol, um grupo aberto e observe seus links:

`Discussions` `What's New` `Members`

Os links do grupo são exibidos abaixo dos links do site principal e resultam na seguinte exibição:

![grouplink2](assets/grouplink2.png)

Na criação - com privilégios administrativos, navegue até o [console Grupos de Comunidades](/help/communities/members.md) e adicione Weston McCall ao grupo `Community Engage Gymnastics <uid> Members`.

Continuando a publicar, saia como Aaron McDonald e visualize os grupos no Sports Group como um visitante anônimo do site:

* Da home page
* Selecionar link `Groups`
* Selecionar link `Sports`
* Selecione o link de `Groups` dos esportes

Somente o grupo Beisebol é visível.

Faça logon como Weston McCall (weston.mccall@dodgit.com / password) e navegue até o mesmo local. Observe que Weston pode `Join` o grupo `Baseball` aberto e `enter or Leave` o grupo `Gymnastics` privado.

![grouplink3](assets/grouplink3.png)

### Link da página da Web {#web-page-link}

Exiba a página da Web básica incluída no site selecionando o link Página da Web. As ferramentas de criação padrão do AEM podem ser usadas para adicionar conteúdo a esta página no ambiente de criação.

Por exemplo, vá para a instância do **autor**, abra a pasta `engage` no [console Sites de Comunidades](/help/communities/sites-console.md) e selecione o ícone **Abrir Site** para entrar no modo de edição do autor. Em seguida, selecione o modo de visualização para poder selecionar o link `Web Page` e, em seguida, selecione o modo de edição para adicionar componentes de Título e Texto. Por último, publique novamente apenas a página ou todo o site.

![webpagelink](assets/webpagelink.png)

### Link de moderação {#moderationlink}

Quando o membro da comunidade tem privilégios de moderação, o link Moderação fica visível. Selecionar o link exibe o conteúdo da comunidade que é postado e permite que ele seja [moderado](/help/communities/moderate-ugc.md) de uma maneira semelhante ao [console de moderação](/help/communities/moderation.md) no ambiente de criação.

Use o botão Voltar do navegador para retornar ao site publicado. A maioria dos consoles não pode ser acessada a partir da navegação global no ambiente de publicação.

![moderationlink](assets/moderationlink.png)

## Autorregistro {#self-registration}

Depois de fazer logoff, é possível criar um registro de usuário.

* Selecionar `Log In`
* Selecionar `Sign up for a new account`

![registro](assets/registration.png)

![inscrição](assets/signup.png)

Por padrão, o endereço de email é a ID de logon. Se estiver desmarcada, o visitante poderá inserir sua própria ID de logon (nome de usuário). O nome de usuário deve ser exclusivo no ambiente de publicação.

Depois de especificar o nome de usuário, email e senha, selecionar `Sign Up` cria o usuário e habilita-o a assinar.

Depois de entrar, a primeira página apresentada é a `Profile`, que eles podem personalizar.

![perfil](assets/profile.png)

Se o membro esquecer sua ID de logon, é possível recuperar o está usando seu endereço de email.

![forgotusername](assets/forgotusername.png)
