---
title: Dia difícil
seo-title: Dia difícil
description: O teste Tough Day simula a carga diária de cerca de 1000 autores em um cenário pior, com todas as operações acontecendo ao mesmo tempo.
seo-description: O teste Tough Day simula a carga diária de cerca de 1000 autores em um cenário pior, com todas as operações acontecendo ao mesmo tempo.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
translation-type: tm+mt
source-git-commit: 3727b561a2ee9778d75f18530caf16c6c3ef846a
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 2%

---

# Dia difícil{#tough-day}

## O que é o Dia 2 difícil {#what-is-tough-day}

&quot;Dia 2 difícil&quot; é um aplicativo que permite testar os limites da sua instância do AEM. Ele pode ser executado imediatamente com o conjunto de teste padrão ou pode ser configurado para atender às suas necessidades de teste. Você pode assistir a [esta gravação](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) para uma apresentação do aplicativo.

## Como executar o Dia 2 difícil {#how-to-run-tough-day}

Baixe a versão mais recente do Tough Day 2 no [Adobe Repository](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/). Depois de baixar o aplicativo, você pode executá-lo imediatamente fornecendo o parâmetro `host`. No exemplo a seguir, a instância AEM é executada localmente para que o valor `localhost` seja usado:

```xml
java -jar toughday2.jar --host=localhost
```

O conjunto padrão que é executado depois de adicionar os parâmetros é chamado de `toughday`. Ele contém os seguintes casos de uso:

* Criar páginas e cópias ao vivo para elas (incluindo implantações)
* Obter página inicial
* Executar consultas no querybuilder
* Criar hierarquias de ativos
* Excluir ativos

O conjunto contém 15% de ações de gravação e 85% de ações de leitura.

