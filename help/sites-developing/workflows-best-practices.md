---
title: Práticas recomendadas do workflow
seo-title: Workflow Best Practices
description: Práticas recomendadas do workflow
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# Práticas recomendadas do workflow{#workflow-best-practices}

Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM).

Geralmente, eles representam uma grande quantidade do processamento que ocorre em um ambiente de AEM, de modo que, quando as etapas do fluxo de trabalho personalizado não são gravadas de acordo com as práticas recomendadas ou os fluxos de trabalho prontos não são configurados para serem executados da maneira mais eficiente possível, o sistema pode sofrer como resultado.

Portanto, é altamente recomendável planejar suas implementações de workflows com cuidado.

## Configuração {#configuration}

Ao configurar processos de fluxo de trabalho (personalizados e/ou prontos para uso), há algumas coisas que devem ser levadas em conta.

### Workflows transitórios {#transient-workflows}

Para otimizar cargas altas de ingestão, você pode definir um valor de [fluxo de trabalho como transitório](/help/sites-developing/workflows.md#transient-workflows).

Quando um workflow é transitório, os dados de tempo de execução relacionados às etapas de trabalho intermediárias não são persistentes no JCR quando são executados (as renderizações de saída são persistentes, é claro).

As vantagens podem incluir:

* Redução do tempo de processamento do workflow; de até 10%.
* Reduza significativamente o crescimento do repositório.
* Não é necessário mais workflows CRUD para limpar.
* Além disso, reduz o número de arquivos TAR a serem compactados.

>[!CAUTION]
>
>Se sua empresa determinar que você persiste/arquiva dados de tempo de execução do fluxo de trabalho para fins de auditoria, não ative esse recurso.

### Ajuste de fluxos de trabalho do DAM {#tuning-dam-workflows}

Para obter diretrizes de ajuste de desempenho para workflows DAM, consulte o [Guia de ajuste de desempenho do AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configurar o número máximo de fluxos de trabalho simultâneos {#configure-the-maximum-number-of-concurrent-workflows}

AEM pode permitir que vários threads de workflow sejam executados simultaneamente. Por padrão, o número de threads é configurado para ser metade do número de núcleos do processador no sistema.

Nos casos em que os workflows que estão sendo executados são exigentes dos recursos do sistema, isso pode significar que pouco resta para AEM usar em outras tarefas, como renderizar a interface do usuário de criação. Como resultado, o sistema pode ficar lento durante atividades como o upload de imagens em massa.

Para resolver esse problema, o Adobe recomenda configurar o número de **Máximo de trabalhos paralelos** deve estar entre metade e três quartos do número de núcleos do processador no sistema. Isso deve permitir capacidade suficiente para que o sistema continue responsivo ao processar esses workflows.

Para configurar **Máximo de trabalhos paralelos**, você pode:

* Configure o **[Configuração do OSGi](/help/sites-deploying/configuring-osgi.md)** do console AEM Web; para **Fila: Fila de Fluxo de Trabalho do Granite** a) **Configuração da fila de trabalhos do Apache Sling**).

* Configure a fila do **Trabalhos Sling** opção do console da Web AEM; para **Configuração da fila de trabalhos: Fila de Fluxo de Trabalho do Granite**, em `http://localhost:4502/system/console/slingevent`.

Além disso, há uma configuração separada para a variável **Fila de Trabalho de Processo Externo do Fluxo de Trabalho Granite**. Isso é usado para processos de workflow que iniciam binários externos, como **InDesign Server** ou **Imagem Magick**.

### Configurar filas de trabalhos individuais {#configure-individual-job-queues}

Em alguns casos, é útil configurar filas de trabalhos individuais para controlar encadeamentos simultâneos ou outras opções de fila, com base em um trabalho individual. Você pode adicionar e configurar uma fila individual no console da Web por meio do **Configuração da fila de trabalhos do Apache Sling** fábrica. Para encontrar o tópico apropriado para ser listado, execute o modelo de seu fluxo de trabalho e procure-o no **Trabalhos Sling** console; por exemplo, em `http://localhost:4502/system/console/slingevent`.

As filas de trabalhos individuais também podem ser adicionadas para fluxos de trabalho transitórios.

### Configurar limpeza de workflow {#configure-workflow-purging}

Numa instalação padrão, o AEM fornece um console de manutenção, onde as atividades de manutenção diárias e semanais podem ser programadas e configuradas; por exemplo, em:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Por padrão, a variável **Janela de manutenção semanal** tem um **Limpeza de Fluxo de Trabalho** , mas isso precisa ser configurado antes de ser executado. Para configurar limpeza de workflow, um novo **Configuração de limpeza de fluxo de trabalho do Adobe Granite** deve ser adicionado no console da Web.

Para obter mais detalhes sobre tarefas de manutenção no AEM, consulte o [Painel de operações](/help/sites-administering/operations-dashboard.md).

## Personalização {#customization}

Ao gravar processos de fluxo de trabalho personalizados, alguns itens devem ser considerados.

### Localizações {#locations}

As definições de modelos de fluxo de trabalho, iniciadores, scripts e notificações são mantidas no repositório de acordo com o tipo; ou seja, pronto, personalizado, entre outros.

>[!NOTE]
>
>Consulte também [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Locais - Modelos de fluxo de trabalho {#locations-workflow-models}

Os modelos de fluxo de trabalho são armazenados no repositório de acordo com o tipo :

* Os designs de fluxo de trabalho prontos para uso são mantidos no seguinte caminho:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos seus modelos de fluxo de trabalho personalizados nesta pasta
   >* edite qualquer item em `/libs`

   >
   >Como qualquer alteração pode ser substituída na atualização ou na instalação de hotfixes, pacotes de correções cumulativas ou service packs.

* Os designs de fluxo de trabalho personalizados são mantidos em:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Os designs de fluxo de trabalho em tempo de execução (integrados e personalizados) são mantidos no seguinte caminho:

   `/var/workflow/models/`

* Os designs de fluxo de trabalho herdados (tempo de design e tempo de execução) são mantidos no seguinte caminho:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Se esses designs forem editados *uso da interface do usuário do AEM*, os detalhes serão copiados para os novos locais.

#### Locais - Inicializadores de fluxo de trabalho {#locations-workflow-launchers}

As definições de iniciador de fluxo de trabalho também são armazenadas no repositório de acordo com o tipo :

* Os inicializadores de fluxo de trabalho prontos para uso são mantidos no seguinte caminho:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos seus iniciadores de fluxo de trabalho personalizados nesta pasta
   >* edite qualquer item em `/libs`

   >
   >Como qualquer alteração pode ser substituída na atualização ou na instalação de hotfixes, pacotes de correções cumulativas ou service packs.

* Os inicializadores de fluxo de trabalho personalizados são mantidos em:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* Os inicializadores de fluxo de trabalho herdados são mantidos no seguinte caminho:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Se essas definições forem editadas *uso da interface do usuário do AEM*, os detalhes serão copiados para os novos locais.

#### Locais - Scripts de fluxo de trabalho {#locations-workflow-scripts}

Os scripts de workflow também são armazenados no repositório de acordo com o tipo :

* Os scripts de workflow prontos para uso são mantidos no seguinte caminho:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer um dos scripts de fluxo de trabalho personalizados nesta pasta
   >* edite qualquer item em `/libs`

   >
   >Como qualquer alteração pode ser substituída na atualização ou na instalação de hotfixes, pacotes de correções cumulativas ou service packs.

* Os scripts de fluxo de trabalho personalizados são mantidos em:

   ```
   /apps/workflow/scripts/...
   ```

* Os scripts de fluxo de trabalho herdados são mantidos no seguinte caminho:

   `/etc/workflow/scripts/`

#### Locais - Notificações de fluxo de trabalho {#locations-workflow-notifications}

As notificações de workflow também são armazenadas no repositório de acordo com o tipo :

* As definições de notificação de workflow prontas para uso são mantidas no seguinte caminho:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Não:
   >
   >* coloque qualquer uma das suas definições de notificação de fluxo de trabalho personalizadas nesta pasta
   >* edite qualquer item em `/libs`

   >
   >Como qualquer alteração pode ser substituída na atualização ou na instalação de hotfixes, pacotes de correções cumulativas ou service packs.

* As definições de notificação de fluxo de trabalho personalizado são mantidas em:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Para substituir um texto de notificação de workflow, crie um caminho sobreposto em:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* As definições de notificação de fluxo de trabalho herdadas são mantidas no seguinte caminho:

   `/etc/workflow/notification/`

### Sessões de Processo {#process-sessions}

Como em qualquer desenvolvimento personalizado, sempre é recomendável usar uma sessão de usuário quando possível:

* para melhor cumprimento das diretrizes de segurança
* para permitir que o sistema gerencie a abertura e o fechamento da sessão

Ao implementar um processo de workflow:

* Uma sessão de workflow será fornecida e deverá ser usada, a menos que haja um motivo convincente para não fazê-lo.
* Novas sessões não devem ser criadas a partir de etapas do fluxo de trabalho, pois isso causa inconsistências no(s) estado(s) junto com possíveis problemas de simultaneidade no mecanismo de fluxo de trabalho.
* Você não deve adquirir uma nova sessão JCR de dentro de uma etapa do processo em um fluxo de trabalho; você deve adaptar a sessão do workflow fornecida pela API da etapa do processo a uma sessão jcr. Por exemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvar uma sessão:

* Em um processo de workflow, se a variável `WorkflowSession` está sendo usada para modificar o repositório e não salva explicitamente a sessão; o workflow salvará a sessão quando ela for concluída.
* `Session.Save` não deve ser chamado de em uma etapa do fluxo de trabalho:

   * é recomendável adaptar a sessão jcr do workflow; then `save` não é necessário, pois o mecanismo de workflow salva a sessão automaticamente após a conclusão da execução do workflow.
   * não é recomendado que uma etapa do processo crie sua própria sessão jcr.

* Ao eliminar salvamentos desnecessários, é possível reduzir a sobrecarga e, portanto, tornar os workflows mais eficientes.

>[!CAUTION]
>
>Se, apesar das recomendações aqui, você criar sua própria sessão jcr, ela precisará ser salva.

### Minimizar o número/escopo de iniciadores {#minimize-the-number-scope-of-launchers}

Há um ouvinte que é responsável por todos os [inicializadores de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) registrados:

* Ele vai acompanhar as alterações em todos os caminhos especificados nas propriedades de globalização dos outros lançadores.
* Quando um evento é despachado, o mecanismo de workflow avaliará cada iniciador para determinar se ele deve ser executado.

Criar muitos lançadores fará com que o processo de avaliação seja executado mais lentamente.

Criar um caminho de globalização na raiz do repositório em um único iniciador faria com que o mecanismo de fluxo de trabalho escutasse e avaliasse eventos de criação/modificação em cada nó no repositório. Por esse motivo, é recomendável criar apenas iniciadores necessários e tornar o caminho do globbing o o mais específico possível.

Devido ao impacto desses lançadores no comportamento do fluxo de trabalho, também pode ser útil desativar os iniciadores prontos para uso que não estejam em uso.

### Aprimoramentos de configuração para inicializadores {#configuration-enhancements-for-launchers}

O [configuração do iniciador](/help/sites-administering/workflows-starting.md#workflows-launchers) foi aprimorado para oferecer suporte ao seguinte:

* Ter várias condições &quot;AND&quot; juntas.
* Ter condições OU em uma única condição.
* Desativar/ativar lançadores com base no fato de um sinalizador de recurso estar ativado ou desativado.
* Suporte a regex nas condições do iniciador.

### Não iniciar fluxos de trabalho de outros fluxos de trabalho {#do-not-start-workflows-from-other-workflows}

Os workflows podem carregar uma quantidade significativa de sobrecarga, tanto em termos de objetos criados na memória quanto de nós rastreados no repositório. Por isso, é melhor fazer com que um workflow faça seu processamento sozinho em vez de iniciar workflows adicionais.

Um exemplo disso seria um fluxo de trabalho que implementa um processo de negócios em um conjunto de conteúdo e, em seguida, ativa esse conteúdo. É melhor criar um processo de fluxo de trabalho personalizado que ative cada um desses nós, em vez de iniciar um **Ativar conteúdo** modelo para cada um dos nós de conteúdo que precisam ser publicados. Essa abordagem exigirá trabalho de desenvolvimento adicional, mas é mais eficiente quando executada do que iniciar uma instância de fluxo de trabalho separada para cada ativação.

Outro exemplo seria um fluxo de trabalho que processa vários nós, cria um pacote de fluxo de trabalho e ativa esse pacote. Em vez de criar o pacote e depois iniciar um fluxo de trabalho separado com o pacote como carga útil, você pode alterar a carga do fluxo de trabalho na etapa que cria o pacote e, em seguida, chamar a etapa para ativar o pacote no mesmo modelo de fluxo de trabalho.

### Handler avançado {#handler-advance}

Ao projetar um modelo de fluxo de trabalho, você tem a opção de ativar o avanço do manipulador em suas etapas do fluxo de trabalho. Como alternativa, você pode adicionar código à etapa do fluxo de trabalho para determinar qual etapa deve ser executada em seguida e, em seguida, executá-la.

Recomenda-se usar o handler advance, pois oferece melhor desempenho.

### Estágios do Fluxo de Trabalho {#workflow-stages}

Você pode definir [estágios do workflow](/help/sites-developing/workflows.md#workflow-stages), atribua tarefas/etapas a um estágio de fluxo de trabalho específico.

Essas informações são usadas para exibir o progresso de um workflow quando você clica no [**Informações do fluxo de trabalho** guia de um item de trabalho da **Caixa de entrada**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Os modelos de fluxo de trabalho existentes podem ser editados para adição de estágios.

### Etapa Ativar processo da página {#activate-page-process-step}

O **Ativar processo de página** Essa etapa ativará páginas para você, mas não encontrará automaticamente quaisquer ativos do DAM referenciados e os ativará também.

Isso é algo que deve ser lembrado se você planeja usar essa etapa como parte de um modelo de fluxo de trabalho.

### Considerações sobre atualização {#upgrade-considerations}

Ao atualizar sua instância:

* certifique-se de que qualquer modelo de fluxo de trabalho personalizado tenha backup antes que uma instância seja atualizada.
* confirme se nenhum de seus fluxos de trabalho personalizados é armazenado na variável [localização](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte também [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Ferramentas do sistema {#system-tools}

Há muitas ferramentas de sistema disponíveis para ajudar com monitoramento, manutenção e solução de problemas de workflows. Todos os URLs de exemplo abaixo usam `localhost:4502`, mas deve estar disponível em qualquer instância do autor ( `<hostname>:<port>`).

### Console de Manuseio de Trabalho do Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

O console Sling Job Handling mostrará:

* Estatísticas do estado dos trabalhos no sistema desde a última reinicialização.
* Ele também mostrará as configurações para todas as filas de tarefas e fornecerá um atalho para editá-las no gerenciador de configuração.

### Ferramenta Relatório de Fluxo de Trabalho {#workflow-report-tool}

A ferramenta de relatório do workflow está sendo removida na versão 6.3 para evitar a degradação do desempenho.

### MBean de operações de manutenção de fluxo de trabalho {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

O MBean de manutenção de workflow expõe várias rotinas de manutenção úteis, como limpar workflows concluídos e recuperar estatísticas de workflow.

## Informações adicionais {#further-information}

Para obter mais informações, consulte:

* [Trabalhar com fluxos de trabalho](/help/sites-authoring/workflows.md)
* [Administração de fluxos de trabalho](/help/sites-administering/workflows.md)
* [Desenvolvimento e extensão de workflows](/help/sites-developing/workflows.md)
* [Otimização de desempenho](/help/sites-deploying/configuring-performance.md)
