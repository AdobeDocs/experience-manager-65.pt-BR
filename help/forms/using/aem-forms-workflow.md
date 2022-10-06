---
title: Fluxo de trabalho centrado no Forms no OSGi
seo-title: Rapidly build adaptive forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Use o fluxo de trabalho do AEM Forms para automatizar e criar rapidamente revisões e aprovações, a fim de iniciar serviços de documento
seo-description: Use AEM Forms Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
source-git-commit: d9608d584e822accc0c198fcf1d1b706d065938e
workflow-type: tm+mt
source-wordcount: '3681'
ht-degree: 2%

---

# Fluxo de trabalho centrado no Forms no OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

As empresas coletam dados de centenas e milhares de formulários, vários sistemas back-end e fontes de dados online ou offline. Eles também têm um conjunto dinâmico de usuários para tomar decisões sobre os dados, o que envolve processos iterativos de revisão e aprovação.

Juntamente com fluxos de trabalho de revisão e aprovação para públicos internos e externos, grandes organizações e empresas têm tarefas repetitivas. Por exemplo, converter um documento PDF para outro formato. Quando realizadas manualmente, essas tarefas demoram muito tempo e recursos. As empresas também têm requisitos legais para assinar digitalmente um documento e arquivar dados de formulário para uso posterior em formatos predefinidos.

## Introdução ao fluxo de trabalho centrado no Forms no OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Você pode usar fluxos de trabalho AEM para criar rapidamente fluxos de trabalho baseados em formulários adaptáveis. Esses fluxos de trabalho podem ser usados para revisão e aprovações, fluxos de processos comerciais, para iniciar serviços de documento, integrar com o fluxo de trabalho de assinatura do Adobe Sign e operações semelhantes. Por exemplo, processamento de aplicativos de cartão de crédito, fluxo de trabalho de aprovação de licença de funcionário, salvando um formulário como um documento PDF. Além disso, esses fluxos de trabalho podem ser usados em uma organização ou por meio de um firewall de rede.

Com o fluxo de trabalho centrado na Forms no OSGi, você pode criar e implantar rapidamente fluxos de trabalho para várias tarefas na pilha OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos na pilha JEE. O desenvolvimento e o gerenciamento de workflows usam os recursos conhecidos AEM Fluxo de trabalho e AEM Caixa de entrada. Os fluxos de trabalho são a base para automatizar processos de negócios reais que abrangem vários sistemas de software, redes, departamentos e até mesmo organizações.

Após a configuração, esses workflows podem ser acionados manualmente para concluir um processo definido ou ser executados de forma programática quando os usuários enviam um formulário ou [gerenciamento de correspondência](/help/forms/using/cm-overview.md) carta. Com esses recursos aprimorados de Fluxo de trabalho AEM, a AEM Forms oferece dois recursos distintos, mas semelhantes. Como parte de sua estratégia de implantação, você precisa decidir qual delas funciona para você. Consulte um [comparação](capabilities-osgi-jee-workflows.md) dos AEM Workflows centrados na Forms no OSGi e no Process Management no JEE. Além disso, para obter a topologia de implantação, consulte [Topologias de arquitetura e implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

O fluxo de trabalho centrado no Forms no OSGi estende [Caixa de entrada AEM](/help/sites-authoring/inbox.md) e fornece componentes extras (etapas) para AEM editor de fluxo de trabalho para adicionar suporte a fluxos de trabalho centrados no AEM Forms. A Caixa de entrada de AEM estendida tem funcionalidades semelhantes a [AEM Forms Workspace](introduction-html-workspace.md). Juntamente com o gerenciamento de fluxos de trabalho centrados no ser humano (Aprovação, Revisão e assim por diante), você pode usar fluxos de trabalho AEM para automatizar [serviços de documento](/help/sites-developing/workflows-step-ref.md)Operações relacionadas a (por exemplo, Gerar PDF) e documentos de assinatura eletrônica (Adobe Sign).

Todas as etapas do fluxo de trabalho do AEM Forms suportam o uso de variáveis. As variáveis permitem que as etapas do fluxo de trabalho mantenham e transmitam metadados pelas etapas no tempo de execução. Você pode criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Você também pode criar coleções variáveis (matriz) para armazenar várias instâncias de dados relacionados do mesmo tipo. Normalmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo. Para obter mais informações sobre como usar variáveis nesses componentes de fluxo de trabalho centrados no Forms (etapas), consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](../../forms/using/aem-forms-workflow-step-reference.md). Para obter informações sobre como criar e gerenciar variáveis, consulte [Variáveis em workflows AEM](../../forms/using/variable-in-aem-workflows.md).

