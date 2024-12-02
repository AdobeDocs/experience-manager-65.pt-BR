---
title: Desenvolvimento de proxy [!DNL Assets]
description: Um proxy é uma instância  [!DNL Experience Manager]  que usa trabalhadores proxy para processar trabalhos. Saiba como configurar um  [!DNL Experience Manager] proxy, operações com suporte, componentes proxy e como desenvolver um trabalhador proxy personalizado.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
solution: Experience Manager, Experience Manager Assets
feature: Proxy Workers
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Desenvolvimento de proxy [!DNL Assets] {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] usa um proxy para distribuir o processamento de determinadas tarefas.

Um proxy é uma instância de Experience Manager específica (e às vezes separada) que usa trabalhadores proxy como processadores responsáveis por lidar com um trabalho e criar um resultado. Um trabalhador proxy pode ser usado para uma grande variedade de tarefas. Se houver um proxy [!DNL Assets], ele poderá ser usado para carregar ativos para renderização no Assets. Por exemplo, o [trabalhador de proxy de IDS](indesign.md) usa um Servidor [!DNL Adobe InDesign] para processar arquivos para uso no Assets.

Quando o proxy é uma instância [!DNL Experience Manager] separada, isso ajuda a reduzir a carga na(s) instância(s) de criação [!DNL Experience Manager]. Por padrão, o [!DNL Assets] executa as tarefas de processamento de ativos na mesma JVM (externalizada via Proxy) para reduzir a carga na instância de criação [!DNL Experience Manager].

## Proxy (Acesso HTTP) {#proxy-http-access}

Um proxy está disponível por meio do Servlet HTTP quando configurado para aceitar trabalhos de processamento em: `/libs/dam/cloud/proxy`. Este servlet cria um trabalho sling a partir dos parâmetros publicados. Ele é adicionado à fila de trabalhos do proxy e conectado ao trabalhador proxy apropriado.

### Operações suportadas {#supported-operations}

* `job`

  **Requisitos**: o parâmetro `jobevent` deve ser definido como um mapa de valores serializados. Isto é usado para criar um `Event` para um processador de trabalho.

  **Resultado**: adiciona um novo trabalho. Se for bem-sucedido, uma ID de tarefa exclusiva será retornada.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **Requisitos**: o parâmetro `jobid` deve ser definido.

  **Resultado**: retorna uma representação JSON do Nó de resultado como criado pelo processador de trabalho.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

  **Requisitos**: a id de trabalho do parâmetro deve ser definida.

  **Resultado**: retorna um recurso associado ao trabalho especificado.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

  **Requisitos**: a id de trabalho do parâmetro deve ser definida.

  **Resultados**: remove um trabalho, se encontrado.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Worker do proxy {#proxy-worker}

Um trabalhador proxy é um processador responsável por gerenciar um trabalho e criar um resultado. Os trabalhadores residem na instância proxy e devem implementar o [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para serem reconhecidos como um trabalhador proxy.

>[!NOTE]
>
>O trabalhador deve implementar o [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconhecido como um trabalhador proxy.

### API do cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) está disponível como um serviço OSGi que fornece métodos para criar trabalhos, remover trabalhos e obter resultados desses trabalhos. A implementação padrão deste serviço (`JobServiceImpl`) usa o cliente HTTP para se comunicar com o servlet proxy remoto.

Veja a seguir um exemplo de uso da API:

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

### configurações de Cloud Service {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

As configurações de proxy e de trabalho de proxy estão disponíveis por meio das configurações de serviços em nuvem, conforme acessível no console [!DNL Assets] **Ferramentas** ou em `/etc/cloudservices/proxy`. Espera-se que cada trabalhador proxy adicione um nó sob `/etc/cloudservices/proxy` para obter detalhes de configuração específicos do trabalhador (por exemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte [Configuração de Trabalho de Proxy de InDesign Server](indesign.md#configuring-the-proxy-worker-for-indesign-server) e [Configuração de Cloud Service](../sites-developing/extending-cloud-config.md) para obter mais informações.

Veja a seguir um exemplo de uso da API:

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

### Desenvolvimento de um Worker de proxy personalizado {#developing-a-customized-proxy-worker}

O [trabalhador de proxy de IDS](indesign.md) é um exemplo de um trabalhador de proxy [!DNL Assets] que já foi fornecido pronto para uso para terceirizar o processamento de ativos de InDesign.

Você também pode desenvolver e configurar seu próprio [!DNL Assets] proxy worker para criar um worker especializado para despachar e terceirizar suas tarefas de processamento de [!DNL Assets].

Para configurar seu próprio trabalhador proxy personalizado, é necessário:

* Configurar e implementar o (usando evento Sling):

   * um tópico de trabalho personalizado
   * um manipulador de eventos de job personalizado

* Em seguida, use a API JobService para:

   * despachar seu trabalho personalizado para o proxy
   * gerenciar seu trabalho

* Se quiser usar o proxy de um fluxo de trabalho, você deve implementar uma etapa externa personalizada usando a API WorkflowExternalProcess e a API JobService.

O diagrama e as etapas a seguir detalham como proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Nas etapas a seguir, equivalentes de InDesign são indicados como exemplos de referência.

1. Um [trabalho do Sling](https://sling.apache.org/site/eventing-and-jobs.html) é usado, portanto, você precisa definir um tópico de trabalho para seu caso de uso.

   Como exemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para o trabalhador proxy de IDS.

1. A etapa externa é usada para acionar o evento e, em seguida, aguardar até que ele seja concluído; isso é feito sondando a id. Desenvolva sua própria etapa para implementar novas funcionalidades.

   Implemente um `WorkflowExternalProcess`, em seguida, use a API JobService e seu tópico de trabalho para preparar um evento de trabalho e despachá-lo para o JobService (um serviço OSGi).

   Como exemplo, consulte `INDDMediaExtractProcess`.java para o trabalhador proxy IDS.

1. Implemente um manipulador de tarefas para o tópico. Esse manipulador requer desenvolvimento para que execute sua ação específica e seja considerado a implementação do trabalhador.

   Como exemplo, consulte `IDSJobProcessor.java` para o trabalhador proxy de IDS.

1. Use `ProxyUtil.java` em dam-commons. Isso permite despachar trabalhos para trabalhadores usando o proxy DAM.

>[!NOTE]
>
>O que a estrutura proxy [!DNL Assets] não fornece pronto para uso é o mecanismo de pool.
>
>A integração [!DNL InDesign] permite o acesso de um pool de [!DNL InDesign] servidores (IDSPool). Este pool é específico à integração do [!DNL InDesign] e não faz parte da estrutura proxy [!DNL Assets].

>[!NOTE]
>
>Sincronização dos resultados:
>
>Com n instâncias usando o mesmo proxy, o resultado do processamento permanece com o proxy. É o trabalho do cliente (Experience Manager Author) solicitar o resultado usando a mesma ID de trabalho exclusiva fornecida ao cliente na criação do trabalho. O proxy simplesmente faz o trabalho e mantém o resultado pronto para ser solicitado.
