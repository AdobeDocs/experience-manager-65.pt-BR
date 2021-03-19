---
title: Execução de uma atualização no local
seo-title: Execução de uma atualização no local
description: Saiba como executar uma atualização no local.
seo-description: Saiba como executar uma atualização no local.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# Execução de uma atualização no local{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Esta página descreve o procedimento de atualização do AEM 6.5. Se você tiver uma instalação implantada em um servidor de aplicativos, consulte [Etapas de atualização para instalações do servidor de aplicativos](/help/sites-deploying/app-server-upgrade.md).

## Etapas de pré-atualização {#pre-upgrade-steps}

Antes de executar sua atualização, há várias etapas que devem ser concluídas. Consulte [Atualizando código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) e [Tarefas de manutenção de pré-atualização](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) para obter mais informações. Além disso, verifique se o sistema atende aos requisitos para a nova versão do AEM. Consulte como o Detector de padrões pode ajudar você a estimar a complexidade da atualização e também consulte a seção Escopo e requisitos de atualização de [Planejamento da atualização](/help/sites-deploying/upgrade-planning.md) para obter mais informações.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Pré-requisitos de migração {#migration-prerequisites}

* **Versão mínima necessária do Java:** a ferramenta de migração só funciona com o Java versões 7 e superior. Observe que para AEM 6.3 e superior, o JRE 8 do Oracle e o JRE 7 e 8 da IBM são as únicas versões compatíveis.

* **Instância atualizada:** se estiver atualizando de uma versão  **anterior à 5.6**, certifique-se de ter realizado uma atualização no local para o AEM 6.0 seguindo o procedimento descrito na versão 6.0 da documentação de Atualização.

## Preparação do arquivo jar AEM Quickstart {#prep-quickstart-file}

1. Pare a instância se ela estiver em execução.

1. Baixe o novo arquivo jar AEM e use-o para substituir o antigo fora da pasta `crx-quickstart`.

1. Descompacte o novo jar de início rápido executando:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migração do repositório de conteúdo {#content-repository-migration}

Essa migração não é necessária se você estiver atualizando do AEM 6.3. Para versões anteriores ao 6.3, o Adobe fornece uma ferramenta que pode ser usada para migrar o repositório para a nova versão do Oak Segment Tar presente no AEM 6.3. Ela é fornecida como parte do pacote de início rápido e é obrigatória para todas as atualizações que usarão o TarMK. As atualizações para ambientes que usam MongoMK não exigem migração de repositório. Para obter mais informações sobre quais são os benefícios do novo formato Tar de segmento, consulte as [Perguntas frequentes sobre a migração para o Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

A migração real é executada usando o arquivo jar AEM quickstart padrão, executado com uma nova opção `-x crx2oak` que executa a ferramenta crx2oak para simplificar a atualização e torná-la mais robusta.

>[!NOTE]
>
>Se você estiver executando a migração de conteúdo do repositório TarMK usando a extensão CRX2Oak Quickstart, poderá remover o **sampling content** runmode adicionando o seguinte à linha de comando de migração:
>
>* `--promote-runmode nosamplecontent`

>



Para determinar o comando que deve ser executado, use o seguinte comando:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Onde `<<YOUR_PROFILE>>` e `<<ADDITIONAL_FLAGS>>` são substituídas pelo perfil e pelos sinalizadores listados na tabela a seguir:

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

* Se você estiver executando a atualização em um sistema Windows onde o mapeamento da memória Java não é manipulado corretamente, adicione o parâmetro `--disable-mmap` ao comando.

* Se você estiver usando o Java 7, adicione o parâmetro `-XX:MaxPermSize=2048m` logo após o parâmetro `-Xmx`.

Para obter instruções adicionais sobre como usar a ferramenta crx2oak, consulte Uso da [Ferramenta de Migração CRX2Oak](/help/sites-deploying/using-crx2oak.md). O JAR auxiliar do crx2oak pode ser atualizado manualmente se necessário, substituindo-o manualmente por versões mais recentes após desempacotar o início rápido. Sua localização na pasta de instalação AEM é: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. A versão mais recente da ferramenta de migração CRX2Oak está disponível para download no Repositório de Adobe em: [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Se a migração tiver sido concluída com êxito, a ferramenta sairá com um código de saída zero. Além disso, verifique se há mensagens AVISO e ERRO no arquivo `upgrade.log`, localizado em `crx-quickstart/logs` no diretório de instalação do AEM, pois elas podem indicar erros não fatais que ocorreram durante a migração.

Verifique os arquivos de configuração abaixo da pasta `crx-quickstart/install`. Se for necessária uma migração, ela será atualizada para refletir o repositório de destino.

**Uma observação sobre os armazenamentos de dados:**

Embora `FileDataStore` seja o novo padrão para AEM instalações 6.3, não é necessário usar um armazenamento de dados externo. Embora o uso de um armazenamento de dados externo seja recomendado como prática recomendada para implantações de produção, não é um pré-requisito para atualizar. Devido à complexidade já presente no AEM de atualização, recomendamos executar a atualização sem fazer uma migração do armazenamento de dados. Se desejar, a migração do armazenamento de dados pode ser executada posteriormente como um esforço separado.

## Solução de problemas de migração {#troubleshooting-migration-issues}

Ignore esta seção se estiver atualizando a partir da versão 6.3. Embora os perfis do crx2oak fornecidos devam atender às necessidades da maioria dos clientes, há momentos em que parâmetros adicionais serão necessários. Se você encontrar um erro durante a migração, é possível que haja aspectos do seu ambiente que exijam a disponibilização de opções de configuração adicionais. Nesse caso, você provavelmente encontrará o seguinte erro:

**Os pontos de verificação não serão copiados porque nenhum armazenamento de dados externo foi especificado. Isso resultará na reindexação completa do repositório na primeira inicialização. Use —ignore pontos de verificação para forçar a migração ou consulte https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration para obter mais informações.**

Por algum motivo, o processo de migração precisa acessar binários no armazenamento de dados e não pode encontrá-los. Para especificar a configuração do armazenamento de dados, inclua os seguintes sinalizadores na parte `<<ADDITIONAL_FLAGS>>` do comando de migração:

**Para armazenamentos de dados S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Onde `/path/to/SharedS3DataStore.config` representa o caminho para o arquivo de configuração do armazenamento de dados S3 e `/path/to/datastore` representa o caminho para o armazenamento de dados S3.

**Para armazenamentos de dados de arquivo:**

```shell
--src-datastore=/path/to/datastore
```

Onde `/path/to/datastore` representa o caminho para o Armazenamento de dados do arquivo.

## Execução Da Atualização {#performing-the-upgrade}

**Se estiver usando S3:**

1. Remova todos os jars abaixo de `crx-quickstart/install` associados a uma versão anterior do conector S3.

1. Baixe a versão mais recente do conector S3 1.10.x de [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extraia o pacote para uma pasta temporária e copie o conteúdo de `jcr_root/libs/system/install` para a pasta `crx-quickstart/install`.

### Determinar o comando de início de atualização correto {#determining-the-correct-upgrade-start-command}

Para executar a atualização, é importante começar a AEM usando o arquivo jar para trazer a instância para frente. Para atualizar para a versão 6.5, consulte também outras opções de reestruturação e migração de conteúdo em [Migração de conteúdo ocioso](/help/sites-deploying/lazy-content-migration.md) que você pode escolher com o comando de atualização.

>[!IMPORTANT]
>
>Se você estiver executando o Oracle Java 11 (ou, em geral, versões do Java mais recentes do que 8), será necessário adicionar opções adicionais à linha de comando ao iniciar o AEM. Para obter mais informações, consulte [Considerações sobre o Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Observe que iniciar AEM a partir do script de início não iniciará a atualização. A maioria dos clientes começa a AEM usando o script de início e personalizou esse script para incluir switches para configurações do ambiente, como configurações de memória, certificados de segurança, etc. Por isso, recomendamos seguir este procedimento para determinar o comando de atualização correto:

1. Em uma instância de AEM em execução, execute o seguinte na linha de comando:

   ```shell
   ps -ef | grep java
   ```

1. Procure o processo de AEM. Será algo como:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifique o comando substituindo o caminho para o jar existente ( `crx-quickstart/app/aem-quickstart*.jar` neste caso) pelo novo jar que é um irmão da pasta `crx-quickstart`. Usando nosso comando anterior como exemplo, nosso comando seria:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Isso garantirá que todas as configurações de memória adequadas, modos de execução personalizados e outros parâmetros ambientais sejam aplicados para a atualização. Após a conclusão da atualização, a instância pode ser iniciada a partir do script de início em inicializações futuras.

## Implantar a base de código atualizada {#deploy-upgraded-codebase}

Depois que o processo de atualização no local for concluído, a base de código atualizada deverá ser implantada. As etapas para atualizar a base de código para funcionar na versão de destino do AEM podem ser encontradas na página [Atualizar Código e Personalizações](/help/sites-deploying/upgrading-code-and-customizations.md).

## Executar verificações e solução de problemas pós-atualização {#perform-post-upgrade-check-troubleshooting}

Consulte [Verificações de pós-atualização e solução de problemas](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
