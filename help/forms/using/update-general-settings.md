---
title: Atualização de configurações gerais
description: Atualize as configurações do aplicativo AEM Forms, como a tela inicial, e busque as opções de pontos iniciais e anexos
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Atualização de configurações gerais{#updating-general-settings}

As configurações gerais do aplicativo AEM Forms permitem especificar configurações como busca de anexos, modo offline, tela de aterrissagem, categoria padrão e frequência de salvamento automático.

## Atualização das Configurações gerais no aplicativo {#working-with-the-form}

Ao sincronizar o aplicativo com o servidor do AEM Forms, todos os formulários e tarefas definidas são baixados para o dispositivo móvel.

A solução de aplicativo pronta para uso do AEM Forms não baixa os anexos associados a cada formulário quando o aplicativo é sincronizado.

Na guia General, altere as configurações de download de anexos, modo offline, tela de aterrissagem, salvamento automático e sincronização. Você pode alterar a [tela inicial](../../forms/using/home-screen.md) do seu aplicativo.

**Navegue até a guia Geral na tela Configurações**

1. Para ir para a tela Configuração, selecione o botão Menu no canto superior esquerdo da tela inicial e selecione **Configurações**.
1. Na tela Settings, selecione a guia General.

   ![Configurações gerais no aplicativo AEM Forms](assets/gen-settings-1.png)

   tela Configurações gerais

   >[!NOTE]
   >
   >As opções podem ser exibidas de forma diferente em diferentes dispositivos móveis.

### Configurações gerais {#general-settings}

Você pode fazer as seguintes alterações nas configurações do seu aplicativo.

* **Buscar anexos de tarefa**: para especificar se os anexos associados devem ser baixados quando cada tarefa for baixada no aplicativo.
* **Modo offline**: para habilitar ou desabilitar o serviço offline para o aplicativo AEM Forms. Consulte [Trabalhando no modo offline](/help/forms/using/work-offline-mode.md) para obter detalhes.
* **Tela de aterrissagem**: para definir o local de início ([Tela inicial](../../forms/using/home-screen.md)) do aplicativo.
Opções disponíveis:

   * Forms
   * Tarefas
   * Favoritos

* **Categoria padrão**: permite que você selecione a categoria de formulários a serem exibidos na tela inicial. Ao selecionar Tudo, você pode ver todos os formulários na tela inicial. As categorias são preenchidas com base nos formulários carregados no aplicativo. Os Forms estão disponíveis no aplicativo com base nas configurações de formulário especificadas no servidor do AEM Forms.

* **Frequência de Salvamento Automático**: Para definir a frequência na qual seu [aplicativo para dispositivos móveis salva dados de formulário](../../forms/using/autosave-data-app.md) localmente.
* **Frequência de Sincronização**: para definir a frequência com que seu [aplicativo móvel é sincronizado](../../forms/using/sync-app.md) com o servidor AEM Forms no modo online.
  **Limpar Dados Locais**: Limpa o banco de dados, incluindo as configurações e os dados locais de todos os usuários e o armazenamento de arquivos do dispositivo.

>[!NOTE]
>
>Limpar o cache encerra sua sessão imediatamente no aplicativo.
>
>No entanto, você será solicitado a confirmar a operação de limpeza do cache.
