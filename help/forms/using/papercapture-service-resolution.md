---
title: Artigo de solução de problemas para resolver o problema quando o serviço PaperCapture falha ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) no PDF.
description: Saiba mais sobre as etapas para resolver o problema em que o serviço PaperCapture falha ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) em PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# O PaperCature Service não executa o OCR nos PDF

## Problema

Depois de atualizar para o AEM Forms Service Pack 6.5.21.0, a variável `PaperCapture` falha do serviço ao executar operações de OCR (Optical Character Recognition, reconhecimento ótico de caracteres) no PDF. O serviço não gera saída na forma de um PDF ou um arquivo de log.

## Solução

1. Baixe o [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) no Portal de distribuição de software.
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
1. Substituir o conteúdo existente do `PaperCaptureSvc` com o conteúdo copiado.
1. [Reinicie a instância do AEM](/help/forms/using/restart-aem-sdk.md).


