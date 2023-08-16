---
title: Execução de uma atualização no local
description: Saiba como executar uma atualização no local.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# Execução de uma atualização no local{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página descreve o procedimento de atualização do AEM 6.5. Se você tiver uma instalação implantada em um servidor de aplicativos, consulte [Etapas de Atualização para Instalações de Servidor de Aplicativos](/help/sites-deploying/app-server-upgrade.md).

## Etapas de pré-atualização {#pre-upgrade-steps}

Antes de executar a atualização, há várias etapas que devem ser concluídas. Consulte [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) e [Tarefas de Manutenção de Pré-Atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obter mais informações. Além disso, verifique se o seu sistema atende aos requisitos da nova versão do AEM. Veja como o Detector de padrões pode ajudar você a estimar a complexidade da atualização e também veja a seção Escopo e requisitos de atualização do [Planejando sua atualização](/help/sites-deploying/upgrade-planning.md) para obter mais informações.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Pré-requisitos de migração {#migration-prerequisites}

* **Versão mínima necessária do Java:** A ferramenta de migração só funciona com o Java versões 7 e superiores. Observe que para AEM 6.3 e superior, o JRE 8 do Oracle e o JRE 7 e 8 da IBM são as únicas versões compatíveis.

* **Instância atualizada:** Se você estiver atualizando de uma versão **mais antigo que 5.6**, verifique se você executou uma atualização in-loco para o AEM 6.0 seguindo o procedimento descrito na versão 6.0 da documentação de Atualização.

## Preparação do arquivo jar AEM Quickstart {#prep-quickstart-file}

1. Pare a instância se ela estiver em execução.

1. Baixe o novo arquivo AEM jar e use-o para substituir o antigo fora do `crx-quickstart` pasta.

1. Descompacte o novo jar de início rápido executando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migração do repositório de conteúdo {#content-repository-migration}

Essa migração não é necessária se você estiver atualizando a partir do AEM 6.3. Para versões anteriores à 6.3, o Adobe fornece uma ferramenta que pode ser usada para migrar o repositório para a nova versão do Oak Segment Tar presente no AEM 6.3. Ele é fornecido como parte do pacote de início rápido e é obrigatório para todos os upgrades que usarão TarMK. As atualizações para ambientes que usam MongoMK não exigem migração de repositório. Para obter mais informações sobre quais são os benefícios do novo formato Tar de segmento, consulte a [Perguntas frequentes sobre a migração para o Oak Segment TAR](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

A migração real é realizada usando o arquivo jar padrão AEM quickstart, executado com um novo `-x crx2oak` opção que executa a ferramenta crx2oak para simplificar a atualização e torná-la mais robusta.

>[!NOTE]
>
>Se você estiver executando a migração de conteúdo do repositório TarMK usando a extensão Quickstart CRX2Oak, poderá remover a variável **samplecontent** runmode adicionando o seguinte à linha de comando de migração:
>
>* `--promote-runmode nosamplecontent`
>

Para determinar o comando que deve ser executado, use o seguinte comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Onde `<<YOUR_PROFILE>>` e `<<ADDITIONAL_FLAGS>>` são substituídos pelo perfil e pelos sinalizadores listados na tabela a seguir:

<table>
 <tbody>
  <tr>
   <td><strong>Repositório de origem</strong></td>
   <td><strong>Repositório de destino</strong></td>
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

* `mongo-port` é a porta do servidor MongoDB (por exemplo: 27017)

* `mongo-database-name` representa o nome do banco de dados (por exemplo: aem-author)

**Você também pode exigir switches adicionais para os seguintes cenários:**

* Se você estiver executando a atualização em um sistema Windows em que o mapeamento da memória Java não é manipulado corretamente, adicione o `--disable-mmap` para o comando.

Para obter instruções adicionais sobre o uso da ferramenta crx2oak, consulte Uso da [Ferramenta de migração CRX2Oak](/help/sites-deploying/using-crx2oak.md). O JAR auxiliar do crx2oak pode ser atualizado manualmente se necessário, substituindo-o manualmente por versões mais recentes depois de descompactar o quickstart. Seu local na pasta de instalação do AEM é: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. A versão mais recente da ferramenta de migração CRX2Oak está disponível para download no Repositório Adobe em: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Se a migração for concluída com êxito, a ferramenta será encerrada com um código de saída zero. Além disso, verifique se há mensagens de AVISO e ERRO no `upgrade.log` arquivo, localizado em `crx-quickstart/logs` no diretório de instalação do AEM, pois isso pode indicar erros não fatais que ocorreram durante a migração.

Verifique os arquivos de configuração abaixo de `crx-quickstart/install` pasta. Se uma migração for necessária, elas serão atualizadas para refletir o repositório de destino.

**Uma observação sobre armazenamentos de dados:**

Enquanto `FileDataStore` O é o novo padrão para instalações do AEM 6.3. Não é necessário usar um armazenamento de dados externo. Embora o uso de um armazenamento de dados externo seja recomendado como uma prática recomendada para implantações de produção, não é um pré-requisito para a atualização. Devido à complexidade já presente na atualização do AEM, a Adobe recomenda executar a atualização sem fazer uma migração do armazenamento de dados. Se desejar, uma migração de armazenamento de dados pode ser executada posteriormente como um esforço separado.

## Solução de problemas de migração {#troubleshooting-migration-issues}

Pule esta seção se estiver atualizando do 6.3. Embora os perfis do crx2oak fornecidos devam atender às necessidades da maioria dos clientes, há momentos em que parâmetros adicionais serão necessários. Se ocorrer um erro durante a migração, é possível que existam aspectos do ambiente que exigem a oferta de opções de configuração adicionais. Em caso afirmativo, você provavelmente encontrará o seguinte erro:

**Os pontos de verificação não serão copiados porque nenhum armazenamento de dados externo foi especificado. Isso resultará na reindexação completa do repositório na primeira inicialização. Use —skip-checkpoints para forçar a migração ou consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obter mais informações.**

Por algum motivo, o processo de migração precisa acessar binários no armazenamento de dados e não pode encontrá-los. Para especificar a configuração do armazenamento de dados, inclua os seguintes sinalizadores no `<<ADDITIONAL_FLAGS>>` parte do comando de migração:

**Para armazenamentos de dados S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Onde `/path/to/SharedS3DataStore.config` representa o caminho para o arquivo de configuração do armazenamento de dados S3 e `/path/to/datastore` representa o caminho para o armazenamento de dados S3.

**Para armazenamentos de dados de arquivos:**

```shell
--src-datastore=/path/to/datastore
```

Onde `/path/to/datastore` representa o caminho para o armazenamento de dados de arquivos.

## Execução Da Atualização {#performing-the-upgrade}

**Se estiver usando S3:**

1. Remova os jars abaixo de `crx-quickstart/install` associado a uma versão anterior do S3 connector.

1. Baixe a versão mais recente do conector S3 1.10.x do [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraia o pacote para uma pasta temporária e copie o conteúdo de `jcr_root/libs/system/install` para o `crx-quickstart/install` pasta.

### Determinando o comando de início de atualização correto {#determining-the-correct-upgrade-start-command}

Para executar a atualização, é importante iniciar o AEM usando o arquivo jar para ativar a instância. Para atualizar para a versão 6.5, consulte também outras opções de migração e reestruturação de conteúdo em [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md) que você pode escolher com o comando upgrade.

>[!IMPORTANT]
>
>Se você estiver executando o Oracle Java 11 (ou versões do Java mais recentes que 8), será necessário adicionar opções adicionais à linha de comando ao iniciar o AEM. Para obter mais informações, consulte [Considerações sobre o Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Observe que iniciar o AEM a partir do script de inicialização não iniciará a atualização. A maioria dos clientes inicia o AEM usando o script de inicialização e personaliza esse script de inicialização para incluir switches para configurações de ambiente, como configurações de memória, certificados de segurança etc. Por esse motivo, a Adobe recomenda seguir esse procedimento para determinar o comando de atualização adequado:

1. Em uma instância do AEM em execução, execute o seguinte a partir da linha de comando:

   ```shell
   ps -ef | grep java
   ```

1. Procure o processo de AEM. Será algo parecido com:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique o comando substituindo o caminho para o jar existente ( `crx-quickstart/app/aem-quickstart*.jar` neste caso) com o novo jar que é um irmão do `crx-quickstart` pasta. Usando nosso comando anterior como exemplo, nosso comando seria:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Isso garantirá que todas as configurações apropriadas de memória, modos de execução personalizados e outros parâmetros ambientais sejam aplicados para a atualização. Após a conclusão da atualização, a instância poderá ser iniciada a partir do script de inicialização em inicializações futuras.

## Implantar Base De Código Atualizada {#deploy-upgraded-codebase}

Depois que o processo de atualização no local for concluído, a base de código atualizada deverá ser implantada. As etapas para atualizar a base de código para funcionar na versão de destino do AEM podem ser encontradas em [Página Atualizar Código e Personalizações](/help/sites-deploying/upgrading-code-and-customizations.md).

## Executar Verificações Pós-Upgrade e Solução de Problemas {#perform-post-upgrade-check-troubleshooting}

Consulte [Verificações pós-atualização e solução de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
