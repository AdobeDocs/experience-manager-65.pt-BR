---
title: Configuração da ação Enviar
description: O Forms permite configurar uma ação de envio para definir como um formulário adaptável é processado após o envio. Você pode usar ações de envio integradas ou escrever as suas próprias ações do zero.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2593'
ht-degree: 2%

---

# Configuração da ação Enviar {#configuring-the-submit-action}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |


## Introdução às ações de envio {#introduction-to-submit-actions}

Uma ação de envio é acionada quando um usuário clica no botão Enviar em um formulário adaptável. É possível configurar a ação enviar no formulário adaptável. Os formulários adaptáveis fornecem algumas ações de envio prontas para uso. Você pode copiar e estender as ações de envio padrão para criar sua própria ação de envio. No entanto, com base em seus requisitos, você pode gravar e registrar sua própria ação de envio para processar dados no formulário enviado. A ação de envio pode usar [envio síncrono ou assíncrono](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Você pode configurar uma ação de envio na seção **Envio** das propriedades do Contêiner de formulário adaptável, na barra lateral.

![Configurar Ação de Envio](assets/thank-you-setting.png)

Configurar ação de envio

As ações de envio padrão disponíveis com formulários adaptáveis são:

* Enviar para endpoint REST
* Enviar e-mail
* Enviar PDF por e-mail
* Chamar um Forms Workflow
* Enviar usando modelo de dados do formulário
* Ação de envio do portal do Forms
* Chamar um fluxo de trabalho de AEM
* Enviar para o Power Automate

>[!NOTE]
>
>A ação de envio Enviar PDF por email é aplicável somente a formulários adaptáveis que usam o modelo XFA como modelo de formulário.

>[!NOTE]
>
>Verifique se a pasta [AEM_Installation_Diretory]\crx-quickstart\temp\datamanager\ASM
>existe. O diretório é necessário para armazenar temporariamente anexos. Caso o diretório não exista, crie-o.

>[!CAUTION]
>
>Se você [preencher previamente](../../forms/using/prepopulate-adaptive-form-fields.md) um modelo de formulário, modelo de dados de formulário ou formulário adaptável baseado em esquema com reclamação de dados XML ou JSON para um esquema (esquema XML, esquema JSON, modelo de formulário ou modelo de dados de formulário) cujos dados não contêm as marcas &lt;afData>, &lt;afBoundData> e &lt;/afUnboundData>, os dados de campos não vinculados (campos não vinculados são campos de formulário adaptável sem a propriedade [bindref](../../forms/using/prepopulate-adaptive-form-fields.md)) do formulário adaptável serão perdidos.

Você pode escrever uma ação de envio personalizada para formulários adaptáveis para atender ao seu caso de uso. Para obter mais informações, consulte [Escrevendo ação enviar personalizada para formulários adaptáveis](../../forms/using/custom-submit-action-form.md).

## Enviar para endpoint REST {#submit-to-rest-endpoint}

A opção de envio **Enviar para o ponto de extremidade REST** passa os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. Você pode adicionar o nome dos campos a serem solicitados. O formato da solicitação é:

`{fieldName}={request parameter name}`

Como mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

Você também pode **Habilitar a solicitação POST** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor Experience Manager que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor Experience Manager. Por exemplo, /content/forms/af/SampleForm.html. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

![Configurando Ação De Envio De Ponto De Extremidade Rest](assets/action-config.png)

Configurar Ação De Envio De Ponto De Extremidade Rest

>[!NOTE]
>
>Para passar os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

### A Post enviou dados para um recurso ou ponto de extremidade rest externo  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Use a ação **Enviar para o Ponto de Extremidade REST** para postar os dados enviados em uma URL restante. A URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, /content/restEndPoint. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

Para publicar dados em um servidor externo, forneça um URL. O formato do URL é https://host:port/path_to_rest_end_point. Configure o caminho para lidar com a solicitação POST de forma anônima.

![Mapeamento para valores de campo passados como parâmetros da Página de Agradecimento](assets/post-enabled-actionconfig.png)

No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para publicar dados capturados usando `param1` é:

`String data=request.getParameter("param1");`

Da mesma forma, os parâmetros que você usa para lançar dados XML e anexos são `dataXml` e `attachments`.

Por exemplo, você usa esses dois parâmetros no script para analisar dados para um ponto final rest. Você usa a seguinte sintaxe para armazenar e analisar os dados:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

Neste exemplo, `data` armazena os dados XML e `att` armazena os dados de anexo.

## Enviar e-mail {#send-email}

A ação de envio **Enviar Email** envia um email para um ou mais destinatários após o envio bem-sucedido do formulário. O email gerado pode conter dados de formulário em um formato predefinido.

>[!NOTE]
>
>Todos os campos de formulário devem ter nomes de elementos diferentes, mesmo que sejam colocados em painéis diferentes), para incluir dados de formulário em um email.

