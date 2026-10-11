---
title: Configuração do AEM Forms para enviar dados a uma AEM Forms no processo JEE
description: Integre formulários adaptáveis com o AEM Forms em processos JEE para processar dados de formulário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%
---
# Configuração do AEM Forms para enviar dados de formulário a um formulário do AEM no processo JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Os formulários adaptáveis oferecem suporte ao envio de dados para o AEM Forms no processo JEE para processamento adicional. Ele permite acionar um processo do AEM Forms no JEE com os dados disponíveis no formulário enviado. Execute as seguintes etapas para permitir que sua instância do AEM Forms envie um formulário adaptável para o processo do AEM Forms no JEE:

## Configurar o servidor do AEM Forms {#configure-your-aem-forms-server}

Execute as seguintes etapas para permitir que seu servidor do AEM Forms envie dados para uma AEM Forms no servidor JEE:

1. Vá para o console de configuração da Web do AEM em https://[*host*]:[*port*]/system/console/configMgr.

1. Localize e clique no componente **Configuração do SDK do Adobe LiveCycle Client**.
1. Clique em para editar o URL do servidor de configuração, o nome de usuário e a senha do AEM Forms no servidor JEE.
1. Revise as configurações e clique em **Salvar**.

![Configuração do Adobe LiveCycle Client SDK](assets/clientsdkconfiguration.jpg)

## Mapear dados com campos de processo {#map-data-with-process-fields}

Depois de configurar o AEM Forms, mapeie o XML de dados e os anexos do formulário enviado para os campos no processo do AEM Forms no JEE. Faça o seguinte:

1. No console de configuração da Web do AEM, clique para editar a configuração **Guia do Localizador de Processos do LiveCycle e do Chamador**.
1. Especifique os seguintes parâmetros:

   * **Nome do parâmetro xml de dados** (obrigatório): especifique o arquivo de propriedades XML do processo AEM Forms no JEE que deve processar os dados enviados. O valor padrão é **dataxml**.

   * **Nome do parâmetro de anexos de arquivo** (opcional): especifique a lista de objetos de documento que o processo do AEM Forms no JEE deve processar. O valor padrão é **fileAttachmentsList**.

1. Revise as configurações e clique em **Salvar**.

![Localizador e Invocador do Guia de Processos do LiveCycle](assets/test3.jpg)

Depois de configurada, a ação de envio Enviar para o Forms Workflow lista os processos de servidor do AEM Forms no JEE que contêm o parâmetro xml de dados especificado.
