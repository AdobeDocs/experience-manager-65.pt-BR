---
title: Configurar fontes de dados
description: Saiba como configurar diferentes tipos de fontes de dados para criar modelos de dados de formulário.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 1%

---

# Configurar fontes de dados{#configure-data-sources}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |


![Integração de dados](do-not-localize/data-integeration.png)

A Integração de dados do AEM Forms permite configurar e conectar-se a diferentes fontes de dados. Os seguintes tipos são prontos para uso. No entanto, com pouca personalização, também é possível integrar outras fontes de dados.

* Bancos de dados relacionais - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS, postgreSQL e Sybase
* Perfil de usuário AEM
* Serviços Web RESTful
* Serviços da Web com base em SOAP
* Serviços OData

A integração de dados oferece suporte aos tipos de autenticação OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais de Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica e Chave de API prontos para uso, e permite a implementação de autenticação personalizada para acessar serviços Web. Enquanto os serviços RESTful, baseados em SOAP e OData são configurados no AEM Cloud Service AEM AEM, o JDBC para bancos de dados relacionais e o conector para perfil de usuário do são configurados no console da Web do.

## Configurar banco de dados relacional {#configure-relational-database}

Você pode configurar bancos de dados relacionais usando a Configuração do Console da Web AEM. Faça o seguinte:

1. Ir para o console da Web do AEM em `https://server:host/system/console/configMgr`.
1. Procure a configuração **[!UICONTROL Fonte de dados agrupada da conexão Apache Sling]**. Selecione para abrir a configuração no modo de edição.
1. Na caixa de diálogo de configuração, especifique os detalhes do banco de dados que você deseja configurar, como:

   * Nome da fonte de dados
   * Propriedade do serviço de fonte de dados que armazena o nome da fonte de dados
   * Nome da classe Java do driver JDBC
   * URI da conexão JDBC
   * Nome de usuário e senha para estabelecer conexão com o driver JDBC

   >[!NOTE]
   >
   >Certifique-se de criptografar informações confidenciais, como senhas, antes de configurar a fonte de dados. Para criptografar:
   >
   > 1. Vá para https://&#39;[server]:[port]&#39;/system/console/crypto.
   > 1. No campo **[!UICONTROL Texto sem formatação]**, especifique a senha ou qualquer cadeia de caracteres a ser criptografada e selecione **[!UICONTROL Protect]**.
   >
   >O texto criptografado é exibido no campo Texto protegido que você pode especificar na configuração.

1. Habilite **[!UICONTROL Test on Borrow]** ou **[!UICONTROL Test on Return]** para especificar que os objetos são validados antes de serem emprestados ou retornados de e para o pool, respectivamente.
1. Especifique uma consulta SQL SELECT no campo **[!UICONTROL Consulta de Validação]** para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Com base no seu banco de dados, especifique uma das seguintes opções:

   * SELECT 1 (MySQL e MS SQL)
   * SELECIONE 1 no duplo (Oracle)

1. Selecione **[!UICONTROL Salvar]** para salvar a configuração.

   >[!NOTE]
   >
   > Se o Modelo de dados do Forms contiver um objeto que seja uma palavra-chave reservada para o banco de dados relacional, ele poderá causar problemas de adição, atualização ou recuperação de dados. Portanto, evite usar esses objetos no Modelo de dados de formulário.

## Configurar perfil de usuário do AEM {#configure-aem-user-profile}

Você pode configurar o perfil de usuário AEM usando a configuração do Conector de perfil de usuário no Console da Web AEM. Faça o seguinte:

1. Acesse o console da Web do AEM em https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Procure por **[!UICONTROL Integrações de Dados do AEM Forms - Configuração do Conector de Perfil de Usuário]** e selecione para abrir a configuração no modo de edição.
1. Na caixa de diálogo Configuração do conector de perfil de usuário, você pode adicionar, remover ou atualizar propriedades de perfil de usuário. As propriedades especificadas estão disponíveis para uso no modelo de dados de formulário. Use o seguinte formato para especificar as propriedades do perfil do usuário:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >O **&#42;** no exemplo acima denota todos os nós sob o nó `profile/empLocation/` no perfil de usuário AEM na estrutura CRXDE. Isso significa que o modelo de dados de formulário pode acessar a propriedade `city` do tipo `string` presente em qualquer nó sob o nó `profile/empLocation/`. No entanto, os nós que contêm a propriedade especificada devem seguir uma estrutura consistente.

