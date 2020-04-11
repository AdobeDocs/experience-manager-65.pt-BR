---
title: Trabalhar no modo offline
seo-title: Trabalhar no modo offline
description: Coloque seu dispositivo móvel offline fora do intervalo de rede do AEM Forms ou em um modo completamente offline e trabalhe no aplicativo AEM Forms
seo-description: Coloque seu dispositivo móvel offline fora do intervalo de rede do AEM Forms ou em um modo completamente offline e trabalhe no aplicativo AEM Forms
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Trabalhar no modo offline {#working-in-the-offline-mode}

O modo offline do aplicativo AEM Forms permite que você trabalhe sem problemas mesmo se o aplicativo ficar offline. Você pode abrir, atualizar e enviar um formulário sem precisar de conectividade de rede.

start de trabalhar no aplicativo AEM Forms sincronizando seu aplicativo com o servidor AEM Forms. Todos os formulários atribuídos a você são baixados no aplicativo. Para o AEM Forms em JEE, o tarefa é buscado na guia tarefa e os pontos de partida associados a formulários e outros formulários na guia Formulários. Para formulários AEM no OSGi, somente os formulários são carregados na guia Formulários.

Para obter detalhes sobre como sincronizar o aplicativo, consulte [Sincronizar o aplicativo](/help/forms/using/sync-app.md).

## Disponibilização offline de formulários {#making-forms-available-offline}

Quando você sincroniza seu aplicativo com o servidor de formulários AEM, os formulários são baixados para seu dispositivo móvel. No entanto, por padrão, os anexos associados ao formulário não são baixados. Isso significa que, se você estiver online, poderá visualização os anexos. Entretanto, para garantir que você possa visualização o anexo no modo offline, altere as configurações padrão no aplicativo.

Para garantir que os anexos associados sejam baixados com cada formulário, defina a opção Buscar anexos como ON. Para obter detalhes, consulte [Atualização de configurações](/help/forms/using/update-general-settings.md)gerais.

Como o download de dados no dispositivo móvel pode afetar o desempenho do dispositivo, por padrão, a configuração Buscar anexos está definida como OFF. Os anexos são buscados no dispositivo para qualquer tarefa baixada do servidor depois que a configuração é atualizada para ON. No modo offline, um usuário pode trabalhar em todas as tarefas baixadas no dispositivo depois de definir as opções **Buscar anexos** como ATIVADO.

## Configurar o serviço offline para o aplicativo AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

O serviço offline do aplicativo AEM Forms identifica os recursos usados em um formulário. O aplicativo AEM Forms depende desse serviço para obter informações sobre dependências de formulários. As informações sobre dependências de formulário são necessárias para ativar funcionalidades offline. O serviço offline do aplicativo AEM Forms armazena em cache os caminhos ou URLs dos recursos usados em um formulário. O cache é atualizado com base nas alterações no formulário e no período de validade configurado para o serviço offline. O cache de caminhos ou URLs dos recursos usados em um formulário melhora o desempenho do servidor.

Para configurar o componente offline do lado do servidor do aplicativo AEM Forms:

1. Na instância do autor, navegue até **Adobe Experience Manager** >**Ferramentas** > **Formulários** > **Configurar o serviço** offline do aplicativo para formulários.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. Em Configurações gerais, é possível executar o seguinte:

   * **Limpar cache**: Limpa o cache do lado do servidor das dependências do formulário.
   * **Redefinir configuração**: Redefine a configuração offline do aplicativo AEM Forms.
   * **Validade** do cache: Especifica o período de validade do cache offline do lado do servidor.
   * **Caminhos** de observação de recursos: Especifica caminhos nos quais o serviço offline monitora alterações de recursos. Se ocorrerem alterações nos caminhos especificados, o cache offline de todos os formulários dependentes será atualizado. Por exemplo, `/etc/clientlibs/fd,/content/dam/images`.

1. Na guia Cache **de recursos** manual, especifique as dependências de formulário que o serviço offline não pode identificar. Você pode especificar recursos como imagens carregadas em JavaScript. O aplicativo AEM Forms baixará esses recursos também para o modo offline.
