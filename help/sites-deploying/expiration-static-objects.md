---
title: Expiração de objetos estáticos
seo-title: Expiration of Static Objects
description: Saiba como configurar o AEM para que objetos estáticos não expirem (por um período razoável).
seo-description: Learn how to configure AEM so that static objects do not expire (for a reasonable period of time).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Expiração de objetos estáticos{#expiration-of-static-objects}

Os objetos estáticos (por exemplo, ícones) não são alterados. Portanto, o sistema deve ser configurado de modo que não expire (por um período de tempo razoável) e, assim, reduza o tráfego desnecessário.

Isso tem o seguinte impacto:

* Descarrega solicitações da infraestrutura do servidor.
* Aumenta o desempenho do carregamento da página, à medida que o navegador armazena objetos em cache no cache do navegador.

As expirações são especificadas pelo padrão HTTP em relação à &quot;expiração&quot; de arquivos (consulte, por exemplo, o capítulo 14.21 de [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Protocolo de Transferência de Hipertexto — HTTP 1.1&quot;). Esse padrão usa o cabeçalho para permitir que os clientes armazenem objetos em cache até que sejam considerados obsoletos; esses objetos são armazenados em cache pelo período especificado sem que nenhuma verificação de status seja feita no servidor de origem.

>[!NOTE]
>
>Essa configuração é completamente separada do (e não funcionará para) Dispatcher.
>
>A finalidade do Dispatcher é armazenar dados em cache na frente do AEM.

Todos os arquivos, que não são dinâmicos e que não mudam com o tempo, podem e devem ser armazenados em cache. A configuração do servidor HTTPD do Apache pode ser semelhante a um dos seguintes - dependendo do ambiente:

>[!CAUTION]
>
>Você deve ter cuidado ao definir o período durante o qual um objeto é considerado atualizado. Como há *nenhuma verificação até que o período especificado tenha expirado*, o cliente pode acabar apresentando conteúdo antigo do cache.

1. **Para uma instância de Autor:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Isso permite que o cache intermediário (por exemplo, o cache do navegador) armazene arquivos CSS, JavaScript, PNG e GIF por até um mês, até que expirem. Isso significa que eles não precisam ser solicitados do AEM ou do servidor Web, mas podem permanecer no cache do navegador.

   Outras seções do site não devem ser armazenadas em cache em uma instância de autor, pois estão sujeitas a alterações a qualquer momento.

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

   Isso permite que o cache intermediário (por exemplo, o cache do navegador) armazene arquivos CSS, JavaScript, PNG e GIF por até um dia nos caches do cliente. Embora este exemplo ilustre as configurações globais para tudo abaixo `/content` e `/etc/designs`, você deve torná-lo mais granular.

   Dependendo da frequência com que seu site é atualizado, você também pode considerar o armazenamento em cache de páginas de HTML. Um período de tempo razoável seria de 1 hora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Após configurar os objetos estáticos, faça a varredura `request.log`, ao selecionar páginas que contêm esses objetos, para confirmar que nenhuma solicitação (desnecessária) está sendo feita para objetos estáticos.
