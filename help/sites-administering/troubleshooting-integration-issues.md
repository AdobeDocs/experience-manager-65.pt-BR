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
ht-degree: 2%

---

# Solução de problemas de integração{#troubleshooting-integration-issues}

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

### Verifique se não há erros de JavaScript {#ensure-there-are-no-javascript-errors}

Verifique se o console JavaScript do navegador exibe erros. Erros não tratados podem impedir que o código subsequente seja executado corretamente. Caso haja erros, verifique qual script está causando o erro e em qual área. O caminho para o script pode fornecer uma indicação para a funcionalidade à qual o script pertence.

### Logon no nível do componente {#logging-on-component-level}

Em alguns casos, pode ser útil adicionar mais instruções no nível do componente. Como o componente é renderizado, é possível adicionar uma marcação temporária para mostrar valores de variável, o que pode ajudar a identificar possíveis problemas. Por exemplo:

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

Para obter mais detalhes sobre o registro, consulte o [Registro](/help/sites-deploying/configure-logging.md) e [Trabalhar com registros de auditoria e arquivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) páginas.

## Problemas de integração do Analytics {#analytics-integration-issues}

### O Importador de relatórios causa alto uso de CPU/memória {#the-report-importer-causes-high-cpu-memory-usage}

O Importador de relatórios causa alto uso de CPU/memória ou causa `OutOfMemoryError` exceções.

#### Solução {#solution}

Para corrigir esse problema, você pode tentar o seguinte:

