---
title: Definir configurações AEM DS
seo-title: Definir configurações AEM DS
description: Você precisa especificar o URL do servidor de processamento antes de enviar um formulário.
seo-description: Você precisa especificar o URL do servidor de processamento antes de enviar um formulário.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Definir AEM configurações do DS{#configuring-aem-ds-settings}

Este artigo descreve como configurar o **AEM Serviço de Definições do DS**. Essa configuração pode ser usada em vários cenários, por exemplo:

* Em gerenciamento de correspondência

   * Para configurar o Fluxo de trabalho do AEM Forms
   * Ao usar o portal de formulários para salvar remotamente o rascunho/envio

* Em Formulários adaptáveis para casos em que o formulário adaptável é enviado da instância de publicação

A seguir estão as etapas para configurar as **[!UICONTROL AEM Configurações do DS]**:

1. Abra o Configuration Manager na instância de publicação usando o URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configuração do Console da Web AEM](assets/web_configuration_console_new.png)

1. Na janela **[!UICONTROL Adobe Experience Manager Web Console Configuration]**, localize e clique na opção **[!UICONTROL AEM DS Settings]**.

   ![Definições do DS](assets/ds_settings_new.png)

1. A janela **[!UICONTROL AEM DS Settings Service]** exibe as definições de configuração comuns para AEM componentes DS.

   ![Serviço de Definições do DS](assets/ds_settings_service_new.png)

1. Adicione as seguintes informações nos respectivos campos:

   **[!UICONTROL URL]** do servidor de processamento: O Servidor de processamento é o servidor no qual o fluxo de trabalho do Forms ou AEM precisa ser acionado. Isso pode ser igual ao URL da instância do autor do AEM ou ao outro URL do Servidor (ou seja, https://localhost:port/).

   **[!UICONTROL Nome]** de usuário do servidor de processamento: Nome de usuário do usuário do workflow  [com base no URL do servidor que está sendo usado]

   **[!UICONTROL Senha]** do servidor de processamento: Senha do usuário do fluxo de trabalho

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Ao usar workflows do Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário configurar o serviço de configurações do DS. Caso contrário, a apresentação do formulário não será válida.