1. Selecione **[!UICONTROL Salvar]** para salvar a configuração.

## Configurar pasta para configurações do serviço em nuvem {#cloud-folder}

>[!NOTE]
>
>A configuração da pasta de serviços em nuvem é necessária para configurar serviços em nuvem para serviços RESTful, SOAP e OData.

Todas as configurações do serviço de nuvem no AEM são consolidadas na pasta `/conf` no repositório AEM. Por padrão, a pasta `conf` contém a pasta `global`, na qual você pode criar configurações do serviço de nuvem. No entanto, é necessário ativá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais no `conf` para criar e organizar as configurações do serviço de nuvem.

Para definir a pasta de configurações do serviço de nuvem:

1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   * Consulte a documentação do [Navegador de Configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

   1. No **[!UICONTROL Navegador de Configuração]**, selecione a pasta `global` e selecione **[!UICONTROL Propriedades]**.

   1. Na caixa de diálogo **[!UICONTROL Propriedades da Configuração]**, habilite as **[!UICONTROL Configurações de Nuvem]**.

   1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. No **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um título para a pasta e habilite as **[!UICONTROL Configurações de Nuvem]**.
1. Selecione **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do serviço de nuvem.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando [especificações do Swagger](https://swagger.io/specification/) no formato JSON ou YAML em um arquivo de definição do Swagger. Para configurar o serviço Web RESTful nos serviços em nuvem AEM, certifique-se de que você tenha o arquivo Swagger no seu sistema de arquivos ou o URL onde o arquivo está hospedado.

Faça o seguinte para configurar os serviços RESTful:

1. Acesse **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** no menu suspenso **[!UICONTROL Tipo de serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione URL ou Arquivo no menu suspenso Swagger Source e especifique o URL do Swagger para o arquivo de definição do Swagger ou faça upload do arquivo Swagger a partir do seu sistema de arquivos local.
   * Com base na entrada do Source Swagger, os seguintes campos são pré-preenchidos com valores:

      * Esquema: os protocolos de transferência usados pela API REST. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na origem do Swagger.
      * Host: o nome do domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho base: o prefixo do URL para todos os caminhos da API. É um campo opcional.\
        Se necessário, edite os valores pré-preenchidos nesses campos.

   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key, Custom Authentication ou Mutual Authentication — para acessar o serviço RESTful e fornecer os detalhes de autenticação de acordo.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na lista suspensa **[!UICONTROL Local]** e especifique o nome do cabeçalho ou do parâmetro de consulta no campo **[!UICONTROL Nome do Parâmetro]**.

   Se você selecionar **[!UICONTROL Autenticação Mútua]** como o tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP](#mutual-authentication).

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Configuração do cliente HTTP do modelo de dados de formulário para otimizar o desempenho {#fdm-http-client-configuration}

O modelo de dados de formulário [!DNL Experience Manager Forms] ao integrar com serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.
Execute as seguintes etapas para configurar o cliente HTTP do modelo de dados de formulário:

1. Faça logon na Instância do Autor [!DNL Experience Manager Forms] como administrador e acesse os pacotes do console da Web [!DNL Experience Manager]. A URL padrão é [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Selecione **[!UICONTROL Configuração do Cliente Http do Modelo de Dados de Formulário para a fonte de dados REST]**.

1. Na caixa de diálogo [!UICONTROL Configuração do Cliente Http do Modelo de Dados de Formulário para a fonte de dados REST]:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no campo **[!UICONTROL Limite de conexão no total]**. O valor padrão é de 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota no campo **[!UICONTROL Limite de conexão por rota]**. O valor padrão é 2 conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida ativa, no campo **[!UICONTROL Keep alive]**. O valor padrão é de 15 segundos.

   * No campo **[!UICONTROL Tempo limite de conexão]**, especifique a duração pela qual o servidor [!DNL Experience Manager Forms] aguarda o estabelecimento de uma conexão. O valor padrão é de 10 segundos.

   * Especifique o período máximo de inatividade entre dois pacotes de dados no campo **[!UICONTROL Tempo limite do soquete]**. O valor padrão é de 30 segundos.

## Configurar serviços Web SOAP {#configure-soap-web-services}

Os serviços Web baseados em SOAP são descritos usando as [especificações WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Para configurar o serviço da Web com base em SOAP nos serviços de nuvem AEM, verifique se você tem o URL WSDL para o serviço da Web e faça o seguinte:

1. Acesse **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço Web SOAP]** no menu suspenso **[!UICONTROL Tipo de Serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço Web.
   * Ponto de Extremidade de Serviço. Especifique um valor neste campo para substituir o ponto final de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, Custom Authentication, X509 Token ou Mutual Authentication — para acessar o serviço SOAP e fornecer os detalhes da autenticação.

     Se você selecionar **[!UICONTROL X509 Token]** como o Tipo de autenticação, configure o Certificado X509. Para obter mais informações, consulte [Configurar certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique o alias do KeyStore para o certificado X509 no campo **[!UICONTROL Alias da Chave]**. Especifique o tempo, em segundos, até que a solicitação de autenticação permaneça válida, no campo **[!UICONTROL Tempo de vida]**. Opcionalmente, selecione para assinar o corpo da mensagem ou o cabeçalho do carimbo de data e hora, ou ambos.

     Se você selecionar **[!UICONTROL Autenticação Mútua]** como o tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP](#mutual-authentication).

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem do serviço Web SOAP.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData nos serviços em nuvem AEM, verifique se você tem o URL raiz do serviço para o serviço e faça o seguinte:

>[!NOTE]
>
>O modelo de dados de formulário dá suporte a [OData versão 4](https://www.odata.org/documentation/).
>Para obter um guia passo a passo para configurar o Microsoft Dynamics 365, online ou no local, consulte [Configuração OData do Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Acesse **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** na lista suspensa **[!UICONTROL Tipo de Serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL da Raiz de Serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica ou Autenticação Personalizada — para acessar o serviço OData e fornecer os detalhes de autenticação de acordo.

   >[!NOTE]
   >
   >Selecione o tipo de autenticação OAuth 2.0 para se conectar aos serviços do Microsoft Dynamics usando o endpoint OData como a raiz de serviço.

1. Selecione **Criar** para criar a configuração de nuvem para o serviço OData.

## Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP {#mutual-authentication}

Quando você habilita a autenticação mútua para o modelo de dados de formulário, a fonte de dados e o Servidor AEM executando o modelo de dados de formulário autenticam a identidade um do outro antes de compartilhar quaisquer dados. Você pode usar autenticação mútua para conexões REST e SOAP (fontes de dados). Para configurar a autenticação mútua para um modelo de dados de formulário no seu ambiente do AEM Forms:

1. Carregar a chave privada (certificado) para o servidor [!DNL AEM Forms]. Para fazer upload da chave privada:
   1. Faça logon no servidor [!DNL AEM Forms] como administrador.
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**. Selecione o usuário `fd-cloudservice` e selecione **[!UICONTROL Propriedades]**.
   1. Abra a guia **[!UICONTROL Armazenamento de chaves]**, expanda a opção **[!UICONTROL Adicionar chave privada do arquivo do Armazenamento de chaves]**, carregue o arquivo do Armazenamento de chaves, especifique os aliases, as senhas e selecione **[!UICONTROL Enviar]**. O certificado é carregado.  O alias da chave privada é mencionado no certificado e definido ao criar o certificado.
1. Faça upload do certificado de confiança para o armazenamento global de confiança. Para fazer upload do certificado:
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Repositório de Confiança]**.
   1. Expanda a opção **[!UICONTROL Adicionar certificado do arquivo CER]**, selecione **[!UICONTROL Selecionar arquivo de certificado]**, carregue o certificado e selecione **[!UICONTROL Enviar]**.
1. Configure os serviços Web [SOAP](#configure-soap-web-services) ou [RESTful](#configure-restful-web-services) como fonte de dados e selecione **[!UICONTROL Autenticação mútua]** como tipo de autenticação. Se você configurar vários certificados autoassinados para o usuário `fd-cloudservice`, especifique o Nome do Alias da Chave para o certificado.

## Próximas etapas {#next-steps}

Você configurou as fontes de dados. Em seguida, crie um modelo de dados de formulário ou, se já tiver criado um modelo de dados de formulário sem uma fonte de dados, associe-o às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](/help/forms/using/create-form-data-models.md) para obter detalhes.
