---
title: Configurar fontes de dados
seo-title: Configure data sources
description: Saiba como configurar diferentes tipos de fontes de dados e aproveitar para criar modelos de dados de formulário.
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: e4aaef48ce7d6e49e9a76f78a74b7dea127f6cce
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 1%

---

# Configurar fontes de dados{#configure-data-sources}

![Integração de dados](do-not-localize/data-integeration.png)

A Integração de dados do AEM Forms permite configurar e se conectar a fontes de dados diferentes. Os seguintes tipos são suportados prontos para uso. No entanto, com pouca personalização, também é possível integrar outras fontes de dados.

* Bancos de dados relacionais - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS e Sybase
* Perfil de usuário AEM
* Serviços Web RESTful
* Serviços Web baseados em SOAP
* Serviços OData

A integração de dados oferece suporte aos tipos de autenticação OAuth2.0, Basic Authentication e API Key prontos para uso e permite implementar autenticação personalizada para acessar serviços da Web. Embora os serviços RESTful, baseados em SOAP e OData sejam configurados nos Serviços da nuvem AEM, o JDBC para bancos de dados relacionais e o conector para AEM perfil de usuário são configurados AEM console da Web.

## Configurar banco de dados relacional {#configure-relational-database}

Você pode configurar bancos de dados relacionais usando AEM Configuração do Console da Web. Faça o seguinte:

1. Vá para AEM console da Web em `https://server:host/system/console/configMgr`.
1. Procure por **[!UICONTROL Fonte de dados agrupada da conexão Apache Sling]** configuração. Toque em para abrir a configuração no modo de edição.
1. Na caixa de diálogo de configuração, especifique os detalhes do banco de dados que deseja configurar, como:

   * Nome da fonte de dados
   * Propriedade do serviço da fonte de dados que armazena o nome da fonte de dados
   * Nome da classe Java para o driver JDBC
   * URI de conexão JDBC
   * Nome de usuário e senha para estabelecer conexão com o driver JDBC

   >[!NOTE]
   >
   >Certifique-se de criptografar informações confidenciais como senhas antes de configurar a fonte de dados. Para criptografar:
   >
   > 1. Vá para https://&#39;[server]:[porta]&#39;/system/console/crypto.
   > 1. No **[!UICONTROL Texto sem formatação]** , especifique a senha ou qualquer string a ser criptografada e toque em **[!UICONTROL Protect]**.

   >
   >O texto criptografado aparece no campo Texto protegido que pode ser especificado na configuração.

1. Habilitar **[!UICONTROL Teste em linha de crédito]** ou **[!UICONTROL Testar no retorno]** para especificar que os objetos sejam validados antes de serem emprestados ou retornados de e para o pool, respectivamente.
1. Especifique uma consulta SQL SELECT no **[!UICONTROL Consulta de validação]** para validar conexões do pool. A consulta deve retornar pelo menos uma linha. Com base no seu banco de dados, especifique um dos seguintes:

   * SELECT 1 (MySQL e MS SQL)
   * SELECIONE 1 de duplo (Oracle)

1. Toque **[!UICONTROL Salvar]** para salvar a configuração.

   >[!NOTE]
   >
   > Se o Forms Data Model contiver um objeto que é uma palavra-chave reservada para seu banco de dados relacional, ele poderá levar a problemas de adição, atualização ou recuperação de dados. Portanto, evite usar esses objetos em seu Modelo de dados de formulário.

## Configurar AEM perfil de usuário {#configure-aem-user-profile}

Você pode configurar AEM perfil de usuário usando a configuração do Conector de perfil de usuário AEM console da Web. Faça o seguinte:

1. Vá para AEM console da Web em https://&#39;[server]:[porta]&#39;system/console/configMgr.
1. Procure por **[!UICONTROL Integrações de dados do AEM Forms - Configuração do conector do perfil de usuário]** e toque para abrir a configuração no modo de edição.
1. Na caixa de diálogo Configuração do conector do perfil do usuário, é possível adicionar, remover ou atualizar as propriedades do perfil do usuário. As propriedades especificadas estão disponíveis para uso no modelo de dados de formulário. Use o seguinte formato para especificar as propriedades do perfil de usuário:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >O **&#42;** no exemplo acima significa todos os nós sob o `profile/empLocation/` no AEM perfil do usuário na estrutura CRXDE. Isso significa que o modelo de dados de formulário pode acessar a variável `city` propriedade do tipo `string` presente em qualquer nó sob o `profile/empLocation/` nó . No entanto, os nós que contêm a propriedade especificada devem seguir uma estrutura consistente.

