---
title: workflows centrados em formulários no OSGi| Tratamento de dados de utilizadores
seo-title: workflows centrados em formulários no OSGi| Tratamento de dados de utilizadores
description: 'null'
seo-description: 'null'
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# workflows centrados em formulários no OSGi| Tratamento de dados de utilizadores {#forms-centric-workflows-on-osgi-handling-user-data}

workflows AEM centrados em formulários permitem automatizar processos de negócios centrados em formulários no mundo real. Os Workflows consistem em uma série de etapas que são executadas em uma ordem especificada no modelo de fluxo de trabalho associado. Cada etapa executa uma ação específica, como atribuir uma tarefa a um usuário ou enviar uma mensagem de email. Os Workflows podem interagir com ativos no repositório, contas de usuário e serviços. Portanto, os workflows podem coordenar atividades complicadas que envolvem qualquer aspecto do Experience Manager.

Um fluxo de trabalho centrado em formulários pode ser acionado ou iniciado por meio de qualquer um dos seguintes métodos:

* Enviar um aplicativo da Caixa de entrada do AEM
* Enviar um aplicativo do aplicativo AEM Forms
* Enviar um formulário adaptável
* Uso de uma pasta assistida
* Enviar uma comunicação interativa ou uma carta

Para obter mais informações sobre workflows e recursos do AEM centrados no Forms, consulte Fluxo de trabalho centrado no [Forms no OSGi](/help/forms/using/aem-forms-workflow.md).

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

Quando um fluxo de trabalho é acionado, uma carga é gerada automaticamente para a instância do fluxo de trabalho. Cada instância do fluxo de trabalho recebe uma ID de instância exclusiva e uma ID de carga associada. A carga contém os locais do repositório para dados de usuário e formulário associados a uma instância do fluxo de trabalho. Além disso, os rascunhos e os dados históricos de uma instância de fluxo de trabalho também são armazenados no repositório do AEM.

Os locais padrão do repositório onde a carga, os rascunhos e o histórico de uma instância de fluxo de trabalho residem são os seguintes:

>[!NOTE]
>
>Você pode configurar diferentes locais para armazenar dados de carga, rascunho e histórico ao criar um fluxo de trabalho ou aplicativo. Para identificar os locais onde um fluxo de trabalho ou aplicativo armazenou dados, reveja o fluxo de trabalho.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>AEM 6.4 Forms</td>
   <td>AEM 6.3 Forms</td>
  </tr>
  <tr>
   <td><strong>Instância de <br /> fluxo de trabalho</strong></td>
   <td>/var/workflow/instance/[server_id]/&lt;data&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instance/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Carga</strong></td>
   <td>/var/fd/painel/payload/[server_id]/[data]/<br /> [payload-id]/</td>
   <td>/etc/fd/painel/payload/[server_id]/[data]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Rascunhos</strong></td>
   <td>/var/fd/painel/instance/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/painel/instance/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>História</strong></td>
   <td>/var/fd/painel/instance/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/painel/instance/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar e excluir dados do usuário de uma instância do fluxo de trabalho no repositório. Para isso, é necessário saber a ID da instância da instância do fluxo de trabalho associada ao usuário. Você pode encontrar a ID de instância de uma instância do fluxo de trabalho usando o nome de usuário do usuário que iniciou a instância do fluxo de trabalho ou que é o destinatário atual da instância do fluxo de trabalho.

No entanto, você não pode identificar ou os resultados podem ser ambíguos ao identificar workflows associados a um iniciador nos seguintes cenários:

* **Fluxo de trabalho acionado por meio de uma pasta** assistida: Uma instância de fluxo de trabalho não pode ser identificada usando seu iniciador se o fluxo de trabalho for acionado por uma pasta assistida. Nesse caso, as informações do usuário são codificadas nos dados armazenados.
* **Fluxo de trabalho iniciado da instância** do AEM de publicação: Todas as instâncias de fluxo de trabalho são criadas usando um usuário de serviço quando formulários adaptáveis, comunicações interativas ou letras são enviadas da instância de publicação do AEM. Nesses casos, o nome de usuário do usuário conectado não é capturado nos dados da instância do fluxo de trabalho.

### Acessar dados do usuário {#access}

Para identificar e acessar os dados do usuário armazenados para uma instância do fluxo de trabalho, execute as seguintes etapas:

