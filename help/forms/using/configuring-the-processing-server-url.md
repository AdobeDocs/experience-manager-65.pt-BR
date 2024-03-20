---
title: Definição das configurações de AEM DS
description: Saiba como especificar a URL do servidor de processamento antes de enviar um formulário.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Definição das configurações de AEM DS{#configuring-aem-ds-settings}

Este artigo descreve como configurar o **Serviço de Configurações do AEM DS**. Essa configuração pode ser usada em vários cenários, por exemplo:

* No Gerenciamento de correspondência

   * Para configurar o fluxo de trabalho AEM Forms
   * Ao usar o Portal do Forms para salvar remotamente rascunhos/envios

* Em Formulários adaptáveis, para casos em que um Formulário adaptável é enviado da instância de publicação

Veja a seguir as etapas para configurar o **[!UICONTROL Configurações do AEM DS]**:

1. Abra o Configuration Manager na instância de publicação usando o URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configuração do console da Web AEM](assets/web_configuration_console_new.png)

1. No **[!UICONTROL Configuração do console da Web do Adobe Experience Manager]** localize e clique na guia **[!UICONTROL Configurações do AEM DS]** opção.

   ![Configurações DS](assets/ds_settings_new.png)

1. A variável **[!UICONTROL Serviço de Configurações do AEM DS]** exibe as definições de configuração comuns para os Componentes do AEM DS.

   ![Serviço de configurações DS](assets/ds_settings_service_new.png)

1. Adicione as seguintes informações nos respectivos campos:

   **[!UICONTROL URL do servidor de processamento]**: o Servidor de processamento é o servidor no qual o workflow do Forms ou AEM deve ser acionado. Pode ser o mesmo que o URL da instância do autor do AEM ou o outro URL do servidor (ou seja, https://localhost:port/).

   **[!UICONTROL Nome de usuário do servidor de processamento]**: Nome de usuário do usuário do workflow [com base no URL do servidor que está sendo usado]

   **[!UICONTROL Senha do servidor de processamento]**: Senha do usuário do workflow

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Ao usar workflows Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário definir o serviço de configurações do DS. Caso contrário, o envio do Formulário não terá êxito.
   >    
   >
