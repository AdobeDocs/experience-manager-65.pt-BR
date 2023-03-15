---
title: Fragmentos de conteúdo — Navegador de configuração
description: Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: da41f48d08b7629a734e2f60077af6190a7fee8f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 78%

---

# Fragmentos de conteúdo — Navegador de configuração{#content-fragments-configuration-browser}

Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de conteúdo, você precisa usar o **navegador de configuração** para ativar:

* **Modelos de fragmentos de conteúdo** (obrigatório)
* **Consultas persistentes de GraphQL** (opcional)

>[!CAUTION]
>
>Se você não ativar os **modelos de fragmentos de conteúdo**:
>
>* a opção **Criar** não estará disponível para criar novos modelos.
>* você não poderá [selecionar a configuração de sites para criar o ponto de acesso relacionado](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Para ativar a funcionalidade do fragmento de conteúdo, é necessário:

* Ativar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à sua pasta de ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar determinadas funcionalidades do fragmento de conteúdo](#creating-a-content-fragment-model), primeiro é **necessário** habilitá-las por meio do **navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte também [Navegador de configuração:](/help/sites-administering/configurations.md#using-configuration-browser).

1. Navegue até **Ferramentas**, **Geral**, e abra o **Navegador de configuração**.

1. Selecione **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifica um **Título**.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas persistentes de GraphQL**

      ![Definir configuração](assets/cfm-conf-01.png)


1. Selecione **Criar** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplique a configuração à sua pasta de ativos {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** estiver ativado para a funcionalidade de fragmento de conteúdo, então se aplica a qualquer pasta de Ativos.

Para usar outras configurações (ou seja, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Isso é feito ao selecionar a **Configuração** apropriada na guia **Serviços da nuvem** das **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)
