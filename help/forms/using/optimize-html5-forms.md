---
title: Otimizar formulários HTML5
seo-title: Otimizar formulários HTML5
description: É possível otimizar o tamanho de saída dos formulários HTML5.
seo-description: É possível otimizar o tamanho de saída dos formulários HTML5.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Otimizar formulários HTML5 {#optimizing-html-forms}

Formulários HTML5 renderizam formulários no formato HTML5. A saída resultante pode ser grande dependendo de fatores como o tamanho do formulário e as imagens no formulário. Para otimizar a transferência de dados, a abordagem recomendada é compactar a resposta HTML usando o Servidor Web do qual a solicitação está sendo atendida. Essa abordagem reduz o tamanho da resposta, o tráfego da rede e o tempo necessário para transmitir dados entre o servidor e os computadores clientes.

Este artigo descreve as etapas necessárias para habilitar a compactação para o Apache Web Server 2.0 de 32 bits, com JBoss.

*Observação: As instruções a seguir não se aplicam ao servidor que não seja o Apache Web Server 2.0 de 32 bits.*

Obtenha o software do servidor Web Apache aplicável ao seu sistema operacional:

* Para Windows, baixe o servidor Web Apache do site do Apache HTTP Server Project.
* Para Solaris de 64 bits, baixe o servidor da Web Apache do site Sunfreeware para Solaris.
* Para Linux, o servidor Web Apache é pré-instalado em um sistema Linux.

O Apache pode se comunicar com o JBoss usando HTTP ou o protocolo AJP.

1. Exclua as barras de comentário das seguintes configurações de módulo no arquivo *APACHE_HOME/conf/httpd.conf* .

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, o diretório padrão APACHE_HOME é /etc/httpd/.

1. Configure o proxy na porta 8080 do JBoss.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf* .

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Quando você usa um proxy, as seguintes alterações de configuração são necessárias:
   >
   >* Acesso: *https://&lt;servidor>:&lt;porta>/system/console/configMgr*
   * Editar a configuração do Filtro de Quem indicou Apache Sling
   * Em Permitir hosts, adicione a entrada para o servidor proxy


1. Ative a compactação.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf* .

   ```java
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Para acessar o servidor AEM, use https://[Apache_server]:80.