## Enviar PDF por e-mail {#send-pdf-via-email}

A ação de envio **Enviar PDF via Email** envia um email com um PDF contendo dados de formulário para um ou mais destinatários após o envio bem-sucedido do formulário.

>[!NOTE]
>
>Essa ação de envio está disponível para formulários adaptáveis baseados em XFA e formulários de adaptação baseados em XSD que têm o modelo Documento de registro.

## Chamar um Forms Workflow {#invoke-a-forms-workflow}

A opção de envio **Enviar para Forms Workflow** envia um xml de dados e anexos de arquivo (se houver) para um LiveCycle de Adobe ou AEM Forms existente no processo JEE.

Para obter informações sobre como configurar a ação de envio Enviar para Forms Workflow, consulte [Envio e processamento de dados de formulário usando fluxos de trabalho de formulários](../../forms/using/submit-form-data-livecycle-process.md).

## Enviar usando modelo de dados do formulário {#submit-using-form-data-model}

As gravações de ação de envio **Enviar usando o Modelo de Dados de Formulário** enviaram dados de formulário adaptáveis para o objeto de modelo de dados especificado em um modelo de dados de formulário para sua fonte de dados. Ao configurar a ação de envio, você pode escolher um objeto de modelo de dados cujos dados enviados deseja gravar na origem de dados.

Além disso, você pode enviar um anexo de formulário usando um modelo de dados de formulário e um Documento de registro (DoR) para a fonte de dados.

Para obter informações sobre o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

## Ação de envio do portal do Forms {#forms-portal-submit-action}

A opção **Enviar Ação do Forms Portal** disponibiliza dados de formulário por meio de um AEM Forms Portal.

Para obter mais informações sobre o Portal do Forms e a ação de envio, consulte [Componente de rascunhos e envios](../../forms/using/draft-submission-component.md).

## Chamar um fluxo de trabalho de AEM {#invoke-an-aem-workflow}

A Ação de Envio **[!UICONTROL Chamar um Fluxo de Trabalho de AEM]** associa um Formulário Adaptável a um [Fluxo de Trabalho de AEM](/help/sites-developing/workflows-models.md). Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente na instância do Autor. É possível salvar o arquivo de dados, os anexos e o Documento de registro na pasta relativa ou na carga útil do fluxo de trabalho ou em uma variável. Se o workflow estiver marcado para armazenamento de dados externo, a opção variable estará disponível e não a opção payload. É possível selecionar na lista de variáveis disponíveis para o modelo de fluxo de trabalho. Se o workflow estiver marcado para armazenamento de dados externo em um estágio posterior e não no momento da criação do workflow, verifique se as configurações de variável necessárias estão em vigor.

Antes de usar a ação de envio **Invocar um Fluxo de Trabalho de AEM**, [defina as configurações de DS de Experience Manager](../../forms/using/configuring-the-processing-server-url.md). Para obter informações sobre como criar um Fluxo de Trabalho do AEM, consulte [Fluxos de trabalho centrados em formulários no OSGi](../../forms/using/aem-forms-workflow.md).

A ação enviar coloca o seguinte no local da carga útil do fluxo de trabalho. No entanto, observe que somente a opção Variável será exibida se o modelo de fluxo de trabalho estiver marcado para armazenamento de dados externo, e não a opção de carga útil.

* **Arquivo de dados**: contém dados enviados para o Formulário adaptável. Você pode usar a opção **[!UICONTROL Caminho do Arquivo de Dados]** para especificar o nome do arquivo e o caminho do arquivo relativo à carga. Por exemplo, o caminho `/addresschange/data.xml` cria uma pasta chamada `addresschange` e a coloca em relação à carga. Você também pode especificar apenas `data.xml` para enviar apenas dados enviados sem criar uma hierarquia de pastas. Use a opção de variável e selecione a variável na lista de variáveis disponíveis para o modelo de fluxo de trabalho.

