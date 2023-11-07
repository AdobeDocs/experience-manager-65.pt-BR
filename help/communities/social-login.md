---
title: Logon social com o Facebook e o Twitter
description: O logon social permite que os visitantes do site façam logon com sua conta do Facebook ou do Twitter.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2773'
ht-degree: 1%

---

# Logon social com o Facebook e o Twitter {#social-login-with-facebook-and-twitter}

Logon social é a capacidade de apresentar a um visitante do site a opção de fazer logon com sua conta do Facebook ou do Twitter. Portanto, incluir dados de Facebook ou Twitter permitidos em seu perfil de membro AEM.

![socialloginweretail](assets/socialloginweretail.png)

## Visão geral do logon social {#social-login-overview}

Para incluir login social, é *obrigatório* para criar aplicativos personalizados do Facebook e do Twitter.

Embora a amostra de we-retail forneça exemplos de aplicativos Facebook e Twitter e serviços em nuvem, eles não estão disponíveis em um [site de produção](../../help/sites-administering/production-ready.md).

As etapas necessárias são:

1. [Habilitar autenticação OAuth](#adobe-granite-oauth-authentication-handler) em todas as instâncias de publicação do AEM.

   Sem o OAuth habilitado, as tentativas de logon falham.

1. **Criar** um aplicativo social e um serviço na nuvem.

   * Para oferecer suporte ao logon com o Facebook:

      * Criar um [aplicativo facebook](#create-a-facebook-app).
      * Criar e publicar um [Serviço em nuvem facebook Connect](#create-a-facebook-connect-cloud-service).

   * Para oferecer suporte ao logon com o Twitter:

      * Criar um [aplicativo Twitter](#create-a-twitter-app).
      * Criar e publicar um [Twitter Connect Cloud Service](#create-a-twitter-connect-cloud-service).

1. [**Ativar** login social](#enable-social-login) para um site da comunidade.

Há dois conceitos básicos:

1. **Escopo** (permissões) especifica os dados que o aplicativo tem permissão para solicitar.

   * O FACEBOOK e o TWITTER [Aplicativo e provedor Adobe Granite OAuth](#adobe-granite-oauth-application-and-provider) As instâncias do, por padrão, incluem as permissões básicas do aplicativo no escopo.

1. **Campos** (parâmetros) especifica os dados reais solicitados usando parâmetros de URL.

   * Esses campos são especificados em [Provedor OAuth do AEM Communities Facebook](#aem-communities-facebook-oauth-provider) e [Provedor OAuth do AEM Communities Twitter](#aem-communities-twitter-oauth-provider).
   * Os campos padrão são suficientes para a maioria dos casos de uso, mas podem ser modificados.

## Logon no facebook {#facebook-login}

### Versão da API do facebook {#facebook-api-version}

O logon social e a amostra do We-retail Facebook foram desenvolvidos quando a API Graph do Facebook era a versão 1.0. A partir do AEM 6.4 GA e AEM 6.3 SP1, o logon social foi atualizado para funcionar com a versão mais recente da API de gráfico 2.5 do Facebook.

>[!NOTE]
>
>Para versões mais antigas do AEM, se você estiver enfrentando uma exceção nos registros **Não é possível extrair um token deste**, atualize para o CFP mais recente nessa versão do AEM.

Para obter informações sobre a versão da API gráfica do Facebook, consulte a [Change Log da API do facebook](https://developers.facebook.com/docs/apps/changelog).

### Criar um aplicativo Facebook {#create-a-facebook-app}

Um aplicativo do Facebook corretamente configurado é necessário para habilitar o logon social do Facebook.

Para criar um aplicativo do Facebook, siga as instruções da Facebook em [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). As alterações nas instruções não se refletem nas informações a seguir.

Em geral, a partir da API do Facebook v2.7:

* *Adicionar um novo aplicativo Facebook*
   * Para *Platform*, escolha Site:
      * Para *URL do site*, insira `  https://<server>:<port>.`
      * Para *Nome de exibição*, insira um título para usar como o Título do serviço Facebook connect.
      * Para *Categoria*, escolha recomendada *Aplicativos para páginas*, mas pode ser qualquer coisa.
      * *Adicionar produto: logon do Facebook*
      * Para *URIs de redirecionamento OAuth válidos*, insira `  https://<server>:<port>.`

>[!NOTE]
>
>Para desenvolvimento, http://localhost:4503 funcionará.

Depois que o aplicativo tiver sido criado, localize o **[!UICONTROL ID do aplicativo]** e **[!UICONTROL Segredo do aplicativo]** configurações. Essas informações são necessárias para configurar o [Facebook cloud service](#createafacebookcloudservice).

### Criar um Cloud Service de conexão Facebook {#create-a-facebook-connect-cloud-service}

A variável [Aplicativo e provedor Adobe Granite OAuth](#adobe-granite-oauth-application-and-provider) instância, instanciada ao criar uma configuração do cloud service, identifica o aplicativo Facebook e os grupos de membros aos quais os novos usuários são adicionados.

1. Na instância do autor AEM, faça logon com privilégios de administrador.
1. Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de logon social do facebook]**.
1. Selecione a configuração **[!UICONTROL caminho do contexto]**.

   **[!UICONTROL Caminho do contexto]** deve ser o mesmo que o caminho de configuração na nuvem selecionado ao criar/editar um site da comunidade.

1. Verifique se o caminho de contexto está habilitado para criar serviços de nuvem abaixo dele.
1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**. Selecione o contexto e edite as propriedades. Habilite as Configurações de nuvem se ainda não estiver habilitado.

   ![config-propertiespng](assets/config-propertiespng.png)

   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

1. **Criar/Editar** Configuração do facebook Cloud Service.

   ![fbsocialloginconfig](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Título]** (*Obrigatório*) Insira um título de exibição que identifique o aplicativo Facebook. Use o mesmo nome inserido como *Nome de exibição* para o aplicativo Facebook.
   * **[!UICONTROL Chave do aplicativo ID/API]** (*Obrigatório*) Insira o ***ID do aplicativo*** para o aplicativo Facebook. Isso identifica o [Aplicativo e provedor Adobe Granite OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) instância criada a partir da caixa de diálogo.
   * **[!UICONTROL Segredo do aplicativo]** (*Obrigatório*) Insira o ***Segredo do aplicativo*** para o aplicativo Facebook.
   * **[!UICONTROL Criar usuários]** Se marcado, o logon com uma conta do Facebook criará uma entrada de usuário AEM e a adicionará como membro aos grupos de usuários selecionados.  O padrão está marcado (altamente recomendado).
   * **[!UICONTROL Mascarar IDs de usuário]**: Deixe desmarcado.
   * **[!UICONTROL Email do escopo]**: a ID de email do usuário deve ser buscada no Facebook.
   * **[!UICONTROL Adicionar a grupos de usuários]** selecione Adicionar grupo de usuários para escolher um ou mais [grupos de membros](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) para o site da comunidade ao qual os usuários serão adicionados.

   >[!NOTE]
   >
   >Os grupos podem ser adicionados ou removidos a qualquer momento. Mas as associações de usuários existentes não serão afetadas. A associação automática se aplica somente a novos usuários que estão sendo criados após a atualização desse campo. Para os sites em que os usuários anônimos estão desativados, opte por adicionar usuários ao grupo de membros da comunidade correspondente destinado ao site fechado da comunidade.

   * Selecionar **[!UICONTROL SALVE]**.
   * **[!UICONTROL Publicação]**.

O resultado é um [Aplicativo e provedor Adobe Granite OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) instância que não requer mais modificações, a menos que seja adicionado um escopo adicional (permissões). O escopo padrão são as permissões padrão para logon no Facebook. Se desejar escopo adicional, é necessário editar a configuração OSGI diretamente. Se houver modificações feitas diretamente pelo sistema/console, evite editar as configurações do Cloud Service na interface para toque, evitando substituições.

### Provedor OAuth do AEM Communities Facebook {#aem-communities-facebook-oauth-provider}

O provedor do AEM Communities estende o [Aplicativo e provedor Adobe Granite OAuth](#adobe-granite-oauth-application-and-provider) instância.

Esse provedor exigirá edição para:

* Permitir atualizações do usuário
* Adicionar campos adicionais [dentro do escopo](#adobe-granite-oauth-application-and-provider)

   * Nem todos os campos permitidos por padrão são incluídos por padrão.

Se a edição for necessária, em cada instância de publicação AEM:

1. Faça logon com privilégios de administrador.
1. Navegue até a [Console da Web](../../help/sites-deploying/configuring-osgi.md). Por exemplo, http://localhost:4503/system/console/configMgr.
1. Localize o Provedor OAuth do AEM Communities Facebook.
1. Selecione o ícone de lápis a ser aberto para edição.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID do provedor OAuth]**

     (*Obrigatório*) O valor padrão é *soco -facebook*. Não editar.

   * **[!UICONTROL Configuração de Cloud Service]**

     O valor padrão é `/etc/  cloudservices /  facebookconnect`. Não editar.

   * **[!UICONTROL Configuração do serviço do provedor OAuth]**

     O valor padrão é `/apps/social/facebookprovider/config/`. Não editar.

   * **[!UICONTROL Ativar tags]**

     Não editar.

   * **[!UICONTROL Caminho do usuário]**

     Local no repositório onde os dados do usuário estão armazenados. Para um site da comunidade, para garantir permissões para que os membros visualizem o perfil uns dos outros, o caminho deve ser o padrão */home/users/community*.

   * **[!UICONTROL Ativar campos]**

     Se marcados, os Campos listados serão especificados na solicitação ao Facebook para autenticação e informações do usuário. O padrão é desmarcado.

   * **[!UICONTROL Campos]**

     Quando os Campos são ativados, os seguintes campos são incluídos ao chamar a API do gráfico do Facebook. Os campos devem ser permitidos dentro do escopo definido na configuração do Cloud Service. Campos adicionais podem exigir aprovação pela Facebook. Consulte a seção Permissões de logon do Facebook da documentação do Facebook. Os campos padrão adicionados como parâmetros são:

      * id
      * name
      * first_name
      * last_name
      * link
      * localidade
      * imagem
      * fuso horário
      * updated_time
      * verificado
      * email

   Se algum campo for adicionado ou alterado, atualize a configuração correspondente do Manipulador de sincronização padrão para corrigir o mapeamento.

   * **[!UICONTROL Atualizar usuário]**

     Se marcado, atualiza os dados do usuário no repositório em cada logon para refletir as alterações de perfil ou os dados adicionais solicitados. O padrão está desmarcado.

#### Próximas etapas {#next-steps}

As próximas etapas são as mesmas para o Facebook e o Twitter:

* [Publicar as configurações do Cloud Service](#publishcloudservices)
* [Ativar para um site da comunidade](#enable-social-login)

## Login do Twitter {#twitter-login}

### Criar um aplicativo do Twitter {#create-a-twitter-app}

Um aplicativo Twitter configurado é necessário para habilitar o logon na rede social do Twitter.

Siga as instruções mais recentes para criar um aplicativo do Twitter em [https://apps.twitter.com](https://apps.twitter.com/).

Em geral:

1. Insira um *Nome* que identificará o aplicativo Twitter para os usuários do site.
1. Insira um *Descrição*.
1. Para *site* - insira `https://<server>`.
1. Para *URL de retorno* - insira `https://server`.

   >[!NOTE]
   >
   >Não é necessário especificar a porta.
   >
   >Para desenvolvimento, https://127.0.0.1/ funcionará.

1. Depois que o aplicativo tiver sido criado, localize o **[!UICONTROL Chave do consumidor (API)]** e **[!UICONTROL Segredo do consumidor (API)]**. Essas informações serão necessárias para configurar o [Twitter cloud service](#createatwittercloudservice).

#### Permissões {#permissions}

Na seção de permissões do gerenciamento de aplicativos do Twitter:

* **[!UICONTROL Access]**: Selecionar `Read only`.

   * Outras opções não são suportadas

* **[!UICONTROL Permissões adicionais]**: Opcionalmente, escolha `Request email addresses from users`.

   * Se não for selecionada, o perfil do usuário no AEM não incluirá seu endereço de email.
   * as instruções do Twitter observam as etapas adicionais a serem seguidas.

A única solicitação REST feita para logon social é para *[GET account/verificar credenciais](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### Criar um Cloud Service de conexão do Twitter {#create-a-twitter-connect-cloud-service}

A variável [Aplicativo e provedor Adobe Granite OAuth](#adobe-granite-oauth-application-and-provider) instância, instanciada ao criar uma configuração do cloud service, identifica o aplicativo do Twitter e os grupos de membros aos quais os novos usuários são adicionados.

1. Na instância do autor, faça logon com privilégios de administrador.
1. Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de logon social do Twitter]**.
1. Escolha o **[!UICONTROL caminho do contexto]** configuração.

   O Caminho do contexto deve ser igual ao caminho de configuração da nuvem selecionado ao criar/editar um site da comunidade.

1. Verifique se o caminho de contexto está habilitado para criar serviços de nuvem abaixo dele.
1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**. Selecione o contexto e edite as propriedades. Habilite as Configurações de nuvem se ainda não estiver habilitado.

   ![twitterconfigproppng](assets/twitterconfigproppng.png)

   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.

1. Criar/editar a configuração do serviço de nuvem do Twitter.

   ![twittersocialloging](assets/twittersocialloginpng.png)

   * **[!UICONTROL Título]**

     (*Obrigatório*) Insira um título de exibição que identifique o aplicativo Twitter. Use o mesmo nome inserido como *Nome de exibição* para o aplicativo Twitter.

   * **[!UICONTROL Chave do consumidor]**

     (*Obrigatório*) Insira o **Chave do consumidor (API)** para o aplicativo Twitter. Isso identifica o [Aplicativo e provedor Adobe Granite OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) instância criada a partir da caixa de diálogo.

   * **[!UICONTROL Segredo do consumidor]**

     (*Obrigatório*) Insira o ***Segredo do consumidor (API)*** para o aplicativo Twitter.

   * **[!UICONTROL Criar usuários]**

     Se marcado, o login com uma conta do Twitter criará uma entrada de usuário AEM e a adicionará como membro ao(s) grupo(s) de usuários selecionado(s). O padrão está marcado (altamente recomendado).

   * **[!UICONTROL Mascarar IDs de usuário]**

     Deixe desmarcado.

   * **[!UICONTROL Adicionar aos Grupos de usuários]**

     Selecione Adicionar grupo de usuários para escolher um ou mais [grupos de membros](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) para o site da comunidade ao qual os usuários serão adicionados.

   >[!NOTE]
   >
   >Os grupos podem ser adicionados ou removidos a qualquer momento. Mas as associações de usuários existentes não serão afetadas. A associação automática se aplica somente a novos usuários que estão sendo criados após a atualização desse campo. Para os sites em que os usuários anônimos estão desativados, adicione usuários ao grupo de membros da comunidade correspondente destinado ao site da comunidade fechado.
   >

1. Selecionar **[!UICONTROL SALVE]** e **[!UICONTROL Publish]**.

O resultado é um [Aplicativo e provedor Adobe Granite OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) que não exige mais modificações. O escopo padrão são as permissões padrão para logon de Twitter.

### Provedor OAuth do AEM Communities Twitter {#aem-communities-twitter-oauth-provider}

A configuração do AEM Communities estende a [Aplicativo e provedor Adobe Granite OAuth](#adobe-granite-oauth-application-and-provider) instância. Esse provedor exigirá edição para permitir atualizações do usuário.

Se a edição for necessária, em cada instância de publicação AEM:

1. Faça logon com privilégios de administrador.
1. Navegue até a [Console da Web](../../help/sites-deploying/configuring-osgi.md).

   Por exemplo, http://localhost:4503/system/console/configMgr.

1. Localize o Provedor OAuth do AEM Communities Twitter.
1. Selecione o ícone de lápis a ser aberto para edição.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID do provedor OAuth]**

   (*Obrigatório*) O valor padrão é *soco -twitter*. Não editar.

   * **[!UICONTROL Configuração de Cloud Service]**

     O valor padrão é *conf.* Não editar.

   * **[!UICONTROL Configuração do serviço do provedor OAuth]**

     O valor padrão é `/apps/social/twitterprovider/config/`. Não editar.

   * **[!UICONTROL Caminho do usuário]**

     Local no repositório onde os dados do usuário estão armazenados. Para um site da comunidade, para garantir permissões para que os membros visualizem o perfil uns dos outros, o caminho deve ser o padrão `/home/users/community`.

   * **[!UICONTROL Ativar parâmetros]** não editar
   * **[!UICONTROL Parâmetros de URL]** não editar
   * **[!UICONTROL Atualizar usuário]**

     Se marcado, atualiza os dados do usuário no repositório em cada logon para refletir as alterações de perfil ou os dados adicionais solicitados. O padrão é desmarcado.

#### Próximas etapas {#next-steps-1}

As próximas etapas são as mesmas para o Facebook e o Twitter:

* [Publicar as configurações do Cloud Service](#publishcloudservices)
* [Ativar para um site da comunidade](#enable-social-login)

## Ativar logon social {#enable-social-login}

### Console de sites do AEM Communities {#aem-communities-sites-console}

Depois que um serviço em nuvem é configurado, ele pode ser ativado para a configuração relevante de Logon social de um site da comunidade usando o [User Management](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) Subpainel Configurações durante o site da comunidade [criação](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) ou [gerenciamento](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. Escolha o contexto de configuração do site onde você salvou as configurações de logon social.

1. Na guia Geral, defina as configurações de nuvem.

   ![managesites_png](assets/managesites_png.png)

1. Na guia Configurações, ative **[!UICONTROL Logons sociais]** e Salvar.

   ![usermgmt_png](assets/usermgmt_png.png)

## Testar logon social {#test-social-login}

* Assegurar [Manipulador de autenticação OAuth do Adobe Granite](#adobe-granite-oauth-authentication-handler) foi ativado em todas as instâncias de publicação.
* Verifique se os serviços em nuvem foram publicados.
* Verifique se o site da comunidade foi publicado.
* Inicie o site publicado em um navegador.
Por exemplo, http://localhost:4503/content/sites/engage/en.html
* Selecionar **[!UICONTROL Login]**.
* Selecione **[!UICONTROL Fazer logon com a Facebook]** ou **[!UICONTROL Fazer logon com o Twitter]**.
* Se ainda não tiver feito logon no Facebook ou no Twitter, faça logon com as credenciais apropriadas.
* Pode ser necessário conceder permissão dependendo da caixa de diálogo exibida pelo aplicativo Facebook ou Twitter.
* Observe que a barra de ferramentas na parte superior da página é atualizada para refletir o logon bem-sucedido.
* Selecionar **[!UICONTROL Perfil]**: a página Perfil exibe a imagem de avatar, o nome e o sobrenome do usuário. Ela também exibe as informações do perfil do Facebook ou do Twitter de acordo com os campos/parâmetros permitidos.

## Configurações do OAuth para a plataforma AEM {#aem-platform-oauth-configurations}

### Manipulador de autenticação OAuth do Adobe Granite {#adobe-granite-oauth-authentication-handler}

A variável `Adobe Granite OAuth Authentication Handler` não está habilitado por padrão e ***deve ser ativado em todas as instâncias de publicação do AEM.***

Para ativar o manipulador de autenticação na publicação, basta abrir a configuração do OSGi e salvá-la:

* Faça logon com privilégios de administrador.
* Navegue até a [Console da Web](../../help/sites-deploying/configuring-osgi.md).
Por exemplo, http://localhost:4503/system/console/configMgr
* Localizar `Adobe Granite OAuth Authentication Handler`.
* Selecione para abrir a configuração para edição.
* Selecione **[!UICONTROL Salvar]**.

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>Tenha cuidado para não confundir o manipulador de autenticação com uma instância Facebook ou Twitter de *Aplicativo e provedor Adobe Granite OAuth*.

![graniteoauth1](assets/graniteoauth1.png)

### Aplicativo e provedor Adobe Granite OAuth {#adobe-granite-oauth-application-and-provider}

Quando um serviço em nuvem para o Facebook ou Twitter é criado, uma instância de `Adobe Granite OAuth Authentication Handler` é criado.

Para localizar a instância criada para um aplicativo Facebook ou Twitter:

1. Faça logon com privilégios de administrador.
1. Navegue até a [Console da Web](../../help/sites-deploying/configuring-osgi.md).

   Por exemplo, http://localhost:4503/system/console/configMgr.

1. Localize o Aplicativo e Provedor Adobe Granite OAuth.

   * Localize a instância em que **[!UICONTROL ID do cliente]** corresponde ao **[!UICONTROL ID do aplicativo]**.

     ![graniteoauth2](assets/graniteoauth2.png)

     Com exceção das seguintes propriedades, deixe as outras propriedades da configuração inalteradas:

   * **[!UICONTROL ID de configuração]**

     (*Obrigatório*) As IDs de configuração do OAuth devem ser exclusivas. Gerado automaticamente quando o serviço em nuvem é criado.

   * **[!UICONTROL ID do cliente]**

     (*Obrigatório*) A ID do aplicativo fornecida quando o serviço em nuvem foi criado.

   * **[!UICONTROL Client Secret]**

     (*Obrigatório*) A senha do aplicativo fornecida quando o serviço em nuvem foi criado.

   * **[!UICONTROL Escopo]**

     (*Opcional*) Escopo adicional para o que é permitido pode ser solicitado do provedor. O escopo padrão abrange as permissões necessárias para fornecer autenticação social e dados de perfil.

   * **[!UICONTROL ID do provedor]**

     (*Obrigatório*) A ID do provedor do AEM Communities é definida quando o serviço em nuvem é criado. Não editar. Para o Facebook Connect, o valor é *soco -facebook*. Para o Twitter Connect, o valor é *soco -twitter*.

   * **[!UICONTROL Grupos]**

     (*Recomendado*) Um ou mais grupos de membros aos quais os usuários criados são adicionados. No AEM Communities, é recomendável listar o grupo de membros para o site da comunidade.

   * **[!UICONTROL URL de retorno]**

     (*Opcional*) URL configurado com os provedores OAuth para redirecionar o cliente. Use um URL relativo para usar o host da solicitação original. Deixe em branco para utilizar o URL originalmente solicitado. O sufixo &quot;/callback/j_security_check&quot; é anexado automaticamente a este url.

   >[!NOTE]
   >
   >O domínio para o retorno de chamada deve ser registrado com o provedor (Facebook ou Twitter).

Para cada configuração do manipulador de autenticação OAuth, há duas configurações adicionais criadas na instância:

* Manipulador de sincronização padrão do Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) - Nenhuma edição é necessária, mas você pode consultar os mapeamentos de campo de usuário como os campos do Facebook são mapeados para um nó de perfil de usuário do CQ. Observe também que &quot;Nome do manipulador de sincronização&quot; corresponde à ID de configuração da configuração do provedor OAuth.
* Módulo de logon externo do Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - Nenhuma edição é necessária, mas você pode notar que &#39;Nome do provedor de identidade&#39; e &#39;Nome do manipulador de sincronização&#39; são iguais e apontam para as configurações correspondentes do OAuth e do manipulador de sincronização, respectivamente.

Para obter mais informações, consulte [Autenticação com o módulo de logon externo do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## Desempenho de passagem de usuário do OAuth {#oauth-user-traversal-performance}

Para sites da comunidade que veem centenas de milhares de usuários se registrarem usando o logon do Facebook ou do Twitter, o desempenho de passagem da consulta executada quando um visitante do site usa o logon social pode ser aprimorado adicionando o seguinte índice Oak.

Se avisos de passagem forem vistos nos logs, é recomendável adicionar esse índice.

Em uma instância de autor, conectado com privilégios administrativos:

1. Na navegação global: selecione **Ferramentas, [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Crie um índice chamado ntBaseLucene-oauth a partir de uma cópia de ntBaseLucene:

   * No nó `/oak:index`
   * Selecionar nó `ntBaseLucene`
   * Selecionar **[!UICONTROL Copiar]**
   * Selecione `/oak:index`
   * Selecionar **[!UICONTROL Colar]**
   * Renomear cópia de ntBaseLucene para `ntBaseLucene-oauth`

1. Modifique as propriedades do nó ntBaseLucene-oauth:

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL reindexar]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. No nó /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * Exclua todos os nós filhos, exceto cqTags.
   * Renomear cqTags para `oauthid-123****`
   * Modificar as propriedades do nó `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`

   * Selecionar **[!UICONTROL Salvar tudo]**.

* Para o **name** `oauthid-123`, substituir *123* com a Facebook ***ID do aplicativo*** ou Twitter ***Chave do consumidor (API)*** esse é o valor de **ID do cliente** no [Aplicativo e provedor Adobe Granite OAuth](social-login.md#adobe-granite-oauth-application-and-provider) configuração.

  ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

Para obter informações e ferramentas adicionais, consulte [Consultas e indexação do Oak](../../help/sites-deploying/queries-and-indexing.md).

## Configuração do Dispatcher {#dispatcher-configuration}

Consulte [Configuração do Dispatcher para comunidades](dispatcher.md).
