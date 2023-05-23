---
title: Criar um novo site da comunidade
seo-title: Author a New Community Site
description: Como criar um novo site do AEM Communities
seo-description: How to author a new AEM Communities site
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# Criar um novo site da comunidade{#author-a-new-community-site}

## Criar um site da comunidade {#create-a-community-site}

Use a instância do autor para criar um site da comunidade. Na instância do autor do AEM:

1. Faça logon com privilégios de administrador.
1. Na navegação global, acesse **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

O console Sites de comunidades fornece um assistente para guiar um usuário pelas etapas de criação de um site de comunidade. É possível avançar para o `Next` etapa ou `Back` à etapa anterior antes de confirmar o site na etapa final.

Para começar a criar um novo site da comunidade:

* Selecione o `Create` botão.

![createcommunitysite](assets/createcommunitysite.png)

### Etapa 1: modelo de site {#step-site-template}

![modelo para criar site](assets/create-site.png)

No [Etapa do modelo de site](/help/communities/sites-console.md#step2013asitetemplate), insira um título, uma descrição, o nome do URL e selecione um modelo de site da comunidade, por exemplo:

* **Título do site da comunidade**: `Getting Started Tutorial`
* **Descrição do site da comunidade**: `A site for engaging with the community.`
* **Raiz do site da comunidade**: (deixe em branco para a raiz padrão) `/content/sites`)
* **Configurações da nuvem**: (deixe em branco se nenhuma configuração de nuvem for especificada) forneça o caminho para as configurações de nuvem especificadas.
* **Idioma base do site da comunidade**: (deixe intocado para um único idioma: inglês) use a lista suspensa para escolher um *ou mais* Idiomas básicos dos idiomas disponíveis: alemão, italiano, francês, japonês, espanhol, português (Brasil), chinês (tradicional) e chinês (simplificado). Um site da comunidade será criado para cada idioma adicionado e existirá na mesma pasta do site, seguindo as práticas recomendadas descritas em [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md). A página raiz de cada site conterá uma página secundária chamada pelo código de idioma de um dos idiomas selecionados, como &quot;en&quot; para inglês ou &quot;fr&quot; para francês.

* **Nome do site da comunidade**: engajamento

   * Verifique novamente o nome, pois ele não pode ser facilmente alterado após a criação do site
   * O URL inicial será exibido abaixo do Nome do site da comunidade
   * Para um URL válido, anexe um código de idioma base + &quot;.html&quot;
   * *Por exemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modelo**: puxe para baixo para escolher `Reference Site`

* Selecione **Próximo**.

### Etapa 2: design {#step-design}

A etapa Design é apresentada em duas seções para selecionar o tema e o banner da marca:

#### TEMA DO SITE DA COMUNIDADE {#community-site-theme}

Selecione o estilo desejado para aplicar ao modelo. Quando selecionado, o tema será sobreposto com uma marca de seleção.

#### MARCA DO SITE DA COMUNIDADE {#community-site-branding}

(Opcional) Faça upload de uma imagem de banner para exibição nas páginas do site. O banner é fixado na borda esquerda do navegador, entre o cabeçalho do site da comunidade e os links de navegação. A altura do banner é cortada para 120 pixels. Não há redimensionamento do banner para ajustá-lo à largura do navegador e à altura de 120 pixels.