>[!NOTE]
>
>As variáveis podem ser usadas independentemente de o modelo de fluxo de trabalho estar ou não marcado para armazenamento de dados externo.

* **Anexos**: você pode usar a opção **[!UICONTROL Caminho do Anexo]** para especificar o nome da pasta para armazenar os anexos carregados no Formulário Adaptável. A pasta é criada em relação à carga útil. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

* **Documento de Registro**: contém o Documento de Registro gerado para o Formulário Adaptável. Você pode usar a opção **[!UICONTROL Caminho do Documento de Registro]** para especificar o nome do arquivo do Documento de Registro e o caminho do arquivo relativo à carga útil. Por exemplo, o caminho `/addresschange/DoR.pdf` cria uma pasta chamada `addresschange` relativa à carga e coloca a `DoR.pdf` relativa à carga. Você também pode especificar apenas `DoR.pdf` para salvar apenas o documento de registro sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

## Enviar para o Power Automate {#microsoft-power-automate}

Você pode configurar um Formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente. Estes são alguns exemplos do que você pode fazer após integrar um formulário adaptável ao Microsoft® Power Automate:

* Usar dados adaptáveis do Forms em processos de negócios do Power Automate
* Use o Power Automate para enviar dados capturados para mais de 500 fontes de dados ou qualquer API disponível publicamente
* Realizar cálculos complexos em dados capturados
* Salve os dados do Forms adaptável em sistemas de armazenamento em uma programação predefinida

O editor Forms adaptável fornece a **ação de envio Chamar um fluxo do Microsoft® Power Automate** para enviar dados de formulários adaptáveis, anexos e Documento de registro para o fluxo da nuvem do Power Automate. Para usar a ação Enviar para enviar dados capturados para o Microsoft® Power Automate, [Conecte sua instância do AEM Forms com o Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md)

Após uma configuração bem-sucedida, use a ação de envio [Chamar um fluxo do Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) para enviar dados a um Fluxo do Power Automate.

## Enviar para a Lista Microsoft® SharePoint{#submit-to-sharedrive}

>[!NOTE]
>
>O recurso Enviar para a lista do Microsoft® SharePoint foi introduzido com o AEM 6.5 Forms Service Pack 19 (6.5.19.0).

A ação de envio **[!UICONTROL Enviar para o SharePoint]** conecta um Formulário adaptável com um Armazenamento Microsoft® SharePoint. É possível enviar o arquivo de dados de formulário, os anexos ou o Documento de Registro para o Armazenamento do Microsoft® Sharepoint conectado.

### Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

Para conectar um formulário adaptável à lista Microsoft® SharePoint:

