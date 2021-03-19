---
title: Logon único
seo-title: Logon único
description: Saiba como configurar o Logon único (SSO) para uma instância do AEM.
seo-description: Saiba como configurar o Logon único (SSO) para uma instância do AEM.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuração
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---


# Logon único {#single-sign-on}

O Logon único (SSO) permite que um usuário acesse vários sistemas após fornecer credenciais de autenticação (como nome de usuário e senha) uma vez. Um sistema separado (conhecido como autenticador confiável) executa a autenticação e fornece ao Experience Manager as credenciais do usuário. O Experience Manager verifica e aplica as permissões de acesso do usuário (ou seja, determina quais recursos o usuário tem permissão para acessar).

O serviço Manipulador de Autenticação SSO ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) processa os resultados de autenticação fornecidos pelo autenticador confiável. O Manipulador de Autenticação SSO procura um ssid (Identificador SSO) como o valor de um atributo especial nos seguintes locais nesta ordem:

1. Cabeçalhos de solicitação
1. Cookies
1. Parâmetros da solicitação

Quando um valor é encontrado, a pesquisa é concluída e esse valor é usado.

Configure os dois serviços a seguir para reconhecer o nome do atributo que armazena o ssid:

* O módulo de logon.
* O serviço de Autenticação SSO.

Você deve especificar o mesmo nome de atributo para ambos os serviços. O atributo está incluído no `SimpleCredentials` fornecido para `Repository.login`. O valor do atributo é irrelevante e ignorado, sua mera presença é importante e verificada.

## Configuração do SSO {#configuring-sso}

Para configurar o SSO para uma instância de AEM, você precisa configurar o [Manipulador de Autenticação SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

   Por exemplo, para o conjunto NTLM:

   * **Caminho:** conforme necessário; por exemplo,  `/`
   * **Nomes** de Cabeçalho:  `LOGON_USER`
   * **Formato** de ID:  `^<DOMAIN>\\(.+)$`

      Onde `<*DOMAIN*>` é substituído pelo seu próprio nome de domínio.
   Para CoSign:

   * **Caminho:** conforme necessário; por exemplo,  `/`
   * **Nomes** de Cabeçalho: remote_user
   * **Formato de ID:** AsIs

   Para o SiteMinder:

   * **Caminho:** conforme necessário; por exemplo,  `/`
   * **Nomes de Cabeçalho:** SM_USER
   * **Formato** de ID: AsIs



1. Confirme se o Logon único está funcionando conforme necessário; incluindo a autorização.

>[!CAUTION]
>
>Certifique-se de que os usuários não possam acessar AEM diretamente se o SSO estiver configurado.
>
>Ao exigir que os usuários passem por um servidor da Web que executa o agente do sistema SSO, é garantido que nenhum usuário possa enviar diretamente um cabeçalho, cookie ou parâmetro que fará com que o usuário seja confiável pelo AEM, pois o agente filtrará essas informações se forem enviadas de fora.
>
>Qualquer usuário que possa acessar diretamente sua instância do AEM sem passar pelo servidor da Web poderá agir como qualquer usuário enviando o cabeçalho, o cookie ou o parâmetro se os nomes forem conhecidos.
>
>Certifique-se também de que, dos cabeçalhos, cookies e nomes de parâmetros da solicitação, você configure apenas o que é necessário para a configuração do SSO.


>[!NOTE]
>
>O Logon único geralmente é usado junto com o [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Se você também estiver usando o [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) com o Microsoft Internet Information Server (IIS), então será necessária uma configuração adicional em:
>
>* `disp_iis.ini`
>* IIS

>
>
Em `disp_iis.ini` definido:
>(consulte [instalar o Dispatcher com o Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) para obter detalhes completos)
>
>* `servervariables=1` (encaminha variáveis do servidor IIS como cabeçalhos de solicitação para a instância remota)
>* `replaceauthorization=1` (substitui qualquer cabeçalho chamado &quot;Autorização&quot;, diferente de &quot;Básico&quot; pelo seu equivalente &quot;Básico&quot;)

>
>
No IIS:
>
>* desative **Anonymous access**
   >
   >
* habilite **Autenticação integrada do Windows**

>



Você pode ver qual manipulador de autenticação está sendo aplicado a qualquer seção da árvore de conteúdo usando a opção **Authenticator** do Felix Console; por exemplo:

`http://localhost:4502/system/console/slingauth`

O manipulador que melhor corresponde ao caminho é consultado primeiro. Por exemplo, se você configurar o manipulador-A para o caminho `/` e o manipulador-B para o caminho `/content`, uma solicitação para `/content/mypage.html` consultará o manipulador-B primeiro.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Exemplo {#example}

Para uma solicitação de cookie (usando o URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Usando a seguinte configuração:

* **Caminho**: `/`

* **Nomes** de Cabeçalho:  `TestHeader`

* **Nomes** de cookies:  `TestCookie`

* **Nomes** de Parâmetros:  `TestParameter`

* **Formato** de ID:  `AsIs`

A resposta seria:

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

Isso também funciona se você solicitar:
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

Ou você pode usar o seguinte comando curl para enviar o cabeçalho `TestHeader` para `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>Ao usar o parâmetro de solicitação em um navegador, você verá apenas alguns dos HTML - sem CSS. Isso ocorre porque todas as solicitações do HTML são feitas sem o parâmetro de solicitação.

## Removendo AEM Links de Saída {#removing-aem-sign-out-links}

Ao usar o SSO, o logon e o logout são tratados externamente, de modo que os próprios links de logout AEM não são mais aplicáveis e devem ser removidos.

O link para sair na tela de boas-vindas pode ser removido usando as etapas a seguir.

1. Sobrepor `/libs/cq/core/components/welcome/welcome.jsp` para `/apps/cq/core/components/welcome/welcome.jsp`
1. remova a seguinte parte do jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Para remover o link de logoff disponível no menu pessoal do usuário no canto superior direito, siga estas etapas:

1. Sobrepor `/libs/cq/ui/widgets/source/widgets/UserInfo.js` para `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Remova a seguinte parte do arquivo :

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```

