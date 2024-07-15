---
title: Criar um site da comunidade
description: Saiba como criar um site do Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Criar um site da comunidade{#author-a-new-community-site}

## Criar um site da comunidade {#create-a-community-site}

Use a instância do autor para criar um site da comunidade. Na instância do autor AEM:

1. Faça logon com privilégios de administrador.
1. Na navegação global, vá para **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.

O console Sites de comunidades fornece um assistente para guiar um usuário pelas etapas de criação de um site de comunidade. É possível avançar para a etapa `Next` ou `Back` para a etapa anterior antes de confirmar o site na etapa final.

Para começar a criar um site da comunidade:

* Selecione o botão `Create`.

![createcommunitysite](assets/createcommunitysite.png)

### Etapa 1: modelo de site {#step-site-template}

![modelo para criar site](assets/create-site.png)

Na [etapa Modelo de Site](/help/communities/sites-console.md#step2013asitetemplate), insira um título, uma descrição, o nome da URL e selecione um modelo de site de comunidade, por exemplo:

* **Título do site da comunidade**: `Getting Started Tutorial`
* **Descrição do site da comunidade**: `A site for engaging with the community.`
* **Raiz do site da comunidade**: (deixe em branco para a raiz padrão `/content/sites`)
* **Configurações de nuvem**: (deixe em branco se nenhuma configuração de nuvem for especificada) forneça o caminho para as configurações de nuvem especificadas.
* **Idioma Base do Site da Comunidade**: (deixe intocado para um único idioma: inglês) use a lista suspensa para escolher um *ou mais* idiomas base entre os idiomas disponíveis: alemão, italiano, francês, japonês, espanhol, português (Brasil), chinês (tradicional) e chinês (simplificado). Um site da comunidade é criado para cada idioma adicionado e existe na mesma pasta do site, seguindo a prática recomendada descrita em [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md). A página raiz de cada site contém uma página secundária chamada pelo código de idioma de um dos idiomas selecionados, como &quot;en&quot; para inglês ou &quot;fr&quot; para francês.

* **Nome do site da comunidade**: engajamento

   * Verifique novamente o nome, pois ele não pode ser facilmente alterado após a criação do site
   * O URL inicial é exibido abaixo do Nome do site da comunidade
   * Para um URL válido, anexe um código de idioma base + &quot;.html&quot;
   * *Por exemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modelo**: puxe para baixo para escolher `Reference Site`

* Selecione **Próximo**.

### Etapa 2: design {#step-design}

A etapa Design é apresentada em duas seções para selecionar o tema e o banner da marca:

#### TEMA DO SITE DA COMUNIDADE {#community-site-theme}

Selecione o estilo desejado que deseja aplicar ao modelo. Quando selecionado, o tema é sobreposto por uma marca de seleção.

#### MARCA DO SITE DA COMUNIDADE {#community-site-branding}

(Opcional) Faça upload de uma imagem de banner para exibição nas páginas do site. O banner é fixado na borda esquerda do navegador, entre o cabeçalho do site da comunidade e os links de navegação. A altura do banner é cortada para 120 pixels. Não há redimensionamento do banner para ajustá-lo à largura do navegador e à altura de 120 pixels.

![marca-site-comunidade](assets/community-site-branding.png)

![carregar-imagem-site](assets/upload-image-site.png)

Selecione **Próximo**.

### Etapa 3: Configurações {#step-settings}

Na etapa Configurações, antes de selecionar `Next`, há sete seções que fornecem acesso a configurações que envolvem gerenciamento de usuários, marcação, moderação, gerenciamento de grupos, análise e tradução.

#### Gerenciamento de usuários {#user-management}

Marque todas as caixas de seleção para [Gerenciamento de usuários](/help/communities/sites-console.md#user-management)

* Para permitir que os visitantes do site se registrem
* Para permitir que visitantes do site visualizem o site sem fazer logon
* Para permitir que membros enviem e recebam mensagens de outros membros da comunidade
* Para permitir o logon com o Facebook em vez de registrar e criar um perfil
* Para permitir o logon com o Twitter em vez de registrar e criar um perfil

>[!NOTE]
>
>Para um ambiente de produção, é necessário criar aplicativos personalizados do Facebook e do Twitter. Consulte [Logon social com o Facebook e o Twitter](/help/communities/social-login.md).

![configurações do site da comunidade](assets/site-settings.png)

#### MARCAÇÃO {#tagging}

As marcas aplicadas ao conteúdo da comunidade são controladas por meio da seleção de namespaces AEM previamente definidos pelo [Console de Marcação](/help/sites-administering/tags.md#tagging-console) (como o [Namespace do tutorial](/help/communities/setup.md#create-tutorial-tags)).

Encontrar namespaces é fácil usando a pesquisa com digitação antecipada. Por exemplo,

* Tipo `tut`
* Selecionar `Tutorial`

![marcação](assets/tagging.png)

#### FUNÇÕES {#roles}

As [funções de membro da comunidade](/help/communities/users.md) são atribuídas por meio das configurações na seção Funções.

Para permitir que um membro da comunidade (ou grupo de membros) tenha experiência com o site como gerente da comunidade, use a pesquisa com digitação antecipada e selecione o nome do membro ou grupo nas opções da lista suspensa.

Por exemplo,

* Tipo `q`
* Selecione Quinn Harper

>[!NOTE]
>
>O [serviço de túnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) permite a seleção de membros e grupos existentes somente no ambiente de publicação.

![funções de usuário no novo site](assets/site-admin-1.png)

#### MODERAÇÃO {#moderation}

Aceite as configurações globais padrão para [moderação](/help/communities/sites-console.md#moderation) de conteúdo gerado pelo usuário (UGC).

![moderação](assets/moderation1.png)

#### ANALYTICS {#analytics}

Se o Adobe Analytics estiver licenciado e um serviço e uma estrutura do Analytics Cloud tiverem sido configurados, será possível habilitar o Analytics e selecionar a estrutura.

Consulte [Configuração do Analytics para Recursos de Comunidades](/help/communities/analytics.md).

![análises](assets/analytics.png)

#### TRADUÇÃO {#translation}

As [Configurações de tradução](/help/communities/sites-console.md#translation) especificam o idioma base do site e se o UGC pode ser traduzido e para qual idioma, se houver.

* Verificar **Permitir tradução automática**
* Deixar os idiomas padrão selecionados para tradução pelo serviço de Tradução automática padrão
* Deixar o provedor e a configuração de tradução padrão
* Não há necessidade de um armazenamento global porque não há cópias de idioma
* Selecione **Traduzir página inteira**
* Opção Deixar persistência padrão

![configurações-tradução](assets/translation-settings.png)

### Etapa 4: Criar site das comunidades {#step-create-communities-site}

Selecione **Criar.**

![criar-site](assets/create-site2.png)

Quando o processo for concluído, a pasta do novo site será exibida no console Comunidades - Sites.

![communitiessitconsole](assets/communitiessitesconsole.png)

## Publish no site da comunidade {#publish-the-community-site}

O site criado deve ser gerenciado no console Comunidades - Sites, o mesmo console de onde novos sites podem ser criados.

Depois de selecionar a pasta do site da comunidade para abri-lo, passe o mouse sobre o ícone do site, de modo que quatro ícones de ação apareçam:

![siteactionicons-1](assets/siteactionicons-1.png)

Ao selecionar o quarto ícone de reticências (Mais ações), as opções Exportar site e Excluir site são exibidas.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da esquerda para a direita, elas são:

* **Abrir Site**

  Selecionar o ícone de lápis abre o site da comunidade no modo de edição do autor, onde você pode adicionar ou configurar componentes da página.

* **Editar Site**

  Selecionar o ícone de propriedades abre o site da comunidade para a modificação de propriedades, como o título ou para alterar o tema.

* **Site do Publish**

  Selecionar o ícone do mundo publica o site da comunidade (por exemplo, se o servidor de publicação estiver em execução no computador local, em seguida, para localhost:4503 por padrão).

* **Exportar Site**

  Selecionar o ícone de exportação cria um pacote do site da comunidade que é armazenado no [Gerenciador de Pacotes](/help/sites-administering/package-manager.md) e baixado. O UGC não está incluído no pacote do site.

* **Excluir Site**

  Selecionar o ícone excluir exclui o site da comunidade de **[!UICONTROL Communities > console Sites]**. Essa ação remove todos os itens associados ao site, como UGC, grupos de usuários, ativos e registros de banco de dados.

![ações do site](assets/siteactions.png)

>[!NOTE]
>
>Se não estiver usando a porta padrão 4503 para a instância de publicação, edite o agente de replicação padrão para definir o número da porta com o valor correto.
>
>Na instância do autor, no menu principal:
>
>1. Navegue até o menu **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
>1. Selecione **[!UICONTROL Agentes no autor]**.
>1. Selecione **[!UICONTROL Agente Padrão (publicação)]**.
>1. Ao lado de **[!UICONTROL Configurações]**, selecione **[!UICONTROL Editar]**.
>1. Na caixa de diálogo pop-up de Configurações do agente, selecione a guia **[!UICONTROL Transporte]**.
>1. No URI, altere o número da porta, 4503, para o número da porta desejado. Por exemplo, para usar a porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Selecione **[!UICONTROL OK]**.
>1. (Opcional) Selecione **[!UICONTROL Limpar]** ou **[!UICONTROL Forçar Repetição]** para redefinir a fila de replicação.

### Selecionar Publish {#select-publish}

Depois de garantir que o servidor de publicação esteja em execução, selecione o ícone do mundo para publicar o site da comunidade.

![publicar-site](assets/publish-site.png)

Quando o site da comunidade for publicado com êxito, uma mensagem será exibida brevemente como &quot;Site publicado&quot;.

### Novos grupos de usuários da comunidade {#new-community-user-groups}

Junto com o novo site da comunidade, novos grupos de usuários são criados e têm as permissões apropriadas definidas para várias funções administrativas. Para obter detalhes, visite [Grupos de usuários para Sites de comunidade](/help/communities/users.md#usergroupsforcommunitysites).

Para este novo site da comunidade, dado o nome de site &quot;engage&quot; na Etapa 1, os quatro novos grupos de usuários podem ser vistos no [console Grupos](/help/communities/members.md) (navegação global: Comunidades, Grupos):

* Comunidade Envolver gerentes da comunidade
* Administradores do grupo Community Engage
* Membros do Community Engage
* Moderadores do engajamento da comunidade
* Participação na comunidade Membros privilegiados
* Gerenciador de conteúdo do site Community Engage

[Aaron McDonald](/help/communities/tutorials.md#demo-users) é um membro de

* Comunidade Envolver gerentes da comunidade
* Moderadores do engajamento da comunidade
* Membros da participação da comunidade (indiretamente como membro do grupo Moderadores)

![grupo-usuário](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engajamento](assets/engage.png)

## Configurar para erro de autenticação {#configure-for-authentication-error}

Depois que um site for configurado e enviado por push para publicação, [configure o log no mapeamento](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) na instância de publicação. O benefício é que, quando as credenciais de logon não são inseridas corretamente, o erro de autenticação reexibe a página de logon do site da comunidade com uma mensagem de erro.

Adicionar um `Login Page Mapping` como

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Etapas opcionais {#optional-steps}

### Alterar a página inicial padrão {#change-the-default-home-page}

Ao trabalhar com o site de publicação para fins de demonstração, pode ser útil alterar a página inicial padrão para o novo site.

Para fazer isso, é necessário usar o [CRXDE](https://localhost:4503/crx/de) Lite para editar a tabela [resource-mapping](/help/sites-deploying/resource-mapping.md) na publicação.

Para começar:

1. Na instância de publicação, faça logon com privilégios de administrador.
1. Navegue até [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. No navegador do projeto, expanda `/etc/map.`
1. Selecione o nó `http`:

   * Selecionar **Criar Nó:**

      * **Nome** localhost.4503
(faça *não* usar &#39;:&#39;)

      * **Tipo** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Com o nó `localhost.4503` recém-criado selecionado:

   * Adicionar propriedade:

   * sling:match de **Name**
      * Cadeia de Caracteres **Type**
      * **Valor** localhost.4503/$
(deve terminar com o caractere &#39;$&#39;)

   * Adicionar propriedade:

      * **Name** sling:internalRedirect
      * Cadeia de Caracteres **Type**
      * **Valor** /content/sites/engage/en.html

1. Selecione **Salvar tudo.**
1. (Opcional) Exclua o histórico de navegação.
1. Navegue até https://localhost:4503/.

   * Chegar em https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Para desabilitar, basta adicionar um prefixo &#39;x&#39; ao valor da propriedade `sling:match` - `xlocalhost.4503/$` - e **Salvar Tudo**.

![etapas-opcionais](assets/optional-steps.png)

#### Solução de problemas: erro ao salvar o mapa {#troubleshooting-error-saving-map}

Se não for possível salvar as alterações, verifique se o nome do nó é `localhost.4503`, com um separador de &quot;pontos&quot;, e não `localhost:4503` com um separador de &quot;dois pontos&quot;, pois `localhost` não é um prefixo de namespace válido.

![mensagem-erro](assets/error-message.png)

#### Solução de problemas: falha ao redirecionar {#troubleshooting-fail-to-redirect}

O &#39;**$**&#39; no final da cadeia de caracteres da expressão regular `sling:match` é crucial, para que somente `https://localhost:4503/` seja mapeado, caso contrário, o valor de redirecionamento será prefixado a qualquer caminho que possa existir após server:port na URL. Portanto, quando o AEM tenta redirecionar para a página de logon, ocorre uma falha.

### Modificar o site {#modify-the-site}

Após a criação inicial do site, os autores poderão usar o [ícone Abrir site](/help/communities/sites-console.md#authoring-site-content) para realizar atividades padrão de criação de AEM.

Além disso, os administradores podem usar o [ícone Editar Site](/help/communities/sites-console.md#modifying-site-properties) para modificar propriedades do site, como o título.

Após qualquer modificação, lembre-se de **Salvar** e refazer **Publish** o site.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, exiba a documentação sobre [manuseio básico](/help/sites-authoring/basic-handling.md) e um [guia rápido para a criação de páginas](/help/sites-authoring/qg-page-authoring.md).
