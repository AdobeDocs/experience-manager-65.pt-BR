---
title: Solução de problemas da integração do Adobe Campaign Classic
description: Saiba como solucionar problemas com a integração do Adobe Campaign Classic.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Solução de problemas da integração do Adobe Campaign Classic{#troubleshooting-your-adobe-campaign-classic-integration}

Saiba como solucionar problemas com a integração do Adobe Campaign Classic (ACC).

As seguintes dicas de solução de problemas ajudam a resolver os problemas mais comuns que você pode encontrar ao integrar AEM ao ACC.

## Dicas gerais de solução de problemas {#general-troubleshooting-tips}

Verifique se as chamadas HTTP são enviadas e recebidas por ambas as soluções (AEM > Adobe Campaign Classic, Adobe Campaign Classic > AEM). Esta dica ajuda a evitar problemas de firewall/SSL.

* Para a funcionalidade AEM, você pode ver que as chamadas JSON são solicitadas da interface do autor do AEM
   * Essas chamadas não devem resultar em um erro HTTP-500.
   * Se você vir erros HTTP-500, verifique a `error.log` para obter mais informações.
* Aumentar o nível de depuração para classes de campanha no AEM também pode ajudar a solucionar problemas.

## Se a conexão falhar {#when-the-connection-fails}

Verifique se você configurou o **`aemserver`** operador no Adobe Campaign Classic.

## Se as imagens não forem exibidas no console do Adobe Campaign Classic {#if-images-do-not-appear-in-the-adobe-campaign-console}

Verifique a fonte do HTML e confirme se você pode abrir o URL da máquina cliente. Se o URL tiver `localhost:4503` nele, altere a configuração do Day CQ Link Externalizer na instância do autor do AEM. Faça com que ele aponte para uma instância de publicação que possa ser acessada no computador do console do Adobe Campaign Classic.

Consulte [Configurar o externalizador.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## Se não conseguir se conectar do AEM ao Adobe Campaign Classic  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Procure a seguinte mensagem de erro no Adobe Campaign Classic.

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

Para corrigir esse problema, altere o seguinte no `$CAMPAIGN_HOME/conf/config-<instance-name>.xml`:

* `<dataStore hosts="*" lang="en_GB">`

## Se nenhum dado for exibido na caixa de diálogo do Adobe Campaign Classic {#if-no-data-displays-in-the-adobe-campaign-dialog}

No Adobe Campaign Classic, verifique se você não tem nenhuma barra à direita (`/`) após o número da porta.

![Adobe Campaign Classic - certifique-se de que não haja barra à direita após o número da porta](assets/chlimage_1-149.png)

## Se você receber um aviso sobre setlocale {#if-you-get-a-warning-about-your-setlocale}

Ao iniciar o serviço Apache HTTPD para Adobe Campaign Classic, você pode ver o erro `Warning: setlocale: LC_CTYPE cannot change locale`

Verifique se você tem `en_CA.ISO-8859-15 locale` instalado no servidor do Adobe Campaign Classic.

* É possível verificar se ele está instalado usando `local -a`.
* Se não estiver instalado, você poderá corrigir o `/usr/local/neolane/nl6/env.sh` script e altere o local para um local instalado.

## Se você receber um erro ao compilar o script &quot;get_nms_amcGetSeedMetaData_jssp&quot; {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

Se você vir a seguinte mensagem de erro no arquivo de log do AEM:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Use a seguinte solução alternativa no servidor do Adobe Campaign Classic.

1. Abrir arquivo `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. Modificar linha 467 do método `amcGetSeedMetaData`
1. Alterar `label : [inclView.@label](mailto:inclView.@label)` para `label : String([inclView.@label](mailto:inclView.@label))`
1. Salvar.
1. Reinicie o servidor.

## Se o Adobe Campaign Classic exibir um erro ao clicar no botão Sincronizar {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Ao clicar no link **Sincronizar** no Adobe Campaign Classic, você pode ver o seguinte erro.

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

Para corrigir esse problema, verifique se o URL de conexão AEM está configurado no **Contas externas** no Adobe Campaign Classic pode ser acessado no computador.

Um switch de `localhost` para um endereço IP para o URL geralmente pode resolver esse problema.

## Se você receber um erro &quot;Não é possível analisar data+hora XTK&quot; {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

Depois de clicar em **Sincronizar** no AEM, você pode receber um erro informando que ocorreu um script nas páginas.

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

Esse erro acontece se houver informações desatualizadas do Adobe Campaign Classic na instância AEM. Você pode resolver esse problema fazendo o seguinte:

1. Remova todas as configurações de integração do Adobe Campaign Classic que estão no AEM.
1. Recrie a integração.
1. Criar um modelo.

## Se uma conexão com SSL exibir um erro ao configurar o Cloud Service {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

Envie um tíquete com a equipe de suporte da Adobe Campaign se você vir o seguinte na `error.log` do AEM.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## Se você vir HTTP em vez dos links HTTPS esperados na caixa de diálogo de sincronização {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

Ao tentar sincronizar o conteúdo no delivery do Adobe Campaign Classic, o AEM retorna uma lista de boletins informativos. No entanto, os URLs para os boletins informativos na lista podem ser endereços HTTP em vez de HTTPS. Ocorre um erro ao selecionar um dos itens na lista. Esse erro pode ocorrer com a seguinte configuração.

* Adobe Campaign hospedado usando https para comunicação com o AEM Author
* Proxy reverso encerrando SSL
* Instância do autor no local do AEM

Para resolver esse problema, faça o seguinte:

* O Dispatcher do AEM ou o proxy reverso deve ser configurado para transmitir o protocolo original como um cabeçalho.
* A variável **Filtro SSL do serviço Apache Felix Http** na configuração do OSGi do AEM deve ser definido com as configurações de cabeçalho necessárias.
   * `https://<host>:<port>/system/console/configMgr`
   * Consulte [https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter)

## Não é possível selecionar um modelo personalizado nas propriedades da página {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Ao criar um template de email no AEM para Adobe Campaign Classic, você deve incluir a propriedade `acMapping` com o valor `mapRecipient` no `jcr:content` do modelo. Caso contrário, não será possível selecionar o modelo do Adobe Campaign Classic em **Propriedades da página** do AEM. O campo aparece desativado.

## Se você vir o erro &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; nos registros do AEM {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

Você pode ver o erro `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` nos logs AEM ao usar um modelo personalizado.

Esse erro ocorre se a variável `acMapping` estiver definida com um valor diferente de `recipient.firstName`, um valor em branco é criado no Adobe Campaign Manager.

Se esse erro ocorrer, instale o pacote de recursos 6576 para AEM do [Compartilhamento de pacotes](/help/sites-administering/package-manager.md#package-share).
