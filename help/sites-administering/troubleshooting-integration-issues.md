---
title: Solução de problemas de integração
seo-title: Solução de problemas de integração
description: Saiba como solucionar problemas de integração.
seo-description: Saiba como solucionar problemas de integração.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Solução de problemas de integração{#troubleshooting-integration-issues}

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

### Verifique se não há erros de JavaScript {#ensure-there-are-no-javascript-errors}

Verifique se o JavaScript Console do navegador exibe quaisquer erros. Erros sem tratamento podem impedir que o código subsequente seja executado corretamente. Caso haja erros, verifique qual script está causando o erro e em qual área. O caminho para o script pode fornecer uma indicação para a funcionalidade à qual o script pertence.

### Logon no nível do componente {#logging-on-component-level}

Em alguns casos, pode ser útil adicionar declarações adicionais no nível do componente. Como o componente é renderizado, é possível adicionar uma marcação temporária para mostrar valores variáveis que podem ajudar a identificar possíveis problemas. Por exemplo:

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

Para obter detalhes adicionais sobre registro, consulte as páginas [Registro](/help/sites-deploying/configure-logging.md) e [Trabalho com Registros de auditoria e Arquivos](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) de registro.

## Problemas de integração do Analytics {#analytics-integration-issues}

### O Importador de relatórios causa alto uso de CPU/memória {#the-report-importer-causes-high-cpu-memory-usage}

O Importador de relatórios causa alto uso de CPU/memória ou gera `OutOfMemoryError` exceções.

#### Solução {#solution}

Para corrigir esse problema, tente o seguinte:

* Certifique-se de que não haja uma grande quantidade de pesquisadores registrados (consulte a seção &quot;Desligamento leva muito tempo devido ao PollingImporter&quot; abaixo).
* Execute os Importadores de relatórios em um determinado momento do dia usando expressões CRON para as `ManagedPollingImporter` configurações no console [](/help/sites-deploying/configuring-osgi.md)OSGi.

Para obter detalhes adicionais sobre como criar serviços personalizados de importação de dados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### O encerramento demora muito devido ao PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

O Analytics foi projetado tendo em mente um mecanismo de herança. Normalmente, você ativa o Analytics para um site adicionando uma referência a uma configuração do Analytics na guia Serviços [da](/help/sites-developing/extending-cloud-config.md) nuvem de propriedades da página. A configuração é herdada automaticamente para todas as subpáginas, sem a necessidade de referenciá-la novamente, a menos que uma página exija uma configuração diferente. Adicionar uma referência a um site também cria automaticamente vários nós (12 para o AEM 6.3 e anterior ou 6 para o AEM 6.4 e posterior) do tipo `cq;PollConfig` que instancia os Importadores de pesquisa usados para importar dados do Analytics para o AEM. Como resultado:

* Ter muitas páginas referenciando o Analytics resulta em uma grande quantidade de PollingImporters.
* Além disso, copiar e colar páginas com uma referência a uma configuração do Analytics resulta em uma duplicação de seus Importadores de pesquisa.

#### Solução {#solution-1}

Em primeiro lugar, analisar o [error.log](/help/sites-deploying/configure-logging.md) pode fornecer uma ideia sobre a quantidade de PollingImporters ativos ou registrados. Por exemplo:

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

Em segundo lugar, certifique-se de que somente as principais páginas (acima na hierarquia) tenham uma configuração do Analytics referenciada.

Para obter detalhes adicionais sobre como criar serviços personalizados de importação de dados no AEM, leia o seguinte artigo [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## Problemas do DTM (herdado) {#dtm-legacy-issues}

### A tag de script do DTM não é renderizada na fonte da página {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

A tag de script do [DTM](/help/sites-administering/dtm.md) não está incluída corretamente na página, mesmo que a configuração tenha sido referenciada nas propriedades da página na guia Serviços [da](/help/sites-developing/extending-cloud-config.md) Nuvem.

#### Solução {#solution-2}

Para corrigir o problema, tente o seguinte:

* Verifique se as propriedades criptografadas podem ser descriptografadas (observe que a criptografia pode usar uma chave gerada automaticamente diferente em cada instância do AEM). Para obter mais detalhes, leia também Suporte [a criptografia para propriedades](/help/sites-administering/encryption-support-for-configuration-properties.md)de configuração.
* Publicar novamente as configurações encontradas em `/etc/cloudservices/dynamictagmanagement`
* Verifique as ACLs ativadas `/etc/cloudservices`. As ACLs devem ser:

   * permitir; jcr:read; webservice-support-servicelibfinder
   * permitir; jcr:read; todos; rep:global:&amp;ast;/defaults/&amp;ast;
   * permitir; jcr:read; todos; rep:global:&amp;ast;/defaults
   * permitir; jcr:read; todos; rep:global:&amp;ast;/public/&amp;ast;
   * permitir; jcr:read; todos; rep:global:&amp;ast;/public

Para obter mais informações sobre como gerenciar ACLs, leia a página Administração e segurança [do](/help/sites-administering/security.md#permissions-in-aem) usuário.

## Problemas de integração do Target {#target-integration-issues}

### Conteúdo direcionado não visível no modo de Visualização ao usar componentes de página personalizados {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Esse problema ocorre porque os componentes de página personalizados não incluem as bibliotecas JSP ou cliente corretas que manipulam as integrações do Target DTM.

#### Solução {#solution-3}

Você pode experimentar as seguintes soluções:

* Verifique se o personalizado `headlibs.jsp` (se houver) inclui o seguinte `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Certifique-se de que o personalizado `head.html` (se houver `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **não** inclua de forma seletiva cabeçalhos de integração específicos, como o exemplo abaixo:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

O `servicelibs.jsp` adiciona os objetos JavaScript do Analytics necessários e carrega as bibliotecas do serviço de nuvem associadas ao site. Para o serviço do Target, as bibliotecas são carregadas por meio do `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas que são carregadas depende do tipo de biblioteca do cliente de destino ( `mbox.js` ou `at.js`) usada na configuração do Target.

Ao usar o DTM para fornecer `mbox.js` ou `at.js` garantir que as bibliotecas sejam carregadas antes da renderização do conteúdo. O uso de sistemas de gerenciamento de tags que carregam essas bibliotecas de forma assíncrona pode causar problemas na execução do código JavaScript específico do destino.

Para obter mais informações, leia a página [Desenvolvimento para conteúdo](/help/sites-developing/target.md#understanding-the-target-component) direcionado.

### O erro &quot;ID de conjunto de relatórios ausente na inicialização do AppMeasurement&quot; é exibido no console do navegador {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Esse problema pode aparecer quando o Adobe Analytics é implementado no site usando o DTM e o Código personalizado. A causa é usar o objeto `s = new AppMeasurement()` para instanciar o `s` objeto.

#### Solução {#solution-4}

Use `s_gi` em vez do método de `new AppMeasurement` instanciação. Por exemplo:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Uma oferta padrão é exibida aleatoriamente em vez da oferta correta {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Esse problema pode ter várias causas:

* Carregar bibliotecas de clientes do Target ( `mbox.js` ou `at.js`) de forma assíncrona usando sistemas de gerenciamento de tags de terceiros pode quebrar aleatoriamente a definição de metas. As bibliotecas do Target devem ser carregadas sincronicamente no cabeçalho da página. Isso é sempre verdadeiro quando as bibliotecas são entregues do AEM.

* Carregar duas bibliotecas de clientes do Target ( `at.js`) simultaneamente, por exemplo, uma usando o DTM e outra usando a configuração do Target no AEM. Isso pode causar conflitos para a `adobe.target` definição se as `at.js` versões forem diferentes.

#### Solução {#solution-5}

Você pode experimentar as seguintes soluções:

* Certifique-se de que o código do cliente que carrega as bibliotecas semelhantes ao DTM (que por sua vez carregam as bibliotecas do Target) seja executado sincronicamente no cabeçalho da [página](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* se o site estiver configurado para usar o DTM para fornecer bibliotecas do Target, verifique se a opção **Clientlib fornecida pelo DTM** está marcada na configuração [do](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) Target do site.

### Uma oferta padrão é sempre exibida em vez da oferta correta ao usar o AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

O AEM 6.2 e 6.3 prontos para uso não é compatível com a versão 1.3.0+ do AT.js. Com a versão 1.3.0 do AT.js introduzindo a validação de parâmetro para suas APIs, `adobe.target.applyOffer()` é necessário um parâmetro &quot;mbox&quot; que não é fornecido pelo `atjs-itegration.js` código.

#### Solução {#solution-6}

Para resolver esse problema, edite `atjs-itegration.js` e adicione o `"mbox": mboxName` campo no objeto de parâmetro para o `adobe.target.applyOffer()` seguinte modo:

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

Esse problema provavelmente é um problema de provisionamento da Configuração [da nuvem do](/help/sites-administering/target-configuring.md) A4T Analytics.

#### Solução {#solution-7}

É necessário verificar se o A4T está corretamente ativado para sua conta do Target emitindo a seguinte solicitação de verificação para o AEM:

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

Se a resposta contiver a linha `a4tEnabled:false`, entre em contato com o Atendimento [ao cliente da](https://helpx.adobe.com/contact.html) Adobe para obter a conta provisionada corretamente.

### APIs úteis do Target {#helpful-target-apis}

Abaixo estão apresentadas duas APIs do Target que podem ser úteis ao solucionar problemas do Target:

* Recuperar o terminal do Target para um determinado clientcode

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

