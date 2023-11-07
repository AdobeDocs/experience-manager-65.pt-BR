---
title: Fluxo de trabalho centrado na Forms no OSGi - Referência da etapa
description: O fluxo de trabalho centrado na Forms nas etapas do OSGi permite criar rapidamente fluxos de trabalho baseados em formulários adaptáveis.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '7689'
ht-degree: 0%

---

# Fluxo de trabalho centrado na Forms no OSGi - Referência da etapa {#forms-centric-workflow-on-osgi-step-reference}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html) |
| AEM 6.5 | Este artigo |

Use modelos de fluxo de trabalho para converter uma lógica de negócios em um processo repetitivo automatizado. Um modelo ajuda a definir e executar uma série de etapas. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos. Você pode [incluir várias etapas do fluxo de trabalho do AEM em um modelo para atingir a lógica de negócios](/help/sites-developing/workflows-models.md#extending-aem).

## Etapas do Forms Workflow {#forms-workflow-steps}

As etapas do Forms Workflow executam operações específicas do AEM Forms em um fluxo de trabalho AEM. Essas etapas permitem criar rapidamente formulários adaptáveis com base no fluxo de trabalho centrado no Forms no OSGi. Esses workflows podem ser usados para desenvolver workflows básicos de revisão e aprovação, processos comerciais internos e entre firewalls. Você também pode usar as etapas Forms Workflow para iniciar serviços de documentos, integrar com o fluxo de trabalho de assinatura do Adobe Sign e executar outras operações do AEM Forms. Você precisa [Complemento do AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) para usar essas etapas em um workflow.

As etapas de fluxo de trabalho centradas no Forms executam operações específicas do AEM Forms em um fluxo de trabalho do AEM. Forms Essas etapas permitem criar rapidamente um fluxo de trabalho adaptável baseado em Forms no OSGi. Esses workflows podem ser usados para desenvolver workflows básicos de revisão e aprovação, processos comerciais internos e entre firewalls.

>[!NOTE]
>
>Se o modelo de fluxo de trabalho estiver marcado para um armazenamento externo, para todas as etapas de Forms Workflow, será possível selecionar apenas a opção de variável para armazenar ou recuperar arquivos de dados e anexos.

## Atribuir etapa de tarefa {#assign-task-step}

A etapa atribuir tarefa cria uma tarefa e a atribui a um usuário ou grupo. Junto com a atribuição da tarefa, o componente também especifica o formulário adaptável ou PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar entradas de usuários e PDF não interativos ou um formulário adaptável somente leitura é usado para workflows somente revisão.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem pré-preenchidos e especificar ações padrão. A etapa Atribuir tarefa tem as seguintes propriedades:

* **Título:** Título da tarefa. O título é exibido na Caixa de entrada AEM.
* **Descrição:** Explicação das operações sendo executadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **Caminho da miniatura:** Caminho da miniatura da tarefa. Se nenhum caminho for especificado, para uma miniatura padrão de formulário adaptável será exibida e para o Documento de registro, um ícone padrão será exibido.
* **Estágio do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Prioridade:** A prioridade selecionada é exibida na Caixa de entrada AEM. As opções disponíveis são Alta, Média e Baixa. O valor padrão é Médio.
* **Prazo:** Especifique o número de dias ou horas após o qual a tarefa será marcada como vencida. Se você selecionar **Desligado**, a tarefa nunca será marcada como vencida. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver vencida.

* **Dias:** O número de dias antes dos quais a tarefa deve ser concluída. O número de dias é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de dias especificado no campo Dias, então, se selecionado, um manipulador de tempo limite será acionado após a data de vencimento.
* **Horas:** O número de horas antes das quais a tarefa deve ser concluída. O número de horas é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de horas especificado no campo Horas, então, se selecionado, um manipulador de tempo limite será acionado após as horas de vencimento.
* **Tempo limite após a data de vencimento:** Selecione esta opção para ativar o campo de seleção Manipulador de tempo limite.
* **Manipulador de tempo limite:** Selecione o script a ser executado quando a etapa de atribuição da tarefa ultrapassar a data de vencimento. Scripts colocados no repositório CRX em [aplicativos]/fd/dashboard/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **Realçar a ação e o comentário da última tarefa em Detalhes da tarefa:** Selecione essa opção para exibir a última ação realizada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **Tipo:** Escolha o tipo de documento a ser preenchido quando o fluxo de trabalho for iniciado. Você pode escolher um formulário adaptável, um formulário adaptável somente leitura, um documento PDF não interativo, a interface do usuário do agente de comunicação interativa ou o documento de canal da Web de comunicação interativa.
* **Usar formulário adaptável:** Especifique o método para localizar o formulário adaptável de entrada. Essa opção estará disponível se você selecionar Formulário adaptável ou Formulário adaptável somente leitura na lista suspensa Tipo. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
  É possível associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

* **Usar a comunicação interativa:** Especifique o método para localizar a comunicação interativa de entrada. É possível usar a comunicação interativa enviada para o workflow, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho. Essa opção estará disponível se você selecionar Interface do usuário do agente de comunicação interativa ou Documento do canal da Web de comunicação interativa na lista suspensa Tipo.

>[!NOTE]
>
>Você deve ter atribuições de grupo cm-agent-users e workflow-users para acessar a interface do usuário do Agente de comunicações interativas na Caixa de entrada do AEM.

* **Formulário adaptável ou caminho de comunicação interativa**: especifique o caminho do formulário adaptável ou da Comunicação interativa. Você pode usar o formulário adaptável ou a comunicação interativa enviada ao fluxo de trabalho, disponível em um caminho absoluto ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados string.
* **Selecione o PDF de entrada usando:** Especifique o caminho de um documento PDF não interativo. O campo está disponível ao escolher um documento PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você precisa de uma opção Documento de registro ativada ou de formulários adaptáveis baseados em modelo de formulário para usar a opção Caminho do PDF.
* **Na tarefa concluída, renderize o formulário adaptável como**: Quando uma tarefa é marcada como concluída, você pode renderizar o formulário adaptável como um formulário adaptável somente leitura ou um documento PDF. Você precisa de uma opção Documento de registro ativada ou de formulários adaptáveis baseados em modelo de formulário para renderizar o formulário adaptável como Documento de registro.
* **Preenchido:** Os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **[!UICONTROL Selecione o arquivo de dados de entrada usando]**: caminho do arquivo de dados de entrada (.json, .xml, .doc ou modelo de dados de formulário). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga útil ou recuperar o arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo Caixa de entrada AEM. Um exemplo de caminho é [Payload_Diretory]/workflow/data.

   * **Selecione os anexos de entrada usando:** Anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho pode ser relativo à carga ou recuperar os anexos armazenados em uma variável do tipo ArrayList of Document. Um exemplo de caminho é [Payload_Diretory]/attachments/. Você pode especificar anexos colocados em relação à carga ou usar uma variável do tipo de documento (Lista de matriz > Documento) para especificar um anexo de entrada para o Formulário adaptável.

      * **Escolha o JSON de entrada:** Selecione um arquivo JSON de entrada usando um caminho relativo à carga ou armazenado em uma variável do tipo de dados Documento, JSON ou Modelo de dados de formulário. Essa opção estará disponível se você selecionar Interface do usuário do agente de comunicação interativa ou Documento do canal da Web de comunicação interativa na lista suspensa Tipo.
      * **Escolha um serviço personalizado:** Selecione o serviço de preenchimento prévio para recuperar os dados e preencher previamente o documento do canal da Web de comunicação interativa ou a interface do usuário do agente.
      * **Utilizar o serviço de preenchimento da comunicação interativa selecionada acima:** Use essa opção para usar o serviço de preenchimento prévio da Comunicação interativa definida na lista suspensa Usar comunicação interativa.
      * **Mapeamento de atributo de solicitação:** Use a seção Mapeamento do atributo de solicitação para definir a [nome e valor do atributo de solicitação](../../forms/using/work-with-form-data-model.md#bindargument). Recupere os detalhes da fonte de dados com base no nome e valor do atributo especificado na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.\
        As opções de mapeamento de serviço de preenchimento prévio e atributo de solicitação estarão disponíveis somente se você selecionar Interface do usuário do agente de comunicação interativa ou Documento de canal da Web de comunicação interativa na lista suspensa Tipo.

* **Informações enviadas:** Os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **Salvar arquivo de dados de saída usando:** Salve o arquivo de dados (.json,. xml, .doc ou modelo de dados de formulário). O arquivo de dados contém informações enviadas por meio do formulário associado. Você pode salvar o arquivo de dados de saída usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, [Payload_Diretory]/Workflow/data, onde os dados são um arquivo.
   * **Salvar anexos usando:** Salve os anexos de formulário fornecidos em uma tarefa. Você pode salvar os anexos usando um caminho relativo à carga útil ou armazená-lo em uma variável de matriz do tipo de dados Documento.
   * **Salvar documento de registro usando:** Caminho para salvar um arquivo de documento de registro. Por exemplo, [Payload_Diretory]/DocumentofRecord/credit-card.pdf. Você pode salvar o documento de registro usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento. Se você selecionar **Relativo à carga útil** , o documento de registro não será gerado se o campo de caminho estiver vazio. Essa opção estará disponível somente se você selecionar Formulário adaptável na lista suspensa Tipo.

   * **Salvar dados do canal da Web usando:** Salve o arquivo de dados do Canal da Web usando um caminho relativo à carga ou armazene-o em uma variável do tipo de dados Documento, JSON ou Modelo de dados de formulário. Essa opção estará disponível somente se você selecionar Interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.
   * **Salvar documento de PDF usando:** Salve o documento PDF usando um caminho relativo à carga útil ou armazene-o em uma variável do tipo de dados Documento. Essa opção estará disponível somente se você selecionar Interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.
   * **Salvar modelo de layout usando:** Salve o modelo de layout usando um caminho relativo à carga útil ou armazene-o em uma variável do tipo de dados Documento. A variável [modelo de layout](../../forms/using/layout-design-details.md) refere-se a um arquivo XDP criado por você usando o Forms Designer. Essa opção estará disponível somente se você selecionar Interface do usuário do Agente de comunicação interativa na lista suspensa Tipo.

* **Destinatário > Atribuir opções:** Especifique o método para atribuir a tarefa a um usuário. Você pode atribuir dinamicamente a tarefa a um usuário ou grupo usando o script Seletor de participante ou atribuir a tarefa a um usuário ou grupo AEM específico.
* **Seletor de participantes:** A opção está disponível quando a variável **Dinamicamente para um usuário ou grupo** for selecionada no campo Assign options. Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte [Atribuir dinamicamente um fluxo de trabalho aos usuários](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Criação de uma etapa personalizada de Participante dinâmico do Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **Participantes:** O campo está disponível quando a variável **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** estiver selecionada na caixa **Seletor de participantes** campo. O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **Destinatário:** O campo está disponível quando a variável **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** está selecionado no **Seletor de participantes** campo. O campo permite selecionar uma variável de tipo de dados String para definir o destinatário.

* **Argumentos:** O campo está disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de participantes. O campo permite fornecer uma lista de argumentos separados por vírgula para o script selecionado no campo Seletor de participantes.

* **Usuário ou Grupo:** A tarefa é atribuída ao usuário ou grupo selecionado. A opção está disponível quando a variável **Para uma opção específica de usuário ou grupo** está selecionado no **Opções de atribuição** campo. O campo lista todos os usuários e grupos do grupo workflow-usuários.\
  A variável **Usuário ou grupo** lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende se você tem permissões de acesso no **usuários** no repositório crx para esse usuário específico.

* **[!UICONTROL Enviar email de notificação]**: selecione essa opção para enviar notificações por email ao signatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário ou grupo. Você pode usar o **[!UICONTROL Endereço de email do destinatário]** opção para especificar o mecanismo para recuperar o endereço de email.

* **[!UICONTROL Endereço de email do destinatário]**: você pode armazenar o endereço de email em uma variável, usar um literal para especificar um endereço de email permanente ou usar o endereço de email padrão do destinatário especificado no perfil do destinatário. Você pode usar o literal ou uma variável para especificar o endereço de email de um grupo. A opção de variável é útil para recuperar e usar dinamicamente um endereço de email. A variável **[!UICONTROL Usar endereço de email padrão do destinatário]** A opção é somente para um único destinatário. Nesse caso, o endereço de email armazenado no perfil de usuário dos atribuídos é usado.

* **Modelo de e-mail HTML**: selecione o modelo de email para o email de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no repositório crx.
* **Permitir delegação para:** A Caixa de entrada AEM fornece uma opção ao usuário conectado para delegar o fluxo de trabalho atribuído a outro usuário. Você tem permissão para delegar no mesmo grupo ou para o usuário de workflow de outro grupo. Se a tarefa for atribuída a um único usuário e a variável **permitir delegação a membros do grupo responsável** for selecionada, não será possível delegar a tarefa a outro usuário ou grupo.
* **Configurações de compartilhamento:** A Caixa de entrada AEM fornece opções para compartilhar uma única tarefa ou todas as tarefas na caixa de entrada com outros usuários:
   * Quando a variável **Permitir que o destinatário compartilhe explicitamente na caixa de entrada** for selecionada, o usuário poderá clicar na tarefa e compartilhá-la com outro usuário AEM.
   * Quando a variável **Permitir que o destinatário compartilhe através do compartilhamento da caixa de entrada** for selecionada e um usuário compartilhar seus itens da Caixa de entrada ou permitir que outros usuários acessem seus itens da Caixa de entrada, somente as tarefas com a opção mencionada acima ativada serão compartilhadas com outros usuários.

* **Ações > Ações padrão:** As ações Enviar, Salvar e Redefinir prontas para uso estão disponíveis. Todas as ações padrão são ativadas, por padrão.
* **Variável de rota:** Nome da variável de rota. A variável de rota captura as ações personalizadas que um usuário seleciona na Caixa de entrada do AEM.
* **Rotas:** Uma tarefa pode se ramificar para rotas diferentes. Quando selecionado na Caixa de entrada do AEM, o roteiro retorna um valor e o workflow ramifica com base no roteiro selecionado. Você pode armazenar rotas em uma variável de matriz do tipo de dados String ou selecionar **Literal** para adicionar rotas manualmente.

* **Título**: especifique o título do roteiro. É exibido na Caixa de entrada do AEM.
* **Ícone do Coral**: Especifique o atributo HTML de um ícone de coral. A biblioteca CorelUI do Adobe fornece um vasto conjunto de ícones de primeiro toque. Você pode escolher e usar um ícone para a rota. É exibido junto com o título na Caixa de entrada AEM. Se você armazenar as rotas em uma variável, elas usarão um ícone de coral &quot;Tags&quot; padrão.
* **Permitir ao signatário adicionar comentário**: selecione essa opção para ativar comentários para a tarefa. Um signatário pode adicionar os comentários da Caixa de entrada AEM no momento do envio da tarefa.
* **Salvar comentário na variável:** Salve o comentário em uma variável do tipo de dados String. Essa opção será exibida somente se você selecionar a opção **Permitir ao signatário adicionar comentário** caixa de seleção

* **Permitir ao signatário adicionar anexos à tarefa**: selecione esta opção para ativar anexos para a tarefa. Um destinatário pode adicionar os anexos da Caixa de entrada AEM no momento do envio da tarefa.
* **Salvar anexos de saída da tarefa usando**: especifique o local da pasta de anexos. Você pode salvar anexos de saída da tarefa usando um caminho relativo à carga útil ou em uma variável de matriz do tipo de dados do documento. Essa opção será exibida somente se você selecionar a opção **Permitir ao signatário adicionar anexos à tarefa** e selecione **Formulário adaptável**, **Formulário adaptável somente leitura** ou **Documento PDF não interativo** do **Tipo** lista suspensa na **Formulário/Documento** guia.

>[!NOTE]
>
>Use a guia Anexos na interface do usuário do agente durante o tempo de execução para associar os anexos a uma comunicação interativa. Os anexos associados são exibidos como anexos de tarefa no sidekick após abrir o item de trabalho em um estado Concluído.

* **Usar metadados personalizados:** Selecione essa opção para ativar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **Metadados personalizados:** Selecione metadados personalizados para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/dashboard/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Também é possível estender a interface WorkitemUserMetadataService para fornecer metadados personalizados.
* **Mostrar dados das etapas anteriores**: selecione essa opção para permitir que os atribuídos exibam os atribuídos anteriores, a ação já tomada na tarefa, os comentários adicionados à tarefa e o documento de registro da tarefa concluída, se disponível.
* **Mostrar dados das etapas subsequentes:** Selecione esta opção para permitir que o destinatário atual visualize a ação executada e os comentários adicionados à tarefa pelos atribuídos subsequentes. Também permite que o responsável atual exiba um documento de registro da tarefa concluída, se disponível.
* **Visibilidade do tipo de dados:** Por padrão, um destinatário pode exibir um documento de registro, destinatários, ações executadas e comentários adicionados por destinatários anteriores e subsequentes. Use a opção de visibilidade do tipo de dados para limitar o tipo de dados visível para os atribuídos.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um [!DNL Adobe Experience Manager] modelo de fluxo de trabalho para armazenamento de dados externo. Além disso, na Caixa de entrada, a opção para salvar está desativada.

## Etapa Enviar email {#send-email-step}

Use a etapa do email para enviar um email, por exemplo, um email com um documento de registro, link de um formulário adaptável, link de uma comunicação interativa ou com um documento PDF anexado. Suporte à etapa Enviar email [email do HTML](https://en.wikipedia.org/wiki/HTML_email). Os emails de HTML são responsivos e se adaptam ao cliente de email dos recipients e ao tamanho da tela. Você pode usar um template de email HTML para definir a aparência, o esquema de cores e o comportamento do email.

A etapa de email usa o Day CQ Mail Service para enviar emails. Antes de usar a etapa de email, verifique se [serviço de e-mail](../../forms/using/aem-forms-workflow.md) está configurado. A etapa de email tem as seguintes propriedades:

**Título:** O título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**Descrição:** A explicação é útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

**Assunto do email:** O assunto pode ser recuperado de metadados de fluxo de trabalho, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione entre as seguintes opções:

* **Literal -** Especificar manualmente um assunto.
* **Recuperar dos metadados de fluxo de trabalho** - Recuperar o assunto de uma propriedade de metadados.
* **Variável** - Recupere o assunto do valor armazenado em uma variável do tipo de dados string.

**Modelo de e-mail HTML**: modelo de HTML para o email. Você pode especificar variáveis em um template de email. A etapa Email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**Metadados do modelo de email:** O valor das variáveis de modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no autor ou no servidor de publicação, a imagem ou uma propriedade de metadados de fluxo de trabalho.

* **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **Metadados do fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de fluxo de trabalho. Depois de selecionar a opção, insira o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho. Por exemplo, emailAddress.
* **URL do ativo:** Use a opção para incorporar ao email um link da Web de uma comunicação interativa. Depois de selecionar a opção, navegue e escolha a comunicação interativa a ser incorporada. O ativo pode residir no autor ou no servidor de publicação.
* **Imagem:** Use a opção para incorporar uma imagem ao email. Depois de selecionar a opção, navegue e escolha a imagem. A opção de imagem está disponível somente para as tags de imagem (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponíveis no template de email.&#42;

**Endereço de email do remetente/destinatário:** Selecione o **Literal** opção para especificar manualmente um endereço de email ou selecionar o **Recuperar dos metadados de fluxo de trabalho** opção para recuperar o endereço de email de uma propriedade de metadados. Você também pode especificar uma lista de matrizes de propriedades de metadados para o **Recuperar dos metadados de fluxo de trabalho** opção. Selecione o **Variável** opção para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados string.

**Anexo de arquivo:** O ativo disponível no local especificado é anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um exemplo de caminho é [Payload_Diretory]/attachments/.

Selecione o **Variável** opção para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON.

**Nome do arquivo:** Nome do arquivo de anexo de email. A Etapa Email altera o nome de arquivo original do anexo para o nome de arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados de fluxo de trabalho ou de uma variável. Use o **Literal** opção quando você souber o valor exato a ser especificado. Use o **Variável** opção para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados string. Use o **Recuperar de metadados de fluxo de trabalho** opção quando o valor a ser usado é salvo em uma propriedade de metadados de workflow.

## Etapa Gerar documento de registro {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, você pode manter um registro do formulário, impresso ou no formato do documento. Isso é chamado de Documento de registro (DoR). Você pode usar a etapa Gerar documento de registro para criar uma versão de PDF somente leitura ou interativa de um formulário adaptável. A versão do PDF contém informações preenchidas no formulário junto com o layout do formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**Usar formulário adaptável**: especifique o método para localizar o formulário adaptável de entrada. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho na variável **Selecionar variável para resolver** campo.\
É possível associar vários formulários adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**Caminho do formulário adaptável**: especifique o caminho do formulário adaptável. O campo está disponível ao selecionar a variável **Disponível em um caminho absoluto** opção no **Usar formulário adaptável** campo.

**Selecione os dados de entrada usando:** Caminho dos dados de entrada para o formulário adaptável. Você pode manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável do tipo de dados Documento, JSON ou XML. Os dados de entrada são mesclados com o formulário adaptável para criar um documento de registro.

**Selecione o caminho do anexo de entrada usando:** Caminho dos anexos. Esses anexos são incluídos no documento de registro. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável de matriz do tipo de dados Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao documento de registro. Se houver arquivos disponíveis nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de registro como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

**Salve o documento de registro gerado usando as opções abaixo:** Especifique o local para manter um documento de arquivo de registro. Você pode optar por substituir a pasta de carga útil, colocar o documento de registro em um local no diretório da carga útil ou armazenar o documento de registro em uma variável do tipo de dados Documento.

**Localidade**: especifique o idioma do documento de registro. Selecionar **Literal** para selecionar o local em uma lista suspensa ou selecione **Variável** para recuperar o local do valor armazenado em uma variável do tipo de dados string. Você deve definir o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **pt_BR** para inglês e **fr_FR** para o francês.

## Chamar etapa do serviço de modelo de dados de formulário {#invoke-form-data-model-service-step}

Você pode usar [Integração de dados do AEM Forms](../../forms/using/data-integration.md) para configurar e conectar-se a diferentes fontes de dados. Essas fontes de dados podem ser um banco de dados, serviço Web, serviço REST, serviço OData e solução de CRM. A Integração de dados do AEM Forms permite criar um modelo de dados de formulário que abrange vários serviços para executar operações de recuperação, adição e atualização de dados no banco de dados configurado. Você pode usar o **Chamar etapa de serviço do modelo de dados** para selecionar um modelo de dados de formulário (FDM) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a diferentes fontes de dados.

Para explicar entradas para campos da etapa, a seguinte tabela de banco de dados e arquivo JSON são usados como exemplo:

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

**Arquivo JSON de amostra**

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

A etapa Chamar serviço do modelo de dados de formulário tem os campos listados abaixo para facilitar as operações do modelo de dados de formulário:

* **Título:** Título da etapa. Ajuda a identificar a etapa no editor de workflow.
* **Descrição:** Explicação útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **Caminho do modelo de dados de formulário**: Procure e selecione um modelo de dados de formulário presente no servidor.

* **Serviço**: lista dos serviços que o modelo de dados de formulário selecionado fornece.
* **Entrada para serviços > Forneça dados de entrada usando literal, variável ou metadados de fluxo de trabalho e um arquivo JSON**: um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço de uma propriedade de metadados do fluxo de trabalho, um objeto JSON, uma variável ou insira o valor diretamente na caixa de texto fornecida:

   * **Literal:** Use a opção quando souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **Variável:** Use a opção para recuperar o valor armazenado em uma variável.
   * **Recuperar dos metadados de fluxo de trabalho:** Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de fluxo de trabalho. Por exemplo, emailAddress.
   * **[!UICONTROL Relativo à carga útil]**: use a opção para recuperar o anexo de arquivo salvo em um caminho relativo à carga. Selecione a opção e especifique o nome da pasta que inclui o anexo de arquivo ou especifique o nome do anexo de arquivo na caixa de texto.

     Por exemplo, se a pasta Relativo à carga no repositório CRX incluir um anexo de arquivo na `attachment\attachment-folder` local, especificar `attachment\attachment-folder` na caixa de texto após selecionar a variável **[!UICONTROL Relativo à carga útil]** opção.
   * **Anotação JSON Dot:** Use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, insurance.customerDetails.emailAddress. A opção Anotação JSON Dot estará disponível somente se a opção Mapear campos de entrada a partir de JSON de entrada estiver selecionada.
   * **Mapear campos de entrada do JSON de entrada:** Especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Modelo de dados de formulário.

* **Entrada para serviços > Forneça dados de entrada usando variável ou um arquivo JSON:** Selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga útil ou em uma variável.
* **Selecione o documento JSON de entrada usando**: o arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **relativo à carga útil** ou um **caminho absoluto.** Você também pode recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Modelo de dados de formulário.

* **Anotação JSON Dot:** Deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON. Por exemplo, se você tiver um JSON semelhante ao listado no início da seção, especifique insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **Saída do serviço > Mapear e gravar valores de saída na variável ou nos metadados:** Selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância do fluxo de trabalho no repositório crx. Especifique o nome da propriedade de metadados e selecione o atributo de saída de serviço correspondente a ser mapeado com a propriedade de metadados, por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, você pode armazenar a saída em uma variável do tipo de dados Long. Ao selecionar uma propriedade para a variável **[!UICONTROL Atributo de saída de serviço a ser mapeado]** opção, somente as variáveis capazes de armazenar dados da propriedade selecionada serão preenchidas para o **[!UICONTROL Salvar a saída em]** opção.

* **Saída do serviço > Salvar saída na variável ou em um arquivo JSON:** Selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga útil ou em uma variável.
* **Salve o documento JSON de saída usando as opções abaixo:** Salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga útil ou a um caminho absoluto. Você também pode salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Modelo de dados de formulário.

## Etapa Assinar documento {#sign-document-step}

A etapa Assinar documento permite usar o Adobe Sign para assinar documentos. A etapa Assinar documento tem as seguintes propriedades:

* **Nome do Contrato:** Especifique o título do contrato. O nome do contrato torna-se parte do assunto e do corpo do texto do email enviado aos recipients. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **Literal** para adicionar o nome manualmente.

* **Localidade:** Especifique o idioma para as opções de email e verificação. Você pode armazenar o local em uma variável do tipo de dados String ou selecionar **Literal** para escolher o local na lista de opções disponíveis. Você deve definir o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **pt_BR** para inglês e **fr_FR** para o francês.

* **Configuração da nuvem do Adobe Sign**: escolha uma configuração de nuvem do Adobe Sign. Se não tiver configurado o Adobe Sign para o AEM Forms, consulte [Integrar o Adobe Sign com o AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Selecione o documento a ser assinado usando:** Você pode escolher um documento de um local relativo à carga útil, usar a carga útil como o documento, especificar um caminho absoluto do documento ou recuperar o documento armazenado em uma variável do tipo de dados Documento.


* **Selecione o caminho do anexo de entrada usando:** Caminho dos anexos. Esses anexos estão incluídos no Documento de assinatura. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável de matriz do tipo de dados Documento.


  Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao Documento de assinatura. Se algum arquivo estiver disponível nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de assinatura como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

* **Dias até o prazo final:** Um documento está marcado como vencido (com prazo excedido) depois que não há nenhuma atividade na tarefa pelo número de dias especificado no **Dias até o prazo** campo. O número de dias é contado depois que o documentado é atribuído a um usuário para assinatura.
* **Frequência de e-mails de lembrete:** Você pode enviar um email de lembrete em intervalos diários ou semanais. A semana é contada a partir do dia em que o documento é atribuído a um usuário para assinatura.
* **Processo de assinatura:** Você pode optar por assinar um documento em uma ordem sequencial ou paralela. Em ordem sequencial, um destinatário recebe o documento de cada vez para assinar. Depois que o primeiro destinatário concluir a assinatura do documento, o documento será enviado para o segundo destinatário e assim por diante. Em ordem paralela, vários destinatários podem assinar um documento de cada vez.
* **URL de redirecionamento:** Especifique um URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou mais instruções.
* **Estágio do fluxo de trabalho:** Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **Selecionar Destinatários:** Especifique o método para escolher o destinatário do documento. Você pode atribuir o fluxo de trabalho de maneira dinâmica a um usuário ou grupo ou adicionar manualmente os detalhes de um recipient. Ao selecionar Manualmente na lista suspensa, você adiciona detalhes do recipient, como Email, Função e Método de autenticação.

  >[!NOTE]
  >
  >* Na seção Função, você pode especificar a função do destinatário como Signatário, Aprovador, Aceitador, Destinatário certificado, Preenchedor de formulário e Delegador.
  >* Se você selecionar Delegator na opção Role, o Delegator poderá atribuir a tarefa de assinatura a outros recipients.
  >* Se você tiver configurado um método de autenticação para [!DNL Adobe Sign], com base em sua configuração, você seleciona um método de autenticação, como autenticação baseada em telefone, autenticação baseada em identidade social, autenticação baseada em conhecimento, autenticação baseada em identidade governamental.


* **Script ou serviço para selecionar destinatários:** A opção estará disponível somente se a opção Dynamically estiver selecionada no campo Select Recipients. Você pode especificar um ECMAScript ou um serviço para escolher os destinatários e as opções de verificação de um documento.
* **Detalhes do destinatário:** A opção estará disponível somente se a opção Manually estiver selecionada no campo Select Recipients. Especifique o endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação de duas etapas, verifique se a opção de verificação correspondente está habilitada para a conta configurada do Adobe Sign. Você pode usar uma variável do tipo de dados String para definir valores para **[!UICONTROL E-mail]**, **[!UICONTROL Código do país]**, e **[!UICONTROL Número de telefone]** campos. A variável **[!UICONTROL Código do país]** e **[!UICONTROL Número de telefone]** os campos são exibidos somente se você selecionar **[!UICONTROL Verificação de telefone]** do **[!UICONTROL Verificação de 2 etapas]** lista suspensa.
* **Variável de status:** Um documento habilitado para Adobe Sign armazena o status de assinatura do documento em uma variável do tipo de dados String. Especifique o nome da variável de status (adobeSignStatus). Uma variável de status de uma instância está disponível no CRXDE em /etc/workflow/instances/&lt;server>/&lt;date-time>/&lt;instance of=&quot;&quot; workflow=&quot;&quot; model=&quot;&quot;>/workItems/&lt;node>/metaData contém o status de uma variável.
* **[!UICONTROL Documento assinado]**: é possível salvar o status do documento assinado na variável. Para adicionar uma trilha de auditoria de assinatura eletrônica para maior segurança e legalidade ao Documento assinado, você pode Incluir o Relatório de auditoria. Você pode salvar o documento assinado usando a pasta Variável ou Carga.
  >[!NOTE]
  >
  > O relatório de auditoria é anexado à última página do documento assinado.
<!--
* **Save signed document using below options:** Specify the location to keep signed documents. You can choose to overwrite the payload file, place the signed document at a location within the payload directory, or store the signed document in a variable of Document type.
-->

## Etapas dos serviços de documento {#document-services-steps}

Os serviços de documento AEM são um conjunto de serviços para criar, montar e proteger os documentos PDF. O AEM Forms fornece uma etapa do fluxo de trabalho AEM separada para cada serviço de documento.

Semelhante a outras etapas do fluxo de trabalho do AEM Forms, como Atribuir tarefa, Enviar email e Assinar documento, você pode usar variáveis em todas as etapas dos serviços de Documento AEM. Para obter mais informações sobre criação e gerenciamento de variáveis, consulte [Variáveis em fluxos de trabalho de AEM](../../forms/using/variable-in-aem-workflows.md).

### Etapa Aplicar Carimbo de Data e Hora do Documento {#apply-document-time-stamp-step}

Adicionar carimbo de data/hora a um documento. Você fornece detalhes do documento, como caminho do documento de entrada, nome do documento de entrada, local para armazenar dados exportados. Você pode optar por substituir um arquivo de carga útil existente, escolher um nome de arquivo diferente para armazenar dados em um arquivo diferente na pasta de carga útil, fornecer um caminho absoluto para os dados ou armazenar dados em uma variável do tipo de dados Documento.

### Etapa Converter para imagem {#convert-to-image-step}

Converte um documento PDF em lista de imagens. Os formatos de imagem compatíveis são JPEG, JPEG2000, PNG e TIFF. As seguintes informações se aplicam às conversões para imagens de TIFF:

* Um arquivo TIFF de várias páginas é gerado.
* Algumas anotações não estão incluídas nas imagens de TIFF. As anotações que exigem que o Acrobat gere sua aparência não são incluídas.

### Converter em etapa PDF/A {#convert-to-pdf-a-step}

Converte um documento PDF para o formato PDF/A usando as opções fornecidas. A versão PDF/A do Portable Document Format (PDF) é especializada em arquivamento e preservação de documentos a longo prazo.

### Converter para etapa PS {#convert-to-ps-step}

Converta documentos PDF em PostScript. Ao converter em PostScript, você pode usar a operação de conversão para especificar o documento de origem e se deseja converter em PostScript nível 2 ou 3. O documento PDF que você converter em um arquivo PostScript deve ser não interativo.

### Criar PDF a partir da etapa de tipo especificada {#create-pdf-from-specified-type-step}

Gere um documento PDF a partir de um arquivo de entrada. O documento de entrada pode ser relativo à carga útil, ter um caminho absoluto, pode ser a própria carga útil ou armazenado em uma variável do tipo de dados Documento.

### Criar PDF a partir da etapa URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Gera um documento PDF a partir do URL, HTML e arquivo ZIP fornecidos.

### Etapa Exportar dados {#export-data-step}

Exporta dados de um arquivo PDF forms ou XDP. É necessário inserir o caminho de arquivo do documento de entrada e o formato dos dados de exportação. As opções para Exportar formato de dados são Auto, XDP e XmlData.

### Export PDF para a etapa de tipo especificada {#export-pdf-to-specified-type-step}

Converte um documento PDF em um formato selecionado.

### Gerar etapa PDF não interativa {#generatenoninteractive}

Gere um PDF não interativo. Ele fornece várias opções de personalização.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa Importar dados {#import-data-step}

Mescla dados de formulário em um formulário PDF. Você pode importar dados de formulário em um formulário PDF.

### Chamar etapa DDX {#invokeddx}

Executa o arquivo DDX no mapa especificado de documentos de entrada e retorna os documentos PDF manipulados.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo DDX para documentos de entrada. Armazene o arquivo DDX em uma variável do tipo de dados Document ou XML.

### etapa do Optimize PDF {#optimize-pdf-step}

Otimiza os arquivos PDF reduzindo seu tamanho. O resultado dessa conversão são arquivos PDF que podem ser menores que suas versões originais. Essa operação também converte documentos de PDF para a versão de PDF especificada nos parâmetros de otimização.

As configurações de otimização especificam como os arquivos são otimizados. Estes são exemplos de configurações:

* Versão do PDF de destino
* Descartar objetos como ações JavaScript e miniaturas de página incorporadas
* Descartar dados do usuário, como comentários e anexos de arquivo
* Descartando configurações inválidas ou não usadas
* Compactação de dados descompactados ou uso de algoritmos de compactação mais eficientes
* Remoção de fontes incorporadas
* Configuração de valores de transparência

### Renderizar etapa do Formulário PDF {#renderpdf}

Renderiza um formulário criado no Designer de formulários (XDP) para um formulário PDF.

>[!NOTE]
>
>Você pode usar variáveis para especificar o arquivo de modelo para documentos de entrada. Armazene o caminho do arquivo de modelo em uma variável do tipo de dados String.

### Etapa de documento seguro {#secure-document-step}

Criptografar, Assinar e certificar um documento. O AEM Forms oferece suporte à criptografia baseada em senha e em certificado. Você também pode escolher entre vários algoritmos para assinar documentos. Por exemplo, SHA-256 e SH-512. Você também pode usar a etapa do fluxo de trabalho para ler e estender documentos PDF. A etapa do fluxo de trabalho fornece a opção para habilitar a decodificação de código de barras, assinaturas digitais, importação e exportação de dados de PDF e outras opções.

### Etapa Enviar para a impressora {#send-to-printer-step}

Envie um documento diretamente para uma impressora. Ela é compatível com os seguintes mecanismos de acesso de impressão:

* **Impressora acessível diretamente**: uma impressora instalada no mesmo computador é chamada de impressora acessível diretamente, e o computador é denominado host da impressora. Esse tipo de impressora pode ser uma impressora local conectada diretamente ao computador.
* **Impressora acessível indiretamente**: a impressora instalada em um servidor de impressão é acessada de outros computadores. Tecnologias como o sistema de impressão comum UNIX® (CUPS) e o protocolo LPD (Line Printer Daemon) estão disponíveis para conexão com uma impressora de rede. Para acessar uma impressora acessível indiretamente, especifique o IP ou o nome de host do servidor de impressão. Usando este mecanismo, você pode enviar um documento para um URI de LPD quando a rede tiver um LPD em execução. O mecanismo permite rotear o documento para qualquer impressora que esteja conectada à rede que tenha um LPD em execução.

### Etapa Gerar Saída Impressa {#generatePrintedOutput}

A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL, considerando um design de formulário e um arquivo de dados. O arquivo de dados é mesclado com o design do formulário e formatado para impressão. A saída gerada por essa etapa pode ser enviada diretamente para uma impressora ou salva como arquivo. É recomendável usar essa etapa quando quiser usar designs de formulário ou dados de um aplicativo. Se os designs de formulário ou os designs de formulário estiverem localizados na rede, no sistema de arquivos local ou no local HTTP, use a operação generatePrintedOutput.

Por exemplo, seu aplicativo exige a mesclagem de um design de formulário com um arquivo de dados. Os dados contêm centenas de registros. Além disso, requer que a saída seja enviada para uma impressora que suporte ZPL. O design do formulário e os dados de entrada estão em um aplicativo. Use a operação generatePrintedOutput para mesclar cada registro com um design de formulário e enviar a saída para uma impressora compatível com ZPL.

A etapa Gerar Saída Impressa tem as seguintes propriedades:

**Propriedades de entrada**

* **[!UICONTROL Selecione o arquivo de modelo usando]**: especifique o caminho do arquivo de modelo. Você pode selecionar o arquivo de modelo usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo. Além disso, você também pode aceitar a carga como o arquivo de dados de entrada.

* **[!UICONTROL Selecione o documento de dados usando]**: especifique o caminho de um arquivo de dados de entrada. Você pode selecionar o arquivo de dados de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

* **[!UICONTROL Formato da impressora]**: um valor de Formato de impressão que especifica a linguagem de descrição de página a ser usada, quando um arquivo XDC não for fornecido, para gerar o fluxo de saída. Se você fornecer um valor literal, selecione um destes valores:

   * **[!UICONTROL PCL personalizado]**: use a opção para especificar um arquivo XDC personalizado para PCL.
   * **[!UICONTROL PostScript personalizado]**: use a opção para especificar um arquivo XDC personalizado para PostScript.
   * **[!UICONTROL ZPL personalizado]**: use a opção para especificar um arquivo XDC personalizado para ZPL.
   * **[!UICONTROL Generic Color PCL (5c)]**: Use um PCL de cor genérica (5c).
   * **[!UICONTROL PostScript genérico nível 3]**: Use o PostScript genérico Nível 3.
   * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. O zpl300.xdc é usado.
   * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. O arquivo zpl600.xdc é usado.
   * **[!UICONTROL IPL personalizado]**: use a opção para especificar um arquivo XDC personalizado para IPL.
   * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. O ipl300.xdc é usado.
   * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. O arquivo ipl400.xdc é usado.
   * **[!UICONTROL TPCL personalizado]**: use a opção para especificar um arquivo XDC personalizado para TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. O arquivo tpcl305.xdc é usado.
   * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. O arquivo tpcl600.xdc é usado.
   * **[!UICONTROL DPL personalizado]**: use a opção para especificar um DPL de arquivo XDC personalizado.
   * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. O arquivo dpl300.xdc é usado.
   * **[!UICONTROL DPL406DPI]**: Use DPL 400 DPI. A dpl406.xdc é usada.
   * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. A dpl600.xdc é usada.

**Propriedades de saída**

* **[!UICONTROL Salvar documento de saída usando]**: especifique o local em que o arquivo de saída será salvo. Você pode salvar o arquivo de saída em um local relativo à carga útil, em uma variável ou especificar um local absoluto para salvar o arquivo de saída. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

**Propriedades avançadas**

* **[!UICONTROL Selecione o local da raiz do conteúdo usando]**: raiz de conteúdo é um valor de cadeia de caracteres que especifica o URI, a referência absoluta ou o local no repositório para recuperar ativos relativos usados pelo design do formulário. Por exemplo, se o design do formulário referenciar uma imagem relativamente, como ../myImage.gif, myImage.gif deverá estar localizado em repository://. O valor padrão é repository://, que aponta para o nível raiz do repositório.

  Quando você seleciona um ativo do aplicativo, o caminho do URI da raiz do conteúdo deve ter a estrutura correta. Por exemplo, se um formulário for separado de um aplicativo chamado SampleApp e for colocado em SampleApp/1.0/forms/Test.xdp, o URI da Raiz de conteúdo deverá ser especificado como repository://administrator@password/Applications/SampleApp/1.0/forms/ ou repositório:/Applications/SampleApp/1.0/forms/ (quando a autoridade for nula). Quando o URI da raiz do conteúdo é especificado dessa maneira, os caminhos de todos os ativos referenciados no formulário serão resolvidos em relação a esse URI.

* **[!UICONTROL Selecione o arquivo XCI usando]**: os arquivos XCI são usados para descrever fontes e outras propriedades usadas para elementos de design de formulário. Você pode manter um arquivo XCI relativo à carga útil, em um caminho absoluto ou usando uma variável do tipo de dados Documento.

* **[!UICONTROL Localidade]**: especifica a linguagem usada para gerar o documento PDF. Se você fornecer um valor literal, selecione um idioma na lista ou selecione um destes valores:
   * **Para usar o padrão do servidor**: (padrão) Use a configuração de Local definida no servidor do AEM Forms. A configuração Local é definida usando o Console de administração. (Consulte [Ajuda do Designer](https://www.adobe.com/go/learn_aemforms_designer_65_pt).)

   * **Para usar o valor personalizado**: digite o código de localidade na caixa literal ou selecione uma variável de cadeia de caracteres que contenha o código de localidade. Para obter uma lista completa de códigos de localidade compatíveis, consulte https://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Cópias]**: um valor inteiro que especifica o número de cópias para gerar para a saída. O valor padrão é 1.

* **[!UICONTROL Impressão frente e verso]**: um valor de Paginação que especifica se a impressão em frente e verso ou em verso deve ser usada. As impressoras que suportam PostScript e PCL usam esse valor. Se você fornecer um valor literal, selecione um destes valores:
   * **[!UICONTROL Borda maior frente e verso]**: use a impressão frente e verso e imprima usando a paginação de borda maior.
   * **[!UICONTROL Borda menor frente e verso]**: use a impressão frente e verso e imprima usando a paginação de borda curta.
   * **[!UICONTROL Simples]**: use a impressão de lado único.