---
title: Trabalhar no modo offline
seo-title: Working in the offline mode
description: Coloque seu dispositivo móvel offline fora do intervalo de rede do AEM Forms ou em um modo totalmente offline e trabalhe no aplicativo AEM Forms
seo-description: Take your mobile device offline outside your AEM Forms network range or in a completely offline mode and work on the AEM Forms app
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Trabalhar no modo offline {#working-in-the-offline-mode}

O modo offline do aplicativo AEM Forms permite que você trabalhe sem interrupções, mesmo que o aplicativo fique offline. Você pode abrir, atualizar e enviar um formulário sem precisar de conectividade de rede.

Você começa a trabalhar no aplicativo AEM Forms sincronizando seu aplicativo com o servidor AEM Forms. Todos os formulários atribuídos a você são baixados no aplicativo. Para o AEM Forms no JEE, as tarefas são buscadas na guia tarefas e os pontos de partida associados e outros formulários na guia Forms . Para o AEM Forms no OSGi, somente o Forms é carregado na guia Forms .

Para obter detalhes sobre como sincronizar o aplicativo, consulte [Sincronização do aplicativo](/help/forms/using/sync-app.md).

## Disponibilizar o Forms offline {#making-forms-available-offline}

Quando você sincroniza seu aplicativo com o servidor do AEM Forms, os formulários são baixados no dispositivo móvel. No entanto, por padrão, os anexos associados ao formulário não são baixados. Isso implica que, se estiver online, poderá visualizar os anexos. No entanto, para garantir que você possa visualizar o anexo no modo offline, altere as configurações padrão no seu aplicativo.

Para garantir que os anexos associados sejam baixados com cada formulário, defina Buscar anexos como ATIVADO. Para obter detalhes, consulte [Atualização das configurações gerais](/help/forms/using/update-general-settings.md).

Como o download de dados no dispositivo móvel pode afetar o desempenho do dispositivo, por padrão, a configuração Buscar anexos está definida como OFF. Os anexos são buscados no dispositivo para qualquer tarefa que é baixada do servidor depois que a configuração é atualizada para ON. No modo offline, um usuário pode trabalhar em todas as tarefas baixadas no dispositivo depois de definir a variável **Buscar anexos** para ATIVADO.

## Configuração do serviço offline para aplicativos AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

O serviço offline de aplicativos AEM Forms identifica os recursos usados em um formulário. O aplicativo AEM Forms depende desse serviço para obter informações sobre dependências de formulário. São necessárias informações sobre dependências de formulário para ativar funcionalidades offline. O serviço offline de aplicativo AEM Forms armazena em cache os caminhos ou URLs dos recursos usados em um formulário. O cache é atualizado com base nas alterações no formulário e no período de validade configurado para o serviço offline. O armazenamento em cache de caminhos ou URLs dos recursos usados em um formulário melhora o desempenho do lado do servidor.

Para configurar o componente offline do lado do servidor do aplicativo AEM Forms:

1. Na instância do autor, navegue até **Adobe Experience Manager** >**Ferramentas** > **Forms** > **Configurar o serviço offline do aplicativo Forms**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. Em Configurações gerais, você pode executar o seguinte:

   * **Limpar Cache**: Limpa o cache do lado do servidor das dependências do formulário.
   * **Redefinir configuração**: Redefine a configuração offline do aplicativo AEM Forms.
   * **Validação do Cache**: Especifica o período de validade do cache offline do lado do servidor.
   * **Caminhos de observação de recursos**: Especifica caminhos nos quais o serviço offline monitora alterações de recursos. Se ocorrer alguma alteração nos caminhos especificados, o cache offline de todos os formulários dependentes será atualizado. Por exemplo, `/etc/clientlibs/fd,/content/dam/images`.

1. No **Cache de Recursos Manual** , especifique as dependências de formulário que o serviço offline não pode identificar. Você pode especificar recursos como imagens carregadas de dentro do JavaScript. O aplicativo AEM Forms baixará esses recursos também para o modo offline.
