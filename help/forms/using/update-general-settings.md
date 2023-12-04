---
title: Atualização de configurações gerais
seo-title: Updating general settings
description: Atualize as configurações do aplicativo AEM Forms, como a tela inicial, e busque as opções de pontos iniciais e anexos
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Atualização de configurações gerais{#updating-general-settings}

As configurações gerais do aplicativo AEM Forms permitem especificar configurações como busca de anexos, modo offline, tela de aterrissagem, categoria padrão e frequência de salvamento automático.

## Atualização das Configurações gerais no aplicativo {#working-with-the-form}

Ao sincronizar o aplicativo com o servidor do AEM Forms, todos os formulários e tarefas definidas são baixados para o dispositivo móvel.

A solução de aplicativo pronta para uso do AEM Forms não baixa os anexos associados a cada formulário quando o aplicativo é sincronizado.

Na guia General, altere as configurações de download de anexos, modo offline, tela de aterrissagem, salvamento automático e sincronização. Você pode alterar a [Tela inicial](../../forms/using/home-screen.md) do seu aplicativo.

**Acesse a guia Geral na tela Configurações**

1. Para ir até a tela Configuração, selecione o botão Menu no canto superior esquerdo da tela inicial e clique em Selecionar **Configurações**.
1. Na tela Settings, selecione a guia General.

   ![Configurações gerais no aplicativo AEM Forms](assets/gen-settings-1.png)

   tela Configurações gerais

   >[!NOTE]
   >
   >As opções podem ser exibidas de forma diferente em diferentes dispositivos móveis.

### Configurações gerais {#general-settings}

Você pode fazer as seguintes alterações nas configurações do seu aplicativo.

* **Buscar anexos da tarefa**: para especificar se os anexos associados devem ser baixados quando cada tarefa for baixada no aplicativo.
* **Modo offline**: para ativar ou desativar o serviço offline para o aplicativo AEM Forms. Consulte [Trabalhar no modo offline](/help/forms/using/work-offline-mode.md) para obter detalhes.
* **Landing screen**: Para definir o local inicial ([Tela inicial](../../forms/using/home-screen.md)) para o aplicativo.
Opções disponíveis:

   * Forms
   * Tarefas
   * Favoritos

* **Categoria padrão**: permite selecionar a categoria de formulários para mostrar na tela inicial. Ao selecionar Tudo, você pode ver todos os formulários na tela inicial. As categorias são preenchidas com base nos formulários carregados no aplicativo. Os Forms estão disponíveis no aplicativo com base nas configurações de formulário especificadas no servidor do AEM Forms.

* **Frequência de salvamento automático**: Para definir a frequência com que seus [o aplicativo móvel salva dados de formulário](../../forms/using/autosave-data-app.md) localmente.
* **Frequência de sincronização**: Para definir a frequência com que seus [o aplicativo móvel está sincronizado](../../forms/using/sync-app.md) com o servidor do AEM Forms no modo online.
  **Limpar dados locais**: limpe o banco de dados, incluindo as configurações e os dados locais para todos os usuários e o armazenamento de arquivos do dispositivo.

>[!NOTE]
>
>Limpar o cache encerra sua sessão imediatamente no aplicativo.
>
>No entanto, você será solicitado a confirmar a operação de limpeza do cache.
