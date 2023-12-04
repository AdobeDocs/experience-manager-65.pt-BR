---
title: Criar ou configurar uma pasta monitorada
description: Saiba como criar ou excluir uma pasta monitorada ou modificar as propriedades de uma pasta monitorada existente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---

# Criar ou configurar uma pasta monitorada {#create-or-configure-a-watched-folder}

Um administrador pode configurar uma pasta de rede, conhecida como *pasta monitorada*, para que, quando um usuário colocar um arquivo (como um arquivo PDF) na pasta monitorada, uma operação pré-configurada seja iniciada e manipule o arquivo. Depois que a operação especificada é executada, a operação salva o arquivo modificado em uma pasta de saída especificada. Para obter informações detalhadas sobre como administrar uma pasta monitorada, consulte [Ajuda de administração](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

É possível usar a interface de usuário da pasta monitorada para:

* Criar uma pasta monitorada
* Modificar propriedades de uma pasta monitorada existente
* Excluir uma pasta monitorada

## Criar uma pasta monitorada {#create-a-watched-folder}

Antes de configurar uma pasta monitorada, verifique o seguinte:

* As pastas monitoradas são um recurso avançado dos formulários AEM. Ele requer o pacote complementar do AEM forms para funcionar. Verifique se o pacote complementar apropriado do AEM Forms está instalado e configurado.
* Você pode criar a pasta monitorada em um armazenamento local ou compartilhado. Verifique se o usuário do AEM Forms configurado para executar a pasta monitorada tem permissões de leitura e gravação nessa pasta.
* Você pode usar um Serviço, Fluxo de trabalho ou Script para automatizar uma operação com a pasta monitorada. Verifique se o Serviço, Fluxo de trabalho ou Script correspondente foi criado e está pronto para ser executado. Para obter informações sobre como criar um Serviço, Fluxo de Trabalho e Script, consulte [Vários métodos de processamento de arquivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Uma pasta monitorada tem várias propriedades, consulte [Propriedades da pasta monitorada](watched-folder-in-aem-forms.md#watchedfolderproperties).

Execute as seguintes etapas para criar uma pasta monitorada:

1. Selecionar **Adobe Experience Manager** no canto superior esquerdo da tela.
1. Selecionar **Ferramentas** > **Forms** > **Configurar a pasta monitorada.** Uma lista de pastas monitoradas já configuradas é exibida.
1. Selecionar **Novo**. Uma lista de campos necessários para criar a pasta monitorada é exibida:

   * **Nome**: identifica a pasta monitorada. Use somente caracteres alfanuméricos para o nome.
   * **Caminho**: especifica o local da pasta monitorada. Em um ambiente clusterizado, essa configuração deve apontar para uma pasta de rede compartilhada acessível a cada usuário que executa o AEM em diferentes nós de um cluster.
   * **Processar arquivos usando**: o tipo do processo a ser iniciado. Você pode especificar um fluxo de trabalho, script ou serviço.
   * **Nome do serviço/Caminho do script/Caminho do fluxo de trabalho**: o comportamento do campo se baseia no valor especificado para o **Processar arquivos usando** campo. Você pode especificar os seguintes valores:

      * Em Fluxo de trabalho, especifique o modelo de fluxo de trabalho que será executado. Por exemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Para Script, especifique o caminho JCR do script a ser executado. Por exemplo, /etc/watchfolder/test/testScript.ecma
      * Para Serviço, especifique o filtro usado para localizar um serviço OSGi. O serviço é registrado como uma implementação da interface com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Por exemplo, o código a seguir é uma implementação personalizada da interface ContentProcessor com uma propriedade personalizada (foo=bar).

   >[!NOTE]
   >
   >Se você selecionou **Serviço** para o **Processar arquivos usando** , o valor do campo Service Name(inputProcessorType) deve ser entre parênteses. Por exemplo, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Padrão do arquivo de saída**: especifique uma lista de padrões delimitada por ponto e vírgula (;) que uma pasta monitorada usa para determinar o nome e o local dos arquivos e pastas de saída. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. Selecionar **Avançado**. A guia Advanced contém mais campos. A maioria desses campos contém um valor padrão.

   * **Filtro do mapeador de carga útil:** Quando você cria uma pasta monitorada, ela cria uma estrutura de pastas dentro da pasta que está sendo monitorada. A estrutura de pastas tem pastas de preparo, resultado, preservação, entrada e falha. A estrutura de pastas pode servir como carga de entrada para o fluxo de trabalho e aceitar a saída de um fluxo de trabalho. Ele também pode listar pontos de falha, se houver. A estrutura de uma carga é diferente da estrutura de uma pasta monitorada. Você pode gravar scripts personalizados para mapear a estrutura de uma pasta monitorada para a carga útil. Esse script é chamado de filtro de mapeador de carga útil. Duas implementações prontas para uso do mapeador de carga estão disponíveis. Se você não tiver [uma implementação personalizada](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), use uma das implementações prontas para uso:

      * **Mapeador padrão:** Use o mapeador de carga útil padrão para manter os conteúdos de entrada e saída das pastas monitoradas em pastas de entrada e saída separadas na carga útil.
      * **Mapeador de conteúdo simples baseado em arquivo:** Use o mapeador de carga útil baseado em arquivo simples para manter o conteúdo de entrada e saída diretamente na pasta de carga útil. Ela não cria nenhuma hierarquia extra, como o mapeador padrão.

   * **Modo de execução**: especifique a lista separada por vírgulas de modos de execução permitidos para a execução do workflow.
   * **Arquivos por etapa expirados após**: especifique o número de segundos de espera antes que um arquivo/pasta de entrada que já foi selecionado para processamento seja tratado como tendo ultrapassado o tempo limite e marcado como uma falha. O mecanismo de tempo limite só é ativado quando o valor dessa propriedade é um número positivo.
   * **Excluir arquivos do Palco expirados quando sincronizados**: Se ativada, a variável **Arquivos por etapa expirados após** o mecanismo é ativado somente quando a limitação está ativada para a pasta monitorada.
   * **Verificar a pasta de entrada após cada:** Especifique o intervalo de tempo, em segundos, para verificar a pasta monitorada quanto a entradas. A menos que a configuração de Aceleração esteja ativada, o Intervalo de Sondagem deve ser maior que o tempo médio para processar um trabalho; caso contrário, o sistema pode ficar sobrecarregado. O valor do intervalo deve ser maior ou igual a um.
   * **Excluir Padrão do Arquivo**: especifique uma lista de padrões delimitada por ponto e vírgula (;) que uma pasta monitorada usa para determinar quais arquivos e pastas serão verificados e selecionados. Qualquer arquivo ou pasta com o padrão especificado não é examinado para processamento. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Incluir Padrão do Arquivo**: especifique uma lista de padrões delimitada por ponto e vírgula (;) que a pasta monitorada usa para determinar quais pastas e arquivos serão verificados e selecionados. Por exemplo, se o Padrão de arquivo de inclusão for input&amp;ast;, todos os arquivos e pastas que corresponderem a input&amp;ast; serão selecionados. O valor padrão é &amp;ast; e indica todos os arquivos e pastas. Para obter mais informações sobre padrões de arquivo, consulte [Sobre Padrões de Arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo de espera:** Especifique o tempo, em milissegundos, a ser aguardado antes de examinar uma pasta ou um arquivo após sua criação. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será selecionado após 59 minutos ou mais. O valor padrão é 0.

     Essa configuração é útil para garantir que todo o conteúdo do arquivo ou pasta seja copiado para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e ele levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Esse intervalo impede que a pasta monitorada verifique o arquivo se ele não tiver dez minutos.

   * **Excluir Resultados Mais Antigos Que:** Especifique o tempo, em número de dias, de espera antes de excluir os arquivos e pastas anteriores ao valor especificado. Essa configuração é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que a pasta de resultados nunca deve ser excluída. O valor padrão é -1.
   * **Nome da pasta de resultado:** Especifique o nome da pasta onde os resultados serão armazenados. Se os resultados não aparecerem nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e são salvos na pasta de falha. Você pode usar um caminho absoluto ou relativo com os seguintes padrões de arquivo:

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
      * %R = número aleatório (entre 0-9)
      * %P = id do processo ou da tarefa
      * Por exemplo, se for 8 PM em 17 de julho de 2009 e você especificar C:/Test/WF0/failure/%Y/%M/%D/%H/, a pasta resultante será C:/Test/WF0/failure/2009/07/17/20.
      * Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta monitorada. O valor padrão é result/%Y/%M/%D/, que é a pasta Result dentro da pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **Falha no nome da pasta:** Especifique a pasta onde os arquivos com falha são salvos. Este local é sempre relativo à pasta monitorada. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados.
   * **Preservar nome da pasta:** Especifique a pasta onde os arquivos são armazenados após a verificação e a coleta bem-sucedidas. O caminho pode ser um diretório absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito em Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.
   * **Tamanho do lote:** Especifique o número de arquivos ou pastas a serem selecionados por varredura. Isso evita uma sobrecarga no sistema; a varredura de muitos arquivos de uma vez pode causar travamento. O valor padrão é 2.

     Se o intervalo de verificação for pequeno, as threads examinam a pasta de entrada com frequência. Se os arquivos forem colocados com frequência na pasta monitorada, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar as threads.

   * **Acelerador Ligado:** Quando essa opção está ativada, ela limita o número de trabalhos de pastas monitoradas que os formulários AEM processam a qualquer momento. O valor Tamanho do Lote determina o número máximo de trabalhos. Para obter mais informações, consulte [limitação](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Substituir arquivos existentes com nome semelhante**: quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como False, os arquivos e as pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.
   * **Preservar os arquivos na falha:** Quando definido como Verdadeiro, os arquivos de entrada são preservados se houver falha. O valor padrão é true.
   * **Incluir arquivos com o padrão:** Especifique uma lista delimitada por ponto e vírgula (;) de padrões que a pasta monitorada usa para determinar quais pastas e arquivos serão verificados e selecionados. Por exemplo, se Incluir padrão de arquivo for entrada, todos os arquivos e pastas que correspondem à entrada serão coletados. Para obter mais informações, consulte [Ajuda de administração](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Chame a pasta monitorada de forma assíncrona:** Identifica o tipo de invocação como assíncrono ou síncrono. O valor padrão é assíncrono. O assíncrono é recomendado para processos de longa duração, enquanto o síncrono é recomendado para processos transitórios ou de curta duração.
   * **Ativar a pasta monitorada:** Quando esta opção está habilitada, a pasta observada é habilitada. O valor padrão é True.

## Modificar propriedades de uma pasta monitorada existente {#modify-properties-of-an-existing-watched-folder}

Além de alterar o nome da pasta monitorada, você pode modificar todas as propriedades de uma pasta monitorada existente. Execute as seguintes etapas para modificar propriedades de uma pasta monitorada existente:

1. Selecione o **Adobe Experience Manager** no canto superior esquerdo da tela.
1. Selecionar **Ferramentas** > **Forms** > **Configurar a pasta monitorada.** Uma lista de pastas monitoradas já configuradas é exibida.
1. No lado esquerdo da tela Pasta monitorada, selecione a pasta monitorada e selecione **Editar.** Uma lista de campos necessários para criar a pasta monitorada é exibida. Os campos listados na variável **Básico** As guias são obrigatórias. A guia Advanced contém mais campos. A maioria desses campos contém um valor padrão. Você pode modificar essas propriedades de acordo com seus requisitos.
1. Depois de modificar as propriedades, selecione **Atualizar**. As propriedades modificadas são salvas.
