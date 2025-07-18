---
title: Logs
description: Saiba como configurar parâmetros globais para o serviço de log central, configurações específicas para serviços individuais ou como solicitar o registro de dados.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Logs{#logging}

O AEM oferece a possibilidade de configurar:

* parâmetros globais para o serviço de log central
* registro de dados de solicitação; uma configuração de registro especializada para informações de solicitação
* definições específicas para os serviços individuais; por exemplo, um arquivo de log individual e o formato para as mensagens de log

Estas são todas as [configurações de OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>O logon no AEM é baseado nos princípios do Sling. Consulte [Sling Logging](https://sling.apache.org/site/logging.html) para obter mais informações.

## Log global {#global-logging}

A [Configuração de log do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) é usada para configurar o agente raiz. Isso define as configurações globais para fazer logon no AEM:

* o nível de registro
* o local do arquivo de log central
* número de versões a manter
* rotação de versão; tamanho máximo ou um intervalo de tempo
* o formato a ser usado ao gravar as mensagens de log

## Registradores e Gravadores para Serviços Individuais {#loggers-and-writers-for-individual-services}

Além das configurações de registro global, o AEM permite definir configurações específicas para um serviço individual:

* o nível de registro específico
* o local do arquivo de log individual
* número de versões a manter
* rotação de versão; tamanho máximo ou intervalo de tempo
* o formato a ser usado ao gravar as mensagens de log
* o logger (o serviço OSGi que fornece as mensagens de log)

Isso permite canalizar mensagens de log de um único serviço em um arquivo separado. Isso pode ser particularmente útil durante o desenvolvimento ou o teste; por exemplo, quando você precisa de um nível de log maior para um serviço específico.

O AEM usa o seguinte para gravar mensagens de log no arquivo:

1. Um **serviço OSGi** (agente de log) grava uma mensagem de log.
1. Um **Logger** pega essa mensagem e a formata de acordo com sua especificação.
1. Um **Gravador de Log** grava todas essas mensagens no arquivo físico definido.

Esses elementos estão vinculados pelos seguintes parâmetros para os elementos apropriados:

* **Agente (Agente de Log)**

  Defina os serviços que geram as mensagens.

* **Arquivo de Log (Agente de Log)**

  Defina o arquivo físico para armazenar as mensagens de log.

  Isso é usado para vincular um Logger de Log a um Gravador de Log. O valor deve ser idêntico ao mesmo parâmetro na configuração do Gravador de Log para que a conexão seja estabelecida.

* **Arquivo de Log (Gravador de Log)**

  Defina o arquivo físico no qual as mensagens de log serão gravadas.

  Deve ser idêntico ao mesmo parâmetro na configuração do Gravador de log, caso contrário, a correspondência não será feita. Se não houver correspondência, um Gravador implícito será criado com a configuração padrão (rotação diária de log).

### Registradores e gravadores padrão {#standard-loggers-and-writers}

Alguns registradores e gravadores estão incluídos em uma instalação padrão do AEM.

O primeiro é um caso especial, pois controla os arquivos `request.log` e `access.log`:

* O logger:

   * Agente de dados de solicitação personalizável do Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Gravar mensagens sobre o conteúdo da solicitação em `request.log`.

* Links para:

   * Logger de solicitação do Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Grava as mensagens em `request.log` ou `access.log`.

Eles podem ser personalizados, se necessário, embora a configuração padrão seja adequada para a maioria das instalações.

Os outros pares seguem a configuração padrão:

* O logger:

   * Configuração do logger de log do Apache Sling

     (org.apache.sling.commons.log.LogManager.fatory.config)

   * Grava `Information` mensagens em `logs/error.log`.

* Links para o autor:

   * Configuração do Apache Sling Logging Writer

     (org.apache.sling.commons.log.LogManager.fatory.writer)

* O logger:

   * Configuração do logger de log do Apache Sling
(org.apache.sling.commons.log.LogManager.fatory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Grava `Warning` mensagens em `../logs/error.log` para o serviço `org.apache.pdfbox`.

* Não vincula a um Gravador específico, portanto, criará e usará um Gravador implícito com configuração padrão (rotação diária de log).

### Criar seus próprios registradores e gravadores {#creating-your-own-loggers-and-writers}

Você pode definir seu próprio par de Logger/Gravador:

1. Crie uma instância da Configuração de Fábrica [Configuração do Agente de Log do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique o Arquivo de log.
   1. Especifique o Logger.
   1. Configure os outros parâmetros conforme necessário.

1. Crie uma instância da Configuração de Fábrica [Configuração de Gravador de Log do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique o Arquivo de log - deve corresponder ao especificado para o Logger.
   1. Configure os outros parâmetros conforme necessário.

>[!NOTE]
>
>Em determinadas circunstâncias, talvez você queira criar um [arquivo de log personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
