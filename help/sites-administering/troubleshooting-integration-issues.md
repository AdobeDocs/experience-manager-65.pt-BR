---
title: Solução de problemas de integração
seo-title: Troubleshooting Integration Issues
description: Saiba como solucionar problemas de integração.
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1096'
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

Para obter detalhes adicionais sobre registro, consulte a seção [Logs](/help/sites-deploying/configure-logging.md) e [Trabalhar com registros de auditoria e arquivos de log](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) páginas.

## Problemas de integração do Analytics {#analytics-integration-issues}

### O Importador de relatórios causa alto uso de CPU/memória {#the-report-importer-causes-high-cpu-memory-usage}

O Importador de relatórios causa alto uso de CPU/memória ou causa `OutOfMemoryError` exceções.

#### Solução {#solution}

Para corrigir esse problema, você pode tentar o seguinte:

* Verifique se não há uma grande quantidade de PollingImporters registrados (consulte a seção &quot;Shutdown leva muito tempo devido ao PollingImporter&quot; abaixo).
* Execute importadores de relatórios em um determinado horário do dia usando expressões CRON para o `ManagedPollingImporter` configurações no [Console OSGi](/help/sites-deploying/configuring-osgi.md).

Para obter mais detalhes sobre como criar serviços de importador de dados personalizados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### O encerramento leva muito tempo devido ao Importador de buscas {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

O Analytics foi projetado tendo em mente um mecanismo de herança. Normalmente, você habilita o Analytics para um site adicionando uma referência a uma configuração do Analytics nas propriedades da página [Cloud Services](/help/sites-developing/extending-cloud-config.md) guia. A configuração é herdada para todas as subpáginas automaticamente, sem a necessidade de referenciá-la novamente, a menos que uma página exija uma configuração diferente. Adicionar uma referência a um site também cria automaticamente vários nós (12 para AEM 6.3 e anterior ou 6 para AEM 6.4 e posterior) do tipo `cq;PollConfig` que instancia os PollingImporters usados para importar os dados do Analytics para o AEM. Como resultado:

* Ter muitas páginas referenciando o Analytics resulta em uma grande quantidade de Importadores de buscas.
* Além disso, copiar e colar páginas com uma referência a uma configuração do Analytics leva a uma duplicação de PollingImporters.

#### Solução {#solution-1}

Em primeiro lugar, a [error.log](/help/sites-deploying/configure-logging.md) O pode fornecer alguns insights sobre a quantidade de Importadores de buscas ativos ou registrados. Por exemplo:

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

