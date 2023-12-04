---
title: Práticas recomendadas de workflow
seo-title: Workflow Best Practices
description: Conheça as práticas recomendadas para trabalhar com fluxos de trabalho no Adobe Experience Manager.
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 1%

---

# Práticas recomendadas de workflow{#workflow-best-practices}

Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM).

Geralmente representam uma grande quantidade do processamento que ocorre em um ambiente AEM, de modo que, quando as etapas personalizadas do fluxo de trabalho não são gravadas de acordo com as práticas recomendadas ou os fluxos de trabalho prontos para uso não são configurados para serem executados da maneira mais eficiente possível, o sistema pode sofrer como resultado.

Portanto, é altamente recomendável planejar as implementações dos workflows com cuidado.

## Configuração {#configuration}

Ao configurar processos de fluxo de trabalho (personalizados e/ou prontos para uso), há algumas coisas que devem ser lembradas.

### Workflows transitórios {#transient-workflows}

Para otimizar cargas de assimilação altas, é possível definir um [workflow como temporário](/help/sites-developing/workflows.md#transient-workflows).

Quando um workflow é transitório, os dados de tempo de execução relacionados às etapas de trabalho intermediárias não são mantidos no JCR quando executados (as representações de saída são mantidas).

As vantagens podem incluir:

* Uma redução no tempo de processamento do fluxo de trabalho de até 10%.
* Reduzir significativamente o crescimento do repositório.
* Não são necessários mais workflows CRUD para limpar.
* Além disso, reduz o número de arquivos TAR para compactar.

>[!CAUTION]
>
>Se sua empresa determinar que você mantenha/arquive os dados de tempo de execução do fluxo de trabalho para fins de auditoria, não ative esse recurso.

### Ajuste de fluxos de trabalho do DAM {#tuning-dam-workflows}

Para obter diretrizes de ajuste de desempenho para workflows do DAM, consulte o [Guia de ajuste de desempenho do AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configurar o número máximo de workflows simultâneos {#configure-the-maximum-number-of-concurrent-workflows}

O AEM pode permitir que vários threads de fluxo de trabalho sejam executados simultaneamente. Por padrão, o número de processos é configurado para ser a metade do número de núcleos de processador no sistema.

Nos casos em que os workflows que estão sendo executados exigem recursos do sistema, isso pode significar que pouco resta para o AEM usar para outras tarefas, como renderizar a interface do usuário de criação. Como resultado, o sistema pode ficar lento durante atividades como carregamento de imagens em massa.

Para resolver esse problema, o Adobe recomenda configurar o número de **Máximo de Trabalhos Paralelos** ser de metade a três quartos do número de núcleos de processadores no sistema. Isso deve permitir capacidade suficiente para que o sistema permaneça responsivo ao processar esses workflows.

Para configurar **Máximo de Trabalhos Paralelos**, é possível:

* Configure o **[Configuração OSGi](/help/sites-deploying/configuring-osgi.md)** a partir do console da Web AEM; para **Fila: Fila de fluxo de trabalho do Granite** (um **Configuração da fila de trabalhos do Apache Sling**).

* Configure a lata de fila no **Sling Jobs** opção do console da Web AEM; para **Configuração da fila de trabalhos: Fila de fluxos de trabalho do Granite**, em `http://localhost:4502/system/console/slingevent`.

Além disso, há uma configuração separada para o **Fila de trabalho do processo externo do fluxo de trabalho do Granite**. Isso é usado para processos de fluxo de trabalho que iniciam binários externos, como **InDesign Server** ou **Image Magick**.

### Configurar Filas de Trabalhos Individuais {#configure-individual-job-queues}

Em alguns casos, é útil configurar filas de jobs individuais para controlar threads simultâneas ou outras opções de fila, com base em jobs individuais. Você pode adicionar e configurar uma fila individual no console da Web por meio da **Configuração da fila de trabalhos do Apache Sling** fábrica. Para encontrar o tópico apropriado para listar, execute o modelo do fluxo de trabalho e procure-o no **Sling Jobs** console; por exemplo, em `http://localhost:4502/system/console/slingevent`.

Filas de trabalhos individuais também podem ser adicionadas para fluxos de trabalho transitórios.

### Configurar a limpeza de fluxo de trabalho {#configure-workflow-purging}

Em uma instalação padrão, o AEM fornece um console de manutenção em que as atividades de manutenção diárias e semanais podem ser programadas e configuradas; por exemplo, em:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Por padrão, a variável **Janela de manutenção semanal** tem um **Limpeza do fluxo de trabalho** tarefa, mas precisa ser configurada antes de ser executada. Para configurar descartes de fluxo de trabalho, um novo **Configuração de limpeza de fluxo de trabalho do Adobe Granite** deve ser adicionado ao console da Web.

Para obter mais detalhes sobre tarefas de manutenção no AEM, consulte o [Painel de operações](/help/sites-administering/operations-dashboard.md).

## Personalização {#customization}

Ao escrever processos de fluxo de trabalho personalizados, há algumas coisas que devem ser lembradas.

### Localizações {#locations}

As definições de modelos de fluxo de trabalho, iniciadores, scripts e notificações são mantidas no repositório de acordo com o tipo; ou seja, prontas para uso, personalizadas, entre outras.

>[!NOTE]
>
>Consulte também [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Locais - Modelos de fluxo de trabalho {#locations-workflow-models}

Os modelos de fluxo de trabalho são armazenados no repositório de acordo com o tipo:

* Os designs de workflow prontos para uso são mantidos no seguinte caminho:

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >Não:
  >
  >* coloque qualquer um dos modelos de fluxo de trabalho personalizados nesta pasta
  >* editar qualquer item em `/libs`
  >
  >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, cumulative fix packs ou service packs.

* Os designs personalizados de fluxo de trabalho são mantidos em:

  ```
  /conf/global/settings/workflow/models/...
  ```

* Os designs do fluxo de trabalho de tempo de execução (prontos para uso e personalizados) são mantidos no seguinte caminho:

  `/var/workflow/models/`

* Os designs de fluxo de trabalho herdados (tempo de design e tempo de execução) são mantidos no seguinte caminho:

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >Se esses designs forem editados *uso da interface do AEM*, os detalhes serão copiados para os novos locais.

#### Locais - Iniciadores de fluxo de trabalho {#locations-workflow-launchers}

As definições do iniciador de fluxo de trabalho também são armazenadas no repositório de acordo com o tipo:

* Os iniciadores de fluxos de trabalho prontos para uso são mantidos no seguinte caminho:

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >Não:
  >
  >* coloque qualquer um dos iniciadores de fluxo de trabalho personalizados nesta pasta
  >* editar qualquer item em `/libs`
  >
  >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, cumulative fix packs ou service packs.

* Os iniciadores de fluxo de trabalho personalizados são mantidos em:

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* Os iniciadores de fluxos de trabalho herdados são mantidos no seguinte caminho:

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >Se essas definições forem editadas, *uso da interface do AEM*, os detalhes serão copiados para os novos locais.

#### Locais - Scripts de fluxo de trabalho {#locations-workflow-scripts}

Os scripts de fluxo de trabalho também são armazenados no repositório de acordo com o tipo:

* Os scripts de workflow prontos para uso são mantidos no seguinte caminho:

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >Não:
  >
  >* coloque qualquer um dos scripts de fluxo de trabalho personalizados nesta pasta
  >* editar qualquer item em `/libs`
  >
  >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, cumulative fix packs ou service packs.

* Os scripts de fluxo de trabalho personalizados são mantidos em:

  ```
  /apps/workflow/scripts/...
  ```

* Os scripts de workflow herdados são mantidos no seguinte caminho:

  `/etc/workflow/scripts/`

#### Locais - Notificações de fluxo de trabalho {#locations-workflow-notifications}

As notificações de fluxo de trabalho também são armazenadas no repositório de acordo com o tipo:

* As definições de notificação de workflow prontas para uso são mantidas no seguinte caminho:

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >Não:
  >
  >* colocar qualquer uma das definições de notificação de fluxo de trabalho personalizadas nesta pasta
  >* editar qualquer item em `/libs`
  >
  >Como qualquer alteração pode ser substituída na atualização ou ao instalar hot fixes, cumulative fix packs ou service packs.

* As definições de notificação de workflow personalizadas são mantidas em:

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >Se quiser substituir um texto de notificação de workflow, crie um caminho sobreposto em:
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* As definições de notificação de workflow herdadas são mantidas no seguinte caminho:

  `/etc/workflow/notification/`

### Sessões de Processo {#process-sessions}

Como em qualquer desenvolvimento personalizado, é sempre recomendável usar a sessão de um usuário quando possível:

* para melhor adesão às diretrizes de segurança
* para permitir que o sistema gerencie a abertura e o fechamento da sessão

Ao implementar um processo de workflow:

* Uma sessão de fluxo de trabalho será fornecida e deverá ser usada, a menos que haja um motivo convincente para não ser fornecida.
* Novas sessões não devem ser criadas a partir de etapas do fluxo de trabalho, pois isso causa inconsistências no(s) estado(s), juntamente com possíveis problemas de simultaneidade no mecanismo do fluxo de trabalho.
* Você não deve adquirir uma nova sessão JCR de dentro de uma etapa do processo em um fluxo de trabalho; você deve adaptar a sessão do fluxo de trabalho fornecida pela API de etapas do processo a uma sessão jcr. Por exemplo:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvando uma sessão:

* Em um processo de workflow, se a variável `WorkflowSession` está sendo usado para modificar o repositório e não salvar explicitamente a sessão - o fluxo de trabalho salvará a sessão quando ela for concluída.
* `Session.Save` não deve ser chamado de dentro de uma etapa do fluxo de trabalho:

   * é recomendável adaptar a sessão jcr do fluxo de trabalho; em seguida, `save` não é necessário, pois o mecanismo de workflow salva a sessão automaticamente após a conclusão da execução do workflow.
   * não é recomendável que uma etapa do processo crie sua própria sessão jcr.

* Ao eliminar salvamentos desnecessários, você pode reduzir a sobrecarga e, assim, tornar os workflows mais eficientes.

>[!CAUTION]
>
>Se, apesar das recomendações aqui, você criar sua própria sessão jcr, ela deverá ser salva.

### Minimizar o número/escopo de iniciadores {#minimize-the-number-scope-of-launchers}

Há um ouvinte responsável por todos os [iniciadores de fluxo de trabalho](/help/sites-administering/workflows-starting.md#workflows-launchers) que estão registrados:

* Ele ouvirá as alterações em todos os caminhos especificados nas propriedades de recurso de curinga dos outros inicializadores.
* Quando um evento é despachado, o mecanismo de fluxo de trabalho avaliará cada iniciador para determinar se ele deve ser executado.

Criar muitos inicializadores fará com que o processo de avaliação seja executado mais lentamente.

Criar um caminho de recurso de curinga na raiz do repositório em um único iniciador faria com que o mecanismo de fluxo de trabalho ouvisse e avaliasse a criação/modificação de eventos em cada nó no repositório. Por isso, é recomendável criar apenas os iniciadores necessários e tornar o caminho de recurso de curinga o mais específico possível.

Devido ao impacto desses inicializadores no comportamento do fluxo de trabalho, também pode ser útil desativar os inicializadores predefinidos que não estão em uso.

### Aprimoramentos de configuração para iniciadores {#configuration-enhancements-for-launchers}

O personalizado [configuração do inicializador](/help/sites-administering/workflows-starting.md#workflows-launchers) O foi aprimorado para oferecer suporte aos seguintes itens:

* Ter várias condições &quot;AND&quot; juntas.
* Têm condições OR em uma única condição.
* Desabilitar/habilitar inicializadores com base no fato de um sinalizador de recurso estar habilitado ou desabilitado.
* Suporte a regex nas condições do iniciador.

### Não iniciar workflows a partir de outros workflows {#do-not-start-workflows-from-other-workflows}

Os workflows podem transportar uma quantidade significativa de sobrecarga, tanto em termos de objetos criados na memória quanto de nós rastreados no repositório. Por esse motivo, é melhor ter um workflow fazendo seu processamento dentro de si mesmo do que iniciar workflows adicionais.

Um exemplo disso seria um fluxo de trabalho que implementa um processo de negócios em um conjunto de conteúdo e, em seguida, ativa esse conteúdo. É melhor criar um processo de fluxo de trabalho personalizado que ative cada um desses nós, em vez de iniciar um **Ativar conteúdo** para cada um dos nós de conteúdo que precisam ser publicados. Essa abordagem exigirá trabalho de desenvolvimento adicional, mas é mais eficiente ao ser executada do que iniciar uma instância de fluxo de trabalho separada para cada ativação.

Outro exemplo seria um fluxo de trabalho que processa vários nós, cria um pacote de fluxo de trabalho e ativa esse pacote. Em vez de criar o pacote e iniciar um fluxo de trabalho separado com o pacote como a carga, você pode alterar a carga do fluxo de trabalho na etapa que cria o pacote e chamar a etapa para ativar o pacote no mesmo modelo de fluxo de trabalho.

### Handler avançado {#handler-advance}

Ao criar um modelo de fluxo de trabalho, você tem a opção de ativar o avanço do manipulador nas etapas do fluxo de trabalho. Como alternativa, você pode adicionar o código à etapa do fluxo de trabalho para determinar qual etapa deve ser executada em seguida e, em seguida, executá-la.

É recomendável usar o avanço do manipulador, pois ele oferece melhor desempenho.

### Estágios do fluxo de trabalho {#workflow-stages}

Você pode definir [estágios do fluxo de trabalho](/help/sites-developing/workflows.md#workflow-stages), em seguida, atribua tarefas/etapas a um estágio específico do fluxo de trabalho.

Essas informações são usadas para exibir o progresso de um workflow quando você clica no ícone [**Informações do fluxo de trabalho** de um item de trabalho da **Caixa de entrada**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). Os modelos de fluxo de trabalho existentes podem ser editados para adicionar estágios.

### Etapa do processo de ativação da página {#activate-page-process-step}

A variável **Ativar processo de página** Essa etapa ativará as páginas para você, mas não localizará automaticamente nenhum ativo DAM referenciado e os ativará também.

Isso é algo para ter em mente se você planeja usar essa etapa como parte de um modelo de fluxo de trabalho.

### Considerações sobre atualização {#upgrade-considerations}

Ao atualizar sua instância:

* verifique se foi feito backup de todos os modelos de fluxo de trabalho personalizados antes de atualizar uma instância.
* confirme se nenhum dos workflows personalizados está armazenado no [localização](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Consulte também [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Ferramentas do sistema {#system-tools}

Há muitas ferramentas de sistema disponíveis para ajudar no monitoramento, manutenção e solução de problemas de workflows. Todos os URLs de exemplo abaixo usam `localhost:4502`, mas deve estar disponível em qualquer instância de autor ( `<hostname>:<port>`).

### Console de manuseio de trabalhos do Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

O console Manuseio de trabalhos do Sling mostrará:

* Estatísticas do estado dos trabalhos no sistema desde a última reinicialização.
* Ele também mostrará as configurações para todas as filas de trabalhos e fornecerá um atalho para editá-las no gerenciador de configurações.

### Ferramenta Relatório de fluxo de trabalho {#workflow-report-tool}

A ferramenta de relatório de fluxo de trabalho está sendo removida na versão 6.3 para evitar a degradação do desempenho.

### MBean de operações de manutenção do workflow {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

O MBean de manutenção do workflow expõe várias rotinas de manutenção úteis, como limpeza de workflows concluídos e recuperação de estatísticas de workflow.

## Informações adicionais {#further-information}

Para obter mais informações, consulte:

* [Trabalhar com fluxos de trabalho](/help/sites-authoring/workflows.md)
* [Administração de fluxos de trabalho](/help/sites-administering/workflows.md)
* [Desenvolvimento e extensão de workflows](/help/sites-developing/workflows.md)
* [Otimização do desempenho](/help/sites-deploying/configuring-performance.md)
