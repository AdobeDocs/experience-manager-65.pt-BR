---
title: Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas
seo-title: Forms-centric workflow on OSGi - Step Reference
description: O fluxo de trabalho centrado no Forms nas etapas do OSGi permite que você crie rapidamente fluxos de trabalho baseados em formulários adaptáveis.
seo-description: Forms-centric workflow on OSGi steps allow you rapidly build adaptive forms based workflows.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
source-git-commit: e3bc820dd9bfce95cdc0c8c58c075893a1f0a625
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas {#forms-centric-workflow-on-osgi-step-reference}

Você usa modelos de fluxo de trabalho para converter uma lógica de negócios em um processo repetitivo automatizado. Um modelo ajuda você a definir e executar uma série de etapas. Você também pode definir propriedades de modelo, como se o fluxo de trabalho é transitório ou usa vários recursos. Você pode [incluir várias etapas do fluxo de trabalho AEM em um modelo para atingir a lógica de negócios](/help/sites-developing/workflows-models.md#extending-aem).

## Etapas do Forms Workflow {#forms-workflow-steps}

As etapas do fluxo de trabalho do Forms executam operações específicas do AEM Forms em um fluxo de trabalho AEM. Essas etapas permitem que você crie rapidamente formulários adaptáveis com base no fluxo de trabalho centrado no Forms no OSGi. Esses fluxos de trabalho podem ser usados para desenvolver fluxos de trabalho básicos de revisão e aprovação, processos de negócios internos e entre firewall. Você também pode usar as etapas do Forms Workflow para iniciar serviços de documento, integrar com o fluxo de trabalho de assinatura do Adobe Sign e executar outras operações do AEM Forms. Você precisa [Complemento do AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) para usar essas etapas em um workflow.

As etapas do fluxo de trabalho centradas no Forms executam operações específicas do AEM Forms em um Fluxo de trabalho AEM. Essas etapas permitem que você crie rapidamente um fluxo de trabalho adaptável, baseado no Forms e centrado no OSGi. Esses fluxos de trabalho podem ser usados para desenvolver fluxos de trabalho básicos de revisão e aprovação, processos de negócios internos e entre firewall.

>[!NOTE]
>
>Se o modelo de fluxo de trabalho estiver marcado para um armazenamento externo, em seguida, para todas as etapas do fluxo de trabalho do Forms, você poderá selecionar apenas a opção de variável para armazenar ou recuperar arquivos de dados e anexos.

## Atribuir etapa da tarefa {#assign-task-step}

A etapa Atribuir tarefa cria uma tarefa e a atribui a um usuário ou grupo. Ao atribuir a tarefa, o componente também especifica o formulário adaptável ou o PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar a entrada de usuários e o PDF não interativo ou um formulário adaptável somente leitura é usado para fluxos de trabalho de revisão somente.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um documento automático de registro, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem preenchidos previamente e especificar ações padrão. A etapa Atribuir tarefa tem as seguintes propriedades:

* **Título:** Título da tarefa. O título é exibido AEM Caixa de entrada.
* **Descrição:** Explicação das operações que estão sendo executadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **Caminho da miniatura:** Caminho da miniatura da tarefa. Se nenhum caminho for especificado, para uma miniatura padrão de formulário adaptável será exibida e para Documento de registro, um ícone padrão será exibido.
* **Estágio do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Prioridade:** A prioridade selecionada é exibida na Caixa de entrada de AEM. As opções disponíveis são Alto, Médio e Baixo. O valor padrão é Médio.
* **Data de Vencimento:** Especifique o número de dias ou horas após as quais a tarefa está marcada vencida. Se você selecionar **Desligado**, a tarefa nunca será marcada como atrasada. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver vencida.

* **Dias:** O número de dias antes do qual a tarefa deve ser concluída. O número de dias é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não estiver concluída e cruzar o número de dias especificado no campo Dias , então, se selecionado, um manipulador de tempo limite será acionado após a data de vencimento.
* **Horas:** O número de horas antes do qual a tarefa deve ser concluída. O número de horas é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não estiver concluída e cruzar o número de horas especificado no campo Horas , então, se selecionado, um manipulador de tempo limite será acionado após as horas de vencimento.
* **Tempo limite após a data de vencimento:** Selecione esta opção para ativar o campo de seleção Manipulador de tempo limite.
* **Manipulador de tempo limite:** Selecione o script a ser executado quando a etapa Atribuir tarefa atravessar a data de vencimento. Scripts colocados no repositório CRX em [aplicativos]/fd/dashboard/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **Destaque a ação e o comentário da última tarefa em Detalhes da tarefa:** Selecione esta opção para exibir a última ação executada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **Tipo:** Escolha o tipo de documento a ser preenchido quando o workflow for iniciado. Você pode escolher um formulário adaptável, formulário adaptável somente leitura, um documento PDF não interativo, interface do usuário do Agente de comunicação interativa ou Documento do canal da Web de comunicação interativa.
* **Use o formulário adaptável:** Especifique o método para localizar o formulário adaptável de entrada. Essa opção estará disponível se você selecionar Adaptive form ou Read-only adaptive form na lista suspensa Type . É possível usar o formulário adaptável enviado para o fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
   Você pode associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

* **Usar comunicação interativa:** Especifique o método para localizar a comunicação interativa de entrada. Você pode usar a comunicação interativa enviada para o workflow, disponível em um caminho absoluto, ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho. Essa opção estará disponível se você selecionar Interative Communication Agent UI ou Interative Communication Web Channel Document na lista suspensa Tipo.

>[!NOTE]
>
>Você deve ter usuários com agente-cm e atribuições de grupo de usuários de fluxo de trabalho para acessar a interface do Agente de Comunicações Interativas AEM caixa de entrada.

* **Formulário adaptável ou caminho de comunicação interativo**: Especifique o caminho do formulário adaptável ou da Comunicação interativa. Você pode usar o formulário adaptável ou a comunicação interativa enviada ao workflow, disponível em um caminho absoluto, ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados da string.
* **Selecione PDF de entrada usando:** Especifique o caminho de um documento PDF não interativo. O campo fica disponível ao escolher um documento de PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Diretório_de_carga]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você precisa de uma opção Documento de registro ativada ou formulários adaptáveis baseados em modelo de formulário para usar a opção PDF Path.
* **Para tarefas concluídas, renderize o formulário adaptável como**: Quando uma tarefa é marcada como concluída, é possível renderizar o formulário adaptável como um formulário adaptável somente leitura ou um documento PDF. É necessário ativar uma opção Documento de registro ou formulários adaptáveis baseados em modelo de formulário para renderizar o formulário adaptável como Documento de registro.
* **Pré-preenchido:** Os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **[!UICONTROL Selecione o arquivo de dados de entrada usando]**: Caminho do arquivo de dados de entrada (.json, .xml, .doc ou modelo de dados de formulário). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga útil ou recuperar o arquivo armazenado em uma variável do tipo de dados Document, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo AEM Caixa de entrada. Um caminho de exemplo é [Diretório_de_carga]/workflow/data.

   * **Selecione anexos de entrada usando:** Os anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho pode ser relativo à carga ou recuperar os anexos armazenados em uma variável do tipo ArrayList of Document. Um caminho de exemplo é [Diretório_de_carga]/anexos/. Você pode especificar anexos colocados em relação à carga útil ou usar uma variável do tipo de documento (Lista de matriz > Documento) para especificar um anexo de entrada para o Formulário adaptável.

      * **Escolha o JSON de entrada:** Selecione um arquivo JSON de entrada usando um caminho relativo à carga ou armazenado em uma variável do tipo de dados Documento, JSON ou Modelo de dados de formulário. Essa opção estará disponível se você selecionar Interative Communication Agent UI ou Interative Communication Web Channel Document na lista suspensa Tipo.
      * **Escolha um serviço de preenchimento prévio personalizado:** Selecione o serviço de preenchimento prévio para recuperar os dados e preencher previamente o documento do canal Web de Comunicações interativas ou a interface do usuário do agente.
      * **Use o serviço de preenchimento prévio da comunicação interativa selecionada acima:** Use essa opção para usar o serviço de preenchimento prévio da Comunicação interativa definida na lista suspensa Usar comunicação interativa .
      * **Mapeamento do atributo da solicitação:** Use a seção Mapeamento de atributos da solicitação para definir a variável [nome e valor do atributo de solicitação](../../forms/using/work-with-form-data-model.md#bindargument). Recupere os detalhes da fonte de dados com base no nome e no valor do atributo especificados na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.\
         As opções de mapeamento de atributo de solicitação e serviço de preenchimento prévio estarão disponíveis somente se você selecionar Interface do usuário do Agente de Comunicação Interativa ou Documento do Canal da Web de Comunicação Interativa na lista suspensa Tipo .

* **Informações enviadas:** Os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **Salve o arquivo de dados de saída usando:** Salve o arquivo de dados (.json,. xml, .doc ou modelo de dados de formulário). O arquivo de dados contém informações enviadas por meio do formulário associado. Você pode salvar o arquivo de dados de saída usando um caminho relativo à carga ou armazená-lo em uma variável do tipo de dados Document, XML ou JSON. Por exemplo, [Diretório_de_carga]/Workflow/data, onde os dados são um arquivo.
   * **Salvar anexos usando:** Salve o formulário fornecido nos anexos em uma tarefa. Você pode salvar os anexos usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento.
   * **Salvar documento de registro usando:** Caminho para salvar um arquivo de Documento de registro. Por exemplo, [Diretório_de_carga]/DocumentofRecord/credit-card.pdf. Você pode salvar o Documento de registro usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados do Documento. Se você selecionar **Em relação à carga** , o Documento de registro não será gerado se o campo de caminho ficar vazio. Essa opção só estará disponível se você selecionar Adaptive form na lista suspensa Type .

   * **Salvar dados do Canal da Web usando:** Salve o arquivo de dados do Canal da Web usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados Documento, JSON ou Modelo de dados de formulário. Essa opção só estará disponível se você selecionar Interface do usuário do Agente de Comunicação Interativa na lista suspensa Tipo .
   * **Salve o documento do PDF usando:** Salve o documento do PDF usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados Document . Essa opção só estará disponível se você selecionar Interface do usuário do Agente de Comunicação Interativa na lista suspensa Tipo .
   * **Salvar modelo de layout usando:** Salve o modelo de layout usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados Document . O [modelo de layout](../../forms/using/layout-design-details.md) refere-se a um arquivo XDP criado usando o Forms Designer. Essa opção só estará disponível se você selecionar Interface do usuário do Agente de Comunicação Interativa na lista suspensa Tipo .

* **Destinatário > Atribuir opções:** Especifique o método para atribuir a tarefa a um usuário. Você pode atribuir dinamicamente a tarefa a um usuário ou grupo usando o script do Seletor de Participante ou atribuir a tarefa a um usuário ou grupo de AEM específico.
* **Seletor de participante:** A opção está disponível quando a variável **Dinamicamente para um usuário ou grupo** está selecionada no campo Assign options . Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte [Atribuir dinamicamente um fluxo de trabalho aos usuários](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Criando uma etapa personalizada do Adobe Experience Manager Dynamic Participant.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **Participantes:** O campo está disponível quando a variável **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** é selecionada na variável **Seletor de participante** campo. O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **Destinatário:** O campo está disponível quando a variável **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** é selecionado no **Seletor de participante** campo. O campo permite selecionar uma variável do tipo de dados String para definir o destinatário.

* **Argumentos:** O campo fica disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de Participante. O campo permite fornecer uma lista de argumentos separados por vírgula para o script selecionado no campo Seletor de participante.

* **Usuário ou grupo:** A tarefa é atribuída ao usuário ou grupo selecionado. A opção está disponível quando a variável **Para um usuário ou grupo específico** é selecionado no **Atribuir opções** campo. O campo lista todos os usuários e grupos do grupo de usuários do fluxo de trabalho.\
   O **Usuário ou grupo** O menu suspenso lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende de se você tem permissões de acesso no **usuários** no repositório crx para esse usuário específico.

* **[!UICONTROL Enviar email de notificação]**: Selecione essa opção para enviar notificações por email ao destinatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário ou grupo. Você pode usar o **[!UICONTROL Endereço de email do destinatário]** para especificar o mecanismo para recuperar o endereço de email.

* **[!UICONTROL Endereço de email do destinatário]**: Você pode armazenar endereço de email em uma variável, usar um literal para especificar um endereço de email permanente ou usar o endereço de email padrão do destinatário especificado no perfil do destinatário. Você pode usar o literal ou uma variável para especificar o endereço de email de um grupo. A opção de variável é útil na recuperação dinâmica e no uso de um endereço de email. O **[!UICONTROL Usar endereço de email padrão do destinatário]** é somente para um único destinatário. Nesse caso, o endereço de email armazenado no perfil de usuário atribuído é usado.

* **Modelo de email do HTML**: Selecione o modelo de email para o email de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no crx-repository.
* **Permitir delegação para:** AEM Caixa de entrada fornece uma opção para o usuário conectado delegar o fluxo de trabalho atribuído a outro usuário. Você pode delegar no mesmo grupo ou no usuário de workflow de outro grupo. Se a tarefa for atribuída a um único usuário e a variável **permitir delegação aos membros do grupo de destinatários** estiver selecionada, então não é possível delegar a tarefa a outro usuário ou grupo.
* **Compartilhar configurações:** AEM Caixa de entrada fornece opções para compartilhar uma única ou todas as tarefas na caixa de entrada com outros usuários:
   * Quando a variável **Permitir que o destinatário compartilhe explicitamente na caixa de entrada** for selecionada, o usuário poderá clicar na tarefa e compartilhá-la com outro usuário AEM.
   * Quando a variável **Permitir que o destinatário compartilhe via compartilhamento da caixa de entrada** for selecionada e um usuário compartilhar seus itens da Caixa de entrada ou permitir que outros usuários acessem seus itens da Caixa de entrada, somente as tarefas com a opção acima habilitada serão compartilhadas com outros usuários.

* **Ações > Ações padrão:** As ações Enviar, Salvar e Redefinir estão disponíveis e estão prontas para uso. Todas as ações padrão são habilitadas, por padrão.
* **Variável de rota:** Nome da variável de rota. A variável de rota captura ações personalizadas que um usuário seleciona AEM Caixa de entrada.
* **Rotas:** Uma tarefa pode ramificar para rotas diferentes. Quando selecionada em AEM Caixa de entrada, a rota retorna um valor e o workflow ramifica com base na rota selecionada. Você pode armazenar rotas em uma variável do tipo de dados String ou selecionar **Literal** para adicionar rotas manualmente.

* **Título**: Especifique o título da rota. Exibido em AEM Caixa de entrada.
* **Ícone Coral**: Especifique o atributo HTML de um ícone de coral. Adobe A biblioteca CorelUI fornece um vasto conjunto de ícones de toque primeiro. Você pode escolher e usar um ícone para a rota. Ele é exibido junto com o título em AEM Caixa de entrada. Se você armazenar as rotas em uma variável, as rotas usarão um ícone de coral &quot;Tags&quot; padrão.
* **Permitir ao destinatário adicionar comentário**: Selecione esta opção para habilitar comentários para a tarefa. Um destinatário pode adicionar os comentários de dentro AEM Caixa de entrada no momento do envio da tarefa.
* **Salve o comentário na variável :** Salve o comentário em uma variável do tipo de dados String . Essa opção será exibida somente se você selecionar a variável **Permitir ao destinatário adicionar comentário** caixa de seleção.

* **Permitir que o destinatário adicione anexos à tarefa**: Selecione esta opção para ativar anexos para a tarefa. Um destinatário pode adicionar os anexos de dentro AEM Caixa de entrada no momento do envio da tarefa.
* **Salvar anexos de tarefa de saída usando**: Especifique a localização da pasta de anexos. Você pode salvar anexos de tarefa de saída usando um caminho relativo à carga ou em uma variável de matriz de tipo de dados do documento. Essa opção será exibida somente se você selecionar a variável **Permitir que o destinatário adicione anexos à tarefa** e selecione **Formulário adaptável**, **Formulário adaptável somente leitura** ou **Documento de PDF não interativo** do **Tipo** na lista suspensa na **Formulário/Documento** guia .

>[!NOTE]
>
>Use a guia Anexos na interface do agente durante o tempo de execução para associar os anexos a uma Comunicação interativa. Os anexos associados são exibidos como anexos de tarefa no sidekick depois de abrir o item de trabalho em um estado Concluído.

* **Usar metadados personalizados:** Selecione essa opção para ativar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **Metadados personalizados:** Selecione metadados personalizados para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/dashboard/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Também é possível estender a interface WorkitemUserMetadataService para fornecer metadados personalizados.
* **Mostrar dados das etapas anteriores**: Selecione esta opção para permitir que os destinatários visualizem os destinatários anteriores, a ação já executada na tarefa, os comentários adicionados à tarefa e o documento de registro da tarefa concluída, se disponível.
* **Mostrar dados de etapas subsequentes:** Selecione essa opção para permitir que o destinatário atual visualize a ação executada e os comentários adicionados à tarefa pelos destinatários subsequentes. Também permite que o destinatário atual exiba um documento de registro da tarefa concluída, se disponível.
* **Visibilidade do tipo de dados:** Por padrão, um destinatário pode visualizar um Documento de registro, destinatários, ação tomada e comentários que destinatários anteriores e subsequentes adicionaram. Use a opção visibility of data type para limitar o tipo de dados visível para os destinatários.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar uma [!DNL Adobe Experience Manager] modelo de fluxo de trabalho para armazenamento externo de dados. Além disso, na Caixa de entrada, a opção para salvar está desativada.

## Etapa Enviar Email {#send-email-step}

Use a etapa de email para enviar um email, por exemplo, um email com um documento de registro, link de um formulário adaptável, link de uma comunicação interativa ou com um documento de PDF anexado. Enviar suporte à etapa de email [HTML email](https://en.wikipedia.org/wiki/HTML_email). Os emails do HTML são responsivos e adaptam-se ao cliente de email e ao tamanho da tela dos recipients. Você pode usar um modelo de email do HTML para definir a aparência, o esquema de cores e o comportamento do email.

A etapa de email usa o Day CQ Mail Service para enviar emails. Antes de usar a etapa de email, verifique se a variável [serviço de email](../../forms/using/aem-forms-workflow.md) está configurado. A etapa de email tem as seguintes propriedades:

**Título:** O título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**Descrição:** Explicação é útil para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

**Assunto do email:** O assunto pode ser recuperado de metadados de workflow, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione dentre as seguintes opções:

* **Literal -** Especificar um assunto manualmente.
* **Recuperar dos metadados do fluxo de trabalho** - Recupere o assunto de uma propriedade de metadados.
* **Variável** - Recupere o assunto do valor armazenado em uma variável do tipo de dados da string.

**Modelo de email do HTML**: modelo HTML para o email. Você pode especificar variáveis em um modelo de email. A Etapa de email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**Metadados de modelo de email:** O valor das variáveis do modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no autor ou no servidor de publicação, a imagem ou uma propriedade de metadados de workflow.

* **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **Metadados do fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Depois de selecionar a opção , insira o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho . Por exemplo, emailAddress.
* **URL do ativo:** Use a opção para incorporar um link da Web de uma comunicação interativa ao email. Após selecionar a opção , navegue e escolha a comunicação interativa a ser incorporada. O ativo pode residir no autor ou no servidor de publicação.
* **Imagem:** Use a opção para incorporar uma imagem ao email. Depois de selecionar a opção , navegue e escolha a imagem. A opção de imagem está disponível somente para as tags de imagem (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponíveis no modelo de email.&#42;

**Endereço de email do remetente/destinatário:** Selecione o **Literal** para especificar manualmente um endereço de email ou selecionar a opção **Recuperar dos metadados do fluxo de trabalho** para recuperar o endereço de email de uma propriedade de metadados. Também é possível especificar uma lista de matrizes de propriedades de metadados para a variável **Recuperar dos metadados do fluxo de trabalho** opção. Selecione o **Variável** para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados da string.

**Anexo de arquivo:** O ativo disponível no local especificado é anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um caminho de exemplo é [Diretório_de_carga]/anexos/.

Selecione o **Variável** para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Document, XML ou JSON.

**Nome do arquivo:** Nome do arquivo de anexo de email. A Etapa de email altera o nome de arquivo original do anexo para o nome de arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados de workflow ou de uma variável. Use o **Literal** quando você souber o valor exato a ser especificado. Use o **Variável** para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados da string. Use o **Recuperar de metadados de fluxo de trabalho** quando o valor a ser usado for salvo em uma propriedade de metadados de workflow.

## Etapa Gerar Documento de Registro {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, é possível manter um registro do formulário, em formato impresso ou documento. Isso é chamado de Documento de Registro (DoR). Você pode usar a etapa Gerar documento de registro para criar uma versão de PDF somente leitura ou interativa de um formulário adaptável. A versão PDF contém informações preenchidas para o formulário junto com o layout do formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**Usar formulário adaptável**: Especifique o método para localizar o formulário adaptável de entrada. É possível usar o formulário adaptável enviado para o fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho no **Selecione a variável a ser resolvida** campo.\
Você pode associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**Caminho do formulário adaptável**: Especifique o caminho do formulário adaptável. O campo fica disponível ao selecionar a variável **Disponível em um caminho absoluto** da **Usar formulário adaptável** campo.

**Selecione Input data usando:** Caminho dos dados de entrada para o formulário adaptável. Você pode manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável do tipo de dados Document, JSON ou XML. Os dados de entrada são unidos ao formulário adaptável para criar um documento de registro.

**Selecione Caminho do anexo de Entrada usando:** Caminho dos anexos. Esses anexos estão incluídos no Documento de registro. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável do tipo de dados Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao Documento de registro. Se algum arquivo estiver disponível nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de registro como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

**Salvar Documento Gerado de Registro usando as opções abaixo:** Especifique o local para manter um documento de arquivo de registro. Você pode optar por substituir a pasta de carga útil, colocar o documento de registro em um local dentro do diretório de carga ou armazenar o documento de registro em uma variável do tipo de dados Documento.

**Localidade**: Especifique o idioma do documento de registro. Selecionar **Literal** para selecionar a localidade em uma lista suspensa ou selecione **Variável** para recuperar a localidade do valor armazenado em uma variável do tipo de dados da string. Você deve definir o código local enquanto armazena o valor da localidade em uma variável. Por exemplo, especifique **en_US** em inglês e **fr_FR** para francês.

## Invoque a etapa Serviço do Modelo de Dados de Formulário {#invoke-form-data-model-service-step}

Você pode usar [Integração de dados do AEM Forms](../../forms/using/data-integration.md) para configurar e conectar-se a fontes de dados diferentes. Essas fontes de dados podem ser um banco de dados, serviço da Web, serviço REST, serviço OData e solução CRM. A Integração de dados do AEM Forms permite criar um modelo de dados de formulário que abrange vários serviços para executar operações de recuperação de dados, além de atualizar no banco de dados configurado. Você pode usar o **Invoque a etapa Serviço do Modelo de Dados** para selecionar um modelo de dados de formulário (FDM) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a fontes de dados diferentes.

Para explicar entradas para campos da etapa, a tabela de banco de dados a seguir e o arquivo JSON são usados como exemplo :

**Tabela de detalhes do cliente de exemplo**

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
   <td>Customer ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Endereço de email<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**Arquivo JSON de exemplo**

```json
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
* **Descrição:** Explicação útil para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **Caminho do modelo de dados de formulário**: Procure e selecione um modelo de dados de formulário presente no servidor.

* **Serviço**: Lista dos serviços fornecidos pelo modelo de dados de formulário selecionado.
* **Entrada para serviços > Fornecer dados de entrada usando metadados literais, variáveis ou de fluxo de trabalho e um arquivo JSON**: Um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço de uma propriedade de metadados de workflow, um objeto JSON, uma variável ou insira diretamente o valor na caixa de texto fornecida:

   * **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **Variável:** Use a opção para recuperar o valor armazenado em uma variável.
   * **Recuperar dos metadados do fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Por exemplo, emailAddress.
   * **[!UICONTROL Em relação à carga]**: Use a opção para recuperar o anexo de arquivo salvo em um caminho relativo à carga útil. Selecione a opção e especifique o nome da pasta que inclui o anexo do arquivo ou especifique o nome do anexo do arquivo na caixa de texto.

      Por exemplo, se a pasta Relative to Payload no repositório CRX incluir um anexo de arquivo no `attachment\attachment-folder` local, especifique `attachment\attachment-folder` na caixa de texto depois de selecionar a variável **[!UICONTROL Em relação à carga]** opção.
   * **Notação de ponto JSON:** Use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, Insurance.customerDetails.emailAddress. A opção Notação de pontos JSON só estará disponível se a opção Mapear campos de entrada do JSON de entrada estiver selecionada.
   * **Mapear campos de entrada do JSON de entrada:** Especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Form Data Model.

* **Entrada para serviços > Fornecer dados de entrada usando uma variável ou um arquivo JSON:** Selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **Selecione o documento JSON de entrada usando**: O arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **relativo à carga** ou **caminho absoluto.** Também é possível recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Form Data Model.

* **Notação de ponto JSON:** Deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON, por exemplo, Se você tiver um JSON semelhante ao listado no início da seção, especifique Insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **Saída do serviço > Mapear e gravar valores de saída em variáveis ou metadados:** Selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância de fluxo de trabalho no crx-repository. Especifique o nome da propriedade de metadados e selecione o atributo de saída de serviço correspondente a ser mapeado com a propriedade de metadados; por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, você pode armazenar a saída em uma variável do tipo de dados Long.Ao selecionar uma propriedade para o **[!UICONTROL Atributo de saída de serviço a ser mapeado]** , somente as variáveis capazes de armazenar dados da propriedade selecionada são preenchidas para a variável **[!UICONTROL Salve a saída em]** opção.

* **Saída do serviço > Salvar saída na variável ou em um arquivo JSON:** Selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga ou em uma variável .
* **Salve o documento JSON de saída usando as opções abaixo:** Salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga ou a um caminho absoluto. Também é possível salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Form Data Model.

## Etapa Assinar documento {#sign-document-step}

A etapa Assinar documento permite usar o Adobe Sign para assinar documentos. A etapa Assinar documento tem as seguintes propriedades:

* **Nome do Contrato:** Especifique o título do contrato. O nome do contrato se torna parte do assunto e do texto do corpo do email enviado aos signatários. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **Literal** para adicionar o nome manualmente.

* **Localidade:** Especifique o idioma para as opções de email e verificação. Você pode armazenar a localidade em uma variável do tipo de dados String ou selecionar **Literal** para escolher a localidade na lista de opções disponíveis. Você deve definir o código local enquanto armazena o valor da localidade em uma variável. Por exemplo, especifique **en_US** em inglês e **fr_FR** para francês.

* **Configuração da Adobe Sign Cloud**: Escolha uma Configuração da Adobe Sign Cloud. Se você não tiver configurado o Adobe Sign para AEM Forms, consulte [Integrar o Adobe Sign ao AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Selecione Documento a ser assinado usando:** Você pode escolher um documento de um local relativo à carga, usar carga como documento, especificar um caminho absoluto do documento ou recuperar o documento armazenado em uma variável do tipo de dados Documento.


* **Selecione Caminho do anexo de entrada usando:** Caminho dos anexos. Esses anexos estão incluídos no Documento de assinatura. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável do tipo de dados Documento.


Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao Documento de assinatura. Se algum arquivo estiver disponível nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de assinatura como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

* **Dias até o prazo:** Um documento é marcado como vencido (prazo vencido) depois que não há atividade na tarefa para o número de dias especificado na **Dias até o final do prazo** campo. O número de dias é contado depois que o documento é atribuído a um usuário para assinatura.
* **Frequência de email do lembrete:** Você pode enviar um email de lembrete diariamente ou semanalmente. A semana é contada a partir do dia em que o documento foi atribuído a um usuário para assinatura.
* **Processo de assinatura:** Você pode optar por assinar um documento em uma ordem sequencial ou paralela. Em ordem sequencial, um assinante recebe o documento por vez para assinatura. Depois que o primeiro assinante concluir a assinatura do documento, o documento será enviado para o segundo assinante e assim por diante. Em ordem paralela, vários signatários podem assinar um documento de cada vez.
* **URL de redirecionamento:** Especifique um URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou mais instruções.
* **Estágio do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Selecionar Assinantes:** Especifique o método para escolher os signatários do documento. Você pode atribuir dinamicamente o fluxo de trabalho a um usuário ou grupo ou adicionar manualmente detalhes de um assinante.
* **Script ou serviço para selecionar signatários:** A opção estará disponível somente se a opção Dinamicamente estiver selecionada no campo Selecionar signatários . Você pode especificar um ECMAScript ou um serviço para escolher assinantes e opções de verificação para um documento.
* **Detalhes do assinante:** A opção só estará disponível se a opção Manualmente estiver selecionada no campo Selecionar signatários . Especifique o endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação de duas etapas, verifique se a opção de verificação correspondente está habilitada para a conta do Adobe Sign configurada. Você pode usar uma variável do tipo de dados String para definir valores para **[!UICONTROL Email]**, **[!UICONTROL Código do país]** e **[!UICONTROL Número de telefone]** campos. O **[!UICONTROL Código do país]** e **[!UICONTROL Número de telefone]** os campos são exibidos somente se você selecionar **[!UICONTROL Verificação de telefone]** do **[!UICONTROL Verificação em duas etapas]** lista suspensa.
* **Variável de status:** Um documento habilitado para Adobe Sign armazena o status de assinatura do documento em uma variável do tipo de dados String. Especifique o nome da variável de status (adobeSignStatus). Uma variável de status de uma instância está disponível no CRXDE em /etc/workflow/instances/&lt;server>/&lt;date-time>/&lt;instance of=&quot;&quot; workflow=&quot;&quot; model=&quot;&quot;>/workItems/&lt;node>/metaData contém o status de uma variável.
* **Salve o documento assinado usando as opções abaixo:** Especifique o local para manter documentos assinados. Você pode optar por substituir o arquivo de carga útil, colocar o documento assinado em um local dentro do diretório de carga ou armazenar o documento assinado em uma variável do tipo Documento.

## Etapas dos Serviços de documento {#document-services-steps}

AEM serviços de documento são um conjunto de serviços para criar, montar e proteger documentos do PDF. O AEM Forms fornece uma etapa AEM Fluxo de trabalho separada para cada serviço de documento.

Semelhante a outras etapas do fluxo de trabalho do AEM Forms, como Atribuir tarefa, Enviar email e Assinar documento, você pode usar variáveis em todas as etapas AEM serviços de documento. Para obter mais informações sobre como criar e gerenciar variáveis, consulte [Variáveis em workflows AEM](../../forms/using/variable-in-aem-workflows.md).

### Aplicar etapa Carimbo de data/hora do documento {#apply-document-time-stamp-step}

Adicionar carimbo de data/hora a um documento. Você fornece detalhes do documento, como caminho do documento de entrada, nome do documento de entrada, local para armazenar dados exportados. Você pode optar por substituir o arquivo de carga útil existente, escolher um nome de arquivo diferente para armazenar dados em um arquivo diferente na pasta de carga útil, fornecer um caminho absoluto para os dados ou armazenar dados em uma variável do tipo de dados Documento.

### Converter em etapa da imagem {#convert-to-image-step}

Converte um documento do PDF em uma lista de imagens. Os formatos de imagem suportados são JPEG, JPEG2000, PNG e TIFF. As seguintes informações se aplicam às conversões de imagens de TIFF:

* Um arquivo TIFF de várias páginas é gerado.
* Algumas anotações não são incluídas em imagens TIFF. As anotações que exigem que o Acrobat gere sua aparência não são incluídas.

### Converter em etapa PDF/A {#convert-to-pdf-a-step}

Converte um documento PDF em formato PDF/A usando as opções fornecidas. A versão PDF/A do Portable Document Format (PDF) é especializada no arquivamento e na preservação de documentos a longo prazo.

### Etapa Converter em PS {#convert-to-ps-step}

Converta documentos PDF para PostScript. Ao converter para PostScript, você pode usar a operação de conversão para especificar o documento de origem e se deve ser convertido para o nível 2 ou 3 do PostScript. O documento do PDF que você converte em um arquivo PostScript deve ser não interativo.

### Criar PDF a partir da etapa de tipo especificada {#create-pdf-from-specified-type-step}

Gere um documento PDF a partir de um arquivo de entrada. O documento de entrada pode ser relativo à carga, ter um caminho absoluto, pode ser a própria carga ou armazenado em uma variável do tipo de dados Documento.

### Criar PDF a partir de URL/HTML/etapa ZIP {#create-pdf-from-url-html-zip-step}

Gera um documento PDF a partir do URL, HTML e arquivo ZIP fornecidos.

### Etapa Exportar dados {#export-data-step}

Exporta dados de um arquivo PDF forms ou XDP. Ele requer que você insira o caminho de arquivo do Documento de entrada e o Formato de dados de exportação. As opções para Exportar formato de dados são Auto, XDP e XmlData.

### Export PDF para a etapa de tipo especificada {#export-pdf-to-specified-type-step}

Converte um documento PDF em um formato selecionado.

### Gerar etapa PDF não interativa {#generatenoninteractive}

Gere um PDF não interativo. Ele fornece várias opções de personalização.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa Importação de dados {#import-data-step}

Une os dados do formulário em um formulário PDF. É possível importar dados de formulário para um formulário PDF.

### Invocar etapa DDX {#invokeddx}

Executa o arquivo DDX no mapa especificado de documentos de entrada e retorna os documentos PDF manipulados.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo DDX para documentos de entrada. Armazene o arquivo DDX em uma variável do tipo de dados Document ou XML.

### Optimize PDF step {#optimize-pdf-step}

Otimiza arquivos PDF, reduzindo seu tamanho. O resultado dessa conversão são arquivos PDF que podem ser menores do que suas versões originais. Essa operação também converte documentos PDF para a versão PDF especificada nos parâmetros de otimização.

As configurações de otimização especificam como os arquivos são otimizados. Estas são as configurações de exemplo:

* Versão do Target PDF
* Descartar objetos, como ações do JavaScript e miniaturas de página incorporadas
* Descartar dados do usuário, como comentários e anexos de arquivo
* Descartar configurações inválidas ou não usadas
* Compactação de dados descompactados ou uso de algoritmos de compactação mais eficientes
* Remoção de fontes incorporadas
* Configuração de valores de transparência

### Etapa de formulário PDF de renderização {#renderpdf}

Renderiza um formulário criado no Form Designer (XDP) em um formulário PDF.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa do Documento Seguro {#secure-document-step}

Criptografar, assinar e certificar um documento. O AEM Forms suporta criptografia baseada em senha e certificado. Você também pode escolher entre vários algoritmos para assinar documentos. Por exemplo, SHA-256 e SH-512. Você também pode usar a etapa do fluxo de trabalho para o leitor estender documentos do PDF. A etapa do fluxo de trabalho fornece a opção para habilitar a decodificação do código de barras, assinaturas digitais, importação e exportação de dados do PDF e outras opções.

### Enviar para etapa da impressora {#send-to-printer-step}

Envie um documento diretamente para uma impressora. Ele suporta os seguintes mecanismos de acesso de impressão:

* **Impressora acessível diretamente**: Uma impressora instalada no mesmo computador é chamada de impressora acessível diretamente e o computador é nomeado host da impressora. Esse tipo de impressora pode ser uma impressora local conectada diretamente ao computador.
* **Impressora direta acessível**: A impressora instalada em um servidor de impressão é acessada de outros computadores. Tecnologias como o CUPS (Common UNIX® Printer System) e o protocolo LPD (Line Printer Daemon) estão disponíveis para se conectar a uma impressora de rede. Para acessar uma impressora indireta acessível, especifique o IP ou o nome do host do servidor de impressão. Usando esse mecanismo, você pode enviar um documento para um URI LPD quando a rede tiver um LPD em execução. O mecanismo permite rotear o documento para qualquer impressora conectada à rede com um LPD em execução.

### Etapa Gerar Saída Impressa {#generatePrintedOutput}

A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL considerando um design de formulário e um arquivo de dados. O arquivo de dados é unido ao design de formulário e formatado para impressão. A saída gerada por esta etapa pode ser enviada diretamente para uma impressora ou salva como arquivo. É recomendável usar essa etapa quando quiser usar designs de formulário ou dados de um aplicativo. Se os designs de formulário ou designs de formulário estiverem localizados na rede, no sistema de arquivos local ou no local HTTP, use a operação generatePrintedOutput .

Por exemplo, seu aplicativo requer que você mescle um design de formulário com um arquivo de dados. Os dados contêm centenas de registros. Além disso, requer que a saída seja enviada para uma impressora que suporte ZPL. O design de formulário e seus dados de entrada estão localizados em um aplicativo. Use a operação generatePrintedOutput para unir cada registro a um design de formulário e enviar a saída para uma impressora que ofereça suporte a ZPL.

A etapa Gerar saída impressa tem as seguintes propriedades:

**Propriedades de entrada**

* **[!UICONTROL Selecionar arquivo de modelo usando]**: Especifique o caminho do arquivo de modelo. Você pode selecionar o arquivo de modelo usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Diretório_de_carga]/Workflow/data.xml. Se o caminho não existir no crx-repository, um administrador pode criar o caminho antes de usá-lo. Além disso, também é possível aceitar a carga como arquivo de dados de entrada.

* **[!UICONTROL Selecionar documento de dados usando]**: Especifique o caminho de um arquivo de dados de entrada. Você pode selecionar o arquivo de dados de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Diretório_de_carga]/Workflow/data.xml. Se o caminho não existir no crx-repository, um administrador pode criar o caminho antes de usá-lo.

* **[!UICONTROL Formato da impressora]**: Um valor de Formato de Impressão que especifica a linguagem de descrição da página a ser usada, quando um arquivo XDC não for fornecido, para gerar o fluxo de saída. Se você fornecer um valor literal, selecione um destes valores:

   * **[!UICONTROL PCL personalizado]**: Use a opção para especificar um arquivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript personalizado]**: Use a opção para especificar um arquivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL personalizado]**: Use a opção para especificar um arquivo XDC personalizado para ZPL.
   * **[!UICONTROL PCL de cor genérica (5c)]**: Use uma cor genérica PCL (5c).
   * **[!UICONTROL Nível 3 de PostScript Genérico]**: Use o PostScript Nível 3 genérico.
   * **[!UICONTROL ZPL 300 DPI]**: Utilizar ZPL 300 DPI. O zpl300.xdc é usado.
   * **[!UICONTROL ZPL 600 DPI]**: Utilizar ZPL 600 DPI. O arquivo zpl600.xdc é usado.
   * **[!UICONTROL IPL Personalizado]**: Use a opção para especificar um arquivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 DPI]**: Utilizar IPL 300 DPI. O ipl300.xdc é usado.
   * **[!UICONTROL IPL 400 DPI]**: Utilizar IPL 400 DPI. O arquivo ipl400.xdc é usado.
   * **[!UICONTROL TPCL personalizado]**: Use a opção para especificar um arquivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. O arquivo tpcl305.xdc é usado.
   * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. O arquivo tpcl600.xdc é usado.
   * **[!UICONTROL DPL personalizado]**: Use a opção para especificar um arquivo XDC personalizado DPL.
   * **[!UICONTROL DPL300DPI]**: Utilizar DPL 300 DPI. O arquivo dpl300.xdc é usado.
   * **[!UICONTROL DPL406DPI]**: Utilizar DPL 400 DPI. O dpl406.xdc é usado.
   * **[!UICONTROL DPL600DPI]**: Utilizar DPL 600 DPI. O dpl600.xdc é usado.

**Propriedades de saída**

* **[!UICONTROL Salvar documento de saída usando]**: Especifique o local para salvar o arquivo de saída. Você pode salvar o arquivo de saída em um local relativo à carga, em uma variável ou especificar um local absoluto para salvar o arquivo de saída. Se o caminho não existir no crx-repository, um administrador pode criar o caminho antes de usá-lo.

**Propriedades avançadas**

* **[!UICONTROL Selecionar local raiz do conteúdo usando]**: A raiz de conteúdo é um valor de string que especifica o URI, a referência absoluta ou o local no repositório para recuperar os ativos relativos usados pelo design de formulário. Por exemplo, se o design de formulário fizer referência a uma imagem relativamente, como ../myImage.gif, myImage.gif deve estar localizado em repository://. O valor padrão é repository://, que aponta para o nível raiz do repositório.

   Quando você seleciona um ativo do seu aplicativo, o caminho do URI da raiz de conteúdo deve ter a estrutura correta. Por exemplo, se um formulário for extraído de um aplicativo chamado SampleApp e for colocado em SampleApp/1.0/forms/Test.xdp, o URI da Raiz de Conteúdo deve ser especificado como repository://administrator@password/Applications/SampleApp/1.0/forms/ ou repository:/Applications/SampleApp/1.0/forms/ (quando a autoridade é nula). Quando o URI raiz do conteúdo é especificado dessa forma, os caminhos de todos os ativos referenciados no formulário serão resolvidos em relação a esse URI.

* **[!UICONTROL Selecione o arquivo XCI usando]**: Os arquivos XCI são usados para descrever fontes e outras propriedades usadas para elementos de design de formulário. Você pode manter um arquivo XCI relativo à carga, em um caminho absoluto ou usando uma variável do tipo de dados Document .

* **[!UICONTROL Localidade]**: Especifica o idioma usado para gerar o documento PDF. Se você fornecer um valor literal, selecione um idioma na lista ou selecione um destes valores:
   * **Para usar o padrão do servidor**: (Padrão) Use a configuração Local definida no AEM Forms Server. A configuração Local é configurada usando o Console de administração. (Consulte [Ajuda do Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **Para usar um valor personalizado**: Digite o Código de localidade na caixa literal ou selecione uma variável de string que contenha o código de localidade. Para obter uma lista completa dos códigos de localidade compatíveis, consulte http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Cópias]**: Um valor inteiro que especifica o número de cópias a serem geradas para a saída. O valor padrão é 1.

* **[!UICONTROL Impressão frente e verso]**: Um valor de Paginação que especifica o uso da impressão nos dois lados ou nos dois lados. As impressoras compatíveis com PostScript e PCL usam esse valor. Se você fornecer um valor literal, selecione um destes valores:
   * **[!UICONTROL Borda longa duplex]**: Use impressão nos dois lados e impressão usando paginação de borda longa.
   * **[!UICONTROL Borda curta duplex]**: Use impressão nos dois lados e impressão usando paginação de borda curta.
   * **[!UICONTROL Simplex]**: Use impressão em um único lado.
