---
title: Desenvolvimento proxy de ativos
description: Um proxy é uma instância do Experience Manager que usa trabalhadores proxy para processar trabalhos. Saiba como configurar um proxy do Experience Manager, operações suportadas, componentes proxy e como desenvolver um representante personalizado.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---


# Desenvolvimento proxy de ativos {#assets-proxy-development}

O Adobe Experience Manager Assets usa um proxy para distribuir o processamento de determinadas tarefas.

Um proxy é uma instância específica (e, às vezes, separada) do Experience Manager que usa os funcionários proxy como processadores responsáveis por manipular um trabalho e criar um resultado. Um funcionário proxy pode ser usado para uma grande variedade de tarefas. No caso de um proxy de Ativos, isso pode ser usado para carregar ativos para renderização dentro de Ativos. Por exemplo, o trabalho [proxy](indesign.md) IDS usa um [!DNL Adobe InDesign] Servidor para processar arquivos para uso no Assets.

Quando o proxy é uma instância separada do Experience Manager, isso ajuda a reduzir a carga nas instâncias de criação do Experience Manager. Por padrão, o Assets executa as tarefas de processamento de ativos na mesma JVM (externalizada via Proxy) para reduzir a carga na instância de criação do Experience Manager.

## Proxy (Acesso HTTP) {#proxy-http-access}

Um proxy está disponível via Servlet HTTP quando está configurado para aceitar trabalhos de processamento em: `/libs/dam/cloud/proxy`. Este servlet cria um trabalho sling a partir dos parâmetros publicados. Isso é adicionado à fila de trabalhos proxy e conectado ao trabalhador proxy apropriado.

### Operações suportadas {#supported-operations}

* `job`

   **Requisitos**: o parâmetro `jobevent` deve ser definido como um mapa de valores serializado. Isso é usado para criar um `Event` para um processador de trabalho.

   **Resultado**: Adiciona um novo trabalho. Se bem-sucedido, uma ID de trabalho exclusiva será retornada.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisitos**: o parâmetro `jobid` deve ser definido.

   **Resultado**: Retorna uma representação JSON do Nó de resultado, conforme criado pelo processador de trabalho.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Requisitos**: o parâmetro jobid deve ser definido.

   **Resultado**: Retorna um recurso associado ao trabalho especificado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Requisitos**: o parâmetro jobid deve ser definido.

   **Resultados**: Remove um trabalho, se encontrado.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

Um trabalhador proxy é um processador responsável por manipular um trabalho e criar um resultado. Os funcionários residem na instância proxy e devem implementar o [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para serem reconhecidos como um trabalhador proxy.

>[!NOTE]
>
>O trabalhador deve implementar o [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconhecido como um trabalhador proxy.

### API do cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) está disponível como um serviço OSGi que fornece métodos para criar trabalhos, remover trabalhos e obter resultados desses trabalhos. A implementação padrão deste serviço (`JobServiceImpl`) usa o cliente HTTP para se comunicar com o servlet proxy remoto.

Este é um exemplo de uso da API:

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Configurações do Cloud Service {#cloud-service-configurations}

>[!NOTE]
>
>A documentação de referência da API de proxy está disponível em [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

As configurações de proxy e de trabalho proxy estão disponíveis por meio de configurações de serviços em nuvem, conforme acessado pelo console **Ferramentas** de ativos ou em `/etc/cloudservices/proxy`. Espera-se que cada representante adicione um nó em `/etc/cloudservices/proxy` para detalhes de configuração específicos do trabalhador (por exemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte Configuração [do](indesign.md#configuring-the-proxy-worker-for-indesign-server) InDesign Server Proxy Worker e configuração [do](../sites-developing/extending-cloud-config.md) Cloud Services para obter mais informações.

Este é um exemplo de uso da API:

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Desenvolvendo um representante personalizado {#developing-a-customized-proxy-worker}

O trabalho [proxy do](indesign.md) IDS é um exemplo de um funcionário proxy do Assets que já é fornecido prontamente para terceirizar o processamento de ativos do InDesign.

Você também pode desenvolver e configurar seu próprio funcionário proxy do Assets para criar um funcionário especializado para despachar e terceirizar suas tarefas de processamento do Assets.

A configuração de seu próprio representante personalizado requer que você:

* Configure e implemente (usando o evento Sling):

   * um tópico de trabalho personalizado
   * um manipulador de eventos de trabalho personalizado

* Em seguida, use a API JobService para:

   * despache seu trabalho personalizado para o proxy
   * gerenciar seu trabalho

* Se quiser usar o proxy de um fluxo de trabalho, você deve implementar uma etapa externa personalizada usando a API WorkflowExternalProcess e a API JobService.

O diagrama e as etapas a seguir detalham como proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Nas etapas a seguir, os equivalentes do InDesign são indicados como exemplos de referência.

1. Um trabalho [do](https://sling.apache.org/site/eventing-and-jobs.html) Sling é usado, portanto, é necessário definir um tópico de trabalho para seu caso de uso.

   Como exemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para obter o representante do IDS.

1. A etapa externa é usada para acionar o evento e, em seguida, aguardar até que ele seja concluído; isso é feito por pesquisa no id. Você deve desenvolver sua própria etapa para implementar novas funcionalidades.

   Implemente um `WorkflowExternalProcess`e, em seguida, use a API JobService e o tópico de seu trabalho para preparar um evento de trabalho e enviá-lo para o JobService (um serviço OSGi).

   Como exemplo, consulte `INDDMediaExtractProcess`.java para o trabalho proxy do IDS.

1. Implemente um gerenciador de tarefas para o seu tópico. Esse manipulador requer desenvolvimento para que execute sua ação específica e seja considerado a implementação do trabalhador.

   Como exemplo, consulte `IDSJobProcessor.java` para obter o representante do IDS.

1. Aproveite o `ProxyUtil.java` dialeto comum. Isso permite que você despache trabalhos para trabalhadores usando o proxy dam.

>[!NOTE]
>
>O que a estrutura de proxy Ativos não fornece prontamente é o mecanismo de pool.
>
>A [!DNL InDesign] integração permite o acesso de um pool de [!DNL InDesign] servidores (IDSPool). Esse pooling é específico para a [!DNL InDesign] integração e não faz parte da estrutura de [!DNL Assets] proxy.

>[!NOTE]
>
>Sincronização dos resultados:
>
>Com nenhuma instância usando o mesmo proxy, o resultado do processamento permanece com o proxy. É tarefa do cliente (Autor do Experience Manager) solicitar o resultado usando a mesma ID de trabalho exclusiva que foi fornecida ao cliente na criação de um trabalho. O proxy simplesmente faz o trabalho e mantém o resultado pronto para ser solicitado.
