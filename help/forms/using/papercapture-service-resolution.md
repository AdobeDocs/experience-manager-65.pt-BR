---
title: Artigo de solução de problemas para resolver o problema quando o serviço PaperCapture falha ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) no PDF.
description: Saiba mais sobre as etapas para resolver o problema em que o serviço PaperCapture falha ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) em PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: f9e98d7de24d516eab163d42f6c1c3155915856e
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---


# O serviço PaperCature não executa a operação de OCRs em PDF

## Problema

Depois de atualizar para o AEM Forms Service Pack 6.5.21.0, a variável `PaperCapture` falha do serviço ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) no PDF. O serviço não gera saída na forma de um PDF ou um arquivo de log.

## Aplica-se a

Esta solução aplica-se a:
* AEM Forms em todos os servidores JEE (JBoss, Weblogic, Websphere)
* AEM Forms em servidores OSGi

## Solução

1. Baixe o [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0) no Portal de distribuição de software.
1. Extraia e copie o conteúdo da pasta baixada.
1. Navegue até os caminhos abaixo para os servidores de aplicativos correspondentes:
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configuração do OSGi**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Pare o servidor de aplicativos AEM.
1. Substituir o conteúdo existente do `PaperCaptureSvc` com o conteúdo copiado.
1. Reinicie o servidor de aplicativos do AEM.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
