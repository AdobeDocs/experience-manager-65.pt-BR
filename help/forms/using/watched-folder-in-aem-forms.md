---
title: Pasta assistida no AEM Forms
seo-title: Watched folder in AEM Forms
description: Um administrador pode colocar uma pasta em observação e iniciar uma operação de fluxo de trabalho, serviço ou script quando um arquivo é colocado na pasta que está sendo observada.
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 79dcba8e14eac39467510416bf31737ac721b07f
workflow-type: tm+mt
source-wordcount: '7118'
ht-degree: 0%

---

# Pasta assistida no AEM Forms{#watched-folder-in-aem-forms}

Um administrador pode configurar uma pasta de rede, conhecida como Pasta assistida, de modo que, quando um usuário colocar um arquivo (como um arquivo PDF) na Pasta assistida, um fluxo de trabalho, serviço ou operação de script pré-configurado seja iniciado para processar o arquivo adicionado. Depois que o serviço executa a operação especificada, ele salva o arquivo de resultado em uma pasta de saída especificada. Para obter mais informações sobre workflow, serviço e script, consulte [Vários métodos para processar arquivos](#variousmethodsforprocessingfiles).

## Criar uma pasta assistida {#create-a-watched-folder}

Você pode usar um dos seguintes métodos para criar uma Pasta assistida no sistema de arquivos:

* Ao configurar as propriedades de um nó de configuração de Pasta assistida, digite o caminho completo do diretório pai na propriedade folderPath e anexe o nome da Pasta assistida a ser criada, conforme mostrado no exemplo a seguir: `C:/MyPDFs/MyWatchedFolder`
A pasta `MyWatchedFolder`não existe, o AEM Forms tenta criar a pasta no caminho especificado.

* Crie uma pasta no sistema de arquivos antes de configurar um endpoint de Pasta assistida e forneça o caminho completo na propriedade folderPath. Para obter informações detalhadas sobre a propriedade folderPath, consulte [Propriedades da pasta assistida](#watchedfolderproperties).

>[!NOTE]
>
>Em um ambiente em cluster, a pasta usada como uma Pasta assistida deve ser acessível, gravável e compartilhada no sistema de arquivos ou na rede. Cada instância do servidor de aplicativos do cluster deve ter acesso à mesma pasta compartilhada. No Windows, crie uma unidade de rede mapeada em todos os servidores e especifique o caminho da unidade de rede mapeada na propriedade folderPath.

## Criar nó de configuração de pasta assistida {#create-watched-folder-configuration-node}

Para configurar uma Pasta assistida, crie um nó de configuração de Pasta assistida. Execute as seguintes etapas para criar o nó de configuração:

1. Faça logon no CRX-DE lite como administrador e navegue até a pasta /etc/fd/watchfolder/config.

1. Crie um nó do tipo `nt:unstructured`. Por exemplo, watchedfolder

   >[!NOTE]
   >
   >O nome do nó da Pasta assistida não pode incluir espaços e caracteres especiais.

1. Adicione as seguintes propriedades ao nó :

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`
   Para obter uma lista completa das propriedades compatíveis, consulte [Propriedades da pasta assistida](#watchedfolderproperties).

1. Clique em **Salvar tudo**. Depois que o nó é criado e as propriedades são salvas. As pastas `input`, `result`, `failure`, `preserve` e `stage`são criadas no caminho especificado na propriedade `folderPath`.

   O trabalho de digitalização começa a digitalizar a Pasta assistida em um intervalo de tempo definido.

## Propriedades da pasta assistida {#watchedfolderproperties}

Você pode configurar as seguintes propriedades para uma Pasta assistida.

* **folderPath (String)**: O caminho da pasta a ser digitalizada em intervalos de tempo definidos. Para um ambiente em cluster, a pasta deve estar em um local compartilhado com todos os servidores que tenham acesso total ao servidor. É uma propriedade obrigatória.
* **inputProcessorType (String)**: O tipo do processo a ser iniciado. Você pode especificar workflow, script ou serviço. É uma propriedade obrigatória.
* **inputProcessorId (String)**: O comportamento da propriedade inputProcessorId é baseado no valor especificado para a propriedade inputProcessorType. É uma propriedade obrigatória. A lista a seguir detalha todos os valores possíveis da propriedade inputProcessorType e os requisitos correspondentes da propriedade inputProcessorType:

   * Para workflow, especifique o modelo de workflow a ser executado. Por exemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * Para o script, especifique o caminho JCR do script a ser executado. Por exemplo, /etc/fd/watchfolder/test/testScript.ecma
   * Para serviço, especifique o filtro usado para localizar um serviço OSGi. O serviço é registrado como uma implementação da interface com.adobe.aemfd.watchfolder.service.api.ContentProcessor .

* **runModes (String)**: Uma lista separada por vírgulas de run-modes permitidos para execução de workflows. Alguns exemplos:

   * author

   * publicação

   * autor,publicação

   * publicar, autor

>[!NOTE]
>
>Se o servidor que hospeda a Pasta assistida não tiver um dos modos de execução especificados, a Pasta assistida sempre será ativada independentemente dos modos de execução no servidor.

* **outputFilePattern (String)**: Padrão do arquivo de saída. Você pode especificar um padrão de pasta ou arquivo. Se um padrão de pasta for especificado, os arquivos de saída terão nomes como descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes como descrito em padrão de arquivo. [O ](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) padrão File and folder também pode especificar uma estrutura de diretório para os arquivos de saída. É uma propriedade obrigatória.

* **stageFileExpirationDuration (Long, padrão -1)**: O número de segundos a aguardar antes de um arquivo/pasta de entrada que já foi selecionado para processamento deve ser tratado como tendo o tempo limite expirado e marcado como uma falha. Esse mecanismo de expiração só é ativado quando o valor dessa propriedade é um número positivo.

>[!NOTE]
>
>Mesmo quando uma entrada é marcada como tendo o tempo limite expirado usando esse mecanismo, ela ainda pode estar sendo processada em segundo plano, mas apenas levando mais tempo do que o esperado. Se o conteúdo de entrada tiver sido consumido antes do início do mecanismo de tempo limite, o processamento poderá até prosseguir para a conclusão mais tarde e a saída será despejada para a pasta de resultados. Se o conteúdo não tiver sido consumido antes do tempo limite, é muito provável que o processamento ocorra um erro posteriormente ao tentar consumir o conteúdo, e esse erro também será registrado na pasta de falha da mesma entrada. Por outro lado, se o processamento da entrada nunca tiver sido ativado devido a um erro intermitente de trabalho/workflow (que é o cenário que o mecanismo de expiração pretende abordar), é claro que nenhuma dessas duas ocorrências ocorrerá. Assim, para quaisquer entradas na pasta de falha que foram marcadas como falhas devido a um tempo limite (procure mensagens do formulário &quot;Arquivo não processado após um período significativo, marcando como falha!&quot;) no log de falha), é aconselhável verificar a pasta de resultados (e também a própria pasta de falha para outra entrada para a mesma entrada) para verificar se qualquer um dos eventos descritos anteriormente ocorreu realmente.

* **deleteExpirouStageFileOnlyWhenThrottled (Boolean, padrão verdadeiro):** Se o mecanismo de expiração deve ativar somente quando a pasta de observação for acelerada. O mecanismo é mais relevante para pastas de relógio limitadas, pois um pequeno número de arquivos que permanecem em um estado não processado (devido a falhas intermitentes de trabalho/fluxo de trabalho) tem o potencial de sufocar o processamento para todo o lote quando a limitação está habilitada. Se essa propriedade for mantida como true (o padrão), o mecanismo de expiração não será ativado para pastas de observação que não são limitadas. Se a propriedade for mantida como falsa, o mecanismo sempre será ativado, desde que a propriedade stageFileExpirationDuration seja um número positivo.

* **pollInterval (Longo)**: O intervalo em segundos para verificar a entrada da Pasta assistida. A menos que a configuração Throttle esteja ativada, o Intervalo de pesquisa deve ser maior que o tempo para processar um trabalho médio; caso contrário, o sistema poderá ficar sobrecarregado. O valor padrão é 5. Consulte a descrição do Tamanho do Lote para obter mais informações. O valor do intervalo de pesquisa deve ser maior ou igual a um.
* **excludeFilePattern (String)**: Uma lista de padrões delimitada por ponto e vírgula (;) que uma Pasta assistida usa para determinar quais arquivos e pastas serão examinados e coletados. Qualquer arquivo ou pasta com esse padrão não é verificado para processamento. Essa configuração é útil quando a entrada é uma pasta com vários arquivos. O conteúdo da pasta pode ser copiado para uma pasta com um nome que é selecionado pela Pasta assistida. Isso impede que a Pasta assistida escolha uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada. O valor padrão é nulo.
Você pode usar [padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) para excluir:

   * Arquivos com extensões de nome de arquivo específicas; por exemplo, *.dat, *.xml, .pdf, *.*
   * Arquivos com nomes específicos; por exemplo, data* excluiria arquivos e pastas nomeados como data1, data2 e assim por diante.
   * Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

      * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: Uma lista de padrões delimitada por ponto e vírgula (;) que a Pasta assistida usa para determinar quais pastas e arquivos digitalizar e coletar. Por exemplo, se IncludeFilePattern for input*, todos os arquivos e pastas que correspondem a input* serão selecionados. Isso inclui arquivos e pastas chamados input1, input2 e assim por diante. O valor padrão é * e indica todos os arquivos e pastas. Você pode usar padrões de arquivo para incluir:

   * Arquivos com extensões de nome de arquivo específicas; por exemplo, *.dat, *.xml, .pdf, *.*
   * Arquivos com nomes específicos; por exemplo, dados .* incluiria arquivos e pastas chamados data1, data2 e assim por diante.

* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Longo)**: O tempo, em milissegundos, para aguardar antes de digitalizar uma pasta ou arquivo depois que ele for criado. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado um minuto atrás, esse arquivo será selecionado após 59 ou mais minutos terem passado. O valor padrão é 0. Essa configuração é útil para garantir que um arquivo ou pasta seja copiado completamente para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o arquivo levar dez minutos para ser baixado, defina o tempo de espera como 10*60 *1000 milissegundos. Isso impede que a Pasta assistida verifique o arquivo se ele não tiver dez minutos.
* **purgeDuration (Longo)**: Os arquivos e pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Essa configuração é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que nunca excluir a pasta de resultados. O valor padrão é -1.
* **resultFolderName (String)**: A pasta onde os resultados salvos são armazenados. Se os resultados não forem exibidos nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e são salvos na pasta de falha. Esse valor pode ser um caminho absoluto ou relativo com os seguintes padrões de arquivo:

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
   * %l = milissegundos
   * %R = número aleatório (entre 0 e 9)
   * %P = id de processo ou tarefa
   Por exemplo, se for 8 PM em 17 de julho de 2009 e você especificar C:/Test/WF0/failure/%Y/%M/%D/%H/, a pasta de resultado será C:/Test/WF0/failure/2009/07/17/20

   Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da Pasta assistida. O valor padrão é result/%Y/%M/%D/, que é a pasta Result dentro da Pasta Assistida. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Quanto menor for o tamanho das pastas de resultados, melhor será o desempenho da Pasta assistida. Por exemplo, se a carga estimada para a Pasta Assistida for de 1000 arquivos a cada hora, tente um padrão como resultado/%Y%M%D%H para que uma nova subpasta seja criada a cada hora. Se a carga for menor (por exemplo, 1000 arquivos por dia), você poderá usar um padrão como resultado/%Y%M%D.

* **failureFolderName (String)**: A pasta onde os arquivos de falha são salvos. Esse local é sempre relativo à Pasta assistida. Você pode usar padrões de arquivo, conforme descrito para Pasta de resultados. Arquivos somente leitura não são processados e são salvos na pasta de falha. O valor padrão é falha/%Y/%M/%D/.
* **preserveFolderName (String):** o local onde os arquivos são armazenados após o processamento bem-sucedido. O caminho pode ser absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito para Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.
* **batchSize (Long)**: O número de arquivos ou pastas a serem coletados por varredura. Utilização para evitar sobrecarga no sistema; a varredura de muitos arquivos de uma vez pode causar uma falha. O valor padrão é 2.

   As configurações Intervalo de pesquisa e Tamanho do lote determinam quantos arquivos a Pasta assistida recebe em cada verificação. A Pasta assistida usa um conjunto de encadeamentos do Quartz para digitalizar a pasta de entrada. O conjunto de threads é compartilhado com outros serviços. Se o intervalo de varredura for pequeno, os threads verificarão a pasta de entrada com frequência. Se os arquivos forem soltos com frequência na Pasta assistida, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de varredura maior para que os outros serviços possam usar os threads.

   Se houver um grande volume de arquivos sendo descartados, torne o tamanho do lote grande. Por exemplo, se o serviço iniciado pelo endpoint Pasta assistida puder processar 700 arquivos por minuto e os usuários soltarem arquivos na pasta de entrada na mesma taxa, em seguida, definir o Tamanho do lote como 350 e o Intervalo de pesquisa como 30 segundos ajudará no desempenho da Pasta assistida sem incorrer no custo de varredura da Pasta assistida com muita frequência.

   Quando os arquivos são soltos na Pasta assistida, ela lista os arquivos na entrada, o que pode reduzir o desempenho se a varredura estiver acontecendo a cada segundo. Aumentar o intervalo de varredura pode melhorar o desempenho. Se o volume de arquivos que está sendo descartado for pequeno, ajuste o Tamanho do lote e o Intervalo de pesquisa de acordo. Por exemplo, se 10 arquivos forem descartados a cada segundo, tente definir o pollInterval como 1 segundo e o Tamanho do lote como 10

* **throttleOn (Booleano)**: Quando essa opção é selecionada, ela limita o número de trabalhos de Pasta assistida que o AEM Forms processa em um determinado momento. O número máximo de tarefas é determinado pelo valor Tamanho do Lote. O valor padrão é true. (Consulte [Sobre a limitação](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (Booleano)**: Quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como Falso, os arquivos e pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.
* **preserveOnFailure (Booleano)**: Preservar arquivos de entrada em caso de falha na execução da operação em um serviço. O valor padrão é true.
* **inputFilePattern (String)**: Especifica o padrão dos arquivos de entrada para uma Pasta assistida. Cria uma lista de permissões dos arquivos.
* **asynch (booleano)**: Identifica o tipo de invocação como assíncrona ou síncrona. O valor padrão é true (assíncrono). O processamento de arquivos é uma tarefa que consome recursos, mantenha o valor do sinalizador asynch como true para evitar o bloqueio do thread principal do trabalho de varredura. Em um ambiente em cluster, é essencial manter o sinalizador true para permitir o balanceamento de carga para os arquivos que estão sendo processados nos servidores disponíveis. Se o sinalizador for falso, o trabalho de varredura tentará executar o processamento para cada arquivo/pasta de nível superior sequencialmente em seu próprio thread. Não defina o sinalizador como falso sem um motivo específico, como processamento baseado em fluxo de trabalho em uma configuração de servidor único.

>[!NOTE]
>
>Por design, os fluxos de trabalho são assíncronos. Mesmo que você defina o valor como false, os workflows serão iniciados no modo assíncrono.

* **ativado (booleano)**: Desativa e ativa a verificação de uma Pasta assistida. Defina ativado como verdadeiro, para começar a digitalizar a Pasta assistida. O valor padrão é true.
* **payloadMapperFilter:** quando uma pasta é configurada como pasta assistida, uma estrutura de pasta é criada na pasta assistida. A estrutura tem pastas para fornecer entradas, receber saídas (resultados), salvar dados para falhas, preservar dados para processos de longa duração e salvar dados para vários estágios. A estrutura de pastas de uma Pasta assistida pode servir como uma carga de fluxos de trabalho centrados no Forms. Um mapeador de carga permite definir a estrutura de uma carga que usa uma Pasta assistida para entrada, saída e processamento. Por exemplo, se você usar o mapeador padrão, ele mapeará o conteúdo da Pasta assistida com a pasta [payload]\input e a pasta [payload]\output. Duas implementações prontas para uso do mapeador de carga estão disponíveis. Se você não tiver [uma implementação personalizada](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), use uma implementação pronta para uso:

   * **Mapeador padrão:** use o mapeador de carga padrão para manter o conteúdo de entrada e saída das pastas assistidas em pastas separadas de entrada e saída no payload. Além disso, no caminho de carga de um workflow, use [payload]/input/ e [payload]/output paths para recuperar e salvar o conteúdo.

   * **Mapeador de carga baseado em arquivo simples:** use o mapeador de carga útil baseado em arquivo simples para manter o conteúdo de entrada e saída diretamente na pasta de carga útil. Ela não cria nenhuma hierarquia extra, como o mapeador padrão.

### Parâmetros de configuração personalizada {#custom-configuration-parameters}

Juntamente com as propriedades de configuração da Pasta assistida listadas acima, você também pode especificar parâmetros de configuração personalizados. Os parâmetros personalizados são passados para o código de processamento de arquivos. Ela permite que o código altere seu comportamento com base no valor do parâmetro . Para especificar um parâmetro:

1. Faça logon no CRXDE-Lite e navegue até o nó de configuração da Pasta assistida.
1. Adicione um parâmetro de propriedade.&lt;property_name> para o nó de configuração Pasta assistida. O tipo da propriedade só pode ser Booliano, Date, Decimal, Double, Long e String. É possível especificar propriedades de valor único e múltiplo.

>[!NOTE]
>
>Se o tipo de dados da propriedade for Double, especifique um ponto decimal no valor dessas propriedades. Para todas as propriedades, onde o tipo de dados é Double e nenhum ponto decimal é especificado no valor, o tipo é convertido em Long.

Essas propriedades são passadas como um mapa imutável do tipo Map&lt;String, Object> para o código de processamento. O código de processamento pode ser um ECMAScript, Workflow ou um Serviço. Os valores fornecidos para as propriedades estão disponíveis como pares de valores chave no mapa. Chave é o nome da propriedade e valor é o valor da propriedade. Para obter mais informações sobre parâmetros de configuração personalizados, consulte a seguinte imagem:

![Um exemplo de nó de configuração de pasta de observação com propriedades obrigatórias, algumas propriedades opcionais, alguns parâmetros de configuração](assets/custom-configuration-parameters.png)

Um exemplo de nó de configuração de pasta de observação com propriedades obrigatórias, algumas propriedades opcionais, alguns parâmetros de configuração.

#### Variáveis mutáveis para fluxos de trabalho {#mutable-variables-for-workflows}

Você pode criar variáveis mutáveis para métodos de processamento de arquivos baseados em fluxo de trabalho. Essas variáveis servem como contêineres para os dados que fluem entre as etapas de um fluxo de trabalho. Para criar essas variáveis:

1. Faça logon no CRXDE-Lite e navegue até o nó de configuração da Pasta assistida.

1. Adicione uma propriedade workflow.var.&lt;variable_name> para o nó de configuração Pasta assistida.

   O tipo da propriedade só pode ser Booliano, Date, Decimal, Double, Long e String. Propriedades com vários valores também são compatíveis. Para propriedades com vários valores, o valor disponível para a etapa do fluxo de trabalho é uma matriz do tipo especificado.

   >[!NOTE]
   >
   >Se o tipo de dados da propriedade for Double, especifique um ponto decimal no valor dessas propriedades. Para todas as propriedades, onde o tipo de dados é Double e nenhum ponto decimal é especificado no valor, o tipo é convertido em Long.

>[!NOTE]
>
>A especificação JCR exige um valor padrão para as propriedades. Os valores padrão estão disponíveis para as etapas de um fluxo de trabalho para processamento. Portanto, especifique os valores padrão adequados.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Vários métodos de processamento de arquivos {#variousmethodsforprocessingfiles}

Você pode iniciar um fluxo de trabalho, serviço ou script para processar os locais dos documentos em uma pasta monitorada.

### Usar um serviço para processar arquivos de uma pasta assistida   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Um Serviço é uma implementação personalizada da interface `com.adobe.aemfd.watchfolder.service.api.ContentProcessor`. Ele é registrado no OSGi junto com algumas propriedades personalizadas. As propriedades personalizadas da implementação a tornam exclusiva e ajudam a identificar a implementação.

#### Implementação personalizada da interface ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

A implementação personalizada aceita um contexto de processamento (um objeto do tipo com.adobe.aemfd.watchfolder.service.api.ProcessorContext), lê documentos de entrada e parâmetros de configuração do contexto, processa as entradas e adiciona a saída de volta ao
contexto. O ProcessorContext tem as seguintes APIs:

* **getWatchFolderId**: Retorna a ID da pasta assistida.
* **getInputMap**: Retorna um mapa do tipo Mapa. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* **getConfigParameters**: Retorna um mapa imutável do tipo Mapa. O mapa contém
os parâmetros de configuração de uma Pasta assistida.

* **setResult**: A implementação ContentProcessor usa a API para gravar o documento de saída na pasta de resultados. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo da pasta de saída/padrão de arquivo especificado. Se um padrão de pasta for especificado, os arquivos de saída terão nomes como descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes como descrito em padrão de arquivo.

Por exemplo, o código a seguir é uma implementação personalizada da interface ContentProcessor com uma propriedade foo=bar personalizada.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

Ao [configurar uma Pasta assistida](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), se você especificar a propriedade inputProcessorId como (foo=bar) e a propriedade inputProcessorType como Serviço, o Serviço mencionado acima (implementação personalizada) será usado para processar os arquivos de entrada da Pasta assistida.

O exemplo a seguir também é uma implementação personalizada da interface ContentProcessor . No exemplo, o Serviço aceita arquivos de entrada, copia os arquivos para um local temporário e retorna um objeto de documento com o conteúdo do arquivo. O conteúdo do objeto de documento é salvo na pasta de resultados. O caminho físico da pasta de resultados é configurado no [nó de configuração da Pasta assistida](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### Como usar scripts para processar arquivos de uma pasta assistida {#using-scripts-to-process-files-of-a-watched-folder}

Scripts são o código personalizado de reclamação do ECMAScript gravado em processos de documentos colocados na Pasta assistida. Um script é representado como um nó JCR. Além das variáveis padrão do ECMAScript (log, sling e muito mais), o Script tem uma variável processorContext. A variável é do tipo ProcessorContext. O ProcessorContext tem as seguintes APIs:

* **getWatchFolderId**: Retorna a ID da pasta assistida.
* **getInputMap**: Retorna um mapa do tipo Mapa. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* **getConfigParameters**: Retorna um mapa imutável do tipo Mapa. O mapa contém os parâmetros de configuração de uma Pasta assistida.
* **setResult**: A implementação ContentProcessor usa a API para gravar o documento de saída na pasta de resultados. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo da pasta de saída/padrão de arquivo especificado. Se um padrão de pasta for especificado, os arquivos de saída terão nomes como descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes como descrito em padrão de arquivo.

O código a seguir é um exemplo de ECMAScript. Ele aceita arquivos de entrada, copia os arquivos para um local temporário e retorna um objeto de documento com o conteúdo do arquivo. O conteúdo do objeto de documento é salvo na pasta de resultados. O caminho físico da pasta de resultados é configurado no [nó de configuração da Pasta assistida](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>A pasta de saída e o prefixo do nome do arquivo são decididos com base nos parâmetros de configuração da Pasta assistida.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Localização de scripts e considerações de segurança {#location-of-scripts-and-security-considerations}

Por padrão, uma pasta de contêiner (/etc/fd/watchfolder/scripts) é fornecida, onde os clientes podem colocar seus scripts, e o usuário de serviço padrão usado pela estrutura de pastas de observação tem as permissões necessárias para ler scripts desse local.

Se você planeja colocar seus scripts em um local personalizado, é provável que o usuário do serviço padrão não tenha permissões de leitura sobre o local personalizado. Para esse cenário, execute as seguintes etapas para fornecer as permissões necessárias para o local personalizado:

1. Crie um usuário do sistema programaticamente ou por meio do console https://&#39;[server]:[port]&#39;/crx/explorer. Você também pode usar um usuário do sistema existente. É importante trabalhar com os usuários do sistema aqui, em vez dos usuários normais.
1. Forneça permissões de leitura ao usuário do sistema recém-criado ou existente no local personalizado onde os scripts são armazenados. Você pode ter vários locais personalizados. Forneça ao menos permissões de leitura para todos os locais personalizados.
1. No console de configuração do Felix (/system/console/configMgr), localize o mapeamento do usuário do serviço para as pastas de observação. Esse mapeamento se parece com &#39;Mapeamento: adobe-aemds-core-watch-folder=..&#39;.
1. Clique no mapeamento. Para a entrada &#39;adobe-aemds-core-watch-folder:scripts=fd-service&#39;, altere fd-service para a ID do usuário do sistema personalizado. Clique em Salvar.

Agora, você pode usar o local personalizado configurado para salvar os scripts.

### Usar um fluxo de trabalho para processar arquivos de uma pasta assistida {#using-a-workflow-to-process-files-of-a-watched-folder}

Os workflows permitem automatizar as atividades do Experience Manager. Os workflows consistem em uma série de etapas executadas em uma ordem específica. Cada etapa realiza uma atividade distinta, como ativar uma página ou enviar uma mensagem de email. Os workflows podem interagir com ativos no repositório, contas de usuário e serviços de Experience Manager. Portanto, os fluxos de trabalho podem coordenar processos complicados.

* Antes de criar um workflow, considere os seguintes pontos:
* A saída de uma etapa deve estar disponível para todas as etapas subsequentes.
As etapas devem ser capazes de atualizar (ou até excluir) as saídas existentes geradas pelas etapas anteriores.
* As variáveis mutáveis são usadas para continuar os dados dinâmicos personalizados entre as etapas.

Execute as seguintes etapas para processar arquivos usando workflows:

1. Crie uma implementação da interface `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`. É semelhante à implementação criada para um Serviço.

   >[!NOTE]
   >
   >Você pode criar a implementação completa totalmente no ECMAScript.

1. Em uma etapa do Fluxo de trabalho, localize o serviço OSGi do tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService e chame o método execute() do serviço com os seguintes argumentos.

   * Sua implementação personalizada da interface WorkflowContextProcessor
   * workItem
   * workflowSession
   * metadados

Se você usar a linguagem de programação Java para implementar o fluxo de trabalho, o mecanismo de fluxo de trabalho AEM fornecerá valor para variáveis workItem, workflowSession e metadados. Essas variáveis são passadas como argumentos para o método execute() de sua implementação personalizada do WorkflowProcess.

Se você usar o ECMAScript para implementar o workflow, o mecanismo de workflow AEM fornecerá valor para graniteWorkItem, graniteWorkflowSession e variáveis de metadados. Essas variáveis são passadas como argumentos para o método WorkflowContextService.execute() .

O argumento para processWorkflowContext() é um objeto do tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. A interface WorkflowContext tem as seguintes APIs para facilitar as considerações específicas do fluxo de trabalho mencionadas acima:

* getWorkItem: Retorna o valor da variável WorkItem. As variáveis são passadas para o método WorkflowContextService.execute() .
* getWorkflowSession: Retorna o valor da variável WorkflowSession. As variáveis são passadas para o método WorkflowContextService.execute() .
* getMetadata: Retorna o valor da variável Metadados . As variáveis são passadas para o método WorkflowContextService.execute() .
* getCommitedVariables: Retorna um mapa de objetos somente leitura que representa variáveis definidas pelas etapas anteriores. Se uma variável não for modificada em nenhuma das etapas anteriores, o valor padrão especificado durante a configuração da Pasta assistida será retornado.
* getCommitedResults: Retorna um Mapa de documentos somente leitura. O mapa representa os arquivos de saída gerados pelas etapas anteriores.
* setVariable: A implementação WorkflowContextProcessor usa a variável para manipular as variáveis que representam os dados dinâmicos personalizados que fluem entre as etapas. O nome e o tipo das variáveis são idênticos ao nome das variáveis especificadas durante [configurar a Pasta assistida](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). Para alterar o valor de uma variável, chame a API setVariable com um valor não nulo. Para remover uma variável, chame setVariable() com um valor nulo.

As seguintes APIs ProcessorContext também estão disponíveis:

* getWatchFolderId: Retorna a ID da pasta assistida.
* getInputMap: Retorna um mapa do tipo Mapa&lt;Cadeia de caracteres, Documento>. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* getConfigParameters: Retorna um mapa imutável do tipo Map&lt;String, Object>. O mapa contém os parâmetros de configuração de uma Pasta assistida.
* setResult: A implementação ContentProcessor usa a API para gravar o documento de saída na pasta de resultados. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo da pasta de saída/padrão de arquivo especificado. Se um padrão de pasta for especificado, os arquivos de saída terão nomes como descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes como descrito no padrão de arquivo

Consideração para a API setResult, quando usada em workflows:

* Para adicionar um novo documento de saída que contribua para a saída geral do workflow, chame a API setResult com um nome de arquivo que não tenha sido usado como nome de arquivo de saída por qualquer etapa anterior.
* Para atualizar uma saída gerada por uma etapa anterior, chame a API setResult com um nome de arquivo já usado por uma etapa anterior.
* Para excluir uma saída gerada por uma etapa anterior, chame setResult com um nome de arquivo já usado por uma etapa anterior e null como conteúdo.

>[!NOTE]
>
>Chamar a API setResult com conteúdo nulo em qualquer outro cenário resultaria em um erro.

O exemplo a seguir é implementado como uma etapa do fluxo de trabalho. No exemplo, o ECMAscript usa uma variável stepCount para rastrear o número de vezes que uma etapa é chamada na instância do fluxo de trabalho atual.
O nome da pasta de saída é uma combinação do número da etapa atual, do nome do arquivo original e do prefixo especificado no parâmetro outPrefix .

O ECMAScript recebe uma referência do serviço de contexto do workflow e cria uma implementação da interface WorkflowContextProcessor . A implementação WorkflowContextProcessor aceita arquivos de entrada, copia o arquivo para um local temporário e retorna um documento representando o arquivo copiado. Com base no valor da variável Booliana purgePrevious, a etapa atual exclui a saída gerada pela última vez pela mesma etapa em que a etapa foi iniciada na instância de fluxo de trabalho atual. No fim, o método wfSvc.execute é chamado para executar a implementação WorkflowContextProcessor . O conteúdo do documento de saída é salvo na pasta de resultados no caminho físico mencionado no nó de configuração da Pasta assistida.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### Criar filtro de mapeador de carga para mapear a estrutura de uma pasta assistida para a carga de um fluxo de trabalho {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Ao criar uma pasta assistida, ela cria uma estrutura de pastas dentro da pasta que está sendo assistida. A estrutura de pastas tem pastas de estágio, resultado, preservação, entrada e falha. A estrutura de pastas pode servir como carga de entrada para o workflow e aceitar a saída de um workflow. Também pode listar pontos de falha, se houver.

Se a estrutura de uma carga for diferente da estrutura da pasta assistida, você poderá gravar scripts personalizados para mapear a estrutura da pasta assistida para a carga. Esse script é chamado de filtro de mapeador de carga. Pronto para uso, o AEM Forms fornece um filtro de mapeamento de carga para mapear a estrutura da pasta assistida para uma carga útil.

#### Criação de um filtro personalizado de mapeador de carga {#creating-a-custom-payload-mapper-filter}

1. Baixe [Adobe Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Configure o SDK do cliente no caminho de compilação do projeto baseado em maven. Para começar, você pode baixar e abrir o seguinte projeto baseado em maven no IDE de sua escolha.
1. Edite o código de filtro do mapeador de carga disponível no conjunto de amostras para atender aos seus requisitos.
1. Use maven para criar um pacote do Filtro personalizado do Mapeador de Carga.
1. Use [AEM console de pacotes](https://localhost:4502/system/console/bundles) para instalar o pacote.

   Agora, o Filtro personalizado do Mapeador de Carga está listado AEM interface do usuário da pasta assistida. Você pode usá-lo com seu fluxo de trabalho.

   O código de exemplo a seguir implementa um mapeador simples baseado em arquivo para os arquivos salvos em relação a uma carga útil. Você pode usá-lo para começar.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## Como os usuários interagem com uma pasta assistida {#how-users-interact-with-a-watched-folder}

Para um endpoint de Pasta assistida, os usuários podem iniciar operações de processamento de arquivos copiando ou arrastando arquivos de entrada ou pastas de suas áreas de trabalho para uma Pasta assistida. Os arquivos são processados na ordem de chegada.

Para endpoints de Pastas vigiadas, se um trabalho exigir apenas um arquivo de entrada, o usuário poderá copiar esse arquivo para a raiz da Pasta assistida.

Se o trabalho contiver mais de um arquivo de entrada, o usuário deverá criar uma pasta fora da hierarquia de Pastas vigiadas que contenha todos os arquivos necessários. Essa nova pasta deve incluir os arquivos de entrada (e, opcionalmente, um arquivo DDX, se exigido pelo processo). Depois que a pasta de trabalho for construída, o usuário a copiará na pasta de entrada da Pasta assistida.

>[!NOTE]
>
>Verifique se o servidor de aplicativos excluiu o acesso aos arquivos na Pasta assistida. Se o AEM Forms não conseguir excluir os arquivos da pasta de entrada após a verificação, o processo associado será iniciado indefinidamente.

## Informações adicionais sobre as Pastas vigiadas {#additional-information-about-the-watched-folders}

### Sobre o controle {#about-throttling}

Quando o controle está ativado para um endpoint da pasta monitorada, ele limita o número de trabalhos da Pasta monitorada que são processados em um determinado momento. O número máximo de tarefas é determinado pelo valor Tamanho do Lote, também configurável no endpoint Pasta Assistida. Quando o limite de limitação é atingido, os documentos de entrada no diretório de entrada da Pasta assistida não são sondados. O documento também permanece no diretório de entrada até que outros trabalhos de Pasta assistida sejam concluídos e outra tentativa de pesquisa seja feita. Para processamento síncrono, todas as tarefas processadas em uma única pesquisa são contadas em direção ao limite de limitação, mesmo que as tarefas sejam processadas consecutivamente em um único thread.

>[!NOTE]
>
>A limitação não é dimensionada com um cluster. Quando a limitação estiver ativada, o cluster como um todo não processará mais do que o número de tarefas especificado no Tamanho do Lote em um determinado momento. Esse limite é de todo o cluster e não é específico para cada nó no cluster. Por exemplo, com um Tamanho de Lote de 2, o limite de limitação poderia ser atingido com um único nó processando duas tarefas, e nenhum outro nó sondaria o diretório de entrada até que uma das tarefas fosse concluída.

#### Como funciona o controle {#how-throttling-works}

A Pasta assistida verifica a pasta de entrada em cada pollInterval, seleciona o número de arquivos especificados no Tamanho do lote e chama o serviço de destino para cada um desses arquivos. Por exemplo, se o Tamanho do Lote for quatro, em cada varredura, a Pasta Assistida selecionará quatro arquivos, criará quatro solicitações de invocação e chamará o serviço de destino. Antes que essas solicitações sejam concluídas, se a Pasta assistida for invocada, ela reiniciará quatro trabalhos, independentemente de as quatro tarefas anteriores serem concluídas ou não.

A limitação impede que a pasta assistida chame novos trabalhos quando os trabalhos anteriores não estiverem concluídos. A Pasta assistida detecta trabalhos em andamento e processa novos trabalhos com base no tamanho do lote menos os trabalhos em andamento. Por exemplo, na segunda invocação , se o número de trabalhos concluídos for apenas três e uma tarefa ainda estiver em andamento, a Pasta assistida chamará apenas mais três trabalhos.

* A Pasta assistida depende do número de arquivos presentes na pasta de estágio para descobrir quantas tarefas estão em andamento. Se os arquivos permanecerem não processados na pasta de preparo, a Pasta assistida não chamará mais tarefas. Por exemplo, se o tamanho do lote for quatro e três trabalhos estiverem paralisados, a Pasta assistida chamará apenas um trabalho em invocações subsequentes. Há vários cenários que podem fazer com que os arquivos permaneçam não processados na pasta de preparo. Quando as tarefas são paralisadas, o administrador pode encerrar o processo na página de administração do Process Management para que a Pasta assistida mova os arquivos para fora da pasta de preparo.
* Se o servidor do AEM Forms ficar inativo antes que a Pasta assistida chame as tarefas, o administrador poderá mover os arquivos para fora da pasta de preparo. Para obter informações, consulte [Pontos de falha e recuperação](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Se o servidor do AEM Forms estiver em execução, mas a Pasta assistida não estiver em execução quando o serviço do Gerenciador de trabalhos retornar, o que ocorre quando os serviços não iniciam na sequência ordenada, o administrador pode mover os arquivos para fora da pasta de palco. Para obter informações, consulte [Pontos de falha e recuperação](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Pontos de falha e recuperaçãoPontos de falha e recuperação {#failure-points-and-recoveryfailure-points-and-recovery}

Em cada evento de pesquisa, a Pasta assistida bloqueia a pasta de entrada, move os arquivos que correspondem ao padrão de arquivo de inclusão para a pasta do palco e, em seguida, desbloqueia a pasta de entrada. O bloqueio é necessário para que dois threads não captem o mesmo conjunto de arquivos e os processem duas vezes. As chances de isso acontecer aumentam com um pequeno pollInterval e um grande lote. Depois que os arquivos são movidos para a pasta de preparo, a pasta de entrada é desbloqueada para que outros threads possam digitalizar a pasta. Esta etapa ajuda a fornecer alta taxa de transferência, pois outros threads podem digitalizar enquanto um thread está processando os arquivos.

Depois que os arquivos são movidos para a pasta do estágio, as solicitações de invocação são criadas para cada arquivo e o serviço de destino é chamado. Pode haver casos em que a Pasta assistida não possa recuperar os arquivos na pasta de estágio:

* Se o servidor ficar inativo antes que a Pasta assistida possa criar a solicitação de invocação, os arquivos na pasta de estágio permanecerão na pasta de estágio e não serão recuperados.

* Se a Pasta assistida tiver criado com êxito a solicitação de invocação para cada um dos arquivos na pasta de estágio e o servidor falhar, há dois comportamentos com base no tipo de invocação:

   * **Síncrono**: Se a Pasta assistida estiver configurada para invocar o serviço de forma síncrona, todos os arquivos na pasta de preparo permanecerão não processados na pasta de preparo.
   * **Assíncrono**: Nesse caso, a Pasta assistida depende do serviço Gerenciador de trabalhos . Se o Serviço do Gerenciador de Tarefas retornar a Pasta Assistida, os arquivos na pasta do estágio serão movidos para a pasta de preservação ou falha com base nos resultados da invocação. Se o serviço Gerenciador de trabalhos não retornar a chamada de Pasta assistida, os arquivos permanecerão não processados na pasta de preparo. Essa situação acontece quando a Pasta assistida não está em execução quando o Gerenciador de trabalhos retorna a chamada.

#### Recuperar arquivos de origem não processados na pasta de preparo {#recover-unprocessed-source-files-in-the-stage-folder}

Quando a Pasta assistida não puder processar os arquivos de origem na pasta de estágio, você poderá recuperar os arquivos não processados.

1. Reinicie o servidor ou nó de aplicativos.

1. Interrompa a Pasta Assistida de processar novos arquivos de entrada. Se ignorar esta etapa, será muito mais difícil determinar quais arquivos não serão processados na pasta de preparo. Para impedir que a Pasta assistida processe novos arquivos de entrada, execute uma das seguintes tarefas:

   * Altere a propriedade includeFilePattern da Pasta assistida para algo que não corresponderá a nenhum dos novos arquivos de entrada (por exemplo, insira NOMATCH).
   * Suspenda o processo que está criando novos arquivos de entrada.
   Aguarde até que o AEM Forms recupere e processe todos os arquivos. A maioria dos arquivos deve ser recuperada e todos os novos arquivos de entrada processados corretamente. O tempo que você espera que a Pasta assistida recupere e processe os arquivos dependerá da duração da operação a ser chamada e do número de arquivos a serem recuperados.

1. Determine quais arquivos não podem ser processados. Se você esperou um tempo adequado e concluiu a etapa anterior e ainda houver arquivos não processados na pasta do palco, vá para a próxima etapa.

   >[!NOTE]
   >
   >Você pode verificar a data e a hora dos arquivos no diretório stage. Dependendo do número de arquivos e do tempo normal de processamento, você pode determinar quais arquivos são antigos o suficiente para serem considerados presos.

1. Copie os arquivos não processados do diretório stage para o diretório de entrada.

1. Se você tiver impedido a Pasta assistida de processar novos arquivos de entrada na etapa 2, altere o Padrão de inclusão de arquivo para seu valor anterior ou reative o processo que você desativou.

### Pastas assistidas em cadeia juntas {#chain-watched-folders-together}

Pastas vigiadas podem ser encadeadas juntas para que um documento de resultado de uma Pasta assistida seja o documento de entrada da próxima Pasta assistida. Cada pasta assistida pode chamar um serviço diferente. Ao configurar Pastas vigiadas dessa maneira, vários serviços podem ser chamados. Por exemplo, uma Pasta assistida poderia converter arquivos PDF para Adobe PostScript® e uma segunda Pasta assistida poderia converter os arquivos PostScript para o formato PDF/A. Para fazer isso, basta definir a pasta de resultados da Pasta assistida definida pelo primeiro endpoint para apontar para a pasta de entrada da Pasta assistida definida pelo segundo endpoint.

A saída da primeira conversão seria para \path\result. A entrada para a segunda conversão seria \path\result, e a saída da segunda conversão seria para \path\result\result  (ou o diretório que você definiu na caixa Pasta de resultados para a segunda conversão).

### Padrões de arquivo e pasta {#file-and-folder-patterns}

Os administradores podem especificar o tipo de arquivo que pode chamar um serviço. Vários padrões de arquivo podem ser estabelecidos para cada Pasta assistida. Um padrão de arquivo pode ser uma das seguintes propriedades de arquivo:

* Arquivos com extensões de nome de arquivo específicas; por exemplo, *.dat, *.xml, .pdf, *.*
* Arquivos com nomes específicos; por exemplo, dados .*
* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * *.[dD][Aa]&#39;port&#39;
   * *.[Xx][Mm][Ll]

* O administrador pode definir o padrão de arquivo da pasta de saída na qual armazenar os resultados. Para as pastas de saída (resultado, preservação e falha), o administrador pode especificar qualquer um desses padrões de arquivo:
* %Y = ano (completo)
* %y = ano (últimos dois dígitos)
* %M = mês,
* %D = dia do mês,
* %d = dia do ano,
* %h = hora,
* %m = minuto,
* %s = segundo,
* %R = número aleatório entre 0 e 9
* %J = Nome do trabalho

Por exemplo, o caminho para a pasta de resultados pode ser C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Os mapeamentos de parâmetros de saída também podem especificar padrões adicionais, como estes:

* %F = Nome do Arquivo de Origem
* %E = Extensão de Nome de Arquivo de Origem

Se o padrão de mapeamento do parâmetro de saída terminar com &quot;File.separator&quot; (que é o separador de caminho), uma pasta será criada e o conteúdo será copiado para essa pasta. Se o padrão não terminar com &quot;File.separator&quot;, o conteúdo (arquivo de resultado ou pasta) será criado com esse nome.

## Uso do PDF Generator com uma pasta assistida {#using-pdf-generator-with-a-watched-folder}

Você pode configurar uma Pasta assistida para iniciar um fluxo de trabalho, serviço ou script para processar os arquivos de entrada. Na seção a seguir, vamos configurar uma Pasta assistida para iniciar um ECMAScript. O ECMAScript usaria o PDF Generator para converter documentos do Microsoft Word (.docx) em documentos PDF.

Execute as seguintes etapas para configurar uma Pasta assistida com PDF Generator:

1. [Criar um ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Criar um workflow](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configurar a pasta assistida](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Criar um ECMAScript {#create-an-ecmascript}

O ECMAScript usaria a API createPDF do PDF Generator para converter documentos Microsoft Word (.docx) em documentos PDF. Execute as seguintes etapas para criar o script:

1. Abra o CRXDE lite em uma janela do navegador. O URL é https://&#39;[server]:[port]&#39;/crx/de.

1. Navegue até /etc/workflow/scripts e crie uma pasta chamada PDFG.

1. Na pasta PDFG, crie um arquivo chamado pdfg-openOffice-sample.ecma e adicione o seguinte código ao arquivo:

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. Salve e feche o arquivo.

### Criar um workflow {#create-a-workflow}

1. Abra AEM interface do usuário do fluxo de trabalho em uma janela do navegador.
https://[servername]:&#39;port&#39;/workflow

1. Na exibição Modelos, clique em **Novo**. Na caixa de diálogo Novo fluxo de trabalho , especifique **Título** e clique em **OK**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Selecione o workflow recém-criado e clique em **Edit**. O workflow é aberto em uma nova janela.

1. Exclua a etapa padrão do fluxo de trabalho. Arraste e solte a Etapa do processo do Sidekick para o Fluxo de trabalho.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Clique com o botão direito do mouse na Etapa do processo e selecione **Editar**. A janela Propriedades da etapa é exibida.

1. Na guia Process , selecione o ECMAScript. Por exemplo, o script pdfg-openOffice-sample.ecma criado em [Create an ECMAScript](#p-create-an-ecmascript-p). Ative a opção **Handler Advance** e clique em **OK**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurar a pasta assistida {#configure-the-watched-folder}

1. Abra o CRXDE lite em uma janela do navegador. https://&#39;[server]:[port]&#39;/crx/de/

1. Navegue até a pasta /etc/fd/watchfolder/config/ e crie um nó do tipo nt:unstructured.

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Adicione as seguintes propriedades ao nó :

   * folderPath (String): O caminho da pasta a ser digitalizada em intervalos de tempo definidos. A pasta deve estar em um local compartilhado com todos os servidores com acesso total ao servidor.
inputProcessorType (String): O tipo do processo a ser iniciado. Neste tutorial, especifique o workflow.

   * inputProcessorId (String): O comportamento da propriedade inputProcessorId é baseado no valor especificado para a propriedade inputProcessorType. Neste exemplo, o valor da propriedade inputProcessorType é workflow. Assim, para a propriedade inputProcessorId , especifique o seguinte caminho do fluxo de trabalho PDFG: /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (String): Padrão do arquivo de saída. Você pode especificar um padrão de pasta ou arquivo. Se um padrão de pasta for especificado, os arquivos de saída terão nomes como descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes como descrito em padrão de arquivo.
   Além das propriedades obrigatórias mencionadas acima, as Pastas vigiadas também oferecem suporte para algumas propriedades opcionais. Para obter a lista completa e a descrição das propriedades opcionais, consulte [Propriedades da pasta assistida](#watchedfolderproperties).
