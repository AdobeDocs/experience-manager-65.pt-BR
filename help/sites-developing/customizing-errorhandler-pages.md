---
title: Personalização de páginas mostradas pelo manipulador de erros
seo-title: Personalização de páginas mostradas pelo manipulador de erros
description: O AEM vem com um manipulador de erros padrão para lidar com erros HTTP
seo-description: O AEM vem com um manipulador de erros padrão para lidar com erros HTTP
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Personalização de páginas mostradas pelo manipulador de erros{#customizing-pages-shown-by-the-error-handler}

O AEM vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![chlimage_1-67](assets/chlimage_1-67a.png)

Os scripts fornecidos pelo sistema existem (em `/libs/sling/servlet/errorhandler`) para responder a códigos de erro, por padrão, os seguintes estão disponíveis com uma instância CQ padrão:

* 403,jsp
* 404,jsp

>[!NOTE]
>
>O AEM é baseado no Apache Sling, portanto consulte [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) para obter informações detalhadas sobre como lidar com erros.

>[!NOTE]
>
>Em uma instância do autor, o Filtro [de Depuração WCM do](/help/sites-deploying/osgi-configuration-settings.md) CQ está ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Em uma instância de publicação, o Filtro de depuração do CQ WCM *sempre* está desativado (mesmo se configurado como ativado).

## Como personalizar páginas mostradas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Suas páginas personalizadas serão criadas em `/apps` e sobrepõem as páginas padrão (que estão em `/libs`).

>[!NOTE]
>
>Consulte [Uso de sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

1. No repositório, copie os scripts padrão:

   * from `/libs/sling/servlet/errorhandler/`
   * para `/apps/sling/servlet/errorhandler/`
   Como o caminho de destino não existe por padrão, será necessário criá-lo ao fazer isso pela primeira vez.

1. Vá até `/apps/sling/servlet/errorhandler`. Aqui você pode:

   * edite o script existente apropriado para fornecer as informações necessárias.
   * crie e edite um novo script para o código necessário.

1. Salve as alterações e teste.

>[!CAUTION]
>
>Os manipuladores 404.jsp e 403.jsp foram especificamente projetados para atender à autenticação CQ5; em particular, para permitir o logon do sistema no caso desses erros.
>
>Assim, a substituição destes dois manipuladores deve ser feita com grande cuidado.

### Personalização da resposta a erros de HTTP 500 {#customizing-the-response-to-http-errors}

Os erros HTTP 500 são causados por exceções do lado do servidor.

* **[Erro](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**interno do servidor 500O servidor encontrou uma condição inesperada que o impedia de atender à solicitação.

Quando o processamento da solicitação resulta em uma exceção, a estrutura Apache Sling (na qual o AEM é criado):

* registra a exceção
* retorna:

   * o código de resposta HTTP 500
   * o rastreamento da pilha de exceções
   no corpo da resposta.

Ao [personalizar as páginas mostradas pelo manipulador](#how-to-customize-pages-shown-by-the-error-handler) de erros, é possível criar um `500.jsp` script. No entanto, só é utilizado se `HttpServletResponse.sendError(500)` for executado explicitamente; Ou seja, de um coletor de exceção.

Caso contrário, o código de resposta será definido como 500, mas o `500.jsp` script não será executado.

Para lidar com erros 500, o nome do arquivo do script do manipulador de erros deve ser o mesmo da classe de exceção (ou superclasse). Para lidar com todas essas exceções, é possível criar um script `/apps/sling/servlet/errorhandler/Throwable.js`p ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Em uma instância do autor, o Filtro [de Depuração WCM do](/help/sites-deploying/osgi-configuration-settings.md) CQ está ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Para um manipulador de erros personalizado, as respostas com o código 500 são necessárias; portanto, o Filtro de Depuração WCM do [CQ precisa ser desativado](/help/sites-deploying/osgi-configuration-settings.md). Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros Sling correto.
>
>Em uma instância de publicação, o Filtro de depuração do CQ WCM *sempre* está desativado (mesmo se configurado como ativado).

