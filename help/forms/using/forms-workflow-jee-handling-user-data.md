---
title: Fluxos de trabalho do Forms JEE | Manipulação de dados do usuário
description: Workflows do AEM Forms JEE para projetar, criar e gerenciar processos de negócios.
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 0%

---

# Fluxos de trabalho do Forms JEE | Manipulação de dados do usuário {#forms-jee-workflows-handling-user-data}

Os fluxos de trabalho do AEM Forms JEE fornecem ferramentas para projetar, criar e gerenciar processos de negócios. Um processo de fluxo de trabalho consiste em uma série de etapas executadas em uma ordem especificada. Cada etapa executa uma ação específica, como atribuir uma tarefa a um usuário ou enviar uma mensagem de email. Um processo pode interagir com ativos, contas de usuário e serviços e pode ser acionado usando qualquer um dos seguintes métodos:

* Iniciar um processo no AEM Forms Workspace
* Uso do serviço SOAP ou RESTful
* Envio de um formulário adaptável
* Usar pasta monitorada
* Usar email

Para obter mais informações sobre como criar o processo de workflow do AEM Forms JEE, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65).

## Dados do usuário e armazenamentos de dados {#user-data-and-data-stores}

Quando um processo é acionado e conforme avança, ele captura dados sobre os participantes do processo, dados inseridos pelos participantes no formulário associado ao processo e anexos adicionados ao formulário. Os dados são armazenados no banco de dados do servidor do AEM Forms JEE e, se configurados, alguns dados como anexos são armazenados no diretório Armazenamento global de documentos (GDS). O diretório GDS pode ser configurado em um sistema de arquivos compartilhados ou em um banco de dados.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Quando um processo é acionado, uma ID de instância de processo exclusiva e uma ID de invocação de longa duração são geradas e associadas à instância de processo. Você pode acessar e excluir dados de uma instância de processo com base na ID de invocação de longa duração. Você pode deduzir a ID de invocação de longa duração de uma instância do processo com o nome de usuário do iniciador do processo ou dos participantes do processo que enviaram suas tarefas.

No entanto, não é possível identificar a ID da instância do processo para um iniciador nos seguintes cenários:

* **Processo acionado por meio de uma pasta monitorada**: uma instância de processo não poderá ser identificada usando seu iniciador se o processo for acionado por uma pasta monitorada. Nesse caso, as informações do usuário são codificadas nos dados armazenados.
* **Processo iniciado pela publicação da instância do AEM**: todas as instâncias de processo acionadas da instância de publicação AEM não capturam informações sobre o iniciador. No entanto, os dados do usuário podem ser capturados no formulário associado ao processo, que é armazenado em variáveis de fluxo de trabalho.
* **Processo iniciado por email**: a ID de email do remetente é capturada como uma propriedade em uma coluna de blob opaco do `tb_job_instance` tabela de banco de dados, que não pode ser consultada diretamente.

### Identificar IDs de instância de processo quando o iniciador ou participante do fluxo de trabalho for conhecido {#initiator-participant}

Execute as seguintes etapas para identificar IDs de instância de processo para um iniciador de fluxo de trabalho ou um participante:

1. Execute o seguinte comando no banco de dados do servidor do AEM Forms para recuperar a ID principal do iniciador ou participante do fluxo de trabalho `edcprincipalentity` tabela de banco de dados.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   A consulta retorna a ID da entidade de segurança para o `user_ID`.