O diagrama a seguir descreve o procedimento completo para criar, executar e monitorar um fluxo de trabalho centrado na Forms no OSGi.

![fluxo de trabalho de introdução ao aem-forms](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de você iniciar {#before-you-start}

* Um fluxo de trabalho é uma representação de um processo de negócios do mundo real. Mantenha seu processo de negócios real e a lista dos participantes do processo de negócios prontos. Além disso, mantenha o material adicional (formulários adaptáveis, Documentos do PDF e muito mais) pronto antes de começar a criar um fluxo de trabalho.
* Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM e no relatório de ajuda sobre o progresso do fluxo de trabalho. Divida seu processo de negócios em estágios lógicos.
* Você pode configurar a etapa de atribuição de fluxos de trabalho AEM para enviar notificações por email aos usuários ou destinatários. Então, [ativar notificações por email](#configure-email-service).
* Um fluxo de trabalho também pode usar o sinal de Adobe para assinaturas digitais. Se você planeja usar o Adobe Sign em um workflow, a variável [configurar o Adobe Sign para AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) antes de usá-lo em um workflow.

## Criar um modelo de fluxo de trabalho {#create-a-workflow-model}

Um modelo de fluxo de trabalho consiste em lógica e fluxo de um processo de negócios. Ele é composto por uma série de etapas. Essas etapas são componentes AEM. É possível estender as etapas do fluxo de trabalho com parâmetros e scripts para fornecer mais funcionalidade e controle, conforme necessário. O AEM Forms fornece algumas etapas além AEM etapas disponíveis para uso imediato. Para obter uma lista detalhada das etapas do AEM e do AEM Forms, consulte [Referência em etapas do fluxo de trabalho AEM](/help/sites-developing/workflows-step-ref.md) e [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](../../forms/using/aem-forms-workflow.md).

O AEM oferece uma interface de usuário intuitiva para criar um modelo de fluxo de trabalho usando as etapas de fluxo de trabalho fornecidas. Para obter instruções passo a passo para criar um modelo de fluxo de trabalho, consulte [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md). O exemplo a seguir fornece instruções passo a passo para criar um modelo de fluxo de trabalho para um fluxo de trabalho de aprovação e revisão:

>[!NOTE]
>
>Você deve ser um membro do grupo editor de fluxo de trabalho para criar ou editar um modelo de fluxo de trabalho.

### Criar um modelo para um fluxo de trabalho de aprovação e revisão {#create-a-model-for-an-approval-and-review-workflow}

O fluxo de trabalho de aprovação e revisão é para as tarefas que exigem intervenção humana para tomar decisões. O exemplo a seguir cria um modelo de fluxo de trabalho para um pedido de empréstimo hipotecário ser preenchido por um agente bancário de front office. Depois que o aplicativo é preenchido, ele é enviado para aprovação. Posteriormente, o pedido aprovado é enviado ao requerente para assinatura eletrônica através da Adobe Sign.

O exemplo está disponível como um pacote anexado abaixo. Importe e instale o exemplo usando o gerenciador de pacotes. Você também pode executar as seguintes etapas para criar manualmente o modelo de fluxo de trabalho para o aplicativo:

O exemplo cria um modelo de fluxo de trabalho para um aplicativo de hipoteca ser preenchido por um agente bancário de front-office. Uma vez preenchido, o aplicativo é enviado para aprovação. Posteriormente, o aplicativo aprovado será enviado ao cliente para assinatura eletrônica usando o Adobe Sign. Você pode importar e instalar o exemplo usando o gerenciador de pacotes.

[Obter arquivo](assets/example-mortgage-loan-application.zip)

1. Abra o console Modelos de fluxo de trabalho . O URL padrão é `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Selecionar **Criar**, em seguida **Criar modelo**. A caixa de diálogo Adicionar modelo de fluxo de trabalho é exibida.
1. Insira o **Título** e **Nome** (opcional). Por exemplo, um aplicativo de hipoteca. Toque **Concluído**.
1. Selecione o modelo de fluxo de trabalho recém-criado e toque em **Editar**. Agora, você pode adicionar etapas de fluxo de trabalho para criar lógica de negócios. Ao criar um modelo de fluxo de trabalho pela primeira vez, ele contém:

   * As etapas: Início e Fim do Fluxo. Essas etapas representam o início e o fim do workflow. Essas etapas são obrigatórias e não podem ser editadas ou removidas.
   * Um exemplo de Etapa do participante chamada Etapa 1. Essa etapa é configurada para atribuir um item de trabalho ao usuário administrador. Remova esta etapa.

1. Habilite notificações por email. Você pode configurar o fluxo de trabalho centrado no Forms no OSGi para enviar notificações por email aos usuários ou destinatários. Execute as seguintes configurações para ativar notificações por email:

   1. Vá para AEM gerenciador de configuração em `https://[server]:[port]/system/console/configMgr`.
   1. Abra o **[!UICONTROL Day CQ Mail Service]** configuração. Especifique um valor para a variável **[!UICONTROL Nome do host do servidor SMTP]**, **[!UICONTROL porta do servidor SMTP,]** e **[!UICONTROL Endereço &quot;De&quot;]** campos. Clique em **[!UICONTROL Salvar]**.
   1. Abra o **[!UICONTROL Externalizador de links CQ do dia]** configuração. No **[!UICONTROL Domínios]** , especifique o nome do host/endereço IP real e o número da porta para instâncias locais, de autor e de publicação. Clique em **[!UICONTROL Salvar]**.

1. Crie estágios do fluxo de trabalho. Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM e no progresso do relatório do fluxo de trabalho.

   Para definir um estágio, toque no ![info-círculo](assets/info-circle.png) ícone para abrir as propriedades do modelo de fluxo de trabalho, abra o **Estágios** , adicione estágios para o modelo de fluxo de trabalho e toque em **Salvar e fechar**. Para o exemplo de aplicativo de hipoteca, crie estágios: solicitação de empréstimo, status de solicitação de empréstimo, para ser assinado e documento de empréstimo assinado.

1. Arraste e solte a **Atribuir tarefa** etapas do navegador para o modelo de fluxo de trabalho. Faça dele o primeiro passo do modelo.

   O componente Atribuir tarefa atribui a tarefa, criada por workflow, a um usuário ou grupo. Ao atribuir a tarefa, você pode usar o componente para especificar um formulário adaptável ou um PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar a entrada de usuários e o PDF não interativo ou um formulário adaptável somente leitura é usado para fluxos de trabalho de revisão somente.

   Você também pode usar a etapa para controlar o comportamento da tarefa. Por exemplo, criar um documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, o caminho dos dados enviados, o caminho dos dados a serem preenchidos previamente e as ações padrão. Para obter informações detalhadas sobre as opções da etapa de atribuição de tarefa, consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](../../forms/using/aem-forms-workflow.md) documento.

   ![editor de fluxo de trabalho](assets/workflow-editor.png)

   Para o exemplo do aplicativo de hipoteca, configure a etapa de atribuição de tarefa para usar um formulário adaptável somente leitura e exibir o Documento PDF após a conclusão da tarefa. Além disso, selecione para o grupo de usuários com permissão para aprovar a solicitação de empréstimo. No **Ações** , desative o **Enviar** opção. Crie um **actionTaken** variável do tipo de dados String e especifique a variável como **Variável de rota**. Por exemplo, actionTaken. Além disso, adicione as rotas Approve e Reject . As rotas são exibidas como ações separadas (botões) AEM Caixa de entrada. O workflow seleciona uma ramificação com base na ação (botão) que um usuário toca.

   É possível importar o pacote de exemplo, disponível para download no início da seção, para o conjunto completo de valores de todos os campos da etapa de tarefa de atribuição configurada, por exemplo, aplicativo de hipoteca.

1. Arraste e solte o componente OU Dividir do navegador da etapa para o modelo de fluxo de trabalho. A divisão OR cria uma divisão no fluxo de trabalho, após a qual apenas uma ramificação está ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas de fluxo de trabalho a cada ramificação, conforme necessário.

   Você pode definir uma expressão de roteamento para uma ramificação usando uma definição de regra, um script ECMA ou um script externo.

   Use o editor de expressão para criar expressões de roteamento para Ramificação 1 e Ramificação 2. Essas expressões de roteamento ajudam a escolher uma ramificação com base na ação do usuário AEM Caixa de entrada.

   **Expressão de roteamento para Ramificação 1**

   Quando um usuário toca **Aprovar** AEM Caixa de entrada, a Ramificação 1 é ativada.

   ![OU Exemplo de divisão](assets/orsplit_branch1_active_new.png)

   **Expressão de roteamento para Ramificação 2**

   Quando um usuário toca **Rejeitar** AEM Caixa de entrada, a Ramificação 2 é ativada.

   ![OU Exemplo de divisão](assets/orsplit_branch2_active_new.png)

   Para obter informações sobre como criar expressões de roteamento usando variáveis, consulte [Variáveis em workflows do AEM Forms](../../forms/using/variable-in-aem-workflows.md).

1. Adicione outras etapas do fluxo de trabalho para criar a lógica de negócios.

   Para o exemplo de hipoteca, adicione um documento de geração de registro, duas etapas de tarefa e uma etapa de assinatura de documento à Ramificação 1 do modelo, conforme exibido na imagem abaixo. Uma etapa de tarefa Atribuir é exibir e enviar **ser assinados documentos de empréstimo ao candidato** e outro componente de atribuição de tarefa é **para exibir documentos assinados**. Além disso, adicione um componente de tarefa à ramificação 2. Ela é ativada, quando um usuário toca em Rejeitar AEM Caixa de entrada.

   Para o conjunto completo de valores de todos os campos de etapas da tarefa de atribuição, etapa do documento de registro e etapa de assinatura de documento configuradas por exemplo aplicativo de hipoteca, importe o pacote de exemplo, disponível para download no início desta seção.

   O modelo de fluxo de trabalho está pronto. Você pode iniciar o workflow por meio de vários métodos. Para obter detalhes, consulte [Iniciar um fluxo de trabalho centrado na Forms no OSGi](#launch).

   ![workflow-editor-hipoteca](assets/workflow-editor-mortgage.png)

## Criar um aplicativo de fluxo de trabalho centrado no Forms {#create-a-forms-centric-workflow-application}

O aplicativo é o formulário adaptável associado ao fluxo de trabalho. Quando um aplicativo é enviado por meio da Caixa de entrada, ele inicia o fluxo de trabalho associado. Para disponibilizar um fluxo de trabalho do Forms como um aplicativo AEM Caixa de entrada e aplicativo do AEM Forms, faça o seguinte para criar um aplicativo de fluxo de trabalho:

>[!NOTE]
>
>Você deve ser um membro do grupo fd-administrators para poder criar e gerenciar aplicativos de fluxo de trabalho.

1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gerenciar aplicativo de fluxo de trabalho]** e torneiras **[!UICONTROL Criar]**.
1. Na janela Criar aplicativo de fluxo de trabalho , forneça entradas para os seguintes campos e toque em **Criar**. Um novo aplicativo é criado e é listado na tela Aplicativos de fluxo de trabalho .

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>O título é visível AEM Caixa de entrada e ajuda os usuários a escolher um aplicativo. Mantenha-o descritivo. Por exemplo, Salvar Conta Abrindo Aplicativo.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Especifique o nome do aplicativo. Todos os caracteres, exceto alfabetos, números, hifens e sublinhados, são substituídos por hifens. </td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>A descrição é visível AEM Caixa de entrada. Forneça informações detalhadas sobre o aplicativo nos campos de descrição. Por exemplo, Finalidade do aplicativo.<br /> </td>
  </tr>
  <tr>
   <td>Formulário adaptativo</td>
   <td><p>Especifique o caminho de um formulário adaptável. Quando um usuário inicia um aplicativo, o formulário adaptável especificado é exibido.</p> <p><strong>Observação</strong>: Os aplicativos de fluxo de trabalho não suportam formulários e documentos PDF que sejam maiores que uma página ou que exijam rolagem no Apple iPad. Quando um aplicativo é aberto no Apple iPad e o formulário adaptável ou o documento PDF é maior que uma página, os campos do formulário e o conteúdo da segunda página são perdidos.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acesso</td>
   <td><p>Selecione um grupo. O aplicativo é visível AEM Caixa de entrada somente para os membros do grupo selecionado. A opção access group disponibiliza todos os grupos do grupo workflow-users para seleção. </p> <br /> </td>
  </tr>
  <tr>
   <td>Preencher Serviço</td>
   <td>Selecione um <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">serviço de preenchimento prévio</a> para o formulário adaptável.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de fluxo de trabalho</td>
   <td>Selecione um <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">modelo de fluxo de trabalho</a> para o aplicativo. Um modelo de fluxo de trabalho consiste em lógica e fluxo do processo de negócios. </td>
  </tr>
  <tr>
   <td>Caminho do arquivo de dados</td>
   <td>Especifique o caminho do arquivo de dados no repositório crx. O caminho é relativo à carga adaptável do formulário e contém o nome do arquivo de dados. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do anexo</td>
   <td>Especifique o caminho da pasta de anexos no repositório crx. O caminho do anexo é relativo ao local da carga útil. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do documento de registro</td>
   <td>Especifique o caminho do arquivo Documento de registro no repositório crx. O caminho é relativo ao local de carga do formulário adaptável. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar um fluxo de trabalho centrado na Forms no OSGi {#launch}

Você pode iniciar ou acionar um fluxo de trabalho centrado no Forms ao:

* [Envio de um aplicativo AEM Caixa de entrada](#inbox)
* [Envio de um aplicativo do aplicativo AEM Forms](#afa)

* [Envio de um formulário adaptável](#af)
* [Usar pasta assistida](#watched)

* [Envio de uma comunicação interativa ou uma carta](#letter)

### Envio de um aplicativo AEM Caixa de entrada {#inbox}

O aplicativo de fluxo de trabalho criado está disponível como um aplicativo na Caixa de entrada. Os usuários que são membros do grupo de usuários do fluxo de trabalho podem preencher e enviar o aplicativo que aciona o fluxo de trabalho associado. Para obter informações sobre como usar AEM Caixa de entrada para enviar aplicativos e gerenciar tarefas, consulte [Gerenciar aplicativos e tarefas do Forms na Caixa de entrada AEM](../../forms/using/manage-applications-inbox.md).

### Envio de um aplicativo do aplicativo AEM Forms {#afa}

O aplicativo AEM Forms é sincronizado com um servidor AEM Forms e permite fazer alterações nos dados do formulário, tarefas, aplicativos de fluxo de trabalho e nas informações salvas (rascunhos/modelos) em sua conta. Para obter mais informações, consulte [Aplicativo AEM Forms](/help/forms/using/aem-forms-app.md) e artigos relacionados.

### Envio de um formulário adaptável {#af}

É possível configurar as ações de envio de um formulário adaptável para iniciar um fluxo de trabalho no envio do formulário adaptável. Os formulários adaptáveis fornecem o **Chamar um fluxo de trabalho AEM** enviar ação para iniciar um fluxo de trabalho ao enviar um formulário adaptável. Para obter informações detalhadas sobre a ação de envio, consulte [Configuração da ação Enviar](../../forms/using/configuring-submit-actions.md). Para enviar um formulário adaptável por meio do aplicativo AEM Forms, ative Sincronizar com o aplicativo AEM Forms nas propriedades do formulário adaptável.

Você pode configurar um formulário adaptável para sincronizar, enviar e acionar um fluxo de trabalho do aplicativo AEM Forms. Para obter detalhes, consulte [como trabalhar com um formulário](/help/forms/using/working-with-form.md).

### Uso de uma pasta assistida {#watched}

Um administrador (um membro do grupo fd-administrators ) pode configurar uma pasta de rede para executar um fluxo de trabalho pré-configurado quando um usuário coloca um arquivo (como um arquivo PDF) na pasta. Depois que o workflow for concluído, ele poderá salvar o arquivo de resultado em uma pasta de saída especificada. Essa pasta é conhecida como [Pasta assistida](../../forms/using/watched-folder-in-aem-forms.md). Execute o seguinte procedimento para configurar uma pasta assistida para iniciar um workflow:

1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configurar pasta assistida]**. Uma lista de pastas de controle já configuradas é exibida.
1. Toque **[!UICONTROL Novo]**. Uma lista de campos é exibida. Especifique um valor para os seguintes campos para configurar uma Pasta assistida para um fluxo de trabalho:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Nome</code></td>
   <td>Especifique o nome da Pasta assistida. Este campo suporta apenas alfanumérico.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Caminho </code></td>
   <td>Especifique a localização física da Pasta assistida. Em um ambiente em cluster, use uma pasta de rede compartilhada que possa ser acessada AEM nó do cluster.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Processar arquivos usando</code></td>
   <td>Selecione o <span class="uicontrol">Fluxo de trabalho </code>opção. </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modelo de fluxo de trabalho</code></td>
   <td>Selecione um modelo de fluxo de trabalho.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Padrão do arquivo de saída</code></td>
   <td>Especifique a estrutura de diretório para arquivos de saída e diretórios. Também é possível especificar uma <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">padrão para arquivos de saída e diretórios</a>.</td>
  </tr>
 </tbody>
</table>

1. Toque **Avançado**. Especifique um valor para o seguinte campo e toque em **Criar**. A Pasta assistida é configurada para iniciar um fluxo de trabalho. Agora, sempre que um arquivo é colocado no diretório de entrada da Pasta assistida, o fluxo de trabalho especificado é acionado.

   | Texto | Descrição |
   |---|---|
   | Filtro do mapeador de carga útil | Ao criar uma pasta assistida, ela cria uma estrutura de pastas no repositório crx. A estrutura de pastas pode servir como uma carga para o fluxo de trabalho. Você pode gravar um script para mapear um Fluxo de trabalho de AEM para aceitar entradas da estrutura de pastas assistida. Uma implementação pronta para uso está disponível e listada no Filtro do Mapeador de Carga. Se não tiver uma implementação personalizada, selecione a implementação padrão. |

   A guia Advanced contém mais campos. A maioria desses campos contém um valor padrão. Para saber mais sobre todos os campos, consulte a [Criar ou configurar uma pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) artigo 10. o

### Envio de uma comunicação interativa ou uma carta {#letter}

Você pode associar e executar um fluxo de trabalho centrado na Forms no OSGi ao enviar uma comunicação interativa ou uma carta. Os workflows de gerenciamento de correspondência são usados para comunicações e cartas interativas de pós-processamento. Por exemplo, envio de emails, impressão, envio de fax ou arquivamento de cartas finais. Para obter etapas detalhadas, consulte [Pós-processamento de comunicações e cartas interativas](../../forms/using/submit-letter-topostprocess.md).

## Configurações adicionais {#additional-configurations}

### Configurar o serviço de email {#configure-email-service}

Você pode usar as etapas Atribuir tarefa e Enviar email dos fluxos de trabalho AEM para enviar um email. Execute as etapas a seguir para especificar servidores de email e outras configurações necessárias para enviar emails:

1. Vá para AEM gerenciador de configuração em `https://[server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Day CQ Mail Service]** configuração. Especifique um valor para a variável **[!UICONTROL Nome do host do servidor SMTP]**, **[!UICONTROL porta do servidor SMTP,]** e **[!UICONTROL Endereço &quot;De&quot;]** campos. Clique em **[!UICONTROL Salvar]**.
1. Abra o **[!UICONTROL Externalizador de links CQ do dia]** configuração. No **[!UICONTROL Domínios]** , especifique o nome do host/endereço IP real e o número da porta para instâncias locais, de autor e de publicação. Clique em **[!UICONTROL Salvar]**.

### Limpar instâncias do fluxo de trabalho {#purge-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do motor de workflow. Portanto, você pode remover regularmente do repositório as instâncias de fluxo de trabalho concluídas ou em execução. Para obter informações detalhadas, consulte [Limpeza regular de instâncias de fluxo de trabalho](/help/sites-administering/workflows-administering.md#regular) limpeza de instâncias de fluxo de trabalho.

## Parâmetros de dados confidenciais para variáveis de fluxo de trabalho e armazenamento em armazenamentos de dados externos {#externalize-wf-variables}

Todos os dados enviados de formulários adaptáveis para [!DNL Experience Manager] Os workflows podem ter PII (Informações de identificação pessoal) ou SPD (Dados pessoais confidenciais) dos usuários finais de sua empresa. No entanto, não é obrigatório que seus dados sejam armazenados em [!DNL Adobe Experience Manager] [Repositório JCR](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html). Você pode externalizar o armazenamento de dados do usuário final em seu armazenamento de dados gerenciado (por exemplo, armazenamento de blob do Azure), parametrizando as informações em [variáveis de fluxo de trabalho](/help/forms/using/variable-in-aem-workflows.md).

Em um [!DNL Adobe Experience Manager] No fluxo de trabalho do Forms, os dados são processados e passados por uma série de etapas do fluxo de trabalho por meio de variáveis de fluxo de trabalho. Essas variáveis são propriedades nomeadas ou pares de valores chave que são armazenados no nó de metadados de instâncias de fluxo de trabalho; por exemplo `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. Essas variáveis de workflow podem ser externalizadas em um repositório separado diferente do JCR e, em seguida, processadas por [!DNL Adobe Experience Manager] fluxos de trabalho. [!DNL Adobe Experience Manager] fornece API `[!UICONTROL UserMetaDataPersistenceProvider]` para armazenar as variáveis do workflow no armazenamento externo gerenciado. Para saber mais sobre como usar variáveis de fluxo de trabalho para armazenamentos de dados de propriedade do cliente em [!DNL Adobe Experience Manager], consulte [Administrar variáveis de fluxo de trabalho para armazenamentos de dados externos](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] fornece o seguinte [amostra](https://github.com/adobe/workflow-variable-externalizer) para armazenar variáveis do mapa de metadados de fluxo de trabalho para o armazenamento de blobs do Azure, usando a API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). Nas linhas semelhantes, você pode usar a amostra como guia para usar [UserMetaDataPersistenceProvider] API para exteriorizar as variáveis de workflow em qualquer outro armazenamento de dados externo ao [!DNL Adobe Experience Manager] e gerenciam o mesmo.

>[!NOTE]
>
>Ao armazenar suas variáveis de workflow em um armazenamento de dados externo, consulte os ponteiros no [diretrizes para armazenamento externo de dados de workflows](#guidelines-workflows-external-data-storage).

### Instalar a implementação de amostra da API de fluxo de trabalho

Para armazenar variáveis de fluxo de trabalho no armazenamento de blobs gerenciado do Azure:
1. Instale o [amostra](https://github.com/adobe/workflow-variable-externalizer) API de fluxo de trabalho [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) como se segue:

   1. Execute o no diretório raiz do projeto no `mvn clean install` com Maven 3.

   1. Para implantar o pacote e o pacote de conteúdo para criar, execute `mvn clean install -PautoInstallPackage`.

   1. Para implantar somente o pacote no autor, execute `mvn clean install -PautoInstallBundle`.

1. Inicialize as seguintes propriedades no arquivo de configuração OSGi do externalizador no `ui.config` pacote de conteúdo:

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

Estas são as finalidades (e exemplos) dessas propriedades:

* **accountKey** é a chave secreta para autorizar o acesso.

* **accountName** é a conta do azure onde os dados devem ser armazenados.

* **endpointSuffix**, por exemplo `core.windows.net`.

* **containerName** é o container na conta em que os dados precisam ser armazenados. A amostra assume que o contêiner está existente.

* **protocolo**, por exemplo `https` ou `http`.

1. Configure o modelo de fluxo de trabalho em [!DNL Adobe Experience Manager]. Para saber como configurar o modelo de fluxo de trabalho para um armazenamento externo, consulte [Configurar o modelo de fluxo de trabalho](#configure-aem-wf-model).

### Configurar modelo de fluxo de trabalho em [!DNL Adobe Experience Manager] para armazenamento externo de dados {#configure-aem-wf-model}

Para configurar um modelo de Fluxo de trabalho AEM para um armazenamento de dados externo:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. Selecione um nome de modelo e selecione **[!UICONTROL Editar]**.

1. Selecione o ícone Informações da página e selecione **[!UICONTROL Abrir propriedades]**.

1. Selecionar **[!UICONTROL Externalizar o armazenamento de dados do workflow]**.

1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar as propriedades.

### Diretrizes para fluxos de trabalho de AEM para armazenamento externo de dados {#guidelines-workflows-external-data-storage}

Estas são as diretrizes ao usar [!DNL Adobe Experience Manager] fluxos de trabalho e armazenamento de dados em armazenamentos de dados externos (por exemplo, servidor de armazenamento do Microsoft Azure):

* Use variáveis para armazenar dados enquanto define arquivos de dados de entrada e saída e anexos em etapas do modelo de fluxo de trabalho. Não selecionar **[!UICONTROL Em relação à carga]** e **[!UICONTROL Disponível em um caminho absoluto]** opções. O **[!UICONTROL Em relação à carga]** e **[!UICONTROL Disponível em um caminho absoluto]** as opções não são exibidas automaticamente após [configure um [!DNL Adobe Experience Manager] modelo de fluxo de trabalho para armazenamento externo de dados](#configure-aem-wf-model).

* Use variáveis para armazenar arquivos de dados e anexos enquanto envia um formulário adaptável para um Fluxo de trabalho AEM. Não selecionar **[!UICONTROL Em relação à carga]** ao enviar um formulário adaptável para um [!DNL Adobe Experience Manager] fluxo de trabalho. O **[!UICONTROL Em relação à carga]** não é exibida automaticamente uma vez que [configure um [!DNL Adobe Experience Manager] modelo de fluxo de trabalho para armazenamento externo de dados](#configure-aem-wf-model).

* Não use um [!DNL Adobe Experience Manager] etapa do fluxo de trabalho em um modelo de fluxo de trabalho para armazenar dados na [!UICONTROL CRX DE] repositório.

* Quando você [configure um [!DNL Adobe Experience Manager] modelo de fluxo de trabalho para armazenamento externo de dados](#configure-aem-wf-model), não crie colunas personalizadas para [!DNL Adobe Experience Manager] [!UICONTROL Caixa de entrada] já que os valores das colunas personalizadas não são buscados se o item de trabalho na [!DNL Adobe Experience Manager] [!UICONTROL Caixa de entrada] pertence a um workflow marcado para armazenamento externo.
