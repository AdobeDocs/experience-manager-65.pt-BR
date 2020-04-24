---
title: Experimente o site publicado
seo-title: Experimente o site publicado
description: Navegar até um site publicado
seo-description: Navegar até um site publicado
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: 31a3ccc1f9f0940515ed64b1b18a535102bf7231

---


# Experimente o site publicado {#experience-the-published-site}

## Navegue até Novo site na publicação {#browse-to-new-site-on-publish}

Agora que o site de comunidades recém-criado foi publicado, navegue até o URL exibido ao criar o site, mas no servidor de publicação, por exemplo

* A\uthor URL = https://localhost:4502/content/sites/engage/en.html
* URL de publicação = https://localhost:4503/content/sites/engage/en.html

Para minimizar a confusão sobre qual membro está conectado no autor e na publicação, recomenda-se usar navegadores diferentes para cada instância.

Ao chegar ao site publicado pela primeira vez, o visitante do site normalmente não estaria conectado e seria anônimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![chlimage_1-31](assets/chlimage_1-31.png)

## Visitante Anônimo do Site {#anonymous-site-visitor}

Um visitante de site anônimo vê o seguinte na interface do usuário:

* Título do site. Tutorial de introdução
* sem link de perfil
* link de nenhuma mensagem
* link sem notificações
* campo de pesquisa
* Link de logon
* O banner da marca
* Links de menu para os componentes incluídos no Modelo de site de referência

Se você selecionar vários links, eles ficarão no modo somente leitura.

### Impedir acesso anônimo no JCR {#prevent-anonymous-access-on-jcr}

Uma limitação conhecida expõe o conteúdo do site da comunidade a visitantes anônimos por meio de conteúdo jcr e json , embora **permita o acesso** anônimo esteja desabilitado para o conteúdo do site. No entanto, esse comportamento pode ser controlado usando Restrições de Sling como uma solução alternativa.

Para proteger o conteúdo do site da sua comunidade do acesso de usuários anônimos por meio de conteúdo jcr e json , siga estas etapas:

1. Na instância do autor de AEM, vá para https://&lt;host>:&lt;porta>/editor.html/content/site/&lt;sitename>.html.

   >[!NOTE]
   >
   >Não vá para o site localizado.

1. Ir para Propriedades **da** página.

   ![autenticação de site](assets/site-authentication.png)

1. Vá para **guia Avançado **guia.

   ![page-properties](assets/page-properties.png)

1. Enable **Authentication Requirement**.
1. Adicione o caminho da página de logon. Por exemplo,**/content/......./GetStarted**.
1. Publique a página.

## Membro da Comunidade Confiável {#trusted-community-member}

