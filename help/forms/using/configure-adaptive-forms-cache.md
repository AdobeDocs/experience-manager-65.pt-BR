---
title: Configurar o cache de formulários adaptáveis
seo-title: Configurar o cache de formulários adaptáveis
description: 'O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente. '
seo-description: 'O cache de formulários adaptáveis foi projetado especificamente para formulários e documentos adaptáveis. Armazena em cache formulários adaptáveis e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurar o cache de formulários adaptáveis{#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache de formulários adaptáveis armazena somente o conteúdo HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente. Ele foi projetado especificamente para formulários adaptáveis e também suporta documentos adaptáveis.

>[!NOTE]
>
>Ao usar o cache de formulários adaptáveis, use o AEM Dispatcher para armazenar em cache as bibliotecas do cliente (CSS e JavaScript) de um formulário ou documento adaptável.

>[!NOTE]
>
>Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache de formulários adaptáveis desativado.

## Configurar o cache {#configure-the-cache}

Execute as seguintes etapas para configurar o cache de formulários adaptáveis:

1. Vá para o gerenciador de configuração do console da Web do AEM em https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Clique em Configuração **de Canal da Web de Formulário** Adaptável e Comunicação Interativa para editar seus valores de configuração.
1. Na caixa de diálogo Editar valores de configuração, especifique o número máximo de formulários ou documentos que uma instância do servidor de formulários AEM pode armazenar em cache no campo **Número de formulários** adaptáveis. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de formulários adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo Configuração para formulários adaptáveis cache HTML](assets/cache-configuration-edit.png)

1. Click **Save** to save the configuration.

