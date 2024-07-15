---
title: Definição das configurações de AEM DS
description: Saiba como especificar a URL do servidor de processamento antes de enviar um formulário.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Definição das configurações de AEM DS{#configuring-aem-ds-settings}

Este artigo descreve como configurar o **Serviço de configurações do AEM DS**. Essa configuração pode ser usada em vários cenários, por exemplo:

* No Gerenciamento de correspondência

   * Para configurar o fluxo de trabalho AEM Forms
   * Ao usar o Portal do Forms para salvar remotamente rascunhos/envios

* Em Formulários adaptáveis, para casos em que um Formulário adaptável é enviado da instância de publicação

Veja a seguir as etapas para configurar as **[!UICONTROL Configurações de AEM DS]**:

1. Abra o Configuration Manager na instância de publicação usando o URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configuração do Console da Web AEM](assets/web_configuration_console_new.png)

1. Na janela **[!UICONTROL Configuração do Adobe Experience Manager Web Console]**, localize e clique na opção **[!UICONTROL Configurações AEM do DS]**.

   ![Configurações DS](assets/ds_settings_new.png)

1. A janela **[!UICONTROL Serviço de Configurações do AEM DS]** exibe as definições de configuração comuns para Componentes AEM DS.

   ![Serviço de Configurações DS](assets/ds_settings_service_new.png)

1. Adicione as seguintes informações nos respectivos campos:

   **[!UICONTROL URL do Servidor de Processamento]**: o Servidor de Processamento é o servidor no qual o fluxo de trabalho Forms ou AEM deve ser acionado. Pode ser o mesmo que o URL da instância do autor do AEM ou o outro URL do servidor (ou seja, https://localhost:port/).

   **[!UICONTROL Nome de Usuário do Servidor de Processamento]**: Nome de Usuário do Fluxo de Trabalho [baseado na URL do servidor sendo usada]

   **[!UICONTROL Processando a senha do servidor]**: senha do usuário do fluxo de trabalho

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Ao usar workflows Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário definir o serviço de configurações do DS. Caso contrário, o envio do Formulário não terá êxito.
   >    
   >
