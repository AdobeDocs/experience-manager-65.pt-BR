---
title: Práticas recomendadas do fluxo de trabalho
seo-title: Práticas recomendadas do fluxo de trabalho
description: 'null'
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Práticas recomendadas do fluxo de trabalho{#workflow-best-practices}

Os fluxos de trabalho permitem automatizar as atividades do Adobe Experience Manager (AEM).

Geralmente, eles representam uma grande quantidade de processamento que ocorre em um ambiente AEM, de modo que, quando as etapas de fluxo de trabalho personalizadas não são gravadas de acordo com as práticas recomendadas ou os fluxos de trabalho predefinidos não são configurados para serem executados com a maior eficiência possível, o sistema pode sofrer como resultado.

Portanto, é altamente recomendável planejar suas implementações de fluxos de trabalho com cuidado.

## Configuração {#configuration}

Ao configurar processos de fluxo de trabalho (personalizados e/ou prontos para uso), há algumas coisas que devem ser lembradas.

### Fluxos de trabalho transitórios {#transient-workflows}

Para otimizar cargas de ingestão altas, é possível definir um [fluxo de trabalho como transitório](/help/sites-developing/workflows.md#transient-workflows).

Quando um fluxo de trabalho é temporário, os dados de tempo de execução relacionados às etapas de trabalho intermediárias não são persistentes no JCR quando são executados (as renderizações de saída são, claro, persistentes).

As vantagens podem incluir:

* Redução do tempo de processamento do fluxo de trabalho; de até 10%.
* Reduza significativamente o crescimento do repositório.
* Não é necessário mais fluxos de trabalho CRUD para expurgar.
* Além disso, reduz o número de arquivos TAR para compactar.

>[!CAUTION]
>
>Se a sua empresa determinar que você persiste/arquiva dados de tempo de execução do fluxo de trabalho para fins de auditoria, não ative esse recurso.

### Ajustar fluxos de trabalho de DAM {#tuning-dam-workflows}

Para obter diretrizes de ajuste de desempenho para fluxos de trabalho DAM, consulte o Guia [de ajuste de desempenho do](/help/assets/performance-tuning-guidelines.md)AEM Assets.

### Configurar o número máximo de fluxos de trabalho simultâneos {#configure-the-maximum-number-of-concurrent-workflows}

O AEM pode permitir que vários processos de fluxo de trabalho sejam executados simultaneamente. Por padrão, o número de threads é configurado para ser metade do número de núcleos do processador no sistema.

Nos casos em que os fluxos de trabalho que estão sendo executados exigem recursos do sistema, isso pode significar que pouco é deixado para o AEM usar para outras tarefas, como renderizar a interface de criação. Como resultado, o sistema pode ficar lento durante atividades como upload de imagens em massa.

Para resolver esse problema, a Adobe recomenda configurar o número de **Máximo de Trabalhos** Paralelos para que fique entre metade e três quartos do número de núcleos do processador no sistema. Isso deve permitir capacidade suficiente para que o sistema continue respondendo ao processar esses fluxos de trabalho.

Para configurar **Máximo de Trabalhos** Paralelos, você pode:

* Configurar a configuração **[do](/help/sites-deploying/configuring-osgi.md)**OSGi no console da Web do AEM; para **Fila: Fila**de fluxo de trabalho Granite (uma configuração ****de fila de trabalho Apache Sling).

* Configure a fila da opção **Sling Jobs** do console da Web do AEM; para Configuração da Fila de **Tarefas: Fila** de Fluxo de Trabalho Granite, em `http://localhost:4502/system/console/slingevent`.

Além disso, há uma configuração separada para a Fila **de Trabalho do Processo Externo do Fluxo de Trabalho** Granite. Isso é usado para processos de fluxo de trabalho que iniciam binários externos, como o **InDesign Server** ou o **Image Magick**.

### Configurar filas de trabalho individuais {#configure-individual-job-queues}

Em alguns casos, é útil configurar filas de trabalhos individuais para controlar threads simultâneos, ou outras opções de fila, com base em tarefas individuais. Você pode adicionar e configurar uma fila individual do console da Web por meio da fábrica Configuração **da fila de trabalhos do** Apache Sling. Para localizar o tópico apropriado para listar, execute o modelo do seu fluxo de trabalho e procure-o no console **Sling Jobs** ; por exemplo, em `http://localhost:4502/system/console/slingevent`.

As filas de trabalhos individuais também podem ser adicionadas para fluxos de trabalho transitórios.

### Configurar Expurgação do Fluxo de Trabalho {#configure-workflow-purging}

Em uma instalação padrão, o AEM fornece um console de manutenção no qual as atividades de manutenção diárias e semanais podem ser programadas e configuradas; por exemplo, em:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Por padrão, a Janela **de Manutenção** Semanal tem uma tarefa de Expurgação **do** Fluxo de Trabalho, mas isso precisa ser configurado antes de ser executada. Para configurar expurgações de fluxo de trabalho, uma nova Configuração **de Expurgação de Fluxo de Trabalho do** Adobe Granite deve ser adicionada ao console da Web.

Para obter mais detalhes sobre as tarefas de manutenção no AEM, consulte o Painel [de](/help/sites-administering/operations-dashboard.md)operações.

## Personalização {#customization}

Ao escrever processos de fluxo de trabalho personalizados, há algumas coisas que devem ser levadas em consideração.

### Localizações {#locations}

As definições de modelos de fluxo de trabalho, lançadores, scripts e notificações são mantidas no repositório de acordo com o tipo; ou seja, fora da caixa, personalizado, entre outros.

>[!NOTE]
>
>Consulte também Reestruturação [de repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Locais - Modelos de fluxo de trabalho {#locations-workflow-models}

Os modelos de fluxo de trabalho são armazenados no repositório de acordo com o tipo:

* Os designs de fluxo de trabalho predefinidos são mantidos no seguinte caminho:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos seus modelos de fluxo de trabalho personalizados nesta pasta
   >* editar qualquer item em `/libs`
   >
   >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, pacotes de correção cumulativos ou service packs.

* Os designs de fluxo de trabalho personalizados são mantidos em:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Os designs de fluxo de trabalho de tempo de execução (prontos para uso e personalizados) são mantidos no seguinte caminho:

   `/var/workflow/models/`

* Os designs de fluxo de trabalho herdados (tempo de design e tempo de execução) são mantidos no seguinte caminho:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Se esses designs forem editados *usando a interface do usuário* do AEM, os detalhes serão copiados para os novos locais.

#### Locais - Inicializações de fluxo de trabalho {#locations-workflow-launchers}

As definições do iniciador do fluxo de trabalho também são armazenadas no repositório de acordo com o tipo:

* Os iniciadores de fluxo de trabalho predefinidos são mantidos no seguinte caminho:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos seus iniciadores de fluxo de trabalho personalizados nesta pasta
   >* editar qualquer item em `/libs`
   >
   >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, pacotes de correção cumulativos ou service packs.

* Os iniciadores de fluxo de trabalho personalizados são mantidos em:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Os iniciadores de fluxo de trabalho herdados são mantidos sob o seguinte caminho:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Se essas definições forem editadas *usando a interface do usuário* do AEM, os detalhes serão copiados para os novos locais.

#### Locais - Scripts de fluxo de trabalho {#locations-workflow-scripts}

Os scripts de fluxo de trabalho também são armazenados no repositório de acordo com o tipo:

* Os scripts de fluxo de trabalho predefinidos são mantidos no seguinte caminho:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos scripts de fluxo de trabalho personalizados nesta pasta
   >* editar qualquer item em `/libs`
   >
   >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, pacotes de correção cumulativos ou service packs.

* Os scripts de fluxo de trabalho personalizados são mantidos em:

   ```
   /apps/workflow/scripts/...
   ```

* Os scripts de fluxo de trabalho herdados são mantidos no seguinte caminho:

   `/etc/workflow/scripts/`

#### Locais - Notificações de fluxo de trabalho {#locations-workflow-notifications}

As notificações de fluxo de trabalho também são armazenadas no repositório de acordo com o tipo:

* As definições de notificação de fluxo de trabalho predefinidas são mantidas no seguinte caminho:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer uma de suas definições de notificação de fluxo de trabalho personalizadas nesta pasta
   >* editar qualquer item em `/libs`
   >
   >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, pacotes de correção cumulativos ou service packs.

* As definições de notificação de fluxo de trabalho personalizado são mantidas em:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Se desejar substituir um texto de notificação de fluxo de trabalho, crie um caminho sobreposto em:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* As definições de notificação de fluxo de trabalho herdado são mantidas no seguinte caminho:

   `/etc/workflow/notification/`

### Processar sessões {#process-sessions}

Como em qualquer desenvolvimento personalizado, sempre é recomendável usar uma sessão de usuário quando possível:

* para melhor cumprimento das diretrizes de segurança
* para permitir que o sistema gerencie a abertura e o fechamento da sessão

Ao implementar um processo de fluxo de trabalho:

* Uma sessão de fluxo de trabalho será fornecida e deverá ser usada, a menos que haja uma razão convincente para não o fazer.
* As novas sessões não devem ser criadas a partir das etapas do fluxo de trabalho, pois isso causa inconsistências no(s) estado(s) juntamente com possíveis problemas de simultaneidade no mecanismo de fluxo de trabalho.
* Você não deve adquirir uma nova sessão JCR de dentro de uma etapa do processo em um fluxo de trabalho; você deve adaptar a sessão do fluxo de trabalho fornecida pela API de Etapa do Processo a uma sessão jcr. Por exemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvando uma sessão:

* Em um processo de fluxo de trabalho, se o `WorkflowSession` estiver sendo usado para modificar o repositório, não salve explicitamente a sessão - o fluxo de trabalho salvará a sessão quando ela for concluída.
* `Session.Save` não deve ser chamado de dentro de uma etapa de fluxo de trabalho:

   * recomenda-se adaptar a sessão jcr do fluxo de trabalho; então, não `save` é necessário, pois o mecanismo de fluxo de trabalho salva a sessão automaticamente assim que o fluxo de trabalho terminar de ser executado.
   * não é recomendado que uma etapa do processo crie sua própria sessão jcr.

* Ao eliminar economias desnecessárias, você pode reduzir a sobrecarga e, assim, tornar os fluxos de trabalho mais eficientes.

>[!CAUTION]
>
>Se, apesar das recomendações aqui, você criar sua própria sessão jcr, então ela precisará ser salva.

### Minimizar o número/escopo de iniciadores {#minimize-the-number-scope-of-launchers}

Há um listener responsável por todos os iniciadores [de](/help/sites-administering/workflows-starting.md#workflows-launchers) fluxo de trabalho registrados:

* Ele vai acompanhar as mudanças em todos os caminhos especificados nas propriedades de globalização dos outros lançadores.
* Quando um evento é despachado, o mecanismo de fluxo de trabalho avaliará cada iniciador para determinar se ele deve ser executado.

Criar muitos lançadores fará com que o processo de avaliação seja executado mais lentamente.

A criação de um caminho de globalização na raiz do repositório em um único iniciador faria com que o mecanismo de fluxo de trabalho ouvisse e avaliasse eventos de criação/modificação para cada nó no repositório. Por essa razão, recomenda-se criar apenas os iniciadores necessários e tornar o caminho de globalização o mais específico possível.

Devido ao impacto desses iniciadores no comportamento do fluxo de trabalho, também pode ser útil desativar os iniciadores prontos para uso que não estejam em uso.

### Aprimoramentos de configuração para iniciadores {#configuration-enhancements-for-launchers}

A configuração [personalizada do](/help/sites-administering/workflows-starting.md#workflows-launchers) iniciador foi aprimorada para suportar o seguinte:

* Têm várias condições &quot;AND&quot; juntas.
* Ter condições OU em uma única condição.
* Desabilitar/habilitar iniciadores com base no fato de um sinalizador de recurso estar habilitado ou desabilitado.
* Regex de suporte em condições de lançamento.

### Não iniciar fluxos de trabalho de outros fluxos de trabalho {#do-not-start-workflows-from-other-workflows}

Os fluxos de trabalho podem conter uma quantidade significativa de sobrecarga, tanto em termos de objetos criados na memória quanto em nós rastreados no repositório. Por essa razão, é melhor fazer com que um fluxo de trabalho faça seu processamento em si mesmo em vez de iniciar fluxos de trabalho adicionais.

Um exemplo disso seria um fluxo de trabalho que implementa um processo de negócios em um conjunto de conteúdo e, em seguida, ativa esse conteúdo. É melhor criar um processo de fluxo de trabalho personalizado que ative cada um desses nós, em vez de iniciar um modelo **Ativar conteúdo** para cada um dos nós de conteúdo que precisam ser publicados. Essa abordagem exigirá trabalho de desenvolvimento adicional, mas é mais eficiente quando executada do que iniciar uma instância de fluxo de trabalho separada para cada ativação.

Outro exemplo seria um fluxo de trabalho que processa vários nós, cria um pacote de fluxo de trabalho e, em seguida, ativa esse pacote. Em vez de criar o pacote e iniciar um fluxo de trabalho separado com o pacote como carga, você pode alterar a carga do fluxo de trabalho na etapa que cria o pacote e, em seguida, chamar a etapa para ativar o pacote dentro do mesmo modelo de fluxo de trabalho.

### Handler avançado {#handler-advance}

Ao projetar um modelo de fluxo de trabalho, você tem a opção de ativar o avanço do manipulador nas etapas do fluxo de trabalho. Como alternativa, você pode adicionar código à etapa do fluxo de trabalho para determinar qual etapa deve ser executada em seguida e, em seguida, executá-la.

Recomenda-se usar o handler advanced, pois ele oferece melhor desempenho.

### Etapas do fluxo de trabalho {#workflow-stages}

Você pode definir estágios [do](/help/sites-developing/workflows.md#workflow-stages)fluxo de trabalho e, em seguida, atribuir tarefas/etapas a uma etapa específica do fluxo de trabalho.

Essas informações são usadas para exibir o progresso de um fluxo de trabalho quando você clica na guia Informações [**do **fluxo de trabalho de um item da** Caixa de entrada **](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Os modelos de fluxo de trabalho existentes podem ser editados para adicionar estágios.

### Etapa Ativar processo de página {#activate-page-process-step}

A etapa **Ativar processo** de página ativará as páginas para você, mas não encontrará automaticamente nenhum ativo DAM referenciado e os ativará também.

Isso é algo que deve ser lembrado se você planeja usar essa etapa como parte de um modelo de fluxo de trabalho.

### Considerações sobre atualização {#upgrade-considerations}

Ao atualizar sua instância:

* verifique se foi feito backup de todos os modelos de fluxo de trabalho personalizados antes de atualizar uma instância.
* confirme se nenhum de seus fluxos de trabalho personalizados está armazenado no [local](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte também Reestruturação [de repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Ferramentas do sistema {#system-tools}

Há muitas ferramentas de sistema disponíveis para ajudar no monitoramento, manutenção e solução de problemas de fluxos de trabalho. Todos os URLs de exemplo abaixo usam `localhost:4502`, mas devem estar disponíveis em qualquer instância do autor ( `<hostname>:<port>`).

### Console de Manuseio de Trabalho Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

O console Sling Job Handling mostrará:

* Estatísticas sobre o estado dos trabalhos no sistema desde a última reinicialização.
* Também mostrará as configurações de todas as filas de trabalhos e fornecerá um atalho para editá-las no gerenciador de configurações.

### Ferramenta de relatório de fluxo de trabalho {#workflow-report-tool}

A ferramenta de relatório de fluxo de trabalho está sendo removida na versão 6.3 para evitar a degradação do desempenho.

### MBean de operações de manutenção de fluxo de trabalho {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

O MBean de manutenção de fluxo de trabalho expõe várias rotinas de manutenção úteis, como expurgar fluxos de trabalho concluídos e recuperar estatísticas de fluxo de trabalho.

## Informações adicionais {#further-information}

Para obter mais informações, consulte:

* [Trabalhar com fluxos de trabalho](/help/sites-authoring/workflows.md)
* [Administração de fluxos de trabalho](/help/sites-administering/workflows.md)
* [Desenvolvimento e extensão de fluxos de trabalho](/help/sites-developing/workflows.md)
* [Otimização do desempenho](/help/sites-deploying/configuring-performance.md)