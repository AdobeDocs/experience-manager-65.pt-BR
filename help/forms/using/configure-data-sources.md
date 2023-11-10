---
title: Configurar fontes de dados
description: Saiba como configurar diferentes tipos de fontes de dados para criar modelos de dados de formulário.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: d39b4b1d921fc93a4871b74469953f2dfc5c470b
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 1%

---

# Configurar fontes de dados{#configure-data-sources}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | Este artigo |


![Integração de dados](do-not-localize/data-integeration.png)

A Integração de dados do AEM Forms permite configurar e conectar-se a diferentes fontes de dados. Os seguintes tipos são prontos para uso. No entanto, com pouca personalização, também é possível integrar outras fontes de dados.

* Bancos de dados relacionais - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS, postgreSQL e Sybase
* Perfil de usuário AEM
* Serviços Web RESTful
* Serviços da Web com base em SOAP
* Serviços OData

A integração de dados é compatível com OAuth2.0([Código de autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação básica e Autenticação de chave de API tipos prontos para uso e permite a implementação de autenticação personalizada para acessar serviços da Web. Enquanto os serviços RESTful, baseados em SOAP e OData são configurados no AEM Cloud Service, o JDBC para bancos de dados relacionais e conector para perfil de usuário do AEM AEM são configurados no console da Web do.

## Configurar banco de dados relacional {#configure-relational-database}

Você pode configurar bancos de dados relacionais usando a Configuração do Console da Web AEM. Faça o seguinte:

1. Ir para o console da Web do AEM em `https://server:host/system/console/configMgr`.
1. Procure **[!UICONTROL Fonte de dados agrupada da conexão Apache Sling]** configuração. Toque para abrir a configuração no modo de edição.
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
   > 1. Acesse https://&#39;[server]:[porta]&#39;/system/console/crypto.
   > 1. No **[!UICONTROL Texto sem formatação]** especifique a senha ou qualquer string para criptografar e toque em **[!UICONTROL Protect]**.
   >
   >O texto criptografado é exibido no campo Texto protegido que você pode especificar na configuração.

1. Ativar **[!UICONTROL Teste ao tomar emprestado]** ou **[!UICONTROL Testar na devolução]** para especificar que os objetos sejam validados antes de serem emprestados ou retornados de e para o pool, respectivamente.
1. Especifique uma consulta SQL SELECT no **[!UICONTROL Consulta de validação]** para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Com base no seu banco de dados, especifique uma das seguintes opções:

   * SELECT 1 (MySQL e MS SQL)
   * SELECIONE 1 no duplo (Oracle)

1. Toque **[!UICONTROL Salvar]** para salvar a configuração.

   >[!NOTE]
   >
   > Se o Modelo de dados do Forms contiver um objeto que seja uma palavra-chave reservada para o banco de dados relacional, ele poderá causar problemas de adição, atualização ou recuperação de dados. Portanto, evite usar esses objetos no Modelo de dados de formulário.

## Configurar perfil de usuário do AEM {#configure-aem-user-profile}

Você pode configurar o perfil de usuário AEM usando a configuração do Conector de perfil de usuário no Console da Web AEM. Faça o seguinte:

1. Acesse o console da Web do AEM em https://&#39;[server]:[porta]&quot;sistema/console/configMgr.
1. Procure **[!UICONTROL Integrações de dados do AEM Forms - Configuração do conector de perfil do usuário]** e toque para abrir a configuração no modo de edição.
1. Na caixa de diálogo Configuração do conector de perfil de usuário, você pode adicionar, remover ou atualizar propriedades de perfil de usuário. As propriedades especificadas estão disponíveis para uso no modelo de dados de formulário. Use o seguinte formato para especificar as propriedades do perfil do usuário:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >A variável **&#42;** no exemplo acima, indica todos os nós sob `profile/empLocation/` nó no perfil de usuário AEM na estrutura CRXDE. Isso significa que o modelo de dados de formulário pode acessar a variável `city` propriedade do tipo `string` presente em qualquer nó sob o `profile/empLocation/` nó. No entanto, os nós que contêm a propriedade especificada devem seguir uma estrutura consistente.

1. Toque **[!UICONTROL Salvar]** para salvar a configuração.

## Configurar pasta para configurações do serviço em nuvem {#cloud-folder}

>[!NOTE]
>
>A configuração da pasta de serviços em nuvem é necessária para configurar serviços em nuvem para serviços RESTful, SOAP e OData.

Todas as configurações do Cloud Service no AEM são consolidadas no `/conf` pasta no repositório AEM. Por padrão, a variável `conf` a pasta contém o `global` pasta onde você pode criar configurações do cloud service. No entanto, é necessário ativá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais no `conf` para criar e organizar configurações do cloud service.

Para definir a pasta de configurações do serviço de nuvem:

1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

   1. No **[!UICONTROL Navegador de configuração]**, selecione o `global` pasta e toque em **[!UICONTROL Propriedades]**.

   1. No **[!UICONTROL Propriedades de configuração]** caixa de diálogo, ativar **[!UICONTROL Configurações da nuvem]**.

   1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. No **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
1. Toque **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do cloud service.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando [Especificações do Swagger](https://swagger.io/specification/) no formato JSON ou YAML em um arquivo de definição do Swagger. Para configurar o serviço Web RESTful nos serviços em nuvem AEM, certifique-se de que você tenha o arquivo Swagger no seu sistema de arquivos ou o URL onde o arquivo está hospedado.

Faça o seguinte para configurar os serviços RESTful:

1. Ir para **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione URL ou Arquivo no menu suspenso Origem do Swagger e especifique o URL do Swagger para o arquivo de definição do Swagger ou faça upload do arquivo Swagger a partir do seu sistema de arquivos local.
   * Com base na entrada de Origem do Swagger, os seguintes campos são pré-preenchidos com valores:

      * Esquema: os protocolos de transferência usados pela API REST. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na origem do Swagger.
      * Host: o nome do domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho base: o prefixo do URL para todos os caminhos da API. É um campo opcional.\
        Se necessário, edite os valores pré-preenchidos nesses campos.

   * Selecione o tipo de autenticação — None, OAuth2.0([Código de autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação básica, Chave de API, Autenticação personalizada ou Autenticação mútua — para acessar o serviço RESTful e, de acordo, fornecer detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na lista suspensa **[!UICONTROL Nome do parâmetro]** em conformidade.

   Se você selecionar **[!UICONTROL Autenticação mútua]** como o tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços da web RESTful e SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Configuração do cliente HTTP do modelo de dados de formulário para otimizar o desempenho {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] o modelo de dados de formulário ao integrar com os serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.
Execute as seguintes etapas para configurar o cliente HTTP do modelo de dados de formulário:

1. Efetue logon no [!DNL Experience Manager Forms] Instância do autor como administrador e acesse [!DNL Experience Manager] pacotes do console da web. O URL padrão é [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Toque **[!UICONTROL Configuração do cliente Http do modelo de dados de formulário para fonte de dados REST]**.

1. No [!UICONTROL Configuração do cliente Http do modelo de dados de formulário para fonte de dados REST] diálogo:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no **[!UICONTROL Limite de conexão total]** campo. O valor padrão é de 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota na **[!UICONTROL Limite de conexão por rota]** campo. O valor padrão é 2 conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida ativa, em **[!UICONTROL Manter vivo]** campo. O valor padrão é de 15 segundos.

   * Especificar a duração, para a qual o [!DNL Experience Manager Forms] o servidor aguarda uma conexão ser estabelecida, no campo **[!UICONTROL Tempo limite da conexão]** campo. O valor padrão é de 10 segundos.

   * Especifique o período máximo de inatividade entre dois pacotes de dados no **[!UICONTROL Tempo limite do soquete]** campo. O valor padrão é de 30 segundos.

## Configurar serviços da Web SOAP {#configure-soap-web-services}

Os serviços da Web baseados em SOAP são descritos usando [Especificações da Web Services Description Language (WSDL)](https://www.w3.org/TR/wsdl). Para configurar o serviço da Web com base em SOAP em serviços na nuvem AEM, verifique se você tem o URL WSDL para o serviço da Web e faça o seguinte:

1. Ir para **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço da Web SOAP]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço Web.
   * Terminal de serviço. Especifique um valor neste campo para substituir o ponto final de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica, Autenticação Personalizada, Token X509 ou Autenticação Mútua — para acessar o serviço SOAP e fornecer os detalhes de autenticação de acordo.

     Se você selecionar **[!UICONTROL X509 Token]** como o Authentication type, configure o certificado X509. Para obter mais informações, consulte [Configurar certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique o alias do KeyStore para o certificado X509 na **[!UICONTROL Alias da chave]** campo. Especifique o tempo, em segundos, até que a solicitação de autenticação permaneça válida, no **[!UICONTROL Tempo de vida]** campo. Opcionalmente, selecione para assinar o corpo da mensagem ou o cabeçalho do carimbo de data e hora, ou ambos.

     Se você selecionar **[!UICONTROL Autenticação mútua]** como o tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços da web RESTful e SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem do serviço da Web SOAP.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData nos serviços em nuvem AEM, verifique se você tem o URL raiz do serviço para o serviço e faça o seguinte:

>[!NOTE]
>
>Suporte ao modelo de dados de formulário [OData versão 4](https://www.odata.org/documentation/).
>Para obter um guia passo a passo para configurar o Microsoft Dynamics 365, online ou no local, consulte [Configuração OData do Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL da Raiz de Serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica ou Autenticação Personalizada — para acessar o serviço OData e fornecer os detalhes de autenticação de acordo.

   >[!NOTE]
   >
   >Você deve selecionar o tipo de autenticação OAuth 2.0 para se conectar aos serviços do Microsoft Dynamics usando o ponto de extremidade OData como raiz de serviço.

1. Toque **Criar** para criar a configuração de nuvem para o serviço OData.

## Autenticação mútua baseada em certificado para serviços da web RESTful e SOAP {#mutual-authentication}

Quando você habilita a autenticação mútua para o modelo de dados de formulário, a fonte de dados e o Servidor AEM executando o modelo de dados de formulário autenticam a identidade um do outro antes de compartilhar quaisquer dados. Você pode usar autenticação mútua para conexões REST e SOAP (fontes de dados). Para configurar a autenticação mútua para um modelo de dados de formulário no seu ambiente do AEM Forms:

1. Fazer upload da chave privada (certificado) para [!DNL AEM Forms] servidor. Para fazer upload da chave privada:
   1. Faça logon no [!DNL AEM Forms] servidor como administrador.
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**. Selecione o `fd-cloudservice` usuário e toque em **[!UICONTROL Propriedades]**.
   1. Abra o **[!UICONTROL Armazenamento de chaves]** , expanda a **[!UICONTROL Adicionar chave de privacidade do arquivo do KeyStore]** , carregue o arquivo do KeyStore, especifique os aliases, senhas e toque em **[!UICONTROL Enviar]**. O certificado é carregado.  O alias da chave privada é mencionado no certificado e definido ao criar o certificado.
1. Faça upload do certificado de confiança para o armazenamento global de confiança. Para fazer upload do certificado:
   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Armazenamento de confiança]**.
   1. Expanda a **[!UICONTROL Adicionar certificado do arquivo CER]** opção, toque em **[!UICONTROL Selecionar arquivo de certificado]**, carregue o certificado e toque em **[!UICONTROL Enviar]**.
1. Configurar [SOAP](#configure-soap-web-services) ou [RESTful](#configure-restful-web-services) serviços da web como fonte de dados e selecione **[!UICONTROL Autenticação mútua]** como o tipo de autenticação. Se você configurar vários certificados autoassinados para `fd-cloudservice` usuário, especifique o Alias da Chave para o certificado.

## Próximas etapas {#next-steps}

Você configurou as fontes de dados. Em seguida, crie um modelo de dados de formulário ou, se já tiver criado um modelo de dados de formulário sem uma fonte de dados, associe-o às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](/help/forms/using/create-form-data-models.md) para obter detalhes.
