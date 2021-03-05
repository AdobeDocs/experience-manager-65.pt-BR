---
title: Configuração da ação Enviar
seo-title: Configuração da ação Enviar
description: O Forms permite configurar uma ação de envio para definir como um formulário adaptável é processado após o envio. Você pode usar as ações de envio incorporadas ou escrever suas próprias ações do zero.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: 82fcc7ea1029f069aff95f50b3eb1a1581ec5c95
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 1%

---


# Configurar a ação Enviar{#configuring-the-submit-action}

## Introdução ao envio de ações {#introduction-to-submit-actions}

Uma ação Enviar é acionada quando um usuário clica no botão Enviar em um formulário adaptável. É possível configurar a ação de envio no formulário adaptável. Os formulários adaptáveis fornecem algumas ações de envio prontas para uso. Você pode copiar e estender as ações de envio padrão para criar sua própria ação de envio. No entanto, com base em suas necessidades, você pode gravar e registrar sua própria ação de envio para processar dados no formulário enviado. A ação de envio pode usar [envio síncrono ou assíncrono](../../forms/using/asynchronous-submissions-adaptive-forms.md).

Você pode configurar uma ação de envio na seção **Submission** das propriedades do Contêiner de formulário adaptável, na barra lateral.

![Configurar ação de envio](assets/thank-you-setting.png)

Configurar ação de envio

As ações de envio padrão disponíveis com formulários adaptáveis são:

* Enviar para ponto de extremidade REST
* Enviar e-mail
* Enviar PDF por email
* Chamar um fluxo de trabalho de formulários
* Enviar usando modelo de dados do formulário
* Ação de envio do portal de formulários
* Chamar um fluxo de trabalho do AEM

>[!NOTE]
>
>A ação Enviar PDF por envio de email é aplicável somente a formulários adaptáveis que usam o modelo XFA como modelo de formulário.

>[!NOTE]
>
>Certifique-se de que o [AEM_Installation_Diretory]\crx-quickstart\temp\datamanager\ASM folder
>existe. O diretório é necessário para armazenar anexos temporariamente. Se o diretório não existir, crie-o.

>[!CAUTION]
>
>Se você [preencher previamente](../../forms/using/prepopulate-adaptive-form-fields.md) um modelo de formulário, modelo de dados de formulário ou formulário adaptável baseado em esquema com reclamação de dados XML ou JSON para um esquema (esquema XML, esquema JSON, modelo de formulário ou modelo de dados de formulário) que seja de dados não conterá &lt;afData>, &lt;afBoundData> e &lt;/afUnboundData> tags, os dados dos campos não vinculados (Unbound campos limitados são campos de formulário adaptáveis sem a propriedade [bindref](../../forms/using/prepopulate-adaptive-form-fields.md)) do formulário adaptável é perdida.

Você pode escrever uma ação de envio personalizada para formulários adaptáveis para atender ao seu caso de uso. Para obter mais informações, consulte [Gravando ação de ação de Enviar personalizado para formulários adaptáveis](../../forms/using/custom-submit-action-form.md).

## Enviar para o ponto final REST {#submit-to-rest-endpoint}

A opção de envio **Enviar para o endpoint REST** passa os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. É possível adicionar o nome dos campos a serem solicitados. O formato da solicitação é:

`{fieldName}={request parameter name}`

Conforme mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

Você também pode **Habilitar solicitação POST** e fornecer um URL para postar a solicitação. Para enviar dados para o servidor do Experience Manager que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do Experience Manager. Por exemplo, /content/forms/af/SampleForm.html. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

![Configurar a ação de envio do ponto de extremidade restante](assets/action-config.png)

Configurar a ação de envio do ponto de extremidade restante

>[!NOTE]
Para transmitir os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

### Postar dados enviados para um recurso ou ponto final de repouso externo  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

Use a ação **Submit to REST Endpoint** para postar os dados enviados em um URL restante. O URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

Para postar dados em um servidor interno, forneça o caminho do recurso. Os dados são postados no caminho do recurso. Por exemplo, /content/restEndPoint. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

Para postar dados em um servidor externo, forneça um URL. O formato do URL é https://host:port/path_to_rest_end_point. Certifique-se de configurar o caminho para lidar com a solicitação POST anonimamente.

![Mapeamento para valores de campo passados como parâmetros da Página de agradecimento](assets/post-enabled-actionconfig.png)

No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para postar dados capturados usando `param1` é:

`String data=request.getParameter("param1");`

Da mesma forma, os parâmetros usados para publicar dados e anexos XML são `dataXml` e `attachments`.

Por exemplo, esses dois parâmetros são usados no script para analisar os dados em um ponto de extremidade de repouso. Use a seguinte sintaxe para armazenar e analisar os dados:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

Neste exemplo, `data` armazena os dados XML e `att` armazena os dados do anexo.

## Enviar e-mail {#send-email}

A ação de envio de **Email** envia um email para um ou mais recipients após o envio bem-sucedido do formulário. O email gerado pode conter dados de formulário em um formato predefinido.

>[!NOTE]
Todos os campos de formulário devem ter nomes de elemento diferentes, mesmo que sejam colocados em painéis diferentes), para incluir dados de formulário em um email.

## Enviar PDF por email {#send-pdf-via-email}

A ação de envio **Enviar PDF por email** envia um email com um PDF contendo dados de formulário para um ou mais recipients após o envio bem-sucedido do formulário.

>[!NOTE]
Essa ação de envio está disponível para formulários adaptáveis baseados em XFA e formulários de adaptação baseados em XSD que têm o modelo Documento de registro.

