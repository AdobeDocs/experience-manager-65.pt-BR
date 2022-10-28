---
title: Etapas de atualização para instalações do servidor de aplicativos
description: Saiba como atualizar instâncias de AEM que são implantadas pelos Servidores de Aplicativos.
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: c0574b50f3504a4792405d6fcd8aa3a2e8e6c686
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Etapas de atualização para instalações do servidor de aplicativos{#upgrade-steps-for-application-server-installations}

Esta seção descreve o procedimento que precisa ser seguido para atualizar AEM para instalações do Servidor de Aplicativos.

Todos os exemplos neste procedimento usam o Tomcat como o Servidor de Aplicativos e implicam que você tem uma versão funcional do AEM já implantada. O procedimento destina-se a documentar as atualizações realizadas a partir de **AEM versão 6.4 a 6.5**.

1. Primeiro, comece o Tom Cat. Na maioria das situações, é possível fazer isso executando o `./catalina.sh` inicie o script de inicialização executando este comando a partir do terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se o AEM 6.4 já estiver implantado, verifique se os pacotes estão funcionando corretamente acessando:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Em seguida, desimplante o AEM 6.4. Isso pode ser feito no Gerenciador de aplicativos do Tom Cat (`http://serveraddress:serverport/manager/html`)

1. Agora, migre o repositório usando a ferramenta de migração crx2oak. Para fazer isso, baixe a versão mais recente do crx2oak de [esta localização](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. Exclua as propriedades necessárias no arquivo sling.properties fazendo o seguinte:

   1. Abra o arquivo localizado em `crx-quickstart/launchpad/sling.properties`
   1. Texto da etapa Remova as seguintes propriedades e salve o arquivo:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Remova os arquivos e pastas que não são mais necessários. Os itens que você precisa remover especificamente são:

   * O **pasta de inicialização/inicialização**. Você pode excluí-lo executando o seguinte comando no terminal: `rm -rf crx-quickstart/launchpad/startup`

   * O **arquivo base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * O **Arquivo BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Remover **sling.options.file** executando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Agora, crie o armazenamento de nó e o armazenamento de dados que serão usados com o AEM 6.5. Você pode fazer isso criando dois arquivos com os seguintes nomes em `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Esses dois arquivos configurarão AEM para usar um armazenamento de nó TarMK e um armazenamento de dados File.

1. Edite os arquivos de configuração para prepará-los para uso. Mais especificamente:

   * Adicione a seguinte linha em `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      `customBlobStore=true`

   * Em seguida, adicione as seguintes linhas a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. Agora é necessário alterar os modos de execução no arquivo war AEM 6.5. Para fazer isso, primeiro crie uma pasta temporária que estará hospedando a guerra AEM 6.5. O nome da pasta neste exemplo será `temp`. Depois que o arquivo war for copiado, extraia seu conteúdo executando de dentro da pasta temporária:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Depois que o conteúdo tiver sido extraído, vá para a variável **WEB-INF** e edite o arquivo web.xml para alterar os modos de execução. Para localizar o local em que estão definidos no XML, procure a variável `sling.run.modes` string. Depois de encontrá-lo, altere os modos de execução na próxima linha de código, que por padrão é definida como author:

   ```bash
   <param-value >author</param-value>
   ```

1. Altere o valor do autor acima e defina os modos de execução como: `author,crx3,crx3tar`. O bloco final do código deve ter esta aparência:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Recrie o jar com o conteúdo modificado:

   ```bash
   jar cvf aem65.war
   ```

1. Finalmente, implante o novo arquivo de guerra em TomCat.
