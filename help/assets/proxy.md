---
title: '"[!DNL Assets] desenvolvimento de proxy"'
description: Um proxy é um [!DNL Experience Manager] instância que usa trabalhadores proxy para processar trabalhos. Saiba como configurar um [!DNL Experience Manager] proxy, operações compatíveis, componentes de proxy e como desenvolver um trabalhador proxy personalizado.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Assets] desenvolvimento de proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] O usa um proxy para distribuir o processamento de determinadas tarefas.

Um proxy é uma instância de Experience Manager específica (e às vezes separada) que usa trabalhadores proxy como processadores responsáveis por manipular um trabalho e criar um resultado. Um trabalhador proxy pode ser usado para uma grande variedade de tarefas. No caso de um [!DNL Assets] proxy, que pode ser usado para carregar ativos para renderização no Assets. Por exemplo, a variável [Trabalhador proxy IDS](indesign.md) usa uma [!DNL Adobe InDesign] Servidor para processar arquivos para uso no Assets.

Quando o proxy é separado [!DNL Experience Manager] isso ajuda a reduzir a carga no [!DNL Experience Manager] instância(s) de criação. Por padrão, [!DNL Assets] executa as tarefas de processamento de ativos na mesma JVM (externalizada via Proxy) para reduzir a carga no [!DNL Experience Manager] instância de criação.

## Proxy (Acesso HTTP) {#proxy-http-access}

Um proxy está disponível por meio do Servlet HTTP quando está configurado para aceitar tarefas de processamento em: `/libs/dam/cloud/proxy`. Este servlet cria um trabalho de sling a partir dos parâmetros publicados. Isso é então adicionado à fila de trabalhos de proxy e conectado ao trabalhador proxy apropriado.

### Operações suportadas {#supported-operations}

* `job`

   **Requisitos**: o parâmetro `jobevent` deve ser definido como um mapa de valores serializado. Isso é usado para criar um `Event` para um processador de trabalho.

   **Resultado**: Adiciona um novo trabalho. Se bem-sucedido, uma ID de trabalho exclusiva é retornada.

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

   **Resultado**: Retorna um recurso associado ao trabalho em questão.

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

### Trabalhador Proxy {#proxy-worker}

Um trabalhador proxy é um processador responsável por manipular uma tarefa e criar um resultado. Os trabalhadores residem na instância proxy e devem implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconhecido como um trabalhador proxy.

>[!NOTE]
>
>O trabalhador deve implementar [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) para ser reconhecido como um trabalhador proxy.

### API do cliente {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) O está disponível como um serviço OSGi que fornece métodos para criar trabalhos, remover trabalhos e obter resultados desses trabalhos. A implementação padrão deste serviço (`JobServiceImpl`) usa o cliente HTTP para se comunicar com o servlet proxy remoto.

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

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

As configurações do proxy e do trabalhador proxy estão disponíveis por meio das configurações dos serviços em nuvem como acessíveis na [!DNL Assets] **Ferramentas** ou em `/etc/cloudservices/proxy`. Espera-se que cada trabalhador proxy adicione um nó em `/etc/cloudservices/proxy` para detalhes de configuração específicos do trabalhador (por exemplo, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Consulte [Configuração do InDesign Server Proxy Worker](indesign.md#configuring-the-proxy-worker-for-indesign-server) e [Configuração do Cloud Services](../sites-developing/extending-cloud-config.md) para obter mais informações.

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

### Desenvolvendo um trabalhador proxy personalizado {#developing-a-customized-proxy-worker}

O [Trabalhador proxy IDS](indesign.md) é um exemplo de um [!DNL Assets] trabalhador proxy que já foi fornecido pronto para uso para terceirizar o processamento de ativos do InDesign.

Você também pode desenvolver e configurar seus próprios [!DNL Assets] trabalhador proxy para criar um trabalhador especializado para despachar e terceirizar [!DNL Assets] tarefas de processamento.

Configurar seu próprio trabalho proxy personalizado requer:

* Configurar e implementar (usando o evento Sling):

   * um tópico de tarefa personalizada
   * um manipulador de evento de trabalho personalizado

* Em seguida, use a API JobService para:

   * despache seu trabalho personalizado para o proxy
   * gerencie seu trabalho

* Se quiser usar o proxy de um workflow, é necessário implementar uma etapa externa personalizada usando a API WorkflowExternalProcess e a API JobService.

O diagrama e as etapas a seguir detalham como proceder:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Nas etapas a seguir, os equivalentes de InDesign são indicados como exemplos de referência.

1. A [Trabalho Sling](https://sling.apache.org/site/eventing-and-jobs.html) é usado, portanto, é necessário definir um tópico de trabalho para seu caso de uso.

   Como exemplo, consulte `IDSJob.IDS_EXTENDSCRIPT_JOB` para o trabalhador proxy IDS.

1. A etapa externa é usada para acionar o evento e, em seguida, aguardar até que isso seja concluído; isso é feito pesquisando a id. Você deve desenvolver sua própria etapa para implementar novas funcionalidades.

   Implementar um `WorkflowExternalProcess`, use a API JobService e o tópico do trabalho para preparar um evento de trabalho e enviá-lo para o JobService (um serviço OSGi).

   Como exemplo, consulte `INDDMediaExtractProcess`.java para o trabalhador proxy IDS.

1. Implemente um manipulador de trabalho para seu tópico. Esse manipulador requer desenvolvimento para executar sua ação específica e é considerado a implementação do trabalhador.

   Como exemplo, consulte `IDSJobProcessor.java` para o trabalhador proxy IDS.

1. Utilizar `ProxyUtil.java` em dam-commons. Isso permite despachar trabalhos para trabalhadores usando o proxy dam.

>[!NOTE]
>
>O que [!DNL Assets] a estrutura de proxy não fornece o mecanismo de pool pronto para uso.
>
>O [!DNL InDesign] a integração permite o acesso de um pool de [!DNL InDesign] servidores (IDSPool). Esse pooling é específico para [!DNL InDesign] integração e não parte do [!DNL Assets] estrutura de proxy.

>[!NOTE]
>
>Sincronização dos resultados:
>
>Com n instâncias usando o mesmo proxy, o resultado do processamento permanece com o proxy. É tarefa do cliente (Autor do Experience Manager) solicitar o resultado usando a mesma id de trabalho exclusiva fornecida ao cliente na criação de emprego. O proxy simplesmente faz o trabalho e mantém o resultado pronto para ser solicitado.
