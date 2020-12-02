---
title: Integração com o Salesforce
seo-title: Integração com o Salesforce
description: Saiba mais sobre a integração de AEM com o Salesforce.
seo-description: Saiba mais sobre a integração de AEM com o Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 1%

---


# Integração com o Salesforce {#integrating-with-salesforce}

A integração do Salesforce com o AEM fornece recursos de gerenciamento de lead e aproveita os recursos existentes fornecidos prontamente pelo Salesforce. Você pode configurar AEM para publicar clientes potenciais no Salesforce e criar componentes que acessam dados diretamente do Salesforce.

A integração bidirecional e extensível entre AEM e Salesforce permite:

* Organizações para usar e atualizar totalmente os dados para aprimorar a experiência do cliente.
* Participação do marketing para atividades de vendas.
* Organizações para transmitir e receber dados automaticamente de um armazenamento de dados do Salesforce.

Este documento descreve o seguinte:

* como configurar os Cloud Services do Salesforce (configurar AEM para integração com o Salesforce).
* como usar informações de cliente potencial/contato do Salesforce no Contexto do cliente e para personalização.
* como usar o modelo de fluxo de trabalho do Salesforce para publicar AEM usuários como resulta no salesforce.
* como criar um componente que mostra dados do Salesforce.

## Configurar AEM para integração com o Salesforce {#configuring-aem-to-integrate-with-salesforce}

Para configurar AEM para integração com o Salesforce, é necessário configurar primeiro um aplicativo de acesso remoto no Salesforce. Em seguida, você configura o serviço de nuvem salesforce para apontar para esse aplicativo de acesso remoto.

>[!NOTE]
>
>Você pode criar uma conta gratuita de desenvolvedor no Salesforce.

Para configurar AEM para integração com o Salesforce:

