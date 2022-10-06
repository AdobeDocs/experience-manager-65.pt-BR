---
title: Criação de extensões personalizadas
seo-title: Creating Custom Extensions
description: Você pode chamar seu código personalizado no Adobe Campaign de AEM ou de AEM para Adobe Campaign
seo-description: You can call your custom code in Adobe Campaign from AEM or from AEM to Adobe Campaign
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
exl-id: 0702858e-5e46-451f-9ac3-40a4fec68ca0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# Criação de extensões personalizadas{#creating-custom-extensions}

Geralmente, ao implementar um projeto, você tem um código personalizado no AEM e no Adobe Campaign. Com o uso da API existente, você pode chamar o código personalizado no Adobe Campaign de AEM ou de AEM para Adobe Campaign. Este documento descreve como fazer isso.

## Pré-requisitos {#prerequisites}

Você precisa ter o seguinte instalado:

* Adobe Experience Manager
* Adobe Campaign 6.1

Consulte [Integração de AEM com o Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) para obter mais informações.

## Exemplo 1: AEM para Adobe Campaign {#example-aem-to-adobe-campaign}

A integração padrão entre o AEM e o Campaign é baseada em JSON e JSSP (JavaScript Server Page). Esses arquivos JSSP podem ser encontrados no console do Campaign e todos começam com **amc** (Adobe Marketing Cloud).

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[Para este exemplo, consulte Geometrixx](/help/sites-developing/we-retail.md), que está disponível em Compartilhamento de pacotes.

Neste exemplo, criamos um novo arquivo JSSP personalizado e o chamamos do lado do AEM para recuperar o resultado. Isso pode ser usado, por exemplo, para recuperar dados do Adobe Campaign ou para salvar dados no Adobe Campaign.

1. No Adobe Campaign, para criar um novo arquivo JSSP, clique no botão **Novo** ícone .

   ![](do-not-localize/chlimage_1-4a.png)

1. Insira o nome desse arquivo JSSP. Neste exemplo, usamos **cus:custom.jssp** (o que significa que estará no **cus** namespace).

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Coloque o seguinte código no arquivo jssp:

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. Salve o trabalho. O trabalho restante está em AEM.
1. Crie um servlet simples no AEM para chamar este JSSP. Neste exemplo, assumimos o seguinte:

   * Você tem a conexão trabalhando entre o AEM e o Campaign
   * O serviço de nuvem da campanha está configurado em **/content/geometrixx-outdoors**

   O objeto mais importante neste exemplo é o **GenericCampaignConnector**, que permite chamar (obter e publicar) arquivos jssp no lado do Adobe Campaign.

   Este é um pequeno trecho de código:

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. Como você vê neste exemplo, é necessário transmitir as credenciais na chamada do . Você pode obter isso por meio do método getCredentials() , onde é passado uma página que tem o serviço de nuvem do Campaign configurado.

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

O código completo é o seguinte:

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## Exemplo 2: Adobe Campaign para AEM {#example-adobe-campaign-to-aem}

AEM oferece APIs prontas para recuperar os objetos disponíveis em qualquer lugar na visualização do siteadmin explorer.

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[Para este exemplo, consulte Geometrixx](/help/sites-developing/we-retail.md), que está disponível em Compartilhamento de pacotes.

Para cada nó no explorador, há uma API vinculada a ela. Por exemplo, para o nó :

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

a API é:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

O fim do URL **.1.json** pode ser substituído por **.2.json**, **.3.json**, de acordo com o número de subníveis que você está interessado em obter a palavra-chave para todos eles **infinito** pode ser usada:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Agora, para consumir a API, devemos saber que o AEM, por padrão, usa autenticação básica.

Uma biblioteca JS chamada de **amcIntegration.js** O está disponível na versão 6.1.1 (build 8624 e superior) que implementa essa lógica entre vários outros.

### Chamada de API AEM {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
