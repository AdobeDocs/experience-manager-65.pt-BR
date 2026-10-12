---
title: Etapas de Atualização para Instalações de Servidor de Aplicativos
description: Saiba como atualizar instâncias do AEM implantadas por meio de servidores de aplicativos.
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%
---
# Etapas de Atualização para Instalações de Servidor de Aplicativos{#upgrade-steps-for-application-server-installations}

Esta seção descreve o procedimento que deve ser seguido para atualizar o AEM para instalações do Servidor de Aplicativos.

Todos os exemplos neste procedimento usam o Tomcat como o servidor da aplicação e implicam que você tem uma versão funcional do AEM já implantada. O procedimento destina-se a documentar atualizações executadas da **AEM versão 6.4 para a 6.5**.

1. Primeiro, inicie o TomCat. Na maioria das situações, você pode fazer isso executando o script de inicialização `./catalina.sh`, executando este comando no terminal:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se o AEM 6.4 já estiver implantado, verifique se os pacotes estão funcionando corretamente acessando:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Em seguida, desimplante o AEM 6.4. Isso pode ser feito no App Manager do TomCat (`http://serveraddress:serverport/manager/html`)

1. Agora, migre o repositório usando a ferramenta de migração crx2oak. Para fazer isso, baixe a versão mais recente do crx2oak de [este local](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. Exclua as propriedades necessárias no arquivo sling.properties fazendo o seguinte:

   1. Abrir o arquivo localizado em `crx-quickstart/launchpad/sling.properties`
   1. Texto da etapa Remova as seguintes propriedades e salve o arquivo:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Remova os arquivos e as pastas que não são mais necessários. Os itens que você precisa remover especificamente são:

   * A **pasta de inicialização/inicialização**. Você pode excluí-lo executando o seguinte comando no terminal: `rm -rf crx-quickstart/launchpad/startup`

   * O **arquivo base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * O **arquivo BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Remover **sling.options.file** executando: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Agora, crie o armazenamento de nós e o armazenamento de dados usados com o AEM 6.5. Você pode fazer isso criando dois arquivos com os seguintes nomes em `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Esses dois arquivos configurarão o AEM para usar um armazenamento de nó TarMK e um armazenamento de dados File.

1. Edite os arquivos de configuração para deixá-los prontos para uso. Mais especificamente:

   * Adicionar a seguinte linha a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

     `customBlobStore=true`

   * Em seguida, adicione as seguintes linhas a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. Agora é necessário alterar os modos de execução no arquivo WAR do AEM 6.5. Para fazer isso, primeiro crie uma pasta temporária que hospedará a guerra do AEM 6.5. O nome da pasta neste exemplo será `temp`. Depois que o arquivo WAR tiver sido copiado, extraia o conteúdo executando de dentro da pasta temporária:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Depois de extrair o conteúdo, vá para a pasta **WEB-INF** e edite o arquivo web.xml para alterar os modos de execução. Para localizar o local onde eles estão definidos no XML, procure a cadeia de caracteres `sling.run.modes`. Depois de encontrá-lo, altere os modos de execução na próxima linha do código, que por padrão é definida como autor:

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

1. Finalmente, implante o novo arquivo war no TomCat.
