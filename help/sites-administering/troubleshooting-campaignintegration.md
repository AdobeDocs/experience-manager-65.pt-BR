---
title: Solução de problemas da integração do Adobe Campaign
seo-title: Troubleshooting your Adobe Campaign Integration
description: Saiba como solucionar problemas com a Integração do Adobe Campaign.
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

As seguintes dicas de solução de problemas ajudam a resolver os problemas mais comuns que você pode encontrar ao integrar o AEM com o Adobe Campaign:

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

Para ambas as integrações, você pode verificar se as chamadas HTTP são enviadas (AEM > Adobe Campaign, Adobe Campaign > AEM):

* Quando as integrações estiverem falhando, verifique se essas chamadas chegam na outra extremidade (para evitar problemas de firewall/SSL).
* Para obter AEM funcionalidade, você verá que as chamadas json são solicitadas na interface AEM autor; isso não deve resultar em um erro HTTP-500. Se você vir erros HTTP-500, verifique o `error.log` para obter mais informações sobre isso.
* Aumentar o nível de depuração para classes de campanha no AEM também ajuda a solucionar problemas.

## Se a conexão falhar {#if-the-connection-fails}

Verifique se você configurou a variável **aemserver** no Adobe Campaign.

## Se as imagens não forem exibidas no console Adobe Campaign {#if-images-do-not-appear-in-the-adobe-campaign-console}

Verifique a fonte do HTML e valide se você pode abrir o URL do computador cliente. Se a URL tiver localhost:4503 nela, altere a configuração do Day CQ Link Externalizer em sua instância de autor para apontar para uma instância de publicação que pode ser acessada da máquina de console do Adobe Campaign.

Consulte [Configurar o Externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Caso não seja possível se conectar do AEM ao Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Procure a seguinte mensagem de erro no Adobe Campaign:

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para corrigir esse problema, altere o seguinte em **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Se nenhum dado for exibido na caixa de diálogo do Adobe Campaign {#if-no-data-displays-in-the-adobe-campaign-dialog}

No Adobe Campaign, verifique se não há barra à direita (/) após o número da porta.

![chlimage_1-149](assets/chlimage_1-149.png)

## Se você receber um aviso sobre sua localidade definida {#if-you-get-a-warning-about-your-setlocale}

Se você estiver iniciando o serviço Apache HTTPD e vir o erro `"Warning: setlocale: LC_CTYPE cannot change locale"` certifique-se de que você **en_CA.ISO-8859-15 localidade** instalado no seu sistema.

Você pode verificar se ele está instalado usando `local -a`. Se não estiver instalado, você pode aplicar patch **/usr/local/neolane/nl6/env.sh** e altere o local para um local instalado.

## Se ocorrer um erro ao compilar o script &#39;get_nms_amcGetSeedMetaData_jssp&#39; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se você vir a seguinte mensagem de erro no arquivo de log de AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Use a seguinte solução alternativa:

1. Abrir arquivo **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. Modifique a linha 467 do método &quot;amcGetSeedMetaData&quot;
1. Alterar `label : [inclView.@label](mailto:inclView.@label)` para `label : String([inclView.@label](mailto:inclView.@label))`

1. Salvar.
1. Reinicie o servidor.

## Se o Adobe Campaign exibir um erro ao clicar no botão Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Se ao clicar no botão **Sincronizar** no Adobe Campaign Classic, você verá o seguinte erro:

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Para corrigir esse problema, verifique se o URL de conexão AEM configurado nas Contas Externas está acessível no computador.

Um switch de **localhost** para um endereço IP resolveu esse problema.

## Se você receber um erro &#39;Não é possível analisar a data e hora de XTK &#39;indefinido&#39; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Depois de clicar em Sincronizar, ocorre um erro que ocorre um script nas páginas: Não é possível analisar Data e Hora XTK &#39;undefined&#39;: não é um valor XTK válido.

Isso acontece se ainda houver informações desatualizadas do Adobe Campaign na instância de AEM. Resolva esse problema removendo todas as configurações de integração de campanha que estão em AEM e reconstruindo-as. Em seguida, crie um novo template.

## Se uma conexão com SSL exibir um erro ao configurar o serviço de nuvem {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

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

Gere um tíquete junto à equipe de suporte da Adobe Campaign.

## Se você vir http em vez de um https esperado na caixa de diálogo de sincronização {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Com a seguinte configuração:

* Adobe Campaign hospedado usando https para comunicação com o autor do AEM
* Proxy reverso que encerra o SSL
* Instância local do AEM Author

Ao tentar sincronizar o conteúdo na entrega do Adobe Campaign, o AEM retorna uma lista de boletins informativos. No entanto, os urls dos boletins informativos na lista são endereços http. Ao selecionar um dos itens na lista, ocorre um erro.

Para resolver esse problema:

* O dispatcher ou proxy reverso precisa ser configurado para passar o protocolo original como cabeçalho.
* O *Filtro SSL do Serviço Http Apache Felix* na configuração OSGi ([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)) precisa ser configurado para as respectivas configurações de cabeçalho. Consulte [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## Se o modelo personalizado que criei não puder ser selecionado nas Propriedades da página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Ao criar um template de email para o Adobe Campaign, você deve incluir a propriedade **acMapping** com o valor **mapRecipient** no **jcr:content** do modelo, ou você não poderá selecionar o modelo do Adobe Campaign em **Propriedades da página** de AEM (o campo está desativado).

## Se você receber o erro &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; em seus logs {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Ao usar seu modelo personalizado, você recebe o erro &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; em seus logs. Nesse caso, instale o Featurepack 6576 a partir de [Compartilhamento de pacotes](/help/sites-administering/package-manager.md#package-share). Esse é um problema em que, se a propriedade acMapping for definida como um valor diferente de recipient.firstName, um valor em branco será criado no lado do Gerenciador do Adobe Campaign.
