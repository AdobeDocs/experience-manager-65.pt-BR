---
title: Uso da Ferramenta de Migração CRX2Oak
description: Saiba como usar a ferramenta de migração CRX2Oak com o Adobe Experience Manager. A ferramenta foi projetada para ajudar a migrar dados entre repositórios diferentes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Uso da Ferramenta de Migração CRX2Oak{#using-the-crx-oak-migration-tool}

## Introdução {#introduction}

O CRX2Oak é uma ferramenta projetada para migrar dados entre repositórios diferentes.

Ele pode ser usado para migrar dados de versões mais antigas do CQ com base no Apache Jackrabbit 2 para o Oak e também pode ser usado para copiar dados entre repositórios do Oak.

Você pode baixar a versão mais recente do crx2oak do repositório Adobe público neste local:
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>Para obter mais informações sobre o Apache Oak e os principais conceitos da persistência do Adobe Experience Manager (AEM), consulte [Introdução à plataforma do AEM](/help/sites-deploying/platform.md).

## Casos de uso de migração {#migration-use-cases}

A ferramenta pode ser usada para:

* Migração de versões anteriores do CQ 5 para o AEM 6
* Cópia de dados entre vários repositórios Oak
* Conversão de dados entre diferentes implementações do Oak MicroKernel.

O suporte para migrar repositórios usando Armazenamentos de blob externos (comumente conhecidos como Armazenamentos de dados) é fornecido em combinações diferentes. Um possível caminho de migração é de um repositório CRX2 que está usando um `FileDataStore` externo para um repositório Oak usando um `S3DataStore`.

O diagrama abaixo ilustra todas as combinações de migração possíveis compatíveis com o CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Recursos {#features}

O CRX2Oak é chamado durante atualizações do AEM de uma maneira em que o usuário pode especificar um perfil de migração predefinido que automatiza a reconfiguração dos modos de persistência. Isso é chamado de modo de início rápido.

Ela também pode ser executada separadamente caso exija mais personalização. No entanto, nesse modo, as alterações são feitas somente no repositório e qualquer reconfiguração adicional do AEM deve ser executada manualmente. Isso é chamado de modo independente.

Outra coisa a ser observada é que, com as configurações padrão no modo independente, somente o Armazenamento de nós é migrado e o novo repositório reutiliza o armazenamento binário antigo.

### Modo de início rápido automatizado {#automated-quickstart-mode}

Desde o AEM 6.3, o CRX2Oak é capaz de lidar com perfis de migração definidos pelo usuário que podem ser configurados com todas as opções de migração já disponíveis. Isso permite maior flexibilidade e a capacidade de automatizar a configuração de AEM, recursos que não estarão disponíveis se você estiver usando a ferramenta no modo independente.

Para alternar o CRX2Oak para o modo de início rápido, defina o caminho para a pasta crx-quickstart no diretório de instalação do AEM por meio dessa variável de ambiente do sistema operacional:

**Para sistemas baseados em UNIX e macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Para Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Retomar suporte {#resume-support}

A migração pode ser interrompida a qualquer momento, com a possibilidade de retomá-la posteriormente.

#### Lógica de atualização personalizável {#customizable-upgrade-logic}

A lógica Java™ personalizada pode ser implementada usando `CommitHooks`. As classes `RepositoryInitializer` personalizadas podem ser implementadas para inicializar o repositório com valores personalizados.

#### Suporte para operações com mapeamento de memória {#support-for-memory-mapped-operations}

O CRX2Oak também oferece suporte a operações com mapeamento de memória por padrão. O mapeamento de memória melhora muito o desempenho e deve ser usado sempre que possível.

>[!CAUTION]
>
>No entanto, observe que as operações com mapeamento de memória não são suportadas para plataformas Windows. Portanto, é recomendável adicionar o parâmetro **—disable-mmap** ao executar a migração no Windows.

#### Migração seletiva de conteúdo {#selective-migration-of-content}

Por padrão, a ferramenta migra todo o repositório no caminho `"/"`. No entanto, você tem controle total sobre qual conteúdo deve ser migrado.

Se houver alguma parte do conteúdo que não seja necessária na nova instância, você poderá usar o parâmetro `--exclude-path` para excluir o conteúdo e otimizar o procedimento de atualização.

#### Mesclagem de caminho {#path-merging}

Se os dados tiverem de ser copiados entre dois repositórios e você tiver um caminho de conteúdo diferente em ambas as instâncias, poderá defini-lo no parâmetro `--merge-path`. Ao fazer isso, o CRX2Oak copia somente os novos nós para o repositório de destino e mantém os antigos no lugar.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Suporte à versão {#version-support}

Por padrão, o AEM cria uma versão de cada nó ou página modificada e a armazena no repositório. As versões podem ser usadas para restaurar a página para um estado anterior.

No entanto, essas versões nunca são removidas mesmo se a página original for excluída. Ao lidar com repositórios que estão em operação há muito tempo, a migração pode reprocessar dados redundantes causados por versões órfãs.

Um recurso útil para esses tipos de situações é a adição do parâmetro `--copy-versions`. Ele pode ser usado para ignorar os nós da versão durante a migração ou cópia de um repositório.

Você também pode escolher se deseja copiar versões órfãs adicionando `--copy-orphaned-versions=true`.

Ambos os parâmetros também suportam um formato de data `YYYY-MM-DD`, caso você queira copiar versões até uma data específica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Abrir versão do Source {#open-source-version}

Uma versão de código aberto do CRX2Oak está disponível na forma de oak-upgrade. É compatível com todos os recursos, exceto:

* Suporte para CRX2
* Suporte ao perfil de migração
* Suporte para reconfiguração automatizada do AEM

Consulte a [Documentação do Apache](https://jackrabbit.apache.org/oak/docs/migration.html) para obter mais informações.

## Parâmetros {#parameters}

### Opções de armazenamento de nós {#node-store-options}

* `--cache`: Tamanho do cache em MB (o padrão é `256`)

* `--mmap`: Habilitar acesso a arquivo mapeado na memória para o Repositório de Segmentos
* `--src-password:` Senha para o banco de dados RDB de origem

* `--src-user:` Usuário para o RDB de origem

* `--user`: Usuário do RDB de destino

* `--password`: Senha para o RDB de destino.

### Opções de migração {#migration-options}

* `--early-shutdown`: desliga o repositório JCR2 de origem depois que os nós são copiados e antes que os ganchos de confirmação sejam aplicados
* `--fail-on-error`: força uma falha da migração se os nós não puderem ser lidos do repositório de origem.
* `--ldap`: migra usuários LDAP de uma instância do CQ 5.x para uma instância baseada no Oak. Para que isso funcione, o Provedor de identidade na configuração do Oak deve ser chamado de ldap. Para obter mais informações, consulte a [documentação sobre LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Use com o parâmetro `--ldap` para repositórios CQ 5.x que usaram vários servidores LDAP para autenticação. Você pode usá-lo para apontar para os arquivos de configuração `ldap_login.conf` ou `jaas.conf` do CQ 5.x. O formato é `--ldapconfig=path/to/ldap_login.conf`.

### Opções de armazenamento de versão {#version-store-options}

* `--copy-orphaned-versions`: ignora a cópia de versões órfãs. Parâmetros com suporte: `true`, `false` e `yyyy-mm-dd`. O padrão é `true`.

* `--copy-versions:` Copia o armazenamento da versão. Parâmetros: `true`, `false`, `yyyy-mm-dd`. O padrão é `true`.

#### Opções de caminho {#path-options}

* `--include-paths:` Lista separada por vírgulas de caminhos a serem incluídos durante a cópia
* `--merge-paths`: lista separada por vírgulas de caminhos a serem mesclados durante a cópia
* `--exclude-paths:` Lista separada por vírgulas de caminhos a serem excluídos durante a cópia.

### Opções da Source Blob Store {#source-blob-store-options}

* `--src-datastore:` O diretório de armazenamento de dados a ser usado como uma origem `FileDataStore`

* `--src-fileblobstore`: O diretório de armazenamento de dados a ser usado como uma origem `FileBlobStore`

* `--src-s3datastore`: O diretório de armazenamento de dados a ser usado para a origem `S3DataStore`

* `--src-s3config`: O arquivo de configuração para a origem `S3DataStore`.

### Opções do BlobStore de destino {#destination-blobstore-options}

* `--datastore:` O diretório de armazenamento de dados a ser usado como destino `FileDataStore`

* `--fileblobstore:` O diretório de armazenamento de dados a ser usado como destino `FileBlobStore`

* `--s3datastore`: O diretório de armazenamento de dados a ser usado para o destino `S3DataStore`

* `--s3config`: o arquivo de configuração para o destino `S3DataStore`.

### Opções de ajuda {#help-options}

* `-?, -h, --help:` Mostra informações de ajuda.

## Depuração {#debugging}

Você também pode ativar as informações de depuração do processo de migração para solucionar quaisquer problemas que possam ocorrer durante o processo. Você pode fazer isso de forma diferente dependendo do modo em que deseja executar a ferramenta:

<table>
 <tbody>
  <tr>
   <td><strong>Modo CRX2Oak</strong></td>
   <td><strong>Ação</strong></td>
  </tr>
  <tr>
   <td>Modo de início rápido</td>
   <td>Você pode adicionar as opções <strong>—log-level TRACE</strong> ou <strong>—log-level DEBUG </strong> à linha de comando ao executar o CRX2Oak. Neste modo, os logs são automaticamente redirecionados para o <strong>arquivo upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modo independente</td>
   <td><p>Adicione as opções <strong>—trace</strong> à linha de comando do CRX2Oak para que você possa mostrar eventos TRACE na saída padrão (você deve redirecionar os logs usando o caractere de redirecionamento: '&gt;' ou o comando 'tee' para inspeção posterior).</p> </td>
  </tr>
 </tbody>
</table>

## Outras considerações {#other-considerations}

Ao migrar para um conjunto de réplicas do MongoDB, defina o parâmetro `WriteConcern` como `2` em todas as conexões com os bancos de dados Mongo.

Você pode fazer isso adicionando o parâmetro `w=2` no final da cadeia de conexão, desta forma:

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Para obter mais informações, consulte a documentação da Cadeia de Conexão MongoDB em [Preocupações com Gravação](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
