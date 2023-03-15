---
title: Gerenciar [!DNL Adobe Stock] ativos
description: Pesquisar, buscar, licenciar e gerenciar [!DNL Adobe Stock] ativos de dentro [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 8%

---

# Use [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/aem-assets-adobe-stock.html?lang=en) |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

[!DNL Adobe Stock] por padrão, a oferta para empresas inclui direitos de compartilhamento na organização. Depois que um ativo tiver sido licenciado por um usuário de sua organização, outros usuários da organização poderão identificar, baixar e usar esse ativo sem ter que licenciá-lo novamente. Depois que um ativo tiver sido licenciado pela sua organização, o direito de usá-lo é perpétuo.

As organizações podem integrar sua empresa [!DNL Adobe Stock] planejar com [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos da [!DNL Experience Manager]. [!DNL Experience Manager] os usuários podem encontrar, visualizar e licenciar rapidamente os ativos da Adobe Stock que foram salvos em [!DNL Experience Manager], sem deixar o [!DNL Experience Manager] interface.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] fornece aos usuários a capacidade de pesquisar, visualizar, salvar e licenciar [!DNL Adobe Stock] ativos diretamente de [!DNL Experience Manager].

**Pré-requisitos**

A integração exige:

* Um [empresa [!DNL Adobe Stock] plano](https://stockenterprise.adobe.com/)
* Um usuário com permissões no Admin Console para o perfil de produto do Stock padrão
* Um usuário com permissões para o perfil de Acesso do desenvolvedor para criar integração no Adobe Developer Console

Uma empresa [!DNL Adobe Stock] plano,

* Fornece direito ao produto para [!DNL Adobe Stock] (Existências ligadas a Experience Manager)
* Créditos comprados na [!DNL Adobe Admin Console] para seu direito ao estoque
* Habilita a autenticação da conta de serviço (JWT) em [!DNL Adobe Developer Console] para seu direito ao estoque
* Permite gerenciar os créditos e o licenciamento globalmente de dentro do [!DNL Adobe Admin Console]

No direito, um perfil de produto padrão para [!DNL Adobe Stock] existe em [!DNL Admin Console]. Vários perfis podem ser criados, e esses perfis determinam quem pode licenciar ativos do Stock. Um usuário com acesso direto ao perfil do produto pode acessar [https://stock.adobe.com/](https://stock.adobe.com/) e licenciar ativos do Stock. Considerando que há outro método de usar o Developer Access para criar integração (API) para autenticar a comunicação entre [!DNL Experience Manager] e [!DNL Adobe Stock].

>[!NOTE]
>
>A autenticação da conta de serviço de estoque (JWT) vem com o direito ao estoque empresarial.
>
>A integração não oferece suporte à autenticação Oauth para o direito ao Enterprise Stock.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Etapas para integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integration-steps}

Para integrar [!DNL Experience Manager] e [!DNL Adobe Stock], execute as seguintes etapas na sequência listada:

1. [Obter certificado público](#public-certificate)

   Em [!DNL Experience Manager], crie uma conta IMS e gere um certificado público (chave pública).

1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)

   Em [!DNL Adobe Developer Console], crie um projeto para [!DNL Adobe Stock] organização. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT). Obtenha as credenciais da conta de serviço e as informações de carga JWT.

1. [Configurar conta IMS](#create-ims-account-configuration)

   Em [!DNL Experience Manager], configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.

1. [Configurar o serviço em nuvem](#configure-the-cloud-service)

   Em [!DNL Experience Manager], configure um [!DNL Adobe Stock] serviço em nuvem usando a conta IMS.


### Criar uma configuração IMS {#create-an-ims-configuration}

A configuração IMS autentica seu [!DNL Experience Manager Assets] instância do autor com a [!DNL Adobe Stock] direito.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

A chave pública (certificado) autentica o perfil do produto no Adobe Developer Console.

1. Faça logon no [!DNL Experience Manager Assets] instância do autor. O URL padrão é `http://localhost:4502/aem/start.html`.

1. No **[!UICONTROL Ferramentas]** , navegue até **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Na página Configurações do Adobe IMS , clique em **[!UICONTROL Criar]**. O **[!UICONTROL Configuração de conta técnica do Adobe IMS]** será aberta.

1. No **[!UICONTROL Certificado]** guia , selecione **[!UICONTROL Adobe Stock]** do **[!UICONTROL Solução da nuvem]** lista suspensa.

1. Você pode criar um certificado ou reutilizar um certificado existente para a configuração.

   Para criar um certificado, selecione **[!UICONTROL Criar novo certificado]** e especifique uma **alias** para a chave pública. O alias serve como nome da chave pública.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** para gerar a chave pública.

1. Clique no botão **[!UICONTROL Baixar chave pública]** e salve o arquivo de chave pública (.crt) em sua máquina. A chave pública é usada posteriormente para configurar a API do locatário do Brand Portal e gerar credenciais de conta de serviço no Adobe Developer Console.

   Clique em **[!UICONTROL Avançar]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. No **Conta** , é criada a conta do Adobe IMS que requer as credenciais da conta de serviço.

   Abra uma nova guia e [criar uma conexão de conta de serviço (JWT) no Adobe Developer Console](#createnewintegration).

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Adobe Developer Console, os projetos e as APIs são configurados no nível da organização. Configurar uma API cria uma conexão de conta de serviço (JWT). Há dois métodos para configurar a API, gerando um par de chaves (chaves privadas e públicas) ou carregando uma chave pública. Neste exemplo, as credenciais da conta de serviço são geradas pelo upload da chave pública.

Para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Adobe Developer Console com privilégios de administrador do sistema. O URL padrão é [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Certifique-se de ter selecionado a organização IMS correta (direito ao estoque) na lista suspensa (organização).

1. Clique em **[!UICONTROL Criar novo projeto]**. Um projeto em branco com um nome gerado pelo sistema é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]**. Atualize o **[!UICONTROL Título do projeto]** e **[!UICONTROL Descrição]** e, em seguida, clique em **[!UICONTROL Salvar]**.

1. No **[!UICONTROL Visão geral do projeto]** clique em **[!UICONTROL Adicionar API]**.

1. No **[!UICONTROL Adicionar uma janela de API]**, selecione **[!UICONTROL Adobe Stock]**. Clique em **[!UICONTROL Avançar]**.

1. No **[!UICONTROL Configurar API]** janela , selecione **[!UICONTROL Conta de serviço (JWT)]** autenticação. Clique em **[!UICONTROL Avançar]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Clique em **[!UICONTROL Fazer upload de sua chave pública]**. Clique em **[!UICONTROL Selecionar um Arquivo]** e faça upload da chave pública (arquivo .crt) que você baixou no [obter certificado público](#public-certificate) seção. Clique em **[!UICONTROL Avançar]**.

1. Verifique a chave pública e clique em **[!UICONTROL Próximo]**.

1. Selecione o padrão **[!UICONTROL Adobe Stock]** perfil do produto e clique em **[!UICONTROL Salvar API configurada]**.

1. Depois que a API for configurada, você será redirecionado para a página de visão geral da API. Na navegação à esquerda em **[!UICONTROL Credenciais]**, clique no botão **[!UICONTROL Conta de serviço (JWT)]** opção. Aqui, você pode exibir as credenciais e executar ações como gerar tokens JWT, copiar detalhes da credencial e recuperar o segredo do cliente.

1. No **[!UICONTROL Credenciais do Cliente]** , copie a **[!UICONTROL client ID]**.

   Clique em **[!UICONTROL Recuperar Segredo do Cliente]** e copie o **[!UICONTROL segredo do cliente]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navegue até o **[!UICONTROL Gerar JWT]** e copie a **[!UICONTROL Carga JWT]** informações.

Agora você pode usar a ID do cliente (chave de API), o segredo do cliente e a carga JWT para [configurar a conta IMS](#create-ims-account-configuration) em [!DNL Experience Manager Assets].

### Configurar conta IMS {#create-ims-account-configuration}

Você deve ter o [certificate](#public-certificate) e [credenciais da conta de serviço (JWT)](#createnewintegration) para configurar a conta IMS.

Para configurar a conta IMS:

1. Abra a Configuração IMS e navegue até o **[!UICONTROL Conta]** guia . Você manteve a página aberta enquanto [obtenção do certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No **[!UICONTROL Servidor de autorização]** , insira o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Insira a ID do cliente no **[!UICONTROL Chave da API]** campo , **[!UICONTROL Segredo do cliente]** e **[!UICONTROL Carga]** (Carga JWT) que você copiou enquanto [criação da conexão da conta de serviço (JWT)](#createnewintegration).

1. Clique em **[!UICONTROL Criar]**. Uma configuração de conta IMS é criada.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Selecione a configuração da conta IMS e clique em **[!UICONTROL Verificar integridade]**.

   Clique em **[!UICONTROL Verificar]** na caixa de diálogo. Na configuração bem-sucedida, uma mensagem aparece informando que a variável *O token foi recuperado com êxito*.

   ![exame de integridade](assets/aem-stock-healthcheck.png)


### Configurar o serviço em nuvem {#configure-the-cloud-service}

Para configurar o [!DNL Adobe Stock] serviço em nuvem:

1. No [!DNL Experience Manager] interface do usuário, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. No [!DNL Adobe Stock Configurations] página, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração da nuvem.

   Selecione a configuração IMS que você criou ao [configuração da conta IMS](#create-ims-account-configuration).

   Selecione o local na lista suspensa.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Clique em **[!UICONTROL Salvar e fechar]**.

   Seu [!DNL Experience Manager Assets] a instância do autor agora é integrada com [!DNL Adobe Stock]. Você pode criar vários [!DNL Adobe Stock] configurações (por exemplo, configurações baseadas em localidade). Agora você pode acessar, pesquisar e licenciar a variável [!DNL Adobe Stock] ativos da [!DNL Experience Manager] interface do usuário.

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >Nesse estágio de integração, somente os administradores podem acessar a variável [!DNL Adobe Stock] ativos, pesquisar ativos do Stock (usando o omnisearch) e licenciar o [!DNL Adobe Stock] ativos.
   >
   >Os administradores podem adicionar usuários ou grupos à [!DNL Adobe Stock] o serviço em nuvem e fornece permissões para esses usuários não administradores no [!DNL Experience Manager] para acessar a configuração do Stock.

1. Para adicionar usuários ou grupos, selecione o [!DNL Adobe Stock] configuração da nuvem e clique em **[!UICONTROL Propriedades]**.

1. Pesquise para adicionar os usuários ou grupos aos quais você atribuiu permissões para acessar a configuração do Adobe Stock. Consulte [atribuir permissões ao grupo de usuários](#assign-permissions-to-group).


## Atribuir permissões ao grupo de usuários {#assign-permissions-to-group}

Os administradores podem criar grupos de usuários e conceder permissões a determinados usuários ou grupos para acessar o [!DNL Adobe Stock] serviço em nuvem.

A seguir estão as permissões necessárias para um usuário pesquisar e licenciar ativos do Adobe Stock:

* Configure o caminho: `/conf/global/settings/stock`
* Privilégios: `jcr:read`
* Tipo de permissão: `Allow`

Você pode criar um grupo de usuários ou atribuir permissões a um grupo de usuários existente. As permissões podem ser atribuídas a partir do [!DNL Experience Manager Assets] ou da [!DNL User Admin] Console.

**Para fornecer acesso a um grupo de usuários do [!DNL Experience Manager]:**

1. No [!DNL Experience Manager] interface do usuário, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**. Criar um grupo de usuários para [!DNL Adobe Stock].

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Permissões]**.

1. Procure o grupo de usuários no painel esquerdo e adicione um novo **[!UICONTROL Entrada de Controle de Acesso (ACE)]** para Adobe Stock.

   * Configure o caminho: `/conf/global/settings/stock`
   * Privilégios: `jcr:read`
   * Tipo de permissão: `Allow`

   Clique em **[!UICONTROL Adicionar]**.

   ![permissões de usuário](assets/aem-stock-user-permissions.png)

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Selecione o [!DNL Adobe Stock] configuração da nuvem e clique em **[!UICONTROL Propriedades]**.

1. Adicione o grupo de usuários recém-criado à [!DNL Adobe Stock] configuração. Clique em **[!UICONTROL Salvar e fechar]**.

   ![usuário atribuído](assets/aem-stock-adduser.png)

**Para fornecer acesso a um usuário do [!DNL User Admin Console]:**

1. Abra o [!DNL Experience Manager] Admin Console do usuário. O URL padrão é `http://localhost:4502/userdamin`.

1. No painel esquerdo, procure o usuário inserindo o `user_id` ou `name`. Clique duas vezes para abrir as propriedades do usuário.

1. Navegue até o **[!UICONTROL Permissões]** e permitir `read` permissões para o [!DNL Adobe Stock] configuração da nuvem: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se a configuração da nuvem não for permitida, o usuário só poderá acessar **[!UICONTROL Ativos]** no [!DNL Experience Manager] interface.
   >
   >Para permitir o acesso ao [!UICONTROL Ativos] e [!DNL Adobe Stock] , verifique se a configuração da nuvem é permitida para o usuário.

1. Clique em **[!UICONTROL Salvar]** para atualizar as permissões.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Adicione o usuário ou o grupo à [!DNL Adobe Stock] configuração da nuvem.


## Acessar ativos da Adobe Stock {#access-stock-assets}

Um usuário não administrador com permissões para o [!DNL Adobe Stock] a configuração da nuvem pode pesquisar e licenciar o [!DNL Adobe Stock] ativos do [!DNL Experience Manager] interface.

O usuário precisa executar uma etapa extra para ativar o [!DNL Adobe Stock] configuração da nuvem antes de acessar [!DNL Adobe Stock] ativos. É uma atividade única. Se o usuário receber permissões em vários [!DNL Adobe Stock] configurações de nuvem, o usuário pode selecionar a configuração desejada no **[!UICONTROL Preferências do usuário]**.

Para ativar o [!DNL Adobe Stock] configuração da nuvem:

1. Faça logon em [!DNL Experience Manager].

1. Clique no ícone do usuário no canto superior direito e clique em **[!UICONTROL Minhas preferências]**. O **[!UICONTROL Preferências do usuário]** será aberta.

1. Selecione o **[!UICONTROL Configuração de estoque]** na lista suspensa e clique em **[!UICONTROL Aceitar]** para ativar a configuração.

   ![preferências de usuário](assets/aem-stock-preferences.png)

1. Navegar para **[!UICONTROL Ativos]** > **[!UICONTROL Adobe Stock]**. Agora você pode visualizar, pesquisar e licenciar [!DNL Adobe Stock] ativos.

A tabela a seguir explica como as permissões do usuário funcionam ao acessar o [!DNL Adobe Stock] ativos:

| Usuário | Grupo | Permissões | Aceitar configuração do Stock nas Preferências do Usuário | Acessar ativos | Acessar o Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/A | Todos | N/A | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global /settings/stock/cloud-config | Sim | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global /settings/stock/cloud-config | Não | Erro: Falha ao carregar dados | Não |
| test-doc1 | Usuário do DAM | **allow**: /conf/global /settings/stock     **negar**: /cloud-config | A configuração do estoque não está visível | Sim | Não |


## Usar e gerenciar [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Com esse recurso, as organizações podem permitir que seus usuários trabalhem usando [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]. No [!DNL Experience Manager] interface do usuário, os usuários podem pesquisar [!DNL Adobe Stock] ativos e licencie os ativos necessários.

Uma vez [!DNL Adobe Stock] o ativo é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo típico. Em [!DNL Experience Manager], os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos em [!DNL Brand Portal]; acessar e usar os ativos por meio de [!DNL Experience Manager] aplicativo de desktop; e assim por diante.

![Procurar por [!DNL Adobe Stock] ativos e filtrar resultados de seus [!DNL Adobe Experience Manager] espaço de trabalho](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] Pesquise ativos semelhantes aos ativos cuja ID do é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Procure um dos tipos de ativos mais compatíveis **D.** Abra ou recolha o painel Filtros **E.** Licencie e salve o ativo selecionado no [!DNL Experience Manager]**F.**[!DNL Experience Manager] Salve o ativo no com a marca d&#39;água **G.**[!DNL Adobe Stock] Explore os ativos no site do que são semelhantes ao ativo selecionado **H.**[!DNL Adobe Stock] Exiba os ativos selecionados no site do **I.** Número de ativos selecionados dos resultados de pesquisa **J.** Alterne entre a exibição Cartão e a exibição em Lista

### Localizar ativos {#find-assets}

Seu [!DNL Experience Manager] os usuários do podem pesquisar ativos em ambos, [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando o local de pesquisa não estiver limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] são exibidas.

* Para pesquisar por [!DNL Adobe Stock] ativos, clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisa](assets/do-not-localize/search_icon.png).

Como alternativa, comece a digitar `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. [!DNL Experience Manager] O oferece recursos de filtragem avançados nos ativos pesquisados, permitindo que os usuários entrem rapidamente nos ativos necessários usando filtros, como tipos de ativos compatíveis, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Ativos pesquisados [!DNL Adobe Stock] são exibidos em [!DNL Experience Manager]. [!DNL Adobe Stock] os ativos são buscados e armazenados em [!DNL Experience Manager] repositório somente após um usuário [salva um ativo](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [licencia e salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Ativos já armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, a variável [!DNL Stock] os ativos são salvos com alguns metadados adicionais para indicar a fonte como [!DNL Stock].

![Pesquisar filtros em [!DNL Experience Manager] e destacado [!DNL Adobe Stock] ativos em resultados de pesquisa](assets/aem-search-filters2.jpg)

### Salvar e exibir os ativos necessários {#saveassets}

Selecione um ativo que deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Salvar] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão destacados com um selo, para indicar que tais ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez do selo Licenciado .

### Ativos da licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] usando a cota de seus [!DNL Adobe Stock] plano empresarial. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso no [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo o [!DNL Adobe Stock] propriedades de metadados para os ativos salvos em [!DNL Experience Manager]e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações para referência de licença não são sincronizadas entre [!DNL Experience Manager] e [!DNL Adobe Stock] site.

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)


## Limitações conhecidas {#known-limitations}

* **Problemas na integração com o [!DNL Experience Manager] Service Pack 6.5.7.0 e superior**: Um problema inesperado é identificado durante a integração com o [!DNL Experience Manager] 6.5.7.0 e superior. O problema está sendo testado e deve estar disponível em [!DNL Experience Manager] 6.5.11.0. Contato [!DNL Customer Support] para obter um hotfix imediato.

* **A funcionalidade para restringir usuários do licenciamento não está funcionando corretamente**: Todos os usuários com `read` as permissões para a configuração de estoque podem pesquisar e licenciar o [!DNL Adobe Stock] ativos.

* **Usuários não administradores precisam ativar manualmente a variável [!DNL Adobe Stock] configuração na nuvem**: No **[!UICONTROL Preferências do usuário]** , a **[!UICONTROL Configuração de estoque]** mostra o [!DNL Adobe Stock] configuração de nuvem como ativada, mas não funciona para um usuário não administrador. O usuário precisa clicar no botão **[!UICONTROL Aceitar]** para ativar a configuração do Stock. Na ausência dessa etapa, o sistema reflete uma mensagem de erro ao acessar **[!UICONTROL Ativos]**.

* **O aviso de imagem editorial não é apresentado**: Ao licenciar uma imagem, os usuários não podem verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais no Admin Console.

* **Tipo de licença incorreto exibido**: É possível que um tipo de licença incorreto seja exibido em [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon na [!DNL Adobe Stock] para ver o tipo de licença.

* **Os campos e metadados de referência não são sincronizados**: Quando um usuário atualiza um campo de referência de licença, as informações de referência da licença são atualizadas em [!DNL Experience Manager] mas não no [!DNL Adobe Stock] site. Da mesma forma, se o usuário atualizar os campos de referência na variável [!DNL Adobe Stock] no site, as atualizações não são sincronizadas no [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre como usar [!DNL Adobe Stock] ativos com [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ajuda do plano empresarial](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Perguntas frequentes](https://helpx.adobe.com/stock/faq.html)



<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

