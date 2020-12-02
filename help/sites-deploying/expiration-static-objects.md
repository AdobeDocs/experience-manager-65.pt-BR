---
title: Expiração de objetos estáticos
seo-title: Expiração de objetos estáticos
description: Saiba como configurar AEM para que objetos estáticos não expirem (por um período de tempo razoável).
seo-description: Saiba como configurar AEM para que objetos estáticos não expirem (por um período de tempo razoável).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Expiração de objetos estáticos{#expiration-of-static-objects}

Objetos estáticos (por exemplo, ícones) não são alterados. Portanto, o sistema deve ser configurado para que não expire (por um período de tempo razoável) e, assim, reduza o tráfego desnecessário.

Isso tem o seguinte impacto:

* Descarrega solicitações da infraestrutura do servidor.
* Aumenta o desempenho do carregamento da página, à medida que o navegador armazena objetos em cache no cache do navegador.

As expirações são especificadas pelo padrão HTTP referente à &quot;expiração&quot; dos arquivos (consulte, por exemplo, o capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;). Esse padrão usa o cabeçalho para permitir que os clientes armazenem objetos em cache até que sejam considerados obsoletos; esses objetos são armazenados em cache pelo tempo especificado, sem que seja feita nenhuma verificação de status no servidor de origem.

>[!NOTE]
>
>Essa configuração é completamente separada do Dispatcher (e não funcionará para ele).
>
>A finalidade do Dispatcher é armazenar dados em cache na frente da AEM.

Todos os arquivos, que não são dinâmicos e que não mudam ao longo do tempo, podem e devem ser armazenados em cache. A configuração do servidor HTTPD do Apache pode parecer com uma das seguintes opções - dependendo do ambiente:

>[!CAUTION]
>
>Você deve ter cuidado ao definir o período de tempo durante o qual um objeto é considerado atualizado. Como *não há verificação até que o período de tempo especificado tenha expirado*, o cliente pode acabar apresentando o conteúdo antigo do cache.

1. **Para uma instância de autor:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Isso permite que o cache intermediário (por exemplo, o cache do navegador) armazene arquivos CSS, Javascript, PNG e GIF por até um mês, até que eles expirem. Isso significa que eles não precisam ser solicitados do AEM ou do servidor da Web, mas podem permanecer no cache do navegador.

   Outras seções do site não devem ser armazenadas em cache em uma instância do autor, pois estão sujeitas a alterações a qualquer momento.

1. **Para uma instância de publicação:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   Isso permite que o cache intermediário (por exemplo, o cache do navegador) armazene arquivos CSS, Javascript, PNG e GIF por até um dia nos caches do cliente. Embora este exemplo ilustre as configurações globais para tudo o que está abaixo de `/content` e `/etc/designs`, você deve torná-lo mais granular.

   Dependendo da frequência com que seu site é atualizado, você também pode considerar armazenar páginas HTML em cache. Um período razoável seria de 1 hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Depois de configurar os objetos estáticos, faça a varredura `request.log`, ao selecionar as páginas que contêm esses objetos, para confirmar que nenhuma solicitação (desnecessária) está sendo feita para objetos estáticos.
