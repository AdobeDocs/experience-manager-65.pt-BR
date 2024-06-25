---
title: Fazer logon em workflows do AEM Forms
description: Saiba como depurar problemas de fluxo de trabalho do AEM Forms e habilitar o log de depuração para fluxos de trabalho do AEM Forms para visualizar os logs.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---

# Fazer logon em workflows do AEM Forms{#logging-in-aem-forms-workflows}

As etapas de Forms Workflow fornecem registros detalhados para depurar problemas relacionados ao fluxo de trabalho convenientemente. Habilite o log de depuração para workflows do AEM Forms para visualizar os logs.

Por padrão, todas as informações de registro estão disponíveis no **error.log** arquivo no */crx-repository/logs/* diretório.

Os logs de depuração para workflows de formulários incluem:

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

* Parâmetros de metadados de etapa dinâmicos. Por exemplo:

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

Use os logs para avaliar se:

* Você está usando uma configuração correta do Adobe Sign.
* O Serviço Adobe Sign é encerrado após a criação bem-sucedida de um contrato.
* A etapa Assinar documento sai com uma mensagem de sucesso.

Se houver uma exceção, você poderá exibir o rastreamento de pilha completo para avaliar a causa do erro.

## Habilitar log de depuração para workflows do AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Faça o seguinte para ativar o log de depuração para workflows do AEM Forms:

1. Vá para o gerenciador de configuração do console da Web do AEM em:

   https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Selecionar **[!UICONTROL Sling]** > **[!UICONTROL Suporte de registro]**.
1. Selecionar **[!UICONTROL Adicionar novo logger.]**
1. Selecionar **[!UICONTROL Depurar]** como o **[!UICONTROL Nível de registro]**.
1. Especifique o local do arquivo de log. O local padrão para o arquivo de log é: *logs\error.log*
1. Especifique o nome do pacote como **com.adobe.granite.workflow.core** no **[!UICONTROL Logger]** coluna.

   A execução dessas etapas permite armazenar os logs de depuração da **com.adobe.granite.workflow.core** pacote. Selecionar **[!UICONTROL +]** e adicione os seguintes nomes de pacote à lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
