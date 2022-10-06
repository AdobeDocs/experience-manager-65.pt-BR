---
title: Logon em workflows do AEM Forms
seo-title: Logging in AEM Forms workflows
description: Use logs para depurar problemas de fluxo de trabalho do AEM Forms.
seo-description: Use logs to debug AEM Forms workflow issues.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# Logon em workflows do AEM Forms{#logging-in-aem-forms-workflows}

As etapas do fluxo de trabalho do Forms fornecem logs detalhados para depurar os problemas relacionados ao fluxo de trabalho de maneira conveniente. Ative o log de depuração para fluxos de trabalho do AEM Forms para visualizar os logs.

Por padrão, todas as informações de registro estão disponíveis na variável **error.log** no */crx-repository/logs/* diretório.

Os logs de depuração para fluxos de trabalho de formulários incluem:

* Entrada de cada etapa do fluxo de trabalho. Por exemplo:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Saída de cada etapa do fluxo de trabalho. Por exemplo:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensagens de invocação de serviço. Por exemplo:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensagens de saída do serviço. Por exemplo:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variáveis lidas no mapa de metadados. Por exemplo:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variáveis gravadas no repositório JCR. Por exemplo:

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Mensagens de exceção com rastreamento de pilha completo. Por exemplo:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parâmetros de metadados de etapas dinâmicas. Por exemplo:

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

O exemplo a seguir ilustra os logs da etapa Assinar documento:

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Use os logs para avaliar que:

* Você está usando uma configuração correta do adobe sign.
* O serviço Adobe Sign sai após a criação de um contrato com êxito.
* A etapa Assinar documento sai com uma mensagem de sucesso.

Se houver uma exceção, você poderá visualizar o rastreamento completo da pilha para avaliar a causa do erro.

## Ativar o log de depuração para workflows do AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Execute as seguintes etapas para ativar o log de depuração para workflows do AEM Forms:

1. Vá para AEM gerenciador de configuração do console da Web em:

   https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Selecionar **[!UICONTROL Sling]** > **[!UICONTROL Suporte de log]**.
1. Toque **[!UICONTROL Adicionar novo logger.]**
1. Selecionar **[!UICONTROL Depurar]** como **[!UICONTROL Nível de log]**.
1. Especifique o local do arquivo de log. O local padrão do arquivo de log é: *logs\error.log*
1. Especifique o nome do pacote como **com.adobe.granite.workflow.core** no **[!UICONTROL Logger]** coluna.

   A execução dessas etapas permite armazenar os logs de depuração do **com.adobe.granite.workflow.core** pacote. Toque **[!UICONTROL +]** e adicione os seguintes nomes de pacote à lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