![marca de site da comunidade](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Selecione **Próximo**.

### Etapa 3: Configurações {#step-settings}

Na etapa Configurações, antes de selecionar `Next`, observe que há sete seções que fornecem acesso a configurações que envolvem gerenciamento de usuários, marcação, moderação, gerenciamento de grupos, análise e tradução.

#### Gerenciamento de usuários {#user-management}

Marque todas as caixas de seleção para [User Management](/help/communities/sites-console.md#user-management)

* Para permitir que os visitantes do site se registrem
* Para permitir que visitantes do site visualizem o site sem fazer logon
* Para permitir que membros enviem e recebam mensagens de outros membros da comunidade
* Para permitir o logon com o Facebook em vez de registrar e criar um perfil
* Para permitir o logon com o Twitter em vez de registrar e criar um perfil

>[!NOTE]
>
>Para um ambiente de produção, é necessário criar aplicativos Facebook e Twitter personalizados. Consulte [Logon social com a Facebook e o Twitter](/help/communities/social-login.md).

![configurações do site da comunidade](assets/site-settings.png)

#### MARCAÇÃO {#tagging}

As tags que podem ser aplicadas ao conteúdo da comunidade são controladas selecionando namespaces AEM previamente definidos por meio do [Console de marcação](/help/sites-administering/tags.md#tagging-console) (como o [Namespace do tutorial](/help/communities/setup.md#create-tutorial-tags)).

Encontrar namespaces é fácil usando a pesquisa com digitação antecipada. Por exemplo,

* Tipo `tut`
* Selecionar `Tutorial`

![marcação](assets/tagging.png)

#### FUNÇÕES {#roles}

[Funções dos membros da comunidade](/help/communities/users.md) são atribuídas por meio das configurações na seção Funções.

Para permitir que um membro da comunidade (ou grupo de membros) tenha experiência com o site como gerente da comunidade, use a pesquisa com digitação antecipada e selecione o nome do membro ou grupo nas opções da lista suspensa.

Por exemplo,

* Tipo `q`
* Selecione Quinn Harper

>[!NOTE]
>
>[Serviço de túnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) permite a seleção de membros e grupos existentes somente no ambiente de publicação.

![funções de usuário em novo site](assets/site-admin-1.png)

#### MODERAÇÃO {#moderation}

Aceitar as configurações globais padrão para [moderando](/help/communities/sites-console.md#moderation) conteúdo gerado pelo usuário (UGC).

![moderação](assets/moderation1.png)

#### ANALYTICS {#analytics}

Se o Adobe Analytics estiver licenciado e um serviço na nuvem e uma estrutura do Analytics tiverem sido configurados, será possível habilitar o Analytics e selecionar a estrutura.

Consulte [Configuração do Analytics para recursos das comunidades](/help/communities/analytics.md).

![analytics](assets/analytics.png)

#### TRADUÇÃO {#translation}

A variável [Configurações de tradução](/help/communities/sites-console.md#translation) especifique o idioma base do site, bem como se o UGC pode ou não ser traduzido e em qual idioma, se houver.

* Marcar **Permitir tradução automática**
* Deixar os idiomas padrão selecionados para tradução pelo serviço de Tradução automática padrão
* Deixar o provedor e a configuração de tradução padrão
* Não há necessidade de um armazenamento global porque não há cópias de idioma
* Selecionar **Traduzir página inteira**
* Opção Deixar persistência padrão

![configurações de tradução](assets/translation-settings.png)

### Etapa 4: Criar site das comunidades {#step-create-communities-site}

Selecione **Criar.**

![create-site](assets/create-site2.png)

Quando o processo for concluído, a pasta do novo site será exibida no console Comunidades - Sites.

![communitiessitconsole](assets/communitiessitesconsole.png)

## Publicar o site da comunidade {#publish-the-community-site}

O site criado deve ser gerenciado no console Comunidades - Sites, o mesmo console de onde novos sites podem ser criados.

Depois de selecionar a pasta do site da comunidade para abri-lo, passe o mouse sobre o ícone do site, de modo que quatro ícones de ação apareçam:

![siteactionicons-1](assets/siteactionicons-1.png)

Ao selecionar o quarto ícone de reticências (Mais ações), as opções Exportar site e Excluir site são exibidas.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da esquerda para a direita, elas são:

* **Abrir site**

   Selecione o ícone de lápis para abrir o site da comunidade no modo de edição do autor, para adicionar e/ou configurar componentes da página

* **Editar site**

   Selecione o ícone de propriedades para abrir o site da comunidade para modificação de propriedades, como o título ou para alterar o tema

* **Publicar site**

   Selecione o ícone de mundo para publicar o site da comunidade (por exemplo, se o servidor de publicação estiver em execução no computador local e para localhost:4503 por padrão)

* **Exportar site**

   Selecione o ícone de exportação para criar um pacote do site da comunidade que esteja armazenado em [gerenciador de pacotes](/help/sites-administering/package-manager.md) e baixados.
Observe que o UGC não está incluído no pacote do site.

* **Excluir site**

   Selecione o ícone excluir para excluir o site da comunidade de dentro do **[!UICONTROL Console Comunidades > Sites]**. Essa ação remove todos os itens associados ao site, como UGC, grupos de usuários, ativos e registros de banco de dados.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Se não estiver usando a porta padrão 4503 para a instância de publicação, edite o agente de replicação padrão para definir o número da porta com o valor correto.
>
>Na instância do autor, no menu principal:
>
>1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]** menu.
>1. Selecionar **[!UICONTROL Agentes sobre o autor]**.
>1. Selecionar **[!UICONTROL Agente padrão (publicação)]**.
>1. Ao lado de **[!UICONTROL Configurações]**, selecione **[!UICONTROL Editar]**.
>1. Na caixa de diálogo pop-up de Configurações do agente, selecione **[!UICONTROL Transporte]** guia.
>1. No URI, altere o número da porta, 4503, para o número da porta desejado. Por exemplo, para usar a porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Selecionar **[!UICONTROL OK]**.
>1. (Opcional) Selecione **[!UICONTROL Limpar]** ou **[!UICONTROL Forçar nova tentativa]** para redefinir a fila de replicação.


### Selecione Publicar {#select-publish}

Depois de garantir que o servidor de publicação esteja em execução, selecione o ícone do mundo para publicar o site da comunidade.

![site de publicação](assets/publish-site.png)

Quando o site da comunidade for publicado com êxito, uma mensagem será exibida brevemente como &quot;Site publicado&quot;.

### Novos grupos de usuários da comunidade {#new-community-user-groups}

Junto com o novo site da comunidade, novos grupos de usuários são criados e têm as permissões apropriadas definidas para várias funções administrativas. Para obter detalhes, visite [Grupos de usuários para sites de comunidade](/help/communities/users.md#usergroupsforcommunitysites).

Para esse novo site da comunidade, dado o nome de site &quot;engajar&quot; na Etapa 1, os quatro novos grupos de usuários podem ser vistos no [Console de grupos](/help/communities/members.md) (navegação global: Comunidades, Grupos):

* Comunidade Envolver gerentes da comunidade
* Administradores do grupo Community Engage
* Membros do Community Engage
* Moderadores do engajamento da comunidade
* Participação na comunidade Membros privilegiados
* Gerenciador de conteúdo do site Community Engage

Observe que [Aaron McDonald](/help/communities/tutorials.md#demo-users) é membro de

* Comunidade Envolver gerentes da comunidade
* Moderadores do engajamento da comunidade
* Membros da participação da comunidade (indiretamente como membro do grupo Moderadores)

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engajar](assets/engage.png)

## Configurar para erro de autenticação {#configure-for-authentication-error}

Depois que um site é configurado e enviado para publicação, [configurar mapeamento de logon](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) na instância de publicação. A vantagem é que, quando as credenciais de logon não forem inseridas corretamente, o erro de autenticação exibirá novamente a página de logon do site da comunidade com uma mensagem de erro.

Adicionar um `Login Page Mapping` as

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Etapas opcionais {#optional-steps}

### Alterar a página inicial padrão {#change-the-default-home-page}

Ao trabalhar com o site de publicação para fins de demonstração, pode ser útil alterar a página inicial padrão para o novo site.

Para fazer isso, é necessário usar [CRXDE](https://localhost:4503/crx/de) Lite para editar o [mapeamento de recursos](/help/sites-deploying/resource-mapping.md) tabela na publicação.

Para começar:

1. Na instância de publicação, faça logon com privilégios de administrador.
1. Navegue até [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. No navegador do projeto, expanda `/etc/map.`
1. Selecione o `http` nó:

   * Selecionar **Criar nó:**

      * **Nome** localhost.4503 (fazer *não* use &#39;:&#39;)

      * **Tipo** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Com os recém-criados `localhost.4503` nó selecionado:

   * Adicionar propriedade:

   * **Nome** sling:match
      * **Tipo** String
      * **Valor** localhost.4503/$ (deve terminar com o caractere &#39;$&#39;)
   * Adicionar propriedade:

      * **Nome** sling:internalRedirect
      * **Tipo** String
      * **Valor** /content/sites/engage/en.html


1. Selecionar **Salvar tudo.**
1. (Opcional) Exclua o histórico de navegação.
1. Navegue até https://localhost:4503/.

   * Chegar em https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Para desativar, basta adicionar o prefixo `sling:match` valor de propriedade com um &#39;x&#39; - `xlocalhost.4503/$` - e **Salvar tudo**.

![etapas-opcionais](assets/optional-steps.png)

#### Solução de problemas: erro ao salvar o mapa {#troubleshooting-error-saving-map}

Se não for possível salvar as alterações, verifique se o nome do nó é `localhost.4503`, com um separador de &quot;pontos&quot;, e não `localhost:4503` com um separador de &quot;dois pontos&quot;, como `localhost`não é um prefixo de namespace válido.

![error-message](assets/error-message.png)

#### Solução de problemas: falha ao redirecionar {#troubleshooting-fail-to-redirect}

O &#39;**$**&#39; no final da expressão regular `sling:match`a sequência de caracteres é crucial, para que somente `https://localhost:4503/` for mapeado, caso contrário, o valor de redirecionamento receberá um prefixo em qualquer caminho que possa existir após o server:port no URL. Assim, quando o AEM tenta redirecionar para a página de logon, ocorre uma falha.

### Modificar o site {#modify-the-site}

Após a criação inicial do site, os autores poderão usar o [Ícone Abrir site](/help/communities/sites-console.md#authoring-site-content) para realizar atividades padrão de criação de AEM.

Além disso, os administradores podem usar o [Ícone Editar site](/help/communities/sites-console.md#modifying-site-properties) para modificar as propriedades do site, como o título.

Após qualquer modificação, lembre-se de **Salvar** e re-**Publish** no site.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, consulte a documentação em [manuseio básico](/help/sites-authoring/basic-handling.md) e uma [guia rápido para a criação de páginas](/help/sites-authoring/qg-page-authoring.md).