>[!CAUTION]
>
>É necessário instalar o pacote de integração [API do Salesforce Force](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/com.adobe.cq.mcm.salesforce.content#) antes de continuar com o procedimento. Para obter mais detalhes sobre como trabalhar com pacotes, consulte a página [Como trabalhar com pacotes](/help/sites-administering/package-manager.md#package-share).

1. Em AEM, navegue até **Cloud Services**. Em Serviços de terceiros, clique em **Configurar agora** em **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Crie uma nova configuração, por exemplo, **developer**.

   >[!NOTE]
   >
   >A nova configuração redireciona para uma nova página: **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Esse é exatamente o mesmo valor que você precisa especificar no URL de retorno de chamada ao criar o aplicativo de acesso remoto no Salesforce. Esses valores devem corresponder.

1. Faça logon em sua conta do salesforce (ou, se você não tiver uma, crie uma em [https://developer.force.com](https://developer.force.com).)
1. No Salesforce, navegue até **Criar** > **Aplicativos** para acessar **Aplicativos conectados** (em versões anteriores do salesforce, o fluxo de trabalho era **Implantar** > **Acesso Remoto**).
1. Clique em **Novo** para conectar AEM com o Salesforce.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Digite o **Nome do aplicativo conectado**, **Nome da API** e **Email do contato**. Marque a caixa de seleção **Ativar configurações OAuth** e digite o **URL de retorno de chamada** e adicione um escopo OAuth (por exemplo, acesso total). O URL de retorno de chamada é semelhante a: `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   Altere o nome do servidor/número da porta e o nome da página para corresponder à sua configuração.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Clique em **Salvar** para salvar a configuração do salesforce. O Salesforce cria um **consumer key** e **consumer secret**, necessários para AEM configuração.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Talvez seja necessário aguardar vários minutos (até 15 minutos) para que o aplicativo de acesso remoto no Salesforce seja ativado.

1. Em AEM, navegue até **Cloud Services** e navegue até a configuração do salesforce criada anteriormente (por exemplo, **developer**). Clique em **Editar** e insira a chave do cliente e o segredo do cliente em salesforce.com.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | URL de login | Este é o Ponto Final de Autorização do Salesforce. Seu valor é pré-preenchido e serve a maioria dos casos. |
   |---|---|
   | Chave do cliente | Digite o valor obtido na página Registro de aplicativo de acesso remoto em salesforce.com |
   | Segredo do cliente | Digite o valor obtido na página Registro de aplicativo de acesso remoto em salesforce.com |

1. Clique em **Conectar-se ao Salesforce** para conectar-se. O Salesforce solicita que você permita que sua configuração se conecte ao salesforce.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   No AEM, uma caixa de diálogo de confirmação é aberta informando que você se conectou com êxito.

1. Navegue até a página raiz do site e clique em **Propriedades da página**. Em seguida, selecione **Cloud Services** e adicione **Salesforce** e selecione a configuração correta (por exemplo, **developer**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   Agora, você pode usar o modelo de fluxo de trabalho para postar clientes potenciais no Salesforce e criar componentes que acessam dados do Salesforce.

## Exportar usuários AEM como Salesforce Leads {#exporting-aem-users-as-salesforce-leads}

Se você quiser exportar um usuário AEM como um cliente potencial salesforce, é necessário configurar o fluxo de trabalho para publicar os clientes potenciais no salesforce.

Para exportar AEM usuários como o Salesforce leva:

1. Navegue até o fluxo de trabalho do Salesforce em `http://localhost:4502/workflow` clicando com o botão direito do mouse no fluxo de trabalho **Exportar do Salesforce.com** e clicando em **Start**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Selecione o usuário AEM que deseja criar como cliente potencial como **Carga** para este fluxo de trabalho (home -> usuários). Certifique-se de selecionar o nó de perfil do usuário, pois ele contém informações como **GIID**, **familyName**, e assim por diante, que estão mapeadas para os campos **FirstName** e **LastName** do cliente potencial do Salesforce.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Antes de iniciar esse fluxo de trabalho, há determinados campos obrigatórios que um nó principal no AEM deve ter antes de ser publicado no Salesforce. Estes são **providedName**, **familyName**, **empresa** e **email**. Para ver uma lista completa de mapeamento entre AEM usuário e o cliente potencial Salesforce, consulte [Configuração de Mapeamento entre AEM usuário e o cliente potencial Slaesforce.](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. Clique em **OK**. As informações do usuário são exportadas para salesforce.com. Você pode verificá-lo em salesforce.com.

   >[!NOTE]
   >
   >Os registros de erros mostrarão se um cliente potencial é importado. Consulte o log de erros para obter mais informações.

### Configuração do fluxo de trabalho de exportação do Salesforce.com {#configuring-the-salesforce-com-export-workflow}

Talvez seja necessário configurar o fluxo de trabalho de exportação do Salesforce.com para equipará-lo à configuração correta do Salesforce.com ou para fazer outras alterações.

Para configurar o fluxo de trabalho de exportação do Salesforce.com:

1. Vá até `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Abra a etapa Exportar do Salesforce.com, selecione a guia **Argumentos** e selecione se a configuração correta está selecionada e clique em **OK**. Além disso, se você quiser que o fluxo de trabalho recrie um cliente potencial que foi excluído no Salesforce, marque a caixa de seleção.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Clique em **Salvar** para salvar as alterações.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### Mapeamento da configuração entre AEM usuário e Salesforce Lead {#mapping-configuration-between-aem-user-and-salesforce-lead}

Para visualização ou edição da configuração de mapeamento atual entre um usuário AEM e um cliente potencial Salesforce, abra o Configuration Manager: `https://<hostname>:<port>/system/console/configMgr` e procure **Configuração de Mapeamento de Chumbo do Salesforce**.

1. Abra o Configuration Manager clicando em **Web Console** ou indo diretamente para `https://<hostname>:<port>/system/console/configMgr.`
1. Procure **Configuração de Mapeamento de Chumbo do Salesforce**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Altere os mapeamentos, conforme necessário. O mapeamento padrão segue o padrão **aemUserAttribute=sfLeadAttribute**. Clique em **Salvar** para salvar as alterações.

## Configuração do Salesforce Client Context Store {#configuring-salesforce-client-context-store}

O repositório de contexto do cliente salesforce mostra informações adicionais sobre o usuário conectado no momento do que o que já está disponível no AEM. Ele obtém essas informações adicionais do Salesforce, dependendo da conexão do usuário com o Salesforce.

Para fazer isso, é necessário configurar o seguinte:

1. Vincule um usuário AEM com uma ID do Salesforce por meio do componente do Salesforce Connect.
1. Adicione os Dados do Perfil do Salesforce na página de contexto do cliente para configurar quais propriedades você deseja visualizar.
1. (Opcional) Crie um segmento que use os dados do Salesforce Client Context Store.

### Vincular um usuário AEM com uma ID do Salesforce {#linking-an-aem-user-with-a-salesforce-id}

É necessário mapear um usuário AEM com uma ID do Salesforce para carregá-lo no contexto do cliente. Em um cenário real, você estaria vinculando com base em dados conhecidos do usuário com validação. Para fins demonstrativos, neste procedimento, você usa o componente **Salesforce Connect**.

1. Navegue até um site da Web em AEM, faça logon e arraste e solte o componente **Salesforce Connect** do sidekick.

   >[!NOTE]
   >
   >Se o componente **Salesforce Connect** não estiver disponível, vá para a visualização **Design** e selecione-a para disponibilizá-la na visualização **Editar**.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   Quando você arrasta o componente para a página, ele exibe **Link para Salesforce=Off**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >Este componente é apenas para fins de demonstração. Para cenários do mundo real, haveria outro processo para vincular/igualar usuários a clientes potenciais.

1. Depois de arrastar o componente na página, abra-o para configurá-lo. Selecione a configuração, o tipo de contato e o cliente potencial ou contato do Salesforce e clique em **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM vincula o usuário ao contato ou cliente potencial do Salesforce.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Adicionando dados do Salesforce ao contexto do cliente {#adding-salesforce-data-to-client-context}

Você pode carregar os dados do usuário do Salesforce no Contexto do cliente para usá-los na personalização:

1. Abra o contexto do cliente que deseja estender navegando até ele, por exemplo, `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. Arraste o componente **Dados do Perfil do Salesforce** para o contexto do cliente.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. Clique no componente com o duplo do mouse para abri-lo. Selecione **Adicionar Item** e selecione uma propriedade na lista suspensa. Adicione quantas propriedades desejar e selecione **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Agora, você vê propriedades específicas do Salesforce exibidas no contexto do cliente.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Criação de um segmento usando dados do Salesforce Client Context Store {#building-a-segment-using-data-from-salesforce-client-context-store}

Você pode criar um segmento que usa dados do Salesforce Client Context Store. Para fazer isso:

1. Navegue até a segmentação no AEM indo para **Ferramentas** > **Segmentação** ou indo para [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Crie ou atualize um segmento para incluir dados do Salesforce. Para obter mais informações, consulte [Segmentação](/help/sites-administering/campaign-segmentation.md).

## Pesquisando clientes potenciais {#searching-leads}

AEM é fornecido com um componente de pesquisa de amostra que pesquisa clientes potenciais no Salesforce de acordo com os critérios especificados. Este componente mostra como usar a API REST do Salesforce para pesquisar objetos do salesforce. É necessário vincular uma página com uma configuração do Salesforce para acionar uma chamada para salesforce.com.

>[!NOTE]
>
>Este é um componente de amostra que mostra como usar a API REST do Salesforce para query de objetos do Salesforce. Use-o como exemplo para criar componentes mais complexos com base em suas necessidades.

Para usar este componente:

1. Navegue até a página onde deseja usar essa configuração. Abra as propriedades da página e selecione **Cloud Services.** Clique em  **Adicionar** serviços, selecione  **** Salesforcecee a configuração apropriada e clique em  **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Arraste o componente de pesquisa do Salesforce para a página (desde que tenha sido ativado). Para ativá-lo, vá para o modo Design e adicione-o à área apropriada).

   ![chlimage_1-29](assets/chlimage_1-21.jpeg)

1. Abra o componente de pesquisa e especifique os parâmetros de pesquisa e clique em **OK.**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM exibe os clientes em potencial especificados em seu componente de pesquisa que correspondem aos critérios especificados.

   ![chlimage_1-87](assets/chlimage_1-87.png)

