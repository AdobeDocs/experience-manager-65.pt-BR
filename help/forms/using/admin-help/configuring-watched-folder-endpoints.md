---
title: Configurando pontos de extremidade de pasta monitorada
description: Saiba como configurar os pontos de extremidade de pastas monitoradas. Se um documento for colocado na pasta monitorada, uma operação de serviço configurada será chamada e manipulará o arquivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '7174'
ht-degree: 0%

---

# Configurando pontos de extremidade de pasta monitorada {#configuring-watched-folder-endpoints}

Um administrador pode configurar uma pasta de rede, conhecida como *pasta monitorada*, para que, quando um usuário colocar um arquivo (como um arquivo PDF) na pasta monitorada, uma operação de serviço configurada seja chamada e manipule o arquivo. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado em uma pasta de saída especificada.

## Configurar o serviço Pasta monitorada {#configuring-the-watched-folder-service}

Antes de configurar um endpoint de pasta monitorada, configure o serviço Pasta monitorada. Os parâmetros de configuração do serviço Pasta monitorada têm duas finalidades:

* Para configurar atributos que são comuns para todos os endpoints de pasta monitorados
* Para fornecer valores padrão para todos os pontos de extremidade da pasta monitorada

Depois de configurar o serviço Pasta monitorada, você adiciona um terminal Pasta monitorada para o serviço de destino. Ao adicionar o endpoint, você define valores, como o nome do serviço e o nome da operação a serem chamados quando arquivos ou pastas forem colocados na pasta de entrada do serviço Pasta monitorada configurado. Para obter detalhes sobre como configurar o serviço Pasta monitorada, consulte [Configurações do serviço de pasta monitorada](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Criação de uma pasta monitorada {#creating-a-watched-folder}

Você pode criar uma pasta monitorada das duas seguintes maneiras:

* Ao definir as configurações para um endpoint de pasta monitorada, digite o caminho completo para o diretório principal na caixa Caminho e anexe o nome da pasta monitorada a ser criada, como mostrado neste exemplo:
  `  C:\MyPDFs\MyWatchedFolder`Como a pasta MyWatchedFolder ainda não existe, os formulários AEM tentam criá-la nesse local.

* Crie uma pasta no sistema de arquivos antes de configurar um endpoint de pasta monitorada e digite o caminho completo na caixa Caminho.

Em um ambiente em cluster, a pasta usada como uma pasta monitorada deve ser acessível, gravável e compartilhada no sistema de arquivos ou na rede. Nesse cenário, cada instância do servidor de aplicativos do cluster deve ter acesso à mesma pasta compartilhada.

No Windows, se o servidor de aplicativos estiver sendo executado como um serviço, ele deverá ser iniciado com acesso apropriado à pasta compartilhada de uma das seguintes maneiras:

* Configurar o serviço do servidor de aplicativos Fazer Logon como **parâmetro** para iniciar como um usuário específico com acesso apropriado à pasta monitorada compartilhada.
* Configure a opção Iniciar como Sistema Local do serviço do servidor de aplicativos para Permitir que o Serviço interaja com a área de trabalho. Esta opção requer que a pasta monitorada compartilhada seja acessível e gravável para todos.

## Encadeamento de pastas monitoradas {#chaining-together-watched-folders}

As pastas monitoradas podem ser encadeadas para que um documento de resultado de uma pasta monitorada seja o documento de entrada da próxima pasta monitorada. Cada pasta monitorada pode chamar um serviço diferente. Ao configurar pastas monitoradas dessa maneira, vários serviços podem ser chamados. Por exemplo, uma pasta monitorada poderia converter arquivos PDF para Adobe PostScript® e uma segunda pasta monitorada poderia converter os arquivos PostScript para o formato PDF/A. Para fazer isso, basta definir a variável *resultado* pasta da pasta monitorada definida pelo seu primeiro endpoint para apontar para a *entrada* pasta da pasta monitorada definida pelo segundo ponto de extremidade.

A saída da primeira conversão iria para \path\result. A entrada para a segunda conversão seria \path\result, e a saída da segunda conversão iria para \path\result\result (ou o diretório definido na caixa Pasta de resultados para a segunda conversão).

## Como os usuários interagem com as pastas monitoradas {#how-users-interact-with-watched-folders}

Para um endpoint de pasta monitorada, os usuários podem chamar copiando ou arrastando arquivos ou pastas de entrada de suas áreas de trabalho para uma pasta monitorada. Os arquivos serão processados na ordem em que chegarem.

Para endpoints de pasta monitorada, se o trabalho exigir apenas um arquivo de entrada, o usuário poderá copiar esse arquivo para a raiz da pasta monitorada.

Se o trabalho contiver mais de um arquivo de entrada, o usuário deverá criar uma pasta fora da hierarquia de pastas monitoradas que contenha todos os arquivos necessários. Essa nova pasta deve incluir os arquivos de entrada (e, opcionalmente, um arquivo DDX, se exigido pelo processo). Após a construção da pasta de trabalho, o usuário a copia para a pasta de entrada da pasta monitorada.

>[!NOTE]
>
>Verifique se o servidor de aplicativos excluiu o acesso aos arquivos da pasta monitorada. Se os formulários AEM não puderem excluir os arquivos da pasta de entrada após serem digitalizados, o processo associado será chamado indefinidamente.

## Saída da pasta monitorada {#watched-folder-output}

Quando a entrada é uma pasta e a saída consiste em vários arquivos, os formulários AEM criam uma pasta de saída com o mesmo nome da pasta de entrada e copiam os arquivos de saída nessa pasta. Quando a saída consiste em um mapa de documentos contendo um par de valores chave, como a saída de um processo de Saída, a chave é usada como o nome do arquivo de saída.

Os nomes de arquivo de saída que resultam de um processo de ponto de extremidade não podem conter caracteres diferentes de letras, números e um ponto final (.) antes da extensão do arquivo. Formulários AEM convertem outros caracteres em seus valores hexadecimais.

Os aplicativos clientes selecionam os documentos de resultado da pasta monitorada. Erros de processo são registrados na pasta de falha da pasta monitorada.

## Como a pasta monitorada funciona {#how-watched-folder-works}

O módulo Pasta monitorada contém estes serviços:

* Serviço de pasta monitorada
* provider.file_scan_service
* provider.file_write_results_service

Além dos serviços listados acima, a Pasta monitorada também depende de outros serviços, incluindo o serviço Agendador para agendar os trabalhos e o serviço Gerenciador de trabalhos para oferecer suporte à invocação assíncrona de serviços de destino.

### Como o Watched Folder processa uma solicitação de chamada {#how-watched-folder-processes-an-invocation-request}

O serviço Pasta monitorada lida com a criação, atualização e exclusão dos pontos de extremidade. Depois que o administrador cria os endpoints, eles são agendados para serem acionados pelo serviço Scheduler com base no intervalo de repetição ou expressão CRON especificada.

Este diagrama ilustra como o Watched Folder processa uma solicitação de chamada.

![en_watchedfolder](assets/en_watchedfolder.png)

O processo de chamar um serviço usando pastas monitoradas é o seguinte:

1. Um aplicativo cliente coloca arquivos ou pastas na pasta de entrada da pasta monitorada.
1. Quando o intervalo de verificação do job ocorre, o serviço Scheduler chama o provider.file_scan_service para processar os arquivos ou pastas na pasta de entrada.
1. O provider.file_scan_service executa estas tarefas:


   * Examina a pasta de entrada em busca de arquivos ou pastas que correspondam ao padrão de inclusão de arquivos e exclui arquivos ou pastas para o padrão de exclusão de arquivos especificado. Os arquivos ou pastas mais antigos são selecionados primeiro. Arquivos e pastas mais antigos que o tempo de espera também são coletados. Em uma varredura, o número de arquivos ou pastas processados se baseia no tamanho do lote. Para obter informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](configuring-watched-folder-endpoints.md#about-file-patterns). Para obter informações sobre como definir o tamanho do lote, consulte [Configurações do serviço de pasta monitorada](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Seleciona os arquivos ou pastas para processamento. Se os arquivos ou pastas não tiverem sido completamente baixados, eles serão selecionados na próxima verificação. Para garantir que as pastas sejam completamente baixadas, os administradores devem criar uma pasta com um nome usando o padrão de exclusão de arquivo. Depois que a pasta tiver todos os arquivos, ela deverá ser renomeada para o padrão especificado no padrão de arquivo de inclusão. Essa etapa garante que a pasta tenha todos os arquivos necessários para chamar o serviço. Para obter mais informações sobre como garantir que as pastas sejam completamente baixadas, consulte [Dicas e truques para pastas monitoradas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Move os arquivos ou pastas para a pasta de preparo depois de selecioná-los para processamento.
   * Converte os arquivos ou pastas na pasta de preparo para a entrada apropriada com base nos mapeamentos do parâmetro de entrada do ponto de extremidade. Para obter exemplos de mapeamentos de parâmetro de entrada, consulte [Dicas e truques para pastas monitoradas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. O serviço de destino configurado para o ponto de extremidade é chamado de forma síncrona ou assíncrona. O serviço de destino é chamado usando o nome de usuário e a senha configurados para o ponto de extremidade.

   * A invocação síncrona chama o serviço de destino diretamente e manipula imediatamente a resposta.
   * Para invocação assíncrona, o serviço do target é chamado por meio do serviço Gerenciador de Jobs, que coloca a solicitação em uma fila. Por sua vez, o Serviço de Gerenciamento de Jobs chama o provider.file_write_results_service para lidar com os resultados.

1. O provider.file_write_results_service manipula a resposta ou a falha da chamada de serviço de destino. Quando bem-sucedido, a saída é salva na pasta de resultados com base na configuração do endpoint. O provider.file_write_results_service também preserva a origem se o endpoint estiver configurado para preservar os resultados após a conclusão bem-sucedida.

   Quando a chamada do serviço de destino resulta em uma falha, o provider.file_write_results_service registra o motivo da falha em um arquivo failure.log e coloca esse arquivo na pasta de falha. A pasta de falha é criada com base nos parâmetros de configuração especificados para o endpoint. Quando o administrador define a opção Preservar na Falha para a configuração do endpoint, o provider.file_write_results_service também copia os arquivos de origem na pasta de falha. Para obter informações sobre como recuperar arquivos da pasta de falha, consulte [Pontos de falha e recuperação](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Configurações de ponto de extremidade da pasta monitoradas {#watched-folder-endpoint-settings}

Use as configurações a seguir para configurar um ponto de extremidade de pasta monitorada.

**Nome:** (Obrigatório) Identifica o endpoint. Não inclua um caractere &lt; porque ele truncará o nome exibido no Workspace. Se você estiver inserindo um URL como o nome do endpoint, verifique se ele está em conformidade com as regras de sintaxe especificadas no RFC1738.

**Descrição:** Uma descrição do endpoint. Não inclua um caractere &lt; porque ele truncará a descrição exibida no Workspace.

**Caminho:** (Obrigatório) Especifica o local da pasta monitorada. Em um ambiente clusterizado, essa configuração deve apontar para uma pasta de rede compartilhada que possa ser acessada de todos os computadores no cluster.

**Assíncrono:** Identifica o tipo de invocação como assíncrono ou síncrono. O valor padrão é assíncrono. O assíncrono é recomendado para processos de longa duração, enquanto o síncrono é recomendado para processos transitórios ou de curta duração.

**Expressão Cron:** Insira uma expressão CRON se a pasta monitorada precisar ser agendada usando uma expressão CRON. Quando esta configuração é definida, o Intervalo de repetição é ignorado.

**Intervalo de Repetição:** O intervalo em segundos para verificar a entrada da pasta monitorada. A menos que a configuração Acelerador esteja ativada, o Intervalo de Repetição deve ser maior que o tempo médio para processar um trabalho; caso contrário, o sistema pode ficar sobrecarregado. O valor padrão é 5. Consulte a descrição do Tamanho do lote para obter informações adicionais.

**Contagem de repetição:** Número de vezes que a pasta monitorada verifica a pasta ou o diretório. Um valor de -1 indica varredura indefinida. O valor padrão é -1.

**Acelerador:** Quando essa opção é selecionada, ela limita o número de trabalhos de pastas monitoradas que o AEM forma processados a qualquer momento. O número máximo de trabalhos é determinado pelo valor Tamanho do Lote. (Consulte Sobre limitação.)

**Nome de usuário:** (Obrigatório) O nome de usuário usado ao chamar um serviço de destino da pasta monitorada. O valor padrão é SuperAdmin.

**Nome do domínio:** (Obrigatório) O domínio do usuário. O valor padrão é DefaultDom.

**Tamanho do lote:** O número de arquivos ou pastas a serem selecionados por varredura. Use para evitar uma sobrecarga no sistema; a verificação de muitos arquivos de uma vez pode causar uma falha. O valor padrão é 2.

As configurações Intervalo de repetição e Tamanho do lote determinam quantos arquivos a Pasta monitorada coleta em cada verificação. A pasta monitorada usa um pool de threads do Quartz para verificar a pasta de entrada. O pool de threads é compartilhado com outros serviços. Se o intervalo de verificação for pequeno, as threads examinarão a pasta de entrada com frequência. Se os arquivos forem colocados com frequência na pasta monitorada, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar as threads.

Se houver um grande volume de arquivos sendo descartados, aumente o tamanho do lote. Por exemplo, se o serviço chamado pelo endpoint da pasta monitorada puder processar 700 arquivos por minuto e os usuários soltarem arquivos na pasta de entrada na mesma taxa, definir o Tamanho do lote como 350 e o Intervalo de repetição como 30 segundos ajudará no desempenho da Pasta monitorada sem incorrer no custo de verificar a pasta monitorada com muita frequência.

Quando os arquivos são colocados na pasta monitorada, ela lista os arquivos na entrada, o que pode reduzir o desempenho se a varredura estiver ocorrendo a cada segundo. O aumento do intervalo de verificação pode melhorar o desempenho. Se o volume de arquivos que está sendo descartado for pequeno, ajuste o Tamanho do lote e o Intervalo de repetição de acordo. Por exemplo, se 10 arquivos forem descartados a cada segundo, tente definir o Intervalo de repetição como 1 segundo e o Tamanho do lote como 10.

**Tempo de espera:** O tempo, em milissegundos, que deve ser aguardado antes que você verifique uma pasta ou um arquivo após sua criação. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será selecionado após 59 minutos ou mais. O valor padrão é 0.

Essa configuração é útil para garantir que um arquivo ou pasta seja copiado completamente para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e ele levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Isso impede que a pasta monitorada verifique o arquivo se ele não tiver dez minutos.

**Excluir Padrão do Arquivo:** Ponto e vírgula **;** lista delimitada de padrões que uma pasta monitorada usa para determinar quais arquivos e pastas serão verificados e selecionados. Qualquer arquivo ou pasta com este padrão não será examinado para processamento.

Essa configuração é útil quando a entrada é uma pasta com vários arquivos. O conteúdo da pasta pode ser copiado para uma pasta com um nome que será selecionado pela pasta monitorada. Isso impede que a pasta monitorada selecione uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada.

Você pode usar padrões de arquivo para excluir:

* Arquivos com extensões de nome de arquivo específicas; por exemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Arquivos com nomes específicos; por exemplo, dados.&amp;ast; excluiria arquivos e pastas nomeados *dados1*, *dados2* e assim por diante.
* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;
   * &amp;ast;.[dD][Aa]&#39;porta&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](configuring-watched-folder-endpoints.md#about-file-patterns).

**Incluir Padrão do Arquivo:** (Obrigatório) Um ponto e vírgula **;** lista delimitada de padrões que a pasta monitorada usa para determinar quais pastas e arquivos serão verificados e coletados. Por exemplo, se o Padrão de arquivo de inclusão for input&amp;ast;, todos os arquivos e pastas que corresponderem a input&amp;ast; serão selecionados. Isso inclui arquivos e pastas chamados input1, input2 e assim por diante.

O valor padrão é &amp;ast; e indica todos os arquivos e pastas.

Você pode usar padrões de arquivo para incluir:

* Arquivos com extensões de nome de arquivo específicas; por exemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Arquivos com nomes específicos; por exemplo, dados.&amp;ast; incluiria arquivos e pastas nomeados *dados1*, *dados2* e assim por diante.
* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;
   * &amp;ast;.[dD][Aa]&#39;porta&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](configuring-watched-folder-endpoints.md#about-file-patterns).


**Pasta de resultado:** A pasta onde os resultados salvos são armazenados. Se os resultados não aparecerem nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e serão salvos na pasta de falha. Esse valor pode ser um caminho absoluto ou relativo com os seguintes padrões de arquivo:

* %F = prefixo do nome do arquivo
* %E = extensão de nome de arquivo
* %Y = ano (completo)
* %y = ano (últimos dois dígitos)
* %M = mês
* %D = dia do mês
* %d = dia do ano
* %H = hora (relógio de 24 horas)
* %h = hora (relógio de 12 horas)
* %m = minuto
* %s = segundo
* %l = milissegundo
* %R = número aleatório (entre 0 e 9)
* %P = id do processo ou da tarefa

Por exemplo, se forem 20h em 17 de julho de 2009 e você especificar `C:/Test/WF0/failure/%Y/%M/%D/%H/`, a pasta de resultados é `C:/Test/WF0/failure/2009/07/17/20`.

Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta monitorada. O valor padrão é result/%Y/%M/%D/, que é a pasta Result dentro da pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Quanto menor o tamanho das pastas de resultados, melhor será o desempenho das Pastas monitoradas. Por exemplo, se a carga estimada para a pasta monitorada for de 1000 arquivos a cada hora, tente um padrão como `result/%Y%M%D%H` para que uma nova subpasta seja criada a cada hora. Se a carga for menor (por exemplo, 1000 arquivos por dia), você poderá usar um padrão como `result/%Y%M%D`.

**Preservar pasta:** O local onde os arquivos são armazenados após a verificação e coleta bem-sucedidas. O caminho pode ser um caminho de diretório absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.

**Pasta com falha:** A pasta onde os arquivos de falha são salvos. Este local é sempre relativo à pasta monitorada. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados.

Arquivos somente leitura não são processados e serão salvos na pasta de falha.

O valor padrão é failure/%Y/%M/%D/.

**Preservar na Falha:** Preserva os arquivos de entrada se houver uma falha ao executar a operação em um serviço. O valor padrão é true.

**Substituir nomes de arquivo duplicados:** Quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como False, os arquivos e as pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.

**Duração da Remoção:** (Obrigatório) Os arquivos e as pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Essa configuração é útil para garantir que a pasta de resultados não fique cheia.

Um valor de -1 dias indica que a pasta de resultados nunca deve ser excluída. O valor padrão é -1.

**Nome da operação:** (Obrigatório) Uma lista de operações que podem ser atribuídas ao endpoint da pasta monitorada.

**Mapeamentos de parâmetros de entrada:** Usado para configurar a entrada necessária para processar o serviço e a operação. As configurações disponíveis dependem do serviço que está usando o ponto de extremidade da pasta monitorada. Estes são os dois tipos de entradas:

**Literal:** A pasta monitorada usa o valor inserido no campo como é exibido. Todos os tipos básicos de Java são compatíveis. Por exemplo, se uma API usar entradas como String, long, int e Boolean, a cadeia de caracteres será convertida no tipo adequado e o serviço será chamado.

**Variável:** O valor inserido é um padrão de arquivo que a pasta monitorada usa para escolher a entrada. Por exemplo, se houver o serviço de criptografia de senhas, em que o documento de entrada deve ser um arquivo PDF, o usuário poderá usar &amp;ast;.pdf como padrão de arquivo. A pasta monitorada capturará todos os arquivos na pasta monitorada que correspondam a este padrão e chamará o serviço para cada arquivo. Quando uma variável é usada, todos os arquivos de entrada são convertidos em documentos. Somente APIs que usam Documento como tipo de entrada são compatíveis.

**Mapeamentos de Parâmetros de Saída:** Usado para configurar as saídas do serviço e da operação. As configurações disponíveis dependem do serviço que está usando o ponto de extremidade da pasta monitorada.

A saída da pasta monitorada pode ser um único documento, uma lista de documentos ou um mapa de documentos. Esses documentos de saída são salvos na pasta de resultados, usando o padrão especificado no Mapeamento do parâmetro de saída.

>[!NOTE]
>
>A especificação de nomes que resultam em nomes de arquivo de saída exclusivos melhora o desempenho. Por exemplo, considere o caso em que o serviço retorna um documento de saída e o Mapeamento de parâmetros de saída o mapeia para `%F.%E` (o nome e a extensão do arquivo de entrada). Nesse caso, se os usuários soltarem arquivos com o mesmo nome a cada minuto e a pasta de resultados estiver configurada como `result/%Y/%M/%D`e se a configuração Substituir nome de arquivo duplicado estiver desativada, a Pasta monitorada tentará resolver os nomes de arquivo duplicados. O processo de resolver nomes de arquivo duplicados pode afetar o desempenho. Nessa situação, alterando o Mapeamento de Parâmetros de Saída para `%F_%h_%m_%s_%l` adicionar horas, minutos, segundos e milissegundos ao nome ou garantir que os arquivos soltos tenham nomes exclusivos pode melhorar o desempenho.

## Sobre padrões de arquivo {#about-file-patterns}

Os administradores podem especificar o tipo de arquivo que pode chamar um serviço. Vários padrões de arquivo podem ser estabelecidos para cada pasta monitorada. Um padrão de arquivo pode ser uma das seguintes propriedades de arquivo:

* Arquivos com extensões de nome de arquivo específicas; por exemplo, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf,;
* Arquivos com nomes específicos; por exemplo, dados.&amp;ast;
* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;
   * &amp;ast;.[dD][Aa]&#39;porta&#39;
   * &amp;ast;.[Xx][Mm][Ll]

O administrador pode definir o padrão de arquivo da pasta de saída na qual os resultados serão armazenados. Para as pastas de saída (resultado, preservação e falha), o administrador pode especificar qualquer um destes padrões de arquivo:

* %Y = ano (completo)
* %y = ano (últimos dois dígitos)
* %M = mês,
* %D = dia do mês,
* %d = dia do ano,
* %h = hora,
* %m = minuto,
* %s = segundo,
* %R = número aleatório entre 0-9
* %J = Nome da tarefa

Por exemplo, o caminho para a pasta de resultados pode ser `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Os mapeamentos de parâmetros de saída também podem especificar padrões adicionais, como estes:

* %F = Nome de arquivo de origem
* %E = Extensão De Nome De Arquivo De Origem

Se o padrão de mapeamento do parâmetro de saída terminar com &quot;File.separator&quot; (que é o separador de caminhos), uma pasta será criada e o conteúdo será copiado nessa pasta. Se o padrão não terminar com &quot;File.separator&quot;, o conteúdo (arquivo de resultado ou pasta) será criado com esse nome. Para obter mais informações sobre mapeamentos de parâmetros de saída, consulte [Dicas e truques para pastas monitoradas](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## Sobre a limitação {#about-throttling}

Quando a limitação é ativada para um endpoint de pasta observada, ela limita o número de trabalhos de pasta observados que podem ser processados a qualquer momento. O número máximo de trabalhos é determinado pelo valor Tamanho do lote, também configurável no endpoint Pasta monitorada. Os documentos de entrada no diretório de entrada da pasta monitorada não serão sondados quando o limite de limitação for atingido. Os documentos também permanecerão no diretório de entrada até que outros trabalhos de pasta observados sejam concluídos e outra tentativa de enquete seja feita. Se houver processamento síncrono, todos os trabalhos processados em uma única enquete serão contados para o limite de limitação, mesmo que os trabalhos sejam processados consecutivamente em um único thread.

>[!NOTE]
>
>A limitação não é dimensionada com um cluster. Quando a limitação estiver habilitada, o cluster como um todo não processará mais do que o número de trabalhos especificados no Tamanho do Lote em um determinado momento. Esse limite é em todo o cluster e não específico para cada nó no cluster. Por exemplo, com um Tamanho de lote de 2, o limite de limitação pode ser atingido com um único nó processando dois trabalhos e nenhum outro nó sondaria o diretório de entrada até que um dos trabalhos seja concluído.

### Como funciona a limitação {#how-throttling-works}

A Pasta monitorada verifica a pasta de entrada em cada Intervalo de repetição, seleciona o número de arquivos especificados no Tamanho do lote e chama o serviço de destino para cada um desses arquivos. Por exemplo, se o Tamanho do Lote for quatro, em cada varredura, a Pasta monitorada coletará quatro arquivos, criará quatro solicitações de chamada e chamará o serviço de destino. Antes que essas solicitações sejam concluídas, se a Pasta monitorada for invocada, ela iniciará novamente quatro trabalhos, independentemente da conclusão dos quatro trabalhos anteriores.

A limitação impede que a Pasta monitorada chame novos trabalhos quando os trabalhos anteriores não estiverem concluídos. A pasta monitorada detectará trabalhos em andamento e processará novos trabalhos com base no tamanho do lote menos os trabalhos em andamento. Por exemplo, na segunda invocação, se o número de trabalhos concluídos for apenas três e um trabalho ainda estiver em andamento, a Pasta monitorada chamará apenas mais três trabalhos.

* A Pasta monitorada depende do número de arquivos presentes na pasta de preparo para descobrir quantos trabalhos estão em andamento. Se os arquivos permanecerem não processados na pasta de preparo, a Pasta monitorada não chamará mais tarefas. Por exemplo, se o tamanho do lote for quatro e três trabalhos estiverem paralisados, a Pasta monitorada chamará apenas um trabalho em invocações subsequentes. Há vários cenários que podem fazer com que os arquivos permaneçam não processados na pasta de preparo. Quando os trabalhos são interrompidos, o administrador pode encerrar o processo na página de administração do fluxo de trabalho de formulários para que a Pasta monitorada mova os arquivos para fora da pasta de preparo.
* Se o Forms Server ficar inativo antes que a Pasta monitorada possa chamar os trabalhos, o administrador poderá mover os arquivos para fora da pasta de preparo. Para obter informações, consulte [Pontos de falha e recuperação](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Se o Servidor do Forms estiver em execução, mas a Pasta monitorada não estiver em execução quando o serviço Gerenciador de trabalhos chamar de volta, o que ocorre quando os serviços não iniciam na sequência ordenada, o administrador poderá mover os arquivos para fora da pasta de preparo. Para obter informações, consulte [Pontos de falha e recuperação](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Desempenho e escalabilidade {#performance-and-scalability}

A pasta monitorada pode atender a 100 pastas no total em um único nó. O desempenho da Pasta monitorada depende do desempenho do Servidor do Forms. Para invocação assíncrona, o desempenho é mais dependente da carga do sistema e dos trabalhos que estão na fila do Gerenciador de trabalhos.

O desempenho da Pasta monitorada pode ser aprimorado adicionando nós ao cluster. Os trabalhos de Pastas monitoradas são distribuídos pelos nós do cluster em virtude do Quartz scheduler e, se houver solicitações assíncronas, pelo serviço Gerenciador de trabalhos. Todos os trabalhos são mantidos no banco de dados.

A Pasta monitorada depende do serviço Agendador para agendamento, cancelamento de agendamento e reagendamento dos trabalhos. Outros serviços, como o serviço de Gerenciamento de Eventos, o serviço do Gerenciador de Usuários e o serviço do Provedor de Email, estão disponíveis e compartilham o pool de threads do serviço do Agendador. Isso pode afetar o desempenho da Pasta monitorada. O ajuste do pool de threads do serviço Agendador será necessário quando todos os serviços começarem a usá-lo.

## Pastas monitoradas em um cluster {#watched-folders-in-a-cluster}

Em um cluster, o Watched Folder depende do Quartz scheduler e do serviço Job Manager para balanceamento de carga e failover. Para obter mais informações sobre o comportamento do cluster Quartz, consulte [Documentação do Quartz](https://www.quartz-scheduler.org/documentation).

A pasta monitorada executa estas três tarefas principais em cada enquete:

* Examinar a pasta
* Chamar o serviço de público alvo
* Lidar com os resultados

O comportamento de balanceamento de carga e failover muda dependendo se a pasta monitorada está configurada para invocação síncrona ou assíncrona.

### Pasta monitorada síncrona em um cluster {#synchronous-watched-folder-in-a-cluster}

Para invocações síncronas, o balanceador de carga Quartz decide qual nó receberá o evento de pesquisa. O nó que obtém o evento de pesquisa executará todas as tarefas: verificar a pasta, chamar o serviço de destino e lidar com os resultados.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Para invocações síncronas, quando um nó falha, o Quartz scheduler envia novos eventos de polling para outros nós. As chamadas que foram iniciadas no nó com falha serão perdidas. Para obter mais informações sobre como recuperar os arquivos associados ao job com falha, consulte [Pontos de falha e recuperação](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Pasta monitorada assíncrona em um cluster {#asynchronous-watched-folder-in-a-cluster}

Para invocações assíncronas, o balanceador de carga Quartz decide qual nó receberá o evento de sondagem. O nó que obtém o evento de pesquisa verificará a pasta de entrada e chamará o serviço de destino colocando a solicitação na fila de serviço do Gerenciador de trabalhos. O balanceador de carga do serviço Gerenciador de trabalhos, por sua vez, é responsável por decidir qual nó processará a solicitação de invocação. É possível que, mesmo que o nó A tenha criado a solicitação de chamada, o nó B termine processando a solicitação. Ou o nó que iniciou a solicitação de chamada também pode acabar processando a solicitação.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Para invocações assíncronas, quando um nó falha, o Quartz scheduler envia novos eventos de polling para outros nós. As solicitações de chamada criadas no nó com falha estarão na fila de serviços do Gerenciador de trabalhos e serão enviadas para outros nós para processamento. Os arquivos para os quais as solicitações de invocação não forem criadas permanecerão na pasta de preparo. Para obter mais informações sobre como recuperar os arquivos associados ao job com falha, consulte [Pontos de falha e recuperação](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Pontos de falha e recuperação {#failure-points-and-recovery}

Em cada evento de pesquisa, a Pasta monitorada bloqueia a pasta de entrada, move os arquivos que correspondem ao padrão de arquivo de inclusão para a pasta de preparo e, em seguida, desbloqueia a pasta de entrada. O bloqueio é necessário para que dois threads não selecionem o mesmo conjunto de arquivos e os processem duas vezes. As chances de isso acontecer aumentam com um pequeno intervalo de repetição e um grande tamanho de lote. Depois que os arquivos forem movidos para a pasta de preparo, a pasta de entrada será desbloqueada para que outras threads possam examinar a pasta. Esta etapa ajuda a fornecer alta taxa de transferência, pois outras threads podem examinar enquanto uma thread está processando os arquivos.

Depois que os arquivos são movidos para a pasta de preparo, solicitações de invocação são criadas para cada arquivo e o serviço de destino é chamado. Pode haver casos em que a Pasta monitorada não possa recuperar os arquivos na pasta de preparo:

* Se o servidor ficar inativo antes que a Pasta monitorada possa criar a solicitação de invocação, os arquivos na pasta de preparo permanecerão na pasta de preparo e não serão recuperados.
* Se a Pasta monitorada tiver criado com sucesso a solicitação de invocação para cada um dos arquivos na pasta de preparo e o servidor falhar, há dois comportamentos com base no tipo de invocação:

**Síncrono:** Se a Pasta monitorada estiver configurada para chamar o serviço de forma síncrona, todos os arquivos na pasta de preparo permanecerão não processados na pasta de preparo.

**Assíncrono:** Nesse caso, a Pasta monitorada depende do serviço Gerenciador de trabalhos. Se o serviço do Gerenciador de trabalhos retornar as chamadas da Pasta monitorada, os arquivos na pasta de preparo serão movidos para a pasta de preservação ou falha com base nos resultados da invocação. Se o serviço Gerenciador de trabalhos não retornar a chamada da Pasta monitorada, os arquivos permanecerão não processados na pasta de preparo. Essa situação ocorre quando a Pasta monitorada não está em execução quando o Gerenciador de trabalhos chama de volta.

### Recuperando arquivos de origem não processados na pasta de preparo {#recovering-unprocessed-source-files-in-the-stage-folder}

Quando a Pasta monitorada não puder processar os arquivos de origem na pasta de preparo, você poderá recuperar os arquivos não processados.

1. Reinicie o servidor de aplicativos ou nó.
1. (Opcional) Impedir que a Pasta monitorada processe novos arquivos de entrada. Se ignorar esta etapa, será muito mais difícil determinar quais arquivos não serão processados na pasta de preparo. Para impedir que a Pasta monitorada processe novos arquivos de entrada, execute uma das seguintes tarefas:

   * Em Aplicativos e Serviços, altere o parâmetro Incluir Padrão do Arquivo do endpoint da pasta monitorada para algo que não corresponda a nenhum dos novos arquivos de entrada (por exemplo, insira `NOMATCH`).
   * Suspenda o processo que está criando novos arquivos de entrada.

   Aguarde até que o AEM recupere e e processe todos os arquivos. A maioria dos arquivos deve ser recuperada e os novos arquivos de entrada processados corretamente. O tempo de espera pela Pasta monitorada para recuperar e processar os arquivos dependerá da duração da operação a ser chamada e do número de arquivos a serem recuperados.

1. Determine quais arquivos não podem ser processados. Se você esperou um tempo apropriado e concluiu a etapa anterior e ainda há arquivos não processados na pasta de preparo, vá para a próxima etapa.

   >[!NOTE]
   >
   >Você pode verificar a data e o carimbo de data e hora dos arquivos no diretório do estágio. Dependendo do número de arquivos e do tempo de processamento normal, você pode determinar quais arquivos são antigos o suficiente para serem considerados travados.

1. Copie os arquivos não processados do diretório de preparo para o diretório de entrada.
1. Se você impediu que a Pasta monitorada processasse novos arquivos de entrada na etapa 2, altere o Padrão de arquivo de inclusão para seu valor anterior ou reative o processo desativado.

## Considerações de segurança para pastas monitoradas {#security-considerations-for-watched-folders}

Cada pasta monitorada é configurada com um nome de usuário e senha. Essas credenciais são usadas ao chamar os serviços. A Pasta monitorada depende do fato de que a pasta compartilhada está protegida com o sistema de arquivos de segurança subjacente, de modo que somente o proprietário da pasta monitorada possa acessar a pasta compartilhada.

## Dicas e truques para pastas monitoradas {#tips-and-tricks-for-watched-folders}

Estas são algumas dicas e truques ao configurar o endpoint da Pasta monitorada:

* Se você tiver uma pasta monitorada no Windows que esteja processando arquivos de imagem, especifique valores para a opção Incluir padrão do arquivo ou Excluir padrão do arquivo para impedir que o arquivo Thumbs.db gerado automaticamente pelo Windows seja sondado pela pasta monitorada.
* Se uma expressão CRON for especificada, o intervalo de repetição será ignorado. O uso da expressão cron é baseado no sistema de agendamento de tarefas de código aberto Quartz, versão 1.4.0.
* O tamanho do lote é o número de arquivos ou pastas que serão selecionados em cada varredura da pasta monitorada. Se o tamanho do lote estiver definido como dois e dez arquivos ou pastas forem descartados na pasta de entrada da pasta monitorada, apenas dois serão coletados em cada verificação. Na próxima verificação, que ocorrerá após o tempo especificado no intervalo de repetição, os próximos dois arquivos serão coletados.
* Para padrões de arquivo, os administradores podem especificar expressões regulares com suporte adicionado de padrões curinga para especificar padrões de arquivo. A Pasta monitorada modifica a expressão regular para suportar padrões curinga, como o &amp;ast;.&amp;ast; ou &amp;ast;.pdf. Esses padrões curingas não são suportados pelas expressões regulares.
* A Pasta monitorada verifica a pasta de entrada em busca da entrada e não sabe se o arquivo ou a pasta de origem foi completamente copiada para a pasta de entrada antes de iniciar o processamento do arquivo ou da pasta. Para garantir que o arquivo ou pasta de origem seja completamente copiado para a pasta de entrada da pasta monitorada antes que o arquivo ou pasta seja selecionado, execute estas tarefas:

   * Use o Tempo de espera, que é o tempo em milissegundos que a Pasta monitorada aguarda desde a última modificação. Use esse recurso se você tiver arquivos grandes para processar. Por exemplo, se o download de um arquivo levar 10 minutos, especifique o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Isso impedirá que a Pasta monitorada selecione o arquivo, se ele não tiver 10 minutos de idade.
   * Use o padrão de exclusão de arquivo e o padrão de inclusão de arquivo. Por exemplo, se o padrão de exclusão de arquivo for `ex*` e o padrão do arquivo include é `in*`, A Pasta monitorada capturará os arquivos que começam com &quot;in&quot; e não capturará os arquivos que começam com &quot;ex&quot;. Para copiar arquivos ou pastas grandes, primeiro renomeie o arquivo ou pasta de modo que o nome comece com &quot;ex&quot;. Depois que o arquivo ou pasta chamado &quot;ex&quot; for completamente copiado para a pasta monitorada, renomeie-o para &quot;in&amp;ast;&quot;.

* Use a duração da limpeza para manter a pasta de resultados limpa. A Pasta monitorada limpa todos os arquivos mais antigos que a duração mencionada na duração da limpeza. A duração é em dias.
* Ao adicionar um endpoint de Pasta monitorada, após selecionar o nome da operação, o mapeamento do parâmetro de entrada é preenchido. Para cada entrada da operação, um campo de mapeamento de parâmetro de entrada é gerado. Estes são exemplos de mapeamentos de parâmetro de entrada:

   * Para `com.adobe.idp.Document` input: Se a operação de serviço tiver uma entrada do tipo `Document`, o administrador poderá especificar o tipo de mapeamento como `Variable`. A Pasta monitorada coletará a entrada da pasta de entrada monitorada com base no padrão de arquivo especificado para o parâmetro de entrada. Se o administrador especificar `*.pdf` como parâmetro, cada arquivo com extensão .pdf será selecionado, convertido em `com.adobe.idp.Document`e o serviço chamado.
   * Para `java.util.Map` input: Se a operação de serviço tiver uma entrada do tipo `Map`, o administrador poderá especificar o tipo de mapeamento como `Variable` e insira um valor de mapeamento com um padrão como `*.pdf`. Por exemplo, um serviço precisa de um mapa de dois `com.adobe.idp.Document` objetos que representam dois arquivos na pasta de entrada, como 1.pdf e 2.pdf. A pasta monitorada criará um mapa com a chave como o nome do arquivo e o valor como `com.adobe.idp.Document`.
   * Para `java.util.List` input: Se a operação de serviço tiver uma entrada do tipo Lista, o administrador poderá especificar o tipo de mapeamento como `Variable` e insira um valor de mapeamento com um padrão como `*.pdf`. Quando os arquivos PDF forem soltos na pasta de entrada, a Pasta monitorada criará uma lista das `com.adobe.idp.Document` objetos que representam esses arquivos e chamam o serviço de destino.
   * Para `java.lang.String`: O administrador tem duas opções. Primeiro, o administrador pode especificar o tipo de mapeamento como `Literal` e insira um valor de mapeamento como uma string, como `hello.` A pasta monitorada chamará o serviço com a cadeia de caracteres `hello`. Em segundo lugar, o administrador pode especificar o tipo de mapeamento como `Variable` e insira um valor de mapeamento com um padrão como `*.txt`. Nesse último caso, os arquivos com a extensão .txt serão lidos como um documento forçado como uma sequência de caracteres para invocar o serviço.
   * Tipo primitivo de Java: o administrador pode especificar o tipo de mapeamento como `Literal` e forneça o valor. A Pasta monitorada chamará o serviço com o valor especificado.

* A Pasta monitorada deve funcionar com documentos. As saídas suportadas são `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node`, e uma lista e um mapa desses tipos. Qualquer outro tipo resultará em uma saída com falha na pasta de falha.
* Se os resultados não estiverem na pasta de resultados, verifique a pasta com falha para ver se ocorreu uma falha.
* A pasta monitorada funciona melhor se usada no modo assíncrono. Nesse modo, a Pasta monitorada coloca a solicitação de chamada na fila e retorna a chamada. A fila é processada de forma assíncrona. Quando a opção Assíncrono não está definida, a Pasta monitorada chama o serviço de destino de forma síncrona e o Mecanismo do processo aguarda até que o serviço seja concluído com a solicitação e os resultados sejam produzidos. Se o serviço de destino levar muito tempo para processar a solicitação, a Pasta monitorada poderá receber erros de tempo limite.
* A criação de pastas monitoradas para operações de importação e exportação não permite a abstração da extensão do nome de arquivo. Ao chamar o serviço de Integração de Dados de Formulário usando pastas monitoradas, o tipo de extensão do nome de arquivo para o arquivo de saída pode não corresponder ao formato de saída pretendido para o tipo de objeto do documento. Por exemplo, se o arquivo de entrada para uma pasta monitorada que chama a operação de exportação for um formulário XFA que contém dados, a saída deverá ser um arquivo de dados XDP. Para obter um arquivo de saída com a extensão de nome de arquivo correta, você pode especificá-lo no mapeamento do parâmetro de saída. Neste exemplo, você pode usar %F.xdp para o mapeamento do parâmetro de saída.
* A pasta monitorada pode processar arquivos de entrada antes que eles sejam copiados completamente para a pasta. O bloqueio de arquivos não é obrigatório no UNIX, como acontece no Windows. Por esse motivo, quando um arquivo está sendo copiado para uma pasta monitorada, a Pasta monitorada pode mover o arquivo para o preparo sem esperar a conclusão da cópia. Esse comportamento faz com que somente uma parte do arquivo de entrada seja processada. Atualmente, há duas soluções alternativas:

   * Solução alternativa 1

      1. Especifique um padrão para Excluir padrão de arquivo, como temp&amp;ast;.ps.
      1. Copie os arquivos que começam com temp (por exemplo, temp1.ps) para a pasta monitorada.
      1. Depois que o arquivo tiver sido completamente copiado para a pasta monitorada, renomeie-o para corresponder ao padrão especificado em Incluir padrão de arquivo. A Pasta monitorada move o arquivo concluído para o estágio.

   * Solução alternativa 2

     Se você souber o tempo máximo necessário para copiar os arquivos para uma pasta monitorada, especifique o tempo em segundos para o Tempo de espera. A Pasta monitorada aguarda o período especificado antes de mover o arquivo para o preparo.

     Isso não é um problema para arquivos no Windows porque o Windows bloqueia um arquivo quando um thread está gravando. No entanto, esse é um problema para pastas no Windows. Para pastas, você deve seguir as etapas da Solução alternativa 1.

* Se o atributo de ponto de extremidade Preservar nome da pasta para a pasta monitorada estiver definido como um caminho de diretório nulo, o diretório de preparo não será limpo como deveria ser. O diretório ainda contém o arquivo processado e a pasta temporária.

## Recomendações específicas de serviço para pastas monitoradas {#service-specific-recommendations-for-watched-folders}

Para todos os serviços, você deve ajustar o tamanho do lote e o intervalo de repetição da pasta monitorada para que a taxa na qual a pasta monitorada seleciona novos arquivos e pastas para processamento não exceda a taxa de tarefas que podem ser processadas pelo servidor do AEM Forms. Os parâmetros reais a serem usados podem variar dependendo da quantidade de pastas monitoradas configuradas, dos serviços que estão usando pastas monitoradas e da intensidade dos trabalhos no processador.

### Gerar recomendações de serviço do PDF {#generate-pdf-service-recommendations}

* O serviço Gerar PDF pode converter apenas um arquivo por vez para estes tipos de arquivos: Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® e Adobe PageMaker®. Esses são trabalhos de longa duração; portanto, mantenha o tamanho do lote em uma configuração baixa. Além disso, aumente o intervalo de repetição se houver mais nós no cluster.
* Para PostScript (PS), Encapsulated PostScript (EPS) e tipos de arquivos de imagem, o serviço Gerar PDF pode processar vários arquivos em paralelo. Você deve ajustar cuidadosamente o tamanho do pool do bean de sessão (que controla o número de conversões que serão feitas em paralelo) dependendo da capacidade do servidor e do número de nós no cluster. Em seguida, aumente o tamanho do lote para um número igual ao tamanho do pool de beans de sessão para os tipos de arquivos que você está tentando converter. A frequência de polling deve ser ditada pelo número de nós no cluster; no entanto, como o serviço Gerar PDF processa esses tipos de jobs com bastante rapidez, você pode configurar o intervalo de repetição para um valor baixo, como 5 ou 10.
* Embora o serviço Gerar PDF possa converter apenas um arquivo OpenOffice de cada vez, a conversão é bastante rápida. A lógica acima para conversões de PS, EPS e imagem também se aplica a conversões OpenOffice.
* Para permitir uma distribuição de carga uniforme no cluster, mantenha o tamanho do lote baixo e aumente o intervalo de repetição.

### recomendações do serviço de formulários com código de barras {#barcoded-forms-service-recommendations}

* Para obter o melhor desempenho ao processar formulários com código de barras (arquivos pequenos), insira `10` para Tamanho do Lote e `2` em Intervalo de repetição.
* Quando muitos arquivos são colocados na pasta de entrada, erros com arquivos ocultos são chamados *thumbs.db* pode ocorrer. Portanto, é recomendável definir o Padrão do arquivo de inclusão para os arquivos de inclusão com o mesmo valor especificado para a variável de entrada (por exemplo, `*.tiff`). Isso impede que a Pasta monitorada processe os arquivos do banco de dados.
* Um valor de Tamanho de Lote de `5` e intervalo de repetição de `2` O normalmente é suficiente porque o serviço Forms com código de barras geralmente leva cerca de 0,5 segundo para processar um código de barras.
* A Pasta monitorada não espera que o Mecanismo do processo conclua o trabalho antes que ele selecione novos arquivos ou pastas. Ele continua verificando a pasta monitorada e chamando o serviço de destino. Esse comportamento pode sobrecarregar o mecanismo, causando problemas de recursos e tempos limite. Certifique-se de usar o intervalo de repetição e o tamanho do lote para limitar a entrada da Pasta monitorada. É possível aumentar o intervalo de repetição e reduzir o tamanho do lote se existirem mais pastas monitoradas ou ativar a limitação no endpoint. Para obter informações sobre limitação, consulte [Sobre a limitação](configuring-watched-folder-endpoints.md#about-throttling).
* A pasta monitorada representa o usuário especificado no nome do usuário e no nome do domínio. A Pasta monitorada chama o serviço como este usuário se invocada diretamente ou se o processo for de curta duração. Para um processo de longa duração, o processo é chamado com o contexto Sistema. Os administradores podem definir políticas do sistema operacional para a Pasta monitorada para determinar a qual usuário permitir ou negar acesso.
* Use padrões de arquivo para organizar resultados, falhas e preservar pastas. (Consulte [Sobre padrões de arquivo](configuring-watched-folder-endpoints.md#about-file-patterns).)

* A pasta monitorada depende do Quartz scheduler para digitalizar as pastas monitoradas. O Quartz scheduler tem um pool de threads para digitalizá-los. Se o intervalo de repetição da pasta monitorada for muito baixo (&lt; 5 segundos) e o tamanho do lote for alto (> 2), pode ocorrer uma condição de corrida. Quando essa condição ocorre, um arquivo é selecionado por dois threads de Quartz:

   * Um dos threads localiza com êxito o arquivo e invoca o serviço de destino com o arquivo.
   * O segundo thread vê o arquivo, mas falha ao tentar descobrir se o arquivo é válido (arquivo de leitura ou gravação), o que causa falhas falsas que indicam que o arquivo não pode ser processado porque é somente leitura. Isso acontece somente com um intervalo de repetição baixo e um tamanho de lote alto.