1. Toque **[!UICONTROL Salvar]** para salvar a configuração.

## Configurar pasta para configurações do serviço de nuvem {#cloud-folder}

>[!NOTE]
>
>A configuração da pasta de serviços em nuvem é necessária para configurar os serviços em nuvem para os serviços RESTful, SOAP e OData.

Todas as configurações do serviço em nuvem no AEM são consolidadas no `/conf` pasta no repositório AEM. Por padrão, a variável `conf` A pasta contém o `global` pasta onde você pode criar configurações do serviço de nuvem. No entanto, é necessário ativá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais em `conf` para criar e organizar configurações do serviço de nuvem.

Para configurar a pasta das configurações do serviço de nuvem:

1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações do serviço de nuvem.

   1. No **[!UICONTROL Navegador de configuração]**, selecione o `global` pasta e toque **[!UICONTROL Propriedades]**.

   1. No **[!UICONTROL Propriedades da configuração]** caixa de diálogo, habilitar **[!UICONTROL Configurações da nuvem]**.

   1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. No **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
1. Toque **[!UICONTROL Criar]** para criar a pasta habilitada para as configurações do serviço de nuvem.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando [Especificações do Swagger](https://swagger.io/specification/) no formato JSON ou YAML em um arquivo de definição Swagger. Para configurar o serviço Web RESTful nos serviços em nuvem do AEM, verifique se você tem o arquivo Swagger no sistema de arquivos ou o URL onde o arquivo está hospedado.

Faça o seguinte para configurar os serviços RESTful:

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione URL ou Arquivo na lista suspensa Fonte do Swagger e especifique o URL do Swagger correspondente para o arquivo de definição do Swagger ou faça o upload do arquivo Swagger de seu sistema de arquivos local.
   * Com base na entrada Origem do Swagger, os seguintes campos são preenchidos previamente com valores:

      * Regime: Os protocolos de transferência usados pela REST API. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na origem do Swagger.
      * Host: O nome de domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho básico: O prefixo do URL para todos os caminhos da API. É um campo opcional.\
         Se necessário, edite os valores pré-preenchidos para esses campos.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API, Autenticação Personalizada ou Autenticação Mútua — para acessar o serviço RESTful e, portanto, forneça detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   Se você selecionar **[!UICONTROL Autenticação Mútua]** como tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com os serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.
Execute as seguintes etapas para configurar o cliente HTTP do modelo de dados de formulário:

1. Faça logon em [!DNL Experience Manager Forms] Instância do autor como administrador e acesse [!DNL Experience Manager] pacotes do console da web. O URL padrão é [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Toque **[!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST]**.

1. No [!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST] caixa de diálogo:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no **[!UICONTROL Limite de conexão no total]** campo. O valor padrão é 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota no **[!UICONTROL Limite de conexão por rota]** campo. O valor padrão é 2 conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida viva, no **[!UICONTROL Manter vivo]** campo. O valor padrão é de 15 segundos.

   * Especifique a duração, para a qual a variável [!DNL Experience Manager Forms] O servidor aguarda que uma conexão seja estabelecida no **[!UICONTROL Tempo limite da conexão]** campo. O valor padrão é de 10 segundos.

   * Especifique o período máximo de tempo para a inatividade entre dois pacotes de dados no **[!UICONTROL Tempo limite do soquete]** campo. O valor padrão é de 30 segundos.

## Configurar serviços Web SOAP {#configure-soap-web-services}

Os serviços da Web baseados em SOAP são descritos usando [Especificações de WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Para configurar o serviço da Web baseado em SOAP nos serviços em nuvem do AEM, verifique se você tem o URL WSDL para o serviço da Web e faça o seguinte:

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço Web SOAP]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço da Web.
   * Terminal de serviço. Especifique um valor nesse campo para substituir o ponto de extremidade de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Autenticação Personalizada, Token X509 ou Autenticação Mútua — para acessar o serviço SOAP e, portanto, forneça os detalhes para autenticação.

      Se você selecionar **[!UICONTROL Token X509]** como o Tipo de autenticação, configure o certificado X509. Para obter mais informações, consulte [Configurar certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique o alias do KeyStore para o certificado X509 no **[!UICONTROL Alias da chave]** campo. Especifique o tempo, em segundos, até que a solicitação de autenticação permaneça válida, no **[!UICONTROL Tempo de vida]** campo. Como opção, selecione para assinar o corpo da mensagem ou o cabeçalho do carimbo de data e hora ou ambos.

      Se você selecionar **[!UICONTROL Autenticação Mútua]** como tipo de autenticação, consulte [Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço da Web SOAP.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por seu URL raiz do serviço. Para configurar um serviço OData nos serviços em nuvem do AEM, verifique se você tem o URL raiz do serviço para o serviço e faça o seguinte:

>[!NOTE]
>
>Suporte ao modelo de dados de formulário [OData versão 4](https://www.odata.org/documentation/).
>Para obter o guia passo a passo para configurar o Microsoft Dynamics 365, online ou no local, consulte [Configuração do Microsoft Dynamics OData](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](../../forms/using/configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL raiz do serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica ou Autenticação Personalizada — para acessar o serviço OData e fornecer os detalhes para autenticação.

   >[!NOTE]
   >
   >Você deve selecionar o tipo de autenticação OAuth 2.0 para se conectar aos serviços do Microsoft Dynamics usando o ponto de extremidade OData como a raiz do serviço.

1. Toque **Criar** para criar a configuração de nuvem para o serviço OData.

## Autenticação mútua baseada em certificado para serviços Web RESTful e SOAP {#mutual-authentication}

Ao habilitar a autenticação mútua para o modelo de dados de formulário, a fonte de dados e o Servidor AEM que executa o modelo de dados de formulário autenticam a identidade uns dos outros antes de compartilhar quaisquer dados. Você pode usar a autenticação mútua para conexões baseadas em REST e SOAP (fontes de dados). Para configurar a autenticação mútua para um modelo de dados de formulário no ambiente AEM Forms:

1. Fazer upload da chave privada (certificado) para [!DNL AEM Forms] servidor. Para fazer upload da chave privada:
   1. Faça logon no [!DNL AEM Forms] como administrador.
   1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**. Selecione o `fd-cloudservice` usuário e toque **[!UICONTROL Propriedades]**.
   1. Abra o **[!UICONTROL Armazenamento de chaves]** , expanda a **[!UICONTROL Adicionar chave privada do arquivo KeyStore]** , faça upload do arquivo KeyStore, especifique os aliases, senhas e toque em **[!UICONTROL Enviar]**. O Certificado é carregado.  O alias da chave privada é mencionado no certificado e definido ao criar o certificado.
1. Faça upload do certificado de confiança no Armazenamento de Confiança Global. Para fazer upload do certificado:
   1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Armazenamento de confiança]**.
   1. Expanda o **[!UICONTROL Adicionar certificado do arquivo CER]** opção, toque em **[!UICONTROL Selecionar arquivo de certificado]**, faça upload do certificado e toque em **[!UICONTROL Enviar]**.
1. Configurar [SOAP](#configure-soap-web-services) ou [RESTful](#configure-restful-web-services) serviços da Web como fonte de dados e selecione **[!UICONTROL Autenticação mútua]** como o tipo de autenticação. Se você configurar vários certificados autoassinados para `fd-cloudservice` usuário, especifique o nome do Alias da chave para o certificado.

## Próximas etapas {#next-steps}

As fontes de dados foram configuradas. Em seguida, é possível criar um modelo de dados de formulário ou, se já tiver criado um modelo de dados de formulário sem uma fonte de dados, associá-lo às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](/help/forms/using/create-form-data-models.md) para obter detalhes.
