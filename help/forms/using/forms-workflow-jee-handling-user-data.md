---
title: Workflows Forms JEE | Tratamento de dados de utilizadores
seo-title: Workflows Forms JEE | Tratamento de dados de utilizadores
description: Workflows Forms JEE | Tratamento de dados de utilizadores
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---


# Workflows Forms JEE | Tratamento de dados de utilizadores {#forms-jee-workflows-handling-user-data}

Os workflows AEM Forms JEE fornecem ferramentas para projetar, criar e gerenciar processos comerciais. Um processo de fluxo de trabalho consiste em uma série de etapas que são executadas em uma ordem especificada. Cada etapa executa uma ação específica, como atribuir uma tarefa a um usuário ou enviar uma mensagem de email. Um processo pode interagir com ativos, contas de usuário e serviços, e pode ser acionado usando qualquer um dos seguintes métodos:

* Iniciar um processo a partir do AEM Forms Workspace
* Uso do serviço SOAP ou RESTful
* Enviar um formulário adaptável
* Uso da pasta assistida
* Usando email

Para obter mais informações sobre como criar o processo de fluxo de trabalho do AEM Forms JEE, consulte a Ajuda [do](http://www.adobe.com/go/learn_aemforms_workbench_65)Workbench.

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

Quando um processo é acionado e à medida que ele avança, ele captura dados sobre os participantes do processo, dados inseridos pelos participantes no formulário associado ao processo e anexos adicionados ao formulário. Os dados são armazenados no banco de dados do servidor AEM Forms JEE e, se configurados, alguns dados como anexos são armazenados no diretório GDS (Global Documento Armazenamento). O diretório GDS pode ser configurado em um sistema de arquivos compartilhado ou em um banco de dados.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Quando um processo é acionado, uma ID de instância de processo exclusiva e uma ID de invocação de longa duração são geradas e associadas à instância de processo. Você pode acessar e excluir dados de uma instância de processo com base na ID de invocação de longa duração. Você pode deduzir a ID de invocação de longa duração de uma instância do processo com o nome de usuário do iniciador do processo ou dos participantes do processo que enviaram suas tarefas.

No entanto, não é possível identificar a ID da instância do processo para um iniciador nos seguintes cenários:

* **Processo acionado por meio de uma pasta** assistida: Uma instância do processo não pode ser identificada usando seu iniciador se o processo for acionado por uma pasta monitorada. Nesse caso, as informações do usuário são codificadas nos dados armazenados.
* **Processo iniciado da instância** de publicação AEM: Todas as instâncias de processo acionadas AEM instância de publicação não capturam informações sobre o iniciador. No entanto, os dados do usuário podem ser capturados no formulário associado ao processo, que é armazenado nas variáveis do fluxo de trabalho.
* **Processo iniciado por email**: A ID de e-mail do remetente é capturada como uma propriedade em uma coluna de blob opaca da tabela do `tb_job_instance` banco de dados, que não pode ser consultada diretamente.

### Identificar as IDs de instância do processo quando o iniciador ou participante do fluxo de trabalho for conhecido {#initiator-participant}

Execute as seguintes etapas para identificar as IDs de instância de processo para um iniciador de fluxo de trabalho ou um participante:

1. Execute o seguinte comando no banco de dados do servidor AEM Forms para recuperar a ID principal do iniciador ou participante do fluxo de trabalho da tabela do `edcprincipalentity` banco de dados.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   O query retorna a ID principal do especificado `user_ID`.

1. (**Para iniciador** de fluxo de trabalho) Execute o seguinte comando para recuperar todas as tarefas associadas à ID principal do iniciador da tabela do `tb_task` banco de dados.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   O query retorna tarefas iniciadas pelo especificado `initiator`_ `principal_id`. As tarefas são de dois tipos:

   * **Tarefas** concluídas: Essas tarefas foram enviadas e exibem um valor alfanumérico no `process_instance_id` campo. Anote todas as IDs de instância de processo para tarefas enviadas e continue com as etapas.
   * **Tarefas iniciadas mas não concluídas**: Essas tarefas foram iniciadas, mas ainda não foram enviadas. O valor no `process_instance_id` campo dessas tarefas é **0** (zero). Nesse caso, anote as IDs de tarefa correspondentes e consulte [Trabalhar com tarefas](#orphan)órfãs.

1. (**Para participantes** do fluxo de trabalho) Execute o seguinte comando para recuperar as IDs de instância do processo associadas à ID principal do participante do processo do iniciador na tabela do `tb_assignment` banco de dados.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   O query retorna as IDs de instância de todos os processos associados ao participante, incluindo aqueles em que o participante não tenha submetido nenhuma tarefa.

   Anote todas as IDs de instância de processo para tarefas enviadas e continue com as etapas.

   Para tarefas órfãs ou tarefas em que o `process_instance_id` é 0 (zero), anote as IDs de tarefa correspondentes e consulte [Trabalhar com tarefas](#orphan)órfãs.

1. Siga as instruções em [Expurgar dados de usuário das instâncias de fluxo de trabalho com base na seção IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) de instância do processo para excluir dados de usuário para IDs de instância do processo identificadas.

### Identificar IDs de instância do processo quando os dados do usuário são armazenados em variáveis primitivas {#primitive}

Um fluxo de trabalho pode ser projetado de modo que os dados do usuário sejam capturados em uma variável que seja armazenada como um blob no banco de dados. Nesses casos, você pode query dados do usuário somente se eles estiverem armazenados em uma das seguintes variáveis primitivas:

* **Sequência**: Contém a ID do usuário diretamente ou como uma substring e pode ser consultada usando o SQL.
* **Numérico**: Contém a ID do usuário diretamente.
* **XML**: Contém a ID do usuário como uma substring dentro do texto armazenado como colunas de texto no banco de dados e pode ser consultado como strings.

Execute as seguintes etapas para determinar se um fluxo de trabalho que armazena dados em variáveis de tipo primitivo contém dados para o usuário:

1. Execute o seguinte comando de banco de dados:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   O query retorna um nome de tabela no `tb_<number>` formato para o aplicativo especificado ( `app_name`) e o fluxo de trabalho ( `workflow_name`).

   >[!NOTE]
   >
   >O valor da `name` propriedade pode ser complexo se o fluxo de trabalho estiver aninhado dentro de subpastas dentro do aplicativo. Certifique-se de especificar o caminho completo exato para o fluxo de trabalho, que você pode obter da tabela do `omd_object_type` banco de dados.

1. Revise o schema da `tb_<number>` tabela. A tabela contém variáveis que armazenam dados do usuário para o fluxo de trabalho especificado. As variáveis na tabela correspondem às variáveis no fluxo de trabalho.

   Identifique e anote a variável que corresponde à variável de fluxo de trabalho que contém a ID do usuário. Se a variável identificada for do tipo primitivo, você poderá executar um query para determinar as instâncias do fluxo de trabalho associadas a uma ID de usuário.

1. Execute o seguinte comando de banco de dados. Nesse comando, a variável `user_var` é do tipo primitivo que contém a ID do usuário.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   O query retorna todas as IDs de instância do processo associadas ao especificado `user_ID`.

1. Siga as instruções em [Expurgar dados de usuário das instâncias de fluxo de trabalho com base na seção IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) de instância do processo para excluir dados de usuário para IDs de instância do processo identificadas.

### Expurgar dados de usuário de instâncias de fluxo de trabalho com base nas IDs de instância do processo {#purge}

Agora que você identificou as IDs de instância de processo associadas a um usuário, faça o seguinte para excluir os dados do usuário das respectivas instâncias de processo.

1. Execute o seguinte comando para recuperar a ID de invocação de longa duração e o status de uma instância de processo da `tb_process_instance` tabela.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   O query retorna a ID de invocação de longa duração e o status do especificado `process_instance_id`.

1. Crie uma instância do `ProcessManager` cliente público ( `com.adobe.idp.workflow.client.ProcessManager`) usando uma `ServiceClientFactory` instância com as configurações de conexão corretas.

   Para obter mais informações, consulte Referência da API Java para [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Verifique o status da instância do fluxo de trabalho. Se o status for diferente de 2 (COMPLETE) ou 4 (TERMINATED), termine a instância primeiro chamando o seguinte método:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Expurgue a instância do fluxo de trabalho chamando o seguinte método:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   O `purgeProcessInstance` método exclui completamente todos os dados para a ID de invocação especificada do banco de dados do servidor AEM Forms e do GDS, se configurado.

### Trabalhar com tarefas órfãs {#orphan}

As tarefas órfãs são as tarefas cujo processo de contenção foi iniciado mas ainda não foi submetido. nesse caso, o `process_instance_id` é **0** (zero). Portanto, não é possível rastrear dados de usuário armazenados para tarefas órfãs usando IDs de instância de processo. No entanto, você pode rastreá-lo usando a ID de tarefa para uma tarefa órfã. Você pode identificar as tarefa IDs da tabela de um usuário como descrito em `tb_task` Identificar IDs de instância do processo quando o iniciador ou participante do fluxo de trabalho for conhecido [](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Depois de ter as IDs de tarefa, faça o seguinte para expurgar os arquivos e dados associados com uma tarefa órfã do GDS e do banco de dados.

1. Execute o seguinte comando no banco de dados do servidor AEM Forms para recuperar IDs para as IDs de tarefa identificadas.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   O query retorna uma lista de IDs. Para cada ID ( `fd_id`) retornada nos resultados, crie uma lista de sequências de caracteres de ID de sessão da seguinte maneira:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Dependendo de seu GDS apontar para um sistema de arquivos ou um banco de dados, execute uma das seguintes etapas:

   1. **GDS no sistema de arquivos**

      No sistema de arquivos GDS:

      1. Procure arquivos com as seguintes sequências de ID de sessão como suas extensões:
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Os arquivos com essas extensões são os arquivos de marcador. Eles são armazenados com nomes de arquivo no seguinte formato:

      `<file_name_guid>.session<session_id_string>`

      1. Exclua todos os arquivos de marcador e outros arquivos com o nome de arquivo exato do sistema `<file_name_guid>` de arquivos.
   1. **GDS no banco de dados**

      Execute os seguintes comandos para cada ID de sessão:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Execute os seguintes comandos para excluir dados de IDs de tarefa do banco de dados do servidor AEM Forms:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

