---
title: Solução de problemas da integração do Adobe Campaign
seo-title: Troubleshooting your Adobe Campaign Integration
description: Saiba como solucionar problemas da integração do Adobe Campaign.
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Solução de problemas da integração do Adobe Campaign{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>Esta página se aplica ao Campaign Classic.

As seguintes dicas de solução de problemas ajudam a resolver os problemas mais comuns que você pode encontrar ao integrar o AEM ao Adobe Campaign:

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

Para ambas as integrações, é possível verificar se as chamadas HTTP são enviadas (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Quando as integrações estiverem falhando, verifique se essas chamadas chegam na outra extremidade (para evitar problemas de firewall/SSL).
* Para a funcionalidade AEM, você verá que chamadas json são solicitadas da interface do autor AEM; elas não devem resultar em um erro HTTP-500. Se você vir erros HTTP-500, verifique a `error.log` para obter mais informações sobre isso.
* Aumentar o nível de depuração para classes de campanha no AEM também ajuda a solucionar problemas.

## Se a conexão falhar {#if-the-connection-fails}

Verifique se você configurou o **aemserver** operador no Adobe Campaign.

## Se as imagens não aparecerem no console do Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Verifique a fonte do HTML e confirme se você pode abrir o URL da máquina cliente. Se o URL tiver localhost:4503, altere a configuração do Day CQ Link Externalizer na instância do autor para apontar para uma instância de publicação que possa ser acessada no computador do console do Adobe Campaign.

Consulte [Configurar o externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se não conseguir se conectar do AEM ao Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Procure a seguinte mensagem de erro no Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para corrigir esse problema, altere o seguinte no **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se nenhum dado for exibido na caixa de diálogo do Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

No Adobe Campaign, certifique-se de que você não tenha nenhuma barra à direita (/) após o número da porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se você receber um aviso sobre seu setlocale {#if-you-get-a-warning-about-your-setlocale}

Se você estiver iniciando o serviço Apache HTTPD e vir o erro `"Warning: setlocale: LC_CTYPE cannot change locale"` verifique se você tem o seu **en_CA.ISO-8859-15 localidade** instalado no sistema.

É possível verificar se ele está instalado usando `local -a`. Se ele não estiver instalado, você poderá corrigir **/usr/local/neolane/nl6/env.sh** script e altere o local para um local instalado.

## Se você receber um erro ao compilar o script &quot;get_nms_amcGetSeedMetaData_jssp&quot; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se você vir a seguinte mensagem de erro no arquivo de log do AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Use a seguinte solução alternativa:

1. Abrir arquivo **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modificar a linha 467 do método &quot;amcGetSeedMetaData&quot;
1. Alterar `label : [inclView.@label](mailto:inclView.@label)` para `label : String([inclView.@label](mailto:inclView.@label))`

1. Salvar.
1. Reinicie o servidor.

## Se o Adobe Campaign exibir um erro ao clicar no botão Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se, ao clicar no botão **Sincronizar** no Adobe Campaign Classic, você verá o seguinte erro:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Para corrigir esse problema, verifique se o URL de conexão do AEM configurado nas Contas externas pode ser acessado no computador.

Um switch de **localhost** para um endereço IP resolveu esse problema.

## Se você receber um erro &quot;Não é possível analisar data+hora XTK&quot; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Após clicar em Sincronizar, você receberá um erro informando que ocorreu um script nas páginas: Não é possível analisar Data+Hora XTK &#39;indefinida&#39;: não é um valor XTK válido.

Isso acontece se ainda houver informações desatualizadas do Adobe Campaign na instância do AEM. Resolva esse problema removendo todas as configurações de integração do Campaign que estão no AEM e reconstruindo-as. Em seguida, crie um novo template.

## Se uma conexão com SSL exibir um erro ao configurar o serviço em nuvem {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

No error.log de AEM, se você vir o seguinte:

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Crie um tíquete para a equipe de suporte da Adobe Campaign.

## Se você vir links http em vez de https na caixa de diálogo de sincronização {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Com a seguinte configuração:

* Adobe Campaign hospedado usando https para comunicação com o AEM Author
* Proxy reverso encerrando SSL
* Instância de autor local do AEM

Ao tentar sincronizar o conteúdo no delivery do Adobe Campaign, o AEM retorna uma lista de boletins informativos. No entanto, os urls para os boletins informativos na lista são endereços http. Ocorre um erro ao selecionar um dos itens na lista.

Para resolver esse problema:

* O dispatcher ou proxy reverso precisa ser configurado para transmitir o protocolo original como um cabeçalho.
* A variável *Filtro SSL do serviço Apache Felix Http* na configuração do OSGi ([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) precisa ser definida para as respectivas configurações de cabeçalho. Consulte [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se o modelo personalizado que criei não puder ser selecionado nas Propriedades da página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Ao criar um template de email para o Adobe Campaign, você deve incluir a propriedade **acMapping** com o valor **mapRecipient** no **jcr:content** do modelo, ou você não poderá selecionar o modelo Adobe Campaign em **Propriedades da página** de AEM (o campo está desativado).

## Se você receber o erro &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; em seus logs {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Ao usar o modelo personalizado, você recebe o erro &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; em seus logs. Nesse caso, instale o Featurepack 6576 da [Compartilhamento de pacotes](/help/sites-administering/package-manager.md#package-share). Esse é um problema em que, se a propriedade acMapping for definida como um valor diferente de recipient.firstName, um valor em branco será criado no lado do Adobe Campaign Manager.
