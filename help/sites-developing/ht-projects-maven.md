---
title: Como criar projetos do AEM usando o Apache Maven
description: Este documento descreve como configurar um projeto do AEM com base no Apache Maven
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 15%
---
# Como criar projetos do AEM usando o Apache Maven {#how-to-build-aem-projects-using-apache-maven}

O AEM 6.5 segue as práticas recomendadas mais recentes para o gerenciamento de pacotes e a estrutura do projeto, conforme implementado pelo Arquétipo de projeto do AEM mais recente para implementações locais e do AMS.

>[!TIP]
>
>Para obter mais detalhes, consulte:
>
>* O artigo [Estrutura de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=pt-BR) na documentação do AEM as a Cloud Service sobre como estruturar projetos modernos do AEM.
>* A documentação do [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) para saber como iniciar um novo projeto do AEM usando o arquétipo.
>* O [artigo Plug-in Maven do Pacote de conteúdo do Adobe](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=pt-BR#developer-tools), na documentação do AEM as a Cloud Service, sobre como implantar aplicativos da AEM.
>
>Os três documentos se aplicam ao AEM 6.5.
