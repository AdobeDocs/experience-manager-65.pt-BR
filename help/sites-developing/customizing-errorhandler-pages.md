---
title: Personalizar páginas mostradas pelo Manipulador de erros
description: O Adobe Experience Manager vem com um manipulador de erros padrão para lidar com erros HTTP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Personalizar páginas mostradas pelo Manipulador de erros{#customizing-pages-shown-by-the-error-handler}

O Adobe Experience Manager (AEM) vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Existem scripts fornecidos pelo sistema (em `/libs/sling/servlet/errorhandler`) para responder a códigos de erro; por padrão, os seguintes estão disponíveis com uma instância CQ padrão:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>O AEM é baseado no Apache Sling. Dessa forma, consulte [Tratamento de erros](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html) para obter informações detalhadas sobre a manipulação de erros de Sling.

>[!NOTE]
>
>Em uma instância de autor, o [Filtro de Depuração WCM do CQ](/help/sites-deploying/osgi-configuration-settings.md) está habilitado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Em uma instância de publicação, o Filtro de Depuração CQ WCM está *sempre* desabilitado (mesmo se configurado como habilitado).

## Como personalizar páginas mostradas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Suas páginas personalizadas são criadas em `/apps` e sobrepõem as páginas padrão (que estão em `/libs`).

>[!NOTE]
>
>Consulte [Usando Sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

1. No repositório, copie os scripts padrão:

   * de `/libs/sling/servlet/errorhandler/`
   * para `/apps/sling/servlet/errorhandler/`

   Como o caminho de destino não existe por padrão, você deve criá-lo ao fazer isso pela primeira vez.

1. Navegue até `/apps/sling/servlet/errorhandler` e execute um dos procedimentos a seguir:

   * edite o script existente apropriado para que você possa fornecer as informações necessárias.
   * crie e edite um novo script para o código necessário.

1. Salve as alterações e teste.

>[!CAUTION]
>
>Os manipuladores 404.jsp e 403.jsp foram projetados para atender à autenticação CQ5; em particular, para permitir o logon do sistema se houver esses erros.
>
>Portanto, a substituição desses dois manipuladores deve ser feita com muito cuidado.

### Personalização da resposta a erros HTTP 500 {#customizing-the-response-to-http-errors}

Os erros HTTP 500 são causados por exceções do lado do servidor.

* **[Erro Interno do Servidor](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
O servidor encontrou uma condição inesperada que o impediu de atender à solicitação.

Quando o processamento de solicitações resulta em uma exceção, a estrutura do Apache Sling (em que o AEM está integrado):

* registra a exceção
* devoluções:

   * o código de resposta HTTP 500
   * o rastreamento de pilha de exceção

  no corpo da resposta.

Com a [personalização das páginas mostradas pelo manipulador de erros](#how-to-customize-pages-shown-by-the-error-handler), um script `500.jsp` pode ser criado. No entanto, ele só é usado se `HttpServletResponse.sendError(500)` for executado explicitamente; ou seja, a partir de um capturador de exceção.

Caso contrário, o código de resposta será definido como 500, mas o script `500.jsp` não será executado.

Para tratar erros 500, o nome de arquivo do script do manipulador de erros deve ser igual à classe de exceção (ou superclasse). Para lidar com todas essas exceções, você pode criar um script `/apps/sling/servlet/errorhandler/Throwable.js`p ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Em uma instância de autor, o [Filtro de Depuração WCM do CQ](/help/sites-deploying/osgi-configuration-settings.md) está habilitado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Para um manipulador de erros personalizado, são necessárias respostas com o código 500; portanto, o [Filtro de Depuração WCM do CQ deve ser desabilitado](/help/sites-deploying/osgi-configuration-settings.md). Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros Sling correto.
>
>Em uma instância de publicação, o Filtro de Depuração CQ WCM está *sempre* desabilitado (mesmo se configurado como habilitado).
