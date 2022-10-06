---
title: Como transmitir credenciais usando cabeçalhos WS-security?
description: Saiba como transmitir credenciais usando cabeçalhos WS-security
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Transmitindo credenciais usando cabeçalhos WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Ao chamar uma AEM Forms no serviço JEE usando serviços da Web, você pode usar cabeçalhos WS-Security para passar informações de autenticação de cliente necessárias para a AEM Forms no JEE. O WS-Security define extensões SOAP para implementar autenticação de cliente, confidencialidade de mensagem e integridade de mensagem. Como resultado, você pode invocar o AEM Forms em serviços JEE quando o AEM Forms no JEE for implantado como servidor independente ou em um ambiente em cluster.

A forma como você passa cabeçalhos WS-Security para o AEM Forms no JEE depende de você estar usando classes Java geradas pelo Axis ou um assembly de cliente .NET que consome uma pilha SOAP nativa de um serviço.

>[!NOTE]
>
>Como exemplo de invocar um serviço usando cabeçalhos WS-Security, esse tópico criptografa um documento do PDF com uma senha chamando o serviço de Criptografia.

Este documento aborda os seguintes tópicos:

* Passar autenticação de cliente usando classes Java geradas pelo Axis

* Geração de arquivos de biblioteca do Axis necessários para chamar o serviço de criptografia

* Chamar o serviço de criptografia usando um cabeçalho WS-Security

* Passando autenticação de cliente usando um assembly de cliente .NET

* Chamar o serviço de criptografia usando um cabeçalho WS-Security


## Requisitos {#requirements}

Para aproveitar ao máximo esse documento, você precisa ter uma compreensão sólida do AEM Forms sobre o software JEE.

>[!MORELIKETHIS]
>
>* [Transmitindo credenciais usando cabeçalhos WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)

