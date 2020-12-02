---
title: Uso da API sendToPrinter
seo-title: Uso da API sendToPrinter
description: Usando o serviço sendToPrinter para enviar um documento para a impressora.
seo-description: Usando o serviço sendToPrinter para enviar um documento para a impressora.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 13%

---


# Uso da API sendToPrinter {#using-the-sendtoprinter-api}

## Visão geral {#overview}

No AEM Forms, você pode usar o serviço SendToPrinter para enviar um documento para a impressora. O serviço SendToPrinter suporta os seguintes mecanismos de acesso de impressão:

* **Impressora acessível diretamente** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Impressora acessível indiretamente** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   Ao enviar um documento para uma impressora, especifique um destes protocolos de impressão:

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**: O serviço de Saída suporta o protocolo de impressão CIFS (Common Internet File System).

## Usando o Serviço SendToPrinter {#using-sendtoprinter-service}

A tabela abaixo listas:

* informações sobre o printerName ou printServer a ser usado para vários protocolos.
* valor ou exceção que uma impressora retorna para várias combinações de URI e Nome do Servidor de Impressora

| Protocolo (mecanismo de acesso) | URI do servidor de impressão (PrinterSpec.printServer) | Nome da impressora (PrinterSpec.printerName) | Resultado |
|--- |--- |--- |--- |
| SharedPrinter | Qualquer | Vazio | Exceção: O argumento necessário sPrinterName não pode estar vazio. |
| SharedPrinter | Qualquer | Inválido | Uma exceção indica que a impressora não foi encontrada. |
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

## Suporte de autenticação {#authentication-support}

A autenticação é suportada apenas para impressão CIFS. Para autenticar, forneça o nome de usuário/senha/domínio em PrinterSpec. Você pode criptografar uma senha usando AEM Serviço CyprtoSupport Granite executando as seguintes etapas:

1. Vá para https://&lt;servidor>:&lt;porta>/sistema/console.

1. Vá para **[!UICONTROL Principal]** > **[!UICONTROL Suporte de criptografia]**.

1. Digite um texto simples e clique em **[!UICONTROL Protect]**.

