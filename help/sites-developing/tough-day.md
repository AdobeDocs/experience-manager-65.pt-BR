---
title: Dia difícil
description: O teste Dia difícil simula a carga diária de cerca de 1000 autores em um cenário de pior caso, com todas as operações ocorrendo ao mesmo tempo.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# Dia difícil{#tough-day}

## O que é difícil dia 2 {#what-is-tough-day}

&quot;Dia difícil 2&quot; é um aplicativo que permite testar os limites da sua instância de AEM. Ele pode ser executado imediatamente com o conjunto de testes padrão ou pode ser configurado para atender às suas necessidades de teste. Você pode assistir [esta gravação](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) para a apresentação do pedido.

>[!CAUTION]
>
>O Dia Difícil 2 exige o Java™ 8.

## Como executar difícil dia 2 {#how-to-run-tough-day}

Baixe a versão mais recente do Dia difícil 2 do [Repositório Adobe](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). Após baixar o aplicativo, é possível executá-lo imediatamente, fornecendo a `host` parâmetro. No exemplo a seguir, a instância AEM é executada localmente para que o `localhost` o valor é usado:

```xml
java -jar toughday2.jar --host=localhost
```

O conjunto padrão executado após a adição dos parâmetros é nomeado como `toughday`. Ele contém os seguintes casos de uso:

* Criar páginas e Live Copies para elas (incluindo implantações)
* Obter Página Inicial
* Executar consultas no querybuilder
* Criar hierarquias de ativos
* Excluir ativos

O conjunto contém 15% de ações de gravação e 85% de ações de leitura.

