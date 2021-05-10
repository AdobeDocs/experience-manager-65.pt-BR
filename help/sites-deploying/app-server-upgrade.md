---
title: Etapas de atualização para instalações do servidor de aplicativos
seo-title: Etapas de atualização para instalações do servidor de aplicativos
description: Saiba como atualizar instâncias de AEM que são implantadas pelos Servidores de Aplicativos.
seo-description: Saiba como atualizar instâncias de AEM que são implantadas pelos Servidores de Aplicativos.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
feature: Atualização
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
translation-type: tm+mt
source-git-commit: d99f4ce072688f8e7d453199742618f0b2357d07
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Etapas de atualização para instalações do servidor de aplicativos{#upgrade-steps-for-application-server-installations}

Esta seção descreve o procedimento que precisa ser seguido para atualizar AEM para instalações do Servidor de Aplicativos.

Todos os exemplos neste procedimento usam o Tomcat como o Servidor de Aplicativos e implicam que você tem uma versão funcional do AEM já implantada. O procedimento destina-se a documentar atualizações realizadas de **AEM versão 6.4 para 6.5**.

1. Primeiro, comece o Tom Cat. Na maioria das situações, é possível fazer isso executando o script de inicialização `./catalina.sh` iniciando ao executar esse comando a partir do terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se o AEM 6.4 já estiver implantado, verifique se os pacotes estão funcionando corretamente acessando:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Em seguida, desimplante o AEM 6.4. Isso pode ser feito no Gerenciador de aplicativos do TomCat (`http://serveraddress:serverport/manager/html`)

1. Agora, migre o repositório usando a ferramenta de migração crx2oak. Para fazer isso, baixe a versão mais recente do crx2oak de [this location](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
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

   * A pasta **launchpad/startup**. Você pode excluí-lo executando o seguinte comando no terminal: `rm -rf crx-quickstart/launchpad/startup`

   * O arquivo **base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * O arquivo **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Remova **sling.options.file** executando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Agora, crie o armazenamento de nó e o armazenamento de dados que serão usados com o AEM 6.5. Você pode fazer isso criando dois arquivos com os seguintes nomes em `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Esses dois arquivos configurarão AEM para usar um armazenamento de nó TarMK e um armazenamento de dados File.

1. Edite os arquivos de configuração para prepará-los para uso. Mais especificamente:

   * Adicione a seguinte linha em `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * Em seguida, adicione as seguintes linhas a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. Agora é necessário alterar os modos de execução no arquivo war AEM 6.5. Para fazer isso, primeiro crie uma pasta temporária que estará hospedando a guerra AEM 6.5. O nome da pasta neste exemplo será `temp`. Depois que o arquivo war for copiado, extraia seu conteúdo executando de dentro da pasta temporária:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Depois que o conteúdo tiver sido extraído, vá para a pasta **WEB-INF** e edite o arquivo web.xml para alterar os modos de execução. Para localizar o local onde estão definidos no XML, procure pela string `sling.run.modes`. Depois de encontrá-lo, altere os modos de execução na próxima linha de código, que por padrão é definida como author:

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
