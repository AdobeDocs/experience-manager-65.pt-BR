---
title: Como usar a ferramenta VLT
seo-title: Como usar a ferramenta VLT
description: A ferramenta Jackrabbit FileVault (VLT) é desenvolvida pela Fundação Apache que mapeia o conteúdo de uma instância do Jackrabbit/AEM para seu sistema de arquivos
seo-description: A ferramenta Jackrabbit FileVault (VLT) é desenvolvida pela Fundação Apache que mapeia o conteúdo de uma instância do Jackrabbit/AEM para seu sistema de arquivos
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
translation-type: tm+mt
source-git-commit: 2da3da1a36f074593e276ddd15ed8331239ab70f

---


# Como usar a ferramenta VLT {#how-to-use-the-vlt-tool}

A ferramenta Jackrabbit FileVault (VLT) é uma ferramenta desenvolvida pela Fundação [](https://www.apache.org/) Apache que mapeia o conteúdo de uma instância do Jackrabbit/AEM para seu sistema de arquivos. A ferramenta VLT tem funções semelhantes ao cliente do sistema de controle de origem (como um cliente SVN (Subversion)), fornecendo operações normais de check-in, check-out e gerenciamento, bem como opções de configuração para representação flexível do conteúdo do projeto.

Execute a ferramenta VLT na linha de comando. Este documento descreve como usar a ferramenta, incluindo como começar e obter ajuda, bem como uma lista de todos os [comandos](#vlt-commands) e [opções](#vlt-global-options)disponíveis.

## Conceitos e arquitetura {#concepts-and-architecture}

Consulte a Visão geral [do](https://jackrabbit.apache.org/filevault/overview.html) Filevault e a página do [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) na documentação [oficial do](https://jackrabbit.apache.org/filevault/index.html) Apache Jackrabbit Filevault para obter uma visão geral completa dos conceitos e da estrutura da ferramenta Filevault.

## Introdução ao VLT {#getting-started-with-vlt}

Para começar a usar o VLT, é necessário fazer o seguinte:

1. Instale o VLT, atualize as variáveis de ambiente e atualize os arquivos de subversão globais ignorados.
1. Configure o repositório do AEM (caso ainda não tenha feito isso).
1. Verifique o repositório do AEM.
1. Sincronizar com o repositório.
1. Teste se a sincronização funcionou.

### Instalação da ferramenta VLT {#installing-the-vlt-tool}

Para usar a ferramenta VLT, primeiro é necessário instalá-la. Por padrão, ele não é instalado, pois é uma ferramenta adicional. Além disso, é necessário definir a variável de ambiente do sistema.

1. Baixe o arquivo de arquivamento do FileVault no repositório de artefatos [Maven.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >A origem da ferramenta VLT está [disponível no GitHub.](https://github.com/apache/jackrabbit-filevault)
1. Extraia o arquivo.
1. Adicione `<archive-dir>/vault-cli-<version>/bin` ao seu ambiente `PATH` para que os arquivos de comando `vlt` ou `vlt.bat` sejam acessados conforme apropriado. Por exemplo:

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Abra um shell de linha de comando e execute `vlt --help`. Verifique se a saída é semelhante à tela de ajuda a seguir:

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

Depois de instalá-lo, é necessário atualizar os arquivos de subversão globais ignorados. Edite suas configurações svn e adicione o seguinte:

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### Configuração do caractere de fim de linha {#configuring-the-end-of-line-character}

O VLT trata automaticamente o Fim da Linha (EOF) de acordo com as seguintes regras:

* linhas de arquivos cujo check-out foi feito no Windows end com uma `CRLF`
* linhas de arquivos com check-out no final Linux/Unix com um `LF`
* linhas de arquivos comprometidos no repositório terminam com uma `LF`

Para garantir a correspondência entre as configurações de VLT e SVN, configure a `svn:eol-style` propriedade para `native` a extensão dos arquivos armazenados no repositório. Edite suas configurações svn e adicione o seguinte:

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### Fazendo check-out do repositório {#checking-out-the-repository}

Verifique o repositório usando o sistema de controle de origem. Em svn, por exemplo, digite o seguinte (substituindo o URI e o caminho pelo repositório):

```shell
svn co https://svn.server.com/repos/myproject
```

### Sincronização com o repositório {#synchronizing-with-the-repository}

É necessário sincronizar o arquivo padrão com o repositório. Para fazer isso:

1. Na linha de comando, navegue até `content/jcr_root`.
1. Verifique o repositório digitando o seguinte (substituindo o número da porta por **4502** e suas senhas de administrador):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >As credenciais devem ser especificadas apenas uma vez no check-out inicial. Eles serão armazenados em seu diretório inicial dentro `.vault/auth.xml`.

### Testando se a sincronização funcionou {#testing-whether-the-synchronization-worked}

Depois de fazer check-out do repositório e sincronizá-lo, você deve testar para garantir que tudo funcione corretamente. Uma maneira fácil de fazer isso é editar um arquivo **.jsp** e ver se suas alterações são refletidas após confirmar as alterações.

Para testar a sincronização:

1. Vá até `.../jcr_content/libs/foundation/components/text`.
1. Edite algo em `text.jsp`.
1. Consulte os arquivos modificados digitando `vlt st`
1. Veja as alterações digitando `vlt diff text.jsp`
1. Confirme as alterações: `vlt ci test.jsp`.
1. Recarregue uma página que contém um componente de texto e veja se as alterações estão presentes.

## Obter ajuda com a ferramenta VLT {#getting-help-with-the-vlt-tool}

Depois de instalar a ferramenta VLT, você pode acessar seu arquivo de Ajuda na linha de comando:

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

Para obter ajuda sobre um comando específico, digite o comando help seguido do nome do comando. Por exemplo:

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## Tarefas Comuns Executadas no VLT {#common-tasks-performed-in-vlt}

Veja a seguir algumas tarefas comuns executadas no VLT. Para obter informações detalhadas sobre cada comando, consulte os [comandos](#vlt-commands)individuais.

### Fazendo check-out de uma subárvore {#checking-out-a-subtree}

Se você quiser fazer check-out apenas de uma subárvore do repositório, por exemplo, `/apps/geometrixx`, digite o seguinte:

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

Isso cria uma nova raiz de exportação `geo` com um diretório `META-INF` e `jcr_root` e coloca todos os arquivos abaixo `/apps/geometrixx` no `geo/jcr_root`.

### Realização de uma finalização filtrada {#performing-a-filtered-checkout}

Se você tiver um filtro de espaço de trabalho existente e quiser usá-lo para finalização, poderá criar primeiro o `META-INF/vault` diretório e colocar o filtro lá, ou especificá-lo na linha de comando da seguinte maneira:

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

Um filtro de exemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### Uso do controle Importar/Exportar em vez do controle .vlt {#using-import-export-instead-of-vlt-control}

É possível importar e exportar conteúdo entre um repositório JCR e o sistema de arquivos local sem usar arquivos de controle.

Para importar e exportar conteúdo sem usar `.vlt` controle:

1. Inicialmente, configure o repositório:

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. Altere a cópia remota e atualize o JCR:

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. Altere a cópia remota e atualize o servidor de arquivos:

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## Uso de VLT {#using-vlt}

Para emitir comandos no VLT, digite o seguinte na linha de comando:

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

As opções e os comandos são descritos detalhadamente nas seções a seguir.

## Opções Globais de VLT {#vlt-global-options}

A seguir está uma lista de opções VLT, que estão disponíveis para todos os comandos. Consulte os comandos individuais para obter informações sobre opções adicionais disponíveis.

|  |  |
|--- |--- |
| Opção | Descrição |
| `-Xjcrlog <arg>` | Opções JcrLog estendidas |
| `-Xdavex <arg>` | Opções remotas JCR estendidas |
| `--credentials <arg>` | As credenciais padrão a serem usadas |
| `--config <arg>` | A configuração JcrFs a ser usada |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprimir o mínimo possível |
| `--version` | Imprime as informações da versão e sai do VLT |
| `--log-level <level>` | Indica o nível de log, por exemplo, o nível de log4j. |
| `-h (--help) <command>` | Imprime a ajuda desse comando em particular |

## Comandos VLT {#vlt-commands}

A tabela a seguir descreve todos os comandos VLT disponíveis. Consulte os comandos individuais para obter informações detalhadas sobre sintaxe, opções disponíveis e exemplos.

|  |  |  |
|--- |--- |--- |
| Comando | Comando abreviado | Descrição |
| `export` |  | Exporta de um repositório JCR (sistema de arquivos padrão) para o sistema de arquivos local sem arquivos de controle. |
| `import` |  | Importa um sistema de arquivos local para um repositório JCR (sistema de arquivos de cofre). |
| `checkout` | `co` | Verifica um sistema de arquivos Vault. Use-o para um repositório JCR inicial para o sistema de arquivos local. (Observação: Primeiro, faça o check-out do repositório na subversão.) |
| `analyze` |  | Analisa pacotes. |
| `status` | `st` | Imprime o status dos arquivos e diretórios da cópia de trabalho. |
| `update` | `up` | Importa alterações do repositório para a cópia de trabalho. |
| `info` |  | Exibe informações sobre um arquivo local. |
| `commit` | `ci` | Envia alterações da sua cópia de trabalho para o repositório. |
| `revert` | `rev` | Restaura o arquivo de cópia de trabalho para seu estado original e desfaz a maioria das edições locais. |
| `resolved` | `res` | Remove o estado conflitante em arquivos ou diretórios de cópia de trabalho. |
| `propget` | `pg` | Imprime o valor de uma propriedade em arquivos ou diretórios. |
| `proplist` | `pl` | Imprime as propriedades em arquivos ou diretórios. |
| `propset` | `ps` | Define o valor de uma propriedade em arquivos ou diretórios. |
| `add` |  | Coloca arquivos e diretórios sob controle de versão. |
| `delete` | `del` ou `rm` | Remove arquivos e diretórios do controle de versão. |
| `diff` | `di` | Exibe as diferenças entre dois caminhos. |
| `console` |  | Executa um console interativo. |
| `rcp` |  | Copia uma árvore de nó de um repositório remoto para outro. |
| `sync` |  | Permite controlar o serviço de sincronização do cofre. |

### Exportar {#export}

Exporta o sistema de arquivos Vault montado em &lt;uri> para o sistema de arquivos local em &lt;local-path>. Um &lt;jcr-path> opcional pode ser especificado para exportar apenas uma subárvore.

#### Sintaxe {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Opções {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-t (--type) <arg>` | especifica o tipo de exportação, seja a plataforma ou o jar. |
| `-p (--prune-missing)` | especifica se os arquivos locais ausentes devem ser excluídos |
| `<uri>` | uri ponto de montagem |
| `<jcrPath>` | Caminho JCR |
| `<localPath>` | caminho local |

#### Exemplos {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### Importar {#import}

Importa o sistema de arquivos local (começando `<local-path>` no sistema de arquivos do cofre em `<uri>`. Você pode especificar uma raiz `<jcr-path>` como importação. Se `--sync` for especificado, os arquivos importados serão automaticamente colocados sob controle de cofre.

#### Sintaxe {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Opções {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-s (-- sync)` | coloca os arquivos locais sob controle de cofre |
| `<uri>` | uri ponto de montagem |
| `<jcrPath>` | Caminho JCR |
| `<localPath>` | caminho local |

#### Exemplos {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Check-out (co) {#checkout-co}

Realiza uma verificação inicial de um repositório JCR para o sistema de arquivos local, iniciando em &lt;uri> para o sistema de arquivos local em &lt;local-path>. Você também pode adicionar um argumento &lt;jcrPath> para fazer check-out de um subdiretório da árvore remota. É possível especificar filtros de espaço de trabalho que são copiados para o diretório META-INF.

#### Sintaxe {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Opções {#options-2}

|  |  |
|--- |--- |
| `--force` | força o check-out para substituir arquivos locais se eles já existirem |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `-f (--filter) <file>` | especifica os filtros automáticos se nenhum estiver definido |
| `<uri>` | uri ponto de montagem |
| `<jcrPath>` | (opcional) caminho remoto |
| `<localPath>` | (opcional) caminho local |

#### Exemplos {#examples-2}

Usando o JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

Com o espaço de trabalho padrão:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

Se o URI estiver incompleto, ele será expandido:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### Analisar {#analyze}

Analisa pacotes.

#### Sintaxe {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### Opções {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | formato printf para links de hotfix (nome, id), por exemplo `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `<localPaths> [<localPaths> ...]` | caminho local |

### Status {#status}

Imprime o status dos arquivos e diretórios da cópia de trabalho.

Se `--show-update` for especificado, cada arquivo será verificado em relação à versão remota. A segunda letra especifica então qual ação seria executada por uma operação de atualização.

#### Sintaxe {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Opções {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `-u (--show-update)` | exibe informações de atualização |
| `-N (--non-recursive)` | opera em um único diretório |
| `<file> [<file> ...]` | arquivo ou diretório para exibir o status |

### Atualizar {#update}

Copia as alterações do repositório para a cópia em funcionamento.

#### Sintaxe {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opções {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `--force` | força a substituição de arquivos locais |
| `-N (--non-recursive)` | opera em um único diretório |
| `<file> [<file> ...]` | arquivo ou diretório a ser atualizado |

### Informações {#info}

Exibe informações sobre um arquivo local.

#### Sintaxe {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### Opções {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | opera recursivamente |
| `<file> [<file> ...]` | arquivo ou diretório para exibir informações |

### Confirmar {#commit}

Envia alterações da sua cópia de trabalho para o repositório.

#### Sintaxe {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opções {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `--force` | força a confirmação mesmo se a cópia remota for modificada |
| `-N (--non-recursive)` | opera em um único diretório |
| `<file> [<file> ...]` | arquivo ou diretório a ser confirmado |

### Reverter {#revert}

Restaura o arquivo de cópia de trabalho para o estado original e desfaz a maioria das edições locais.

#### Sintaxe {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### Opções {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | descendente recursivamente |
| `<file> [<file> ...]` | arquivo ou diretório a ser confirmado |

### Resolvido {#resolved}

Remove o estado **conflitante** em arquivos ou diretórios de cópia de trabalho.

>[!NOTE]
>
>Esse comando não resolve conflitos semânticos nem remove marcadores de conflito; apenas remove os arquivos de artefato relacionados a conflitos e permite que o PATH seja confirmado novamente.

#### Sintaxe {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Opções {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | descendente recursivamente |
| `--force` | resolve, mesmo se houver marcadores de conflito |
| `<file> [<file> ...]` | arquivo ou diretório a ser resolvido |

### Propget {#propget}

Imprime o valor de uma propriedade em arquivos ou diretórios.

#### Sintaxe {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### Opções {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | descendente recursivamente |
| `<propname>` | o nome da propriedade |
| `<file> [<file> ...]` | arquivo ou diretório do qual obter a propriedade |

### Proplist {#proplist}

Imprime as propriedades em arquivos ou diretórios.

#### Sintaxe {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### Opções {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | descendente recursivamente |
| `<file> [<file> ...]` | arquivo ou diretório do qual listar as propriedades |

### Propset {#propset}

Define o valor de uma propriedade em arquivos ou diretórios.

>[!NOTE]
>
>O VLT reconhece as seguintes propriedades de versão especiais:
>
>`vlt:mime-type`
>
>O tipo de mimetype do arquivo. Usado para determinar se o arquivo deve ser unido. Um mimetype que começa com &#39;text/&#39; (ou um mimetype ausente) é tratado como texto. Qualquer outra coisa é tratada como binária.

#### Sintaxe {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Opções {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime o mínimo possível |
| `-R (--recursive)` | descendente recursivamente |
| `<propname>` | o nome da propriedade |
| `<propval>` | o valor da propriedade |
| `<file> [<file> ...]` | arquivo ou diretório para definir a propriedade como |

### Adicionar {#add}

Coloca arquivos e diretórios sob controle de versão, agendando-os para adição ao repositório. Eles serão adicionados na próxima confirmação.

#### Sintaxe {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Opções {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `-N (--non-recursive)` | opera em um único diretório |
| `--force` | força a operação a ser executada |
| `<file> [<file> ...]` | arquivo ou diretório local a ser adicionado |

### Exclua {#delete}

Remove arquivos e diretórios do controle de versão.

#### Sintaxe {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Opções {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada |
| `-q (--quiet)` | imprime o mínimo possível |
| `--force` | força a operação a ser executada |
| `<file> [<file> ...]` | arquivo ou diretório local a ser excluído |

### Diff {#diff}

Exibe as diferenças entre dois caminhos.

#### Sintaxe {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Opções {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | opera em um único diretório |
| `<file> [<file> ...]` | arquivo ou diretório do qual exibir as diferenças |

### Console {#console}

Executa um console interativo.

#### Sintaxe {#syntax-16}

```shell
console -F <file>
```

#### Opções {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | especifica o arquivo de configurações do console. O arquivo padrão é console.properties. |

### Rcp {#rcp}

Copia uma árvore de nó de um repositório remoto para outro. `<src>` aponta para o nó de origem e `<dst>` especifica o caminho de destino, onde o nó pai deve existir. O Rcp processa os nós fazendo o streaming dos dados.

#### Sintaxe {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### Opções {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime o mínimo possível. |
| `-r (--recursive)` | Descende recursivamente. |
| `-b (--batchSize) <size>` | Número de nós a serem processados antes de uma gravação intermediária. |
| `-t (--throttle) <seconds>` | Número de segundos para aguardar após uma gravação intermediária. |
| `-u (--update)` | Substituir/excluir nós existentes. |
| `-n (--newer)` | Respeite as propriedades lastModified para atualização. |
| `-e (--exclude) <arg> [<arg> ...]` | Regexp de caminhos de origem excluídos. |
| `<src>` | O endereço do repositório da árvore de origem. |
| `<dst>` | O endereço do repositório do nó de destino. |

#### Exemplos {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>As `--exclude` opções precisam ser seguidas por outra opção antes dos `<src>` argumentos e `<dst>` . Por exemplo:
>
>`vlt rcp -e ".*\.txt" -r`

### Sincronizar {#sync}

Permite controlar o serviço de sincronização do cofre. Sem nenhum argumento, esse comando tenta colocar o diretório de trabalho atual sob controle sincronizado. Se executado em um check-out vlt, ele usará o respectivo filtro e host para configurar a sincronização. Se executado fora de um check-out vlt, ele registra a pasta atual para sincronização somente se o diretório estiver vazio.

#### Sintaxe {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Opções {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | saída detalhada. |
| `--force` | forçar a execução de determinados comandos. |
| `-u (--uri) <uri>` | especifica o URI do host de sincronização. |
| `<command>` | comando sync para executar. |
| `<localPath>` | pasta local a ser sincronizada. |

### Códigos de status {#status-codes}

Os códigos de status usados pelo VLT são:

* &#39; &#39; sem modificações
* &#39;A&#39; adicionado
* &#39;C&#39; em Conflito
* &#39;D&#39; Excluído
* &#39;I&#39; Ignorado
* &#39;M&#39; Modificado
* &#39;R&#39; substituído
* &#39;?&#39; item não está sob controle de versão
* &#39;!&#39; item ausente (removido pelo comando non-svn) ou incompleto
* Item com versão &#39;~&#39; obstruído por algum item de um tipo diferente

## Configurando a sincronização do FileVault {#setting-up-filevault-sync}

O serviço de sincronização de cofre é usado para sincronizar o conteúdo do repositório com uma representação local do sistema de arquivos e vice-versa. Isso é feito instalando um serviço OSGi que acompanhará as alterações no repositório e verificará o conteúdo do sistema de arquivos periodicamente. Ele usa o mesmo formato de serialização que o cofre para mapear o conteúdo do repositório para o disco.

>[!NOTE]
>
>O serviço de sincronização de cofres é uma ferramenta de desenvolvimento e é altamente desencorajador usá-lo em um sistema produtivo. Observe também que o serviço só pode sincronizar com o sistema de arquivos local e não pode ser usado para desenvolvimento remoto.

### Instalação do serviço usando vlt {#installing-the-service-using-vlt}

O `vlt sync install` comando pode ser usado para instalar automaticamente o pacote de serviços de sincronização de cofre e a configuração.

O conjunto é instalado abaixo `/libs/crx/vault/install` e o nó de configuração é criado em `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. Inicialmente, o serviço é ativado, mas nenhuma raiz de sincronização é configurada.

O exemplo a seguir instala o serviço de sincronização para a instância CRX acessível pelo uri especificado.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### Exibir o status do serviço {#displaying-the-service-status}

O `status` comando pode ser usado para exibir informações sobre o serviço de sincronização em execução. &quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>O `status` comando não busca dados ao vivo do serviço, mas lê a configuração em `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### Adicionar uma pasta de sincronização {#adding-a-sync-folder}

O `register` comando é usado para adicionar uma pasta para sincronizar com a configuração.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>O `register` comando não aciona uma sincronização até que você configure a `sync-once` configuração.

### Removendo uma pasta de sincronização {#removing-a-sync-folder}

O `unregister` comando é usado para remover uma pasta para sincronizar da configuração.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>É necessário cancelar o registro de uma pasta de sincronização antes de excluí-la.

### Configuração da sincronização {#configuring-synchronization}

#### Service configuration {#service-configuration}

Quando o serviço estiver em execução, ele poderá ser configurado com os seguintes parâmetros:

* `vault.sync.syncroots`: Um ou vários caminhos de sistema de arquivos locais que definem as raízes de sincronização.

* `vault.sync.fscheckinterval`: Frequência (em segundos) da qual o sistema de arquivos deve ser examinado para detectar possíveis alterações. O padrão é 5 segundos.
* `vault.sync.enabled`: Sinalizador geral que ativa/desativa o serviço.

>[!NOTE]
>
>O serviço pode ser configurado com o console da Web ou com um `sling:OsgiConfig` nó (com o nome `com.day.jcr.sync.impl.VaultSyncServiceImpl`) no repositório.
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details.

#### Sincronizar configuração de pasta {#sync-folder-configuration}

Cada pasta de sincronização armazena a configuração e o status em três arquivos:

* `.vlt-sync-config.properties`: arquivo de configuração.

* `.vlt-sync.log`: arquivo de log que contém informações sobre as operações executadas durante a sincronização.
* `.vlt-sync-filter.xml`: filtros que definem quais partes do repositório são sincronizadas. O formato desse arquivo é descrito pela seção [Executando uma finalização](#performing-a-filtered-checkout) filtrada.

O `.vlt-sync-config.properties` arquivo permite configurar as seguintes propriedades:

**desativada** Ativa ou desativa a sincronização. Por padrão, esse parâmetro é definido como falso para permitir a sincronização.

**sync-once** Se não estiver vazio, a próxima verificação sincronizará a pasta na direção especificada, então o parâmetro será apagado. Dois valores são suportados:

* `JCR2FS`: exporta todo o conteúdo no repositório JCR e grava no disco local.
* `FS2JCR`: importa todo o conteúdo do disco para o repositório JCR.

**sync-log** Define o nome do arquivo de log. Por padrão, o valor é .vlt-sync.log

### Uso da sincronização VLT para desenvolvimento {#using-vlt-sync-for-development}

Para configurar um ambiente de desenvolvimento com base em uma pasta de sincronização, faça o seguinte:

1. Faça check-out do seu repositório com a linha de comando vlt:

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >Você pode usar filtros para verificar apenas os caminhos apropriados. Consulte a seção [Executando uma finalização](#performing-a-filtered-checkout) filtrada para obter informações.

1. Vá para a pasta raiz da sua cópia de trabalho:

   ```shell
   $ cd dev/jcr_root/
   ```

1. Instale o serviço de sincronização no repositório:

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. Inicialize o serviço de sincronização:

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. Edite o arquivo `.vlt-sync-config.properties` oculto e configure a sincronização para sincronizar o conteúdo do repositório:

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >Esta etapa baixa o repositório inteiro de acordo com a configuração do filtro.

1. Verifique o arquivo de log `.vlt-sync.log` para ver o andamento:

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

Sua pasta local agora é sincronizada com o repositório. A sincronização é bidirecional, portanto, a modificação do repositório será aplicada à sua pasta de sincronização local e vice-versa.

>[!NOTE]
>
>O recurso Sincronização VLT só oferece suporte a arquivos e pastas simples, mas detecta arquivos serializados de cofre especiais (.content.xml, dialog.xml etc.) e os ignora silenciosamente. Assim, é possível usar a sincronização de cofre em um check-out vlt padrão.