Para executar os testes do conjunto, o Dia Difícil 2 instalará seu pacote de conteúdo padrão. Isso pode ser evitado definindo o `installsamplecontent`parâmetro para `false`, mas lembre-se de que você também deve alterar os caminhos padrão para os testes que pretende executar. Se o jar for executado sem parâmetros, o Dia Difícil 2 exibirá a variável [informações de ajuda](/help/sites-developing/tough-day.md#getting-help).

Como regra, você pode usar o aplicativo seguindo este padrão:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
O Dia Difícil 2 não tem uma etapa de limpeza. Como resultado, é recomendável executar o Dia de resistência 2 em uma instância de preparo clonada e não na instância de produção principal. A instância de preparo deve ser descartada após os testes.
>

### Obtendo ajuda {#getting-help}

O Dia Difícil 2 oferece uma ampla variedade de opções de ajuda que podem ser acessadas a partir da linha de comando. Por exemplo:

```xml
java -jar toughday2.jar --help_full
```

Na tabela abaixo, você pode encontrar os parâmetros de ajuda relevantes.

<table>
 <tbody>
  <tr>
   <td><strong>Parâmetro</strong></td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exemplo</strong></td>
  </tr>
  <tr>
   <td>--ajuda</td>
   <td>Imprime informações globais, por exemplo: as ações disponíveis, conjuntos predefinidos, modos de execução e parâmetros globais.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Imprime todos os editores disponíveis.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>Imprime as classes de teste e suas descrições.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Imprime todos os itens acima, além de testes, editores e componentes de conjuntos.</td>
   <td> </td>
  </tr>
  <tr>
   <td> — help — runmode/publishmode type=&lt;mode&gt;</td>
   <td>Lista informações sobre o modo de execução ou publicação especificado.</td>
   <td><p>Java™ - jar toughday2.jar — help — runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>— help — suite=&lt;suitename&gt;</td>
   <td>Lista todos os testes de um determinado conjunto e suas respectivas propriedades configuráveis.</td>
   <td><br /> Java™ - jar toughday2.jar — help — suite=get_tests</td>
  </tr>
  <tr>
   <td> — help — tag=&lt;tag&gt;</td>
   <td><br /> Lista todos os itens que têm a tag especificada.</td>
   <td>Java™ -jar toughday2.jar — help —tag=publish</td>
  </tr>
  <tr>
   <td>— help &lt;testclass publisherclass=""&gt;</td>
   <td><br /> Lista todas as propriedades configuráveis para determinado teste ou editor.</td>
   <td><p>Java™ -jar toughday2.jar —ajuda UploadPDFTest</p> <p>Java™ -jar toughday2.jar —ajuda CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parâmetros Globais {#global-parameters}

O Dia Difícil 2 oferece parâmetros globais que definem ou alteram o ambiente para os testes. Isso inclui o host de destino, o número da porta, o protocolo usado, o usuário e a senha da instância e muito mais. Por exemplo:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Você pode encontrar os parâmetros relevantes na lista abaixo:

| **Parâmetro** | **Descrição** | **Valor padrão** | **Valores possíveis** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Instala ou ignora o pacote de conteúdo padrão do Dia Difícil 2. | verdadeiro | verdadeiro ou falso |
| `--protocol=<Val>` | O protocolo usado para o host. | http | http ou https |
| `--host=<Val>` | O nome do host ou IP que será direcionado. |  |  |
| `--port=<Val>` | A porta do host. | 4502 |  |
| `--user=<Val>` | O nome de usuário da instância. | admin |  |
| `--password=<Val>` | Senha do usuário especificado. | admin |  |
| `--duration=<Val>` | A duração dos testes. Pode ser expresso em (**s**)segundos, (**m**)minutos, (**h**)horas e (**d** Dias. | 1d |  |
| `--timeout=<Val>` | Por quanto tempo um teste será executado antes de ser interrompido e marcado como reprovado. Expressa em segundos. | 180 |  |
| `--suite=<Val>` | O valor pode ser um ou uma lista (separada por vírgulas) de conjuntos de testes predefinidos. | toughday |  |
| `--configfile=<Val>` | O arquivo de configuração yaml de destino. |  |  |
| `--contextpath=<Val>` | Caminho de contexto da instância. |  |  |
| `--loglevel=<Val>` | O nível de log do mecanismo Dia Difícil 2. | INFO | ALL, DEBUG, INFO, WARN, ERROR, FATAL, OFF |
| `--dryrun=<Val>` | Se verdadeiro, imprime a configuração resultante e não executa nenhum teste. | falso | verdadeiro ou falso |

## Personalização {#customizing}

A personalização pode ser obtida de duas maneiras: parâmetros de linha de comando ou arquivos de configuração yaml. **Os arquivos de configuração são usados para grandes conjuntos personalizados e eles substituem os parâmetros padrão do Dia difícil 2. Os parâmetros de linha de comando substituem os arquivos de configuração e os parâmetros padrão.**

A única maneira de salvar uma configuração de teste é copiá-la no formato yaml.

### Adicionar um novo teste {#adding-a-new-test}

Se não quiser usar o padrão `toughday` conjunto de relatórios, é possível adicionar um teste de sua escolha usando o `add` parâmetro. Os exemplos abaixo mostram como adicionar a variável `CreateAssetTreeTest` teste usando parâmetros de linha de comando ou um arquivo de configuração yaml.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Adicionar várias instâncias do mesmo teste  {#adding-multiple-instances-of-the-same-test}

Você também pode adicionar e executar várias instâncias do mesmo teste, mas cada instância deve ter um nome exclusivo. Os exemplos abaixo mostram como adicionar duas instâncias do mesmo teste usando parâmetros de linha de comando ou um arquivo de configuração yaml.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### Alterando as propriedades do teste {#changing-the-test-properties}

Caso precise alterar uma ou mais propriedades de teste, é possível adicionar essa propriedade à linha de comando ou ao arquivo de configuração yaml. Para ver todas as propriedades de teste disponíveis, adicione o `--help <TestClass/PublisherClass>` para a linha de comando, por exemplo:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Lembre-se de que os arquivos de configuração yaml substituirão os parâmetros padrão do Dia Difícil 2 e os parâmetros de linha de comando substituirão os arquivos de configuração e os padrões.

Os exemplos abaixo mostram como alterar o `template` propriedade para o `CreatePageTreeTest` teste usando parâmetros de linha de comando ou um arquivo de configuração yaml.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Trabalhar com conjuntos de testes predefinidos {#working-with-predefined-test-suites}

Os exemplos abaixo mostram como adicionar um teste a um conjunto predefinido e como reconfigurar e excluir um teste existente de um conjunto predefinido.

É possível adicionar um novo teste a uma suíte predefinida usando a `add` e especificando o conjunto predefinido de públicos-alvos.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Os testes existentes em um determinado conjunto também podem ser reconfigurados usando o `config`* *parâmetro. Você também deve especificar o nome do conjunto e o nome real do teste (não o nome da Classe de Teste). Você pode encontrar o nome do teste na variável `name` propriedade da classe de teste. Para obter mais detalhes sobre como encontrar propriedades de teste, leia a [Alterando propriedades de teste](/help/sites-developing/tough-day.md#changing-the-test-properties) seção.

No exemplo abaixo, o título de ativo padrão para o `CreatePageTreeTest` (nomeado como `UploadAsset`) foi alterado para &quot;NewAsset&quot;.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Além disso, também é possível remover testes de conjuntos ou editores predefinidos da configuração padrão usando o `exclude` parâmetro. Você também deve especificar o nome do conjunto e o nome real do teste (não o Test C `lass` nome). Você pode encontrar o nome do teste na variável `name` propriedade da classe de teste. No exemplo abaixo, a variável `CreatePageTreeTest` (nomeado como `UploadAsset`) é removido do conjunto de dias úteis.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Ao usar um arquivo de configuração yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modos de execução {#run-modes}

O Dia Difícil 2 pode ser executado em um dos seguintes modos: **normal** e **carga constante**.

A variável **normal** o modo de execução tem dois parâmetros:

* `concurrency` - a simultaneidade representa o número de threads que o Dia Difícil 2 criará para execução de teste. Nesses threads, os testes serão executados até que a duração tenha se esgotado ou que não haja mais testes para executar.

* `waittime` - o tempo de espera entre duas execuções de teste consecutivas no mesmo thread. O valor deve ser expresso em milissegundos.

O exemplo abaixo mostra como adicionar os parâmetros usando a linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

ou usando um arquivo de configuração yaml:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

A variável **carga constante** o modo de execução difere do modo de execução normal gerando um número constante de execuções de teste iniciadas, em vez de um número constante de threads. Você pode definir a carga usando o parâmetro de modo de execução com o mesmo nome.

### Testar seleção {#test-selection}

O processo de seleção de teste é o mesmo para ambos os modos de execução e é executado da seguinte maneira: todos os testes têm uma `weight` propriedade, que determina a probabilidade de execução em um thread. Por exemplo, se você tiver dois testes, um com um peso de 5 e o outro com um peso de 10, o último terá duas vezes mais probabilidade de ser executado do que o primeiro.

Além disso, os testes `count` propriedade, que limita o número de execuções a um determinado número. Após esse número ser aprovado, não ocorrerá mais nenhuma execução do teste. Todas as instâncias de teste que já estão em execução concluirão a execução como configurada. O exemplo a seguir mostra como adicionar esses parâmetros na linha de comando ou usando um arquivo de configuração yaml.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

ou

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
Devido a execuções paralelas, o número real de execuções de teste não será exatamente a quantidade configurada no `count` parâmetro. Espere um desvio proporcional ao número de threads em execução (controlado pelo `concurrency parameter`).

### Execução de prática {#dry-run}

Uma execução seca analisa todas as entradas fornecidas (parâmetros de linha de comando ou arquivos de configuração), mesclando-as com os padrões e, em seguida, gera os resultados. Ele não executa nenhum dos testes.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Saída {#output}

O Dia difícil 2 gera métricas de teste e logs. Para obter mais detalhes, leia as seções a seguir.

### Métricas de teste {#test-metrics}

Atualmente, o Dia difícil 2 relata nove métricas de teste que você pode avaliar. Métricas com o **&#42;** símbolo são relatados somente após execuções bem-sucedidas:

| **Nome** | **Descrição** |
|---|---|
| Carimbo de data e hora | Carimbo de data e hora da última execução de teste concluída. |
| Aprovado | Número de execuções com êxito. |
| Falhou | Número de execuções com falha. |
| Mín&#42; | Menor duração de execução de teste. |
| Max&#42; | Maior duração de execução de teste. |
| Mediana&#42; | Duração média computada de todas as execuções de teste. |
| Média&#42; | Duração média computada de todas as execuções de teste. |
| StdDev&#42; | O desvio padrão. |
| 90p&#42; | 90 por cento. |
| 99p&#42; | 99 por cento. |
| 99.9p&#42; | 99,9 por cento. |
| Taxa de transferência real&#42; | Número de execuções dividido pelo tempo de execução decorrido. |

Essas métricas são escritas com a ajuda de editores que podem ser adicionadas com o `add` (de forma semelhante à adição de testes). Atualmente, há duas opções:

* **CSVPublisher** - a saída é um arquivo CSV.
* **ConsolePublisher** - a saída é exibida no console.

Por padrão, ambos os editores estão ativados.

Além disso, há dois modos nos quais as métricas são relatadas:

* A variável **simples** modo de publicação — relata os resultados do início da execução até o ponto de publicação.
* A variável **intervalos** modo de publicação - relata os resultados em um determinado intervalo de tempo. Você pode definir o intervalo de tempo com a variável **intervalo** parâmetro do modo de publicação.

O exemplo a seguir mostra como configurar o `intervals` na linha de comando ou usando um arquivo de configuração yaml.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Ao usar um arquivo de configuração yaml:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Logs {#logging}

O Dia Difícil 2 cria uma pasta de logs no mesmo diretório em que você executou o Dia Difícil 2. Esta pasta contém dois tipos de logs:

* **toughday.log**: contém mensagens relacionadas ao estado do aplicativo, informações de depuração e mensagens globais.
* **dia difícil_&lt;testname>.log**: mensagens relacionadas ao teste especificado.

Os logs não são substituídos, as execuções subsequentes anexam mensagens aos logs existentes. Os logs têm vários níveis. Para obter mais informações, consulte a ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
