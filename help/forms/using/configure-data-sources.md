---
title: Configurar fontes de dados
seo-title: Configurar fontes de dados
description: Saiba como configurar diferentes tipos de fontes de dados e aproveitar para criar modelos de dados de formulário.
seo-description: Saiba como configurar diferentes tipos de fontes de dados e aproveitar para criar modelos de dados de formulário.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: 9df949b0069dad7fc1627977097cec5546cd845f
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---


# Configurar fontes de dados{#configure-data-sources}

![](do-not-localize/data-integeration.png)

A Integração de dados do AEM Forms permite configurar e conectar-se a fontes de dados diferentes. Os seguintes tipos são suportados prontamente. No entanto, com pouca personalização, também é possível integrar outras fontes de dados.

* Bancos de dados relacionais - MySQL, Microsoft SQL Server, IBM DB2 e Oracle RDBMS
* perfil de usuário do AEM
* Serviços Web RESTful
* Serviços Web baseados em SOAP
* Serviços OData

A integração de dados suporta os tipos de autenticação OAuth2.0, Autenticação básica e Chave de API prontos para uso e permite implementar autenticação personalizada para acessar serviços da Web. Embora os serviços RESTful, SOAP e OData estejam configurados em AEM cloud services, o JDBC para bancos de dados relacionais e o conector para o perfil de usuário do AEM são configurados no console da Web do AEM.

## Configurar banco de dados relacional {#configure-relational-database}

Você pode configurar bancos de dados relacionais usando a Configuração do console da Web do AEM. Faça o seguinte:

1. Vá para o console da Web do AEM em https://server:host/system/console/configMgr.
1. Procure a configuração **[!UICONTROL Apache Sling Connection Pooling DataSource]** . Toque em para abrir a configuração no modo de edição.
1. Na caixa de diálogo de configuração, especifique os detalhes do banco de dados que deseja configurar, como:

   * Nome da fonte de dados
   * Propriedade do serviço da fonte de dados que armazena o nome da fonte de dados
   * Nome da classe Java para o driver JDBC
   * URI de conexão JDBC
   * Nome de usuário e senha para estabelecer conexão com o driver JDBC

   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >Certifique-se de criptografar informações confidenciais, como senhas, antes de configurar a fonte de dados. Para criptografar:
   >
   >    
   >    
   >    1. Vá para https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. No campo Texto **** simples, especifique a senha ou qualquer string a ser criptografada e clique em **[!UICONTROL Proteger]**.

   >    
   >    
   >    
   >O texto criptografado aparece no campo Texto protegido que você pode especificar na configuração.

1. Ative **[!UICONTROL Testar emprestado]** ou **[!UICONTROL Testar ao Retornar]** para especificar que os objetos são validados antes de serem emprestados ou devolvidos de e para o pool, respectivamente.
1. Especifique um query SELECT SQL no campo Query **** Validação para validar conexões do pool. O query deve retornar pelo menos uma linha. Com base no banco de dados, especifique um dos seguintes:

   * SELECT 1 (MySQL e MS SQL)
   * SELECT 1 from dual (Oracle)

1. Toque em **[!UICONTROL Salvar]** para salvar a configuração.

## Configurar o perfil de usuário do AEM {#configure-aem-user-profile}

Você pode configurar o perfil do usuário do AEM usando a configuração do Conector do Perfil do usuário no console da Web do AEM. Faça o seguinte:

1. Vá para o console da Web do AEM em https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Procure Integrações de dados do **[!UICONTROL AEM Forms - Configuração]** do conector do Perfil do usuário e toque para abrir a configuração no modo de edição.
1. Na caixa de diálogo Configuração do conector do Perfil do usuário, você pode adicionar, remover ou atualizar as propriedades do perfil do usuário. As propriedades especificadas estarão disponíveis para uso no modelo de dados de formulário. Use o seguinte formato para especificar as propriedades do perfil do usuário:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >O ***** no exemplo acima indica todos os nós sob o `profile/empLocation/` nó no perfil de usuário do AEM na estrutura CRXDE. Isso significa que o modelo de dados de formulário pode acessar a `city` propriedade do tipo `string` presente em qualquer nó sob o `profile/empLocation/` nó. No entanto, os nós que contêm a propriedade especificada devem seguir uma estrutura consistente.

1. Toque em **[!UICONTROL Salvar]** para salvar a configuração.

## Configurar pasta para configurações do serviço de nuvem {#cloud-folder}

>[!NOTE]
A configuração da pasta de serviços em nuvem é necessária para configurar serviços em nuvem para os serviços RESTful, SOAP e OData.

Todas as configurações de serviço em nuvem no AEM são consolidadas na `/conf` pasta no repositório do AEM. Por padrão, a `conf` pasta contém a `global` pasta onde você pode criar configurações de serviço em nuvem. No entanto, é necessário ativá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais em `conf` para criar e organizar configurações de serviço em nuvem.

Para configurar a pasta das configurações do serviço de nuvem:

1. Vá até **[!UICONTROL Ferramentas > Geral > Navegador]** de configuração.
1. Faça o seguinte para ativar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

   1. No Navegador **[!UICONTROL de]** configuração, selecione a `global` pasta e toque em **[!UICONTROL Propriedades]**.

   1. Na caixa de diálogo Propriedades **** de configuração, ative Configurações **[!UICONTROL da]** nuvem.

   1. Toque em **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. No Navegador **** de configuração, toque em **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar configuração]** , especifique um título para a pasta e ative Configurações **[!UICONTROL da]** nuvem.
