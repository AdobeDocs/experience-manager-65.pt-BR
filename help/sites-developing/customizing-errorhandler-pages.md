---
title: Personalizar páginas mostradas pelo Manipulador de erros
description: O Adobe Experience Manager vem com um manipulador de erros padrão para lidar com erros HTTP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# Personalizar páginas mostradas pelo Manipulador de erros{#customizing-pages-shown-by-the-error-handler}

O Adobe Experience Manager (AEM) vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Existem scripts fornecidos pelo sistema (em `/libs/sling/servlet/errorhandler`) para responder a códigos de erro, por padrão, os itens a seguir estão disponíveis com uma instância CQ padrão:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>O AEM é baseado no Apache Sling. Como tal, ver [Tratamento de erros](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html) para obter informações detalhadas sobre o tratamento de erros do Sling.

>[!NOTE]
>
>Em uma instância de autor, a variável [Filtro de depuração CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) é ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Em uma instância de publicação, o Filtro de depuração WCM do CQ é *sempre* desativado (mesmo se configurado como ativado).

## Como personalizar páginas mostradas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Suas páginas personalizadas são criadas em `/apps` e sobrepor as páginas padrão (que estão em `/libs`).

>[!NOTE]
>
>Consulte [Uso de sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

1. No repositório, copie os scripts padrão:

   * de `/libs/sling/servlet/errorhandler/`
   * para `/apps/sling/servlet/errorhandler/`

   Como o caminho de destino não existe por padrão, você deve criá-lo ao fazer isso pela primeira vez.

1. Navegue até `/apps/sling/servlet/errorhandler` e siga um destes procedimentos:

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

* **[Erro interno de servidor 500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
O servidor encontrou uma condição inesperada que o impediu de atender à solicitação.

Quando o processamento de solicitações resulta em uma exceção, a estrutura do Apache Sling (em que o AEM está integrado):

* registra a exceção
* devoluções:

   * o código de resposta HTTP 500
   * o rastreamento de pilha de exceção

  no corpo da resposta.

Por [personalização das páginas mostradas pelo manipulador de erros](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` pode ser criado. No entanto, só é utilizado se `HttpServletResponse.sendError(500)` é executado explicitamente; ou seja, de um capturador de exceção.

Caso contrário, o código de resposta será definido como 500, mas a variável `500.jsp` não é executado.

Para tratar erros 500, o nome de arquivo do script do manipulador de erros deve ser igual à classe de exceção (ou superclasse). Para lidar com todas essas exceções, você pode criar um script `/apps/sling/servlet/errorhandler/Throwable.js`p ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Em uma instância de autor, a variável [Filtro de depuração CQ WCM](/help/sites-deploying/osgi-configuration-settings.md) é ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Para um manipulador de erros personalizado, são necessárias respostas com o código 500 - para que o [O Filtro de Depuração CQ WCM deve estar desabilitado](/help/sites-deploying/osgi-configuration-settings.md). Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros Sling correto.
>
>Em uma instância de publicação, o Filtro de depuração WCM do CQ é *sempre* desativado (mesmo se configurado como ativado).
