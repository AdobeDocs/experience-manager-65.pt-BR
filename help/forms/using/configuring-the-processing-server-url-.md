---
title: Definição das configurações do AEM DS
seo-title: Definição das configurações do AEM DS
description: É necessário especificar o URL do servidor de processamento antes de enviar um formulário.
seo-description: É necessário especificar o URL do servidor de processamento antes de enviar um formulário.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Definição das configurações do AEM DS{#configuring-aem-ds-settings}

Este artigo descreve como configurar o Serviço **de configurações do** AEM DS. Essa configuração pode ser usada em vários cenários, por exemplo:

* No gerenciamento de correspondência

   * Para configurar o fluxo de trabalho do AEM Forms
   * Ao usar o portal de formulários para salvar remotamente o rascunho/envio

* Em Formulários adaptáveis para casos em que o formulário adaptativo é enviado da instância de publicação

Veja a seguir as etapas para configurar as configurações **[!UICONTROL do]** AEM DS:

1. Abra o Configuration Manager na instância de publicação usando o URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configuração do console da Web AEM](assets/web_configuration_console_new.png)

1. Na janela Configuração **[!UICONTROL do console da Web do]** Adobe Experience Manager, localize e clique na opção Configurações **[!UICONTROL do]** AEM DS.

   ![Configurações de DS](assets/ds_settings_new.png)

1. A janela Serviço **[!UICONTROL de configurações do]** AEM DS exibe as configurações comuns dos componentes do AEM DS.

   ![Serviço de Configurações de DS](assets/ds_settings_service_new.png)

1. Adicione as seguintes informações nos respectivos campos:

   **[!UICONTROL URL]** do servidor de processamento: O Servidor de processamento é o servidor no qual o fluxo de trabalho do Forms ou AEM precisa ser acionado. Isso pode ser igual ao URL da instância do autor do AEM ou do outro URL do servidor (ou seja, https://localhost:port/).

   **[!UICONTROL Nome]** de usuário do servidor de processamento: Nome de usuário do usuário do fluxo de trabalho [com base no URL do servidor que está sendo usado]

   **[!UICONTROL Senha]** do servidor de processamento: Senha do usuário do fluxo de trabalho

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Ao usar os fluxos de trabalho do Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário configurar o serviço de configurações do DS. Caso contrário, a apresentação do formulário não será efetuada.


