---
title: Fluxos de trabalho centrados na Forms no OSGi | Tratamento de dados de utilizadores
seo-title: Forms-centric workflows on OSGi | Handling user data
description: Fluxos de trabalho centrados na Forms no OSGi | Tratamento de dados de utilizadores
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Admin
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Fluxos de trabalho centrados na Forms no OSGi | Tratamento de dados de utilizadores {#forms-centric-workflows-on-osgi-handling-user-data}

Os fluxos de trabalho de AEM centrados no Forms permitem automatizar processos de negócios centrados no Forms. Os workflows consistem em uma série de etapas executadas em uma ordem especificada no modelo de workflow associado. Cada etapa executa uma ação específica, como atribuir uma tarefa a um usuário ou enviar uma mensagem de email. Os workflows podem interagir com ativos no repositório, contas de usuário e serviços. Portanto, os workflows podem coordenar atividades complicadas que envolvem qualquer aspecto do Experience Manager.

Um fluxo de trabalho centrado em formulários pode ser acionado ou iniciado por meio de qualquer um dos seguintes métodos:

* Envio de um aplicativo AEM Caixa de entrada
* Apresentação de um pedido de AEM [!DNL Forms] Aplicativo
* Envio de um formulário adaptável
* Uso de uma pasta assistida
* Envio de uma comunicação interativa ou uma carta

Para obter mais informações sobre fluxos de trabalho e recursos de AEM centrados no Forms, consulte [Fluxo de trabalho centrado no Forms no OSGi](/help/forms/using/aem-forms-workflow.md).

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

Quando um workflow é acionado, uma carga é gerada automaticamente para a instância do workflow. Cada instância do fluxo de trabalho recebe uma ID de instância exclusiva e uma ID de carga associada. A carga contém os locais do repositório para dados de usuário e formulário associados a uma instância de fluxo de trabalho. Além disso, rascunhos e dados históricos de uma instância de workflow também são armazenados no repositório AEM.

Os locais padrão do repositório onde reside a carga, os rascunhos e o histórico de uma instância de fluxo de trabalho são os seguintes:

>[!NOTE]
>
>Você pode configurar diferentes locais para armazenar dados de carga, rascunho e histórico ao criar um fluxo de trabalho ou aplicativo. Para identificar os locais onde um fluxo de trabalho ou aplicativo armazena dados, revise o fluxo de trabalho.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Fluxo de trabalho <br /> instância</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Carga</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Rascunhos</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/rascunho/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/rascunho/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>História</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar e excluir dados do usuário de uma instância de workflow no repositório. Para isso, você deve saber a ID da instância da instância do fluxo de trabalho associada ao usuário. Você pode encontrar a ID da instância de uma instância de fluxo de trabalho usando o nome de usuário do usuário que iniciou a instância do fluxo de trabalho ou que é o destinatário atual da instância do fluxo de trabalho.

No entanto, você não pode identificar ou os resultados podem ser ambíguos ao identificar workflows associados a um iniciador nos seguintes cenários:

* **Fluxo de trabalho acionado por meio de uma pasta monitorada**: Uma instância de workflow não pode ser identificada usando seu iniciador se o workflow for acionado por uma pasta monitorada. Nesse caso, as informações do usuário são codificadas nos dados armazenados.
* **Fluxo de trabalho iniciado a partir da instância de publicação AEM**: Todas as instâncias de fluxo de trabalho são criadas usando um usuário de serviço quando formulários adaptáveis, comunicações interativas ou cartas são enviadas AEM instância de publicação. Nesses casos, o nome de usuário do usuário conectado não é capturado nos dados da instância do fluxo de trabalho.

### Acessar dados do usuário {#access}

Para identificar e acessar os dados do usuário armazenados para uma instância de workflow, execute as seguintes etapas:

1. Na instância AEM autor, acesse `https://'[server]:[port]'/crx/de` e navegue até **[!UICONTROL Ferramentas > Consulta]**.

   Selecionar **[!UICONTROL SQL2]** do **[!UICONTROL Tipo]** lista suspensa.

1. Dependendo das informações disponíveis, execute uma das seguintes consultas:

   * Execute o seguinte se o iniciador do workflow for conhecido:

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Execute o seguinte se o usuário cujos dados você está encontrando for o destinatário do fluxo de trabalho atual:

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   A query retorna o local de todas as instâncias de fluxo de trabalho para o iniciador do fluxo de trabalho especificado ou o destinatário do fluxo de trabalho atual.

   Por exemplo, a consulta a seguir retorna dois caminhos de instâncias de fluxo de trabalho da variável `/var/workflow/instances` nó cujo iniciador do fluxo de trabalho é `srose`.

   ![instância de fluxo de trabalho](assets/workflow-instance.png)

1. Vá para um caminho de instância de workflow retornado pela query. A propriedade status exibe o status atual da instância do fluxo de trabalho.

   ![status](assets/status.png)

1. No nó da instância do fluxo de trabalho, navegue até `data/payload/`. O `path` armazena o caminho para a carga da instância do fluxo de trabalho. Você pode navegar até o caminho para acessar dados armazenados no payload.

   ![payload-path](assets/payload-path.png)

1. Navegue até os locais para rascunhos e histórico da instância do workflow.

   Por exemplo:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Repita as etapas 3 a 5 para todas as instâncias de fluxo de trabalho retornadas pela consulta na etapa 2.

   >[!NOTE]
   >
   >AEM [!DNL Forms] o aplicativo também armazena dados no modo offline. É possível que os dados de uma instância de workflow sejam armazenados localmente em dispositivos individuais e sejam enviados ao [!DNL Forms] quando o aplicativo é sincronizado com o servidor.

### Excluir dados do usuário {#delete-user-data}

Você deve ser um administrador AEM para excluir dados do usuário das instâncias do fluxo de trabalho, executando as seguintes etapas:

1. Siga as instruções em [Acessar dados do usuário](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) e tomar nota do seguinte:

   * Caminhos para instâncias de fluxo de trabalho associadas ao usuário
   * Status das instâncias de fluxo de trabalho
   * Caminhos para cargas das instâncias do fluxo de trabalho
   * Caminhos para rascunhos e histórico das instâncias do fluxo de trabalho

1. Execute esta etapa para instâncias de fluxo de trabalho em **EM EXECUÇÃO**, **SUSPENSA** ou **STALE** status:

   1. Ir para `https://'[server]:[port]'/aem/start.html` e faça logon com credenciais de administrador.
   1. Navegar para **[!UICONTROL Ferramentas > Fluxo de trabalho > Instâncias]**.
   1. Selecione as instâncias de fluxo de trabalho relevantes para o usuário e toque em **[!UICONTROL Encerrar]** para encerrar instâncias em execução.

      Para obter mais informações sobre como trabalhar com instâncias de fluxo de trabalho, consulte [Administração de instâncias de fluxo de trabalho](/help/sites-administering/workflows-administering.md).

1. Ir para [!DNL CRXDE Lite] , navegue até o caminho de carga de uma instância de fluxo de trabalho e exclua o `payload` nó .
1. Navegue até o caminho de rascunhos de uma instância de fluxo de trabalho e exclua o `draft` nó .
1. Navegue até o caminho do histórico para uma instância de fluxo de trabalho e exclua o `history` nó .
1. Navegue até o caminho da instância do fluxo de trabalho para uma instância do fluxo de trabalho e exclua o `[workflow-instance-ID]` nó do fluxo de trabalho.

   >[!NOTE]
   >
   >A exclusão do nó da instância do fluxo de trabalho removerá a instância do fluxo de trabalho para todos os participantes do fluxo de trabalho.

1. Repita as etapas 2 a 6 para todas as instâncias de fluxo de trabalho identificadas para um usuário.
1. Identificar e excluir dados de rascunho e envio offline do AEM [!DNL Forms] Caixa de saída do aplicativo dos participantes do fluxo de trabalho para evitar qualquer envio para o servidor.

Também é possível usar APIs para acessar e remover nós e propriedades. Consulte os documentos a seguir para obter mais informações.

* [Como acessar programaticamente o JCR AEM](/help/sites-developing/access-jcr.md)
* [Remover nós e propriedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Referência da API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)
