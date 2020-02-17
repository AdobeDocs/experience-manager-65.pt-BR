---
title: Logon em fluxos de trabalho do AEM Forms
seo-title: Logon em fluxos de trabalho do AEM Forms
description: Use logs para depurar problemas de fluxo de trabalho do AEM Forms.
seo-description: Use logs para depurar problemas de fluxo de trabalho do AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Logon em fluxos de trabalho do AEM Forms{#logging-in-aem-forms-workflows}

As etapas do fluxo de trabalho do Forms fornecem registros detalhados para depurar problemas relacionados ao fluxo de trabalho de forma conveniente. Ative o registro de depuração para fluxos de trabalho do AEM Forms para exibir os registros.

Por padrão, todas as informações de registro estão disponíveis no arquivo **error.log** no diretório */crx-repository/logs/* .

Os registros de depuração para fluxos de trabalho de formulários incluem:

* Entrada de cada etapa do fluxo de trabalho. Por exemplo:\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Saída de cada etapa do fluxo de trabalho. Por exemplo:\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensagens de invocação do serviço. Por exemplo:\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensagens de saída do serviço. Por exemplo:\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variáveis lidas no mapa de metadados. Por exemplo:\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variáveis gravadas no repositório JCR. Por exemplo:

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Mensagens de exceção com rastreamento completo da pilha. Por exemplo:\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parâmetros de metadados de etapa dinâmica. Por exemplo:

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

O exemplo a seguir ilustra os registros da etapa Assinar documento:

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Use os registros para avaliar que:

* Você está usando uma configuração correta do adobe sign.
* O Adobe Sign Service sai após a criação de um contrato com êxito.
* A etapa Assinar documento sai com uma mensagem de sucesso.

Se houver uma exceção, você poderá exibir o rastreamento completo da pilha para avaliar a causa do erro.

## Ativar o registro de depuração para fluxos de trabalho do AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Execute as seguintes etapas para ativar o registro de depuração para fluxos de trabalho do AEM Forms:

1. Vá para o gerenciador de configuração do console da Web do AEM em:

   https://[server]:[port]/system/console/configMgr

1. Selecione **[!UICONTROL Sling]** > Suporte **** de registro.
1. Toque em **[!UICONTROL Adicionar novo registrador.]**
1. Selecione **[!UICONTROL Depurar]** como o Nível **[!UICONTROL de]** log.
1. Especifique o local do arquivo de log. O local padrão do arquivo de log é: *logs\error.log*
1. Especifique o nome do pacote como **com.adobe.granite.workflow.core** na coluna **[!UICONTROL Logger]** .

   A execução dessas etapas permite armazenar os logs de depuração para o pacote **com.adobe.granite.workflow.core** . Toque em **[!UICONTROL +]** e adicione os seguintes nomes de pacote à lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

