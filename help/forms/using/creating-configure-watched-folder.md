---
title: Criar ou configurar uma pasta monitorada
seo-title: Create or Configure a watched folder
description: Saiba como criar ou excluir uma pasta assistida ou modificar as propriedades de uma pasta assistida existente.
seo-description: Learn how to create or delete a watched folder, or modify the properties of an existing watched folder.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Criar ou configurar uma pasta monitorada {#create-or-configure-a-watched-folder}

Um administrador pode configurar uma pasta de rede, conhecida como *pasta assistida*, para que quando um usuário coloque um arquivo (como um PDF file) na pasta assistida, uma operação pré-configurada seja iniciada e manipule o arquivo. Depois que a operação especificada é executada, a operação salva o arquivo modificado em uma pasta de saída especificada. Para obter informações detalhadas sobre como administrar uma pasta assistida, consulte [Ajuda da administração](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Você pode usar a interface do usuário da pasta assistida para:

* Criar uma pasta monitorada
* Modificar propriedades de uma pasta observada existente
* Excluir uma pasta monitorada

## Criar uma pasta monitorada {#create-a-watched-folder}

Antes de configurar uma pasta monitorada, verifique o seguinte:

* As pastas assistidas são um recurso avançado de formulários AEM. Para funcionar, é necessário AEM pacote complementar de formulários. Certifique-se de que o pacote do complemento AEM Forms apropriado esteja instalado e configurado.
* Você pode criar a pasta monitorada em um armazenamento compartilhado ou local. Certifique-se de que AEM usuário do forms configurado para executar a pasta monitorada tenha permissões de leitura e gravação na pasta monitorada.
* Você pode usar um Serviço, Workflow ou Script para automatizar uma operação com uma pasta monitorada. Certifique-se de que o Serviço, o Fluxo de Trabalho ou um Script correspondente tenha sido criado e esteja pronto para ser executado. Para obter informações sobre como criar um Serviço, Fluxo de Trabalho e Script, consulte [Vários métodos de processamento de arquivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Uma pasta assistida tem várias propriedades, consulte [Propriedades da pasta assistida](watched-folder-in-aem-forms.md#watchedfolderproperties).

Execute as seguintes etapas para criar uma pasta assistida:

1. Toque **Adobe Experience Manager** no canto superior esquerdo da tela.
1. Toque **Ferramentas** > **Forms** > **Configurar pasta assistida.** Uma lista de pastas de controle já configuradas é exibida.
1. Toque **Novo**. Uma lista de campos necessários para criar a pasta assistida é exibida:

   * **Nome**: Identifica a pasta observada. Use somente caracteres alfanuméricos para o nome.
   * **Caminho**: Especifica o local da pasta monitorada. Em um ambiente em cluster, essa configuração deve apontar para uma pasta de rede compartilhada acessível a cada usuário que estiver executando AEM em diferentes nós de um cluster.
   * **Processar arquivos usando**: O tipo do processo a ser iniciado. Você pode especificar workflow, script ou serviço.
   * **Nome do serviço/Caminho do script/Caminho do fluxo de trabalho**: O comportamento do campo se baseia no valor especificado para a variável **Processar arquivos usando** campo. Você pode especificar os seguintes valores:

      * Para Fluxo de trabalho, especifique o modelo de fluxo de trabalho a ser executado. Por exemplo, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Para Script, especifique o caminho JCR do script a ser executado. Por exemplo, /etc/watchfolder/test/testScript.ecma
      * Para Serviço, especifique o filtro usado para localizar um serviço OSGi. O serviço é registrado como uma implementação da interface com.adobe.aemfd.watchfolder.service.api.ContentProcessor . Por exemplo, o código a seguir é uma implementação personalizada da interface ContentProcessor com uma propriedade personalizada (foo=bar).

   >[!NOTE]
   >
   >Se você selecionou **Serviço** para **Processar arquivos usando** , o valor do campo Service Name(inputProcessorType) deve ser incluído entre parênteses. Por exemplo, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Padrão do arquivo de saída**: Especifique uma lista delimitada por ponto e vírgula (;) de padrões que uma pasta assistida usa para determinar o nome e o local dos arquivos e pastas de saída. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Toque **Avançado**. A guia advanced contém mais campos. A maioria desses campos contém um valor padrão.

   * **Filtro do Mapeador de Carga:** Ao criar uma pasta assistida, ela cria uma estrutura de pastas dentro da pasta que está sendo assistida. A estrutura de pastas tem pastas de estágio, resultado, preservação, entrada e falha. A estrutura de pastas pode servir como carga de entrada para o workflow e aceitar a saída de um workflow. Também pode listar pontos de falha, se houver. A estrutura de uma carga é diferente da estrutura de uma pasta assistida. Você pode gravar scripts personalizados para mapear a estrutura de uma pasta assistida para o payload. Esse script é chamado de filtro de mapeador de carga. Duas implementações prontas para uso do mapeador de carga estão disponíveis. Se você não tiver [uma implementação personalizada](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), use uma implementação pronta para uso:

      * **Mapeador padrão:** Use o mapeador de carga padrão para manter o conteúdo de entrada e saída das pastas assistidas em pastas separadas de entrada e saída no payload.
      * **Mapeador de carga baseado em arquivo simples:** Use o mapeador de carga baseado em arquivo simples para manter o conteúdo de entrada e saída diretamente na pasta de carga útil. Ela não cria nenhuma hierarquia extra, como o mapeador padrão.
   * **Modo de execução**: Especifique a lista separada por vírgulas de run-modes permitidos para execução de workflow.
   * **Arquivos preparados de tempo limite após**: Especifique o número de segundos a aguardar antes que um arquivo/pasta de entrada que já foi selecionado para processamento seja tratado como tendo expirado e marcado como uma falha. O mecanismo de tempo limite só é ativado quando o valor dessa propriedade é um número positivo.
   * **Excluir arquivos preparados com tempo limite quando limitados**: Se estiver habilitado, a variável **Arquivos preparados de tempo limite após** O mecanismo é ativado somente quando a limitação é ativada para a pasta assistida.
   * **Verificar Pasta De Entrada Depois De Cada:** Especifique o intervalo de tempo, em segundos, para verificar as entradas da pasta observada. A menos que a configuração Throttle esteja ativada, o Intervalo de pesquisa deve ser maior que o tempo para processar um trabalho médio; caso contrário, o sistema pode estar sobrecarregado. O valor do intervalo deve ser maior ou igual a um.
   * **Excluir padrão de arquivo**: Especifique uma lista de padrões delimitada por ponto e vírgula (;) que uma pasta assistida usa para determinar quais arquivos e pastas serão examinados e coletados. Qualquer arquivo ou pasta com o padrão especificado não é verificado para processamento. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Incluir padrão de arquivo**: Especifique uma lista de padrões delimitada por ponto e vírgula (;) que a pasta assistida usa para determinar quais pastas e arquivos devem ser digitalizados e coletados. Por exemplo, se o Padrão Incluir Arquivo for input&amp;ast;, todos os arquivos e pastas que correspondam a input&amp;ast; são selecionadas. O valor padrão é &amp;ast; e indica todos os arquivos e pastas. Para obter mais informações sobre padrões de arquivo, consulte [Sobre Padrões de Arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo de espera:** Especifique o tempo, em milissegundos, a ser aguardado antes de digitalizar uma pasta ou arquivo depois que ele for criado. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado um minuto atrás, esse arquivo será selecionado após 59 ou mais minutos terem passado. O valor padrão é 0.

      Essa configuração é útil para garantir que todo o conteúdo do arquivo ou pasta seja copiado para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o arquivo levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Esse intervalo impede que a pasta assistida verifique o arquivo se ele não tiver dez minutos.

   * **Excluir Resultados Antes De:** Especifique o tempo, em número de dias, a ser aguardado antes de excluir os Arquivos e pastas anteriores ao valor especificado. Essa configuração é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que nunca excluir a pasta de resultados. O valor padrão é -1.
   * **Nome da Pasta de Resultado:** Especifique o nome da pasta para armazenar os resultados. Se os resultados não forem exibidos nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e são salvos na pasta de falha. Você pode usar um caminho absoluto ou relativo com os seguintes padrões de arquivo:

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
      * Por exemplo, se for 8 PM em 17 de julho de 2009 e você especificar C:/Test/WF0/failure/%Y/%M/%D/%H/, a pasta de resultado será C:/Test/WF0/failure/2009/07/17/20.
      * Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta assistida. O valor padrão é result/%Y/%M/%D/, que é a pasta Result dentro da pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Nome da Pasta de Falha:** Especifique a pasta onde os arquivos com falha são salvos. Esse local é sempre relativo à pasta assistida. Você pode usar padrões de arquivo, conforme descrito para Pasta de resultados.
   * **Preservar nome da pasta:** Especifique a pasta onde os arquivos são armazenados após a varredura e coleta bem-sucedidas. O caminho pode ser absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito para Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.
   * **Tamanho do lote:** Especifique o número de arquivos ou pastas a serem selecionados por varredura. Evita sobrecarga no sistema; a varredura de muitos arquivos de uma vez pode causar uma falha. O valor padrão é 2.

      Se o intervalo de varredura for pequeno, os threads verificarão a pasta de entrada com frequência. Se os arquivos forem soltos com frequência na pasta monitorada, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de varredura maior para que os outros serviços possam usar os threads.

   * **Acelerador:** Quando essa opção é ativada, ela limita o número de trabalhos de pasta monitorados que AEM formulários processados em um determinado momento. O valor Tamanho do Lote determina o número máximo de tarefas. Para obter mais informações, consulte [controle](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Substituir arquivos existentes por um nome semelhante**: Quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como Falso, os arquivos e pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.
   * **Preservar Arquivos Na Falha:** Quando definido como True, os arquivos de entrada são preservados em caso de falha. O valor padrão é true.
   * **Incluir Arquivos Com Padrão:** Especifique uma lista de padrões delimitada por ponto e vírgula (;) que a pasta assistida usa para determinar quais pastas e arquivos devem ser digitalizados e coletados. Por exemplo, se o Padrão de inclusão de arquivo for inserido, todos os arquivos e pastas que correspondem à entrada serão selecionados. Para obter mais informações, consulte [Ajuda da administração](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Invocar pasta assistida de forma assíncrona:** Identifica o tipo de invocação como assíncrona ou síncrona. O valor padrão é assíncrono. Recomenda-se o assíncrono para processos de longa duração, enquanto o síncrono é recomendado para processos transitórios ou de curta duração.
   * **Habilitar pasta assistida:** Quando essa opção é ativada, a pasta de monitoramento é ativada. O valor padrão é True.



## Modificar propriedades de uma pasta observada existente {#modify-properties-of-an-existing-watched-folder}

Além de alterar o nome da pasta assistida, você pode modificar todas as propriedades de uma pasta assistida existente. Execute as seguintes etapas para modificar as propriedades de uma pasta assistida existente:

1. Toque no **Adobe Experience Manager** ícone no canto superior esquerdo da tela.
1. Toque **Ferramentas** > **Forms** > **Configurar pasta assistida.** Uma lista de pastas de controle já configuradas é exibida.
1. No lado esquerdo da tela Pasta assistida, selecione a pasta de observação e toque em **Editar.** Uma lista de campos necessários para criar a pasta assistida é exibida. Os campos listados na variável **Básico** As guias são obrigatórias. A guia advanced contém mais campos. A maioria desses campos contém um valor padrão. Você pode modificar essas propriedades de acordo com suas necessidades.
1. Depois de modificar as propriedades, toque em **Atualizar**. As propriedades modificadas são salvas.
