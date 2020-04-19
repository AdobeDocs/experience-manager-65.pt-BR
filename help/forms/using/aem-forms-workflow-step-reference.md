---
title: Fluxo de trabalho centrado em formulários no OSGi - Referência de etapas
seo-title: Fluxo de trabalho centrado em formulários no OSGi - Referência de etapas
description: O fluxo de trabalho centrado em formulários nas etapas do OSGi permite que você crie rapidamente workflows baseados em formulários adaptáveis.
seo-description: O fluxo de trabalho centrado em formulários nas etapas do OSGi permite que você crie rapidamente workflows baseados em formulários adaptáveis.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
contentOwner: null
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Fluxo de trabalho centrado em formulários no OSGi - Referência de etapas{#forms-centric-workflow-on-osgi-step-reference}

## Etapas do fluxo de trabalho do Forms {#forms-workflow-steps}

As etapas do fluxo de trabalho do Forms executam operações específicas do AEM Forms em um fluxo de trabalho do AEM. Essas etapas permitem que você crie rapidamente fluxos de trabalho adaptáveis baseados em formulários centrados em formulários no OSGi. Esses workflows podem ser usados para desenvolver workflows básicos de revisão e aprovação, processos de negócios internos e entre firewall. Você também pode usar as etapas do Fluxo de trabalho do Forms para serviços de documento de start, integrar-se ao fluxo de trabalho de assinatura do Adobe Sign e executar outras operações do AEM Forms. Você precisa do complemento [](https://www.adobe.com/go/learn_aemforms_documentation_63) AEM Forms para usar essas etapas em um fluxo de trabalho.

## Assign task step {#assign-task-step}

A etapa Atribuir tarefa cria uma tarefa e a atribui a um usuário ou grupo. Juntamente com a atribuição da tarefa, o componente também especifica o formulário adaptável ou PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar a entrada de usuários e um PDF não interativo ou um formulário adaptável somente leitura é usado apenas para workflows de revisão.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um documento automático de registro, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem pré-preenchidos e especificar ações padrão. A etapa Atribuir Tarefa tem as seguintes propriedades:

* **Título:** Título da tarefa. O título é exibido na Caixa de entrada do AEM.
* **Descrição:** Explicação das operações que estão a ser efetuadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você trabalha em um ambiente de desenvolvimento compartilhado.

* **Caminho da miniatura:** Caminho da miniatura da tarefa. Se nenhum caminho for especificado, para uma miniatura padrão de formulário adaptável será exibida e para o Documento de Registro, um ícone padrão será exibido.
* **Fase do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Prioridade:** A prioridade selecionada é exibida na Caixa de entrada do AEM. As opções disponíveis são Alto, Médio e Baixo. O valor padrão é Médio.
* **Data de Vencimento:** Especifique o número de dias ou horas após os quais a tarefa está marcada como atrasada. Se você selecionar **Desativado**, a tarefa nunca será marcada como atrasada. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver atrasada.

* **Dias:** O número de dias antes do qual a tarefa deve ser concluída. O número de dias é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não for concluída e ultrapassar o número de dias especificado no campo Dias, então, se selecionado, um manipulador de tempo limite será acionado após a data de vencimento.
* **Horas:** O número de horas antes das quais a tarefa deve ser concluída. O número de horas é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não for concluída e ultrapassar o número de horas especificado no campo Horas, então, se selecionado, um manipulador de tempo limite será acionado após as horas de vencimento.
* **Tempo limite após a data de vencimento:** Selecione essa opção para ativar o campo de seleção Manipulador de tempo limite.
* **Manipulador de tempo limite:** Selecione o script a ser executado quando a etapa de atribuição de tarefa ultrapassar a data de vencimento. Os scripts colocados no repositório CRX em [apps]/fd/painel/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **Realce a ação e o comentário da última tarefa em Detalhes da Tarefa:** Selecione essa opção para exibir a última ação executada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **Tipo:** Escolha o tipo de documento a ser preenchido quando o fluxo de trabalho for iniciado. Você pode escolher um formulário adaptável, um formulário adaptável somente leitura, um documento PDF não interativo, uma interface do usuário do Interative Communication Agent ou um Documento do Canal da Web Interative Communication.
* **Usar formulário adaptável:** Especifique o método para localizar o formulário adaptável de entrada. Essa opção estará disponível se você selecionar Formulário adaptável ou Formulário adaptável somente leitura na lista suspensa Tipo. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
   É possível associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

* **Usar comunicação interativa:** Especifique o método para localizar a comunicação interativa de entrada. Você pode usar a comunicação interativa enviada ao fluxo de trabalho, disponível em um caminho absoluto, ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho. Essa opção estará disponível se você selecionar IU do agente de comunicação interativo ou Documento do Canal da Web de comunicação interativa na lista suspensa Tipo.

>[!NOTE]
>
>É necessário ter usuários com agente de cm e atribuições de grupo de usuários de fluxo de trabalho para acessar a interface do usuário do agente do Interative Communications na caixa de entrada do AEM.

* **Formulário adaptável ou caminho** de comunicação interativo: Especifique o caminho do formulário adaptável ou da Comunicação interativa. Você pode usar o formulário adaptável ou a comunicação interativa enviada para o fluxo de trabalho, disponível em um caminho absoluto, ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados da string.
* **Selecione PDF de entrada usando:** Especifique o caminho de um documento PDF não interativo. O campo está disponível quando você escolhe um documento PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga, salvo em um caminho absoluto ou usando uma variável do tipo de dados do Documento. Por exemplo, [Payload_Diretory]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. É necessário ativar uma opção Documento de registro ou formulários adaptáveis baseados em modelo de formulário para usar a opção Caminho do PDF.
* **Para a tarefa concluída, renderize o formulário adaptável como**: Quando uma tarefa está marcada como concluída, é possível renderizar o formulário adaptável como um formulário adaptável somente leitura ou um documento PDF. É necessário ativar uma opção Documento de registro ou formulários adaptáveis baseados em modelo de formulário para renderizar o formulário adaptável como Documento de registro.
* **Pré-preenchido:** Os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **Selecione o arquivo de dados de entrada usando:** Caminho do arquivo de dados de entrada (.json,. xml, .doc ou modelo de dados de formulário). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga ou recuperar o arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo AEM Inbox. Um caminho de exemplo é [Payload_Diretory]/workflow/data.
   * **Selecione anexos de entrada usando:** Os anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho é sempre relativo à carga. Um caminho de exemplo é [Payload_Diretory]/attachments/
   * **Escolha entrada JSON:** Selecione um arquivo JSON de entrada usando um caminho relativo à carga ou armazenado em uma variável do tipo de dados Documento, JSON ou Modelo de dados de formulário. Essa opção estará disponível se você selecionar IU do agente de comunicação interativo ou Documento do Canal da Web de comunicação interativa na lista suspensa Tipo.
   * **Escolha um serviço de preenchimento prévio personalizado:** Selecione o serviço de pré-preenchimento para recuperar os dados e pré-preencher o documento do canal da Web Interative Communication ou a interface do agente.

   * **Use o serviço de preenchimento prévio da comunicação interativa selecionada acima:** Use essa opção para usar o serviço de pré-preenchimento da Comunicação interativa definida na lista suspensa Usar comunicação interativa.
   * **Mapeamento do atributo de solicitação:** Use a seção Solicitar mapeamento de atributo para definir o [nome e o valor do atributo](../../forms/using/work-with-form-data-model.md#bindargument)de solicitação. Recupere os detalhes da fonte de dados com base no nome e no valor do atributo especificados na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.\
      As opções de mapeamento do serviço de preenchimento prévio e do atributo de solicitação estão disponíveis somente se você selecionar a interface do usuário do Interative Communication Agent ou o Documento do Canal da Web Interative Communication na lista suspensa Tipo.

* **Informações enviadas:** Os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **Salve o arquivo de dados de saída usando:** Salve o arquivo de dados (.json,. xml, .doc ou modelo de dados de formulário). O arquivo de dados contém informações enviadas por meio do formulário associado. É possível salvar o arquivo de dados de saída usando um caminho relativo à carga ou armazená-lo em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, [Payload_Diretory]/Workflow/data, onde os dados são um arquivo.
   * **Salvar anexos usando:** Salve os anexos de formulário fornecidos em uma tarefa. É possível salvar os anexos usando um caminho relativo à carga ou armazená-lo em uma variável do tipo de dados do Documento.
   * **Salvar Documento de Registro usando:** Caminho para salvar um Documento do arquivo de registro. Por exemplo, [Payload_Diretory]/DocumentofRecord/credit-card.pdf. É possível salvar o Documento de Registro usando um caminho relativo à carga ou armazená-lo em uma variável do tipo de dados do Documento. Se você selecionar a opção **Em relação à carga útil** , o Documento do registro não será gerado se o campo de caminho ficar vazio. Essa opção estará disponível somente se você selecionar Formulário adaptável na lista suspensa Tipo.

   * **Salvar dados de Canal da Web usando:** Salve o arquivo de dados do Canal da Web usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados Documento, JSON ou Form Data Model. Essa opção estará disponível somente se você selecionar a interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.
   * **Salve o documento PDF usando:** Salve o documento PDF usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados do Documento. Essa opção estará disponível somente se você selecionar a interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.
   * **Salve o modelo de layout usando:** Salve o modelo de layout usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados do Documento. O modelo [de](../../forms/using/layout-design-details.md) layout refere-se a um arquivo XDP que você cria usando o Forms Designer. Essa opção estará disponível somente se você selecionar a interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.

* **Destinatário > Atribuir opções:** Especifique o método para atribuir a tarefa a um usuário. Você pode atribuir dinamicamente a tarefa a um usuário ou grupo usando o script do Seletor de participantes ou atribuir a tarefa a um usuário ou grupo específico do AEM.
* **Seletor de participantes:** A opção está disponível quando a opção **Dinamicamente para um usuário ou grupo** está selecionada no campo Atribuir opções. Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte Atribuir [dinamicamente um fluxo de trabalho aos usuários](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Criar uma etapa personalizada do Adobe Experience Manager Dynamic Participant.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **Participantes:** O campo está disponível quando a opção **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** está selecionada no campo Seletor de **participantes** . O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **Destinatário:** O campo está disponível quando **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** está selecionado no campo Seletor de **participantes** . O campo permite selecionar uma variável do tipo de dados String para definir o destinatário.

* **Argumentos:** O campo está disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de participantes. O campo permite fornecer uma lista de argumentos separados por vírgula para o script selecionado no campo Seletor de participantes.

* **Usuário ou grupo:** A tarefa é atribuída ao usuário ou grupo selecionado. A opção está disponível quando a opção **** Para um usuário ou grupo específico está selecionada no campo **Atribuir opções** . O campo lista todos os usuários e grupos do grupo de usuários do fluxo de trabalho.\
   O menu suspenso **Usuário ou Grupo** lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende se você tiver permissões de acesso no nó **usuários** no repositório crx para esse usuário específico.

* **Notificar o destinatário por email:** Selecione essa opção para enviar notificações por email ao destinatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário. Antes de usar a opção, ative as notificações do console da Web do AEM. Para obter instruções passo a passo, consulte [configurar notificações por email para a etapa de atribuição de tarefa](../../forms/using/aem-forms-workflow.md)

* **Modelo** de email HTML: Selecione o modelo de e-mail para o e-mail de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no repositório crx.
* **Permitir delegação para:** A Caixa de entrada do AEM fornece uma opção para o usuário conectado para delegar o fluxo de trabalho atribuído a outro usuário. Você pode delegar dentro do mesmo grupo ou ao usuário do fluxo de trabalho de outro grupo. Se a tarefa for atribuída a um único usuário e a opção **permitir delegação a membros do grupo** designado for selecionada, não será possível delegar a tarefa a outro usuário ou grupo.
* **Configurações de compartilhamento:** A Caixa de entrada do AEM fornece opções para compartilhar uma única ou todas as tarefas da caixa de entrada com outros usuários:
   * Quando a opção **Permitir que o destinatário compartilhe explicitamente na caixa de entrada** está selecionada, o usuário pode clicar na tarefa e compartilhá-la com outro usuário do AEM.
   * Quando a opção **Permitir compartilhamento pelo destinatário via compartilhamento** de caixa de entrada estiver selecionada e um usuário compartilhar seus itens de Caixa de entrada ou permitir que outros usuários acessem seus itens de Caixa de entrada, somente as tarefas com essa opção ativada serão compartilhadas com outros usuários.

* **Ações > Ações padrão:** As ações Enviar, Salvar e Redefinir estão disponíveis na caixa. Todas as ações padrão são ativadas, por padrão.
* **Variável de rota:** Nome da variável de rota. A variável de rota captura ações personalizadas que um usuário seleciona na Caixa de entrada do AEM.
* **Rotas:** Uma tarefa pode ramificar para rotas diferentes. Quando selecionada na Caixa de entrada do AEM, a rota retorna um valor e o fluxo de trabalho ramifica com base na rota selecionada. Você pode armazenar rotas em uma variável de uma matriz do tipo de dados String ou selecionar **Literal** para adicionar rotas manualmente.

* **Título**: Especifique o título da rota. É exibido na Caixa de entrada do AEM.
* **Ícone** Coral: Especifique o atributo HTML de um ícone de coral. A biblioteca do Adobe CorelUI fornece um vasto conjunto de ícones de toque primeiro. Você pode escolher e usar um ícone para a rota. É exibido junto com o título na Caixa de entrada do AEM. Se você armazenar as rotas em uma variável, as rotas usarão um ícone de coral &#39;Tags&#39; padrão.
* **Permitir que o destinatário adicione comentário**: Selecione essa opção para ativar comentários para a tarefa. Um destinatário pode adicionar os comentários da Caixa de entrada do AEM no momento do envio da tarefa.
* **Salve o comentário na variável:** Salve o comentário em uma variável do tipo de dados String. Essa opção é exibida somente se você marcar a caixa de seleção **Permitir que o destinatário adicione comentário** .

* **Permitir que o destinatário adicione anexos à tarefa**: Selecione essa opção para ativar anexos para a tarefa. Um destinatário pode adicionar os anexos de dentro da Caixa de entrada do AEM no momento do envio da tarefa.
* **Salve anexos de tarefa de saída usando**: Especifique o local da pasta de anexos. É possível salvar anexos de tarefa de saída usando um caminho relativo à carga ou em uma variável de uma matriz de tipo de dados de documento. Essa opção é exibida somente se você marcar a caixa de seleção **Permitir que o destinatário adicione anexos à tarefa** e selecionar Formulário **** Adaptável, Formulário **adaptável somente** leitura ou documento **PDF** não interativo na lista suspensa **Tipo** **** na guia Formulário/Documento.

>[!NOTE]
>
>Use a guia Anexos na interface do agente durante o tempo de execução para associar os anexos a uma comunicação interativa. Os anexos associados são exibidos como anexos de tarefa no sidekick depois de abrir o item de trabalho em um estado Concluído.

* **Usar metadados personalizados:** Selecione essa opção para ativar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **Metadados personalizados:** Selecione um metadados personalizados para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/painel/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Você também pode estender a interface WorkitemUserMetadataService para fornecer metadados personalizados.
* **Mostrar dados das etapas** anteriores: Selecione essa opção para habilitar os destinatários a visualização de destinatários anteriores, ação já tomada na tarefa, comentários adicionados à tarefa e documento do registro da tarefa concluída, se disponível.
* **Mostrar dados de etapas subsequentes:** Selecione essa opção para permitir que o destinatário atual visualização a ação tomada e os comentários adicionados à tarefa pelos destinatários subsequentes. Também permite que o destinatário atual visualização um documento de registro da tarefa concluída, se disponível.
* **Visibilidade do tipo de dados:** Por padrão, um destinatário pode visualização um Documento de Registro, destinatários, ação tomada e comentários que os destinatários anteriores e subsequentes adicionaram. Use a opção de visibilidade do tipo de dados para limitar o tipo de dados visível para os destinatários.

## Etapa Enviar email {#send-email-step}

Use a etapa de email para enviar um email, por exemplo, um email com um documento de registro, link de um formulário adaptável, link de uma comunicação interativa ou com um documento PDF anexado. A etapa Enviar e-mail suporta e-mail [](https://en.wikipedia.org/wiki/HTML_email)HTML. Os emails HTML respondem e se adaptam ao cliente de email e ao tamanho da tela do recipient. Você pode usar um modelo de e-mail HTML para definir a aparência, o esquema de cores e o comportamento do e-mail.

A etapa de email usa o serviço Day CQ Mail para enviar emails. Antes de usar a etapa de email, verifique se o serviço [de](../../forms/using/aem-forms-workflow.md) email está configurado. A etapa de email tem as seguintes propriedades:

**Título:** O título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**Descrição:** A explicação é útil para outros desenvolvedores de processos quando você trabalha em um ambiente de desenvolvimento compartilhado.

**Assunto do email:** O assunto pode ser recuperado de metadados de fluxo de trabalho, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione uma das seguintes opções:

* **Literal -** especifique manualmente um assunto.
* **Recuperar dos metadados** do fluxo de trabalho - Recuperar o assunto de uma propriedade de metadados.
* **Variável** - recupere o assunto do valor armazenado em uma variável do tipo de dados da string.

**Modelo** de email HTML: Modelo HTML para o email. Você pode especificar variáveis em um modelo de email. A Etapa de email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**Metadados de modelo de email:** O valor das variáveis do modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no autor ou no servidor de publicação, imagem ou uma propriedade de metadados do fluxo de trabalho.

* **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **Metadados do fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados do fluxo de trabalho. Depois de selecionar a opção, digite o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho. Por exemplo, emailAddress.
* **URL do ativo:** Use a opção para incorporar um link da Web de uma comunicação interativa ao email. Depois de selecionar a opção, procure e escolha a comunicação interativa a ser incorporada. O ativo pode residir no autor ou no servidor de publicação.
* **Imagem:** Use a opção para incorporar uma imagem ao email. Depois de selecionar a opção, navegue e escolha a imagem. A opção de imagem está disponível somente para as tags de imagem (&lt;img src=&quot;*&quot;/>) disponíveis no modelo de email.

**Endereço de email do remetente/Recipient:** Selecione a opção **Literal** para especificar manualmente um endereço de email ou selecione a opção **Recuperar dos metadados** do fluxo de trabalho para recuperar o endereço de email de uma propriedade de metadados. Também é possível especificar uma lista de matrizes de propriedade de metadados para a opção **Recuperar dos metadados** do fluxo de trabalho. Selecione a opção **Variável** para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados da string.

**Anexo de arquivo:** O ativo disponível no local especificado é anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um caminho de exemplo é [Payload_Diretory]/attachments/.

Selecione a opção **Variável** para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON.

**Nome do arquivo:** Nome do arquivo de anexo de email. A Etapa de e-mail altera o nome do arquivo original do anexo para o nome do arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados do fluxo de trabalho ou de uma variável. Use a opção **Literal** quando souber o valor exato a ser especificado. Use a opção **Variável** para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados da string. Use a **opção Recuperar de metadados** do fluxo de trabalho quando o valor a ser usado for salvo em uma propriedade de metadados do fluxo de trabalho.

## Generate Document of Record step {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, é possível manter um registro do formulário, em formato impresso ou em formato de documento. Isso é conhecido como Documento de registro (DoR). Você pode usar a etapa Gerar Documento de registro para criar uma versão PDF somente leitura ou interativa de um formulário adaptável. A versão PDF contém informações preenchidas no formulário juntamente com o layout do formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**Usar formulário** adaptável: Especifique o método para localizar o formulário adaptável de entrada. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho na variável **Select para resolver** o campo.\
É possível associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**Caminho** do formulário adaptável: Especifique o caminho do formulário adaptável. O campo está disponível quando você seleciona a opção **Disponível em um caminho** absoluto no campo **Usar formulário** adaptável.

**Selecione Dados de entrada usando:** Caminho dos dados de entrada para o formulário adaptável. É possível manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável de tipo de dados Documento, JSON ou XML. Os dados de entrada são unidos ao formulário adaptável para criar um documento de registro.

**Selecione o caminho do anexo de entrada usando:** Caminho dos anexos. Esses anexos estão incluídos no Documento de registro. É possível manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar os anexos armazenados em uma variável do tipo de dados do Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao Documento de registro. Se algum arquivo estiver disponível nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de Registro como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

**Salve o Documento gerado do registro usando as opções abaixo:** Especifique o local para manter um documento do arquivo de registro. Você pode optar por substituir a pasta de carga, colocar o documento do registro em um local dentro do diretório de carga ou armazenar o documento do registro em uma variável do tipo de dados do Documento.

**Local**: Especifique o idioma do documento de registro. Selecione **Literal** para selecionar a localidade de uma lista suspensa ou selecione **Variável** para recuperar a localidade do valor armazenado em uma variável do tipo de dados da string. Você deve definir o código de localidade ao armazenar o valor da localidade em uma variável. Por exemplo, especifique **en_US** para inglês e **fr_FR** para francês.

## Invoke Form Data Model Service step {#invoke-form-data-model-service-step}

Você pode usar a Integração [de dados do](../../forms/using/data-integration.md) AEM Forms para configurar e se conectar a fontes de dados diferentes. Essas fontes de dados podem ser uma solução de banco de dados, serviço da Web, serviço REST, serviço OData e CRM. A integração de dados de formulários AEM permite criar um modelo de dados de formulário abrangendo vários serviços para executar operações de recuperação de dados, adição e atualização no banco de dados configurado. Você pode usar a etapa **** Chamar serviço de modelo de dados para selecionar um modelo de dados de formulário (FDM) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a fontes de dados diferentes.

Para explicar entradas para campos da etapa, a tabela do banco de dados a seguir e o arquivo JSON são usados como exemplo:

**Exemplo de tabela CustomerDetails**

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Valor<br /> </td> 
  </tr> 
  <tr> 
   <td>Nome<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Sobrenome</td> 
   <td>Rosa</td> 
  </tr> 
  <tr> 
   <td>ID do cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Endereço de email<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**Exemplo de arquivo JSON**

```
{ 
  customer: { 
   firstName: "Sarah", 
   lastName:"Rose", 
   customerId: "1", 
   emailAddress:"srose@we.info" 
 }, 
  insurance: {
   customerId: "1", 
  policyType: "Premium,
  policyNumber: "Premium-521499",
  customerDetails: { 
   firstName: "Sarah",
   lastName: "Rose",
   customerId: "1",
   emailAddress: "srose@we.info" 
  }
 }
}
```

A etapa Invocar serviço de modelo de dados de formulário tem os campos listados abaixo para facilitar as operações do modelo de dados de formulário:

* **Título:** Título da etapa. Ajuda a identificar a etapa no editor de fluxo de trabalho.
* **Descrição:** Explicação útil para outros desenvolvedores de processos quando você trabalha em um ambiente de desenvolvimento compartilhado.

* **Caminho** do modelo de dados de formulário: Procure e selecione um modelo de dados de formulário presente no servidor.

* **Serviço**: Lista dos serviços fornecidos pelo modelo de dados de formulário selecionado.
* **Entrada para serviços > Forneça dados de entrada usando metadados literais, variáveis ou de fluxo de trabalho e um arquivo** JSON: Um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço a partir de uma propriedade de metadados de fluxo de trabalho, um objeto JSON, uma variável ou insira diretamente o valor na caixa de texto fornecida:

   * **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **Variável:** Use a opção para recuperar o valor armazenado em uma variável.
   * **Recuperar dos metadados do fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados do fluxo de trabalho. Por exemplo, emailAddress.
   * **Notação de ponto JSON:** Use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, Insurance.customerDetails.emailAddress. A opção JSON Dot Notation (Notação de ponto JSON) está disponível somente se a opção Map input fields from input JSON (Mapear campos de entrada JSON de entrada) estiver selecionada.
   * **Mapear campos de entrada do JSON de entrada:** Especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Form Data Model.

* **Entrada para serviços > Forneça dados de entrada usando uma variável ou um arquivo JSON:** Selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **Selecione documento Input JSON usando**: O arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **relativo à carga** ou a um caminho **absoluto.** Você também pode recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Form Data Model.

* **Notação de ponto JSON:** Deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON, por exemplo, se você tiver um JSON semelhante ao listado no start da seção, especifique Insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **Saída do serviço > Mapear e gravar valores de saída para variáveis ou metadados:** Selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância do fluxo de trabalho no repositório crx. Especifique o nome da propriedade de metadados e selecione o atributo de saída do serviço correspondente a ser mapeado com a propriedade de metadados; por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, é possível armazenar a saída em uma variável do tipo de dados Longo.
* **Saída do serviço > Salvar saída em uma variável ou um arquivo JSON:** Selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **Salve o documento JSON de saída usando as opções abaixo:** Salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga ou a um caminho absoluto. Você também pode salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Form Data Model.

## Etapa Assinar Documento {#sign-document-step}

A etapa Assinar Documento permite que você use o Adobe Sign para assinar documentos. A etapa Assinar Documento tem as seguintes propriedades:

* **Nome do Contrato:** Especifique o título do contrato. O nome do contrato se torna parte do assunto e do texto do corpo do email enviado aos signatários. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **Literal** para adicionar o nome manualmente.

* **Local:** Especifique o idioma para as opções de email e verificação. Você pode armazenar a localidade em uma variável do tipo de dados String ou selecionar **Literal** para escolher a localidade na lista de opções disponíveis. Você deve definir o código de localidade ao armazenar o valor da localidade em uma variável. Por exemplo, especifique **en_US** para inglês e **fr_FR** para francês.

* **Configuração** da Adobe Sign Cloud: Escolha uma configuração da Adobe Sign Cloud. Se você não tiver configurado o Adobe Sign para formulários AEM, consulte [Integrar o Adobe Sign a formulários](../../forms/using/adobe-sign-integration-adaptive-forms.md)AEM.

* **Selecione o Documento a ser assinado usando:** Você pode escolher um documento de um local relativo à carga, usar a carga como o documento, especificar um caminho absoluto do documento ou recuperar o documento armazenado em uma variável do tipo de dados do Documento.
* **Dias até o prazo:** Um documento é marcado como vencido (prazo vencido) depois que não há atividade na tarefa pelo número de dias especificado no campo **Dias até o término** . O número de dias é contado depois que o documento é atribuído a um usuário para assinatura.
* **Frequência de email do lembrete:** Você pode enviar um email de lembrete diariamente ou semanalmente. A semana é contada a partir do dia em que o documento é atribuído a um usuário para assinatura.
* **Processo de assinatura:** Você pode optar por assinar um documento em uma ordem sequencial ou paralela. Em ordem sequencial, um assinante recebe o documento por vez para assinatura. Depois que o primeiro assinante concluir a assinatura do documento, o documento será enviado para o segundo assinante e assim por diante. Em ordem paralela, vários signatários podem assinar um documento de cada vez.
* **URL de redirecionamento:** Especifique um URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou instruções adicionais.
* **Fase do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Selecionar signatários:** Especifique o método para escolher os signatários do documento. Você pode atribuir dinamicamente o fluxo de trabalho a um usuário ou grupo ou adicionar manualmente detalhes de um assinante.
* **Script ou serviço para selecionar signatários:** A opção estará disponível somente se a opção Dinamicamente estiver selecionada no campo Selecionar signatários. Você pode especificar um ECMAScript ou um serviço para escolher assinantes e opções de verificação para um documento.
* **Detalhes do assinante:** A opção estará disponível somente se a opção Manualmente estiver selecionada no campo Selecionar signatários. Especifique o endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação de 2 etapas, verifique se a opção de verificação correspondente está ativada para a conta configurada do Adobe Sign. Você pode usar uma variável do tipo de dados String para definir valores para os campos **[!UICONTROL Email]**, Código **[!UICONTROL do]** país e Número **[!UICONTROL de]** telefone. Os campos Código **[!UICONTROL do]** país e Número **[!UICONTROL de]** telefone são exibidos somente se você selecionar Verificação **[!UICONTROL de]** telefone na lista suspensa de verificação **[!UICONTROL de]** 2 etapas.
* **Variável de status:** Um documento habilitado para o Adobe Sign armazena o status de assinatura do documento em uma variável do tipo de dados String. Especifique o nome da variável de status (adobeSignStatus). Uma variável de status de uma instância está disponível no CRXDE em /etc/workflow/instance/&lt;server>/&lt;date-time>/&lt;instance of workflow model>/workItems/&lt;node>/metaData contém o status de uma variável.
* **Salve o documento assinado usando as opções abaixo:** Especifique o local para manter documentos assinados. Você pode optar por substituir o arquivo de carga, colocar o documento assinado em um local dentro do diretório de carga ou armazenar o documento assinado em uma variável do tipo de Documento.

## Etapas dos serviços do Documento {#document-services-steps}

Os serviços de Documento AEM são um conjunto de serviços para criar, montar e proteger Documentos PDF. O AEM Forms fornece uma etapa separada do fluxo de trabalho do AEM para cada serviço de documento.

Semelhante a outras etapas do fluxo de trabalho do AEM Forms, como Atribuir Tarefa, Enviar e-mail e Assinar Documento, você pode usar variáveis em todas as etapas dos serviços de Documento do AEM. Para obter mais informações sobre como criar e gerenciar variáveis, consulte [Variáveis em workflows](../../forms/using/variable-in-aem-workflows.md)AEM.

### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Adicione carimbo de data/hora a um documento. Você fornece detalhes do documento, como caminho do documento de entrada, nome do documento de entrada, local para armazenar dados exportados. Você pode optar por substituir o arquivo de carga existente, escolher um nome de arquivo diferente para armazenar dados em um arquivo diferente em uma pasta de carga, fornecer um caminho absoluto para os dados ou armazenar dados em uma variável do tipo de dados do Documento.

### Converter em etapa de imagem {#convert-to-image-step}

Converte um documento PDF em lista de imagens. Os formatos de imagem suportados são JPEG, JPEG2000, PNG e TIFF. As seguintes informações se aplicam às conversões em imagens TIFF:

* Um arquivo TIFF de várias páginas é gerado.
* Algumas anotações não são incluídas em imagens TIFF. As anotações que exigem que o Acrobat gere sua aparência não são incluídas.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converte um documento PDF em formato PDF/A usando as opções fornecidas. A versão PDF/A do PDF (Portable Documento Format) é especializada para arquivamento e preservação de documentos a longo prazo.

### Converter para etapa PS {#convert-to-ps-step}

Converta documentos PDF em PostScript. Ao converter para PostScript, você pode usar a operação de conversão para especificar o documento de origem e se deve ser convertida para PostScript nível 2 ou 3. O documento PDF convertido em um arquivo PostScript deve ser não interativo.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Gere um documento PDF a partir de um arquivo de entrada. O documento de entrada pode ser relativo à carga, ter um caminho absoluto, pode ser a própria carga ou armazenado em uma variável do tipo de dados do Documento.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Gera um documento PDF a partir do URL fornecido, do HTML e do arquivo ZIP.

### Etapa Exportar dados {#export-data-step}

Exporta dados de um formulário PDF ou arquivo XDP. É necessário inserir o caminho de arquivo do Documento de entrada e o Formato de dados de exportação. As opções para Formato de dados de exportação são Auto, XDP e XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converte um documento PDF em um formato selecionado.

### Gerar etapa de PDF não interativo {#generatenoninteractive}

Gerar um PDF não interativo. Fornece várias opções de personalização.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa Importar dados {#import-data-step}

Une dados de formulário em um formulário PDF. É possível importar dados de formulário para um formulário PDF.

### Invocar etapa DDX {#invokeddx}

Executa o arquivo DDX no mapa especificado de documentos de entrada e retorna os documentos PDF manipulados.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo DDX para documentos de entrada. Armazene o arquivo DDX em uma variável do tipo de dados Documento ou XML.

### Otimizar etapa do PDF {#optimize-pdf-step}

Otimiza arquivos PDF reduzindo seu tamanho. O resultado dessa conversão são arquivos PDF que podem ser menores que suas versões originais. Essa operação também converte documentos PDF na versão PDF especificada nos parâmetros de otimização.

As configurações de otimização especificam como os arquivos são otimizados. Estas são configurações de exemplo:

* Versão PDF do Público alvo
* Descartar objetos como ações JavaScript e miniaturas de página incorporadas
* Descartar dados do usuário, como comentários e anexos de arquivo
* Descartar configurações inválidas ou não usadas
* Compactação de dados descompactados ou uso de algoritmos de compactação mais eficientes
* Remoção de fontes incorporadas
* Configuração de valores de transparência

### Etapa Renderizar formulário PDF {#renderpdf}

Renderiza um formulário criado no Form Designer (XDP) em um formulário PDF.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa do Documento seguro {#secure-document-step}

Criptografe, assine e certifique um documento. O AEM Forms é compatível com criptografia baseada em senha e baseada em certificado. Você também pode escolher entre vários algoritmos para assinar documentos. Por exemplo, SHA-256 e SH-512. Também é possível usar a etapa de fluxo de trabalho para o leitor estender documentos PDF. A etapa do fluxo de trabalho fornece opções para ativar a decodificação de códigos de barras, assinaturas digitais, importação e exportação de dados PDF e outras opções.

### Etapa Enviar para impressora {#send-to-printer-step}

Envie um documento diretamente para uma impressora. Ele suporta os seguintes mecanismos de acesso de impressão:

* **Impressora** acessível diretamente: Uma impressora instalada no mesmo computador é chamada de impressora acessível diretamente e o computador é nomeado host da impressora. Esse tipo de impressora pode ser uma impressora local que está conectada diretamente ao computador.
* **Impressora** acessível indiretamente: A impressora instalada em um servidor de impressão é acessada de outros computadores. Tecnologias como o CUPS (Common UNIX® Print System) e o protocolo LPD (Line Printer Daemon) estão disponíveis para conexão com uma impressora de rede. Para acessar uma impressora acessível indiretamente, especifique o IP ou o nome do host do servidor de impressão. Usando esse mecanismo, você pode enviar um documento para um URI LPD quando a rede tiver um LPD em execução. O mecanismo permite direcionar o documento para qualquer impressora conectada à rede que tenha um LPD em execução.

### Etapa Gerar saída impressa {#generatePrintedOutput}

A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL, considerando um design de formulário e um arquivo de dados. O arquivo de dados é unido ao design de formulário e formatado para impressão. A saída gerada por essa etapa pode ser enviada diretamente para uma impressora ou salva como arquivo. É recomendável usar essa etapa quando quiser usar designs de formulário ou dados de um aplicativo. Se os designs de formulário ou os designs de formulário estiverem localizados na rede, no sistema de arquivos local ou no local HTTP, use a operação generatePrintedOutput.

Por exemplo, seu aplicativo exige que você mescle um design de formulário a um arquivo de dados. Os dados contêm centenas de registros. Além disso, requer que a saída seja enviada para uma impressora que suporte ZPL. O design de formulário e seus dados de entrada estão localizados em um aplicativo. Use a operação generatePrintedOutput para unir cada registro a um design de formulário e enviar a saída para uma impressora que suporte ZPL.

A etapa Gerar saída impressa tem as seguintes propriedades:

**Propriedades de entrada**

* **[!UICONTROL Selecione o arquivo de modelo usando]**: Especifique o caminho do arquivo de modelo. Você pode selecionar o arquivo de modelo usando o caminho relativo à carga, salvo em um caminho absoluto ou usando uma variável do tipo de dados do Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo. Além disso, você também pode aceitar a carga como o arquivo de dados de entrada.

* **[!UICONTROL Selecione o documento de dados usando]**: Especifique o caminho de um arquivo de dados de entrada. Você pode selecionar o arquivo de dados de entrada usando o caminho relativo à carga, salvo em um caminho absoluto ou usando uma variável do tipo de dados do Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

* **[!UICONTROL Formato]** da impressora: Um valor de Formato de impressão que especifica a linguagem de descrição da página a ser usada, quando um arquivo XDC não for fornecido, para gerar o fluxo de saída. Se você fornecer um valor literal, selecione um destes valores:

   * **[!UICONTROL PCL]** personalizado: Use a opção para especificar um arquivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript]** personalizado: Use a opção para especificar um arquivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL]** personalizado: Use a opção para especificar um arquivo XDC personalizado para ZPL.
   * **[!UICONTROL PCL de cor genérica (5c)]**: Use um PCL de cor genérica (5c).
   * **[!UICONTROL PostScript Nível3]** genérico: Use o PostScript Nível 3 genérico.
   * **[!UICONTROL ZPL 300 DPI]**: Utilizar ZPL 300 DPI. O zpl300.xdc é usado.
   * **[!UICONTROL ZPL 600 DPI]**: Utilizar ZPL 600 DPI. O arquivo zpl600.xdc é usado.
   * **[!UICONTROL IPL]** personalizado: Use a opção para especificar um arquivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 DPI]**: Utilizar IPL 300 DPI. O ipl300.xdc é usado.
   * **[!UICONTROL IPL 400 DPI]**: Utilizar IPL 400 DPI. O arquivo ipl400.xdc é usado.
   * **[!UICONTROL TPCL]** personalizado: Use a opção para especificar um arquivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. O arquivo tpcl305.xdc é usado.
   * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. O arquivo tpcl600.xdc é usado.
   * **[!UICONTROL DPL]** personalizado: Use a opção para especificar um arquivo XDC personalizado DPL.
   * **[!UICONTROL DPL300DPI]**: Utilizar DPL 300 DPI. O arquivo dpl300.xdc é usado.
   * **[!UICONTROL DPL406DPI]**: Utilizar DPL 400 DPI. O dpl406.xdc é usado.
   * **[!UICONTROL DPL600DPI]**: Utilizar DPL 600 DPI. O dpl600.xdc é usado.

**Propriedades de saída**

* **[!UICONTROL Salve o documento de saída usando]**: Especifique o local para salvar o arquivo de saída. É possível salvar o arquivo de saída em um local relativo à carga, em uma variável ou especificar um local absoluto para salvar o arquivo de saída. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

**Propriedades avançadas**

* **[!UICONTROL Selecione o local raiz do conteúdo usando]**: Raiz do conteúdo é um valor de string que especifica o URI, a referência absoluta ou o local no repositório para recuperar ativos relativos usados pelo design de formulário. Por exemplo, se o design de formulário fizer referência a uma imagem relativamente, como ../myImage.gif, myImage.gif deve estar localizado em repository://. O valor padrão é repository://, que aponta para o nível raiz do repositório.

   Quando você seleciona um ativo do aplicativo, o caminho URI raiz do conteúdo deve ter a estrutura correta. Por exemplo, se um formulário for escolhido de um aplicativo chamado SampleApp e for colocado em SampleApp/1.0/forms/Test.xdp, o URI raiz do conteúdo deve ser especificado como repository://administrator@password/Applications/SampleApp/1.0/forms/ ou repositório:/Applications/SampleApp/1.0/forms/ (quando a autoridade for nula). Quando o URI raiz do conteúdo for especificado dessa forma, os caminhos de todos os ativos referenciados no formulário serão resolvidos em relação a esse URI.

* **[!UICONTROL Selecione o arquivo XCI usando]**: Os arquivos XCI são usados para descrever fontes e outras propriedades usadas para elementos de design de formulário. É possível manter um arquivo XCI relativo à carga, em um caminho absoluto ou usando uma variável do tipo de dados do Documento.

* **[!UICONTROL Local]**: Especifica o idioma usado para gerar o documento PDF. Se você fornecer um valor literal, selecione um idioma na lista ou selecione um destes valores:
   * **Para usar o padrão**do servidor:
(Padrão) Use a configuração Local configurada no AEM Forms Server. A configuração Local é configurada usando o Console de administração. (Consulte Ajuda [do](http://www.adobe.com/go/learn_aemforms_designer_65)Designer.)

   * **Para usar valor**personalizado:
Digite o código Localidade na caixa literal ou selecione uma variável de string contendo o código de localidade. Para obter uma lista completa dos códigos de localidade compatíveis, consulte http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Cópias]**: Um valor inteiro que especifica o número de cópias a serem geradas para a saída. O valor padrão é 1.

* **[!UICONTROL Impressão]** duplex:  Um valor de Paginação que especifica se a impressão nos dois lados ou em um único lado deve ser usada. As impressoras compatíveis com PostScript e PCL usam esse valor.Se você fornecer um valor literal, selecione um destes valores:
   * **[!UICONTROL Borda]** longa duplex: Use impressão nos dois lados e impressão usando paginação de borda longa.
   * **[!UICONTROL Borda]** curta duplex: Use impressão nos dois lados e impressão usando paginação de borda curta.
   * **[!UICONTROL Simplex]**: Use impressão em um único lado.