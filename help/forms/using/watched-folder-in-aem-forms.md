---
title: Pasta monitorada no AEM Forms
description: Um administrador pode colocar uma pasta em observação e iniciar um fluxo de trabalho, serviço ou operação de script quando um arquivo for colocado na pasta que está sendo monitorada.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '7148'
ht-degree: 0%

---

# Pasta monitorada no AEM Forms{#watched-folder-in-aem-forms}

Um administrador pode configurar uma pasta de rede, conhecida como Pasta monitorada, para que, quando um usuário colocar um arquivo (como um arquivo PDF) na Pasta monitorada, um fluxo de trabalho, serviço ou operação de script pré-configurado seja iniciado para processar o arquivo adicionado. Depois que o serviço executa a operação especificada, ele salva o arquivo de resultado em uma pasta de saída especificada. Para obter mais informações sobre workflow, serviço e script, consulte [Vários métodos de processamento de arquivos](#variousmethodsforprocessingfiles).

## Criar uma pasta monitorada {#create-a-watched-folder}

Você pode usar um dos seguintes métodos para criar uma Pasta monitorada no sistema de arquivos:

* Ao configurar as propriedades de um nó de configuração Pasta monitorada, digite o caminho completo do diretório pai na propriedade folderPath e anexe o nome da Pasta monitorada a ser criada, como mostrado no exemplo a seguir: `C:/MyPDFs/MyWatchedFolder`
A variável `MyWatchedFolder`pasta não existe, o AEM Forms tenta criar a pasta no caminho especificado.

* Crie uma pasta no sistema de arquivos antes de configurar um endpoint de Pasta monitorada e forneça o caminho completo na propriedade folderPath. Para obter informações detalhadas sobre a propriedade folderPath, consulte [Propriedades da pasta monitorada](#watchedfolderproperties).

>[!NOTE]
>
>Em um ambiente em cluster, a pasta usada como uma Pasta monitorada deve ser acessível, gravável e compartilhada no sistema de arquivos ou na rede. Cada instância do servidor de aplicativos do cluster deve ter acesso à mesma pasta compartilhada. No Windows, crie uma unidade de rede mapeada em todos os servidores e especifique o caminho da unidade de rede mapeada na propriedade folderPath.

## Criar nó de configuração da pasta monitorada {#create-watched-folder-configuration-node}

Para configurar uma Pasta monitorada, crie um nó de configuração Pasta monitorada. Execute as seguintes etapas para criar o nó de configuração:

1. Faça logon no CRX-DE lite como administrador e acesse a pasta /etc/fd/watchfolder/config.

1. Criar um nó do tipo `nt:unstructured`. Por exemplo, watchedfolder

   >[!NOTE]
   >
   >O nome do nó Pasta monitorada não pode incluir espaços e caracteres especiais.

1. Adicione as seguintes propriedades ao nó:

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   Para obter uma lista completa de propriedades compatíveis, consulte [Propriedades da pasta monitorada](#watchedfolderproperties).

1. Clique em **Salvar tudo**. Depois que o nó é criado e as propriedades são salvas. A variável `input`, `result`, `failure`, `preserve`, e `stage`as pastas são criadas no caminho especificado no `folderPath` propriedade.

   O job de varredura inicia a varredura da Pasta monitorada em um intervalo de tempo definido.

## Propriedades da pasta monitorada {#watchedfolderproperties}

Você pode configurar as seguintes propriedades para uma Pasta monitorada.

* **folderPath (String)**: O caminho da pasta a ser examinada em intervalos de tempo definidos. Para um ambiente em cluster, a pasta deve estar em um local compartilhado com todos os servidores com acesso total ao servidor. É uma propriedade obrigatória.
* **inputProcessorType (String)**: o tipo do processo a ser iniciado. Você pode especificar um fluxo de trabalho, script ou serviço. É uma propriedade obrigatória.
* **inputProcessorId (String)**: o comportamento da propriedade inputProcessorId é baseado no valor especificado para a propriedade inputProcessorType. É uma propriedade obrigatória. A lista a seguir detalha todos os valores possíveis da propriedade inputProcessorType e o requisito correspondente da propriedade inputProcessorType:

   * Para workflow, especifique o template de workflow a ser executado. Por exemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * Para script, especifique o caminho JCR do script a ser executado. Por exemplo, /etc/fd/watchfolder/test/testScript.ecma
   * Para o serviço, especifique o filtro usado para localizar um serviço OSGi. O serviço é registrado como uma implementação da interface com.adobe.aemfd.watchfolder.service.api.ContentProcessor.

* **runModes (String)**: uma lista separada por vírgulas de modos de execução permitidos para execução do workflow. Alguns exemplos são:

   * autor

   * publicação

   * autor,publicação

   * publicar, autor

>[!NOTE]
>
>Se o servidor que hospeda a Pasta monitorada não tiver nenhum dos modos de execução especificados, a Pasta monitorada sempre será ativada independentemente dos modos de execução no servidor.

* **outputFilePattern (String)**: Padrão do arquivo de saída. Você pode especificar uma pasta ou um padrão de arquivo. Se um padrão de pasta for especificado, os arquivos de saída terão os nomes conforme descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes conforme descrito no padrão de arquivo. [Padrão de arquivo e pasta](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) O também pode especificar uma estrutura de diretório para os arquivos de saída. É uma propriedade obrigatória.

* **stageFileExpirationDuration (Longo, padrão -1)**: O número de segundos de espera antes que um arquivo/pasta de entrada que já tenha sido selecionado para processamento deve ser tratado como tendo expirado e marcado como uma falha. Esse mecanismo de expiração só é ativado quando o valor dessa propriedade é um número positivo.

>[!NOTE]
>
>Mesmo quando uma entrada é marcada como tendo ultrapassado o tempo limite usando esse mecanismo, ela ainda pode estar sendo processada em segundo plano, mas apenas levando mais tempo do que o esperado. Se o conteúdo de entrada foi consumido antes do início do mecanismo de tempo limite, o processamento pode até prosseguir para a conclusão mais tarde e a saída ser despejada na pasta de resultados. Se o conteúdo não foi consumido antes do tempo limite, é muito provável que o processamento expire posteriormente ao tentar consumir o conteúdo, e esse erro também será registrado na pasta de falha para a mesma entrada. Por outro lado, se o processamento da entrada nunca for ativado devido a um erro de disparo intermitente de trabalho/fluxo de trabalho (que é o cenário que o mecanismo de expiração visa resolver), é claro que nenhuma dessas duas eventualidades ocorrerá. Assim, para quaisquer entradas na pasta de falha que foram marcadas como falhas devido a um tempo limite (procure mensagens do formulário &quot;Arquivo não processado após um período significativo, marcando como falha!&quot; no registro de falhas), é aconselhável examinar a pasta de resultados (e também a própria pasta de falhas para outra entrada para a mesma entrada) para verificar se alguma das eventualidades descritas anteriormente realmente ocorreu.

* **deleteExpiredStageFileOnlyWhenThrottled (Booleano, padrão verdadeiro):** Se o mecanismo de expiração deve ser ativado somente quando a pasta observada estiver limitada. O mecanismo é mais relevante para pastas de observação limitadas, pois um pequeno número de arquivos que persistem em um estado não processado (devido a falhas de disparo intermitentes de tarefas/fluxos de trabalho) tem o potencial de obstruir o processamento de todo o lote quando a limitação estiver ativada. Se essa propriedade for mantida como true (o padrão), o mecanismo de expiração não será ativado para pastas de observação que não estão limitadas. Se a propriedade for mantida como false, o mecanismo sempre será ativado, desde que a propriedade stageFileExpirationDuration seja um número positivo.

* **pollInterval (Long)**: o intervalo em segundos para verificar a entrada da Pasta monitorada. A menos que a configuração de Aceleração esteja ativada, o Intervalo de Sondagem deve ser maior que o tempo médio para processar um trabalho; caso contrário, o sistema pode ficar sobrecarregado. O valor padrão é 5. Consulte a descrição do Tamanho do lote para obter informações adicionais. O valor de pollinterval deve ser maior ou igual a um.
* **excludeFilePattern (String)**: uma lista de padrões delimitada por ponto e vírgula (;) que uma Pasta monitorada usa para determinar quais arquivos e pastas serão verificados e selecionados. Qualquer arquivo ou pasta com esse padrão não é examinado para processamento. Essa configuração é útil quando a entrada é uma pasta com vários arquivos. O conteúdo da pasta pode ser copiado para uma pasta com um nome que é selecionado pela Pasta monitorada. Isso impede que a Pasta monitorada selecione uma pasta para processamento antes que ela seja completamente copiada para a pasta de entrada. O valor padrão é nulo.
Você pode usar [padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) para excluir:

   * Arquivos com extensões de nome de arquivo específicas; por exemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Arquivos com nomes específicos; por exemplo, dados&#42; O excluiria arquivos e pastas chamados dados1, dados2 e assim por diante.
   * Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

      * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;
      * &#42;.[dD][Aa]&#39;porta&#39;
      * &#42;.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: uma lista de padrões delimitada por ponto e vírgula (;) que a Pasta monitorada usa para determinar quais pastas e arquivos serão verificados e selecionados. Por exemplo, se IncludeFilePattern for input&#42;, todos os arquivos e pastas que correspondam à entrada&#42; são coletadas. Isso inclui arquivos e pastas chamados input1, input2 e assim por diante. O valor padrão é &#42; e indica todos os arquivos e pastas. Você pode usar padrões de arquivo para incluir:

   * Arquivos com extensões de nome de arquivo específicas; por exemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Arquivos com nomes específicos; por exemplo, dados.&#42; incluiria arquivos e pastas chamados dados1, dados2 e assim por diante.

* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;

      * &#42;.[dD][Aa]&#39;porta&#39;
      * &#42;.[Xx][Mm][Ll]

Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**: o tempo, em milissegundos, que deve ser aguardado antes que você verifique uma pasta ou um arquivo após sua criação. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será selecionado após 59 minutos ou mais. O valor padrão é 0. Essa configuração é útil para garantir que um arquivo ou pasta seja copiado completamente para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o download demorar dez minutos, defina o tempo de espera como 10&#42;60 &#42;1000 milissegundos. Isso impede que a Pasta monitorada verifique o arquivo se ele não tiver dez minutos.
* **purgeDuration (Longo)**: os arquivos e as pastas na pasta de resultados são removidos quando são mais antigos que esse valor. Esse valor é medido em dias. Essa configuração é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que a pasta de resultados nunca deve ser excluída. O valor padrão é -1.
* **resultFolderName (String)**: a pasta onde os resultados salvos são armazenados. Se os resultados não aparecerem nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e são salvos na pasta de falha. Esse valor pode ser um caminho absoluto ou relativo com os seguintes padrões de arquivo:

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

  Por exemplo, se for 8 PM em 17 de julho de 2009 e você especificar C:/Test/WF0/failure/%Y/%M/%D/%H/, a pasta resultante será C:/Test/WF0/failure/2009/07/17/20

  Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da Pasta monitorada. O valor padrão é result/%Y/%M/%D/, que é a pasta Resultado dentro da Pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Quanto menor o tamanho das pastas de resultados, melhor será o desempenho da Pasta monitorada. Por exemplo, se a carga estimada para a Pasta monitorada for de 1000 arquivos a cada hora, tente um padrão como resultado/%Y%M%D%H para que uma nova subpasta seja criada a cada hora. Se a carga for menor (por exemplo, 1000 arquivos por dia), você pode usar um padrão como result/%Y%M%D.

* **failureFolderName (String)**: a pasta onde os arquivos de falha são salvos. Esse local é sempre relativo à Pasta monitorada. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados. Arquivos somente leitura não são processados e são salvos na pasta de falha. O valor padrão é failure/%Y/%M/%D/.
* **preserveFolderName (String):** O local onde os arquivos são armazenados após o processamento bem-sucedido. O caminho pode ser um caminho de diretório absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.
* **batchSize (Long)**: O número de arquivos ou pastas a serem selecionados por verificação. Use para evitar uma sobrecarga no sistema; a verificação de muitos arquivos de uma vez pode causar uma falha. O valor padrão é 2.

  As configurações Intervalo de pesquisa e Tamanho do lote determinam quantos arquivos a Pasta monitorada coleta em cada verificação. A pasta monitorada usa um pool de threads do Quartz para verificar a pasta de entrada. O pool de threads é compartilhado com outros serviços. Se o intervalo de verificação for pequeno, as threads examinam a pasta de entrada com frequência. Se os arquivos forem soltos com frequência na Pasta monitorada, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar as threads.

  Se houver um grande volume de arquivos sendo descartados, aumente o tamanho do lote. Por exemplo, se o serviço iniciado pelo endpoint Pasta monitorada puder processar 700 arquivos por minuto e os usuários soltarem arquivos na pasta de entrada na mesma taxa, definir o Tamanho do lote como 350 e o Intervalo de pesquisa como 30 segundos ajudará no desempenho da Pasta monitorada sem incorrer no custo de verificar a Pasta monitorada com muita frequência.

  Quando os arquivos são soltos na Pasta monitorada, ela lista os arquivos na entrada, o que pode reduzir o desempenho se a varredura estiver ocorrendo a cada segundo. O aumento do intervalo de verificação pode melhorar o desempenho. Se o volume de arquivos que está sendo descartado for pequeno, ajuste o Tamanho do lote e o Intervalo de amostragem de acordo. Por exemplo, se 10 arquivos forem descartados a cada segundo, tente definir pollInterval como 1 segundo e o Tamanho do lote como 10

* **throttleOn (Booleano)**: quando essa opção é selecionada, ela limita o número de trabalhos de Pastas monitoradas que o AEM Forms processa a qualquer momento. O número máximo de trabalhos é determinado pelo valor Tamanho do Lote. O valor padrão é true. (Consulte [Sobre a limitação](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (Booleano)**: quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como False, os arquivos e as pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.
* **preserveOnFailure (Booleano)**: preserva os arquivos de entrada em caso de falha ao executar a operação em um serviço. O valor padrão é true.
* **inputFilePattern (String)**: especifica o padrão dos arquivos de entrada para uma Pasta monitorada. Cria um arquivo de inclui na lista de permissões dos arquivos.
* **assíncrono (Booleano)**: identifica o tipo de invocação como assíncrono ou síncrono. O valor padrão é true (assíncrono). O processamento de arquivos é uma tarefa que consome recursos, mantenha o valor do sinalizador assíncrono como verdadeiro para evitar a obstrução do thread principal do trabalho de verificação. Em um ambiente em cluster, é essencial manter o sinalizador true para permitir o balanceamento de carga para os arquivos que estão sendo processados nos servidores disponíveis. Se o sinalizador for falso, o trabalho de verificação tentará executar o processamento para cada arquivo/pasta de nível superior sequencialmente em seu próprio thread. Não defina o sinalizador como false sem um motivo específico, como processamento baseado em fluxo de trabalho em uma configuração de servidor único.

>[!NOTE]
>
>Por design, os workflows são assíncronos. Mesmo que você defina o valor como false, os workflows serão iniciados no modo assíncrono.

* **ativado (Booleano)**: desativa e ativa a verificação de uma Pasta monitorada. Defina ativado como verdadeiro para iniciar a verificação da Pasta monitorada. O valor padrão é true.
* **payloadMapperFilter:** Quando uma pasta é configurada como pasta monitorada, uma estrutura de pastas é criada dentro da pasta monitorada. A estrutura tem pastas para fornecer entradas, receber saídas (resultados), salvar dados para falhas, preservar dados para processos de longa duração e salvar dados para vários estágios. A estrutura de pastas de uma Pasta monitorada pode servir como uma carga de fluxos de trabalho centrados no Forms. Um mapeador de carga permite definir a estrutura de uma carga que usa uma Pasta monitorada para entrada, saída e processamento. Por exemplo, se você usar o mapeador padrão, ele mapeará o conteúdo da Pasta monitorada com [carga útil]\entrada e [carga útil]\pasta de saída. Duas implementações prontas para uso do mapeador de carga estão disponíveis. Se você não tiver [uma implementação personalizada](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), use uma das implementações prontas para uso:

   * **Mapeador padrão:** Use o mapeador de carga útil padrão para manter os conteúdos de entrada e saída das pastas monitoradas em pastas de entrada e saída separadas na carga útil. Além disso, no caminho de carga de um workflow, use [carga útil]/input/ e [carga útil]/caminhos de saída para recuperar e salvar o conteúdo.

   * **Mapeador de conteúdo simples baseado em arquivo:** Use o mapeador de carga útil baseado em arquivo simples para manter o conteúdo de entrada e saída diretamente na pasta de carga útil. Ela não cria nenhuma hierarquia extra, como o mapeador padrão.

### Parâmetros de configuração personalizados {#custom-configuration-parameters}

Juntamente com as propriedades de configuração da Pasta monitorada listadas acima, você também pode especificar parâmetros de configuração personalizados. Os parâmetros personalizados são passados para o código de processamento do arquivo. Ela permite que o código altere seu comportamento com base no valor do parâmetro. Para especificar um parâmetro:

1. Faça logon no CRXDE-Lite e navegue até o nó de configuração Pasta monitorada.
1. Adicionar um parâmetro de propriedade.&lt;property_name> ao nó de configuração Pasta monitorada. O tipo da propriedade só pode ser Booliano, Date, Decimal, Double, Long e String. Você pode especificar propriedades com um único valor e com vários valores.

>[!NOTE]
>
>Se o tipo de dados da propriedade for Double, especifique um ponto decimal no valor dessas propriedades. Para todas as propriedades, onde o tipo de dados é Double e nenhum ponto decimal é especificado no valor, o tipo é convertido em Long.

Essas propriedades são passadas como um mapa imutável do tipo Mapa&lt;string object=&quot;&quot;> ao código de processamento. O código de processamento pode ser um ECMAScript, Workflow ou um Serviço. Os valores fornecidos para as propriedades estão disponíveis como pares de valores chave no mapa. Chave é o nome da propriedade e valor é o valor da propriedade. Para obter mais informações sobre parâmetros de configuração personalizados, consulte a seguinte imagem:

![Um exemplo de nó de configuração watch-folder com propriedades obrigatórias, algumas propriedades opcionais e alguns parâmetros de configuração](assets/custom-configuration-parameters.png)

Um exemplo de nó de configuração watch-folder com propriedades obrigatórias, algumas propriedades opcionais e alguns parâmetros de configuração.

#### Variáveis mutáveis para fluxos de trabalho {#mutable-variables-for-workflows}

Você pode criar variáveis mutáveis para métodos de processamento de arquivos baseados em fluxo de trabalho. Essas variáveis servem como containers para os dados que fluem entre as etapas de um workflow. Para criar essas variáveis:

1. Faça logon no CRXDE-Lite e navegue até o nó de configuração Pasta monitorada.

1. Adicione uma propriedade workflow.var.&lt;variable_name> ao nó de configuração Pasta monitorada.

   O tipo da propriedade só pode ser Booliano, Date, Decimal, Double, Long e String. Propriedades com vários valores também são compatíveis. Para propriedades com vários valores, o valor disponível para a etapa do fluxo de trabalho é uma matriz do tipo especificado.

   >[!NOTE]
   >
   >Se o tipo de dados da propriedade for Double, especifique um ponto decimal no valor dessas propriedades. Para todas as propriedades, onde o tipo de dados é Double e nenhum ponto decimal é especificado no valor, o tipo é convertido em Long.

>[!NOTE]
>
>A especificação JCR exige um valor padrão para as propriedades. Os valores padrão estão disponíveis para as etapas de um fluxo de trabalho para processamento. Portanto, especifique os valores padrão adequados.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Vários métodos de processamento de arquivos {#variousmethodsforprocessingfiles}

É possível iniciar um fluxo de trabalho, serviço ou script para processar os locais dos documentos em uma pasta observada.

### Usar um serviço para processar arquivos de uma pasta monitorada   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Um Serviço é uma implementação personalizada do `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` interface. Ele está registrado com o OSGi, juntamente com algumas propriedades personalizadas. As propriedades personalizadas da implementação a tornam exclusiva e ajudam a identificar a implementação.

#### Implementação personalizada da interface ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

A implementação personalizada aceita um contexto de processamento (um objeto do tipo com.adobe.aemfd.watchfolder.service.api.ProcessorContext), lê documentos de entrada e parâmetros de configuração do contexto, processa as entradas e adiciona a saída de volta ao contexto. O ProcessorContext tem as seguintes APIs:

* **getWatchFolderId**: retorna a ID da pasta monitorada.
* **getInputMap**: retorna um mapa do tipo Mapa. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* **getConfigParameters**: retorna um mapa imutável do tipo Map. O mapa contém os parâmetros de configuração de uma Pasta monitorada.

* **setResult**: A implementação ContentProcessor usa a API para gravar o documento de saída na pasta de resultado. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo do padrão de pasta/arquivo de saída especificado. Se um padrão de pasta for especificado, os arquivos de saída terão os nomes conforme descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes conforme descrito no padrão de arquivo.

Por exemplo, o código a seguir é uma implementação personalizada da interface ContentProcessor com uma propriedade foo=bar personalizada.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

Enquanto [configurando uma pasta monitorada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), se você especificar a propriedade inputProcessorId como (foo=bar) e a propriedade inputProcessorType como Service, o Serviço mencionado acima (implementação personalizada) será usado para processar os arquivos de entrada da Pasta monitorada.

O exemplo a seguir também é uma implementação personalizada da interface ContentProcessor. No exemplo, o Serviço aceita arquivos de entrada, copia os arquivos para um local temporário e retorna um objeto de documento com o conteúdo do arquivo. O conteúdo do objeto do documento é salvo na pasta de resultados. O caminho físico da pasta de resultados é configurado no [Nó de configuração da pasta monitorada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

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

### Uso de scripts para processar arquivos de uma pasta monitorada {#using-scripts-to-process-files-of-a-watched-folder}

Os scripts são o código personalizado de reclamação do ECMAScript gravado para processar documentos colocados na Pasta monitorada. Um script é representado como um nó JCR. Além das variáveis ECMAScript padrão (log, sling e outras), o script tem uma variável processorContext. A variável é do tipo ProcessorContext. O ProcessorContext tem as seguintes APIs:

* **getWatchFolderId**: retorna a ID da pasta monitorada.
* **getInputMap**: retorna um mapa do tipo Mapa. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* **getConfigParameters**: retorna um mapa imutável do tipo Map. O mapa contém os parâmetros de configuração de uma Pasta monitorada.
* **setResult**: A implementação ContentProcessor usa a API para gravar o documento de saída na pasta de resultado. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo do padrão de pasta/arquivo de saída especificado. Se um padrão de pasta for especificado, os arquivos de saída terão os nomes conforme descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes conforme descrito no padrão de arquivo.

O código a seguir é um exemplo de ECMAScript. Ele aceita arquivos de entrada, copia os arquivos para um local temporário e retorna um objeto de documento com o conteúdo do arquivo. O conteúdo do objeto do documento é salvo na pasta de resultados. O caminho físico da pasta de resultados é configurado no [Nó de configuração da pasta monitorada](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>A pasta de saída e o prefixo do nome de arquivo são decididos com base nos parâmetros de configuração da Pasta monitorada.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Localização de scripts e considerações de segurança {#location-of-scripts-and-security-considerations}

Por padrão, uma pasta de contêiner (/etc/fd/watchfolder/scripts) é fornecida, onde os clientes podem colocar seus scripts, e o usuário de serviço padrão usado pela estrutura watch-folder tem as permissões necessárias para ler scripts desse local.

Se você planeja colocar seus scripts em um local personalizado, é provável que o usuário de serviço padrão não tenha permissões de leitura no local personalizado. Para esse cenário, execute as seguintes etapas para fornecer as permissões necessárias ao local personalizado:

1. Crie um usuário do sistema de forma programática ou pelo console https://&#39;[server]:[porta]&quot;/crx/explorer. Você também pode usar um usuário do sistema existente. É importante trabalhar com os usuários do sistema aqui em vez de com os usuários normais.
1. Forneça permissões de leitura ao usuário do sistema recém-criado ou existente no local personalizado onde os scripts são armazenados. Você pode ter vários locais personalizados. Forneça pelo menos permissões de leitura a todos os locais personalizados.
1. No console de configuração Felix (/system/console/configMgr), localize o mapeamento de usuário de serviço para as pastas de observação. Esse mapeamento se parece com &quot;Mapeamento: adobe-aemds-core-watch-folder=...&quot;.
1. Clique no mapeamento. Para a entrada &quot;adobe-aemds-core-watch-folder:scripts=fd-service&quot;, altere fd-service para a ID do usuário de sistema personalizado. Clique em Salvar.

Agora, você pode usar o local personalizado configurado para salvar os scripts.

### Utilização de um fluxo de trabalho para processar arquivos de uma pasta monitorada {#using-a-workflow-to-process-files-of-a-watched-folder}

Os workflows permitem automatizar atividades de Experience Manager. Os workflows consistem em uma série de etapas executadas em uma ordem específica. Cada etapa executa uma atividade distinta, como ativar uma página ou enviar uma mensagem de email. Os workflows podem interagir com ativos no repositório, contas de usuário e serviços Experience Manager. Portanto, os workflows podem coordenar-se de forma complicada.

* Antes de criar um workflow, considere os seguintes pontos:
* A saída de uma etapa deve estar disponível para todas as etapas subsequentes.
As etapas devem ser capazes de atualizar (ou até mesmo excluir) saídas existentes geradas pelas etapas anteriores.
* As variáveis mutáveis são usadas para transmitir os dados dinâmicos personalizados entre as etapas.

Execute as seguintes etapas para processar arquivos usando workflows:

1. Criar uma implementação do `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` interface. É semelhante à implementação criada para um Serviço.

   >[!NOTE]
   >
   >Você pode criar a implementação completa inteiramente no ECMAScript.

1. Em uma etapa do Fluxo de trabalho, localize o serviço OSGi do tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService e chame o método execute() do serviço com os seguintes argumentos.

   * Sua implementação personalizada da interface WorkflowContextProcessor
   * itemDeTrabalho
   * workflowSession
   * metadados

Se você usar a linguagem de programação Java para implementar o fluxo de trabalho, o mecanismo de fluxo de trabalho AEM fornecerá valor para as variáveis de item de trabalho, sessão do fluxo de trabalho e metadados. Essas variáveis são passadas como argumentos para o método execute() da implementação personalizada do WorkflowProcess.

Se você usar o ECMAScript para implementar o workflow, o mecanismo de workflow AEM fornecerá valor para as variáveis graniteWorkItem, graniteWorkflowSession e de metadados. Essas variáveis são passadas como argumentos para o método WorkflowContextService.execute().

O argumento para processWorkflowContext() é um objeto do tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. A interface WorkflowContext tem as seguintes APIs para facilitar as considerações específicas do fluxo de trabalho mencionadas acima:

* getWorkItem: Retorna o valor da variável WorkItem. As variáveis são passadas para o método WorkflowContextService.execute().
* getWorkflowSession: retorna o valor da variável WorkflowSession. As variáveis são passadas para o método WorkflowContextService.execute().
* getMetadata: retorna o valor da variável de Metadados. As variáveis são passadas para o método WorkflowContextService.execute().
* getCommitedVariables: retorna um mapa de objetos somente leitura que representa variáveis definidas por etapas anteriores. Se uma variável não for modificada em nenhuma das etapas anteriores, o valor padrão especificado durante a configuração da Pasta monitorada será retornado.
* getCommitedResults: retorna um mapa de Documento somente leitura. O mapa representa os arquivos de saída gerados pelas etapas anteriores.
* setVariable: a implementação WorkflowContextProcessor usa a variável para manipular as variáveis que representam os dados dinâmicos personalizados que fluem entre as etapas. O nome e o tipo das variáveis são idênticos ao nome das variáveis especificadas durante [configurando a pasta monitorada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). Para alterar o valor de uma variável, chame a API setVariable com um valor não nulo. Para remover uma variável, chame setVariable() com um valor nulo.

As seguintes APIs ProcessorContext também estão disponíveis:

* getWatchFolderId: retorna a ID da pasta monitorada.
* getInputMap: retorna um mapa do tipo Mapa&lt;string document=&quot;&quot;>. As chaves do mapa são o nome do arquivo de entrada e um objeto de documento contendo o conteúdo do arquivo. Use a API getinputMap para ler os arquivos de entrada.
* getConfigParameters: retorna um mapa imutável do tipo Mapa&lt;string object=&quot;&quot;>. O mapa contém os parâmetros de configuração de uma Pasta monitorada.
* setResult: a implementação do ContentProcessor usa a API para gravar o documento de saída na pasta de resultado. Você pode fornecer um nome para o arquivo de saída para a API setResult. A API pode optar por usar ou ignorar o arquivo fornecido, dependendo do padrão de pasta/arquivo de saída especificado. Se um padrão de pasta for especificado, os arquivos de saída terão os nomes conforme descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes conforme descrito no padrão de arquivo

Consideração para a API setResult, quando usada em workflows:

* Para adicionar um novo documento de saída que contribua para a saída geral do fluxo de trabalho, chame a API setResult com um nome de arquivo que não tenha sido usado como o nome de arquivo de saída por nenhuma etapa anterior.
* Para atualizar uma saída gerada por uma etapa anterior, chame a API setResult com um nome de arquivo já usado por uma etapa anterior.
* Para excluir uma saída gerada por uma etapa anterior, chame setResult com um nome de arquivo já usado por uma etapa anterior e nulo como o conteúdo.

>[!NOTE]
>
>Chamar a API setResult com conteúdo nulo em qualquer outro cenário resultaria em um erro.

O exemplo a seguir é implementado como uma etapa do fluxo de trabalho. No exemplo, o ECMAscript usa uma variável stepCount para rastrear o número de vezes que uma etapa é chamada na instância de workflow atual.
O nome da pasta de saída é uma combinação do número da etapa atual, do nome do arquivo original e do prefixo especificado no parâmetro outPrefix.

O ECMAScript obtém uma referência do serviço de contexto de fluxo de trabalho e cria uma implementação da interface WorkflowContextProcessor. A implementação WorkflowContextProcessor aceita arquivos de entrada, copia o arquivo para um local temporário e retorna um documento que representa o arquivo copiado. Com base no valor da variável booleana purgePrevious, a etapa atual exclui a saída gerada pela última vez pela mesma etapa quando a etapa foi iniciada na instância de fluxo de trabalho atual. No final, o método wfSvc.execute é chamado para executar a implementação WorkflowContextProcessor. O conteúdo do documento de saída é salvo na pasta de resultados no caminho físico mencionado no nó de configuração Pasta monitorada.

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

### Criar filtro do mapeador de carga para mapear a estrutura de uma pasta monitorada para a carga de um fluxo de trabalho {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Quando você cria uma pasta monitorada, ela cria uma estrutura de pastas dentro da pasta que está sendo monitorada. A estrutura de pastas tem pastas de preparo, resultado, preservação, entrada e falha. A estrutura de pastas pode servir como carga de entrada para o fluxo de trabalho e aceitar a saída de um fluxo de trabalho. Ele também pode listar pontos de falha, se houver.

Se a estrutura de um payload for diferente da estrutura da pasta monitorada, você poderá gravar scripts personalizados para mapear a estrutura da pasta monitorada para o payload. Esse script é chamado de filtro de mapeador de carga útil. Pronto para uso, o AEM Forms fornece um filtro de mapeador de carga para mapear a estrutura da pasta monitorada para uma carga.

#### Criação de um filtro personalizado do mapeador de carga {#creating-a-custom-payload-mapper-filter}

1. Baixar [Adobe Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Configure o SDK do cliente no caminho de compilação do projeto baseado em maven. Para começar, você pode baixar e abrir o seguinte projeto baseado em Maven no IDE de sua escolha.
1. Edite o código de filtro do mapeador de carga disponível no pacote de amostra para atender aos seus requisitos.
1. Use o Maven para criar um pacote do Filtro do mapeador de carga personalizado.
1. Uso [Console de pacotes AEM](https://localhost:4502/system/console/bundles) para instalar o pacote.

   Agora, o Filtro do mapeador de carga personalizado está listado na interface do usuário da pasta monitorada pelo AEM. Você pode usá-lo com seu workflow.

   O código de exemplo a seguir implementa um mapeador simples baseado em arquivo para os arquivos salvos em relação a uma carga. Você pode usá-lo para começar.

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

## Como os usuários interagem com uma pasta monitorada {#how-users-interact-with-a-watched-folder}

Para um endpoint de Pasta monitorada, os usuários podem iniciar operações de processamento de arquivos copiando ou arrastando arquivos ou pastas de entrada de suas áreas de trabalho para uma Pasta monitorada. Os arquivos são processados na ordem de chegada.

Para endpoints de Pasta monitorada, se um trabalho exigir apenas um arquivo de entrada, o usuário poderá copiar esse arquivo para a raiz da Pasta monitorada.

Se o trabalho contiver mais de um arquivo de entrada, o usuário deverá criar uma pasta fora da hierarquia de Pastas monitoradas que contenha todos os arquivos necessários. Essa nova pasta deve incluir os arquivos de entrada (e, opcionalmente, um arquivo DDX, se exigido pelo processo). Após a construção da pasta de trabalho, o usuário a copia para a pasta de entrada da Pasta monitorada.

>[!NOTE]
>
>Certifique-se de que o servidor de aplicativos excluiu o acesso aos arquivos da Pasta monitorada. Se o AEM Forms não conseguir excluir os arquivos da pasta de entrada após serem verificados, o processo associado será iniciado indefinidamente.

## Informações adicionais sobre as pastas monitoradas {#additional-information-about-the-watched-folders}

### Sobre a limitação {#about-throttling}

Quando a limitação é ativada para um endpoint de pasta monitorada, ela limita o número de trabalhos de Pasta monitorada que são processados a qualquer momento. O número máximo de trabalhos é determinado pelo valor Tamanho do lote, também configurável no endpoint Pasta monitorada. Quando o limite de limitação é atingido, os documentos de entrada no diretório de entrada da Pasta monitorada não são pesquisados. O documento também permanece no diretório de entrada até que outros trabalhos de Pasta monitorada sejam concluídos e outra tentativa de pesquisa seja feita. Para o processamento síncrono, todos os trabalhos processados em uma única enquete são contados para o limite de limitação, mesmo que os trabalhos sejam processados consecutivamente em um único thread.

>[!NOTE]
>
>A limitação não é dimensionada com um cluster. Quando a limitação estiver habilitada, o cluster como um todo não processará mais do que o número de trabalhos especificados no Tamanho do Lote em um determinado momento. Esse limite é em todo o cluster e não específico para cada nó no cluster. Por exemplo, com um Tamanho de lote de 2, o limite de limitação pode ser atingido com um único nó processando dois trabalhos e nenhum outro nó sondaria o diretório de entrada até que um dos trabalhos seja concluído.

#### Como funciona a limitação {#how-throttling-works}

A Pasta monitorada verifica a pasta de entrada em cada pollInterval, seleciona o número de arquivos especificados no Tamanho do lote e chama o serviço de destino para cada um desses arquivos. Por exemplo, se o Tamanho do Lote for quatro, em cada varredura, a Pasta monitorada selecionará quatro arquivos, criará quatro solicitações de chamada e chamará o serviço de destino. Antes que essas solicitações sejam concluídas, se a Pasta monitorada for invocada, ela iniciará novamente quatro trabalhos, independentemente de os quatro trabalhos anteriores terem sido concluídos ou não.

A limitação impede que a Pasta monitorada chame novos trabalhos quando os trabalhos anteriores não estiverem concluídos. A Pasta monitorada detecta trabalhos em andamento e processa novos trabalhos com base no tamanho do lote menos os trabalhos em andamento. Por exemplo, na segunda invocação, se o número de trabalhos concluídos for apenas três e um trabalho ainda estiver em andamento, a Pasta monitorada chamará apenas mais três trabalhos.

* A Pasta monitorada depende do número de arquivos presentes na pasta de preparo para descobrir quantos trabalhos estão em andamento. Se os arquivos permanecerem não processados na pasta de preparo, a Pasta monitorada não chamará mais tarefas. Por exemplo, se o tamanho do lote for quatro e três trabalhos estiverem paralisados, a Pasta monitorada chamará apenas um trabalho em chamadas subsequentes. Há vários cenários que podem fazer com que os arquivos permaneçam não processados na pasta de preparo. Quando os processos são interrompidos, o administrador pode encerrar o processo na página de administração do Gerenciamento do Processo para que a Pasta monitorada mova os arquivos para fora da pasta de preparo.
* Se o servidor do AEM Forms ficar inativo antes que a Pasta monitorada chame os trabalhos, o administrador poderá mover os arquivos para fora da pasta de preparo. Para obter informações, consulte [Pontos de falha e recuperação](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Se o servidor do AEM Forms estiver em execução, mas a Pasta monitorada não estiver em execução quando o serviço do Gerenciador de trabalhos chamar de volta, o que ocorre quando os serviços não iniciam na sequência ordenada, o administrador poderá mover os arquivos para fora da pasta de preparo. Para obter informações, consulte [Pontos de falha e recuperação](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Pontos de falha e recuperaçãoPontos de falha e recuperação {#failure-points-and-recoveryfailure-points-and-recovery}

Em cada evento de pesquisa, a Pasta monitorada bloqueia a pasta de entrada, move os arquivos que correspondem ao padrão de arquivo de inclusão para a pasta de preparo e, em seguida, desbloqueia a pasta de entrada. O bloqueio é necessário para que dois threads não selecionem o mesmo conjunto de arquivos e os processem duas vezes. As chances de isso acontecer aumentam com um intervalo de pesquisa pequeno e um tamanho de lote grande. Depois que os arquivos forem movidos para a pasta de preparo, a pasta de entrada será desbloqueada para que outras threads possam examinar a pasta. Esta etapa ajuda a fornecer alta taxa de transferência, pois outras threads podem examinar enquanto uma thread está processando os arquivos.

Depois que os arquivos são movidos para a pasta de preparo, solicitações de invocação são criadas para cada arquivo e o serviço de destino é chamado. Pode haver casos em que a Pasta monitorada não possa recuperar os arquivos na pasta de preparo:

* Se o servidor ficar inativo antes que a Pasta monitorada possa criar a solicitação de invocação, os arquivos na pasta de preparo permanecerão na pasta de preparo e não serão recuperados.

* Se a Pasta monitorada tiver criado com sucesso a solicitação de invocação para cada um dos arquivos na pasta de preparo e o servidor falhar, há dois comportamentos com base no tipo de invocação:

   * **Síncrono**: se a Pasta monitorada estiver configurada para chamar o serviço de forma síncrona, todos os arquivos na pasta de preparo permanecerão não processados na pasta de preparo.
   * **Assíncrono**: Nesse caso, a Pasta monitorada depende do serviço Gerenciador de trabalhos. Se o serviço do Gerenciador de trabalhos retornar as chamadas da Pasta monitorada, os arquivos na pasta de preparo serão movidos para a pasta de preservação ou falha com base nos resultados da invocação. Se o serviço Gerenciador de trabalhos não retornar a chamada da Pasta monitorada, os arquivos permanecerão não processados na pasta de preparo. Essa situação ocorre quando a Pasta monitorada não está em execução quando o Gerenciador de trabalhos chama de volta.

#### Recuperar arquivos de origem não processados na pasta de preparo {#recover-unprocessed-source-files-in-the-stage-folder}

Quando a Pasta monitorada não puder processar os arquivos de origem na pasta de preparo, você poderá recuperar os arquivos não processados.

1. Reinicie o servidor de aplicativos ou nó.

1. Impedir que a Pasta monitorada processe novos arquivos de entrada. Se ignorar esta etapa, será muito mais difícil determinar quais arquivos não serão processados na pasta de preparo. Para impedir que a Pasta monitorada processe novos arquivos de entrada, execute uma das seguintes tarefas:

   * Altere a propriedade includeFilePattern da Watched Folder para algo que não corresponda a nenhum dos novos arquivos de entrada (por exemplo, digite NOMATCH).
   * Suspenda o processo que está criando novos arquivos de entrada.

   Aguarde até que o AEM Forms recupere e processe todos os arquivos. A maioria dos arquivos deve ser recuperada e os novos arquivos de entrada processados corretamente. O tempo de espera pela Pasta monitorada para recuperar e processar os arquivos dependerá da duração da operação a ser chamada e do número de arquivos a serem recuperados.

1. Determine quais arquivos não podem ser processados. Se você esperou um tempo apropriado e concluiu a etapa anterior e ainda há arquivos não processados na pasta de preparo, vá para a próxima etapa.

   >[!NOTE]
   >
   >Você pode verificar a data e o carimbo de data e hora dos arquivos no diretório do estágio. Dependendo do número de arquivos e do tempo de processamento normal, você pode determinar quais arquivos são antigos o suficiente para serem considerados travados.

1. Copie os arquivos não processados do diretório de preparo para o diretório de entrada.

1. Se você impediu que a Pasta monitorada processasse novos arquivos de entrada na etapa 2, altere o Padrão de arquivo de inclusão para seu valor anterior ou reative o processo desativado.

### Pastas monitoradas em cadeia juntas {#chain-watched-folders-together}

As Pastas monitoradas podem ser encadeadas para que um documento de resultado de uma Pasta monitorada seja o documento de entrada da próxima Pasta monitorada. Cada Pasta monitorada pode chamar um serviço diferente. Ao configurar Pastas monitoradas dessa maneira, vários serviços podem ser chamados. Por exemplo, uma Pasta monitorada pode converter arquivos PDF para o Adobe PostScript® e uma segunda Pasta monitorada pode converter os arquivos PostScript para o formato PDF/A. Para fazer isso, basta definir a pasta de resultados da Pasta monitorada definida pelo primeiro ponto de extremidade para apontar para a pasta de entrada da Pasta monitorada definida pelo segundo ponto de extremidade.

A saída da primeira conversão iria para \path\result. A entrada para a segunda conversão seria \path\result, e a saída da segunda conversão iria para \path\result\result (ou o diretório definido na caixa Pasta de resultados para a segunda conversão).

### Padrões de arquivos e pastas {#file-and-folder-patterns}

Os administradores podem especificar o tipo de arquivo que pode chamar um serviço. Vários padrões de arquivo podem ser estabelecidos para cada Pasta monitorada. Um padrão de arquivo pode ser uma das seguintes propriedades de arquivo:

* Arquivos com extensões de nome de arquivo específicas; por exemplo, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
* Arquivos com nomes específicos; por exemplo, dados.&#42;
* Arquivos com expressões compostas no nome e na extensão, como nestes exemplos:

   * Dados[0-9][0-9][0-9].[dD][aA]&#39;porta&#39;
   * &#42;.[dD][Aa]&#39;porta&#39;
   * &#42;.[Xx][Mm][Ll]

* O administrador pode definir o padrão de arquivo da pasta de saída na qual os resultados serão armazenados. Para as pastas de saída (resultado, preservação e falha), o administrador pode especificar qualquer um destes padrões de arquivo:
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

Por exemplo, o caminho para a pasta de resultados pode ser C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Os mapeamentos de parâmetros de saída também podem especificar padrões adicionais, como estes:

* %F = Nome de arquivo de origem
* %E = Extensão De Nome De Arquivo De Origem

Se o padrão de mapeamento do parâmetro de saída terminar com &quot;File.separator&quot; (que é o separador de caminhos), uma pasta será criada e o conteúdo será copiado nessa pasta. Se o padrão não terminar com &quot;File.separator&quot;, o conteúdo (arquivo de resultado ou pasta) será criado com esse nome.

## Uso do PDF Generator com uma pasta monitorada {#using-pdf-generator-with-a-watched-folder}

Você pode configurar uma Pasta monitorada para iniciar um fluxo de trabalho, serviço ou script para processar os arquivos de entrada. Na seção a seguir, configuraremos uma Pasta monitorada para iniciar um ECMAScript. O ECMAScript usaria o PDF Generator para converter documentos do Microsoft Word (.docx) em documentos PDF.

Execute as seguintes etapas para configurar uma Pasta monitorada com PDF Generator:

1. [Criar um ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Criar um fluxo de trabalho](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configurar a pasta monitorada](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Criar um ECMAScript {#create-an-ecmascript}

O ECMAScript usaria a API PDF Generator createPDF para converter documentos do Microsoft Word (.docx) em documentos PDF. Execute as seguintes etapas para criar o script:

1. Abra o CRXDE lite em uma janela do navegador. O URL é https://&#39;[server]:[porta]&quot;/crx/de.

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

1. Salvar e fechar o arquivo.

### Criar um fluxo de trabalho {#create-a-workflow}

1. Abra a interface do usuário do fluxo de trabalho do AEM em uma janela do navegador.
   <https://[servername>]:&#39;port&#39;/workflow

1. Na visualização Modelos, clique em **Novo**. Na caixa de diálogo Novo fluxo de trabalho, especifique **Título** e clique em **OK**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Selecione o workflow recém-criado e clique em **Editar**. O workflow é aberto em uma nova janela.

1. Exclua a etapa do fluxo de trabalho padrão. Arraste e solte a Etapa do processo do Sidekick para o fluxo de trabalho.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Clique com o botão direito na Etapa do processo e selecione **Editar**. A janela Propriedades da etapa é exibida.

1. Na guia Processo, selecione o ECMAScript. Por exemplo, o script pdfg-openOffice-sample.ecma criado em [Criar um ECMAScript](#p-create-an-ecmascript-p). Ativar o **Avanço do manipulador** e clique em **OK**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurar a pasta monitorada {#configure-the-watched-folder}

1. Abra o CRXDE lite em uma janela do navegador. https://&#39;[server]:[porta]&quot;/crx/de/

1. Navegue até a pasta /etc/fd/watchfolder/config/ e crie um nó do tipo nt:unstructured.

   ![configure-the-watch-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Adicione as seguintes propriedades ao nó:

   * folderPath (String): o caminho da pasta a ser examinada em intervalos de tempo definidos. A pasta deve estar em um local compartilhado com todos os servidores com acesso total ao servidor.
inputProcessorType (String): o tipo do processo a ser iniciado. Neste tutorial, especifique o workflow.

   * inputProcessorId (String): o comportamento da propriedade inputProcessorId é baseado no valor especificado para a propriedade inputProcessorType. Neste exemplo, o valor da propriedade inputProcessorType é workflow. Portanto, para a propriedade inputProcessorId, especifique o seguinte caminho do workflow PDFG: /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (String): padrão do arquivo de saída. Você pode especificar uma pasta ou um padrão de arquivo. Se um padrão de pasta for especificado, os arquivos de saída terão os nomes conforme descrito em workflows. Se um padrão de arquivo for especificado, os arquivos de saída terão nomes conforme descrito no padrão de arquivo.

   Além das propriedades obrigatórias mencionadas acima, as Pastas monitoradas também oferecem suporte a algumas propriedades opcionais. Para obter a lista e a descrição completas das propriedades opcionais, consulte [Propriedades da pasta monitorada](#watchedfolderproperties).

## Problemas conhecidos {#watched-folder-known-issues}

Ao iniciar o AEM 6.5 Forms no JEE, os arquivos começam a ser processados antes que o JBoss seja totalmente iniciado e os arquivos não sejam processados. Para evitar isso, antes de iniciar o JBoss, limpe todas as Pastas monitoradas.
