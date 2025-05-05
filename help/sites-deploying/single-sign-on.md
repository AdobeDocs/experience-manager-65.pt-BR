---
title: Logon único
description: Saiba como configurar o Logon único (SSO) para uma instância do Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Logon único {#single-sign-on}

O Logon único (SSO) permite que um usuário acesse vários sistemas após fornecer credenciais de autenticação (como um nome de usuário e senha) uma vez. Um sistema separado (conhecido como autenticador confiável) executa a autenticação e fornece ao Experience Manager as credenciais do usuário. O Experience Manager verifica e impõe as permissões de acesso para o usuário (ou seja, determina quais recursos o usuário tem permissão para acessar).

O serviço Manipulador de Autenticação SSO ( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) processa os resultados de autenticação fornecidos pelo autenticador confiável. O Manipulador de autenticação SSO procura um Identificador SSO (SSID) como o valor de um atributo especial nos seguintes locais, nesta ordem:

1. Cabeçalhos de solicitação
1. Cookies
1. Parâmetros de solicitação

Quando um valor é encontrado, a pesquisa é concluída e esse valor é usado.

Configure os dois serviços a seguir para reconhecer o nome do atributo que armazena o SSID:

* O módulo de logon.
* O serviço de autenticação SSO.

Especifique o mesmo nome de atributo para ambos os serviços. O atributo está incluído em `SimpleCredentials`, que é fornecido para `Repository.login`. O valor do atributo é irrelevante e ignorado, a mera presença dele é importante e verificada.

## Configuração de SSO {#configuring-sso}

Para configurar o SSO para uma instância AEM, configure o [Manipulador de Autenticação SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

   Por exemplo, para o conjunto NTLM:

   * **Caminho:** conforme necessário; por exemplo, `/`
   * **Nomes de Cabeçalho**: `LOGON_USER`
   * **Formato da ID**: `^<DOMAIN>\\(.+)$`

     Onde `<*DOMAIN*>` é substituído pelo nome do seu próprio domínio.

   Para CoSign:

   * **Caminho:** conforme necessário; por exemplo, `/`
   * **Nomes de Cabeçalho**: remote_user
   * **Formato da ID:** &#39;Como está&#39;

   Para o SiteMinder:

   * **Caminho:** conforme necessário; por exemplo, `/`
   * **Nomes de Cabeçalho:** SM_USER
   * **Formato de ID**: como está

1. Confirme se o Logon único está funcionando conforme necessário, incluindo autorização.

>[!CAUTION]
>
>Certifique-se de que os usuários não possam acessar o AEM diretamente se o SSO estiver configurado.
>
>Ao exigir que os usuários passem por um servidor Web que execute o agente do sistema SSO, é garantido que nenhum usuário possa enviar diretamente um cabeçalho, cookie ou parâmetro que levará o usuário a ser confiável pelo AEM, pois o agente filtrará essas informações se forem enviadas externamente.
>
>Qualquer usuário que possa acessar diretamente sua instância AEM sem passar pelo servidor da Web poderá agir como qualquer usuário enviando o cabeçalho, cookie ou parâmetro, se os nomes forem conhecidos.
>
>Além disso, certifique-se de que, entre os cabeçalhos, cookies e nomes de parâmetros de solicitação, você configure apenas aquele que é necessário para a configuração do SSO.
>

>[!NOTE]
>
>Logon Único é frequentemente usado com [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Se você também estiver usando o [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) com o Microsoft® Internet Information Server (IIS), será necessária uma configuração adicional em:
>
>* `disp_iis.ini`
>* IIS
>
>No conjunto `disp_iis.ini`:
>(consulte [instalando o Dispatcher com o Microsoft® Internet Information Server](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=pt-BR#microsoft-internet-information-server) para obter detalhes completos)
>
>* `servervariables=1` (encaminha variáveis do servidor IIS como cabeçalhos de solicitação para a instância remota)
>* `replaceauthorization=1` (substitui qualquer cabeçalho chamado &quot;Autorização&quot;, diferente de &quot;Básica&quot;, por seu equivalente &quot;Básica&quot;)
>
>No IIS:
>
>* desabilitar **Acesso anônimo**
>
>* habilitar a **Autenticação integrada do Windows**
>

Você pode ver qual manipulador de autenticação está sendo aplicado a qualquer seção da árvore de conteúdo usando a opção **Autenticador** do Felix Console; por exemplo:

`http://localhost:4502/system/console/slingauth`

O manipulador que melhor corresponde ao caminho é consultado primeiro. Por exemplo, se você configurar o manipulador A para o caminho `/` e o manipulador B para o caminho `/content`, uma solicitação para `/content/mypage.html` consultará o manipulador B primeiro.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Exemplo {#example}

Para uma solicitação de cookie (usando a URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Usando a seguinte configuração:

* **Caminho**: `/`

* **Nomes de Cabeçalho**: `TestHeader`

* **Nomes de Cookies**: `TestCookie`

* **Nomes de Parâmetros**: `TestParameter`

* **Formato da ID**: `AsIs`

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
>Ao usar o parâmetro de solicitação em um navegador, você só verá parte do HTML - sem CSS. Isso ocorre porque todas as solicitações do HTML são feitas sem o parâmetro de solicitação.

## Remoção de links de saída do AEM {#removing-aem-sign-out-links}

Ao usar o SSO, a entrada e a saída são tratadas externamente, de modo que os links de saída do AEM não sejam mais aplicáveis e devam ser removidos.

O link de saída na tela de boas-vindas pode ser removido usando as etapas a seguir.

1. Sobreposição de `/libs/cq/core/components/welcome/welcome.jsp` a `/apps/cq/core/components/welcome/welcome.jsp`
1. remova a seguinte parte da jsp.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Para remover o link de saída disponível no menu pessoal do usuário no canto superior direito, siga estas etapas:

1. Sobreposição de `/libs/cq/ui/widgets/source/widgets/UserInfo.js` a `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Remova a seguinte parte do arquivo:

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
