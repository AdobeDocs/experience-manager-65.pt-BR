---
title: Criar ou configurar uma pasta assistida
seo-title: Criar ou configurar uma pasta assistida
description: Saiba como criar ou excluir uma pasta assistida ou modificar as propriedades de uma pasta assistida existente.
seo-description: Saiba como criar ou excluir uma pasta assistida ou modificar as propriedades de uma pasta assistida existente.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Criar ou configurar uma pasta assistida {#create-or-configure-a-watched-folder}

Um administrador pode configurar uma pasta de rede, conhecida como pasta ** assistida, para que quando um usuário colocar um arquivo (como um arquivo PDF) na pasta assistida, uma operação pré-configurada seja iniciada e manipule o arquivo. Depois que a operação especificada é executada, a operação salva o arquivo modificado em uma pasta de saída especificada. Para obter informações detalhadas sobre como administrar uma pasta assistida, consulte a Ajuda [](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)da Administração.

Você pode usar a interface do usuário da pasta assistida para:

* Criar uma pasta assistida
* Modificar propriedades de uma pasta assistida existente
* Excluir uma pasta assistida

## Criar uma pasta assistida {#create-a-watched-folder}

Antes de configurar uma pasta assistida, verifique o seguinte:

* Pastas assistidas é um recurso avançado de formulários AEM. Requer que o pacote complementar de formulários AEM funcione. Verifique se o pacote complementar AEM Forms apropriado está instalado e configurado.
* Você pode criar a pasta assistida em um armazenamento local ou compartilhado. Verifique se o usuário dos formulários AEM configurado para executar a pasta assistida tem permissões de leitura e gravação na pasta assistida.
* Você pode usar um Serviço, Fluxo de trabalho ou um Script para automatizar uma operação com uma pasta assistida. Certifique-se de que o Serviço, o Fluxo de Trabalho ou um Script correspondente foi criado e está pronto para ser executado. Para obter informações sobre como criar um Serviço, Fluxo de trabalho e Script, consulte [Vários métodos de processamento de arquivos](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Uma pasta assistida tem várias propriedades, consulte Propriedades [da pasta](watched-folder-in-aem-forms.md#watchedfolderproperties)assistida.

Execute as seguintes etapas para criar uma pasta assistida:

1. Toque no ícone **do Adobe Experience Manager** no canto superior esquerdo da tela.
1. Toque em **Ferramentas** > **Formulários** > **Configurar pasta assistida.** Uma lista de pastas monitoradas já configuradas é exibida.
1. Toque em **Novo**. Uma lista de campos necessários para criar a pasta assistida é exibida:

   * **Nome**: Identifica a pasta assistida. Use somente caracteres alfanuméricos para o nome.
   * **Caminho**: Especifica o local da pasta monitorada. Em um ambiente clusterizado, essa configuração deve apontar para uma pasta de rede compartilhada acessível a todos os usuários que executam o AEM em diferentes nós de um cluster.
   * **Processar arquivos usando**: O tipo do processo a ser start. Você pode especificar fluxo de trabalho, script ou serviço.
   * **Nome do serviço/Caminho do script/Caminho** do fluxo de trabalho: O comportamento do campo se baseia no valor especificado para o campo **Processar arquivos usando** . Você pode especificar os seguintes valores:

      * Para Fluxo de trabalho, especifique o modelo de fluxo de trabalho a ser executado. Por exemplo, /etc/workflow/models/&lt;nome_do_fluxo de trabalho>/jcr:content/model
      * Para Script, especifique o caminho JCR do script a ser executado. Por exemplo, /etc/watchfolder/test/testScript.ecma
      * Para Serviço, especifique o filtro usado para localizar um serviço OSGi. O serviço é registrado como uma implementação da interface com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Por exemplo, o código a seguir é uma implementação personalizada da interface ContentProcessor com uma propriedade personalizada (foo=bar).
   >[!NOTE]
   >
   >Se você tiver selecionado **Serviço** para o campo **Processar arquivos usando** , o valor do campo Nome do serviço (inputProcessorType) deverá estar entre parênteses. Por exemplo, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Padrão** do arquivo de saída: Especifique uma lista de padrões delimitada por ponto-e-vírgula (;) que uma pasta assistida usa para determinar o nome e o local dos arquivos e pastas de saída. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)de arquivo.


1. Toque em **Avançado**. A guia avançada contém mais campos. A maioria desses campos contém um valor padrão.

   * **Filtro do mapeador de carga:** Quando você cria uma pasta assistida, ela cria uma estrutura de pasta dentro da pasta que está sendo assistida. A estrutura de pastas tem pastas stage, result, preserve, input e failure. A estrutura de pastas pode servir como carga de entrada para o fluxo de trabalho e aceitar saída de um fluxo de trabalho. Ele também pode lista pontos de falha, se houver. A estrutura de uma carga é diferente da estrutura de uma pasta assistida. Você pode gravar scripts personalizados para mapear a estrutura de uma pasta assistida para a carga. Esse script é chamado de filtro de mapeador de carga. Duas implementações prontas para uso do mapeador de carga estão disponíveis. Se você não tiver [uma implementação](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)personalizada, use uma implementação pronta para uso:

      * **Mapeador padrão:** Use o mapeador de carga padrão para manter o conteúdo de entrada e saída das pastas monitoradas em pastas de entrada e saída separadas na carga.
      * **Mapeador de carga simples baseado em arquivo:** Use o mapeador de carga baseado em Arquivo simples para manter o conteúdo de entrada e saída diretamente na pasta de carga. Ela não cria nenhuma hierarquia extra, como o mapeador padrão.
   * **Modo** de execução: Especifique a lista separada por vírgulas de modos de execução permitidos para execução do fluxo de trabalho.
   * **Ficheiros de Tempo Limite Preparados Após**: Especifique o número de segundos a aguardar antes que um arquivo/pasta de entrada que já foi selecionado para processamento seja tratado como tendo expirado e marcado como uma falha. O mecanismo de tempo limite só é ativado quando o valor para essa propriedade é um número positivo.
   * **Excluir arquivos preparados com tempo limite quando limitados**: Se ativado, o mecanismo **Tempo limite de arquivos preparados após** ser ativado é ativado somente quando a limitação é ativada para a pasta monitorada.
   * **Analisar a pasta de entrada depois de cada:** Especifique o intervalo de tempo, em segundos, para verificar se há entradas na pasta assistida. A menos que a configuração de aceleração esteja ativada, o Intervalo de pesquisa deve ser maior que o tempo para processar um trabalho médio; caso contrário, o sistema pode estar sobrecarregado. O valor do intervalo deve ser maior ou igual a um.
   * **Excluir padrão** de arquivo: Especifique uma lista de padrões delimitada por ponto-e-vírgula (;) que uma pasta assistida usa para determinar quais arquivos e pastas serão examinados e coletados. Nenhum arquivo ou pasta com o padrão especificado é verificado para processamento. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)de arquivo.
   * **Incluir padrão** de arquivo: Especifique uma lista de padrões delimitada por ponto-e-vírgula (;) que a pasta assistida usa para determinar quais pastas e arquivos serão examinados e coletados. Por exemplo, se Incluir padrão de arquivo for input&amp;ast;, todos os arquivos e pastas que correspondem input&amp;ast; são apanhados. O valor padrão é &amp;ast; e indica todos os arquivos e pastas. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)de arquivo.
   * **Tempo de espera:** Especifique o tempo, em milissegundos, para aguardar antes de digitalizar uma pasta ou um arquivo após sua criação. Por exemplo, se o tempo de espera for de 3.600.000 milissegundos (uma hora) e o arquivo tiver sido criado há um minuto, esse arquivo será coletado depois de 59 minutos ou mais. O valor padrão é 0.

      Essa configuração é útil para garantir que todo o conteúdo do arquivo ou pasta seja copiado para a pasta de entrada. Por exemplo, se você tiver um arquivo grande para processar e o arquivo levar dez minutos para ser baixado, defina o tempo de espera como 10&amp;ast;60 &amp;ast;1000 milissegundos. Esse intervalo impede que a pasta assistida digitalize o arquivo se ele não tiver dez minutos.

   * **Excluir resultados anteriores a:** Especifique o tempo, em número de dias, para esperar antes de excluir os Arquivos e pastas mais antigos do que o valor especificado. Essa configuração é útil para garantir que a pasta de resultados não fique cheia. Um valor de -1 dias indica que a pasta de resultados nunca será excluída. O valor padrão é -1.
   * **Nome da pasta de resultado:** Especifique o nome da pasta para armazenar os resultados. Se os resultados não forem exibidos nessa pasta, verifique a pasta de falha. Arquivos somente leitura não são processados e são salvos na pasta de falha. Você pode usar um caminho absoluto ou relativo com os seguintes padrões de arquivo:

      * %F = prefixo de nome de arquivo
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
      * Por exemplo, se forem 8 horas em 17 de julho de 2009 e você especificar C:/Test/WF0/failure/%Y/%M/%D/%H/, a pasta de resultados será C:/Test/WF0/failure/2009/07/17/20.
      * Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta assistida. O valor padrão é result/%Y/%M/%D/, que é a pasta Result dentro da pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)de arquivo.
   * **Nome da pasta de falha:** Especifique a pasta na qual os arquivos com falha são salvos. Esse local é sempre relativo à pasta assistida. Você pode usar padrões de arquivo, conforme descrito para a Pasta de resultados.
   * **Preservar nome da pasta:** Especifique a pasta onde os arquivos são armazenados após a varredura e coleta bem-sucedidas. O caminho pode ser absoluto, relativo ou nulo. Você pode usar padrões de arquivo, conforme descrito para a Pasta de resultados. O valor padrão é preserve/%Y/%M/%D/.
   * **Tamanho do lote:** Especifique o número de arquivos ou pastas a serem coletados por varredura. Evita uma sobrecarga no sistema; a verificação de muitos arquivos ao mesmo tempo pode causar uma falha. O valor padrão é 2.

      Se o intervalo de digitalização for pequeno, os threads normalmente digitalizam a pasta de entrada. Se os arquivos forem descartados com frequência na pasta assistida, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar os threads.

   * **Acender:** Quando essa opção está ativada, ela limita o número de trabalhos de pasta monitorados que os formulários AEM processam a qualquer momento. O valor Tamanho do Lote determina o número máximo de trabalhos. For more information, see [throttling](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Substituir Arquivos Existentes Por Nome** Semelhante: Quando definido como Verdadeiro, os arquivos na pasta de resultados e na pasta de preservação são substituídos. Quando definido como Falso, arquivos e pastas com um sufixo de índice numérico são usados para o nome. O valor padrão é Falso.
   * **Preservar arquivos na falha:** Quando definido como Verdadeiro, os arquivos de entrada são preservados em caso de falha. O valor padrão é true.
   * **Incluir arquivos com padrão:** Especifique uma lista de padrões delimitada por ponto-e-vírgula (;) que a pasta assistida usa para determinar quais pastas e arquivos serão examinados e coletados. Por exemplo, se o Padrão de inclusão de arquivo for inserido, todos os arquivos e pastas que correspondem à entrada serão coletados. Para obter mais informações, consulte Ajuda [da administração](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Chamar a pasta assistida assíncrona:** Identifica o tipo de invocação como assíncrono ou síncrono. O valor padrão é assíncrono. Recomenda-se assíncrono para processos de longa duração, enquanto que síncrono é recomendado para processos transitórios ou de curta duração.
   * **Ativar a pasta assistida:** Quando essa opção estiver ativada, a pasta Watch será ativada. O valor padrão é True.



## Modificar propriedades de uma pasta assistida existente {#modify-properties-of-an-existing-watched-folder}

Além de alterar o nome da pasta assistida, você pode modificar todas as propriedades de uma pasta assistida existente. Execute as seguintes etapas para modificar as propriedades de uma pasta assistida existente:

1. Toque no ícone do **Adobe Experience Manager** no canto superior esquerdo da tela.
1. Toque em **Ferramentas** > **Formulários** > **Configurar pasta assistida.** Uma lista de pastas monitoradas já configuradas é exibida.
1. No lado esquerdo da tela Pasta assistida, selecione a pasta de observação e toque em **Editar.** Uma lista de campos necessários para criar a pasta assistida é exibida. Os campos listados na guia **Básico** são obrigatórios. A guia avançada contém mais campos. A maioria desses campos contém um valor padrão. É possível modificar essas propriedades de acordo com suas necessidades.
1. Depois de modificar as propriedades, toque em **Atualizar**. As propriedades modificadas são salvas.

