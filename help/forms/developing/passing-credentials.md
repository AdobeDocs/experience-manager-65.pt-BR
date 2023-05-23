---
title: Transmitir credenciais usando cabeçalhos de segurança WS
description: Saiba como transmitir credenciais usando cabeçalhos de segurança WS
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Transmitindo credenciais usando cabeçalhos de Segurança WS {#using-execute-script-service-aem-forms-jee-workbench}

Ao chamar um serviço AEM Forms no JEE usando serviços da Web, você pode usar cabeçalhos de segurança WS para transmitir informações de autenticação do cliente exigidas pelo AEM Forms no JEE. WS-Security define extensões SOAP para implementar autenticação de cliente, confidencialidade de mensagem e integridade de mensagem. Como resultado, você pode chamar os serviços do AEM Forms no JEE quando o AEM Forms no JEE for implantado como servidor independente ou em um ambiente em cluster.

A forma como você passa cabeçalhos de segurança WS para o AEM Forms no JEE depende de você estar usando classes Java geradas pelo Axis ou um assembly cliente .NET que consome uma pilha SOAP nativa do serviço.

>[!NOTE]
>
>Como um exemplo de chamada de um serviço usando cabeçalhos WS-Security, este tópico criptografa um documento PDF com uma senha chamando o serviço de Criptografia.

Este documento abrange os seguintes tópicos:

* Passagem da autenticação do cliente usando classes Java geradas pelo Axis

* Geração de arquivos da biblioteca do Axis necessários para chamar o serviço de criptografia

* Chamar o serviço de criptografia usando um cabeçalho WS-Security

* Passando autenticação de cliente usando um assembly de cliente .NET

* Chamar o serviço de criptografia usando um cabeçalho WS-Security


## Requisitos {#requirements}

Para aproveitar ao máximo esse documento, você precisa ter uma sólida compreensão do AEM Forms no software JEE.

>[!MORELIKETHIS]
>
>* [Transmitindo credenciais usando cabeçalhos de Segurança WS](assets/passing-credentials-using-ws-security-headers.pdf)

