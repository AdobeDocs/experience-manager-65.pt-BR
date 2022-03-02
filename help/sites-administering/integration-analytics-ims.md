---
title: Integração com o Adobe Analytics usando IMS
description: Saiba mais sobre como integrar AEM com o Adobe Analytics usando o IMS
source-git-commit: eb05fb92491932e4c2489c5adb533bbbae1d2870
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# Integração com o Adobe Analytics usando IMS {#integration-with-adobe-analytics-using-ims}

A integração do AEM com o Adobe Analytics por meio da API do Analytics Standard requer a configuração do Adobe IMS (Identity Management System) usando o Adobe Developer Console.

>[!NOTE]
>
>O suporte para a API 2.0 do Adobe Analytics Standard é novo no AEM 6.5.12.0. Essa versão da API é compatível com a autenticação IMS.
>
>O uso da API do Adobe Analytics Classic 1.4 no AEM ainda é compatível com versões anteriores. O [A API do Analytics Classic usa a autenticação de credenciais do usuário](/help/sites-administering/adobeanalytics-connect.md).
>
>A seleção da API é orientada pelo método de autenticação usado para a integração do AEM/Analytics.
>
>Outras informações estão também disponíveis no [Migração para as APIs 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Pré-requisitos {#prerequisites}

Antes de iniciar este procedimento:

* [Suporte a Adobe](https://helpx.adobe.com/br/contact/enterprise-support.ec.html) precisa provisionar sua conta para:

   * Console Adobe
   * Console do desenvolvedor do Adobe
   * Adobe Analytics e
   * Adobe IMS (Sistema Identity Management)

* O Administrador de sistema da sua organização deve usar o Admin Console para adicionar os desenvolvedores necessários em sua organização aos perfis de produto relevantes.

   * Isso fornece aos desenvolvedores específicos permissões para ativar integrações no Console do desenvolvedor do Adobe.
   * Para obter mais detalhes, consulte [Gerenciar desenvolvedores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuração de um IMS - Geração de uma chave pública {#configuring-an-ims-configuration-generating-a-public-key}

O primeiro estágio da configuração é criar uma Configuração IMS no AEM e gerar a Chave pública.

1. Em AEM abra o **Ferramentas** menu.
1. No **Segurança** seção selecionar **Configurações do Adobe IMS**.
1. Selecionar **Criar** para abrir o **Configuração de conta técnica do Adobe IMS**.
1. Uso da lista suspensa em **Configuração na nuvem**, selecione **Adobe Analytics**.
1. Ativar **Criar novo certificado** e insira um novo alias.
1. Confirme com **Criar certificado**.

   ![](assets/integrate-analytics-io-01.png)

1. Selecionar **Baixar** ou **Baixar chave pública**) para baixar o arquivo na unidade local, de modo que ele esteja pronto para uso quando [configuração do IMS para integração do Adobe Analytics com o AEM](#configuring-ims-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenha essa configuração aberta, ela será necessária novamente quando [Concluir a configuração IMS no AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-analytics-io-02.png)

## Configuração do IMS para integração do Adobe Analytics com o AEM {#configuring-ims-for-adobe-analytics-integration-with-aem}

Usando o Console do desenvolvedor do Adobe, é necessário criar um Projeto (integração) com o Adobe Analytics (para uso do AEM) e, em seguida, atribuir os privilégios necessários.

### Criação do projeto {#creating-the-project}

Abra o Console do desenvolvedor do Adobe para criar um Projeto com o Adobe Analytics que AEM usará:

1. Abra o Console do desenvolvedor do Adobe para Projetos:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Quaisquer projetos que você tiver serão mostrados. Selecionar **Criar novo projeto** - a localização e utilização dependerão:

   * Se você ainda não tiver um projeto, **Criar novo projeto** será central, inferior.
      ![Criar novo projeto - Primeiro projeto](assets/integration-analytics-io-02.png)
   * Caso já tenha projetos existentes, eles serão listados e **Criar novo projeto** estará no canto superior direito.
      ![Criar novo projeto - Vários projetos](assets/integration-analytics-io-03.png)


1. Selecionar **Adicionar ao projeto** seguida de **API**:

   ![Introdução ao novo projeto](assets/integration-analytics-io-10.png)

1. Selecionar **Adobe Analytics**, em seguida **Próximo**:

   >[!NOTE]
   >
   >Se você estiver inscrito no Adobe Analytics, mas não o vir listado, verifique a variável [Pré-requisitos](#prerequisites).

   ![Adicionar uma API](assets/integration-analytics-io-12.png)

1. Selecionar **Conta de serviço (JWT)** como o tipo de autenticação, continue com **Próximo**:

   ![Selecionar tipo de autenticação](assets/integration-analytics-io-12a.png)

1. **Fazer upload de sua chave pública** e quando terminar, continue com **Próximo**:

   ![Fazer upload de sua chave pública](assets/integration-analytics-io-13.png)

1. Revise as credenciais e continue com **Próximo**:

   ![Revisar credenciais](assets/integration-analytics-io-15.png)

1. Selecione os perfis de produto necessários e continue com **Salvar API configurada**:

   ![Selecionar perfis de produto necessários](assets/integration-analytics-io-16.png)

1. A configuração será confirmada.

### Atribuir privilégios à integração {#assigning-privileges-to-the-integration}

Agora, você deve atribuir os privilégios necessários à integração:

1. Abra o Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navegar para **Produtos** (barra de ferramentas superior), em seguida, selecione **Adobe Analytics - &lt;*your-tenant-id*>** (no painel esquerdo).
1. Selecionar **Perfis de produto**, seu espaço de trabalho necessário na lista apresentada. Por exemplo, Espaço de trabalho padrão.
1. Selecionar **Credenciais da API**, em seguida, a configuração de integração necessária.
1. Selecionar **Editor** como **Função do produto**; em vez de **Observador**.

## Detalhes armazenados para o Projeto de integração do Console do Desenvolvedor do Adobe {#details-stored-for-the-ims-integration-project}

No console Adobe Developer Projects, é possível ver uma lista de todos os seus projetos de integração:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Selecione uma entrada de projeto específica para mostrar mais detalhes sobre a configuração. Dentre elas:

* Visão geral do projeto
* Insights
* Credenciais
   * Conta de serviço (JWT)
      * Detalhes da credencial
      * Gerar JWT
* APIS
   * Por exemplo, Adobe Analytics

Alguns deles, você precisará concluir a integração do Adobe Analytics no AEM.

## Concluir a configuração IMS no AEM {#completing-the-ims-configuration-in-aem}

Ao retornar para AEM, é possível concluir a configuração do IMS adicionando os valores necessários do projeto de integração do Analytics:

1. Retorne ao [Configuração IMS aberta no AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Selecione **Próximo**.

1. Aqui você pode usar o [Detalhes armazenados para o Projeto de integração do Console do Desenvolvedor do Adobe](#details-stored-for-the-ims-integration-project):

   * **Título**: Seu texto.
   * **Servidor de autorização**: Copie/cole no `aud` da **Carga** seção abaixo, por exemplo `https://ims-na1.adobelogin.com` no exemplo abaixo
   * **Chave da API**: Copie isso do **Credenciais** da seção [Visão geral do projeto](#details-stored-for-the-ims-integration-project)
   * **Segredo do cliente**: Gere isso no [Guia Segredo do cliente da seção Conta de serviço (JWT)](#details-stored-for-the-ims-integration-project)e copiar
   * **Carga**: Copie isso do [Guia Gerar JWT da seção Conta de Serviço (JWT)](#details-stored-for-the-ims-integration-project)

   ![Detalhes da configuração do AEM IMS](assets/integrate-analytics-io-10.png)

1. Confirme com **Criar**.

1. Sua configuração do Adobe Analytics será exibida no console AEM.

   ![Configuração IMS](assets/integrate-analytics-io-11.png)

## Confirmação da configuração IMS {#confirming-the-ims-configuration}

Para confirmar que a configuração está funcionando como esperado:

1. Abrir:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por exemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Selecione sua configuração.
1. Selecionar **Verificar integridade** na barra de ferramentas, seguida por **Verificar**.

   ![Configuração IMS - Verificar integridade](assets/integrate-analytics-io-12.png)

1. Se bem-sucedido, você verá uma mensagem de confirmação.

## Configuração do serviço Adobe Analytics Cloud {#configuring-the-adobe-analytics-cloud-service}

A configuração agora pode ser mencionada para um Cloud Service para usar a API do Analytics Standard:

1. Abra o **Ferramentas** menu. Em seguida, no **Cloud Services** seção , selecione **Cloud Services herdados**.
1. Role para baixo até **Adobe Analytics** e selecione **Configurar agora**.

   O **Criar configuração** será aberta.

1. Insira um **Título** e, se quiser, um **Nome** (se deixado em branco, isso será gerado a partir do título).

   Você também pode selecionar o modelo necessário (se mais de um estiver disponível).

1. Confirme com **Criar**.

   O **Editar componente** será aberta.

1. Insira os detalhes na **Configurações do Analytics** guia :

   * **Autenticação**: IMS

   * **Configuração IMS**: selecione o nome da Configuração IMS

1. Clique em **Conectar-se ao Analytics** para inicializar a conexão com o Adobe Analytics.

   Se a conexão for bem-sucedida, a mensagem **Conexão bem-sucedida** é exibida.

1. Selecionar **OK** na mensagem.

1. Complete outros parâmetros, conforme necessário, seguido de **OK** na caixa de diálogo para confirmar a configuração.

1. Agora você pode continuar com [Adicionar uma estrutura do Analytics](/help/sites-administering/adobeanalytics-connect.md) para configurar parâmetros que serão enviados para o Adobe Analytics.
