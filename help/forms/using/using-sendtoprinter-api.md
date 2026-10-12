---
title: Uso da API sendToPrinter
description: Uso do serviço sendToPrinter para enviar um documento à impressora.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,APIs & Integrations
exl-id: 585d4053-1056-4d2b-a9df-9516775afe50
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%
---
# Uso da API sendToPrinter {#using-the-sendtoprinter-api}

## Visão geral {#overview}

No AEM Forms, você pode usar o serviço SendToPrinter para enviar um documento para a impressora. O serviço SendToPrinter oferece suporte aos seguintes mecanismos de acesso de impressão:

* **Impressora acessível diretamente** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Impressora acessível indiretamente** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  Ao enviar um documento para uma impressora, especifique um destes protocolos de impressão:

  * **XÍCARAS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
  * **DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
  * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
  * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
  * **CIFS**: o serviço de saída oferece suporte ao protocolo de impressão CIFS (Common Internet File System).

## Uso do Serviço SendToPrinter {#using-sendtoprinter-service}

A tabela abaixo lista:

* informações sobre printerName ou printServer a serem usadas para vários protocolos.
* valor ou exceção que uma impressora retorna para várias combinações de URI do Servidor de Impressoras e Nome da impressora

| Protocolo (mecanismo de acesso) | URI do Servidor de Impressão (PrinterSpec.printServer) | Nome da impressora (PrinterSpec.printerName) | Resultado |
|--- |--- |--- |--- |
| SharedPrinter | Qualquer | Vazio | Exceção: o argumento obrigatório sPrinterName não pode estar vazio. |
| SharedPrinter | Qualquer | Inválido | Uma exceção indica que a impressora não pode ser encontrada. |
| SharedPrinter | Qualquer | Válido | Trabalho de impressão bem-sucedido. |
| LPD | Vazio | Qualquer | uma exceção informando que o argumento necessário sPrintServerUri não pode estar vazio. |
| LPD | Inválido | Vazio | uma exceção informando que o argumento necessário sPrinterName não pode estar vazio. |
| LPD | Inválido | Não vazio | uma exceção informando que sPrintServerUri não foi encontrada. |
| LPD | Válido | Inválido | uma exceção informando que a impressora não pode ser encontrada. |
| LPD | Válido | Válido | Um trabalho de impressão bem-sucedido. |
| CUPS | Vazio | Qualquer | uma exceção informando que o argumento necessário sPrintServerUri não pode estar vazio. |
| CUPS | Inválido | Qualquer | uma exceção informando que a impressora não pode ser encontrada. |
| CUPS | Válido | Qualquer | Trabalho de impressão bem-sucedido. |
| DirectIP | Vazio | Qualquer | uma exceção informando que o argumento necessário sPrintServerUri não pode estar vazio. |
| DirectIP | Inválido | Qualquer | uma exceção informando que a impressora não pode ser encontrada. |
| DirectIP | Válido | Qualquer | Trabalho de impressão bem-sucedido. |
| CIFS | Válido | Vazio | Trabalho de impressão bem-sucedido. |
| CIFS | Inválido | Qualquer | erro desconhecido ao imprimir usando CIFS. |
| CIFS | Vazio | Qualquer | uma exceção informando que o argumento necessário sPrintServerUri não pode estar vazio. |

## Suporte à autenticação {#authentication-support}

A autenticação é suportada somente para impressão CIFS. Para autenticar, forneça o nome de usuário/senha/domínio em PrinterSpec. Você pode criptografar uma senha usando o Serviço de Suporte do Chip no AEM Granite executando as seguintes etapas:

1. Acesse https://&lt;server>:&lt;port>/system/console.

1. Vá para **[!UICONTROL Principal]** > **[!UICONTROL Suporte de Criptografia]**.

1. Insira um texto sem formatação e clique em **[!UICONTROL Proteger]**.
