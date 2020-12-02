---
title: Configurar a AEM Forms para enviar dados de formulário para um processo AEM Forms no JEE
seo-title: Configurar a AEM Forms para enviar dados de formulário para um processo AEM Forms no JEE
description: A AEM Forms permite integrar formulários adaptáveis com a AEM Forms em processos JEE para processamento de dados de formulários.
seo-description: A AEM Forms permite integrar formulários adaptáveis com a AEM Forms em processos JEE para processamento de dados de formulários.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Configurar a AEM Forms para enviar dados de formulário para uma AEM Forms no processo JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Os formulários adaptáveis são compatíveis com o envio de dados para um processo AEM Forms em JEE para processamento adicional. Ele permite acionar um processo AEM Forms no JEE com os dados disponíveis no formulário enviado. Execute as seguintes etapas para permitir que sua instância do AEM Forms envie um formulário adaptável para a AEM Forms no processo JEE:

## Configure seu servidor AEM Forms {#configure-your-aem-forms-server}

Execute as seguintes etapas para permitir que o servidor de formulários AEM envie dados para uma AEM Forms no servidor JEE:

1. Vá para AEM console de configuração da Web em https://[*host*]:[*port*]/system/console/configMgr.

1. Localize e clique no componente **Configuração do SDK do cliente do LiveCycle do Adobe**.
1. Clique para editar o URL do servidor de configuração, o nome de usuário e a senha do AEM Forms no servidor JEE.
1. Revise as configurações e clique em **Salvar**.

![Configuração do SDK do cliente do LiveCycle Adobe](assets/clientsdkconfiguration.jpg)

## Mapear dados com campos de processo {#map-data-with-process-fields}

Depois que o AEM Forms estiver configurado, mapeie o XML de dados e os anexos do formulário enviado para os campos no processo AEM Forms no JEE. Para fazer isso:

1. No console de configuração da Web AEM, clique para editar a configuração **Guide LiveCycle Process Locator and Invoker**.
1. Especifique os seguintes parâmetros:

   * **Nome do parâmetro**  xml de dados (obrigatório): Especifique o arquivo de propriedade XML do processo AEM Forms em JEE que precisa processar os dados enviados. O valor padrão é **dataxml**.

   * **Nome do parâmetro**  de anexos de arquivo (opcional): Especifique a lista de objetos de documento que o processo AEM Forms no JEE precisa processar. O valor padrão é **fileAttachmentsList**.

1. Revise as configurações e clique em **Salvar**.

![Localizador e Invólucro do Processo de LiveCycle do Guia](assets/test3.jpg)

Depois de configurada, a ação Enviar para envio do Forms Workflow lista  o AEM Forms no servidor JEE que contém o parâmetro xml de dados especificado.
