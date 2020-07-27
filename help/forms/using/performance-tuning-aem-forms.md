---
title: Ajuste de desempenho do servidor AEM Forms
seo-title: Ajuste de desempenho do servidor AEM Forms
description: Para que os AEM Forms tenham um desempenho otimizado, você pode ajustar as configurações de cache e os parâmetros JVM. Além disso, usar um servidor da Web pode melhorar o desempenho da implantação de AEM Forms.
seo-description: Para que os AEM Forms tenham um desempenho otimizado, você pode ajustar as configurações de cache e os parâmetros JVM. Além disso, usar um servidor da Web pode melhorar o desempenho da implantação de AEM Forms.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# Ajuste de desempenho do servidor AEM Forms{#performance-tuning-of-aem-forms-server}

Este artigo discute estratégias e práticas recomendadas que você pode implementar para reduzir gargalos e otimizar o desempenho da implantação de seus AEM Forms.

## Configurações de cache {#cache-settings}

Você pode configurar e controlar a estratégia de cache para AEM Forms usando o componente Configurações **de formulários** móveis no console de configuração da Web do AEM em:

* (AEM Forms no OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

As opções disponíveis para armazenamento em cache são as seguintes:

* **Nenhum**: Implica não armazenar em cache nenhum artefato. Isso, na prática, retarda o desempenho e exige alta disponibilidade de memória devido à ausência do cache.
* **Conservador**: Indica para armazenar em cache apenas os artefatos intermediários que são gerados antes da renderização do formulário, como um modelo que contém fragmentos em linha e imagens.
* **Agressivo**: Força a armazenar em cache quase tudo o que pode ser armazenado em cache, incluindo conteúdo HTML renderizado, além de todos os artefatos do nível de armazenamento em cache do Conservative. Ela resulta no melhor desempenho, mas também consome mais memória para armazenar artefatos em cache. Uma estratégia de cache agressiva significa que você obterá desempenho de tempo constante na renderização de um formulário quando o conteúdo renderizado for armazenado em cache.

As configurações de cache padrão para AEM Forms podem não ser boas o suficiente para alcançar o desempenho ideal. Portanto, é recomendável usar as seguintes configurações:

* **Estratégia** de cache: Agressivo
* **Tamanho** do cache (em termos de número de formulários): Conforme necessário
* **Tamanho** máximo do objeto: Conforme necessário

![Configurações de formulários móveis](assets/snap.png)

>[!NOTE]
>
>Se você usar o AEM Dispatcher para armazenar formulários adaptáveis em cache, ele também armazenará em cache formulários adaptáveis que contêm formulários com dados pré-carregados. Se esses formulários forem fornecidos pelo cache do AEM Dispatcher, isso pode levar ao fornecimento de dados pré-preenchidos ou obsoletos aos usuários. Portanto, use o AEM Dispatcher para armazenar em cache formulários adaptáveis que não usam dados pré-preenchidos. Além disso, um cache do dispatcher não invalidar automaticamente fragmentos em cache. Portanto, não o use para armazenar em cache fragmentos de formulário. Para esses formulários e fragmentos, use o cache [de formulários](../../forms/using/configure-adaptive-forms-cache.md)adaptáveis.

## Parâmetros JVM {#jvm-parameters}

Para obter o desempenho ideal, é recomendável usar os seguintes `init` argumentos JVM para configurar o `Java heap` e `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>As configurações recomendadas são para o JDK do Windows 2008 R2 8 Core e do Oracle HotSpot 1.7 (64 bits) e devem ser ampliadas para cima ou para baixo de acordo com a configuração do seu sistema.

## Uso de um servidor da Web {#using-a-web-server}

Formulários adaptáveis e formulários HTML5 são renderizados no formato HTML5. A saída resultante pode ser grande dependendo de fatores como o tamanho do formulário e as imagens no formulário. Para otimizar a transferência de dados, a abordagem recomendada é compactar a resposta HTML usando o servidor da Web do qual a solicitação está sendo atendida. Essa abordagem reduz o tamanho da resposta, o tráfego da rede e o tempo necessário para transmitir dados entre computadores de servidor e cliente.

Por exemplo, execute as seguintes etapas para ativar a compactação no Apache Web Server 2.0 de 32 bits com JBoss:

>[!NOTE]
>
>As instruções a seguir não se aplicam a nenhum servidor além do Apache Web Server 2.0 de 32 bits. Para obter as etapas específicas de qualquer outro servidor, consulte a documentação do produto correspondente.

As etapas a seguir demonstram as alterações necessárias para habilitar a compactação com o Apache Web Server

**Obtenha o software do servidor Web Apache aplicável ao seu sistema operacional**

* Windows: baixe o servidor Web Apache do site do Apache HTTP Server Project.
* Solaris de 64 bits: faça download do servidor Web Apache no site Sunfreeware para Solaris.
* Linux: o servidor Web Apache é pré-instalado em um sistema Linux.

O Apache pode se comunicar com o CRX usando o protocolo HTTP. As configurações são para otimização usando HTTP.

1. Exclua as barras de comentário das seguintes configurações de módulo no `APACHE_HOME/conf/httpd.conf` arquivo.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, o padrão `APACHE_HOME` é `/etc/httpd/`.

1. Configure o proxy na porta 4502 do crx.
Adicione a seguinte configuração no arquivo `APACHE_HOME/conf/httpd.conf` de configuração.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Ative a compactação. Adicione a seguinte configuração no arquivo `APACHE_HOME/conf/httpd.conf` de configuração.

   **Para formulários HTML5**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **Para formulários adaptáveis**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   Para acessar o servidor crx, use `https://'server':80`, onde `server` é o nome do servidor no qual o servidor Apache está sendo executado.

## Usando um antivírus no servidor que executa AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

Você pode experimentar um desempenho lento nos servidores que executam um software antivírus. Um software antivírus sempre ativado (varredura ao acessar) verifica todos os arquivos de um sistema. Ele pode retardar o servidor e o desempenho dos AEM Forms é afetado.

Para melhorar o desempenho, é possível direcionar o software antivírus para excluir os seguintes arquivos e pastas de AEM Forms da varredura sempre ativada (no acesso):

* Diretório de instalação do AEM. Se não for possível excluir o diretório completo, exclua o seguinte:

   * [Diretório]de instalação do AEM \crx-repository\temp
   * [Diretório]de instalação do AEM \crx-repository\repository
   * [Diretório]de instalação do AEM \crx-repository\launchpad

* Diretório temporário do servidor de aplicativos. O local padrão é:

   * (Jpatrão) Diretório de instalação [do AEM]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Webphere) \Programa Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms somente no diretório JEE)** Global Documento Armazenamento (GDS). O local padrão é:

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(AEM Forms somente no JEE)** Registros do servidor AEM Forms e diretório temporário. O local padrão é:

   * Registros do servidor - diretório [de instalação do]AEM Forms \Adobe\AEM forms\[app-server]\server\all\logs
   * Diretório temporário - diretório [de instalação do]AEM Forms\temp

>[!NOTE]
>
>* Se você estiver usando um local diferente para GDS e diretório temporário, abra AdminUI em `https://'[server]:[port]'/adminui`, navegue até **Início > Configurações > Configurações principais do sistema > Configurações** principais para confirmar o local em uso.

* Se o servidor AEM Forms tiver um desempenho lento mesmo depois de excluir os diretórios sugeridos, exclua também o arquivo executável Java (java.exe).



