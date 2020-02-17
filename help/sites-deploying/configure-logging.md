---
title: Registro
seo-title: Registro
description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
seo-description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Registro{#logging}

O AEM oferece a possibilidade de configurar:

* parâmetros globais para o serviço central de registro
* solicitar o registro de dados; uma configuração de registro especializada para informações de solicitação
* definições específicas para cada serviço; por exemplo, um arquivo de log individual e um formato para as mensagens de log

Estas são todas configurações [](/help/sites-deploying/configuring-osgi.md)OSGi.

>[!NOTE]
>
>Fazer logon no AEM é baseado nos princípios do Sling. Consulte [Sling Logging](https://sling.apache.org/site/logging.html) para obter mais informações.

## Registro global {#global-logging}

[A Configuração](/help/sites-deploying/osgi-configuration-settings.md) de registro do Apache Sling é usada para configurar o agente de registro raiz. Isso define as configurações globais para logon no AEM:

* nível de registro
* a localização do ficheiro de registro central
* o número de versões a conservar
* rotação de versões; tamanho máximo ou intervalo de tempo
* o formato a ser usado ao gravar mensagens de registro

>[!NOTE]
>
>Este artigo [da](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) Base de conhecimento explica como girar os arquivos request.log e access.log.

## Registradores e Escritores para Serviços Individuais {#loggers-and-writers-for-individual-services}

Além das configurações globais de registro, o AEM permite que você defina configurações específicas para um serviço individual:

* nível de registro específico
* o local do arquivo de log individual
* o número de versões a conservar
* rotação de versões; tamanho máximo ou intervalo de tempo
* o formato a ser usado ao gravar mensagens de registro
* o agente de log (o serviço OSGi que fornece as mensagens de log)

Isso permite que você canalize mensagens de log de um único serviço em um arquivo separado. Isto pode ser particularmente útil durante o desenvolvimento ou testes; por exemplo, quando você precisa de um nível de log aumentado para um serviço específico.

O AEM usa o seguinte para gravar mensagens de registro no arquivo:

1. Um serviço **** OSGi (logger) grava uma mensagem de registro.
1. Um **Logging Logger** pega essa mensagem e a formata de acordo com sua especificação.
1. Um Gravador **de** log grava todas essas mensagens no arquivo físico que você definiu.

Estes elementos estão ligados pelos seguintes parâmetros para os elementos apropriados:

* **Logger (Logging Logger)**

   Defina os serviços que geram as mensagens.

* **Arquivo de log (registrador de log)**

   Defina o arquivo físico para armazenar as mensagens de log.

   Isso é usado para vincular um Logging Logger a um Logging Writer. O valor deve ser idêntico ao mesmo parâmetro na configuração do Gravador de log para que a conexão seja feita.

* **Arquivo de log (Gravador de log)**

   Defina o arquivo físico para o qual as mensagens de log serão gravadas.

   Isso deve ser idêntico ao mesmo parâmetro na configuração do Gravador de log, ou a correspondência não será feita. Se não houver correspondência, um Escritor implícito será criado com a configuração padrão (rotação diária do log).

### Registradores e escritores padrão {#standard-loggers-and-writers}

Alguns registradores e gravadores estão incluídos em uma instalação padrão do AEM.

O primeiro é um caso especial, pois controla os arquivos `request.log` e `access.log` :

* O Registrador:

   * Registrador de Dados de Solicitação Personalizável do Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Gravar mensagens sobre o conteúdo da solicitação para `request.log`.

* Links para:

   * Registro de solicitação Sling do Apache

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Grava as mensagens em `request.log` ou `access.log`.

Eles podem ser personalizados se necessário, embora a configuração padrão seja adequada para a maioria das instalações.

Os outros pares seguem a configuração padrão:

* O Registrador:

   * Configuração do Apache Sling Logging Logger

      (org.apache.sling.commons.log.LogManager.fatory.config)

   * Grava `Information` mensagens em `logs/error.log`.

* Links para o Escritor:

   * Configuração do Apache Sling Logging Writer

      (org.apache.sling.commons.log.LogManager.fatory.writer)

* O Registrador:

   * Configuração do Apache Sling Logging Logger (org.apache.sling.commons.log.LogManager.fatory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Grava `Warning` mensagens para `../logs/error.log` o serviço `org.apache.pdfbox`.

* Não vincula a um Escritor específico, portanto, criará e usará um Escritor implícito com configuração padrão (rotação diária do log).

### Criando seus próprios registradores e escritores {#creating-your-own-loggers-and-writers}

Você pode definir seu próprio par de Registrador/Escritor:

1. Crie uma nova instância da Configuração de fábrica Configuração do [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique o arquivo de log.
   1. Especifique o registrador.
   1. Configure os outros parâmetros conforme necessário.

1. Crie uma nova instância da Configuração de fábrica Configuração do [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especificar o arquivo de log - deve corresponder ao especificado para o Logger.
   1. Configure os outros parâmetros conforme necessário.

>[!NOTE]
>
>Em determinadas circunstâncias, talvez você queira criar um arquivo [de log](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)personalizado.

