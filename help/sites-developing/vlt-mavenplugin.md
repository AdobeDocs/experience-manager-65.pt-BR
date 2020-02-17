---
title: Gerenciamento De Pacotes Usando O Maven
seo-title: Gerenciamento De Pacotes Usando O Maven
description: Use o plug-in Content Package Maven para integrar tarefas de gerenciamento de pacotes aos projetos do Maven
seo-description: Use o plug-in Content Package Maven para integrar tarefas de gerenciamento de pacotes aos projetos do Maven
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Gerenciamento De Pacotes Usando O Maven{#managing-packages-using-maven}

Use o plug-in Content Package Maven para integrar tarefas de gerenciamento de pacotes aos projetos do Maven. As metas e os parâmetros do plug-in permitem que você automatize muitas das tarefas que normalmente executaria usando a página Gerenciador de pacotes ou a linha de comando do FileVault:

* Crie novos pacotes a partir de arquivos no sistema de arquivos.
* Instale e desinstale pacotes no servidor CRX ou CQ.
* Crie pacotes que já estão definidos no servidor.
* Obtenha uma lista de pacotes instalados no servidor.
* Remova um pacote do servidor.

## Adicionar o plug-in Content Package Maven ao arquivo POM {#adding-the-content-package-maven-plugin-to-the-pom-file}

Para usar o plug-in Content Package Maven, adicione o seguinte elemento de plug-in dentro do elemento build do arquivo POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Para permitir que o Maven baixe o plug-in, use o perfil fornecido na seção [Obtenção do plug-in](#obtaining-the-content-package-maven-plugin) Content Package Maven nesta página.

## Metas do plug-in Content Package Maven {#goals-of-the-content-package-maven-plugin}

Os parâmetros de metas e metas fornecidos pelo plug-in Pacote de conteúdo são descritos nas seções a seguir. Os parâmetros descritos na seção Parâmetros comuns podem ser usados para a maioria das metas. Os parâmetros que se aplicam a uma meta são descritos na seção para essa meta.

**Prefixo do plug-in**

O prefixo do plug-in é content-package. Use esse prefixo para executar uma meta da linha de comando, como no exemplo a seguir:

```shell
mvn content-package:build
```

**Prefixo do parâmetro**

Salvo indicação em contrário, os parâmetros e metas do plug-in usam o prefixo de cofre, como no exemplo a seguir:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Proxies**

As metas que usam proxy para o servidor CRX ou CQ usam a primeira configuração válida de proxy encontrada nas configurações Maven. Se nenhuma configuração de proxy for encontrada, nenhum proxy será usado. Consulte o parâmetro useProxy na seção Configurações comuns.

### Parâmetros comuns {#common-parameters}

Os parâmetros na tabela a seguir são comuns a todas as metas, exceto quando anotados na coluna Metas.

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obrigatório</th>
   <th>Valor padrão</th>
   <th>Descrição</th>
   <th>Metas</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>boolean</td>
   <td>Não</td>
   <td>falso</td>
   <td>Um valor de <code>true</code> faz com que a compilação falhe quando ocorre um erro. Um valor de <code>false</code> faz com que a compilação ignore o erro.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>name</td>
   <td>Sequência de caracteres</td>
   <td>compilação: Sim<br /> instalar: Sem<br /> rm: Sim</td>
   <td>Criar: Sem padrão.<br /> instalar: O valor da propriedade artiactualId do projeto Maven.</td>
   <td>O nome do pacote em que agir.</td>
   <td>Todos os objetivos exceto ls.</td>
  </tr>
  <tr>
   <td>password</td>
   <td>Sequência de caracteres</td>
   <td>Sim</td>
   <td>admin</td>
   <td>A senha usada para autenticação com o servidor CRX.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td></td>
   <td>A ID do servidor da qual recuperar o nome de usuário e a senha para autenticação.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>Sequência de caracteres</td>
   <td>Sim</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>O URL da API de serviço HTTP do gerenciador de pacote CRX.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>Não</td>
   <td>5</td>
   <td>O tempo limite da conexão para comunicação com o serviço gerenciador de pacotes, em segundos.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>boolean</td>
   <td>Não</td>
   <td>verdadeiro</td>
   <td>Determina se as configurações de proxy devem ser usadas no arquivo de configurações Maven. Um valor de <code>true</code> faz com que o uso da primeira configuração de proxy ativa encontrada para solicitações de proxy para o gerenciador de pacotes. Um valor de false faz com que nenhum proxy seja usado.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>Sequência de caracteres</td>
   <td>Sim</td>
   <td>admin</td>
   <td>O nome de usuário para autenticação no servidor CRX.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
  <tr>
   <td>verboso</td>
   <td>boolean</td>
   <td>Não</td>
   <td>falso</td>
   <td>Ativa ou desativa o registro em log detalhado. Um valor de <code>true</code> permite o registro em log detalhado.</td>
   <td>Todos os objetivos exceto o pacote.</td>
  </tr>
 </tbody>
</table>

### build {#build}

Cria um pacote de conteúdo que já está definido em uma instância do AEM.

>[!NOTE]
>
>Este objetivo não precisa ser executado em um projeto Maven.

#### Parâmetros {#parameters}

Todos os parâmetros para a meta de compilação são descritos na seção Parâmetros [](#common-parameters) comuns.

#### Exemplo {#example}

O exemplo a seguir cria o pacote workflow-mbean instalado na instância do AEM com o endereço IP 10.36.79.223. A meta é executada usando o seguinte comando:

```shell
mvn content-package:build
```

O seguinte arquivo POM está localizado no diretório atual da ferramenta de linha de comando. O POM especifica o nome do pacote e o URL do serviço de pacote.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

Instala um pacote no repositório. A execução desta meta não requer um projeto Maven. A meta está vinculada à fase de instalação do ciclo de vida da construção Maven.

#### Parâmetros {#parameters-1}

Além dos parâmetros a seguir, consulte as descrições na seção Parâmetros [](#common-parameters) comuns.

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obrigatório</th>
   <th>Valor padrão</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>artefato</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td> O valor da propriedade artiactualId do projeto Maven.</td>
   <td>Uma string do form groupId:artifatoId:version[:package].</td>
  </tr>
  <tr>
   <td>artifatoId</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td></td>
   <td>A ID do artefato a ser instalado</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td></td>
   <td>A groupId do artefato a ser instalado</td>
  </tr>
  <tr>
   <td>install</td>
   <td>boolean</td>
   <td>Não</td>
   <td>verdadeiro</td>
   <td>Determina se o pacote deve ser desempacotado automaticamente quando for carregado. Um valor de true descompacta o pacote e false não descompacta o pacote.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artefato. repositório.<br /> ArtiactualRepository</td>
   <td>Não</td>
   <td>O valor da variável de sistema localRepository.</td>
   <td>O repositório Maven local. Não é possível configurar esse parâmetro usando a configuração do plug-in. A propriedade system é sempre usada.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>Não</td>
   <td>O artefato principal definido para o projeto Maven.</td>
   <td>O nome do arquivo de pacote a ser instalado.</td>
  </tr>
  <tr>
   <td>embalagem</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td>zip</td>
   <td>O tipo de empacotamento do artefato a ser instalado</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>Sim</td>
   <td>O valor da propriedade remoteAtiactualRepositories que é definida para o projeto Maven.</td>
   <td>Este valor não pode ser configurado usando a configuração do plug-in. O valor deve ser especificado no projeto. </td>
  </tr>
  <tr>
   <td>projeto</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sim</td>
   <td>O projeto para o qual o plug-in está configurado.</td>
   <td>O projeto Maven. O projeto está implícito porque contém a configuração do plug-in.</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>(linha de comando)</i></td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td>temp</td>
   <td>A ID do repositório a partir do qual o artefato é recuperado. Em um POM, use o repositórioID. Em uma linha de comando, use repoID.</td>
  </tr>
  <tr>
   <td>repositoryUrl <i>(POM)</i><br /> repoURL <i>(linha de comando)</i></td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td></td>
   <td>O URL do repositório do qual o artefato é recuperado. Em um POM, use o URL do repositório. Em uma linha de comando, use repoURL.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>Sequência de caracteres</td>
   <td>Não</td>
   <td></td>
   <td>A versão do artefato a ser instalada.</td>
  </tr>
 </tbody>
</table>

#### Exemplo {#example-1}

O exemplo a seguir cria um pacote que contém o pacote OSGi do fluxo de trabalho (consulte o exemplo para a meta de [compilação](#build) ) e instala o pacote. Como a meta de instalação está vinculada à fase de instalação do pacote, o seguinte comando executa a meta de instalação:

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

Lista os pacotes implantados no Gerenciador de pacotes.

#### Parâmetros {#parameters-2}

Todos os parâmetros da meta de ls estão descritos na seção Parâmetros [](#common-parameters) Comuns.

#### Exemplo {#example-2}

O exemplo a seguir lista os pacotes instalados na instância do AEM com o endereço IP 10.36.79.223. A meta é executada usando o seguinte comando:

```shell
mvn content-package:ls
```

O seguinte arquivo POM está localizado no diretório atual da ferramenta de linha de comando. O POM especifica o URL do serviço de pacote.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

Remove um pacote do Gerenciador de pacotes.

#### Parâmetros {#parameters-3}

Todos os parâmetros do objetivo rm são descritos na seção Parâmetros [](#common-parameters) Comuns.

#### Exemplo {#example-3}

O exemplo a seguir remove o pacote workfow-mbean instalado na instância do AEM com o endereço IP 10.36.79.223. A meta é executada usando o seguinte comando:

```shell
mvn content-package:rm
```

O seguinte arquivo POM está localizado no diretório atual da ferramenta de linha de comando. O POM especifica o URL do serviço de pacote e o nome do pacote.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

Desinstala um pacote. O pacote permanece no servidor no estado desinstalado.

#### Parâmetros {#parameters-4}

Todos os parâmetros da meta de desinstalação estão descritos na seção Parâmetros [](#common-parameters) comuns.

#### Exemplo {#example-4}

O exemplo a seguir desinstala o pacote workflow-mbean instalado na instância do AEM com o endereço IP 10.36.79.223. A meta é executada usando o seguinte comando:

```shell
mvn content-package:uninstall
```

O seguinte arquivo POM está localizado no diretório atual da ferramenta de linha de comando. O POM especifica o nome do pacote e o URL do serviço de pacote.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

Cria um pacote de conteúdo. A configuração padrão do objetivo do pacote inclui o conteúdo do diretório em que os arquivos compilados são salvos. A execução da meta do pacote requer que a fase de compilação tenha sido concluída. A meta do pacote está vinculada à fase do pacote do ciclo de vida da construção Maven.

#### Parâmetros {#parameters-5}

Além dos parâmetros a seguir, consulte a descrição do `name` parâmetro na seção Parâmetros [](#common-parameters) Comuns.

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obrigatório</th>
   <th>Valor padrão</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> arquiver.<br /> MavenArchiveConfiguration</td>
   <td>Não</td>
   <td></td>
   <td>A configuração do arquivo a ser usada. Consulte <a href="https://maven.apache.org/shared/maven-archiver/index.html">a documentação do Maven Archiver</a>.</td>
  </tr>
  <tr>
   <td>buildContentDirectory</td>
   <td>java.io.File</td>
   <td>Sim</td>
   <td>O valor do diretório de saída da compilação Maven.</td>
   <td>O diretório que contém o conteúdo a ser incluído no pacote.</td>
  </tr>
  <tr>
   <td>dependências</td>
   <td>java.util.List</td>
   <td>Não</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>Não</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>incorporados</td>
   <td>java.util.List</td>
   <td>Não</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>boolean</td>
   <td>Sim</td>
   <td>falso</td>
   <td>Um valor true faz com que a compilação falhe quando um artefato incorporado não é encontrado nas dependências do projeto. Um valor de false faz com que a compilação ignore o erro.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>Não</td>
   <td></td>
   <td>Um arquivo que especifica a origem do filtro da área de trabalho. Os filtros especificados na configuração e inseridos por meio de bordas ou subpacotes são unidos ao conteúdo do arquivo.</td>
  </tr>
  <tr>
   <td>filtros</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>Não</td>
   <td></td>
   <td>Contém elementos de filtro que definem o conteúdo do pacote. Quando executados, os filtros são incluídos no arquivo filter.xml. Consulte a seção Usando filtros abaixo.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>Sim</td>
   <td>O finalName definido no projeto Maven (fase de compilação).</td>
   <td>O nome do arquivo ZIP do pacote gerado, sem a extensão de arquivo .zip.</td>
  </tr>
  <tr>
   <td>grupo</td>
   <td>java.lang.String</td>
   <td>Sim</td>
   <td>A groupID definida no projeto Maven.</td>
   <td>A groupId do pacote de conteúdo gerado. Esse valor faz parte do caminho de instalação de destino do pacote de conteúdo.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>Sim</td>
   <td>O diretório build definido no projeto Maven.</td>
   <td>O diretório local onde o pacote de conteúdo é salvo.</td>
  </tr>
  <tr>
   <td>prefixo</td>
   <td>java.lang.String</td>
   <td>Não</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>projeto</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sim</td>
   <td></td>
   <td>O projeto Maven.</td>
  </tr>
  <tr>
   <td>propriedades</td>
   <td>java.util.Map</td>
   <td>Não</td>
   <td></td>
   <td>Propriedades adicionais que podem ser definidas no arquivo properties.xml. Essas propriedades não podem substituir as seguintes propriedades predefinidas:
    <ul>
     <li>grupo: Usar parâmetro de grupo para definir</li>
     <li>name: Usar parâmetro de nome para definir</li>
     <li>versão: Usar parâmetro de versão para definir</li>
     <li>descrição: Definir a partir da descrição do projeto</li>
     <li>groupId: groupId do descritor de projeto Maven</li>
     <li>artefatoId: artefatoId do descritor de projeto Maven</li>
     <li>dependências: Usar parâmetro de dependências para definir</li>
     <li>createdBy: O valor da propriedade do sistema user.name</li>
     <li>criado: A hora atual do sistema</li>
     <li>requirementsRoot: Usar parâmetro requirementsRoot para definir</li>
     <li>packagePath: Gerado automaticamente a partir do nome do grupo e do pacote</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requirementsRoot</td>
   <td>boolean</td>
   <td>Sim</td>
   <td>falso</td>
   <td>Define se o pacote requer raiz. Isso se tornará a propriedade &lt;code&gt;requirementsRoot&lt;/code&gt; do arquivo properties.xml.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>Não</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>Sim</td>
   <td>A versão definida no projeto Maven</td>
   <td>A versão do pacote de conteúdo.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>Sim</td>
   <td>O diretório definido no projeto Maven (fase de compilação).</td>
   <td>O diretório que contém o conteúdo a ser incluído no pacote.</td>
  </tr>
 </tbody>
</table>

#### Uso de filtros {#using-filters}

Use o elemento de filtros para definir o conteúdo do pacote. Os filtros são adicionados ao elemento workspaceFilter no `META-INF/vault/filter.xml` arquivo do pacote.

O exemplo de filtro a seguir mostra a estrutura XML a ser usada:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**Modo de importação**

O `mode` elemento define como o conteúdo é afetado pelo repositório quando o pacote é importado. Os seguintes valores podem ser usados:

* **** Mesclar: O conteúdo no pacote que ainda não está no repositório é adicionado. O conteúdo que está no pacote e no repositório não é alterado. Nenhum conteúdo é removido do repositório.
* **** Substituir: O conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo é removido do repositório quando não existe no pacote.
* **** Atualização: O conteúdo no pacote que não está no repositório é adicionado ao repositório. O conteúdo no repositório é substituído pelo conteúdo correspondente no pacote. O conteúdo existente é removido do repositório.

Quando o filtro não contém nenhum `mode` elemento, o valor padrão de `replace` é usado.

#### Exemplo {#example-5}

O exemplo a seguir cria um pacote que contém o pacote OSGi do fluxo de trabalho. O arquivo POM identifica o diretório jcr_root como o valor da propriedade buildContentDirectory. O diretório jcr_root contém o arquivo JAR do pacote na estrutura de diretório que espelha o repositório:

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

Como a meta está vinculada à fase de criação do pacote, o seguinte comando executa a meta do pacote:

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

Em vez de expressar a `package` meta na seção de plug-in `executions` , você pode usar `content-package` o valor do elemento do projeto `packaging` :

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### ajuda {#help}

#### Parâmetros {#parameters-6}

| Nome | Tipo | Obrigatório | Valor padrão | Descrição |
|---|---|---|---|---|
| detalhe | boolean | Não | falso | Determina se todas as propriedades que podem ser definidas para cada meta devem ser exibidas. Um valor de true exibe todas as propriedades que podem ser definidas. |
| meta | Sequência de caracteres | Não |  | O nome da meta para a qual mostrar ajuda. Se nenhum valor for especificado, a ajuda para todas as metas será exibida. |
| delayedSize | int | Não | 2 | O número de espaços a serem usados para o recuo de cada nível. Se você especificar um valor, ele deverá ser positivo. |
| lineLength | int | Não | 80 | O comprimento máximo de uma linha de exibição. Se você especificar um valor, ele deverá ser positivo. |

## Obtenção do plug-in Content Package Maven {#obtaining-the-content-package-maven-plugin}

O plug-in está disponível no repositório público da Adobe. Para baixar o plug-in, adicione o seguinte perfil Maven ao arquivo de configurações Maven e ative-o. Quando você usa um comando Maven, o plug-in é baixado no repositório local, se necessário.

>[!NOTE]
>
>O repositório do Adobe Public Releases não pode ser navegado, de modo que navegar até o URL do repositório usando o navegador da Web resulta em um erro Não encontrado. No entanto, a Maven pode acessar os diretórios do repositório.

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## Como incorporar pacotes OSGi em um pacote de conteúdo {#embedding-osgi-bundles-in-a-content-package}

Use o Plug-in Content Package Maven para incorporar pacotes OSGi ao pacote de conteúdo. Para incorporar o pacote, implemente as seguintes configurações:

* O pacote deve ser declarado como uma dependência do projeto Maven.
* A configuração do plug-in faz referência ao pacote usando o caminho desejado do pacote no pacote.

O exemplo de POM a seguir cria um pacote que contém o pacote Apache Sling JCR UserManager. No pacote, o JAR do pacote está localizado na `jcr_root/apps/myapp/install` pasta:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## Inclusão de uma imagem em miniatura ou de um arquivo de propriedades no pacote {#including-a-thumbnail-image-or-properties-file-in-the-package}

Substitua os arquivos de configuração do pacote padrão para personalizar as propriedades do pacote. Por exemplo, inclua uma imagem em miniatura para distinguir o pacote no Package Manager e no Package Share.

No pacote, os arquivos específicos do FileVault estão localizados na pasta /META-INF/vault. Os arquivos de origem podem ser localizados em qualquer lugar do sistema de arquivos. No arquivo POM, defina os recursos de compilação para copiar os arquivos de origem para o destino/vault-work/META-INF para inclusão no pacote.

O seguinte código POM adiciona os arquivos na pasta META-INF da fonte do projeto ao pacote:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

O código POM a seguir adiciona apenas uma imagem em miniatura ao pacote. A imagem em miniatura deve ser chamada thumbnail.png e deve estar localizada na pasta META-INF/vault/Definition do pacote. Neste exemplo, o arquivo de origem está localizado na pasta /src/main/content/META-INF/vault/Definition do projeto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Uso De Arquétipos Para Gerar Projetos AEM {#using-archetypes-to-generate-aem-projects}

Vários arquétipos Maven estão disponíveis para gerar projetos do AEM. Use o arquétipo que corresponde às suas metas de desenvolvimento:

* Um pacote de conteúdo que instala recursos para um aplicativo AEM: [simple-content-package-archetype](#simple-content-package-archetype)
* Um pacote de conteúdo que inclui artefatos de terceiros: pacote de conteúdo [simples com arquétipo](#simple-content-package-with-embedded-archetype)incorporado.
* Um aplicativo de vários módulos que acomoda o desenvolvimento de classes Java e testes de unidade: [multimodule-content-package-archetype](#multimodule-content-package-archetype).

>[!NOTE]
>
>O projeto Apache Sling também oferece arquétipos úteis no desenvolvimento do AEM. Eles estão documentados em [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

Cada arquétipo gera os seguintes itens:

* A estrutura da pasta do projeto.
* Arquivos POM.
* Arquivos de configuração do FileVault.

Os artefatos de arquétipo estão disponíveis no repositório do Adobe public Maven. Para baixar e executar um arquétipo, identifique o arquétipo e o repositório da Adobe usando os parâmetros do comando Maven archetype:generate:

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

O plug-in Maven archetype usa o modo interativo no shell ou no prompt de comando para coletar informações sobre seu projeto. As informações fornecidas são usadas para configurar várias propriedades do projeto, como nomes de pastas e IDs de artefato.

**Arquivos POM**

Os arquivos POM gerados incluem comandos para compilar código, criar pacotes e implantá-los no AEM em pacotes. As propriedades `groupID`, `artifactId`, `version`e `name` do projeto Maven são automaticamente preenchidas usando os valores fornecidos ao prompt `archetype:generate` interativo Maven.

Você pode alterar os seguintes valores padrão no arquivo pom.xml gerado:

* O nome do servidor CQ ou endereço IP: O valor padrão é `localhost`. O `crx.host` elemento abaixo `project/properties` contém esse valor.

* O número da porta do servidor CQ: O valor padrão é `4502`. O `crx.port` elemento abaixo `project/properties` contém esse valor.

* A versão do plug-in Content Package Maven: Use a versão mais recente como o conteúdo do `version` elemento para o plug-in com `artifactId` de `content-package-maven-plugin`. O valor padrão é `0.0.24`.

**Uso dos arquétipos**

1. Em uma janela de shell ou prompt de comando, digite o `archetype:generate` comando Maven. Quando solicitado, forneça valores para os parâmetros restantes.

   Para obter informações sobre cada parâmetro, consulte a seção referente ao arquétipo que você está usando.

1. Use um editor de texto para abrir o arquivo pom.xml e editar os valores padrão de acordo com seus requisitos.
1. Preencha as pastas geradas com recursos.
1. Digite o `mvn clean install` comando.

### simple-content-package-archetype {#simple-content-package-archetype}

Cria um projeto maven adequado para instalar recursos para um aplicativo AEM simples. A estrutura de pastas é usada abaixo da `/apps` pasta do repositório do AEM. O POM define comandos para empacotar os recursos que você coloca nas pastas e instalar os pacotes na instância do AEM.

**Propriedades de artefatos de arquétipo:**

* ID do grupo: `com.day.jcr.vault`
* ID do artefato: `simple-content-package-archetype`
* Versão: `1.0.2`
* Repositório: `adobe-public-releases`

**Comando Maven:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parâmetros de tipo de arquivamento:**

* groupId: A groupId do pacote de conteúdo gerado pelo Maven. O valor é usado automaticamente no arquivo POM.
* artefatoId: O nome do pacote de conteúdo. O valor também é usado como o nome da pasta do projeto.
* versão:A versão do pacote de conteúdo.
* pacote: Esse valor não é usado para um tipo de arquivamento de pacote simples.
* appsFolderName: O nome da pasta abaixo de /apps.
* artefatoName: A descrição do pacote de conteúdo.
* packageGroup: O nome do grupo de pacotes de conteúdo. Esse valor configura o parâmetro group para a meta Package do Content Package Maven Plugin.

**Estrutura da pasta:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-Integrated-archetype {#simple-content-package-with-embedded-archetype}

Executa as mesmas tarefas que o simples content-package-archetype e também baixa e inclui um artefato de um repositório Maven público.

**Propriedades do pacote de arquétipos:**

* ID do grupo: `com.day.jcr.vault`
* ID do artefato: `simple-content-package-with-embedded-archetype`
* Versão: `1.0.2`
* Repositório: `adobe-public-releases`

**Comando Maven:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parâmetros de tipo de arquivamento:**

* groupId: A groupId do pacote de conteúdo gerado pelo Maven. O valor é usado automaticamente no arquivo POM.
* artefatoId: O nome do pacote de conteúdo. O valor também é usado como o nome da pasta do projeto.
* versão:A versão do pacote de conteúdo.
* pacote: Este parâmetro não é usado.
* appsFolderName: O nome da pasta abaixo de /apps.
* artefatoName: A descrição do pacote de conteúdo.
* embeddedArtiactualId: A ID do artefato a ser incorporado no pacote de conteúdo.
* embeddedGroupId: A ID de grupo do artefato a ser incorporado.
* embeddedVersion: A versão do artefato a ser incorporada.
* packageGroup: O nome do grupo de pacotes de conteúdo. Esse valor configura o parâmetro group para a meta Package do Content Package Maven Plugin.

**Estrutura da pasta:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-archetype {#multimodule-content-package-archetype}

Cria um projeto maven que inclui a estrutura de pastas para desenvolver um aplicativo AEM e instalar recursos no servidor.

A `bundle` pasta contém a estrutura de pastas que armazena os arquivos de origem Java e JUnit que você desenvolve. O arquivo pom.xml nesta pasta cria o pacote OSGi. Os seguintes valores no POM identificam o artefato e o pacote:

* artefatoID: `${artifactID}-bundle`.
* Bundle-SymbaticName: `${groupId}.${artifactId}-bundle`.

`${artifactID}` e `${groupId}` são os valores fornecidos para esses parâmetros ao executar os arquétipos.

A `content` pasta contém os recursos instalados na instância do AEM. O valor de artiactualID é `${artifactID}multimodule-bundle`.

A pasta pai contém o POM pai que gerencia plug-ins e dependências Maven.

**Propriedades do pacote de arquétipos:**

* ID do grupo: `com.day.jcr.vault`
* ID do artefato: `multimodule-content-package-archetype`
* Versão: `1.0.2`
* Repositório: `adobe-public-releases`

**Comando Maven:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parâmetros de tipo de arquivamento:**

* groupId: A groupId do pacote de conteúdo gerado pelo Maven. O valor é usado automaticamente no arquivo POM.
* artefatoId: O nome do pacote de conteúdo. O valor também é usado como o nome da pasta do projeto.
* versão:A versão do pacote de conteúdo.
* pacote: Esse valor não é usado para multimodule-content-package-archetype.
* appsFolderName: O nome da pasta abaixo de /apps.
* artefatoName: A descrição do pacote de conteúdo.
* packageGroup: O nome do grupo de pacotes de conteúdo. Esse valor configura o parâmetro group para a meta Package do Content Package Maven Plugin.

**Estrutura da pasta:**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

