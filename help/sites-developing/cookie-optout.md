---
title: Configuração do uso de cookies
seo-title: Configuração do uso de cookies
description: O AEM fornece um serviço que permite configurar e controlar como os cookies são usados com suas páginas da Web
seo-description: O AEM fornece um serviço que permite configurar e controlar como os cookies são usados com suas páginas da Web
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 3%

---


# Configuração do uso de cookies{#configuring-cookie-usage}

O AEM fornece um serviço que permite configurar e controlar como os cookies são usados com suas páginas da Web:

* Um serviço configurável do lado do servidor mantém uma lista de cookies que podem ser usados.
* Uma API javascript permite que seu código javascript verifique se um cookie pode ser usado.

Use esse recurso para garantir que suas páginas estejam em conformidade com o consentimento dos usuários em relação ao uso de cookies.

## Configuração de cookies permitidos {#configuring-allowed-cookies}

Configure o serviço de cancelamento do Adobe Granite para especificar como os cookies são usados em suas páginas da Web. A tabela a seguir descreve as propriedades que você pode configurar.

Para configurar o serviço, você pode usar o Console [da](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web ou [adicionar uma configuração OSGi ao repositório](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). A tabela a seguir descreve as propriedades necessárias para qualquer um dos métodos. Para uma configuração OSGi, o PID do serviço é `com.adobe.granite.optout`.

| Nome da propriedade (Console da Web) | Nome da propriedade OSGi | Descrição |
|---|---|---|
| Cookies de não participação | optout.cookies | Os nomes dos cookies que indicam, quando presentes no dispositivo do usuário, que o usuário não consentiu em usar cookies. |
| Cabeçalhos HTTP de opção | optout.headers | Os nomes dos cabeçalhos HTTP que indicam, quando presentes, que o usuário não consentiu em usar cookies. |
| Cookies de Lista branca | optout.whitelist.cookies | Uma lista de cookies essenciais para o funcionamento do site e que podem ser usados sem o consentimento do usuário. |

## Validação do uso de cookies {#validating-cookie-usage}

Use o javascript do lado do cliente para ligar para o Adobe Granite Opt-Out Service para verificar se você pode usar um cookie. Use o objeto javascript Granite.OptOutUtil para executar qualquer uma das seguintes tarefas:

* Obtenha uma lista de nomes de cookies que indicam que o usuário não concorda em usar cookies para fins de rastreamento.
* Obtenha uma lista de cookies que podem ser usados.
* Determine se o navegador da Web contém um cookie que indica que o usuário não concorda com o uso de cookies para rastreamento.
* Determine se um cookie específico pode ser usado.

A pasta [da biblioteca](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) cliente granite.utils fornece o objeto Granite.OptOutUtil. Adicione o seguinte código ao cabeçalho da página JSP para incluir um link para a biblioteca do javascript:

`<ui:includeClientLib categories="granite.utils" />`

Por exemplo, a seguinte função javascript determina se o cookie COOKIE_NAME pode ser usado antes de gravar nele:

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## O objeto JavaScript Granite.OptOutUtil {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil permite determinar se o uso de cookies é permitido.

### função getCookieNames() {#getcookienames-function}

Retorna os nomes dos cookies que, quando presentes, indicam que o usuário não deu consentimento para o uso de cookies.

**Parâmetros**

Nenhum.

**Retorna**

Uma matriz de nomes de cookies.

#### função getWhitelistCookieNames() {#getwhitelistcookienames-function}

Retorna os nomes dos cookies que podem ser usados independentemente do consentimento do usuário.

**Parâmetros**

Nenhum.

**Retorna**

Uma matriz de nomes de cookies.

#### função isOptedOut() {#isoptedout-function}

Determina se o navegador do usuário contém algum cookie que indica que o consentimento não foi dado para o uso de cookies.

**Parâmetros**

Nenhum.

**Retorna**

Um valor booliano de `true` se um cookie for encontrado que indica que não há consentimento, e um valor de `false` se nenhum cookie indicar não-consentimento.

### função maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina se um cookie específico pode ser usado no navegador do usuário. Essa função equivale a usar a `isOptedOut` função em conjunto com a determinação de se o cookie especificado está incluído na lista que a `getWhitelistCookieNames` função retorna.

**Parâmetros**

* cookieName: String. O nome do cookie.

**Retorna**

Um valor booliano de `true` if `cookieName` pode ser usado, ou um valor de `false` if `cookieName` não pode ser usado.
