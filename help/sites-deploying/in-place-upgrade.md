---
title: Execução de uma atualização no local
description: Saiba como executar uma atualização no local.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: c0574b50f3504a4792405d6fcd8aa3a2e8e6c686
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# Execução de uma atualização no local{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página descreve o procedimento de atualização do AEM 6.5. Se você tiver uma instalação implantada em um servidor de aplicativos, consulte [Etapas de atualização para instalações do servidor de aplicativos](/help/sites-deploying/app-server-upgrade.md).

## Etapas de pré-atualização {#pre-upgrade-steps}

Antes de executar sua atualização, há várias etapas que devem ser concluídas. Consulte [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) e [Tarefas de manutenção de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obter mais informações. Além disso, verifique se o sistema atende aos requisitos para a nova versão do AEM. Veja como o Detector de padrões pode ajudar você a estimar a complexidade de sua atualização e também consulte a seção Escopo e requisitos de atualização de [Planejamento da atualização](/help/sites-deploying/upgrade-planning.md) para obter mais informações.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Pré-requisitos de migração {#migration-prerequisites}

* **Versão mínima necessária do Java:** A ferramenta de migração só funciona com o Java versões 7 e superior. Observe que para AEM 6.3 e superior, o Oracle JRE 8 e o IBM JRE 7 e 8 são as únicas versões compatíveis.

* **Instância atualizada:** Se estiver atualizando de uma versão **mais de 5,6**, certifique-se de ter realizado uma atualização no local para o AEM 6.0 seguindo o procedimento descrito na versão 6.0 da documentação de Atualização.

## Preparação do arquivo jar AEM Quickstart {#prep-quickstart-file}

1. Pare a instância se ela estiver em execução.

1. Baixe o novo arquivo jar do AEM e use-o para substituir o antigo fora do `crx-quickstart` pasta.

1. Descompacte o novo jar de início rápido executando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migração do repositório de conteúdo {#content-repository-migration}

Essa migração não é necessária se você estiver atualizando do AEM 6.3. Para versões anteriores ao 6.3, o Adobe fornece uma ferramenta que pode ser usada para migrar o repositório para a nova versão do Oak Segment Tar presente no AEM 6.3. Ela é fornecida como parte do pacote de início rápido e é obrigatória para todas as atualizações que usarão o TarMK. As atualizações para ambientes que usam MongoMK não exigem migração de repositório. Para obter mais informações sobre quais são os benefícios do novo formato Tar de segmento, consulte o [Perguntas frequentes sobre a migração para o Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

A migração real é executada usando o arquivo jar AEM quickstart padrão, executado com um novo `-x crx2oak` opção que executa a ferramenta crx2oak para simplificar a atualização e torná-la mais robusta.

>[!NOTE]
>
>Se estiver executando a migração de conteúdo do repositório TarMK usando a extensão CRX2Oak Quickstart, você poderá remover a variável **conteúdo da amostra** execute o modo adicionando o seguinte à linha de comando de migração:
>
>* `--promote-runmode nosamplecontent`
>


Para determinar o comando que deve ser executado, use o seguinte comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Onde `<<YOUR_PROFILE>>` e `<<ADDITIONAL_FLAGS>>` são substituídos pelo perfil e sinalizadores listados na tabela a seguir:

<table>
 <tbody>
  <tr>
   <td><strong>Repositório de Origem</strong></td>
   <td><strong>Repositório do Target</strong></td>
   <td><strong>Perfil</strong></td>
   <td><strong>Sinalizadores adicionais</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 ou TarMK com <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Consulte a seção Solução de problemas abaixo</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK ou crx2 com <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>Consulte a seção Solução de problemas abaixo</td>
  </tr>
  <tr>
   <td>TarMK sem armazenamento de dados</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>Nenhuma migração é necessária</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Em que:**

* `mongo-host` é o IP do servidor MongoDB (por exemplo, 127.0.0.1)

* `mongo-port` é a porta do servidor MongoDB (por exemplo: (27017)

* `mongo-database-name` representa o nome do banco de dados (por exemplo: aem-author)

**Você também pode exigir opções adicionais para os seguintes cenários:**

* Se você estiver executando a atualização em um sistema Windows em que o mapeamento da memória Java não é manipulado corretamente, adicione o `--disable-mmap` para o comando.

Para obter instruções adicionais sobre como usar a ferramenta crx2oak, consulte Uso do [Ferramenta de migração CRX2Oak](/help/sites-deploying/using-crx2oak.md). O JAR auxiliar do crx2oak pode ser atualizado manualmente se necessário, substituindo-o manualmente por versões mais recentes após desempacotar o início rápido. Sua localização na pasta de instalação AEM é: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. A versão mais recente da ferramenta de migração CRX2Oak está disponível para download no Repositório de Adobe em: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Se a migração tiver sido concluída com êxito, a ferramenta sairá com um código de saída zero. Além disso, verifique se há mensagens AVISO e ERRO na seção `upgrade.log` arquivo, localizado em `crx-quickstart/logs` no diretório de instalação AEM, pois isso poderia indicar erros não fatais que ocorreram durante a migração.

Verifique os arquivos de configuração abaixo `crx-quickstart/install` pasta. Se for necessária uma migração, ela será atualizada para refletir o repositório de destino.

**Uma observação sobre os armazenamentos de dados:**

Ao `FileDataStore` é o novo padrão para instalações do AEM 6.3, não é necessário usar um armazenamento de dados externo. Embora o uso de um armazenamento de dados externo seja recomendado como prática recomendada para implantações de produção, não é um pré-requisito para atualizar. Devido à complexidade já presente no AEM de atualização, recomendamos executar a atualização sem fazer uma migração do armazenamento de dados. Se desejar, a migração do armazenamento de dados pode ser executada posteriormente como um esforço separado.

## Solução de problemas de migração {#troubleshooting-migration-issues}

Ignore esta seção se estiver atualizando a partir da versão 6.3. Embora os perfis do crx2oak fornecidos devam atender às necessidades da maioria dos clientes, há momentos em que parâmetros adicionais serão necessários. Se você encontrar um erro durante a migração, é possível que haja aspectos do seu ambiente que exijam a disponibilização de opções de configuração adicionais. Nesse caso, você provavelmente encontrará o seguinte erro:

**Os pontos de verificação não serão copiados porque nenhum armazenamento de dados externo foi especificado. Isso resultará na reindexação completa do repositório na primeira inicialização. Use —ignore os pontos de verificação para forçar a migração ou consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obter mais informações.**

Por algum motivo, o processo de migração precisa acessar binários no armazenamento de dados e não pode encontrá-los. Para especificar a configuração do armazenamento de dados, inclua os seguintes sinalizadores no `<<ADDITIONAL_FLAGS>>` parte do seu comando de migração:

**Para armazenamentos de dados S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Onde `/path/to/SharedS3DataStore.config` representa o caminho para o arquivo de configuração do armazenamento de dados S3 e `/path/to/datastore` representa o caminho para o armazenamento de dados S3.

**Para armazenamentos de dados de arquivo:**

```shell
--src-datastore=/path/to/datastore
```

Onde `/path/to/datastore` representa o caminho para seu armazenamento de dados de arquivo.

## Execução Da Atualização {#performing-the-upgrade}

**Se estiver usando S3:**

1. Remova todos os jars abaixo `crx-quickstart/install` associado a uma versão anterior do conector S3.

1. Baixe a versão mais recente do conector S3 1.10.x de [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraia o pacote para uma pasta temporária e copie o conteúdo de `jcr_root/libs/system/install` para `crx-quickstart/install` pasta.

### Determinar o comando correto de início da atualização {#determining-the-correct-upgrade-start-command}

Para executar a atualização, é importante começar a AEM usando o arquivo jar para trazer a instância para frente. Para atualizar para o 6.5, consulte também outras opções de reestruturação e migração de conteúdo em [Migração de conteúdo ocioso](/help/sites-deploying/lazy-content-migration.md) que você pode escolher com o comando atualizar.

>[!IMPORTANT]
>
>Se você estiver executando o Oracle Java 11 (ou, em geral, versões do Java mais recentes do que 8), será necessário adicionar opções adicionais à linha de comando ao iniciar o AEM. Para obter mais informações, consulte [Considerações sobre o Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Observe que iniciar AEM a partir do script de início não iniciará a atualização. A maioria dos clientes começa a AEM usando o script de início e personalizou esse script para incluir switches para configurações do ambiente, como configurações de memória, certificados de segurança, etc. Por isso, recomendamos seguir este procedimento para determinar o comando de atualização correto:

1. Em uma instância de AEM em execução, execute o seguinte na linha de comando:

   ```shell
   ps -ef | grep java
   ```

1. Procure o processo de AEM. Será algo parecido com:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique o comando substituindo o caminho para o jar existente ( `crx-quickstart/app/aem-quickstart*.jar` neste caso) com o novo jar que é um irmão da `crx-quickstart` pasta. Usando nosso comando anterior como exemplo, nosso comando seria:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Isso garantirá que todas as configurações de memória adequadas, modos de execução personalizados e outros parâmetros ambientais sejam aplicados para a atualização. Após a conclusão da atualização, a instância pode ser iniciada a partir do script de início em inicializações futuras.

## Implantar a base de código atualizada {#deploy-upgraded-codebase}

Depois que o processo de atualização no local for concluído, a base de código atualizada deverá ser implantada. As etapas para atualizar a base de código para funcionar na versão de destino do AEM podem ser encontradas em [Atualização da página Código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md).

## Executar verificações e solução de problemas pós-atualização {#perform-post-upgrade-check-troubleshooting}

Consulte [Verificação e solução de problemas da pós-atualização](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
