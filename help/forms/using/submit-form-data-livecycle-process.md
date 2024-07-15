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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Configuração do AEM Forms para enviar dados de formulário para um formulário AEM no processo JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Os formulários adaptáveis oferecem suporte ao envio de dados para o AEM Forms no processo JEE para processamento adicional. Ele permite acionar um processo do AEM Forms no JEE com os dados disponíveis no formulário enviado. Execute as seguintes etapas para permitir que sua instância do AEM Forms envie um formulário adaptável para o processo do AEM Forms no JEE:

## Configurar o servidor do AEM Forms {#configure-your-aem-forms-server}

Execute as seguintes etapas para permitir que seu servidor do AEM Forms envie dados para uma AEM Forms no servidor JEE:

1. Vá para o console de configuração da Web do AEM em https://[*host*]:[*port*]/system/console/configMgr.

1. Localize e clique no componente **Configuração do SDK do cliente do Adobe LiveCycle**.
1. Clique em para editar o URL do servidor de configuração, o nome de usuário e a senha do AEM Forms no servidor JEE.
1. Revise as configurações e clique em **Salvar**.

![Configuração do SDK do cliente do Adobe LiveCycle](assets/clientsdkconfiguration.jpg)

## Mapear dados com campos de processo {#map-data-with-process-fields}

Depois de configurar o AEM Forms, mapeie o XML de dados e os anexos do formulário enviado para os campos no processo do AEM Forms no JEE. Faça o seguinte:

1. No console de configuração da Web do AEM, clique para editar a configuração **Localizador do Processo do LiveCycle do Guia e Chamador**.
1. Especifique os seguintes parâmetros:

   * **Nome do parâmetro xml de dados** (obrigatório): especifique o arquivo de propriedades XML do processo AEM Forms no JEE que deve processar os dados enviados. O valor padrão é **dataxml**.

   * **Nome do parâmetro de anexos de arquivo** (opcional): especifique a lista de objetos de documento que o processo do AEM Forms no JEE deve processar. O valor padrão é **fileAttachmentsList**.

1. Revise as configurações e clique em **Salvar**.

![Localizador e Chamador do Processo do LiveCycle do Guia](assets/test3.jpg)

Depois de configurada, a ação enviar para o Forms Workflow lista os processos de servidor do AEM Forms no JEE que contêm o parâmetro xml de dados especificado.
