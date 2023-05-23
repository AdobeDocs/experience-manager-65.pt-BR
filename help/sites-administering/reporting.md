---
title: Relatório
seo-title: Reporting
description: Saiba como trabalhar com relatórios no AEM.
seo-description: Learn how to work with Reporting in AEM.
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 5%

---

# Relatório {#reporting}

Para ajudar você a monitorar e analisar o estado da sua instância, o AEM fornece uma seleção de relatórios padrão, que podem ser configurados para seus requisitos individuais:

* [Relatório do componente](#component-report)
* [Uso do disco](#disk-usage)
* [Verificação de integridade](#health-check)
* [Relatório de atividades de página](#page-activity-report)
* [Relatório de conteúdo gerado pelo usuário](#user-generated-content-report)
* [Relatório do usuário](#user-report)
* [Relatório de instâncias do fluxo de trabalho](#workflow-instance-report)
* [Relatório de fluxo de trabalho](#workflow-report)

>[!NOTE]
>
>Esses relatórios só estão disponíveis na interface clássica. Para obter o monitoramento e os relatórios do sistema na interface moderna do, consulte a [Painel de operações.](/help/sites-administering/operations-dashboard.md)

Todos os relatórios podem ser acessados no **Ferramentas** console. Selecionar **Relatórios** no painel à esquerda, clique duas vezes no relatório desejado no painel à direita para abri-lo para exibição e/ou configuração.

Novas instâncias de um relatório também podem ser criadas no **Ferramentas** console. Selecionar **Relatórios** no painel à esquerda, e **Novo...** na barra de ferramentas. Definir um **Título** e **Nome**, selecione o tipo de relatório necessário e clique em **Criar**. A nova instância do relatório aparecerá na lista. Clique duas vezes para abrir, em seguida, arraste um componente do sidekick para criar a primeira coluna e iniciar a definição do relatório.

>[!NOTE]
>
>Além dos relatórios padrão do AEM que estão disponíveis imediatamente, você pode [desenvolver seus próprios relatórios (completamente novos)](/help/sites-developing/dev-reports.md).

## Noções básicas da personalização de relatórios {#the-basics-of-report-customization}

Há vários formatos de relatórios disponíveis. Os relatórios a seguir usam colunas que podem ser personalizadas conforme detalhado nas seções a seguir:

* [Relatório do componente](#component-report)
* [Relatório de atividades de página](#page-activity-report)
* [Relatório de conteúdo gerado pelo usuário](#user-generated-content-report)
* [Relatório do usuário](#user-report)
* [Relatório de instâncias do fluxo de trabalho](#workflow-instance-report)

>[!NOTE]
>
>Os seguintes relatórios têm seu próprio formato e personalização:
>
>
>* [Verificação de integridade](#health-check) O usa campos de seleção para especificar os dados que você deseja relatar.
>* [Uso do disco](#disk-usage) O usa links para detalhar a estrutura do repositório.
>* [Relatório de fluxo de trabalho](/help/sites-administering/reporting.md#workflow-report) fornece uma visão geral dos workflows em execução na sua instância.
>
>Portanto, os procedimentos a seguir para a configuração da coluna não são apropriados. Consulte as descrições de relatórios individuais para obter seus detalhes.

### Seleção e posicionamento das colunas de dados {#selecting-and-positioning-the-data-columns}

As colunas podem ser adicionadas, reposicionadas ou removidas de qualquer um dos relatórios, seja padrão ou personalizado.

A variável **Componentes** A guia do sidekick (disponível na página de relatório) lista todas as categorias de dados que podem ser selecionadas como colunas.

Para alterar a seleção de dados:

* para adicionar uma nova coluna, arraste o componente desejado do sidekick e solte na posição desejada

   * um tique verde indicará quando a posição é válida e um par de setas indicará exatamente onde ela será colocada
   * um símbolo vermelho de não-navegação indicará quando a posição for inválida

* para mover uma coluna, clique no cabeçalho, mantenha pressionada e arraste para a nova posição
* para remover uma coluna, clique no título da coluna, mantenha pressionada e arraste até a área do cabeçalho do relatório (um símbolo de menos vermelho indicará que a posição não é válida); solte o botão do mouse e a caixa de diálogo Excluir componente(s) solicitará confirmação de que você realmente deseja excluir a coluna.

### Menu Suspenso de Coluna {#column-drop-down-menu}

Cada coluna no relatório tem um menu suspenso. Isso se torna visível quando o cursor do mouse se move sobre a célula de título da coluna.

Uma cabeça de seta aparecerá na extremidade direita da célula de título (não deve ser confundida com a cabeça de seta imediatamente à direita do texto de título que indica a [mecanismo de classificação atual](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

As opções disponíveis no menu dependerão da configuração da coluna (conforme feito durante o desenvolvimento do projeto). Todas as opções inválidas serão esmaecidas.

### Classificação dos dados {#sorting-the-data}

Os dados podem ser classificados de acordo com uma coluna específica por:

* clicar no cabeçalho de coluna apropriado; a classificação alternará entre crescente e decrescente, indicado por uma seta ao lado do texto do título
* use o [menu suspenso da coluna](#column-drop-down-menu) para selecionar especificamente **Ordenar por ordem crescente** ou **Ordenar por ordem decrescente**; novamente, isso será indicado por uma seta imediatamente ao lado do texto do título

### Gráfico de Grupos e Dados Atuais {#groups-and-the-current-data-chart}

Nas colunas apropriadas, você pode selecionar **Agrupar por esta coluna** do [menu suspenso da coluna](#column-drop-down-menu). Isso agrupará os dados de acordo com cada valor distinto dentro dessa coluna. É possível selecionar mais de uma coluna a ser agrupada. A opção estará esmaecida quando os dados na coluna forem inadequados; ou seja, cada entrada é distinta e exclusiva para que nenhum grupo possa ser formado, por exemplo, a coluna ID do usuário do relatório do usuário.

Depois que pelo menos uma coluna tiver sido agrupada, um gráfico de pizza de **Dados atuais** serão geradas, com base nesse agrupamento. Se várias colunas forem agrupadas, isso também será indicado no gráfico.

![reportuser](assets/reportuser.png)

Mover o cursor sobre o gráfico de pizza mostrará o valor agregado do segmento apropriado. Usa a agregação definida no momento para a coluna; por exemplo, count, minimum, average, entre outros.

### Filtros e agregações {#filters-and-aggregates}

Nas colunas apropriadas, você também pode configurar **Configurações do filtro** e/ou **Agregados** do [menu suspenso da coluna](#column-drop-down-menu).

#### Filtros {#filters}

As Configurações de filtro permitem especificar os critérios para as entradas a serem exibidas. Os operadores disponíveis são:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Para definir um filtro:

1. Selecione o operador desejado na lista suspensa.
1. Digite o texto a ser filtrado.
1. Clique em **Aplicar**.

Para desativar o filtro:

1. Remova o texto do filtro.
1. Clique em **Aplicar**.

#### Agregados {#aggregates}

Você também pode selecionar um método de agregação (que pode variar dependendo da coluna selecionada):

![reportaggregate](assets/reportaggregate.png)

### Propriedades da coluna {#column-properties}

Essa opção só estará disponível quando a variável [Coluna genérica](#generic-column) foi usada na [Relatório do usuário](#user-report).

### Dados históricos {#historic-data}

Um gráfico da mudança em seus dados ao longo do tempo pode ser visto em **Dados históricos**. Isso é derivado de instantâneos tirados em intervalos regulares.

Os dados são:

* Coletada por, se disponível, a primeira coluna classificada; caso contrário, a primeira coluna (não agrupada)
* Agrupado pela coluna apropriada

O relatório pode ser gerado:

1. Definir **Agrupamento** na coluna obrigatória.
1. **Editar** a configuração para definir a frequência com que os instantâneos devem ser feitos, por hora ou por dia.
1. **Concluir...** a definição para iniciar a coleta de instantâneos.

   O botão deslizante vermelho/verde na parte superior esquerda indica quando os instantâneos estão sendo coletados.

O gráfico resultante é mostrado na parte inferior direita:

![reporttrends](assets/reporttrends.png)

Depois que a coleta de dados tiver começado, você poderá selecionar:

* **Período**

   Você pode selecionar datas de e até para os dados do relatório a serem mostrados.

* **Intervalo**

   Mês, Semana, Dia, Hora podem ser selecionados para a escala e agregação do relatório.

   Por exemplo, se os instantâneos diários estiverem disponíveis para fevereiro de 2011:

   * Se o intervalo estiver definido como `Day`, cada instantâneo é mostrado como um valor único no gráfico.
   * Se o intervalo estiver definido como `Month`, todos os snapshots de fevereiro são agregados em um único valor (exibido como um único &quot;ponto&quot; no gráfico).

Selecione suas necessidades e clique em **Ir** para aplicá-los ao relatório. Para atualizar a exibição depois que outros instantâneos tiverem sido criados, clique em **Ir** novamente.

![chlimage_1-43](assets/chlimage_1-43.png)

Quando os instantâneos estiverem sendo coletados, você poderá:

* Uso **Concluir...** novamente para reinicializar a coleção.

   **Concluir** &quot;congela&quot; a estrutura do relatório (ou seja, as colunas atribuídas ao relatório e que são agrupadas, classificadas, filtradas etc.) e começa a tirar instantâneos.

* Abra o **Editar** caixa de diálogo para selecionar **Sem instantâneos de dados** para encerrar a coleta até que seja necessário.

   **Editar** apenas ativa ou desativa a captura de instantâneos. Se tirar instantâneos estiver ativado novamente, ele usa o estado do relatório quando foi concluído pela última vez para tirar mais instantâneos.

>[!NOTE]
>
>Os instantâneos são armazenados em `/var/reports/...` onde o restante do caminho reflete o caminho do respectivo relatório e ID criada quando o relatório foi concluído.
>
>
>Os snapshots antigos podem ser removidos manualmente, se você tiver certeza de que não precisa mais dessas instâncias.

>[!NOTE]
>
>Os relatórios pré-configurados não exigem alto desempenho, mas ainda é recomendável usar snapshots diários em um ambiente de produção. Se possível, execute esses instantâneos diários em um horário do dia quando não houver muita atividade no site; isso pode ser definido com o `Daily snapshots (repconf.hourofday)` parâmetro para **Configuração de relatório do Day CQ**; consulte [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes sobre como configurar isso.

#### Limites de exibição {#display-limits}

O relatório de dados históricos também pode mudar levemente de aparência devido a limites que podem ser definidos, de acordo com o número de resultados do período selecionado.

Cada linha horizontal é conhecida como uma série (e corresponde a uma entrada na legenda do gráfico), cada coluna vertical de pontos representa os instantâneos agregados.

![chlimage_1-44](assets/chlimage_1-44.png)

Para manter o gráfico limpo por longos períodos de tempo, há limites que podem ser definidos. Para os relatórios padrão, são:

* série horizontal - o padrão e o máximo do sistema são `9`

* instantâneos verticais agregados - o padrão é `35` (por série horizontal)

Assim, quando os limites (apropriados) são excedidos, o:

* os pontos não serão exibidos
* a legenda do gráfico de dados históricos pode mostrar um número de entradas diferente daquele do gráfico de dados atual

![chlimage_1-45](assets/chlimage_1-45.png)

Relatórios personalizados também podem mostrar a **Total** valor para todas as séries. Isso é mostrado como uma série (linha horizontal e entrada na legenda).

>[!NOTE]
>
>Para relatórios personalizados, os limites podem ser definidos de maneiras diferentes.

### Editar (Relatório) {#edit-report}

A variável **Editar** O botão abre a **Editar relatório** Caixa de diálogo

Este é um local onde o período para coleta de snapshots para [Dados históricos](#historic-data) está definido, mas várias outras configurações também podem ser definidas:

![reportdit](assets/reportedit.png)

* **Título**

   Você pode definir seu próprio título.

* **Descrição**

   Você pode definir sua própria descrição.

* **Caminho raiz** (*ativo somente para determinados relatórios*)

   Use essa opção para limitar o relatório a uma (sub) seção do repositório.

* **Processamento de relatório**

   * **atualização automática de dados**

      Os dados do relatório serão atualizados toda vez que você atualizar a definição de relatório.

   * **atualizar dados manualmente**

      Essa opção pode ser usada para evitar atrasos causados por operações automáticas de atualização quando há um grande volume de dados.

      Selecionar essa opção indica que os dados do relatório devem ser atualizados manualmente quando qualquer aspecto da configuração do relatório for alterado. Também significa que, assim que você alterar qualquer aspecto da configuração, a tabela de relatório ficará em branco.

      Quando essa opção estiver selecionada, a variável **[Carregar dados](#load-data)** será exibido (ao lado de **Editar** relatório). **Carregar dados** carregará os dados e atualizará os dados do relatório mostrados.

* **Instantâneos**
Você pode definir a frequência com que os instantâneos devem ser criados, diariamente, a cada hora ou não.

### Carregar dados {#load-data}

A variável **Carregar dados** O botão só fica visível quando **atualizar dados manualmente** foi selecionado de **[Editar](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

Clicando em **Carregar dados** recarregará os dados e atualizará o relatório que está sendo mostrado.

Selecionar para atualizar dados manualmente significa que:

1. Assim que você alterar a configuração do relatório, a tabela de dados do relatório ficará em branco.

   Por exemplo, se você alterar o mecanismo de classificação de uma coluna, os dados não serão exibidos.

1. Se quiser que os dados do relatório sejam mostrados novamente, clique em **Carregar dados** para recarregar os dados.

### Concluir (relatório) {#finish-report}

Quando você **Concluir** o relatório:

* A definição do relatório *a partir desse momento* serão usados para tirar instantâneos (depois, você pode continuar trabalhando em uma definição de relatório, pois ela é separada dos instantâneos).
* Todos os instantâneos existentes serão removidos.
* Novos instantâneos são coletados para o [Dados históricos](#historic-data).

Com essa caixa de diálogo, é possível definir ou atualizar seu próprio título e descrição para o relatório resultante.

![reportfinish](assets/reportfinish.png)

## Tipos de relatório {#report-types}

### Relatório do componente {#component-report}

O relatório de componentes fornece informações sobre como seu site usa os componentes.

[Colunas de informação](#selecting-and-positioning-the-data-columns) sobre:

* Autor
* Caminho do componente
* Tipo de componente
* Última modificação
* Página

Significa que você pode ver, por exemplo:

* Quais componentes são usados, onde.

   Útil, por exemplo, ao testar.

* Como as instâncias de um componente específico são distribuídas.

   Isso pode ser interessante se páginas específicas (ou seja, &quot;páginas pesadas&quot;) estiverem com problemas de desempenho.

* Identificar partes do site com alterações frequentes/menos frequentes.
* Veja como o conteúdo da página se desenvolve ao longo do tempo.

Todos os componentes estão incluídos, são padrão do produto e específicos do projeto. Usar o **Editar** caixa de diálogo o usuário também pode definir uma **Caminho raiz** que define o ponto de partida do relatório - todos os componentes nessa raiz são considerados para o relatório.

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### Uso do disco {#disk-usage}

O relatório de uso do disco mostra informações sobre os dados armazenados no repositório.

O relatório começa na raiz ( / ) do repositório; clicando em uma ramificação específica, é possível detalhar dentro do repositório (o caminho atual será refletido no título do relatório).

![reportdiskusage](assets/reportdiskusage.png)

### Verificação de integridade {#health-check}

Este relatório analisa o log de solicitação atual:

`<cq-installation-dir>/crx-quickstart/logs/request.log`
para ajudar a identificar as solicitações mais caras em um determinado período.

Para gerar o relatório, você pode especificar:

* **Período (horas)**

   O número de horas (passadas) a serem analisadas.

   Padrão: `24`

* **máx. Resultados**

   Número máximo de linhas de saída.

   Padrão: `50`

* **máx. Solicitações**

   Número máximo de solicitações a serem analisadas.

   Padrão: `-1` (todos)

* **Endereço de e-mail**

   Enviar resultados para um endereço de email.

   Opcional; Padrão: em branco

* **Executar diariamente às (hh:mm)**

   Especifique um horário para que o relatório seja executado automaticamente diariamente.

   Opcional; Padrão: em branco

![reportthealth](assets/reporthealth.png)

### Relatório de atividades de página {#page-activity-report}

O relatório de atividade da página lista as páginas e as ações nelas feitas.

[Colunas de informação](#selecting-and-positioning-the-data-columns) sobre:

* Página
* Hora
* Tipo
* Usuário

Isso significa que é possível monitorar:

* As modificações mais recentes.
* Autores trabalhando em páginas específicas.
* Páginas que não foram modificadas recentemente, portanto, podem estar precisando de ação.
* Páginas alteradas com mais/menos frequência.
* Usuários mais/menos ativos.

O relatório de atividade de página obtém todas as informações do log de auditoria. Por padrão, o caminho raiz é configurado para o log de auditoria em `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### Relatório de conteúdo gerado pelo usuário {#user-generated-content-report}

Este relatório fornece informações sobre o conteúdo gerado pelo usuário, sejam comentários, classificações ou fóruns.

[Colunas de informação](#selecting-and-positioning-the-data-columns) em:

* Data
* Endereço IP
* Página
* Referenciador
* Tipo
* Identificador do usuário

Permite:

* Veja quais páginas estão recebendo mais comentários.
* Obtenha uma visão geral de todos os comentários que os visitantes específicos do site estão deixando, talvez os problemas estejam relacionados.
* Avalie se o novo conteúdo está provocando comentários, monitorando quando os comentários estão sendo feitos em uma página.

![reportusercontent](assets/reportusercontent.png)

### Relatório do usuário {#user-report}

Este relatório fornece informações sobre todos os usuários que registraram uma conta e/ou perfil; isso pode incluir autores em sua organização e visitantes externos.

[Colunas de informação](#selecting-and-positioning-the-data-columns) (se disponível) sobre:

* Idade
* País
* Domínio
* E-mail
* Nome da família
* Sexo
* [Genérico](#generic-column)
* Nome
* Informações
* Interesse
* Idioma
* Hashcode NTLM
* ID de usuário

Permite:

* Veja a distribuição demográfica de seus usuários.
* Relatar campos personalizados adicionados aos perfis.

![reportusercanned](assets/reportusercanned.png)

#### Coluna genérica {#generic-column}

A variável **Genérico** coluna está disponível no Relatório de usuário para que você possa acessar informações personalizadas, normalmente no [perfis de usuário](/help/sites-administering/identity-management.md#profiles-and-user-accounts); por exemplo, [Cor favorita conforme detalhado em Adicionar campos à definição do perfil](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

A caixa de diálogo Generic column será aberta quando você:

* Arraste o componente Genérico do sidekick para o relatório.
* Selecione as Propriedades da Coluna para uma coluna Genérica existente.

![reportusrgenericMalcolm](assets/reportusrgenericcolm.png)

No **Definições** é possível definir:

* **Título**

   Seu próprio título para a coluna genérica.

* **Propriedade**

   O nome da propriedade conforme armazenado no repositório, geralmente no perfil do usuário.

* **Caminho**

   Normalmente, a propriedade é retirada do `profile`.

* **Tipo**

   Selecionar o tipo de campo de `String`, `Number`, `Integer`, `Date`.

* **Agregação Padrão**

   Isso define a agregação usada por padrão se a coluna for desagrupada em um relatório com pelo menos uma coluna agrupada. Selecione a agregação necessária em `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

   Por exemplo, *Contagem* para um `String` campo significa que o número de caracteres distintos `String` valores é exibido para a coluna no estado agregado.

No **Estendido** guia, também é possível definir as agregações e os filtros disponíveis:

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### Relatório de instâncias do fluxo de trabalho {#workflow-instance-report}

Isso fornece uma visão geral concisa, fornecendo informações sobre as instâncias individuais de workflows, em execução e concluídos.

[Colunas de informação](#selecting-and-positioning-the-data-columns) sobre:

* Concluído
* Duração
* Iniciador
* Modelo
* Carga
* Iniciado
* Status

Isso significa que é possível:

* Monitore a duração média dos workflows; se isso ocorrer regularmente, pode destacar problemas com o workflow.

![reportworkflowinstance](assets/reportworkflowintance.png)

### Relatório de fluxo de trabalho {#workflow-report}

Isso fornece estatísticas importantes sobre os workflows em execução na sua instância.

![reportworkflow](assets/reportworkflow.png)

## Uso de relatórios em um ambiente de publicação {#using-reports-in-a-publish-environment}

Depois de configurar os relatórios de acordo com seus requisitos específicos, você pode ativá-los para transferir a configuração para o ambiente de publicação.

>[!CAUTION]
>
>Se você quiser **Dados históricos** para o ambiente de publicação, então **Concluir** o relatório no ambiente do autor antes de ativar a página.

O relatório apropriado estará então acessível em

`/etc/reports`

Por exemplo, o relatório de Conteúdo gerado pelo usuário pode ser encontrado em:

`http://localhost:4503/etc/reports/ugcreport.html`

Agora, ele informará sobre os dados coletados do ambiente de publicação.

Como nenhuma configuração de relatório é permitida no ambiente de publicação, a variável **Editar** e **Concluir** botões não estão disponíveis. No entanto, é possível selecionar a variável **Período** e **Interval** para o **Dados históricos** relata se os snapshots estão sendo coletados.

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>O acesso a esses relatórios pode ser um problema de segurança; portanto, recomendamos que você configure o Dispatcher para que `/etc/reports` não está disponível para visitantes externos. Consulte a [Lista de verificação de segurança](security-checklist.md) para obter mais detalhes.

## Permissões necessárias para executar relatórios {#permissions-needed-for-running-reports}

As permissões necessárias dependem da ação:

* Os dados do relatório são basicamente coletados usando os privilégios do usuário atual.
* Os dados históricos são coletados usando os privilégios do usuário que concluiu o relatório.

Em uma instalação padrão do AEM, as seguintes permissões são predefinidas para os relatórios:

* **Relatório do usuário**

   `user administrators` - ler e gravar

* **Relatório de atividades de página**

   `contributors` - ler e gravar

* **Relatório do componente**

   `contributors` - ler e gravar

* **Relatório de conteúdo gerado pelo usuário**

   `contributors` - ler e gravar

* **Relatório de instâncias do fluxo de trabalho**

   `workflow-users` - ler e gravar

Todos os membros da `administrators` grupo têm os direitos necessários para criar novos relatórios.
