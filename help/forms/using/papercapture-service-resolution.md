---
title: Artigo de solução de problemas para resolver o problema de falha do serviço PaperCapture ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) em PDFs.
description: Saiba mais sobre as etapas para resolver o problema em que o serviço PaperCapture falha ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) em PDFs.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%
---

# O serviço PaperCature não executa a operação de OCRs em PDFs

## Problema

Depois de atualizar para o AEM Forms Service Pack 6.5.21.0 ou o AEM Forms Service Pack 6.5.22.0, o serviço `PaperCapture` falha ao executar operações de OCR (Reconhecimento Ótico de Caracteres) em PDFs. O serviço não gera saída na forma de um PDF ou um arquivo de log.

## Aplica-se a

Esta solução aplica-se a:

* AEM Forms em todos os servidores JEE (JBoss, Weblogic, Websphere)
* AEM Forms em servidores OSGi

## Solução

1. Baixe o [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0) do Portal de Distribuição de Software.
1. Extraia e copie o conteúdo da pasta baixada.
1. Navegue até os caminhos abaixo para os servidores de aplicativos correspondentes:
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configuração OSGi**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Pare o servidor de aplicativos do AEM.
1. Substituir o conteúdo existente da pasta `PaperCaptureSvc` pelo conteúdo copiado.
1. Reinicie o servidor de aplicativos do AEM.

   >[!NOTE]
   >
   > É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
