---
title: Configuração do AEM Forms para enviar dados de formulário a uma AEM Forms no processo JEE
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: O AEM Forms permite integrar formulários adaptáveis com o AEM Forms em processos JEE para processar dados de formulário.
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Configuração do AEM Forms para enviar dados de formulário a uma AEM Forms no processo JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Os formulários adaptáveis oferecem suporte ao envio de dados para um processo AEM Forms no JEE para processamento adicional. Ela permite acionar um processo do AEM Forms no JEE com os dados disponíveis no formulário enviado. Execute as seguintes etapas para permitir que sua instância do AEM Forms envie um formulário adaptável para o AEM Forms no processo JEE:

## Configurar o servidor do AEM Forms {#configure-your-aem-forms-server}

Execute as seguintes etapas para permitir que o servidor de formulários AEM envie dados para uma AEM Forms no servidor JEE:

1. Acesse o console de configuração da Web do AEM em https://[*host*]:[*porta*]/system/console/configMgr

1. Localize e clique no link **Configuração do SDK do cliente do LiveCycle Adobe** componente.
1. Clique em para editar o URL do servidor de configuração, o nome de usuário e a senha do AEM Forms no servidor JEE.
1. Revise as configurações e clique em **Salvar**.

![Configuração do SDK do cliente do LiveCycle Adobe](assets/clientsdkconfiguration.jpg)

## Mapear dados com campos de processo {#map-data-with-process-fields}

Depois que o AEM Forms estiver configurado, mapeie o XML de dados e os anexos do formulário enviado para os campos no processo do AEM Forms no JEE. Para fazer isso:

1. No console de configuração da Web do AEM, clique em para editar a variável **Localizador e Chamador do Processo do LiveCycle do Guia** configuração.
1. Especifique os seguintes parâmetros:

   * **Nome do parâmetro xml de dados** (obrigatório): especifique o arquivo de propriedade XML do processo AEM Forms no JEE que precisa processar os dados enviados. O valor padrão é **dataxml**.

   * **Nome do parâmetro de anexos de arquivo** (opcional): especifique a lista de objetos de documento que o processo do AEM Forms no JEE precisa processar. O valor padrão é **fileAttachmentsList**.

1. Revise as configurações e clique em **Salvar**.

![Localizador e Chamador do Processo do LiveCycle do Guia](assets/test3.jpg)

Depois de configurada, a ação enviar para o Forms Workflow lista os processos de servidor do AEM Forms no JEE que contêm o parâmetro xml de dados especificado.