1. Toque em **[!UICONTROL Criar]** para criar a pasta ativada para configurações de serviço em nuvem.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando as especificações [](https://swagger.io/specification/) Swagger no formato JSON ou YAML em um arquivo de definição Swagger. Para configurar o serviço Web RESTful em AEM cloud services, verifique se você tem o arquivo Swagger no sistema de arquivos ou o URL no qual o arquivo está hospedado.

Faça o seguinte para configurar os serviços RESTful:

1. Vá até **[!UICONTROL Ferramentas > Cloud Service > Fontes]** de dados. Toque em para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações](../../forms/using/configure-data-sources.md#cloud-folder) de serviço em nuvem para obter informações sobre como criar e configurar uma pasta para configurações de serviço em nuvem.

1. Toque em **[!UICONTROL Criar]** para abrir o assistente **** Criar configuração de fonte de dados. Especifique um nome e, opcionalmente, um título para a configuração, selecione Serviço **** RESTful no menu suspenso Tipo **[!UICONTROL de]** serviço, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione URL ou Arquivo no menu suspenso Fonte do Swagger e especifique o URL do Swagger para o arquivo de definição do Swagger ou faça upload do arquivo Swagger do sistema de arquivos local.
   * Com base na entrada Origem do Swagger, os seguintes campos são pré-preenchidos com valores:

      * Regime: Os protocolos de transferência usados pela REST API. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na origem do Swagger.
      * Host: O nome do domínio ou endereço IP do host que serve a REST API. É um campo obrigatório.
      * Caminho básico: O prefixo de URL para todos os caminhos de API. É um campo opcional.\
         Se necessário, edite os valores pré-preenchidos para esses campos.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação básica, Chave da API ou Autenticação personalizada — para acessar o serviço RESTful e, portanto, fornecer detalhes para autenticação.

   Se você selecionar a chave **[!UICONTROL da]** API como o tipo de autenticação, especifique o valor para a chave da API. A chave da API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de query. Selecione uma dessas opções na lista suspensa **[!UICONTROL Local]** e especifique o nome do parâmetro header ou query no campo Nome **[!UICONTROL do]** parâmetro de acordo.

1. Toque em **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

## Configurar serviços Web SOAP {#configure-soap-web-services}

Os serviços Web baseados em SOAP são descritos usando as especificações [WSDL (](https://www.w3.org/TR/wsdl)Web Services Description Language). Para configurar o serviço da Web baseado em SOAP em AEM cloud services, verifique se você tem o URL WSDL para o serviço da Web e faça o seguinte:

1. Vá até **[!UICONTROL Ferramentas > Cloud Service > Fontes]** de dados. Toque em para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações](../../forms/using/configure-data-sources.md#cloud-folder) de serviço em nuvem para obter informações sobre como criar e configurar uma pasta para configurações de serviço em nuvem.

1. Toque em **[!UICONTROL Criar]** para abrir o assistente **** Criar configuração de fonte de dados. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL SOAP Web Service]** no menu suspenso Tipo **[!UICONTROL de]** serviço, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique o seguinte para o serviço da Web SOAP:

   * URL WSDL para o serviço da Web.
   * Terminal de serviço. Especifique um valor neste campo para substituir o ponto de extremidade de serviço mencionado em WSDL.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação básica, Autenticação personalizada ou Token X509 — para acessar o serviço SOAP e, portanto, fornecer os detalhes para autenticação.

      Se você selecionar o Token X509 como o tipo de autenticação, configure o certificado X509. Para obter mais informações, consulte [Configurar certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique o alias KeyStore para o certificado X509 no campo Alias **[!UICONTROL de]** chave. Especifique o tempo, em segundos, até que a solicitação de autenticação permaneça válida, no campo **[!UICONTROL Tempo de ativação]** . Como opção, selecione para assinar o corpo da mensagem ou o cabeçalho do carimbo de data e hora ou ambos.

1. Toque em **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço Web SOAP.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado pelo URL raiz do serviço. Para configurar um serviço OData em AEM cloud services, verifique se você tem o URL raiz do serviço e faça o seguinte:

>[!NOTE]
Para obter um guia passo a passo para configurar o Microsoft Dynamics 365, online ou no local, consulte Configuração [do](/help/forms/using/ms-dynamics-odata-configuration.md)Microsoft Dynamics OData.

1. Vá até **[!UICONTROL Ferramentas > Cloud Service > Fontes]** de dados. Toque em para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações](../../forms/using/configure-data-sources.md#cloud-folder) de serviço em nuvem para obter informações sobre como criar e configurar uma pasta para configurações de serviço em nuvem.

1. Toque em **[!UICONTROL Criar]** para abrir o assistente **** Criar configuração de fonte de dados. Especifique um nome e, opcionalmente, um título para a configuração, selecione Serviço **** OData no menu suspenso Tipo **[!UICONTROL de]** serviço, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL raiz do serviço para o serviço OData a ser configurado.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação básica ou Autenticação personalizada — para acessar o serviço OData e, portanto, fornecer os detalhes para autenticação.

   >[!NOTE]
   Você deve selecionar o tipo de autenticação OAuth 2.0 para se conectar aos serviços do Microsoft Dynamics usando o terminal OData como a raiz do serviço.

1. Toque em **Criar** para criar a configuração de nuvem para o serviço OData.

## Próximos passos {#next-steps}

Você configurou as fontes de dados. Em seguida, é possível criar um modelo de dados de formulário ou, se você já tiver criado um modelo de dados de formulário sem uma fonte de dados, associá-lo às fontes de dados que acabou de configurar. Consulte [Criar modelo](/help/forms/using/create-form-data-models.md) de dados de formulário para obter detalhes.
