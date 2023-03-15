---
title: Relatório
seo-title: Reporting
description: Saiba como trabalhar com Relatórios no AEM.
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

* [Relatório de componentes](#component-report)
* [Uso do disco](#disk-usage)
* [Verificação de integridade](#health-check)
* [Relatório de atividades de página](#page-activity-report)
* [Relatório de conteúdo gerado pelo usuário](#user-generated-content-report)
* [Relatório do usuário](#user-report)
* [Relatório de instâncias do fluxo de trabalho](#workflow-instance-report)
* [Relatório de fluxo de trabalho](#workflow-report)

>[!NOTE]
>
>Esses relatórios só estão disponíveis na interface do usuário clássica. Para monitoramento e relatórios do sistema na interface do usuário moderna, consulte o [Painel de operações.](/help/sites-administering/operations-dashboard.md)

Todos os relatórios podem ser acessados na **Ferramentas** console. Selecionar **Relatórios** no painel esquerdo, clique duas vezes no relatório necessário no painel direito para abri-lo para visualização e/ou configuração.

Novas instâncias de um relatório também podem ser criadas na variável **Ferramentas** console. Selecionar **Relatórios** no painel esquerdo, em seguida **Novo...** na barra de ferramentas. Defina um **Título** e **Nome**, selecione o tipo de relatório necessário e clique em **Criar**. A nova instância do relatório será exibida na lista. Clique duas vezes para abrir e arraste um componente do sidekick para criar a primeira coluna e iniciar a definição do relatório.

>[!NOTE]
>
>Além dos relatórios de AEM padrão que estão disponíveis imediatamente, você pode [desenvolver seus próprios relatórios (completamente novos)](/help/sites-developing/dev-reports.md).

## Noções básicas da personalização de relatórios {#the-basics-of-report-customization}

Há vários formatos de relatórios disponíveis. Os relatórios a seguir usam colunas que podem ser personalizadas conforme detalhado nas seguintes seções:

* [Relatório de componentes](#component-report)
* [Relatório de atividades de página](#page-activity-report)
* [Relatório de conteúdo gerado pelo usuário](#user-generated-content-report)
* [Relatório do usuário](#user-report)
* [Relatório de instâncias do fluxo de trabalho](#workflow-instance-report)

>[!NOTE]
>
>Os relatórios a seguir têm seu próprio formato e personalização:
>
>
>* [Verificação de integridade](#health-check) O usa campos de seleção para especificar os dados nos quais deseja criar relatórios.
>* [Uso de disco](#disk-usage) O usa links para detalhar a estrutura do repositório.
>* [Relatório de workflow](/help/sites-administering/reporting.md#workflow-report) O fornece uma visão geral dos workflows em execução na instância.
>
>Portanto, os procedimentos a seguir para a configuração da coluna não são apropriados. Consulte as descrições dos relatórios individuais para obter seus detalhes.

### Seleção e posicionamento das colunas de dados {#selecting-and-positioning-the-data-columns}

As colunas podem ser adicionadas, reposicionadas ou removidas de qualquer relatório, padrão ou personalizado.

O **Componentes** a guia do sidekick (disponível na página do relatório) lista todas as categorias de dados que podem ser selecionados como colunas.

Para alterar a seleção de dados:

* para adicionar uma nova coluna, arraste o componente desejado do sidekick e solte na posição desejada

   * uma marca de verificação verde indica quando a posição é válida e um par de setas indicará exatamente onde será colocada
   * um símbolo vermelho sem movimento indicará quando a posição for inválida

* para mover uma coluna, clique no cabeçalho, segure e arraste para a nova posição
* para remover uma coluna, clique no título da coluna, arraste e solte na área do cabeçalho do relatório (um símbolo vermelho de menos indicará que a posição não é válida); solte o botão do mouse e a caixa de diálogo Excluir componentes solicitará a confirmação de que você realmente deseja excluir a coluna.

### Menu suspenso Coluna {#column-drop-down-menu}

Cada coluna no relatório tem um menu suspenso. Isso se torna visível quando o cursor do mouse se move sobre a célula do título da coluna.

Uma cabeça de seta aparecerá na extremidade direita da célula de título (não confundir com a cabeça de seta imediatamente à direita do texto do título que indica a [mecanismo de classificação atual](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

As opções disponíveis no menu dependerão da configuração da coluna (conforme feita durante o desenvolvimento do projeto), quaisquer opções inválidas serão esmaecidas.

### Classificação dos dados {#sorting-the-data}

Os dados podem ser classificados de acordo com uma coluna específica por:

* clicar no cabeçalho da coluna apropriado; a classificação alternará entre ascendente e descendente, indicado por uma cabeça de seta imediatamente ao lado do texto do título
* use o [menu suspenso da coluna](#column-drop-down-menu) para selecionar especificamente **Classificar crescente** ou **Classificar decrescente**; novamente, isso será indicado por uma seta imediatamente ao lado do texto do título

### Grupos e Gráfico de dados atuais {#groups-and-the-current-data-chart}

Em colunas apropriadas, você pode selecionar **Agrupar por esta coluna** do [menu suspenso da coluna](#column-drop-down-menu). Isso agrupará os dados de acordo com cada valor distinto dentro dessa coluna. É possível selecionar mais de uma coluna para ser agrupada. A opção ficará esmaecida quando os dados na coluna forem inadequados; ou seja, cada entrada é distinta e exclusiva para que nenhum grupo possa ser formado, por exemplo, a coluna ID de usuário do relatório de usuário.

Depois de pelo menos uma coluna ter sido agrupada, um gráfico de pizza **Dados atuais** será gerado, com base neste agrupamento. Se várias colunas forem agrupadas, isso também será indicado no gráfico.

![reportuser](assets/reportuser.png)

Mover o cursor sobre o gráfico de pizza mostrará o valor agregado do segmento apropriado. Usa a agregação atualmente definida para a coluna; por exemplo, contagem, mínimo, média, entre outras.

### Filtros e agregados {#filters-and-aggregates}

Em colunas apropriadas, você também pode configurar **Configurações de filtro** e/ou **Agregados** do [menu suspenso da coluna](#column-drop-down-menu).

#### Filtros {#filters}

As Configurações de filtro permitem que você especifique os critérios para as entradas a serem exibidas. Os operadores disponíveis são:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Para definir um filtro:

1. Selecione o operador desejado na lista suspensa.
1. Insira o texto a ser filtrado.
1. Clique em **Aplicar**.

Para desativar o filtro:

1. Remova o texto do filtro.
1. Clique em **Aplicar**.

#### Agregados {#aggregates}

Você também pode selecionar um método de agregação (eles podem variar dependendo da coluna selecionada):

![reportaggregate](assets/reportaggregate.png)

### Propriedades da coluna {#column-properties}

Essa opção só estará disponível quando a variável [Coluna genérica](#generic-column) foi usada no [Relatório do usuário](#user-report).

### Dados históricos {#historic-data}

Um gráfico da alteração nos dados ao longo do tempo pode ser visto em **Dados históricos**. Isso é derivado de instantâneos tirados em intervalos regulares.

Os dados são:

* Coletada por, se disponível, a primeira coluna classificada, caso contrário, a primeira coluna (não agrupada)
* Agrupado pela coluna apropriada

O relatório pode ser gerado:

1. Definir **Agrupamento** na coluna obrigatória.
1. **Editar** a configuração para definir a frequência com que os instantâneos devem ser feitos; por hora ou por dia.
1. **Concluir...** a definição para iniciar a coleção de instantâneos.

   O botão deslizante vermelho/verde na parte superior esquerda indica quando os instantâneos estão sendo coletados.

O gráfico resultante é mostrado na parte inferior direita:

![relatórios](assets/reporttrends.png)

Depois de iniciar a coleta de dados, você pode selecionar:

* **Período**

   É possível selecionar datas de e para os dados do relatório a serem exibidos.

* **Intervalo**

   Mês, Semana, Dia, Hora pode ser selecionado para a escala e agregação do relatório.

   Por exemplo, se os instantâneos diários estiverem disponíveis para fevereiro de 2011:

   * Se o intervalo estiver definido como `Day`, cada instantâneo é mostrado como um único valor no gráfico.
   * Se o intervalo estiver definido como `Month`, todos os instantâneos de fevereiro são agregados em um único valor (exibido como um único &quot;ponto&quot; no gráfico).

Selecione seus requisitos e clique em **Ir** para aplicá-las ao relatório. Para atualizar a exibição depois que novos instantâneos forem feitos, clique em **Ir** novamente.

![chlimage_1-43](assets/chlimage_1-43.png)

Quando os instantâneos estão sendo coletados, você pode:

* Use **Concluir...** novamente para reinicializar a coleção.

   **Concluir** &quot;congela&quot; a estrutura do relatório (ou seja, as colunas atribuídas ao relatório e que são agrupadas, classificadas, filtradas, etc.) e começa a tirar instantâneos.

* Abra o **Editar** caixa de diálogo a ser selecionada **Nenhum instantâneo de dados** terminar a coleta até ser necessário.

   **Editar** apenas ativa ou desativa a captura de instantâneos. Se os instantâneos forem ativados novamente, ele usará o estado do relatório quando foi concluído pela última vez para obter mais instantâneos.

>[!NOTE]
>
>Os instantâneos são armazenados em `/var/reports/...` onde o restante do caminho reflete o caminho do respectivo relatório e ID criada quando o relatório foi concluído.
>
>
>Instantâneos antigos podem ser removidos manualmente, se você tiver certeza absoluta de que não precisa mais dessas instâncias.

>[!NOTE]
>
>Os relatórios pré-configurados não exigem muito desempenho, mas ainda é recomendável usar instantâneos diários em um ambiente de produção. Se possível, execute esses instantâneos diários em um momento do dia em que não há muita atividade em seu site; isso pode ser definido com a variável `Daily snapshots (repconf.hourofday)` parâmetro para **Configuração de relatórios do Day CQ**; see [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes sobre como configurar isso.

#### Limites de exibição {#display-limits}

O relatório de dados históricos também pode mudar um pouco na aparência devido a limites que podem ser definidos, de acordo com o número de resultados do período selecionado.

Cada linha horizontal é conhecida como uma série (e corresponde a uma entrada na legenda do gráfico), cada coluna vertical de pontos representa os instantâneos agregados.

![chlimage_1-44](assets/chlimage_1-44.png)

Para manter o gráfico limpo por períodos de tempo maiores, há limites que podem ser definidos. Para os relatórios padrão, são:

* série horizontal - o padrão e o máximo do sistema são `9`

* instantâneos agregados verticais - o padrão é `35` (por série horizontal)

Assim, quando os limites (adequados) forem excedidos, o:

* os pontos não serão exibidos
* a legenda do gráfico de dados históricos pode mostrar um número diferente de entradas em relação ao do gráfico de dados atual

![chlimage_1-45](assets/chlimage_1-45.png)

Os relatórios personalizados também podem mostrar a variável **Total** para todas as séries. Isso é mostrado como uma série (linha horizontal e entrada na legenda).

>[!NOTE]
>
>Para relatórios personalizados, os limites podem ser definidos de forma diferente.

### Editar (Relatório) {#edit-report}

O **Editar** botão abre **Editar relatório** Caixa de diálogo.

Este é um local onde o período para coleta de instantâneos para [Dados históricos](#historic-data) está definida, mas várias outras configurações também podem ser definidas:

![reportedit](assets/reportedit.png)

* **Título**

   Você pode definir seu próprio título.

* **Descrição**

   Você pode definir sua própria descrição.

* **Caminho raiz** (*ativo apenas para determinados relatórios*)

   Use isso para limitar o relatório a uma (sub) seção do repositório.

* **Processamento de relatório**

   * **atualização automática de dados**

      Os dados do relatório serão atualizados toda vez que você atualizar a definição do relatório.

   * **atualizar dados manualmente**

      Essa opção pode ser usada para evitar atrasos causados por operações automáticas de atualização quando há um grande volume de dados.

      Selecionar isso indica que os dados do relatório devem ser atualizados manualmente quando qualquer aspecto da configuração do relatório for alterado. Isso também significa que, assim que você alterar qualquer aspecto da configuração, a tabela do relatório ficará em branco.

      Quando isso é selecionado, a variável **[Carregar dados](#load-data)** será exibido (ao lado de **Editar** do relatório). **Carregar dados** carregará os dados e atualizará os dados do relatório mostrados.

* **Instantâneos**
Você pode definir a frequência com que os instantâneos devem ser feitos; diariamente, a cada hora ou não.

### Carregar dados {#load-data}

O **Carregar dados** só é visível quando **atualizar dados manualmente** foi selecionado de **[Editar](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

Clicando em **Carregar dados** O recarregará os dados e atualizará o relatório que está sendo exibido.

Selecionar para atualizar dados manualmente significa que:

1. Assim que você alterar a configuração do relatório, a tabela de dados do relatório ficará em branco.

   Por exemplo, se você alterar o mecanismo de classificação de uma coluna, os dados não serão exibidos.

1. Se quiser que os dados do relatório sejam exibidos novamente, clique em **Carregar dados** para recarregar os dados.

### Finish (relatório) {#finish-report}

Quando você **Concluir** o relatório:

* A definição do relatório *a partir desse momento* será usada para tirar os instantâneos (depois você pode continuar trabalhando em uma definição de relatório, já que é separada dos instantâneos).
* Quaisquer instantâneos existentes serão removidos.
* Novos instantâneos são coletados para o [Dados históricos](#historic-data).

Com essa caixa de diálogo, você pode definir ou atualizar seu próprio título e descrição para o relatório resultante.

![relatório](assets/reportfinish.png)

## Tipos de relatórios {#report-types}

### Relatório de componentes {#component-report}

O relatório de componente fornece informações sobre como o site usa os componentes do .

[Colunas de informações](#selecting-and-positioning-the-data-columns) sobre:

* Autor
* Caminho do componente
* Tipo de componente
* Última modificação
* Página

Isso significa que você pode ver, por exemplo:

* Quais componentes são usados onde.

   Útil, por exemplo, ao testar.

* Como as instâncias de um componente específico são distribuídas.

   Isso pode ser interessante se páginas específicas (ou seja, &quot;páginas pesadas&quot;) apresentam problemas de desempenho.

* Identificar partes do site com alterações frequentes/menos frequentes.
* Veja como o conteúdo da página se desenvolve ao longo do tempo.

Todos os componentes estão incluídos, padrão do produto e específico do projeto. Usar o **Editar** o usuário também pode definir uma **Caminho raiz** que define o ponto de partida do relatório - todos os componentes dessa raiz são considerados para o relatório.

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### Uso do disco {#disk-usage}

O relatório de uso do disco mostra informações sobre os dados armazenados em seu repositório.

O relatório é iniciado na raiz ( / ) do repositório; ao clicar em uma ramificação específica, você pode fazer drill-down dentro do repositório (o caminho atual será refletido no título do relatório).

![reportdiskusage](assets/reportdiskusage.png)

### Verificação de integridade {#health-check}

Este relatório analisa o log de solicitação atual:

`<cq-installation-dir>/crx-quickstart/logs/request.log`
para ajudá-lo a identificar as solicitações mais caras em um determinado período.

Para gerar o relatório, você pode especificar:

* **Período (horas)**

   O número de horas (passadas) a serem analisadas.

   Padrão: `24`

* **max. Resultados**

   Número máximo de linhas de saída.

   Padrão: `50`

* **max. Solicitações**

   Número máximo de solicitações a serem analisadas.

   Padrão: `-1` (todos)

* **Endereço de e-mail**

   Envie os resultados para um endereço de email.

   Facultativo; Padrão: blank

* **Executar diariamente às (hh:mm)**

   Especifique um horário para a execução automática do relatório diariamente.

   Facultativo; Padrão: blank

![repórter](assets/reporthealth.png)

### Relatório de atividades de página {#page-activity-report}

O relatório de atividade da página lista as páginas e as ações realizadas neles.

[Colunas de informações](#selecting-and-positioning-the-data-columns) sobre:

* Página
* Hora
* Tipo
* Usuário

Isso significa que você pode monitorar:

* As modificações mais recentes.
* Autores que trabalham em páginas específicas.
* As páginas que não foram modificadas recentemente, por isso podem precisar de ação.
* Páginas que são alteradas com mais/menos frequência.
* Usuários mais / menos ativos.

O relatório de atividade da página pega todas as informações do log de auditoria. Por padrão, o caminho raiz é configurado para o log de auditoria em `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### Relatório de conteúdo gerado pelo usuário {#user-generated-content-report}

Este relatório fornece informações sobre o conteúdo gerado pelo usuário; sejam comentários, classificações ou fóruns.

[Colunas de informações](#selecting-and-positioning-the-data-columns) em:

* Data
* Endereço IP
* Página
* Referenciador
* Tipo
* Identificador do usuário

Permitir:

* Veja quais páginas estão recebendo mais comentários.
* Obtenha uma visão geral de todos os comentários que visitantes específicos do site estão deixando, talvez os problemas estejam relacionados.
* Verifique se o novo conteúdo está provocando comentários monitorando quando comentários são feitos em uma página.

![reportusercontent](assets/reportusercontent.png)

### Relatório do usuário {#user-report}

Este relatório fornece informações sobre todos os usuários que registraram uma conta e/ou perfil; isso pode incluir autores em sua organização e visitantes externos.

[Colunas de informações](#selecting-and-positioning-the-data-columns) (se disponível) sobre:

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

Permitir:

* Veja a distribuição demográfica de seus usuários.
* Relate os campos personalizados que você adicionou aos perfis.

![reportusercanned](assets/reportusercanned.png)

#### Coluna Genérica {#generic-column}

O **Genérico** está disponível no Relatório do usuário para que você possa acessar informações personalizadas, normalmente no [perfis de usuário](/help/sites-administering/identity-management.md#profiles-and-user-accounts); por exemplo, [Cor favorita conforme detalhado em Adicionar campos à definição do perfil](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

A caixa de diálogo da coluna Genérica será aberta quando você:

* Arraste o componente Genérico do sidekick para o relatório.
* Selecione as Propriedades da coluna para uma coluna Genérica existente.

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

No **Definições** é possível definir:

* **Título**

   Seu próprio título para a coluna genérica.

* **Propriedade**

   O nome da propriedade como armazenado no repositório, normalmente no perfil do usuário.

* **Caminho**

   Geralmente, a propriedade é retirada do `profile`.

* **Tipo**

   Selecione o tipo de campo de `String`, `Number`, `Integer`, `Date`.

* **Agregação padrão**

   Isso define a agregação usada por padrão se a coluna for desagrupada em um relatório com pelo menos uma coluna agrupada. Selecione a agregação necessária em `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

   Por exemplo, *Contagem* para um `String` campo significa que o número de `String` valores são exibidos para a coluna no estado agregado.

No **Estendido** também é possível definir as agregações e filtros disponíveis:

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### Relatório de instâncias do fluxo de trabalho {#workflow-instance-report}

Isso oferece uma visão geral concisa, fornecendo informações sobre as instâncias individuais de workflows, em execução e concluídos.

[Colunas de informações](#selecting-and-positioning-the-data-columns) sobre:

* Concluído
* Duração
* Iniciador
* Modelo
* Carga
* Iniciado
* Status

Isso significa que você pode:

* Monitorar a duração média dos fluxos de trabalho; se isso acontecer regularmente, é possível destacar problemas com o workflow .

![reportworkflowintance](assets/reportworkflowintance.png)

### Relatório de fluxo de trabalho {#workflow-report}

Isso fornece estatísticas importantes sobre os workflows em execução na sua instância.

![reportworkflow](assets/reportworkflow.png)

## Usar relatórios em um ambiente de publicação {#using-reports-in-a-publish-environment}

Depois de configurar os relatórios para seus requisitos específicos, você pode ativá-los para transferir a configuração para o ambiente de publicação.

>[!CAUTION]
>
>Se desejar **Dados históricos** para o ambiente de publicação, em seguida **Concluir** o relatório sobre o ambiente de criação antes de ativar a página.

O relatório adequado será então acessível em

`/etc/reports`

Por exemplo, o relatório Conteúdo gerado pelo usuário pode ser encontrado em:

`http://localhost:4503/etc/reports/ugcreport.html`

Isso agora relatará os dados coletados do ambiente de publicação.

Como nenhuma configuração de relatório é permitida no ambiente de publicação, a variável **Editar** e **Concluir** botões não estão disponíveis. No entanto, é possível selecionar a variável **Período** e **Intervalo** para **Dados históricos** informa se os instantâneos estão sendo coletados.

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>O acesso a estes relatórios pode constituir uma questão de segurança; portanto, recomendamos que você configure o Dispatcher para que `/etc/reports` não está disponível para visitantes externos. Consulte a [Lista de verificação de segurança](security-checklist.md) para obter mais detalhes.

## Permissões necessárias para executar relatórios {#permissions-needed-for-running-reports}

As permissões necessárias dependem da ação:

* Os dados do relatório são basicamente coletados usando os privilégios do usuário atual.
* Os dados históricos são coletados usando os privilégios do usuário que concluiu o relatório.

Em uma instalação padrão do AEM, as seguintes permissões são predefinidas para os relatórios:

* **Relatório do usuário**

   `user administrators` - ler e escrever

* **Relatório de atividades de página**

   `contributors` - ler e escrever

* **Relatório de componentes**

   `contributors` - ler e escrever

* **Relatório de conteúdo gerado pelo usuário**

   `contributors` - ler e escrever

* **Relatório de instâncias do fluxo de trabalho**

   `workflow-users` - ler e escrever

Todos os membros da `administrators` têm os direitos necessários para criar novos relatórios.
