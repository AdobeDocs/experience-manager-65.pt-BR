---
title: Solução de problemas da integração com o Adobe Campaign
seo-title: Solução de problemas da integração com o Adobe Campaign
description: Saiba como solucionar problemas com a integração com o Adobe Campaign.
seo-description: Saiba como solucionar problemas com a integração com o Adobe Campaign.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---


# Solução de problemas da integração do Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Esta página se aplica ao Campaign Classic.

As seguintes dicas de solução de problemas ajudam a resolver os problemas mais comuns que você pode encontrar ao integrar AEM com a Adobe Campaign:

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

Para ambas as integrações, você pode verificar se chamadas HTTP são enviadas (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Quando as integrações estiverem falhando, verifique se essas chamadas chegam na outra extremidade (para evitar problemas de firewall/SSL).
* Para obter AEM funcionalidade, você verá que chamadas json são solicitadas da interface do autor AEM; isso não deve resultar em um erro HTTP-500. Se você vir erros HTTP-500, verifique `error.log` para obter mais informações sobre isso.
* Aumentar o nível de depuração para as classes de campanha no AEM também ajuda a solucionar problemas.

## Se a conexão falhar {#if-the-connection-fails}

Verifique se você configurou o operador **aemserver** no Adobe Campaign.

## Se as imagens não aparecerem no console do Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Verifique a fonte HTML e valide se você pode abrir o URL do computador cliente. Se o URL tiver localhost:4503 nele, altere a configuração do Externalizador de links do Day CQ na sua instância do autor para apontar para uma instância de publicação que pode ser acessada a partir do computador do console do Adobe Campaign.

Consulte [Configuração do Externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se você não conseguir se conectar do AEM ao Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Procure a seguinte mensagem de erro no Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para corrigir esse problema, altere o seguinte em **$CAMPANHA_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se nenhum dado for exibido na caixa de diálogo do Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

No Adobe Campaign, verifique se não há barra (/) após o número da porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se você receber um aviso sobre seu setlocale {#if-you-get-a-warning-about-your-setlocale}

Se você estiver iniciando o serviço Apache HTTPD e vir o erro `"Warning: setlocale: LC_CTYPE cannot change locale"` certifique-se de que seu **en_CA.ISO-8859-15 locale** esteja instalado no sistema.

Você pode verificar se ele está instalado usando `local -a`. Se ele não estiver instalado, você pode corrigir **/usr/local/neolane/nl6/env.sh** o script e alterar a localidade para uma localidade instalada.

## Se você receber um erro ao compilar o script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se você vir a seguinte mensagem de erro no arquivo de log AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Use a seguinte solução:

1. Abrir arquivo **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modificar a linha 467 do método &quot;amcGetSeedMetaData&quot;
1. Alterar `label : [inclView.@label](mailto:inclView.@label)` para `label : String([inclView.@label](mailto:inclView.@label))`

1. Salvar.
1. Reinicie o servidor.

## Se o Adobe Campaign exibir um erro ao clicar no botão Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se ao clicar no botão **Sincronizar** no Adobe Campaign Classic, você verá o seguinte erro:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Para corrigir esse problema, verifique se o AEM connection-url configurado no Conta externa está acessível no computador.

Um switch de **localhost** para um endereço IP resolveu esse problema.

## Se você receber um erro &#39;Não é possível analisar a Data XTK+Hora &#39;indefinida&#39;&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Depois de clicar em Sincronizar, você recebe um erro informando que um script nas páginas ocorreu: Não é possível analisar Data XTK+Hora &#39;undefined&#39;: não é um valor XTK válido.

Isso acontece se ainda houver informações desatualizadas do Adobe Campaign sobre a instância AEM. Resolva esse problema removendo todas as configurações de integração de campanha que estão em AEM e reconstruindo-as. Em seguida, crie um novo modelo.

## Se uma conexão com SSL exibir um erro ao configurar o serviço de nuvem {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

No error.log do AEM, se você vir o seguinte:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Levante um bilhete para a equipe de suporte da Adobe Campaign.

## Se você vir http em vez de um link https esperado na caixa de diálogo de sincronização {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Com a seguinte configuração:

* Adobe Campaign hospedado usando https para comunicação com o autor de AEM
* Reverter proxy terminando SSL
* Instância de autor de AEM local

Ao tentar sincronizar o conteúdo no Adobe Campaign delivery, AEM retorna uma lista de boletins informativos. No entanto, os urls para os boletins informativos na lista são endereços http. Ao selecionar um dos itens na lista, ocorre um erro.

Para resolver esse problema:

* O dispatcher ou o proxy reverso precisa ser configurado para passar o protocolo original como um cabeçalho.
* O *Filtro SSL do Apache Felix Http Service* na configuração do OSGi ([https://&lt;host>:&lt;porta>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) precisa ser configurado para as respectivas configurações de cabeçalho. Consulte [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se o modelo personalizado que criei não puder ser selecionado em Propriedades da página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Ao criar um modelo de email para Adobe Campaign, você deve incluir a propriedade **acMapping** com o valor **mapRecipient** no nó **jcr:content** do modelo, ou você não poderá selecionar o modelo Adobe Campaign em **Propriedades da página** AEM (o campo está desativado).

## Se você receber o erro &quot;com.day.cq.mcm.campanha.servlets.util.ParameterMapper&quot; em seus registros {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Ao usar seu modelo personalizado, você recebe o erro &quot;com.day.cq.mcm.campanha.servlets.util.ParameterMapper&quot; em seus registros. Neste evento, instale o Featurepack 6576 de [Compartilhamento de pacotes](/help/sites-administering/package-manager.md#package-share). Esse é um problema em que, se a propriedade acMapping estiver definida como um valor diferente de recipient.firstName, um valor em branco será criado no lado do Adobe Campaign Manager.