Para obter mais detalhes sobre como criar serviços de importador de dados personalizados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas do DTM (herdado) {#dtm-legacy-issues}

### A tag do script do DTM não é renderizada na origem da página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

A variável [DTM](/help/sites-administering/dtm.md) a tag de script não está incluída corretamente na página mesmo que a configuração tenha sido referenciada nas propriedades da página [Cloud Services](/help/sites-developing/extending-cloud-config.md) guia.

#### Solução {#solution-2}

Para corrigir o problema, tente o seguinte:

* Verifique se as propriedades criptografadas podem ser descriptografadas (observe que a criptografia pode usar uma chave gerada automaticamente diferente em cada instância do AEM). Para obter detalhes adicionais, leia também [Suporte de criptografia para propriedades de configuração](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Republicar as configurações encontradas em `/etc/cloudservices/dynamictagmanagement`
* Verificar ACLs em `/etc/cloudservices`. As ACLs devem ser:

   * allow; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:read; todos; rep:glob:&amp;ast;/defaults/&amp;ast;
   * permitir; jcr:read; todos; rep:glob:&amp;ast;/defaults
   * permitir; jcr:read; todos; rep:glob:&amp;ast;/public/&amp;ast;
   * permitir; jcr:read; todos; rep:glob:&amp;ast;/public

Para obter mais informações sobre o gerenciamento de ACLs, leia a [Administração e segurança do usuário](/help/sites-administering/security.md#permissions-in-aem) página.

## Problemas de integração do Target {#target-integration-issues}

### O conteúdo direcionado não fica visível no modo de Visualização ao usar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Esse problema ocorre porque os componentes de página personalizados não incluem as bibliotecas JSP ou de clientes corretas que lidam com as integrações do DTM do Target.

#### Solução {#solution-3}

Você pode experimentar as seguintes soluções:

* Verifique se a interface personalizada `headlibs.jsp` (se houver `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) inclui o seguinte:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Verifique se a interface personalizada `head.html` (se houver `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **não** inclua seletivamente headlibs de integração específicos, como o exemplo abaixo:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

A variável `servicelibs.jsp` adiciona os objetos JavaScript necessários do analytics e carrega as bibliotecas do cloud service associadas ao site. Para o serviço do Target, as bibliotecas são carregadas por meio da `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas carregadas depende do tipo de biblioteca do cliente de destino ( `mbox.js` ou `at.js`) usado na configuração do Target.

Ao usar o DTM para entregar `mbox.js` ou `at.js` verifique se as bibliotecas são carregadas antes que o conteúdo seja renderizado. Usar sistemas Tag Management que carregam essas bibliotecas de forma assíncrona pode causar problemas na execução do código JavaScript específico do público-alvo.

Para obter informações adicionais, leia a [Desenvolvimento de conteúdo direcionado](/help/sites-developing/target.md#understanding-the-target-component) página.

### O erro &quot;ID ausente do conjunto de relatórios na inicialização do AppMeasurement&quot; é exibido no console do navegador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Esse problema pode ocorrer quando o Adobe Analytics é implementado no site usando o DTM e o código personalizado. A causa é o uso da variável `s = new AppMeasurement()` para instanciar o `s` objeto.

#### Solução {#solution-4}

Uso `s_gi` em vez de `new AppMeasurement` método de instanciação. Por exemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Uma oferta padrão é exibida aleatoriamente em vez da oferta correta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Esse problema pode ter várias causas:

* Carregamento de bibliotecas de clientes do Target ( `mbox.js` ou `at.js`) usando sistemas Tag Management de terceiros pode quebrar o direcionamento aleatoriamente. As bibliotecas do Target devem ser carregadas de forma síncrona no cabeçalho da página. Isso é sempre verdadeiro quando as bibliotecas são entregues a partir do AEM.

* Carregamento de duas bibliotecas de cliente do Target ( `at.js`) simultaneamente, por exemplo, um usando o DTM e outro usando a configuração do Target no AEM. Isso pode causar conflitos para o `adobe.target` definição se a variável `at.js` diferentes.

#### Solução {#solution-5}

Você pode experimentar as seguintes soluções:

* Verifique se o código do cliente que carrega as bibliotecas do tipo DTM (que, por sua vez, carregam as bibliotecas do Target) é executado de forma síncrona na [cabeçalho da página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se o site estiver configurado para usar o DTM a fim de fornecer bibliotecas do Target, verifique se **Clientlib entregue pelo DTM** estiver marcada na caixa [Configuração do Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) para o site.

### Uma oferta padrão é sempre exibida em vez da oferta correta ao usar AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

O AEM 6.2 e 6.3 prontos para uso não é compatível com a AT.js versão 1.3.0+. Com a versão 1.3.0 da AT.js introduzindo a validação de parâmetros para suas APIs, `adobe.target.applyOffer()` exige um parâmetro &quot;mbox&quot; que não é fornecido pelo `atjs-itegration.js` código.

#### Solução {#solution-6}

Para resolver esse problema, edite `atjs-itegration.js` e adicione o `"mbox": mboxName` no objeto de parâmetro para `adobe.target.applyOffer()` do seguinte modo:

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

Esse problema provavelmente é uma [Configuração do A4T Analytics Cloud](/help/sites-administering/target-configuring.md) problema de provisionamento.

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

Se a resposta contiver a linha `a4tEnabled:false`, contato [Atendimento ao cliente Adobe](https://helpx.adobe.com/contact.html) para que sua conta seja provisionada corretamente.

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
