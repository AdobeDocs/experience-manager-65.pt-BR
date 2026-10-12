---
title: Otimização de formulários do HTML5
description: Você pode otimizar o tamanho de saída dos formulários HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms,Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%
---
# Otimização de formulários do HTML5 {#optimizing-html-forms}

O HTML5 forms renderiza formulários no formato HTML5. A saída resultante pode ser grande, dependendo de fatores como o tamanho do formulário e as imagens no formulário. Para otimizar a transferência de dados, a abordagem recomendada é compactar a resposta do HTML usando o Servidor Web do qual a solicitação está sendo atendida. Essa abordagem reduz o tamanho da resposta, o tráfego de rede e o tempo necessário para transmitir dados entre as máquinas do servidor e do cliente.

Este artigo descreve as etapas necessárias para habilitar a compactação para o Apache Web Server 2.0 de 32 bits, com JBoss.

>[!NOTE]
>
>As instruções a seguir não se aplicam a servidores diferentes do Apache Web Server 2.0 de 32 bits.

Obtenha o software Apache Web Server aplicável ao seu sistema operacional:

* Para Windows, baixe o servidor Web Apache do site do Projeto Apache HTTP Server.
* Para Solaris 64 bits, baixe o servidor Web Apache do site Sunfreeware para Solaris.
* Para Linux, o servidor Web Apache é pré-instalado em um sistema Linux.

O Apache pode se comunicar com o JBoss usando HTTP ou o protocolo AJP.

1. Remova o comentário das seguintes configurações de módulo no arquivo *APACHE_HOME/conf/httpd.conf*.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, o diretório padrão APACHE_HOME é /etc/httpd/.

1. Configure o proxy na porta 8080 do JBoss.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf*.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Quando você usa um proxy, as seguintes alterações de configuração são necessárias:
   >
   >* Acesso: *https://&lt;servidor>:&lt;porta>/system/console/configMgr*
   >* Editar a configuração do Filtro referenciador do Apache Sling
   >* Em Permitir hosts, adicione a entrada para o servidor proxy

1. Ative a compactação.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf*.

   ```xml
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
