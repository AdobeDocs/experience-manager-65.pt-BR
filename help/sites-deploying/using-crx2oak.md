---
title: Uso da ferramenta de migração CRX2Oak
seo-title: Uso da ferramenta de migração CRX2Oak
description: Saiba como usar a ferramenta de migração CRX2Oak.
seo-description: Saiba como usar a ferramenta de migração CRX2Oak.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---


# Uso da ferramenta de migração CRX2Oak{#using-the-crx-oak-migration-tool}

## Introdução {#introduction}

A CRX2Oak é uma ferramenta projetada para migrar dados entre repositórios diferentes.

Ele pode ser usado para migrar dados de versões mais antigas do CQ com base no Apache Jackrabbit 2 para o Oak, e também pode ser usado para copiar dados entre repositórios Oak.

Você pode baixar a versão mais recente do crx2oak do repositório do Adobe público neste local:
[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

A lista de alterações e correções para a versão mais recente pode ser encontrada nas [Notas de versão do CRX2Oak](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html).

>[!NOTE]
>
>Para obter mais informações sobre o Apache Oak e os principais conceitos de AEM persistência, consulte [Introdução à plataforma AEM](/help/sites-deploying/platform.md).

## Casos de uso da migração {#migration-use-cases}

A ferramenta pode ser usada para:

* Migração das versões mais antigas do CQ 5 para o AEM 6
* Copiando dados entre vários repositórios Oak
* Conversão de dados entre diferentes implementações do Oak MicroKernel.

O suporte para migrar repositórios usando armazenamentos de blobs externos (comumente conhecidos como armazenamentos de dados) é fornecido em combinações diferentes. Um caminho de migração possível é de um repositório CRX2 que está usando um `FileDataStore` externo para um repositório Oak usando um `S3DataStore`.

O diagrama abaixo ilustra todas as combinações de migração possíveis compatíveis com o CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Recursos {#features}

O CRX2Oak é chamado durante AEM atualizações de uma maneira em que o usuário pode especificar um perfil de migração predefinido que automatiza a reconfiguração dos modos de persistência. Isso é chamado de modo de início rápido.

Ele também pode ser executado separadamente, caso exija mais personalização. No entanto, observe que nesse modo, as alterações são feitas apenas no repositório e qualquer reconfiguração adicional de AEM precisa ser executada manualmente. Isso é chamado de modo independente.

Outra coisa a observar é que com as configurações padrão no modo independente, somente a Loja de nós será migrada e o novo repositório reutilizará o armazenamento binário antigo.

### Modo de Início Rápido Automatizado {#automated-quickstart-mode}

Desde o AEM 6.3, o CRX2Oak é capaz de lidar com perfis de migração definidos pelo usuário que podem ser configurados com todas as opções de migração já disponíveis. Isso permite maior flexibilidade e a capacidade de automatizar a configuração de AEM, recursos que não estão disponíveis se você estiver usando a ferramenta no modo independente.

Para alternar o CRX2Oak para o modo de início rápido, é necessário definir o caminho para a pasta crx-quickstart no diretório de instalação AEM por meio dessa variável ambiental do sistema operacional:

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

A lógica Java personalizada também pode ser implementada usando `CommitHooks`. As classes `RepositoryInitializer` personalizadas podem ser implementadas para inicializar o repositório com valores personalizados.

#### Suporte para operações de memória mapeada {#support-for-memory-mapped-operations}

O CRX2Oak também oferece suporte a operações mapeadas por memória por padrão. O mapeamento de memória melhora muito o desempenho e deve ser usado sempre que possível.

>[!CAUTION]
>
>Observe, no entanto, que as operações mapeadas de memória não são compatíveis com plataformas Windows. Portanto, é recomendável adicionar o parâmetro **—disable-mmap** ao executar a migração no Windows.

#### Migração seletiva de conteúdo {#selective-migration-of-content}

Por padrão, a ferramenta migra todo o repositório no caminho `"/"`. No entanto, você tem controle total sobre qual conteúdo deve ser migrado.

Se houver alguma parte do conteúdo que não seja necessária na nova instância, você poderá usar o parâmetro `--exclude-path` para excluir o conteúdo e otimizar o procedimento de atualização.

#### Mesclagem de caminho {#path-merging}

Se os dados precisarem ser copiados entre dois repositórios e você tiver um caminho de conteúdo diferente em ambas as instâncias, poderá defini-lo no parâmetro `--merge-path`. Depois disso, o CRX2Oak copiará apenas os novos nós no repositório de destino e manterá os antigos no lugar.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Suporte de versão {#version-support}

Por padrão, o AEM criará uma versão de cada nó ou página que é modificada e a armazenará no repositório. As versões podem ser usadas para restaurar a página para um estado anterior.

No entanto, essas versões nunca são limpas, mesmo se a página original for excluída. Ao lidar com repositórios que estão em operação por muito tempo, a migração pode precisar processar muitos dados redundantes causados por versões órfãs.

Um recurso útil para esses tipos de situações é a adição do parâmetro `--copy-versions` . Ele pode ser usado para ignorar os nós de versão durante a migração ou cópia de um repositório.

Você também pode escolher se deseja copiar versões órfãs adicionando `--copy-orphaned-versions=true`.

Ambos os parâmetros também suportam um formato de data `YYYY-MM-DD`, caso você queira copiar versões até uma data específica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Versão de origem aberta {#open-source-version}

Uma versão de código aberto do CRX2Oak está disponível no formato de atualização do oak. É compatível com todos os recursos, exceto:

* Suporte ao CRX2
* Suporte a perfil de migração
* Suporte para reconfiguração automatizada de AEM

Consulte a [Documentação do Apache](https://jackrabbit.apache.org/oak/docs/migration.html) para obter mais informações.

## Parâmetros {#parameters}

### Opções de armazenamento de nós {#node-store-options}

* `--cache`: Tamanho do cache em MB (o padrão é  `256`)

* `--mmap`: Ativar o acesso de arquivo mapeado de memória para a Loja de segmentos
* `--src-password:` Senha para o banco de dados RDB de origem

* `--src-user:` Usuário do RDB de origem

* `--user`: Usuário do RDB direcionado

* `--password`: Senha para o RDB de destino.

### Opções de migração {#migration-options}

* `--early-shutdown`: Encerra o repositório JCR2 de origem depois que os nós são copiados e antes que os ganchos de confirmação sejam aplicados
* `--fail-on-error`: Força uma falha da migração se os nós não puderem ser lidos do repositório de origem.
* `--ldap`: Migra usuários LDAP de uma instância CQ 5.x para uma baseada em Oak. Para que isso funcione, o Provedor de identidade na configuração do Oak precisa ser nomeado ldap. Para obter mais informações, consulte a [documentação LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Use isso junto com o  `--ldap` parâmetro para repositórios CQ 5.x que usaram vários servidores LDAP para autenticação. Você pode usá-lo para apontar para os arquivos de configuração CQ 5.x `ldap_login.conf` ou `jaas.conf`. O formato é `--ldapconfig=path/to/ldap_login.conf`.

### Opções de armazenamento de versão {#version-store-options}

* `--copy-orphaned-versions`: Ignora a cópia de versões órfãs. Os parâmetros compatíveis são: `true`, `false` e `yyyy-mm-dd`. O padrão é `true`.

* `--copy-versions:` Copia o armazenamento de versão. Parâmetros: `true`, `false`, `yyyy-mm-dd`. O padrão é `true`.

#### Opções de caminho {#path-options}

* `--include-paths:` Lista de caminhos separada por vírgulas a ser incluída durante a cópia
* `--merge-paths`: Lista de caminhos separada por vírgulas para mesclar durante a cópia
* `--exclude-paths:` Lista de caminhos separada por vírgulas a ser excluída durante a cópia.

### Opções de armazenamento de blobs de origem {#source-blob-store-options}

* `--src-datastore:` O diretório do armazenamento de dados a ser usado como uma origem  `FileDataStore`

* `--src-fileblobstore`: O diretório do armazenamento de dados a ser usado como uma origem  `FileBlobStore`

* `--src-s3datastore`: O diretório do armazenamento de dados a ser usado para a origem  `S3DataStore`

* `--src-s3config`: O arquivo de configuração da origem  `S3DataStore`.

### Opções do Target BlobStore {#destination-blobstore-options}

* `--datastore:` O diretório do armazenamento de dados a ser usado como destino  `FileDataStore`

* `--fileblobstore:` O diretório do armazenamento de dados a ser usado como destino  `FileBlobStore`

* `--s3datastore`: O diretório do armazenamento de dados a ser usado para o destino  `S3DataStore`

* `--s3config`: O arquivo de configuração do target  `S3DataStore`.

### Opções de Ajuda {#help-options}

* `-?, -h, --help:` Mostra informações de ajuda.

## Depuração {#debugging}

Você também pode ativar as informações de depuração do processo de migração para solucionar problemas que possam aparecer durante o processo. Você pode fazer isso de forma diferente dependendo do modo em que deseja executar a ferramenta:

<table>
 <tbody>
  <tr>
   <td><strong>Modo CRX2Oak</strong></td>
   <td><strong>Ação</strong></td>
  </tr>
  <tr>
   <td>Modo de início rápido</td>
   <td>Você pode adicionar as opções <strong>—log-level TRACE</strong> ou <strong>—log-level DEBUG </strong>à linha de comando ao executar o CRX2Oak. Neste modo, os logs são automaticamente redirecionados para o arquivo <strong>upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modo autônomo</td>
   <td><p>Adicione as opções <strong>—trace</strong> à linha de comando CRX2Oak para mostrar eventos TRACE na saída padrão (você precisa redirecionar os logs por conta própria usando o caractere de redirecionamento: '&gt;' ou 'tee' para inspeção posterior).</p> </td>
  </tr>
 </tbody>
</table>

## Outras considerações {#other-considerations}

Ao migrar para um conjunto de réplicas do MongoDB, certifique-se de definir o parâmetro `WriteConcern` para `2` em todas as conexões com os bancos de dados do Mongo.

Você pode fazer isso adicionando o parâmetro `w=2` no final da string de conexão, desta forma:

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Para obter mais informações, consulte a documentação da Cadeia de conexão do MongoDB em [Problemas de gravação](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).

