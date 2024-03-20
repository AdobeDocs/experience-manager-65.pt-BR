---
title: Ajuste de desempenho do servidor do AEM Forms
description: Para que o AEM Forms tenha um desempenho ideal, você pode ajustar as configurações de cache e os parâmetros JVM. Além disso, o uso de um servidor Web pode aprimorar o desempenho da implantação do AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Ajuste de desempenho do AEM Forms Server{#performance-tuning-of-aem-forms-server}

Este artigo discute estratégias e práticas recomendadas que você pode implementar para reduzir gargalos e otimizar o desempenho da sua implantação do AEM Forms.

## Configurações de cache {#cache-settings}

Você pode configurar e controlar a estratégia de armazenamento em cache do AEM Forms usando o **Configurações do Forms Mobile** no Console de configuração da Web do AEM em:

* (AEM Forms no OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms no JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

As opções disponíveis para armazenamento em cache são as seguintes:

* **Nenhum**: força o a não armazenar em cache nenhum artefato. Na prática, isso retarda o desempenho e exige alta disponibilidade de memória devido à ausência de cache.
* **Conservador**: determina o armazenamento em cache somente dos artefatos intermediários gerados antes da renderização do formulário, como um modelo contendo fragmentos e imagens embutidas.
* **Agressivo**: força o a armazenar em cache quase tudo o que pode ser armazenado em cache, incluindo o conteúdo de HTML renderizado, além de todos os artefatos do nível de armazenamento em cache conservador. Ele resulta no melhor desempenho, mas também consome mais memória para armazenar artefatos em cache. Estratégia agressiva de armazenamento em cache significa que você obtém desempenho de tempo constante na renderização de um formulário conforme o conteúdo renderizado é armazenado em cache.

As configurações de cache padrão do AEM Forms podem não ser boas o suficiente para alcançar o desempenho ideal. Portanto, é recomendável usar as seguintes configurações:

* **Estratégia de cache**: Agressivo
* **Tamanho do cache** (em termos de número de formulários): Conforme exigido
* **Tamanho máximo do objeto**: conforme necessário

![Configurações do Forms Mobile](assets/snap.png)

>[!NOTE]
>
>Se você usar o AEM Dispatcher para armazenar em cache formulários adaptáveis, ele também armazenará em cache formulários adaptáveis que contêm formulários com dados pré-preenchidos. Se esses formulários forem veiculados a partir do cache do AEM Dispatcher, isso poderá levar ao fornecimento de dados pré-preenchidos ou obsoletos aos usuários. Portanto, use o AEM Dispatcher para armazenar em cache formulários adaptáveis que não usam dados pré-preenchidos. Além disso, um cache do Dispatcher não invalida automaticamente os fragmentos em cache. Portanto, não os use para armazenar em cache fragmentos de formulário. Para esses formulários e fragmentos, use [Cache de formulários adaptáveis](../../forms/using/configure-adaptive-forms-cache.md).

## Parâmetros JVM {#jvm-parameters}

Para um desempenho ideal, é recomendável usar a seguinte JVM `init` argumentos para configurar o `Java heap` e `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>As configurações recomendadas são para o JDK do Windows 2008 R2 8 Core e Oracle HotSpot 1.7 (64 bits) e devem ser aumentadas ou diminuídas de acordo com a configuração do sistema.

## Uso de um servidor Web {#using-a-web-server}

Os formulários adaptáveis e os formulários HTML5 são renderizados no formato HTML5. A saída resultante pode ser grande, dependendo de fatores como o tamanho do formulário e as imagens no formulário. Para otimizar a transferência de dados, a abordagem recomendada é compactar a resposta de HTML usando o servidor Web do qual a solicitação está sendo atendida. Essa abordagem reduz o tamanho da resposta, o tráfego de rede e o tempo necessário para transmitir dados entre máquinas de servidor e cliente.

Por exemplo, execute as seguintes etapas para habilitar a compactação no Apache Web Server 2.0 de 32 bits com JBoss®:

>[!NOTE]
>
>As instruções a seguir não se aplicam a nenhum servidor diferente do Apache Web Server 2.0 de 32 bits. Para as etapas específicas de qualquer outro servidor, consulte a documentação do produto correspondente.

As etapas a seguir demonstram as alterações necessárias para habilitar a compactação com o Apache Web Server

**Obter o software Apache Web Server aplicável ao seu sistema operacional**

* Windows: baixe o servidor Web Apache do site do Projeto Apache HTTP Server.
* Solaris™ 64 bits: baixe o servidor Web Apache do site Sunfreeware para Solaris™.
* Linux®: o servidor Web Apache é pré-instalado em um sistema Linux®.

O Apache pode se comunicar com o CRX usando o protocolo HTTP. As configurações são para otimização usando HTTP.

1. Remova o comentário das seguintes configurações de módulo em `APACHE_HOME/conf/httpd.conf` arquivo.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >No Linux®, o padrão é `APACHE_HOME` é `/etc/httpd/`.

1. Configure o proxy na porta 4502 do crx.
Adicionar configuração a seguir em `APACHE_HOME/conf/httpd.conf` arquivo de configuração.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Ative a compactação. Adicionar configuração a seguir em `APACHE_HOME/conf/httpd.conf` arquivo de configuração.

   **Para formulários HTML5**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
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
           #Do not compress
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

## Usar um antivírus no servidor que executa o AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

Você pode enfrentar desempenho lento nos servidores que executam um software antivírus. Um software antivírus (varredura ao acessar) sempre ativo examina todos os arquivos de um sistema. Ela pode retardar o servidor e o desempenho do AEM Forms é afetado.

Para melhorar o desempenho, você pode direcionar o software antivírus para excluir os seguintes arquivos e pastas do AEM Forms da varredura sempre ativa (ao acessar):

* Diretório de instalação do AEM. Se não for possível excluir o diretório completo, exclua o seguinte:

   * [Diretório de instalação do AEM]\crx-repository\temp
   * [Diretório de instalação do AEM]\crx-repository\repository
   * [Diretório de instalação do AEM]\crx-repository\launchpad

* Diretório temporário do servidor de aplicativos. O local padrão é:

   * (JBoss®) [Diretório de instalação do AEM]\jboss\standalone\tmp
   * (WebLogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (WebSphere®) \Programa Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms somente no JEE)** Diretório de Armazenamento Global de Documentos (GDS). O local padrão é:

   * (JBoss®) [raiz do appserver]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere®) [raiz do appserver]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(AEM Forms somente no JEE)** Registros do servidor do AEM Forms e diretório temporário. O local padrão é:

   * Logs do servidor - [diretório de instalação do AEM Forms]\Adobe\AEM formulários\[servidor-aplicativo]\server\all\logs
   * Diretório temporário - [diretório de instalação do AEM Forms]\temp

>[!NOTE]
>
>* Se você estiver usando um local diferente para GDS e diretório temporário, abra a interface do usuário do administrador em `https://'[server]:[port]'/adminui`, navegue até **Início > Configurações > Configurações do sistema principal > Configurações principais** para confirmar o local em uso.
>
* Se o servidor do AEM Forms funcionar lentamente mesmo após a exclusão dos diretórios sugeridos, exclua também o arquivo executável Java™ (java.exe).
>