Essa experiência supõe que [Aaron McDonald](/help/communities/tutorials.md#demo-users) tenha recebido as funções de gerente e moderador [da](/help/communities/create-site.md#roles)comunidade. Caso contrário, volte ao ambiente do autor para [modificar as configurações](/help/communities/sites-console.md#modifying-site-properties) do site e selecione Aaron McDonald como gerente da comunidade e moderador.

No canto superior direito, selecione `Log in`e assine com o nome de usuário &quot;aaron.mcdonald@mailinator.com&quot; e a senha &quot;senha&quot;. Observe a capacidade de fazer logon com credenciais do Twitter ou Facebook.

![chlimage_1-32](assets/chlimage_1-32.png)

Depois de fazer logon como membro da comunidade registrado, observe os seguintes itens de menu para clicar e explorar seu site da comunidade:

* **A opção Perfil** permite que você visualização e edite seu perfil.
* [A opção Mensagens](/help/communities/configure-messaging.md) direciona você para a seção de mensagens diretas, onde você pode:

1. Visualização as mensagens diretas recebidas (Caixa de entrada), enviadas (Itens enviados) e excluídas (Lixeira).
1. Componha novas mensagens diretas para enviar a indivíduos e grupos.

* [A opção Notificações](/help/communities/notifications.md) direciona você para a seção Notificações, onde você pode visualização seus eventos de interesse e editar configurações de notificação.
* [A administração](/help/communities/published-site.md#moderationlink) direciona você para a página de moderação do AEM Communities, se você tiver privilégios de moderação.

![chlimage_1-33](assets/chlimage_1-33.png)

Observe que a página Calendário é o home page porque o Modelo de site de referência escolhido incluiu a função Calendário primeiro, seguido pela função Fluxo de Atividade, função Fórum e assim por diante. Esta estrutura é visível do console Modelo [de](/help/communities/sites.md#edit-site-template) site ou ao modificar as propriedades do site no ambiente do autor:

![chlimage_1-34](assets/chlimage_1-34.png)

>[!NOTE]
>
>Para obter mais informações sobre componentes e funções das Comunidades, visite
>
>* [Componentes](/help/communities/author-communities.md) das comunidades (para autores)
>* [Componentes, funções e recursos básicos](/help/communities/essentials.md) (para desenvolvedores)
>



### Link do fórum {#forum-link}

Visualização o recurso básico do fórum selecionando o link do Fórum.

Os membros podem publicar um novo tópico ou seguir um tópico.

Os visitantes do site podem visualização as publicações e classificá-las de várias maneiras.

![chlimage_1-35](assets/chlimage_1-35.png)

### Link de grupos {#groups-link}

Como Aaron é um administrador de grupo, selecionar o link Grupos permitirá que Aaron crie um novo grupo da comunidade selecionando um modelo de grupo, uma imagem, se o grupo estiver aberto ou secreto e convidando os membros.

Este é um exemplo onde um grupo é criado no ambiente publish.

Grupos também podem ser criados no ambiente do autor e gerenciados no site da comunidade no ambiente do autor (o console [Grupos da](/help/communities/groups.md)comunidade). A experiência de [criação de grupos no autor](/help/communities/nested-groups.md) é a seguinte neste tutorial.

![chlimage_1-36](assets/chlimage_1-36.png)

Criar um grupo de referência :

1. selecionar **novo grupo**
1. **Guia Configurações**

   * Nome do grupo : `Sports`
   * Descrição : `A parent group for various sporting groups`
   * Nome do URL do grupo : `sports`
   * selecionar `Open Group` (permitir que qualquer membro da comunidade participe ingressando)

1. **Guia Modelo**

   * selecionar `Reference Group` (contém uma função de grupos em sua estrutura para permitir grupos aninhados)

1. selecionar **Criar grupo**

![chlimage_1-37](assets/chlimage_1-37.png)

Após a criação do novo grupo, **selecione o novo grupo** Esportes para criar dois grupos (aninhados) dentro dele. Como uma estrutura de site não pode começar com a função de grupos, após abrir o grupo Esportes, é necessário selecionar o link Grupos :

![chlimage_1-38](assets/chlimage_1-38.png)

O segundo conjunto de links, começando com `Blog`, pertence ao grupo atualmente selecionado, o `Sports`grupo. Ao selecionar o link Esportes, é possível aninhar dois grupos dentro do grupo Esportes `Groups` .

Como exemplo, adicione dois n `ew groups.`

* um nome `Baseball`

   * deixá-lo definido como `Open Group` (associação obrigatória)
   * na guia Modelos, selecione `Conversational Group`

* um nome `Gymnastics`

   * alterar sua configuração para `Member Only Group` (associação restrita)
   * na guia Modelos, selecione `Conversational Group`

**Aviso **:

* uma atualização da página pode ser necessária antes que ambos os grupos sejam exibidos
* este modelo *não *inclui a função de grupos, portanto, nenhum aninhamento adicional de grupos será possível
* em autor, o console [](/help/communities/groups.md) Grupos oferece uma terceira opção - uma `Public Group` (associação opcional)

Depois que ambos os grupos forem criados, selecione o grupo Beisebol, um grupo aberto e observe seus links:

`Discussions` `What's New` `Members`

Os links do grupo são exibidos abaixo dos links do site principal e resulta na seguinte exibição:

![chlimage_1-39](assets/chlimage_1-39.png)

Autor - com privilégios administrativos, navegue até o console [Grupos de](/help/communities/members.md) comunidades e adicione Weston McCall ao `Community Engage Gymnastics <uid> Members` grupo.

Continuando a publicar, faça logout como Aaron McDonald e visualização os grupos no Sports Group como um visitante anônimo do site :

* do home page
* select `Groups`link
* select `Sports`link
* selecione o `Groups`link Esportes

Somente o grupo Beisebol estará visível.

Faça logon como Weston McCall (weston.mccall@dodgit.com / senha) e navegue até o mesmo local. Note que a Weston é capaz de `Join` abrir o `Baseball` grupo e ou `enter or Leave` o `Gymnastics`grupo privado.

![chlimage_1-40](assets/chlimage_1-40.png)

### Link da página da Web {#web-page-link}

Visualização a página da Web básica incluída no site selecionando o link Página da Web. As ferramentas de criação padrão do AEM podem ser usadas para adicionar conteúdo a esta página no ambiente do autor.

Por exemplo, vá para a instância do **autor** , abra a `engage` pasta no console [Sites](/help/communities/sites-console.md)das Comunidades e selecione o ícone **Abrir site** para entrar no modo de edição do autor. Em seguida, selecione o modo de pré-visualização para selecionar o `Web Page`link e, em seguida, selecione o modo de edição para adicionar componentes de Título e Texto. Por último, publique novamente apenas a página ou o site inteiro.

![chlimage_1-41](assets/chlimage_1-41.png)

### Link de moderação {#moderationlink}

Quando o membro da comunidade tiver privilégios de moderação, o link Moderação ficará visível e sua seleção exibirá o conteúdo da comunidade publicado e permitirá que ele seja [moderado](/help/communities/moderate-ugc.md) de maneira semelhante ao console [de](/help/communities/moderation.md) moderação no ambiente do autor.

Use o botão Voltar do navegador para retornar ao site publicado. A maioria dos consoles não está acessível da navegação global no ambiente publish. [](/help/communities/moderate-ugc.md)

![chlimage_1-42](assets/chlimage_1-42.png)

## Autoinscrição {#self-registration}

Depois de fazer logoff, é possível criar um novo registro de usuário.

* select `Log In`
* select `Sign up for a new account`

![chlimage_1-43](assets/chlimage_1-43.png) ![chlimage_1-44](assets/chlimage_1-44.png)

Por padrão, o endereço de email é a ID de login. Se essa opção estiver desmarcada, o visitante poderá inserir sua própria ID de login (nome de usuário). O nome de usuário deve ser exclusivo no ambiente publish.

Depois de especificar o nome, o email e a senha do usuário, a seleção `Sign Up`criará o usuário e permitirá que ele assine.

Depois de conectado, a primeira página apresentada é a `Profile`página deles, que podem personalizar.

![chlimage_1-45](assets/chlimage_1-45.png)

Se o membro se esquecer da ID de login, será possível recuperar se está usando seu endereço de email.

![chlimage_1-46](assets/chlimage_1-46.png)