1. [Criar uma Configuração de Lista do SharePoint](#create-sharepoint-list-configuration): ela conecta o AEM Forms ao Armazenamento de Lista do Microsoft® Sharepoint.
1. [Usar a ação de envio **Enviar usando o Modelo de Dados de Formulário** em um Formulário Adaptável](#use-submit-using-fdm): ela envia seus dados de Formulário Adaptável para o Microsoft® SharePoint configurado.

#### Criar uma configuração de lista do SharePoint {#create-sharepoint-list-configuration}

Para conectar o AEM Forms à sua lista do Microsoft® Sharepoint:

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Lista do SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.
1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` de seu aplicativo do portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Sites.Manage.All` na guia **Microsoft® Graph** para fornecer permissões de leitura/gravação. Adicione a permissão `AllSites.Manage` na guia **Sharepoint** para interagir remotamente com os dados do SharePoint.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

     >[!NOTE]
     >
     >O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.
1. Selecione **[!UICONTROL Site do SharePoint]** e **[!UICONTROL Lista do SharePoint]** na lista suspensa.
1. Toque em **[!UICONTROL Criar]** para criar a configuração de nuvem do Microsoft® SharePointList.

#### Usar o Enviar usando o Modelo de dados de formulário em um Formulário adaptável {#use-submit-using-fdm}

Você pode usar a configuração da Lista do SharePoint criada em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento de Lista do SharePoint em um Formulário adaptável como:

1. [Criar um modelo de dados de formulário usando o Microsoft](/help/forms/using/create-form-data-model.md)
1. [Configurar o modelo de dados do formulário para recuperar e enviar dados](/help/forms/using/work-with-form-data-model.md#configure-services)
1. [Criar um Formulário Adaptável](/help/forms/using/create-adaptive-form.md).
1. [Configurar a ação Enviar usando um Modelo de dados de formulário](/help/forms/using/configuring-submit-actions.md#submit-using-form-data-model-submit)

Ao enviar o formulário, os dados são salvos no Armazenamento de Lista do Microsoft® Sharepoint especificado.

>[!NOTE]
>
>Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
>* coluna de imagem
>* coluna de metadados
>* coluna de pessoa
>* coluna de dados externos


>[!NOTE]
>
>Para definir valores de uma configuração, [Gere Configurações OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=pt-BR#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implante a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR#deployment-process) na instância do Cloud Service.

## Revalidação do lado do servidor no formulário adaptável {#server-side-revalidation-in-adaptive-form}

Normalmente, em qualquer sistema de captura de dados online, os desenvolvedores colocam algumas validações do JavaScript no lado do cliente para aplicar algumas regras de negócios. Mas em navegadores modernos, os usuários finais têm uma maneira de ignorar essas validações e fazer envios manualmente usando várias técnicas, como o Console DevTools do navegador da Web. Tais técnicas também são válidas para formulários adaptativos. Um desenvolvedor de formulários pode criar várias lógicas de validação, mas tecnicamente, os usuários finais podem ignorar essas lógicas de validação e enviar dados inválidos para o servidor. Dados inválidos violariam as regras de negócios aplicadas por um autor de formulários.

O recurso de revalidação do lado do servidor também permite executar as validações que um autor de formulários adaptáveis forneceu ao projetar um formulário adaptável no servidor. Isso evita qualquer possível comprometimento dos envios de dados e violações das regras de negócios representadas em termos de validações de formulário.

### O que validar no servidor? {#what-to-validate-on-server-br}

Todas as validações de campo prontas para uso de um formulário adaptável que são executadas novamente no servidor são:

* Obrigatório
* Cláusula de Imagem de Validação
* Expressão de validação

### Ativar a validação do lado do servidor {#enabling-server-side-validation-br}

Use a **Revalidar no servidor** em Contêiner de Formulário Adaptável na barra lateral para habilitar ou desabilitar a validação no servidor para o formulário atual.

![Habilitando A Validação No Lado Do Servidor](assets/revalidate-on-server.png)

Ativar a validação do lado do servidor

Se o usuário final ignorar essas validações e enviar os formulários, o servidor executará novamente a validação. Se a validação falhar no final do servidor, a transação de envio será interrompida. O usuário final é apresentado ao formulário original novamente. Os dados capturados e os dados enviados são apresentados ao usuário como um erro.

>[!NOTE]
>
>A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca do cliente separada para validações e não misturá-la com outras coisas, como estilo de HTML e manipulação de DOM na mesma biblioteca do cliente.

### Suporte a funções personalizadas em expressões de validação {#supporting-custom-functions-in-validation-expressions-br}

Às vezes, se houver regras de validação complexas, o script de validação exato residirá em funções personalizadas e o autor chamará essas funções personalizadas da expressão de validação de campo. Para tornar esta biblioteca de funções personalizada conhecida e disponível durante a execução de validações no lado do servidor, o autor do formulário pode configurar o nome da biblioteca do cliente AEM na guia **Básico** das propriedades do Contêiner de formulário adaptável, conforme mostrado abaixo.

![Dando suporte a funções personalizadas em Expressões de Validação](assets/clientlib-cat.png)

Suporte a funções personalizadas em expressões de validação

O autor pode configurar a biblioteca JavaScript personalizada por formulário adaptável. Na biblioteca, mantenha somente as funções reutilizáveis, que dependem de bibliotecas de terceiros de jquery e underscore.js.

## Tratamento de erros na ação de envio {#error-handling-on-submit-action}

Como parte das diretrizes de segurança e proteção do Experience Manager, configure páginas de erro personalizadas como 404.jsp e 500.jsp. Esses manipuladores são chamados quando ao enviar um formulário 404 ou 500 erros são exibidos. Os manipuladores também são chamados quando esses códigos de erro são acionados no nó do Publish.

Para obter mais informações, consulte [Personalizando páginas mostradas pelo Manipulador de Erros](/help/sites-developing/customizing-errorhandler-pages.md).