1. Na instância do autor de AEM, vá até `https://'[server]:[port]'/crx/de` e navegue até **[!UICONTROL Ferramentas > Query]**.

   Selecione **[!UICONTROL SQL2]** no menu suspenso **[!UICONTROL Tipo]** .

1. Dependendo das informações disponíveis, execute um dos seguintes query:

   * Execute o seguinte caso o iniciador do fluxo de trabalho seja conhecido:
   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Execute o seguinte caso o usuário cujos dados você está encontrando seja o destinatário atual do fluxo de trabalho:
   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   O query retorna o local de todas as instâncias do fluxo de trabalho para o iniciador do fluxo de trabalho especificado ou o destinatário do fluxo de trabalho atual.

   Por exemplo, o query a seguir retorna dois caminhos de instâncias de fluxo de trabalho do `/var/workflow/instances` nó cujo iniciador de fluxo de trabalho é `srose`.

   ![instância de fluxo de trabalho](assets/workflow-instance.png)

1. Vá para um caminho de instância de fluxo de trabalho retornado pelo query. A propriedade status exibe o status atual da instância do fluxo de trabalho.

   ![status](assets/status.png)

1. No nó da instância do fluxo de trabalho, navegue até `data/payload/`. A `path` propriedade armazena o caminho para a carga da instância do fluxo de trabalho. Você pode navegar até o caminho para acessar os dados armazenados na carga.

   ![caminho da carga](assets/payload-path.png)

1. Navegue até os locais para rascunhos e histórico da instância do fluxo de trabalho.

   Por exemplo:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Repita as etapas 3 a 5 para todas as instâncias de fluxo de trabalho retornadas pelo query na etapa 2.

>[!NOTE]
>
>O aplicativo AEM Forms também armazena dados no modo offline. É possível que os dados de uma instância de fluxo de trabalho sejam armazenados localmente em dispositivos individuais e enviados ao servidor do Forms quando o aplicativo é sincronizado com o servidor.

### Excluir dados do usuário {#delete-user-data}

Você deve ser um administrador do AEM para excluir dados de usuário das instâncias de fluxo de trabalho, executando as seguintes etapas:

1. Siga as instruções em Dados [do usuário do](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) Access e anote o seguinte:

   * Caminhos para instâncias de fluxo de trabalho associadas ao usuário
   * Status das instâncias de fluxo de trabalho
   * Caminhos para cargas para instâncias de fluxo de trabalho
   * Caminhos para rascunhos e histórico das instâncias de fluxo de trabalho

1. Execute esta etapa para instâncias de fluxo de trabalho em **EXECUÇÃO**, **SUSPENSA** ou status **STALE** :

   1. Vá para `https://'[server]:[port]'/aem/start.html` e faça logon com as credenciais de administrador.
   1. Navegue até **[!UICONTROL Ferramentas > Fluxo de trabalho > Instâncias]**.
   1. Selecione as instâncias de fluxo de trabalho relevantes para o usuário e toque em **[!UICONTROL Encerrar]** para encerrar as instâncias em execução.
   Para obter mais informações sobre como trabalhar com instâncias de fluxo de trabalho, consulte [Administração de instâncias](/help/sites-administering/workflows-administering.md)de fluxo de trabalho.

1. Vá para o console CRXDE Lite, navegue até o caminho da carga de uma instância do fluxo de trabalho e exclua o `payload` nó.
1. Navegue até o caminho de rascunhos de uma instância de fluxo de trabalho e exclua o `draft` nó.
1. Navegue até o caminho do histórico de uma instância de fluxo de trabalho e exclua o `history` nó.
1. Navegue até o caminho da instância do fluxo de trabalho para uma instância do fluxo de trabalho e exclua o `[workflow-instance-ID]` nó do fluxo de trabalho.

   >[!NOTE]
   >
   >A exclusão do nó da instância do fluxo de trabalho removerá a instância do fluxo de trabalho para todos os participantes do fluxo de trabalho.

1. Repita as etapas de 2 a 6 para todas as instâncias de fluxo de trabalho identificadas para um usuário.
1. Identifique e exclua dados de rascunho e envio offline da caixa de saída do aplicativo AEM Forms dos participantes do fluxo de trabalho para evitar qualquer envio ao servidor.

Você também pode usar APIs para acessar e remover nós e propriedades. Consulte os documentos a seguir para obter mais informações.

* [Como acessar programaticamente o JCR AEM](/help/sites-developing/access-jcr.md)
* [Remoção de nós e propriedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Referência da API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

