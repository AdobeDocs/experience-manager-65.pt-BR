---
title: Dia difícil
seo-title: Dia difícil
description: O teste de Dia Difícil simula a carga diária de cerca de 1.000 autores em um cenário pior, com todas as operações em andamento ao mesmo tempo.
seo-description: O teste de Dia Difícil simula a carga diária de cerca de 1.000 autores em um cenário pior, com todas as operações em andamento ao mesmo tempo.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Dia difícil{#tough-day}

## O que é o Dia Difícil 2 {#what-is-tough-day}

&quot;Dia difícil 2&quot; é um aplicativo que permite que você teste os limites da sua instância do AEM. Pode ser executado fora da caixa com o conjunto de testes padrão ou pode ser configurado para atender às suas necessidades de teste. Você pode assistir a [esta gravação](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) para uma apresentação do aplicativo.

## Como executar o Dia 2 difícil {#how-to-run-tough-day}

Baixe a versão mais recente do Dia 2 difícil do Repositório [da](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)Adobe. Depois de baixar o aplicativo, você pode executá-lo fora da caixa fornecendo o `host` parâmetro. No exemplo a seguir, a instância do AEM é executada localmente para que o `localhost` valor seja usado:

```xml
java -jar toughday2.jar --host=localhost
```

O conjunto padrão que é executado após a adição dos parâmetros é nomeado `toughday`. Ele contém os seguintes casos de uso:

* Criar páginas e cópias ao vivo para elas (incluindo rolluts)
* Obter página inicial
* Executar consultas no querybuilder
* Criar hierarquias de ativos
* Excluir ativos

O conjunto contém 15% de ações de gravação e 85% de ações de leitura.

Para executar os testes de conjunto, o Dia 2 difícil instalará seu pacote de conteúdo padrão. Isso pode ser evitado definindo o `installsamplecontent`parâmetro como `false`, mas lembre-se de que você também deve alterar os caminhos padrão para os testes que pretende executar. Se o jar for executado sem parâmetros, o Dia 2 difícil exibirá as informações [de](/help/sites-developing/tough-day.md#getting-help)ajuda.

Como regra geral, você pode usar o aplicativo seguindo este padrão:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>O Dia 2 difícil não tem uma etapa de limpeza. Como resultado, é recomendável executar o Dia 2 difícil em uma instância de armazenamento temporário clonada e não na instância de produção principal. A instância de preparo deve ser removida após os testes.


### Obter ajuda {#getting-help}

O Dia 2 difícil oferece uma grande variedade de opções de ajuda que podem ser acessadas da linha de comando. Por exemplo:

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
   <td>—help_testing</td>
   <td>Imprime as classes de teste e sua descrição.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Imprime todas as opções acima, além de testes, editores e componentes do suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Modo&gt;</td>
   <td>Lista informações sobre o modo de execução ou publicação especificado.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervalos</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>Lista todos os testes de um determinado conjunto e suas respectivas propriedades configuráveis.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_testing</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> Lista todos os itens que têm a tag especificada.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Lista todas as propriedades configuráveis para o teste ou editor em questão.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPubeleer</p> </td>
  </tr>
 </tbody>
</table>

### Parâmetros globais {#global-parameters}

O Dia 2 difícil oferece parâmetros globais que definem ou alteram o ambiente para os testes. Eles incluem o host alvo, o número da porta, o protocolo usado, o usuário e a senha da instância e muito mais. Por exemplo:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Você pode encontrar os parâmetros relevantes na lista abaixo:

| **Parâmetro** | **Descrição** | **Valor padrão** | **Valores possíveis** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Instala ou ignora o pacote de conteúdo padrão do Dia difícil 2. | verdadeiro |  true ou false |
| `--protocol=<Val>` | O protocolo usado para o host. | http | http ou https |
| `--host=<Val>` | O nome do host ou IP que será direcionado. |  |  |
| `--port=<Val>` | A porta do host. | 4502 |  |
| `--user=<Val>` | O nome de usuário da instância. | admin |  |
| `--password=<Val>` | Senha para o usuário em questão. | admin |  |
| `--duration=<Val>` | A duração dos testes. Pode ser expresso em (**s**)segundos, (**m**)minutos, (**h**)horas e (**d**)dias. | 1d |  |
| `--timeout=<Val>` | Quanto tempo um teste será executado antes de ser interrompido e marcado como reprovado. Expresso em segundos. | 180 |  |
| `--suite=<Val>` | O valor pode ser uma ou uma lista (separada por vírgulas) de conjuntos de testes predefinidos. | dia difícil |  |
| `--configfile=<Val>` | O arquivo de configuração de email de destino. |  |  |
| `--contextpath=<Val>` | Caminho de contexto da instância. |  |  |
| `--loglevel=<Val>` | O nível de log do mecanismo do Dia 2 Difícil. | INFO | TUDO, DEPURAR, INFORMAÇÕES, AVISO, ERRO, FATAL, DESLIGADO |
| `--dryrun=<Val>` | Se verdadeiro, imprime a configuração resultante e não executa nenhum teste. | falso |  true ou false |

## Personalização {#customizing}

A personalização pode ser alcançada de duas formas: parâmetros de linha de comando ou arquivos de configuração de exemplo. **Os arquivos de configuração geralmente são usados para conjuntos personalizados grandes e substituirão os parâmetros padrão do Dia 2 difícil. Os parâmetros da linha de comando substituem os arquivos de configuração e os parâmetros padrão.**

A única maneira de salvar uma configuração de teste é copiá-la em formato de vídeo. Para obter detalhes adicionais, consulte esta configuração [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) e os exemplos de configuração de yaml nas seções abaixo.

### Adicionando um novo teste {#adding-a-new-test}

Se você não quiser usar o `toughday` conjunto padrão, poderá adicionar um teste de sua escolha usando o `add` parâmetro. Os exemplos abaixo mostram como adicionar o teste `CreateAssetTreeTest` usando parâmetros de linha de comando ou um arquivo de configuração de modelo.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Ao usar um arquivo de configuração de email:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Adicionando várias instâncias do mesmo teste {#adding-multiple-instances-of-the-same-test}

Você também pode adicionar e executar várias instâncias do mesmo teste, mas cada instância deve ter um nome exclusivo. Os exemplos abaixo mostram como adicionar duas instâncias do mesmo teste usando parâmetros de linha de comando ou um arquivo de configuração de vídeo.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Ao usar um arquivo de configuração de email:

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

### Alteração das propriedades de teste {#changing-the-test-properties}

Caso seja necessário alterar uma ou mais propriedades de teste, é possível adicionar essa propriedade à linha de comando ou ao arquivo de configuração de vídeo. Para ver todas as propriedades de teste disponíveis, adicione o `--help <TestClass/PublisherClass>` parâmetro à linha de comando, por exemplo:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Lembre-se de que os arquivos de configuração do Yaml substituirão os parâmetros padrão do Dia 2 difícil e os parâmetros da linha de comando substituirão os arquivos de configuração e os padrões.

Os exemplos abaixo mostram como alterar a `template` propriedade do `CreatePageTreeTest` teste usando os parâmetros da linha de comando ou um arquivo de configuração de modelo.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Ao usar um arquivo de configuração de email:

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

Você pode adicionar um novo teste a um conjunto predefinido usando o `add` parâmetro e especificando o conjunto predefinido direcionado.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Ao usar um arquivo de configuração de email:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Os testes existentes em um determinado conjunto também podem ser reconfigurados usando o parâmetro `config`* *. Observe que você também deve especificar o nome do conjunto e o nome real do teste (não o nome da classe de teste). Você pode encontrar o nome do teste na `name` propriedade da Classe de teste. Para obter mais detalhes sobre como localizar propriedades de teste, leia a seção [Alterando propriedades](/help/sites-developing/tough-day.md#changing-the-test-properties) de teste.

No exemplo abaixo, o título do ativo padrão `CreatePageTreeTest` (nomeado `UploadAsset`) é alterado para &quot;NewAsset&quot;.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Ao usar um arquivo de configuração de email:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Além disso, também é possível remover testes de conjuntos ou editores predefinidos da configuração padrão com o uso do `exclude` parâmetro. Observe que você também deve especificar o nome do conjunto e o nome real do teste (não o `lass` nome Test C). Você pode encontrar o nome do teste na `name` propriedade da classe de teste. No exemplo abaixo, o teste `CreatePageTreeTest` (nomeado `UploadAsset`) é removido da suíte de dias de dura.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Ao usar um arquivo de configuração de email:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modos de execução {#run-modes}

O Dia 2 difícil pode ser executado em um dos seguintes modos: carga **normal** e **constante**.

O modo de execução **normal** tem dois parâmetros:

* `concurrency` - simultaneidade representa o número de threads que o Dia 2 difícil criará para execução de teste. Nesses processos, os testes serão executados até que a duração tenha terminado ou não haja mais testes para executar.

* `waittime` - o tempo de espera entre duas execuções consecutivas de teste no mesmo thread. O valor deve ser expresso em milissegundos.

O exemplo abaixo mostra como adicionar os parâmetros usando a linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

ou usando um arquivo de configuração de modelo:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

O modo de execução de carga **** constante difere do modo de execução normal ao gerar um número constante de execuções de teste iniciadas, em vez de um número constante de threads. Você pode definir a carga usando o parâmetro de modo de execução com o mesmo nome.

### Seleção de teste {#test-selection}

O processo de seleção de teste é o mesmo para ambos os modos de execução e é assim: todos os testes têm uma `weight` propriedade, que determina a probabilidade de execução em um thread. Por exemplo, se tivermos dois testes, um com peso de 5 e outro com peso de 10, o último é duas vezes mais provável de ser executado do que o primeiro.

Além disso, os testes podem ter uma `count` propriedade, o que limita o número de execuções a um determinado número. Após esse número ser aprovado, nenhuma execução adicional do teste ocorrerá. Todas as instâncias de teste que já estão em execução concluirão a execução como configurado. O exemplo a seguir mostra como adicionar esses parâmetros na linha de comando ou usando um arquivo de configuração de modelo.

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
>Devido a execuções paralelas, o número real de execuções de teste não será exatamente a quantidade configurada no `count` parâmetro. Esperar um desvio proporcional ao número de threads em execução (controlado pelo `concurrency parameter`).

### Execução de prática {#dry-run}

Uma execução em seco analisa todas as entradas (parâmetros de linha de comando ou arquivos de configuração), mesclando-os com os padrões e, em seguida, gera os resultados. Não executa nenhum dos testes.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Saída {#output}

O Dia 2 difícil gera métricas de teste e registros. Para obter mais detalhes, leia as seções a seguir.

### Testar métricas {#test-metrics}

O Dia 2 difícil atualmente relata 9 métricas de teste que você pode avaliar. As métricas com o símbolo ***** são reportadas somente após execuções bem-sucedidas:

| **Nome** | **Descrição** |
|---|---|
| Carimbo de data e hora | Carimbo de data e hora da última execução de teste concluída. |
| Aprovado | Número de execuções bem-sucedidas. |
| Falhou | Número de execuções com falha. |
| Mínimo* | Duração mais baixa da execução do teste. |
| Máximo* | A maior duração da execução do teste. |
| Mediana* | Duração mediana calculada de todas as execuções de teste. |
| Média* | Duração média calculada de todas as execuções de teste. |
| StdDev* | O desvio padrão. |
| 90p* | 90%. |
| 99p* | 99%. |
| 99,9 p* | 99,9 percentil. |
| Throughput real* | Número de execuções dividido pelo tempo de execução decorrido. |

Essas métricas são gravadas com a ajuda de editores que podem ser adicionados com o `add` parâmetro (de forma semelhante à adição de testes). Atualmente, existem duas opções:

* **CSVPubeleer** - a saída é um arquivo CSV.
* **ConsolePublisher** - a saída é exibida no console.

Por padrão, ambos os editores estão habilitados.

Além disso, há dois modos nos quais as métricas são reportadas:

* O modo de publicação **simples** - relata os resultados do início da execução até o ponto de publicação.
* O modo de publicação de **intervalos** - relata os resultados em um determinado período. Você pode definir o período com o parâmetro de modo de publicação de **intervalo** .

O exemplo a seguir mostra como configurar o `intervals` parâmetro na linha de comando ou usando um arquivo de configuração de modelo.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Ao usar um arquivo de configuração de email:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Registro {#logging}

O Dia 2 difícil cria uma pasta de registros no mesmo diretório em que você executou o Dia 2 difícil. Esta pasta contém dois tipos de registros:

* **toughday.log**: contém mensagens relacionadas ao estado do aplicativo, informações de depuração e mensagens globais.
* **toughday_&lt;testname>.log**: mensagens relacionadas ao teste especificado.

Os registros não são substituídos, as execuções subsequentes anexarão mensagens aos registros existentes. Os registros têm vários níveis, para obter mais informações, consulte o ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Exemplo de uso {#example-usage}

#### Problemas conhecidos {#known-issues}

[Obter arquivo](assets/toughday-6_1.jar)
