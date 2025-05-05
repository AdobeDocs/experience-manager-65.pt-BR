---
title: Solução de problemas de integração
description: Saiba como solucionar problemas ao integrar com o Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---

# Solução de problemas de integração{#troubleshooting-integration-issues}

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

### Verifique se não há erros de JavaScript {#ensure-there-are-no-javascript-errors}

Verifique se o console JavaScript do navegador exibe erros. Erros não tratados podem impedir que o código subsequente seja executado corretamente. Caso haja erros, verifique qual script está causando o erro e em que área. O caminho para o script pode fornecer uma indicação à funcionalidade à qual o script pertence.

### Efetuando logon no nível do componente {#logging-on-component-level}

Em alguns casos, pode ser útil adicionar instruções adicionais no nível do componente. Como o componente é renderizado, você pode adicionar uma marcação temporária para mostrar valores de variável que podem ajudar a identificar possíveis problemas. Por exemplo:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Para obter detalhes adicionais sobre logs, consulte as páginas [Logging](/help/sites-deploying/configure-logging.md) e [Working with Audit Records and Log Files](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Problemas de integração do Analytics {#analytics-integration-issues}

### O Importador de relatórios causa alto uso de CPU/memória {#the-report-importer-causes-high-cpu-memory-usage}

O Importador de Relatórios causa alto uso de CPU/Memória ou causa `OutOfMemoryError` exceções.

#### Solução {#solution}

Para corrigir esse problema, você pode tentar o seguinte:

* Verifique se não há uma grande quantidade de PollingImporters registrados (consulte a seção &quot;Shutdown leva muito tempo devido ao PollingImporter&quot; abaixo).
* Execute importadores de relatórios em um determinado horário do dia usando expressões CRON para as configurações `ManagedPollingImporter` no [console OSGi](/help/sites-deploying/configuring-osgi.md).

Para obter detalhes adicionais sobre como criar serviços de importador de dados personalizados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### O encerramento leva muito tempo devido ao Importador de buscas {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

O Analytics foi projetado tendo em mente um mecanismo de herança. Normalmente, você habilita o Analytics para um site adicionando uma referência a uma configuração do Analytics na guia [Cloud Service](/help/sites-developing/extending-cloud-config.md) das propriedades da página. A configuração é herdada para todas as subpáginas automaticamente, sem a necessidade de referenciá-la novamente, a menos que uma página exija uma configuração diferente. Adicionar uma referência a um site também cria automaticamente vários nós (12 para AEM 6.3 e anterior ou 6 para AEM 6.4   e posterior) do tipo `cq;PollConfig` que instancia PollingImporters usados para importar dados do Analytics para AEM. Como resultado:

* Ter muitas páginas referenciando o Analytics resulta em uma grande quantidade de Importadores de buscas.
* Além disso, copiar e colar páginas com uma referência a uma configuração do Analytics leva a uma duplicação de PollingImporters.

#### Solução {#solution-1}

Primeiramente, analisar o [error.log](/help/sites-deploying/configure-logging.md) pode fornecer informações sobre a quantidade de PollingImporters ativos ou registrados. Por exemplo:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

Em segundo lugar, verifique se apenas as páginas principais (no alto da hierarquia) têm uma configuração do Analytics referenciada.

Para obter detalhes adicionais sobre como criar serviços de importador de dados personalizados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas do DTM (herdado) {#dtm-legacy-issues}

### A tag do script do DTM não é renderizada na origem da página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

A marca de script do [DTM](/help/sites-administering/dtm.md) não está incluída corretamente na página, embora a configuração tenha sido referenciada na guia de propriedades de página [Cloud Service](/help/sites-developing/extending-cloud-config.md).

#### Solução {#solution-2}

Para corrigir o problema, tente o seguinte:

* Verifique se as propriedades criptografadas podem ser descriptografadas (observe que a criptografia pode usar uma chave gerada automaticamente diferente em cada instância do AEM). Para obter detalhes adicionais, leia também [Suporte a Criptografia para Propriedades de Configuração](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Republicar as configurações encontradas em `/etc/cloudservices/dynamictagmanagement`
* Verificar ACLs em `/etc/cloudservices`. As ACLs devem ser:

   * allow; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/defaults/`&ast;
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/defaults`
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/public/`&ast;
   * permitir; jcr:read; todos; `rep:glob:`&ast;`/public`

Para obter mais informações sobre o gerenciamento de ACLs, leia a página [Administração e Segurança do Usuário](/help/sites-administering/security.md#permissions-in-aem).

## Problemas de integração do Target {#target-integration-issues}

### O conteúdo direcionado não fica visível no modo de Visualização ao usar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Esse problema ocorre porque os componentes de página personalizados não incluem as bibliotecas JSP ou de clientes corretas que lidam com as integrações do DTM do Target.

#### Solução {#solution-3}

Você pode experimentar as seguintes soluções:

* Certifique-se de que o `headlibs.jsp` personalizado (se qualquer `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) inclua o seguinte:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Certifique-se de que o `head.html` personalizado (se qualquer `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **não** inclua seletivamente headlibs de integração específicas, como o exemplo abaixo:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

O `servicelibs.jsp` adiciona os objetos JavaScript de análise necessários e carrega as bibliotecas de serviços de nuvem associadas ao site. Para o serviço do Target, as bibliotecas são carregadas por meio do `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas que são carregadas depende do tipo de biblioteca de cliente de destino ( `mbox.js` ou `at.js`) usada na configuração de Destino.

Ao usar o DTM para entregar `mbox.js` ou `at.js`, verifique se as bibliotecas são carregadas antes do conteúdo ser renderizado. O uso de sistemas Tag Management que carregam essas bibliotecas de forma assíncrona pode causar problemas na execução do código JavaScript específico do público-alvo.

Para obter mais informações, leia a página [Desenvolvimento de Conteúdo Direcionado](/help/sites-developing/target.md#understanding-the-target-component).

### O erro &quot;ID ausente do conjunto de relatórios na inicialização do AppMeasurement&quot; é exibido no console do navegador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Esse problema pode ocorrer quando o Adobe Analytics é implementado no site usando o DTM e o código personalizado. A causa é o uso de `s = new AppMeasurement()` para instanciar o objeto `s`.

#### Solução {#solution-4}

Use `s_gi` em vez do método de instanciação `new AppMeasurement`. Por exemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Uma oferta padrão é exibida aleatoriamente em vez da oferta correta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Esse problema pode ter várias causas:

* O carregamento assíncrono de bibliotecas de cliente do Target ( `mbox.js` ou `at.js`) usando Sistemas Tag Management de terceiros pode quebrar aleatoriamente o direcionamento. As bibliotecas do Target devem ser carregadas de forma síncrona no cabeçalho da página. Isso é sempre verdadeiro quando as bibliotecas são entregues a partir do AEM.

* Carregar duas bibliotecas de clientes do Target ( `at.js`) simultaneamente, por exemplo, uma usando DTM e outra usando a configuração do Target no AEM. Isso poderá causar conflitos para a definição `adobe.target` se as versões `at.js` forem diferentes.

#### Solução {#solution-5}

Você pode experimentar as seguintes soluções:

* Verifique se o código do cliente que carrega as bibliotecas do tipo DTM (que por sua vez carregam as bibliotecas do Target) é executado de forma síncrona no [cabeçalho da página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se o site estiver configurado para usar o DTM para entregar bibliotecas do Target, verifique se a opção **Clientlib entregue pelo DTM** está marcada na [Configuração do Target](https://helpx.adobe.com/br/experience-manager/6-3/sites/administering/using/target-configuring.html) para o site.

### Uma oferta padrão é sempre exibida em vez da oferta correta ao usar AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

O AEM 6.2 e 6.3 prontos para uso não é compatível com a AT.js versão 1.3.0+. Com a versão 1.3.0 da AT.js introduzindo a validação de parâmetro para suas APIs, `adobe.target.applyOffer()` requer um parâmetro &quot;mbox&quot; que não é fornecido pelo código `atjs-itegration.js`.

#### Solução {#solution-6}

Para resolver esse problema, edite `atjs-itegration.js` e adicione o campo `"mbox": mboxName` no objeto de parâmetro para `adobe.target.applyOffer()` da seguinte maneira:

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### A página Metas e configurações não mostra a seção Fontes de relatórios {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Este problema é provavelmente um problema de provisionamento da [Configuração A4T do Analytics Cloud](/help/sites-administering/target-configuring.md).

#### Solução {#solution-7}

Você precisa verificar se o A4T está habilitado corretamente para sua conta Target, emitindo a seguinte solicitação de verificação para o AEM:

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Se a resposta contiver a linha `a4tEnabled:false`, entre em contato com o [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/contact.html) para obter a configuração correta da sua conta.

### APIs úteis do Target {#helpful-target-apis}

Abaixo estão duas APIs do Target que podem ser úteis ao solucionar problemas do Target:

* Recuperar o ponto de extremidade do Target para um determinado clientcode

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Recuperar o perfil de um cliente

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