* Certifique-se de que não haja uma grande quantidade de PollingImporters registrados (consulte a seção &quot;Shutdown&quot; (Desligamento demorado devido ao PollingImporter&quot; abaixo).
* Executar importadores de relatórios em um determinado momento do dia usando expressões CRON para a `ManagedPollingImporter` nas configurações do [Console do OSGi](/help/sites-deploying/configuring-osgi.md).

Para obter detalhes adicionais sobre como criar serviços personalizados de importador de dados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### O encerramento demora muito tempo devido ao PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

O Analytics foi projetado tendo em mente um mecanismo de herança. Normalmente, você ativa o Analytics para um site ao adicionar uma referência a uma configuração do Analytics nas propriedades da página [Cloud Services](/help/sites-developing/extending-cloud-config.md) guia . A configuração é herdada para todas as subpáginas automaticamente, sem a necessidade de referenciá-la novamente, a menos que uma página exija uma configuração diferente. Adicionar uma referência a um site também cria automaticamente vários nós (12 para o AEM 6.3 e anterior ou 6 para o AEM 6.4 e posterior) do tipo `cq;PollConfig` que instancia os PollingImportporters usados para importar os dados do Analytics para o AEM. Como resultado:

* Ter muitas páginas referenciando o Analytics leva a uma grande quantidade de importadores de Polling.
* Além disso, copiar e colar páginas com uma referência a uma configuração do Analytics leva a uma duplicação de seus PollingImporters .

#### Solução {#solution-1}

Primeiro, analisar o [error.log](/help/sites-deploying/configure-logging.md) O pode fornecer-lhe algumas informações sobre a quantidade de PollingImporters ativos ou registrados. Por exemplo:

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

Em segundo lugar, verifique se apenas as páginas superiores (altas na hierarquia) têm uma configuração do Analytics referenciada.

Para obter detalhes adicionais sobre como criar serviços personalizados de importador de dados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas do DTM (herdado) {#dtm-legacy-issues}

### A tag de script do DTM não é renderizada na origem da página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

O [DTM](/help/sites-administering/dtm.md) a tag de script não é incluída corretamente na página, mesmo que a configuração tenha sido referenciada nas propriedades da página [Cloud Services](/help/sites-developing/extending-cloud-config.md) guia .

#### Solução {#solution-2}

Para corrigir o problema, você pode tentar o seguinte:

* Certifique-se de que as propriedades criptografadas possam ser descriptografadas (observe que a criptografia pode usar uma chave gerada automaticamente diferente em cada instância do AEM). Para obter mais detalhes, leia também [Suporte a criptografia para propriedades de configuração](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Republique as configurações encontradas em `/etc/cloudservices/dynamictagmanagement`
* Verificar ACLs em `/etc/cloudservices`. As ACLs devem ser:

   * permitir; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:read; Todos; rep:glob:&amp;ast;/defaults/&amp;ast;
   * permitir; jcr:read; Todos; rep:glob:&amp;ast;/defaults
   * permitir; jcr:read; Todos; rep:glob:&amp;ast;/public/&amp;ast;
   * permitir; jcr:read; Todos; rep:glob:&amp;ast;/public

Para obter mais informações sobre o gerenciamento de ACLs, leia o [Administração e segurança do usuário](/help/sites-administering/security.md#permissions-in-aem) página.

## Problemas de integração do Target {#target-integration-issues}

### O conteúdo direcionado não é visível no modo de Visualização ao usar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Esse problema ocorre porque os componentes de página personalizados não incluem as bibliotecas JSP ou cliente corretas que manipulam as integrações do DTM do Target.

#### Solução {#solution-3}

Você pode experimentar as seguintes soluções:

* Certifique-se de que o `headlibs.jsp` (se for caso disso) `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) inclui o seguinte:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Certifique-se de que o `head.html` (se for caso disso) `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **não** incluir seletivamente os títulos de integração específicos, como o exemplo abaixo:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

O `servicelibs.jsp` adiciona os objetos JavaScript do analytics necessários e carrega as bibliotecas do cloud service associadas ao site. Para o serviço do Target, as bibliotecas são carregadas por meio da variável `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas que são carregadas depende do tipo de biblioteca do cliente de destino ( `mbox.js` ou `at.js`) usada na configuração do Target.

Ao usar o DTM para entregar `mbox.js` ou `at.js` verifique se as bibliotecas estão carregadas antes da renderização do conteúdo. O uso de sistemas Tag Management que carregam essas bibliotecas de forma assíncrona pode causar problemas na execução do código JavaScript específico do Target.

Para obter mais informações, leia a [Desenvolvimento de conteúdo direcionado](/help/sites-developing/target.md#understanding-the-target-component) página.

### O erro &quot;ID de conjunto de relatórios ausente na inicialização do AppMeasurement&quot; é exibido no console do navegador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Esse problema pode aparecer quando o Adobe Analytics é implementado no site usando o DTM e usa o Código personalizado. A causa é usar a variável `s = new AppMeasurement()` para instanciar o `s` objeto.

#### Solução {#solution-4}

Use `s_gi` em vez de `new AppMeasurement` método de instanciação. Por exemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Uma oferta padrão é exibida aleatoriamente em vez da oferta correta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Esse problema pode ter várias causas:

* Carregamento de bibliotecas de clientes do Target ( `mbox.js` ou `at.js`) de forma assíncrona, o uso de sistemas Tag Management de terceiros pode quebrar aleatoriamente a definição de metas. As bibliotecas do Target devem ser carregadas de forma síncrona no cabeçalho da página. Isso sempre é verdadeiro quando as bibliotecas são entregues do AEM.

* Carregamento de duas bibliotecas de clientes do Target ( `at.js`) simultaneamente, por exemplo, um usando o DTM e outro usando a configuração do Target no AEM. Isso pode causar conflitos para a variável `adobe.target` definição se a variável `at.js` as versões do são diferentes.

#### Solução {#solution-5}

Você pode experimentar as seguintes soluções:

* Certifique-se de que o código do cliente que está carregando as bibliotecas do tipo DTM (que, por sua vez, carregam as bibliotecas do Target) seja executado sincronicamente na [cabeçalho da página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se o site estiver configurado para usar o DTM para fornecer bibliotecas do Target, verifique se a variável **Clientlib fornecido pelo DTM** está marcada na opção [Configuração do Target](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) para o site.

### Uma oferta padrão é sempre exibida em vez da oferta correta ao usar a AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

O AEM 6.2 e 6.3 pronto para uso não é compatível com o AT.js versão 1.3.0+. Com a at.js versão 1.3.0 introduzindo a validação de parâmetros para suas APIs, `adobe.target.applyOffer()` requer um parâmetro &quot;mbox&quot; que não é fornecido pelo `atjs-itegration.js` código.

#### Solução {#solution-6}

Para resolver esse problema, edite `atjs-itegration.js` e adicione o `"mbox": mboxName` no objeto de parâmetro para `adobe.target.applyOffer()` como se segue:

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

Esse problema provavelmente é [Configuração do A4T Analytics Cloud](/help/sites-administering/target-configuring.md) problema de provisionamento.

#### Solução {#solution-7}

Você precisa verificar se o A4T está ativado corretamente para sua conta do Target, emitindo a seguinte solicitação de verificação para AEM:

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

Se a resposta contiver a linha `a4tEnabled:false`, contance [Atendimento ao cliente do Adobe](https://helpx.adobe.com/contact.html) para provisionar a conta corretamente.

### APIs úteis do Target {#helpful-target-apis}

Abaixo estão apresentadas duas APIs do Target que podem ser úteis na solução de problemas do Target:

* Recuperar o terminal Target de um determinado código de cliente

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