## Chamar um fluxo de trabalho de formulários {#invoke-a-forms-workflow}

A opção de envio **Enviar para o Forms Workflow** envia um xml de dados e anexos de arquivo (se houver) para um Adobe LiveCycle ou AEM Forms existente no processo JEE.

Para obter informações sobre como configurar a ação de envio do fluxo de trabalho Enviar para formulários , consulte [Enviar e processar os dados do formulário usando fluxos de trabalho de formulários](../../forms/using/submit-form-data-livecycle-process.md).

## Enviar usando modelo de dados do formulário {#submit-using-form-data-model}

A ação **Enviar usando o Modelo de dados de formulário** envia dados de formulário adaptáveis enviados para o objeto de modelo de dados especificado em um modelo de dados de formulário para a fonte de dados. Ao configurar a ação de envio, você pode escolher um objeto de modelo de dados cujos dados enviados deseja gravar de volta em sua fonte de dados.

Além disso, é possível enviar um anexo de formulário usando um modelo de dados de formulário e um Documento de registro (DoR) para a fonte de dados.

Para obter informações sobre o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](../../forms/using/data-integration.md).

## Ação de envio do portal de formulários {#forms-portal-submit-action}

A opção **Ação de envio do portal de formulários** disponibiliza os dados do formulário por meio de um Portal de formulários AEM.

Para obter mais informações sobre o Portal de formulários e a ação de enviar, consulte [Componentes de rascunhos e envios](../../forms/using/draft-submission-component.md).

## Chamar um fluxo de trabalho do AEM {#invoke-an-aem-workflow}

A ação de envio **Invocar um fluxo de trabalho do AEM** associa um formulário adaptável a um fluxo de trabalho do AEM. Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente no nó de processamento. Além disso, ele coloca o arquivo de dados, os anexos e o documento de registro, se aplicável, no local da carga do fluxo de trabalho.

Antes de usar a ação de envio **Invoke an AEM Workflow**, [configure as configurações do Experience Manager DS](../../forms/using/configuring-the-processing-server-url-.md). Para obter informações sobre como criar um fluxo de trabalho do AEM, consulte [Fluxos de trabalho centrados no formulário no OSGi](../../forms/using/aem-forms-workflow.md).

## Revalidação do lado do servidor no formulário adaptável {#server-side-revalidation-in-adaptive-form}

Normalmente, em qualquer sistema de captura de dados online, os desenvolvedores colocam algumas validações de JavaScript no lado do cliente para impor algumas regras de negócios. Mas nos navegadores modernos, os usuários finais têm como ignorar essas validações e fazer envios manualmente usando várias técnicas, como o Console DevTools do navegador Web. Essas técnicas também são válidas para formulários adaptáveis. Um desenvolvedor de formulários pode criar várias lógicas de validação, mas tecnicamente os usuários finais podem ignorar essas lógicas de validação e enviar dados inválidos para o servidor. Dados inválidos quebrariam as regras de negócios que um autor de formulários executou.

O recurso de revalidação do lado do servidor também permite executar as validações fornecidas por um autor de formulários adaptáveis ao projetar um formulário adaptável no servidor. Impede qualquer possível comprometimento de envios de dados e violações de regras comerciais representadas em termos de validações de formulários.

### O que validar no Servidor? {#what-to-validate-on-server-br}

Todas as validações de campo prontas para uso (OOTB) de um formulário adaptável que são executadas novamente no servidor são:

* Obrigatório
* Cláusula de Imagem de Validação
* Expressão de validação

### Ativando a validação do lado do servidor {#enabling-server-side-validation-br}

Use o **Revalidar no servidor** em Contêiner de formulário adaptável na barra lateral para ativar ou desativar a validação do lado do servidor para o formulário atual.

![Ativação da validação no lado do servidor](assets/revalidate-on-server.png)

Ativação da validação no lado do servidor

Se o usuário final ignorar essas validações e enviar os formulários, o servidor executará novamente a validação. Se a validação falhar no final do servidor, a transação de envio será interrompida. O usuário final é apresentado ao formulário original novamente. Os dados capturados e enviados são apresentados ao usuário como um erro.

>[!NOTE]
A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca cliente separada para validações e não misturá-la com outras coisas, como estilo HTML e manipulação DOM na mesma biblioteca do cliente.

### Suporte a funções personalizadas nas expressões de validação {#supporting-custom-functions-in-validation-expressions-br}

Às vezes, se houver regras de validação complexas, o script de validação exato residirá em funções personalizadas e o autor chamará essas funções personalizadas da expressão de validação de campo. Para tornar essa biblioteca de função personalizada conhecida e disponível durante a execução de validações do lado do servidor, o autor do formulário pode configurar o nome da biblioteca do cliente AEM na guia **Basic** das propriedades do Contêiner de formulário adaptável, conforme mostrado abaixo.

![Suporte a funções personalizadas nas expressões de validação](assets/clientlib-cat.png)

Suporte a funções personalizadas nas expressões de validação

O autor pode configurar a biblioteca JavaScript personalizada por formulário adaptável. Na biblioteca, mantenha somente as funções reutilizáveis, que têm dependência em bibliotecas de terceiros jquery e underscore.js.

## Erro ao lidar com a ação de envio {#error-handling-on-submit-action}

Como parte das diretrizes de segurança e proteção do Experience Manager, configure páginas de erro personalizadas, como 404.jsp e 500.jsp. Esses manipuladores são chamados quando um erro de formulário 404 ou 500 é enviado. Os manipuladores também são chamados quando esses códigos de erro são acionados no nó Publicar .

Para obter mais informações, consulte [Personalizando páginas mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md).
