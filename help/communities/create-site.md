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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 2%

---

# Criar um novo site da comunidade{#author-a-new-community-site}

## Criar um site de comunidade {#create-a-community-site}

Use a instância do autor para criar um site da comunidade. Na instância do autor do AEM:

1. Faça logon com privilégios de administrador.
1. Na navegação global, acesse **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.

O console Sites das Comunidades fornece um assistente para guiá-lo pelas etapas de criação de um site da comunidade. É possível avançar para a `Next` etapa ou `Back` para a etapa anterior antes de confirmar o site na etapa final.

Para começar a criar um novo site de comunidade:

* Selecione o `Create` botão.

![createcommunitysite](assets/createcommunitysite.png)

### Etapa 1: Modelo do site {#step-site-template}

![modelo para criar site](assets/create-site.png)

No [Etapa do modelo de site](/help/communities/sites-console.md#step2013asitetemplate), insira um título, descrição, o nome do URL e selecione um modelo de site da comunidade, por exemplo:

* **Título do site da comunidade**: `Getting Started Tutorial`
* **Descrição do site da comunidade**: `A site for engaging with the community.`
* **Raiz do site da comunidade**: (deixe em branco para a raiz padrão `/content/sites`)
* **Configurações da nuvem**: (deixe em branco se nenhuma configuração de nuvem for especificada) forneça o caminho para as configurações de nuvem especificadas.
* **Idioma base do site da comunidade**: (deixar intocado para uma única língua: inglês) use a lista suspensa para escolher uma *ou mais* Idiomas de base dos idiomas disponíveis: alemão, italiano, francês, japonês, espanhol, português (Brasil), chinês (tradicional) e chinês (simplificado). Um site da comunidade será criado para cada idioma adicionado e existirá na mesma pasta do site seguindo a prática recomendada descrita em [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md). A página raiz de cada site conterá uma página filho chamada pelo código de idioma de um dos idiomas selecionados, como &quot;en&quot; para inglês ou &quot;fr&quot; para francês.

* **Nome do site da comunidade**: engajamento

   * Verifique novamente o nome, pois ele não é facilmente alterado após a criação do site
   * O URL inicial será exibido abaixo do Nome do site da comunidade
   * Para um URL válido, anexe um código de idioma base + &quot;.html&quot;
   * *Por exemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modelo**: puxe para baixo para escolher `Reference Site`

* Selecione **Próximo**.

### Etapa 2: Design {#step-design}

A etapa Design é apresentada em duas seções para selecionar o tema e o banner de marca:

#### TEMA DO SITE DA COMUNIDADE {#community-site-theme}

Selecione o estilo desejado para aplicar ao modelo. Quando selecionado, o tema será sobreposto com uma marca de seleção.

#### MARCA DO SITE DA COMUNIDADE {#community-site-branding}

(Opcional) Faça upload de uma imagem de banner para exibição nas páginas do site. O banner é fixado na borda esquerda do navegador, entre o cabeçalho do site da comunidade e os links de navegação. A altura do banner é cortada para 120 pixels. Não há redimensionamento do banner para ajustar a largura do navegador e a altura de 120 pixels.

![marca de site da comunidade](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Selecione **Próximo**.

### Etapa 3: Configurações {#step-settings}

Na etapa Configurações , antes de selecionar `Next`, observe que há sete seções que fornecem acesso a configurações envolvendo gerenciamento de usuários, marcação, moderação, gerenciamento de grupos, análise, tradução e ativação.

Visite o [Introdução ao AEM Communities para ativação](/help/communities/getting-started-enablement.md) tutorial para experimentar o trabalho com os recursos de ativação.

#### Gerenciamento de usuários {#user-management}

Marque todas as caixas de seleção para [Gerenciamento de usuários](/help/communities/sites-console.md#user-management)

* Para permitir que os visitantes do site se registrem automaticamente
* Para permitir que os visitantes do site visualizem o site sem fazer logon
* Para permitir que membros enviem e recebam mensagens de outros membros da comunidade
* Para permitir o logon com o Facebook em vez de registrar e criar um perfil
* Para permitir o logon com o Twitter em vez de registrar e criar um perfil

>[!NOTE]
>
>Para um ambiente de produção, é necessário criar aplicativos Facebook e Twitter personalizados. Consulte [Logon no Social com Facebook e Twitter](/help/communities/social-login.md).

![configurações do site da comunidade](assets/site-settings.png)

#### MARCAÇÃO {#tagging}

As tags que podem ser aplicadas ao conteúdo da comunidade são controladas selecionando AEM namespaces definidos anteriormente por meio da variável [Console de marcação](/help/sites-administering/tags.md#tagging-console) (como [Namespace do tutorial](/help/communities/setup.md#create-tutorial-tags)).

Encontrar namespaces é fácil usando a pesquisa antecipada por tipo. Por exemplo,

* Tipo `tut`
* Selecionar `Tutorial`

![marcação](assets/tagging.png)

#### FUNÇÕES {#roles}

[Funções dos membros da comunidade](/help/communities/users.md) são atribuídas pelas configurações na seção Funções .

Para permitir que um membro da comunidade (ou grupo de membros) experiencie o site como o gerente da comunidade, use a pesquisa do tipo para frente e selecione o nome do membro ou grupo nas opções do menu suspenso.

Por exemplo,

* Tipo `q`
* Selecionar [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Serviço de túnel](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) permite a seleção de membros e grupos existentes somente no ambiente de publicação.

![funções de usuário no novo site](assets/site-admin-1.png)

#### MODERAÇÃO {#moderation}

Aceite as configurações globais padrão para [moderação](/help/communities/sites-console.md#moderation) conteúdo gerado pelo usuário (UGC).

![moderação](assets/moderation1.png)

#### ANALYTICS {#analytics}

Se o Adobe Analytics estiver licenciado e um serviço e uma estrutura de nuvem do Analytics tiverem sido configurados, será possível ativar o Analytics e selecionar a estrutura.

Consulte [Configuração do Analytics para recursos das Comunidades](/help/communities/analytics.md).

![analytics](assets/analytics.png)

#### TRADUÇÃO {#translation}

O [Configurações de tradução](/help/communities/sites-console.md#translation) especifique o idioma base do site, bem como se o UGC pode ser traduzido ou não e em qual idioma, se assim for.

* Verificar **Permitir tradução automática**
* Deixe os idiomas padrão selecionados para tradução pelo serviço de Tradução Automática padrão
* Deixar provedor e configuração de tradução padrão
* Não há necessidade de uma loja global porque não há cópias de idioma
* Selecionar **Traduzir página inteira**
* Deixe a opção de persistência padrão

![configurações de tradução](assets/translation-settings.png)

#### ATIVAÇÃO {#enablement}

Deixe em branco ao criar uma comunidade de envolvimento.

Para obter um tutorial semelhante, crie rapidamente um [comunidade de capacitação](/help/communities/overview.md#enablement-community), consulte [Introdução ao AEM Communities para ativação](/help/communities/getting-started-enablement.md).

Selecione **Próximo**.

![ativação](assets/enablement.png)

### Etapa 4: Criar Site de Comunidades {#step-create-communities-site}

Selecione **Criar.**

![criar site](assets/create-site2.png)

Quando o processo for concluído, a pasta do novo site será exibida no console Comunidades - Sites .

![console comunidades](assets/communitiessitesconsole.png)

## Publicar o site da comunidade {#publish-the-community-site}

O site criado deve ser gerenciado no console Comunidades - Sites , o mesmo console de onde novos sites podem ser criados.

Depois de selecionar a pasta do site da comunidade para abri-lo, passe o mouse sobre o ícone do site para que quatro ícones de ação sejam exibidos:

![siteactionicons-1](assets/siteactionicons-1.png)

Ao selecionar o quarto ícone de elipses (Mais ações), as opções Exportar site e Excluir site são exibidas.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da esquerda para a direita, são:

* **Abrir site**

   Selecione o ícone de lápis para abrir o site da comunidade no modo de edição do autor, para adicionar e/ou configurar os componentes da página

* **Editar site**

   Selecione o ícone de propriedades para abrir o site da comunidade para modificação de propriedades, como o título ou para alterar o tema

* **Publicar site**

   Selecione o ícone do mundo para publicar o site da comunidade (por exemplo, se o servidor de publicação estiver em execução no computador local, em seguida, para localhost:4503 por padrão)

* **Exportar site**

   Selecione o ícone de exportação para criar um pacote do site da comunidade que está armazenado em [gerenciador de pacotes](/help/sites-administering/package-manager.md) e baixado.
Observe que o UGC não está incluído no pacote do site.

* **Excluir site**

   Selecione o ícone de exclusão para excluir o site da comunidade de dentro **[!UICONTROL Comunidades > Console Sites]**. Essa ação remove todos os itens associados ao site, como UGC, grupos de usuários, ativos e registros de banco de dados.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Se não estiver usando a porta padrão 4503 para a instância de publicação, edite o agente de replicação padrão para definir o número da porta com o valor correto.
>
>Na instância do autor, no menu principal:
>
>1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]** menu.
>1. Selecionar **[!UICONTROL Agentes do autor]**.
>1. Selecionar **[!UICONTROL Agente padrão (publicar)]**.
>1. Próximo a **[!UICONTROL Configurações]**, selecione **[!UICONTROL Editar]**.
>1. Na caixa de diálogo pop-up Configurações do agente, selecione **[!UICONTROL Transportes]** guia .
>1. No URI, altere o número da porta, 4503, para o número de porta desejado. Por exemplo, para usar a porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Selecionar **[!UICONTROL OK]**.
>1. (Opcional) Selecione **[!UICONTROL Limpar]** ou **[!UICONTROL Forçar nova tentativa]** para redefinir a fila de replicação.


### Selecione Publicar {#select-publish}

Depois de garantir que o servidor de publicação está em execução, selecione o ícone do mundo para publicar o site da comunidade.

![publicar site](assets/publish-site.png)

Quando o site da comunidade tiver sido publicado com sucesso, uma mensagem aparecerá brevemente &quot;Site publicado&quot;.

### Novos grupos de usuários da comunidade {#new-community-user-groups}

Junto com o novo site da comunidade, novos grupos de usuários são criados com as permissões apropriadas definidas para várias funções administrativas. Para obter detalhes, visite [Grupos de usuários para sites da comunidade](/help/communities/users.md#usergroupsforcommunitysites).

Para este novo site da comunidade, dado o nome do site &quot;engajar&quot; na Etapa 1, os quatro novos grupos de usuários podem ser vistos no [Console Grupos](/help/communities/members.md) (navegação global: Comunidades, Grupos):

* Gerentes da Comunidade do Engajamento
* Administradores do Grupo de envolvimento da comunidade
* Membros do Envolvimento da Comunidade
* Moderadores de participação na comunidade
* Membros privilegiados do Community Engage
* Gerente de conteúdo do site de participação da comunidade

Observe que [Aaron McDonald](/help/communities/tutorials.md#demo-users) é membro de

* Gerentes da Comunidade do Engajamento
* Moderadores de participação na comunidade
* Membros do Community Engage (indiretamente como membro do grupo Moderators)

![grupo de usuários](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engajamento](assets/engage.png)

## Configurar para Erro de Autenticação {#configure-for-authentication-error}

Depois que um site é configurado e enviado para publicação, [configurar o mapeamento de logon](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) na instância de publicação. A vantagem é que, quando as credenciais de logon não forem inseridas corretamente, o erro de autenticação exibirá novamente a página de logon do site da comunidade com uma mensagem de erro.

Adicione um `Login Page Mapping` as

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Etapas opcionais {#optional-steps}

### Alterar a página inicial padrão {#change-the-default-home-page}

Ao trabalhar com o site de publicação para fins de demonstração, pode ser útil alterar a página inicial padrão para o novo site.

Para fazer isso, é necessário usar [CRXDE](https://localhost:4503/crx/de) Lite para editar o [mapeamento de recursos](/help/sites-deploying/resource-mapping.md) tabela em publicar.

Para começar:

1. Na instância de publicação, faça logon com privilégios de administrador.
1. Navegue até [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. No navegador do projeto, expanda `/etc/map.`
1. Selecione o `http` nó:

   * Selecionar **Criar nó:**

      * **Nome** localhost.4503 (do *not* use &#39;:&#39;)

      * **Tipo** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Com recém-criado `localhost.4503` nó selecionado:

   * Adicionar propriedade:

   * **Nome** sling:match
      * **Tipo** String
      * **Valor** localhost.4503/$ (deve terminar com &quot;$&quot; char)
   * Adicionar propriedade:

      * **Nome** sling:internalRedirect
      * **Tipo** String
      * **Valor** /content/sites/engage/en.html


1. Selecionar **Salvar tudo.**
1. (Opcional) Exclua o histórico de navegação.
1. Navegue até https://localhost:4503/.

   * Acesse https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Para desativar, basta prefixar a variável `sling:match` valor da propriedade com um &#39;x&#39; - `xlocalhost.4503/$` - e **Salvar tudo**.

![etapas opcionais](assets/optional-steps.png)

#### Solução de problemas: Erro ao salvar o mapa {#troubleshooting-error-saving-map}

Se não conseguir salvar as alterações, verifique se o nome do nó é `localhost.4503`, com um separador de &quot;ponto&quot;, e não `localhost:4503` com um separador de &quot;dois pontos&quot;, como `localhost`não é um prefixo de namespace válido.

![mensagem de erro](assets/error-message.png)

#### Solução de problemas: Falha ao redirecionar {#troubleshooting-fail-to-redirect}

O &quot;**$**&#39; no final da expressão regular `sling:match`é crucial, de modo que somente `https://localhost:4503/` estiver mapeado, caso contrário, o valor de redirecionamento será prefixado em qualquer caminho que possa existir após server:port no URL. Dessa forma, quando o AEM tenta redirecionar para a página de logon, ela falha.

### Modificar o site {#modify-the-site}

Após a criação inicial do site, os autores podem usar a variável [Ícone Abrir site](/help/communities/sites-console.md#authoring-site-content) para executar atividades de criação de AEM padrão.

Além disso, os administradores podem usar o [Ícone Editar site](/help/communities/sites-console.md#modifying-site-properties) para modificar as propriedades do site, como o título.

Depois de qualquer modificação, lembre-se de **Salvar** e re **Publicar** o site.

>[!NOTE]
>
>Se não estiver familiarizado com AEM, visualize a documentação em [tratamento básico](/help/sites-authoring/basic-handling.md) e [guia rápido para a criação de páginas](/help/sites-authoring/qg-page-authoring.md).