Para executar os testes do conjunto, o Dia 2 difícil instalará seu pacote de conteúdo padrão. Isso pode ser evitado definindo o parâmetro `installsamplecontent`como `false`, mas lembre-se de que você também deve alterar os caminhos padrão dos testes que pretende executar. Se o jar for executado sem parâmetros, o Dia 2 difícil exibirá as [informações de ajuda](/help/sites-developing/tough-day.md#getting-help).

Como regra geral, você pode usar o aplicativo seguindo este padrão:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Embora o Dia 2 não tenha um passo de limpeza. Como resultado, é recomendável executar o Dia 2 difícil em uma instância de armazenamento temporário clonada e não na instância de produção principal. A instância de preparo deve ser removida após os testes.


### Obter ajuda {#getting-help}

Embora o Dia 2 ofereça uma ampla variedade de opções de ajuda que podem ser acessadas a partir da linha de comando. Por exemplo:

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
   <td>Imprime tudo acima, além de testes, editores e componentes do conjunto.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>Lista informações sobre o modo de execução ou publicação especificado.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervalos</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>Lista todos os testes de um determinado conjunto e suas respectivas propriedades configuráveis.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> Lista todos os itens que têm a tag especificada.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Lista todas as propriedades configuráveis para o teste ou editor em questão.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parâmetros globais {#global-parameters}

O Dia 2 difícil oferece parâmetros globais que definem ou alteram o ambiente para os testes. Isso inclui o host que é direcionado, o número da porta, o protocolo usado, o usuário e a senha da instância e muito mais. Por exemplo:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Você pode encontrar os parâmetros relevantes na lista abaixo:

| **Parâmetro** | **Descrição** | **Valor padrão** | **Valores possíveis** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Instala ou ignora o pacote de conteúdo padrão Tough Day 2. | verdadeiro | verdadeiro ou falso |
| `--protocol=<Val>` | O protocolo usado para o host. | http | http ou https |
| `--host=<Val>` | O nome do host ou IP que será direcionado. |  |  |
| `--port=<Val>` | A porta do host. | 4502 |  |
| `--user=<Val>` | O nome de usuário da instância. | admin |  |
| `--password=<Val>` | Senha para o usuário em questão. | administrador |  |
| `--duration=<Val>` | A duração dos testes. Pode ser expresso em (**s**)segundos, (**m**)minutos, (**h**)ours e (**d**)ays. | 1d |  |
| `--timeout=<Val>` | Por quanto tempo um teste será executado antes de ser interrompido e marcado como defeituoso. Expressa em segundos. | 180 |  |
| `--suite=<Val>` | O valor pode ser uma lista ou uma lista (separada por vírgulas) de conjuntos de testes predefinidos. | dilema |  |
| `--configfile=<Val>` | O arquivo de configuração de código direcionado. |  |  |
| `--contextpath=<Val>` | Caminho de contexto da instância. |  |  |
| `--loglevel=<Val>` | O nível de log do mecanismo do Dia 2 Difícil. | INFO | TUDO, DEPURAR, INFORMAÇÕES, AVISO, ERRO, FATAL, DESLIGADO |
| `--dryrun=<Val>` | Se verdadeiro, imprime a configuração resultante e não executa testes. | falso | verdadeiro ou falso |

## Personalização {#customizing}

A personalização pode ser alcançada de duas formas: parâmetros de linha de comando ou arquivos de configuração de yaml. **Os arquivos de configuração geralmente são usados para conjuntos personalizados grandes e substituirão os parâmetros padrão do Dia difícil 2 . Os parâmetros da linha de comando substituem os arquivos de configuração e os parâmetros padrão.**

A única maneira de salvar uma configuração de teste é copiá-la em formato de email. Para obter detalhes adicionais, consulte esta configuração [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) e os exemplos de configuração de yaml nas seções abaixo.

### Adicionar um novo teste {#adding-a-new-test}

Se você não quiser usar o conjunto `toughday` padrão, poderá adicionar um teste de sua escolha usando o parâmetro `add`. Os exemplos abaixo mostram como adicionar o teste `CreateAssetTreeTest` usando parâmetros de linha de comando ou um arquivo de configuração de código.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Usando um arquivo de configuração de exemplo:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Adicionar várias instâncias do mesmo teste {#adding-multiple-instances-of-the-same-test}

Você também pode adicionar e executar várias instâncias do mesmo teste, mas cada instância deve ter um nome exclusivo. Os exemplos abaixo mostram como adicionar duas instâncias do mesmo teste usando parâmetros de linha de comando ou um arquivo de configuração de exemplo.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Usando um arquivo de configuração de exemplo:

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

### Alterar as propriedades de teste {#changing-the-test-properties}

Caso precise alterar uma ou mais propriedades de teste, é possível adicionar essa propriedade à linha de comando ou ao arquivo de configuração de código. Para ver todas as propriedades de teste disponíveis, adicione o parâmetro `--help <TestClass/PublisherClass>` à linha de comando, por exemplo:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Lembre-se de que os arquivos de configuração do yaml substituirão os parâmetros padrão Tough Day 2 e os parâmetros de linha de comando substituirão os arquivos de configuração e os padrões.

Os exemplos abaixo mostram como alterar a propriedade `template` para o teste `CreatePageTreeTest` usando parâmetros de linha de comando ou um arquivo de configuração de código.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Usando um arquivo de configuração de exemplo:

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

Você pode adicionar um novo teste a um conjunto predefinido usando o parâmetro `add` e especificando o conjunto predefinido direcionado.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Usando um arquivo de configuração de exemplo:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Os testes existentes em um determinado conjunto também podem ser reconfigurados usando o parâmetro `config`* *. Observe que você também deve especificar o nome do conjunto e o nome real do teste (não o nome da Classe de teste). Você pode encontrar o nome do teste na propriedade `name` da Classe de teste. Para obter mais detalhes sobre como encontrar propriedades de teste, leia a seção [Alteração das propriedades de teste](/help/sites-developing/tough-day.md#changing-the-test-properties) .

No exemplo abaixo, o título padrão do ativo para `CreatePageTreeTest` (chamado `UploadAsset`) é alterado para &quot;NewAsset&quot;.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Usando um arquivo de configuração de exemplo:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Além disso, também é possível remover testes de conjuntos ou editores predefinidos da configuração padrão com o uso do parâmetro `exclude`. Observe que você também deve especificar o nome do conjunto e o nome real do teste (não o nome do teste C `lass`). Você pode encontrar o nome do teste na propriedade `name` da classe de teste. No exemplo abaixo, o teste `CreatePageTreeTest` (chamado `UploadAsset`) é removido do conjunto de dias de duração.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Usando um arquivo de configuração de exemplo:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modos de execução {#run-modes}

Embora o Dia 2 possa ser executado em um dos seguintes modos: **normal** e **carga constante**.

O modo de execução **normal** tem dois parâmetros:

* `concurrency` - simultaneidade representa o número de threads que o Dia 2 difícil criará para execução de teste. Nesses threads, os testes serão executados até que a duração tenha terminado ou não haja mais testes para executar.

* `waittime` - o tempo de espera entre duas execuções consecutivas de teste no mesmo thread. O valor deve ser expresso em milissegundos.

O exemplo abaixo mostra como adicionar os parâmetros usando a linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

ou usando um arquivo de configuração de código:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

O modo de execução **constante load** difere do modo de execução normal gerando um número constante de execuções de teste iniciadas, em vez de um número constante de threads. Você pode definir a carga usando o parâmetro run mode com o mesmo nome.

### Seleção de teste {#test-selection}

O processo de seleção de teste é o mesmo para ambos os modos de execução e é assim: todos os testes têm uma propriedade `weight`, que determina a probabilidade de execução em um thread. Por exemplo, se tivermos dois testes, um com peso de 5 e outro com peso de 10, o segundo terá duas vezes mais probabilidade de ser executado do que o primeiro.

Além disso, os testes podem ter uma propriedade `count`, que limita o número de execuções a um determinado número. Após esse número ser aprovado, nenhuma outra execução do teste ocorrerá. Todas as instâncias de teste que já estão em execução concluirão a execução como configuradas. O exemplo a seguir mostra como adicionar esses parâmetros na linha de comando ou usando um arquivo de configuração de código.

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
>Devido a execuções paralelas, o número real de execuções de teste não será exatamente o valor configurado no parâmetro `count`. Espere um desvio proporcional ao número de threads em execução (controlado pelo `concurrency parameter`).

### Execução de prática {#dry-run}

Uma execução seca analisa todas as entradas fornecidas (parâmetros da linha de comando ou arquivos de configuração), mesclando-as com os padrões e, em seguida, gera os resultados. Ele não executa nenhum dos testes.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Saída {#output}

O Dia 2 difícil gera métricas de teste e registros. Para obter mais detalhes, leia as seções a seguir.

### Testar métricas {#test-metrics}

O Dia 2 difícil atualmente relata 9 métricas de teste que você pode avaliar. Métricas com o símbolo ***** são relatadas somente após execuções bem-sucedidas:

| **Nome** | **Descrição** |
|---|---|
| Carimbo de data e hora | Carimbo de data e hora da última execução de teste concluída. |
| Aprovado | Número de execuções bem-sucedidas. |
| Falhou | Número de execuções com falha. |
| Mínimo* | Duração mais baixa da execução do teste. |
| Máximo* | Maior duração de execução de teste. |
| Mediana* | Duração mediana calculada de todas as execuções de teste. |
| Média* | Duração média calculada de todas as execuções de teste. |
| StdDev* | O desvio padrão. |
| 90p* | 90 percentil. |
| 99p* | 99 percentil. |
| 99,9p* | Percentil 99,9. |
| Taxa de transferência real* | Número de execuções dividido pelo tempo de execução decorrido. |

Essas métricas são gravadas com a ajuda de editores que podem ser adicionados com o parâmetro `add` (de forma semelhante à adição de testes). Atualmente, há duas opções:

* **CSVPublisher**  - a saída é um arquivo CSV.
* **ConsolePublisher**  - a saída é exibida no console.

Por padrão, ambos os editores estão ativados.

Além disso, há dois modos nos quais as métricas são relatadas:

* O **modo de publicação simples** - relata os resultados do início da execução até o ponto de publicação.
* O **intervalos** modo de publicação - relata os resultados em um determinado intervalo de tempo. Você pode definir o período com o parâmetro de modo de publicação **intervalo** .

O exemplo a seguir mostra como configurar o parâmetro `intervals` na linha de comando ou usando um arquivo de configuração de código.

Usando parâmetros de linha de comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Usando um arquivo de configuração de exemplo:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Logs {#logging}

O Dia 2 difícil cria uma pasta de logs no mesmo diretório em que você executou o Dia 2 difícil. Esta pasta contém dois tipos de logs:

* **toughday.log**: contém mensagens relacionadas ao estado do aplicativo, informações de depuração e mensagens globais.
* **toughday_&lt;testname>.log**: mensagens relacionadas ao teste especificado.

Os logs não são substituídos, as execuções subsequentes anexarão mensagens aos logs existentes. Os logs têm vários níveis. Para obter mais informações, consulte o ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Exemplo de uso {#example-usage}

#### Problemas conhecidos {#known-issues}

[Obter arquivo](assets/toughday-6_1.jar)
