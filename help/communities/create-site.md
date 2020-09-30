---
title: Criar um novo site da comunidade
seo-title: Criar um novo site da comunidade
description: Como criar um novo site do AEM Communities
seo-description: Como criar um novo site do AEM Communities
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 99fb808013da18ed028d59c43deab5e815169e26
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---


# Criar um novo site da comunidade{#author-a-new-community-site}

## Criar um site da comunidade {#create-a-community-site}

Use a instância do autor para criar um site da comunidade. Na instância do autor de AEM:

1. Faça logon com privilégios de administrador.
1. Na navegação global, vá para **[!UICONTROL Comunidades]** > **[!UICONTROL Sites]**.

O console Sites das Comunidades fornece um assistente para guiá-lo pelas etapas de criação de um site da comunidade. É possível avançar para a etapa `Next` ou `Back` para a etapa anterior antes de confirmar o site na etapa final.

Para começar a criar um novo site da comunidade:

* Selecione o `Create` botão.

![createcommunitysite](assets/createcommunitysite.png)

### Etapa 1: Modelo de site {#step-site-template}

![modelo para criar o site](assets/create-site.png)

Na etapa [Modelo de](/help/communities/sites-console.md#step2013asitetemplate)site, insira um título, descrição, o nome do URL e selecione um modelo de site da comunidade, por exemplo:

* **Título do site da comunidade**: `Getting Started Tutorial`
* **Descrição do site da comunidade**: `A site for engaging with the community.`
* **Raiz** do site da comunidade: (deixe em branco para a raiz padrão `/content/sites`)
* **Configurações** da nuvem: (deixe em branco se nenhuma configuração de nuvem for especificada) forneça o caminho para as configurações de nuvem especificadas.
* **Idioma** base do site da comunidade: (deixe intocado para uma única língua: Inglês) use a lista suspensa para escolher um *ou mais* idiomas básicos dos idiomas disponíveis - alemão, italiano, francês, japonês, espanhol, português (Brasil), chinês (tradicional) e chinês (simplificado). Um site da comunidade será criado para cada idioma adicionado e existirá dentro da mesma pasta do site, seguindo as práticas recomendadas descritas em [Translating Content for Multilingual Sites](/help/sites-administering/translation.md). A página raiz de cada site conterá uma página secundária nomeada pelo código de idioma de um dos idiomas selecionados, como &quot;en&quot; para inglês ou &quot;fr&quot; para francês.

* **Nome** do site da comunidade: engajamento

   * Verifique o nome pelo duplo, pois ele não é facilmente alterado depois que o site é criado
   * O URL inicial será exibido abaixo do Nome do site da comunidade
   * Para um URL válido, acrescente um código de idioma base + &quot;.html&quot;
   * *Por exemplo*, https://localhost:4502/content/sites/ `engage/en.html`

* **Modelo**: menu suspenso para escolher `Reference Site`

* Selecione **Próximo**.

### Etapa 2: Design {#step-design}

A etapa de design é apresentada em duas seções para selecionar o tema e o banner de marca:

#### COMMUNITY SITE THEME {#community-site-theme}

Selecione o estilo desejado a ser aplicado ao modelo. Quando selecionado, o tema será sobreposto com uma marca de seleção.

#### COMMUNITY SITE BRANDING {#community-site-branding}

(Opcional) Faça upload de uma imagem de banner para ser exibida nas páginas do site. O banner é fixado na borda esquerda do navegador, entre o cabeçalho do site da comunidade e os links de navegação. A altura do banner é cortada em 120 pixels. Não há redimensionamento do banner para ajustar à largura do navegador e à altura de 120 pixels.

![marca do site da comunidade](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Selecione **Próximo**.

### Etapa 3: Configurações {#step-settings}

Na etapa Configurações, antes de selecionar `Next`, observe que há sete seções que fornecem acesso a configurações que envolvem gerenciamento de usuários, marcação, moderação, gerenciamento de grupos, análise, tradução e ativação.

Visite o tutorial [Introdução ao AEM Communities para ativar](/help/communities/getting-started-enablement.md) e experimente trabalhar com os recursos de ativação.

#### Gerenciamento de usuários {#user-management}

Marque todas as caixas de seleção para Gerenciamento de [usuários](/help/communities/sites-console.md#user-management)

* Para permitir que os visitantes do site se registrem automaticamente
* Para permitir que visitantes do site visualizações do site sem fazer logon
* Para permitir que membros enviem e recebam mensagens de outros membros da comunidade
* Para permitir o logon com o Facebook em vez de registrar e criar um perfil
* Para permitir o logon no Twitter em vez de registrar e criar um perfil

>[!NOTE]
>
>Para um ambiente de produção, é necessário criar aplicativos personalizados do Facebook e do Twitter. Consulte Logon [social com Facebook e Twitter](/help/communities/social-login.md).


![configurações do site da comunidade](assets/site-settings.png)

#### TAGGING {#tagging}

As tags que podem ser aplicadas ao conteúdo da comunidade são controladas selecionando AEM namespaces previamente definidas por meio do Console [de](/help/sites-administering/tags.md#tagging-console) marcação (como a namespace [do](/help/communities/setup.md#create-tutorial-tags)tutorial).

Encontrar namespaces é fácil usando a pesquisa antecipada por tipo. Por exemplo,

* Tipo `tut`
* Selecionar `Tutorial`

![marcação](assets/tagging.png)

#### ROLES {#roles}

[As funções](/help/communities/users.md) de membro da comunidade são atribuídas por meio das configurações na seção Funções.

Para permitir que um membro da comunidade (ou grupo de membros) experimente o site como o gerente da comunidade, use a pesquisa de tipo antecipada e selecione o nome do membro ou grupo nas opções no menu suspenso.

Por exemplo,

* Tipo `q`
* Selecione [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[O serviço](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) de túnel permite a seleção de membros e grupos existentes somente no ambiente publish.


![funções de usuário no novo site](assets/site-admin-1.png)

#### MODERATION {#moderation}

Aceite as configurações globais padrão para [moderar](/help/communities/sites-console.md#moderation) o conteúdo gerado pelo usuário (UGC).

![moderação](assets/moderation1.png)

#### ANALYTICS {#analytics}

Se a Adobe Analytics estiver licenciada e um serviço e uma estrutura em nuvem do Analytics tiverem sido configurados, será possível habilitar o Analytics e selecionar a estrutura.

Consulte Configuração [do Analytics para recursos](/help/communities/analytics.md)de comunidades.

![analytics](assets/analytics.png)

#### TRANSLATION {#translation}

As configurações [de](/help/communities/sites-console.md#translation) Tradução especificam o idioma base do site, bem como se o UGC pode ou não ser traduzido e para qual idioma, se houver.

* Verifique **Permitir tradução automática**
* Deixe os idiomas padrão selecionados para tradução pelo serviço padrão de Tradução Automática
* Deixe o provedor de tradução e a configuração padrão
* Não há necessidade de uma loja global porque não há cópias de idioma
* Selecione **Traduzir a página inteira**
* Deixe a opção de persistência padrão

![configurações de tradução](assets/translation-settings.png)

#### ENABLEMENT {#enablement}

Deixe em branco ao criar uma comunidade de envolvimento.

Para obter um tutorial semelhante para criar rapidamente uma comunidade [de](/help/communities/overview.md#enablement-community)ativação, consulte [Introdução à AEM Communities para Ativação](/help/communities/getting-started-enablement.md).

Selecione **Próximo**.

![capacitação](assets/enablement.png)

### Etapa 4: Criar site de comunidades {#step-create-communities-site}

Selecione **Criar.**

![create-site](assets/create-site2.png)

Quando o processo for concluído, a pasta do novo site será exibida no console Comunidades - Sites.

![communitiesitesconsole](assets/communitiessitesconsole.png)

## Publicar o site da comunidade {#publish-the-community-site}

O site criado deve ser gerenciado a partir do console Comunidades - Sites, o mesmo console de onde os novos sites podem ser criados.

Depois de selecionar a pasta do site da comunidade para abri-la, passe o mouse sobre o ícone do site para que quatro ícones de ação sejam exibidos:

![siteactionicons-1](assets/siteactionicons-1.png)

Ao selecionar o quarto ícone de elipses (Mais ações), as opções Exportar site e Excluir site são exibidas.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da esquerda para a direita estão:

* **Abrir site**

   Selecione o ícone de lápis para abrir o site da comunidade no modo de edição do autor, para adicionar e/ou configurar componentes da página

* **Editar site**

   Selecione o ícone de propriedades para abrir o site da comunidade para modificação de propriedades, como o título ou para alterar o tema

* **Publicar site**

   Selecione o ícone do mundo para publicar o site da comunidade (por exemplo, se o servidor de publicação estiver sendo executado em sua máquina local, em seguida, para localhost:4503 por padrão)

* **Exportar site**

   Selecione o ícone de exportação para criar um pacote do site da comunidade que esteja armazenado no gerenciador [de](/help/sites-administering/package-manager.md) pacotes e baixado.
Observe que o UGC não está incluído no pacote do site.

* **Excluir site**

   Selecione o ícone Excluir para excluir o site da comunidade no console **[!UICONTROL Comunidades > Sites]**. Esta ação remove todos os itens associados ao site, como UGC, grupos de usuários, ativos e registros de banco de dados.

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>Se não estiver usando a porta padrão 4503 para a instância de publicação, edite o agente de replicação padrão para definir o número da porta com o valor correto.
>
>Na instância do autor, no menu principal:
>
>1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > menu **[!UICONTROL Replicação]** .
>1. Selecione **[!UICONTROL Agentes no autor]**.
>1. Selecione Agente **[!UICONTROL padrão (publicar)]**.
>1. Ao lado de **[!UICONTROL Configurações]**, selecione **[!UICONTROL Editar]**.
>1. Na caixa de diálogo pop-up para Configurações do agente, selecione a guia **[!UICONTROL Transporte]** .
>1. No URI, altere o número da porta, 4503, para o número da porta desejado. Por exemplo, para usar a porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Selecione **[!UICONTROL OK]**.
>1. (Opcional) Selecione **[!UICONTROL Limpar]** ou **[!UICONTROL Forçar nova tentativa]** para redefinir a fila de replicação.

>



### Selecione Publicar {#select-publish}

Depois de garantir que o servidor de publicação esteja em execução, selecione o ícone mundial para publicar o site da comunidade.

![site de publicação](assets/publish-site.png)

Quando o site da comunidade for publicado com êxito, uma mensagem será exibida brevemente como &#39;Site publicado&#39;.

### Novos grupos de usuários da comunidade {#new-community-user-groups}

Juntamente com o novo site da comunidade, novos grupos de usuários são criados, que têm as permissões apropriadas definidas para várias funções administrativas. Para obter detalhes, visite Grupos de [usuários para sites](/help/communities/users.md#usergroupsforcommunitysites)da comunidade.

Para este novo site da comunidade, dado o nome do site &quot;engajar&quot; na Etapa 1, os quatro novos grupos de usuários podem ser vistos no console [](/help/communities/members.md) Grupos (navegação global: Comunidades, Grupos):

* Gerentes comunitários envolvidos
* Administradores do Grupo de envolvimento da comunidade
* Membros de participação da comunidade
* Moderadores de envolvimento da comunidade
* Membros privilegiados do Community Engage
* Gerente de conteúdo do Site de participação da comunidade

Observe que [Aaron McDonald](/help/communities/tutorials.md#demo-users) é membro do

* Gerentes comunitários envolvidos
* Moderadores de envolvimento da comunidade
* Membros participantes da comunidade (indiretamente como membro do grupo Moderadores)

![grupo de usuários](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engajamento](assets/engage.png)

## Erro ao configurar para autenticação {#configure-for-authentication-error}

Depois que um site é configurado e enviado para publicação, [configure o mapeamento](/help/communities/sites-console.md#configure-for-authentication-error) de logon ( `Adobe Granite Login Selector Authentication Handler`) na instância de publicação. O benefício é que, quando as credenciais de logon não forem inseridas corretamente, o erro de autenticação exibirá novamente a página de logon do site da comunidade com uma mensagem de erro.

Adicionar um `Login Page Mapping` como

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Etapas opcionais {#optional-steps}

### Alterar o Home page padrão {#change-the-default-home-page}

Ao trabalhar com o site de publicação para fins de demonstração, pode ser útil alterar o home page padrão para o novo site.

Para fazer isso, é necessário usar o [CRXDE](https://localhost:4503/crx/de) Lite para editar a tabela de mapeamento [de](/help/sites-deploying/resource-mapping.md) recursos na publicação.

Para começar:

1. Na instância de publicação, faça logon com privilégios de administrador.
1. Navegue até [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. No navegador do projeto, expanda `/etc/map.`
1. Selecione o `http` nó:

   * Selecione **Criar nó:**

      * **Nome** localhost.4503( *não* use &#39;:&#39;)

      * **Tipo** [sling:Mapeamento](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Com o `localhost.4503` nó recém-criado selecionado:

   * Adicionar propriedade:

   * **Seleção de nome** :correspondência
      * **String de tipo**
      * **Valor** localhost.4503/$(deve terminar com o caractere &#39;$&#39;)
   * Adicionar propriedade:

      * **Nomear** sling:internalRedirect
      * **String de tipo**
      * **Valor** /content/sites/engage/en.html


1. Selecione **Salvar tudo.**
1. (Opcional) Exclua o histórico de navegação.
1. Navegue até https://localhost:4503/.

   * Chegar em https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Para desativar, basta prefixar o valor da `sling:match` propriedade com um &quot;x&quot; - `xlocalhost.4503/$` - e **Salvar tudo**.


![etapas opcionais](assets/optional-steps.png)

#### Solução de problemas: Erro ao salvar mapa {#troubleshooting-error-saving-map}

Se não for possível salvar as alterações, verifique se o nome do nó é `localhost.4503`, com um separador &quot;ponto&quot; e não `localhost:4503` com um separador &quot;dois pontos&quot;, pois não `localhost`é um prefixo de namespace válido.

![error-message](assets/error-message.png)

#### Solução de problemas: Falha ao redirecionar {#troubleshooting-fail-to-redirect}

O &quot;**$**&quot; no final da `sling:match`string de expressão regular é crucial, de modo que apenas `https://localhost:4503/` seja mapeado exatamente; caso contrário, o valor de redirecionamento é prefixado para qualquer caminho que possa existir após server:port no URL. Dessa forma, quando AEM tentar redirecionar para a página de logon, isso falhará.

### Modificar o Site {#modify-the-site}

Após a criação inicial do site, os autores podem usar o ícone [](/help/communities/sites-console.md#authoring-site-content) Abrir site para executar atividades de criação padrão AEM.

Além disso, os administradores podem usar o ícone [](/help/communities/sites-console.md#modifying-site-properties) Editar site para modificar as propriedades do site, como o título.

Após qualquer modificação, lembre-se de **Salvar** e **publicar** o site novamente.

>[!NOTE]
>
>Se não estiver familiarizado com o AEM, visualização a documentação sobre manuseio [](/help/sites-authoring/basic-handling.md) básico e um guia [rápido para a criação de páginas](/help/sites-authoring/qg-page-authoring.md).