1. (**Para iniciador de fluxo de trabalho**) Execute o seguinte comando para recuperar todas as tarefas associadas à ID da entidade de segurança para o iniciador do `tb_task` tabela de banco de dados.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   A consulta retorna tarefas iniciadas pelo especificado `initiator`_ `principal_id`. As tarefas são de dois tipos:

   * **Tarefas concluídas**: essas tarefas foram enviadas e exibem um valor alfanumérico na variável `process_instance_id` campo. Anote todas as IDs de instância de processo para tarefas enviadas e continue com as etapas.
   * **Tarefas iniciadas, mas não concluídas**: essas tarefas foram iniciadas, mas ainda não foram enviadas. O valor no campo `process_instance_id` o campo para essas tarefas é **0** (zero). Nesse caso, anote as IDs de tarefa correspondentes e consulte [Trabalhar com tarefas órfãs](#orphan).

1. (**Para participantes do fluxo de trabalho**) Execute o seguinte comando para recuperar IDs de instância de processo associadas à ID principal do participante do processo para o iniciador do `tb_assignment` tabela de banco de dados.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   A consulta retorna IDs de instância para todos os processos associados ao participante, incluindo aqueles em que ele não enviou nenhuma tarefa.

   Anote todas as IDs de instância de processo para tarefas enviadas e continue com as etapas.

   Para tarefas órfãs ou tarefas em que a `process_instance_id` é 0 (zero), anote as IDs de tarefa correspondentes e consulte [Trabalhar com tarefas órfãs](#orphan).

1. Siga as instruções em [Limpar dados do usuário das instâncias de fluxo de trabalho com base nas IDs de instância de processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) seção para excluir dados do usuário para IDs de instância de processo identificadas.

### Identificar IDs de instância de processo quando os dados do usuário são armazenados em variáveis primitivas {#primitive}

Um fluxo de trabalho pode ser projetado de modo que os dados do usuário sejam capturados em uma variável armazenada como um blob no banco de dados. Nesses casos, você pode consultar dados do usuário somente se eles estiverem armazenados em uma das seguintes variáveis de tipo primitivo:

* **String**: contém o ID do usuário diretamente ou como uma substring e pode ser consultada usando SQL.
* **Numérico**: contém a ID do usuário diretamente.
* **XML**: contém a ID do usuário como uma subcadeia de caracteres no texto armazenado como colunas de texto no banco de dados e pode ser consultado como cadeias de caracteres.

Execute as seguintes etapas para determinar se um workflow que armazena dados em variáveis do tipo primitivo contém dados para o usuário:

1. Execute o seguinte comando de banco de dados:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   A consulta retorna um nome de tabela em `tb_<number>` formato para o aplicativo especificado ( `app_name`) e fluxo de trabalho ( `workflow_name`).

   >[!NOTE]
   >
   >O valor de `name` A propriedade pode ser complexa se o workflow estiver aninhado em subpastas dentro do aplicativo. Certifique-se de especificar o caminho completo exato para o fluxo de trabalho, que pode ser obtido na variável `omd_object_type` tabela de banco de dados.

1. Revise o `tb_<number>` esquema de tabela. A tabela contém variáveis que armazenam dados do usuário para o workflow especificado. As variáveis na tabela correspondem às variáveis no workflow.

   Identifique e anote a variável que corresponde à variável de fluxo de trabalho que contém a ID do usuário. Se a variável identificada for do tipo primitivo, você poderá executar um query para determinar as instâncias de fluxo de trabalho associadas a uma ID de usuário.

1. Execute o seguinte comando de banco de dados. Nesse comando, a variável `user_var` é a variável do tipo primitivo que contém a ID do usuário.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   A consulta retorna todas as IDs de instância de processo associadas à instância especificada `user_ID`.

1. Siga as instruções em [Limpar dados do usuário das instâncias de fluxo de trabalho com base nas IDs de instância de processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) seção para excluir dados do usuário para IDs de instância de processo identificadas.

### Limpar dados do usuário das instâncias de fluxo de trabalho com base nas IDs de instância de processo {#purge}

Agora que você identificou as IDs de instância de processo associadas a um usuário, faça o seguinte para excluir os dados do usuário das respectivas instâncias de processo.

1. Execute o seguinte comando para recuperar a ID de invocação de longa vida e o status de uma instância de processo do `tb_process_instance` tabela.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   A consulta retorna a ID de invocação de vida longa e o status para a `process_instance_id`.

1. Criar uma instância do público `ProcessManager` cliente ( `com.adobe.idp.workflow.client.ProcessManager`) usando um `ServiceClientFactory` com as configurações de conexão corretas.

   Para obter mais informações, consulte Referência da API Java para [Gerenciador de Processos de Classe](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Verifique o status da instância do workflow. Se o status for diferente de 2 (CONCLUÍDO) ou 4 (ENCERRADO), encerre a instância primeiro chamando o seguinte método:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Limpe a instância do workflow chamando o seguinte método:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   A variável `purgeProcessInstance` O método exclui completamente todos os dados da ID de invocação especificada do banco de dados do servidor do AEM Forms e do GDS, se configurado.

### Trabalhar com tarefas órfãs {#orphan}

Tarefas órfãs são as tarefas cujo processo de contenção foi iniciado, mas ainda não foi enviado. neste caso, a `process_instance_id` é **0** (zero). Portanto, não é possível rastrear dados do usuário armazenados para tarefas órfãs usando IDs de instância de processo. No entanto, é possível rastreá-la usando a ID da tarefa para uma tarefa órfã. É possível identificar as IDs das tarefas na `tb_task` para um usuário, conforme descrito em [Identificar IDs de instância de processo quando o iniciador ou participante do fluxo de trabalho for conhecido](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Depois de ter as IDs de tarefa, faça o seguinte para limpar os arquivos e dados associados a uma tarefa órfã do GDS e do banco de dados.

1. Execute o seguinte comando no banco de dados do servidor do AEM Forms para recuperar IDs para as IDs da tarefa identificadas.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   A consulta retorna uma lista de IDs. Para cada ID ( `fd_id`) retornados nos resultados, crie uma lista de strings de ID de sessão da seguinte maneira:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Dependendo de o seu GDS apontar para um sistema de arquivos ou para um banco de dados, execute uma das seguintes etapas:

   1. **GDS no sistema de arquivos**

      No sistema de arquivos GDS:

      1. Procure arquivos com as seguintes cadeias de caracteres de ID de sessão como suas extensões:

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Os arquivos com essas extensões são os arquivos marcadores. Eles são armazenados com nomes de arquivo no seguinte formato:

      `<file_name_guid>.session<session_id_string>`

      1. Exclua todos os arquivos marcadores e outros arquivos com o nome exato de arquivo como `<file_name_guid>` do sistema de arquivos.

   1. **GDS no banco de dados**

      Execute os seguintes comandos para cada ID de sessão:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. Execute os seguintes comandos para excluir dados de IDs de tarefas do banco de dados do servidor do AEM Forms:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
