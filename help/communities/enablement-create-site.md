---
title: Criar um novo site da comunidade para habilitação
seo-title: Criar um novo site da comunidade para habilitação
description: Criar um site da comunidade para ativação
seo-description: Criar um site da comunidade para ativação
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: e9d5a7acad04d841cbc7d62050163f3de998fab6
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 3%

---


# Crie um novo site da comunidade para a ativação {#author-a-new-community-site-for-enablement}

## Criar site da comunidade {#create-community-site}

[A ](/help/communities/sites-console.md) criação do site da comunidade emprega um assistente que o orienta pelas etapas da criação de um site da comunidade. É possível avançar para a etapa `Next` ou `Back` para a etapa anterior antes de confirmar o site na etapa final.

Para começar a criar um novo site da comunidade:

Usando a instância [autor](https://localhost:4502/)

* Faça logon com privilégios de administrador e navegue até **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

* Selecione **Criar**.

### Etapa 1: Modelo do site {#step-site-template}

![modelo de site de ativação](assets/enablement-site-template.png)

Na etapa **Modelo de site**, insira um título, uma descrição, o nome do URL e selecione um modelo de site da comunidade, por exemplo:

* **Título do site da comunidade**: `Enablement Tutorial`.

* **Descrição do site da comunidade**: `A site for enabling the community to learn.`

* **Raiz** do site da comunidade: (deixe em branco para a raiz padrão  `/content/sites`)

* **Configurações** da nuvem: (deixe em branco se nenhuma configuração de nuvem for especificada) forneça o caminho para as configurações de nuvem especificadas.
* **Idioma** base do site da comunidade: (deixe intocado para uma única língua: Inglês) use o menu suspenso para escolher um  *ou* mais idiomas base dos idiomas disponíveis - alemão, italiano, francês, japonês, espanhol, português (Brasil), chinês (tradicional) e chinês (simplificado). Um site da comunidade será criado para cada idioma adicionado e existirá na mesma pasta do site seguindo a melhor prática descrita em [Traduzindo conteúdo para sites multilíngues](/help/sites-administering/translation.md). A página raiz de cada site conterá uma página secundária nomeada pelo código de idioma de um dos idiomas selecionados, como &quot;en&quot; para inglês ou &quot;fr&quot; para francês.

* **Nome do site da comunidade**: `enable`

   * O URL inicial será exibido abaixo do Nome do site da comunidade
   * Para um URL válido, acrescente um código de idioma base + &quot;.html&quot;
      *Por exemplo*, https://localhost:4502/content/sites/  `enable/en.html`

* **Modelo** de site de referência: menu suspenso para escolher  `Reference Structured Learning Site Template`

Selecione **Próximo**.

### Etapa 2: Design {#step-design}

A etapa de design é apresentada em duas seções para selecionar o tema e o banner de marca:

#### TEMA DO SITE DA COMUNIDADE {#community-site-theme}

Selecione o estilo desejado a ser aplicado ao modelo. Quando selecionado, o tema será sobreposto com uma marca de seleção.

#### MARCA DO SITE DA COMUNIDADE {#community-site-branding}

(Opcional) Faça upload de uma imagem de banner para ser exibida nas páginas do site. O banner é fixado na borda esquerda do navegador, entre o cabeçalho e o menu do site da comunidade (links de navegação). A altura do banner é cortada em 120 pixels. Não há redimensionamento do banner para ajustar à largura do navegador e à altura de 120 pixels.

![marca de site1](assets/site-branding1.png)

![marca de site2](assets/site-branding2.png)

Selecione **Próximo**.

### Etapa 3 : Configurações {#step-settings}

Na etapa Configurações, antes de selecionar `Next`, observe que há sete seções fornecendo acesso às configurações que envolvem gerenciamento de usuários, marcação, funções, moderação, análise, tradução e ativação.

#### GERENCIAMENTO DE USUÁRIOS {#user-management}

Recomenda-se que [as comunidades de ativação](/help/communities/overview.md#enablement-community) sejam privadas.

Um site da comunidade é privado quando visitantes anônimos do site têm acesso negado, podem não se inscrever e podem não usar o login social.

Verifique se a maioria das caixas de seleção está desmarcada para [Gerenciamento de usuários](/help/communities/sites-console.md#user-management) :

* NÃO permita que os visitantes do site se registrem automaticamente.
* NÃO permita que visitantes anônimos do site visualizações do site.
* Opcional se permite ou não mensagens entre membros da comunidade.
* NÃO permita logon com o Facebook.
* NÃO permita o logon com o Twitter.

![user-mgmt](assets/user-mgmt.png)

#### MARCANDO {#tagging}

As tags que podem ser aplicadas ao conteúdo da comunidade são controladas selecionando AEM namespaces previamente definidas por meio do [Console de marcação](/help/sites-administering/tags.md#tagging-console) (como [namespace do tutorial](/help/communities/enablement-setup.md#create-tutorial-tags)).

Além disso, selecionar Namespaces de tags para o site da comunidade limita a seleção apresentada ao definir catálogos e recursos de ativação. Consulte [Marcando recursos de ativação](/help/communities/tag-resources.md) para obter informações importantes.

Encontrar namespaces é fácil usando a pesquisa antecipada por tipo. Por exemplo,

* Tipo `tut`
* Selecionar `Tutorial`

![marcação de ativação](assets/enablement-tagging.png)

### ROLES {#roles}

[As ](/help/communities/users.md) funções dos membros da comunidade são atribuídas pelas configurações na seção Funções.

Para permitir que um membro da comunidade (ou grupo de membros) experimente o site como o gerente da comunidade, use a pesquisa de tipo antecipada e selecione o nome do membro ou grupo nas opções no menu suspenso.

Por exemplo,

* Tipo `q`
* Selecione [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[O ](/help/communities/deploy-communities.md#tunnel-service-on-author) serviço de túnel permite a seleção de membros e grupos existentes apenas no ambiente publish.

![funções de ativação](assets/site-admin.png)

#### MODERAÇÃO {#moderation}

Aceite as configurações globais padrão para [moderar](/help/communities/sites-console.md#moderation) conteúdo gerado pelo usuário (UGC).

![moderação1](assets/moderation1.png)

#### ANALYTICS {#analytics}

Na lista suspensa, selecione a estrutura de serviço em nuvem do Analytics configurada para este site da comunidade.

A seleção vista na captura de tela, `Communities`, é o exemplo de estrutura da documentação de configuração [.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![analytics](assets/analytics.png)

#### TRADUÇÃO {#translation}

As [Configurações de tradução](/help/communities/sites-console.md#translation) especificam se o UGC pode ou não ser traduzido e em qual idioma, se assim for.

* Marque **Permitir tradução automática**
* Usar as configurações padrão

![tradução](assets/translation.png)

#### ATIVAÇÃO {#enablement}

Para uma comunidade de ativação, é necessário identificar um ou mais Gerentes de habilitação da comunidade.

* **Gerentes**
 de ativação (obrigatório) Membros do 
`Community Enablement Managers` estão disponíveis para serem selecionados para gerenciar este site da comunidade.

   * Tipo `s`
   * Selecionar `Sirius Nilson`

* **ID**
 de organização do Marketing Cloud (opcional) A ID de uma conta Adobe Analytics que é necessária ao incluir a  [Análise do Video Heartbeat ](/help/communities/analytics.md#video-heartbeat-analytics) no relatórios de ativação.

![capacitação](assets/enablement.png)

Selecione **Próximo**.

### Etapa 4: Criar site da comunidade {#step-create-community-site}

Selecione **Criar.**

![pré-visualização](assets/preview.png)

Quando o processo for concluído, a pasta do novo site será exibida no console Comunidades > Sites.

![enablementsitecreated](assets/enablementsitecreated.png)

### Publicar o novo site da comunidade {#publish-the-new-community-site}

O site criado deve ser gerenciado a partir do console Comunidades - Sites, o mesmo console de onde os novos sites podem ser criados.

Depois de selecionar a pasta do site da comunidade, passe o mouse sobre o ícone do site para que quatro ícones de ação sejam exibidos:

![siteactionicons](assets/siteactionicons.png)

Ao selecionar o ícone de elipses (ícone Mais ações), as opções Exportar site e Excluir site aparecem.

![siteactionsnew](assets/siteactionsnew.png)

Da esquerda para a direita estão:

* **Abrir site**

   Selecione o ícone de lápis para abrir o site da comunidade no modo de edição do autor, para adicionar e/ou configurar componentes da página.

* **Editar site**

   Selecione o ícone de propriedades para abrir o site da comunidade para modificação de propriedades, como o título ou para alterar o tema.

* **Publicar site**

   Selecione o ícone do mundo para publicar o site da comunidade (para localhost:4503 por padrão).

* **Exportar site**

   Selecione o ícone de exportação para criar um pacote do site da comunidade que esteja armazenado em [gerenciador de pacote](/help/sites-administering/package-manager.md) e baixado.
Observe que o UGC não está incluído no pacote do site.

* **Excluir site**

   Para excluir o site da comunidade, selecione o ícone Excluir site que aparece ao passar o mouse sobre o site no console do site Comunidades. Esta ação remove todos os itens associados ao site, como UGC, grupos de usuários, ativos e registros de banco de dados.

   ![ativesiteactions](assets/enablesiteactions.png)

#### Selecione Publicar {#select-publish}

Selecione o ícone do mundo para publicar o site da comunidade.

![site de publicação](assets/publish-site.png)

Haverá uma indicação de que o site foi publicado.

![publicado no site](assets/site-published.png)

## Usuários da comunidade e grupos de usuários {#community-users-user-groups}

### Aviso aos novos grupos de usuários da comunidade {#notice-new-community-user-groups}

Juntamente com o novo site da comunidade, novos grupos de usuários são criados, que têm as permissões apropriadas definidas para várias funções administrativas. Para obter detalhes, visite [Grupos de usuários para sites da comunidade](/help/communities/users.md#usergroupsforcommunitysites).

Para este novo site da comunidade, dado o nome do site &quot;enable&quot; na Etapa 1, os novos grupos de usuários que existem no ambiente de publicação podem ser vistos no [console Membros e grupos das Comunidades](/help/communities/members.md#groups-console):

![community_usergroup](assets/community_usergroup.png)

### Atribuir membros ao grupo Habilitar membros da comunidade {#assign-members-to-community-enable-members-group}

Em autor, com o serviço de túnel ativado, é possível atribuir [usuários criados durante a Configuração Inicial](/help/communities/enablement-setup.md#publishcreateenablementmembers) ao grupo Membros da Comunidade para o site da comunidade recém-criado.

Usando o console Grupos da comunidade, os membros podem ser adicionados individualmente ou adicionados por meio da associação em um grupo.

Neste exemplo, o grupo `Community Ski Class` é adicionado como membro do grupo `Community Enable Members`, bem como membro `Quinn Harper`.

* Navegue até o console **Comunidades, Grupos**
* Selecione o grupo *Membros habilitados da comunidade*
* Digite &#39;ski&#39; na caixa de pesquisa **Adicionar membros ao grupo**
* Selecione *Classe de Esqui da Comunidade* (grupo de alunos)
* Digite &#39;quinn&#39; na caixa de pesquisa
* Selecione *Quinn Harper* (ativação do contato de recursos)

* Selecione **Salvar**

![edit-group-settings](assets/edit-group-settings.png)

## Configurações em Publicar {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enable-login](assets/enablement-login.png)

### Configurar para erro de autenticação {#configure-for-authentication-error}

Depois que um site é configurado e enviado para publicação, [configure o mapeamento de logon](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) na instância de publicação. O benefício é que, quando as credenciais de logon não forem inseridas corretamente, o erro de autenticação exibirá novamente a página de logon do site da comunidade com uma mensagem de erro.

Adicione um `Login Page Mapping` como:

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Opcional) Alterar o Home page padrão {#optional-change-the-default-home-page}

Ao trabalhar com o site de publicação para fins de demonstração, pode ser útil alterar o home page padrão para o novo site.

Para fazer isso, é necessário usar [CRX|DE](https://localhost:4503/crx/de) Lite para editar a tabela [mapeamento de recursos](/help/sites-deploying/resource-mapping.md) na publicação.

Para começar:

1. Ao publicar, acesse o CRXDE e faça logon com privilégios de administrador

   * Por exemplo, navegue até [https://localhost:4503/crx/de](https://localhost:4503/crx/de) e faça logon com `admin/admin`

1. No navegador do projeto, expanda `/etc/map`
1. Selecione o nó `http`

   * Selecione **Criar Nó**

      * **** Namelocalhost.4503

         (do *not* usar &#39;:&#39;)

      * **** [Digitação:Mapeamento](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Com o nó `localhost.4503` recém-criado selecionado

   * Adicionar propriedade

      * **** Nomeação:correspondência
      * **** TypeString
      * **** Valuelocalhost.4503/$

   (deve terminar com o caractere &#39;$&#39;)

   * Adicionar propriedade

      * **** Nomeação:internalRedirect
      * **** TypeString
      * **Valor** /content/sites/enable/en.html


1. Selecione **Salvar tudo**
1. (Opcional) Exclua o histórico de navegação
1. Navegue até https://localhost:4503/

   * Chegar em https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Para desativar, basta anexar o valor da propriedade `sling:match` com um valor &#39;x&#39; - `xlocalhost.4503/$` - e **Salvar tudo**.

![change-default-homepage](assets/change-default-homepage.png)

#### Solução de problemas: Erro ao salvar mapa {#troubleshooting-error-saving-map}

Se não for possível salvar as alterações, verifique se o nome do nó é `localhost.4503`, com um separador &#39;dot&#39; e não `localhost:4503` com um separador &#39;colon&#39;, pois `localhost` não é um prefixo de namespace válido.

![error-map](assets/error-map.png)

#### Solução de problemas: Falha ao redirecionar {#troubleshooting-fail-to-redirect}

O &#39;**$**&#39; no final da cadeia de caracteres de expressão regular `sling:match` é crucial, de modo que apenas `https://localhost:4503/` seja mapeado, caso contrário, o valor de redirecionamento será anexado a qualquer caminho que possa existir após server:port no URL. Dessa forma, quando AEM tentar redirecionar para a página de logon, isso falhará.

## Modificando o Site da Comunidade {#modifying-the-community-site}

Após a criação inicial do site, os autores podem usar o [ícone Abrir site](/help/communities/sites-console.md#authoring-site-content) para executar atividades de criação padrão AEM.

Além disso, os administradores podem usar o [ícone Editar site](/help/communities/sites-console.md#modifying-site-properties) para modificar as propriedades do site, como o título.

Depois de qualquer modificação, lembre-se de **Salvar** e recrie **Publicar** o site.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, visualização a documentação em [manuseio básico](/help/sites-authoring/basic-handling.md) e um [guia rápido para criar páginas](/help/sites-authoring/qg-page-authoring.md).

### Adicionar um catálogo {#add-a-catalog}

O modelo de site da comunidade escolhido para este site da comunidade deve conter o recurso de catálogo.

Caso contrário, a função de catálogo pode ser facilmente adicionada. Isso permitiria que outros membros da comunidade, não atribuídos a recursos de ativação ou a um caminho de aprendizado, selecionassem recursos de ativação de um catálogo.

Se a estrutura do site já contiver o recurso de catálogo, seu Título poderá ser alterado.

Para modificar a estrutura do site, navegue até o console **[!UICONTROL Communities]** > **[!UICONTROL Sites]**, abra a pasta `enable` e selecione o ícone **Editar Site** para acessar as propriedades de `Enablement Tutorial`.

Selecione o painel ESTRUTURA para adicionar um catálogo ou modificar um catálogo existente:

* **Título**: `Ski Catalog`

* **URL**: `catalog`

* **Selecione Todas as Namespaces**: deixe como padrão.

* Selecione **Salvar**.

![modificar a estrutura do site](assets/modify-site-structure.png)

Use o ícone Posição para mover a função Catálogo para a segunda posição, após Atribuições.

![move-Catalog-func](assets/move-catalog-func.png)

Selecione **Salvar** no canto superior direito para salvar as alterações no site da comunidade.

Em seguida, recrie o site **Publish**.

