---
title: AEM Sites - Disponibilidade do GDPR
description: Saiba mais sobre os procedimentos para lidar com solicitações do GDPR no AEM Sites e como usá-los.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: 5c1eda486e31be01f614a3a7ada71563fd996656
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 54%

---

# AEM Sites - Disponibilidade do GDPR{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR, CCPA e assim por diante.

O Regulamento Geral sobre a Proteção de Dados da União Europeia entra em vigor em maio de 2018.

A AEM Sites está pronta para ajudar os clientes em suas obrigações de conformidade com o GDPR. Esta página orienta os clientes por meio de procedimentos para lidar com solicitações do GDPR na AEM Sites. Ele descreve a localização dos dados privados armazenados e como removê-los manualmente ou com um código.

Para obter mais informações, consulte a [página do GDPR no Centro de Privacidade Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparação para o GDPR do AEM](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

## Servidor do autor {#author-server}

As contas de usuário e o conteúdo UGC no servidor do autor são abordados na [documentação do GDPR da plataforma](/help/managing/data-protection-and-privacy.md).

## Publish Server {#publish-server}

As contas de usuário usadas para autenticar visitantes no site e o conteúdo UGC no servidor de publicação são abordados na [Documentação do GDPR da plataforma](/help/managing/data-protection-and-privacy.md).

Por padrão, os componentes dos AEM Sites não armazenam dados de formulário inseridos por visitantes no servidor de publicação. É recomendado encaminhar os dados para um sistema de terceiros ou para o Adobe Campaign para processamento adicional.

## Aceitar/Recusar {#opt-in-opt-out}

O AEM tem um [serviço de cookie de recusa](/help/sites-developing/cookie-optout.md) que pode ser usado para gerenciar a aceitação/recusa dos usuários.

## Insights aprimorados pelo Analytics {#enhanced-insights-by-analytics}

O AEM Sites inclui uma integração opcional com o Enhanced Insights by Analytics que usa a funcionalidade no Adobe Analytics On-demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados do GDPR relacionadas ao Adobe Analytics, consulte [Adobe Analytics e GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalization aprimorado por Target {#enhanced-personalization-by-target}

O AEM Sites inclui uma integração opcional com o Enhanced Personalization by Target que usa a funcionalidade no Adobe Target On-demand Service.

Para obter mais informações sobre como gerenciar solicitações de titulares de dados do GDPR relacionadas ao Adobe Target, consulte [Adobe Target - Privacidade e Regulamento Geral sobre a Proteção de Dados](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

O AEM fornece uma camada de dados opcional com [ContextHub](/help/sites-developing/contexthub.md). Isto mantém os dados específicos do visitante no navegador, para serem usados para personalização baseada em regras.

Por padrão, esses dados do visitante não são armazenados no AEM; o AEM envia as regras para a camada de dados para tomar decisões de personalização no navegador.

>[!NOTE]
>
>Antes do Adobe AEM(CQ) 5.6, o ClientContext (uma versão anterior do ContextHub) enviava os dados para o servidor, mas não os armazenava.
>
>O Adobe AEM 6.4 e versões anteriores estão agora em final de vida útil e não são cobertos por esta documentação. Consulte [Documentação das versões anteriores do Adobe Experience Manager, CQ e CRX](https://experienceleague.adobe.com/br/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions).

### Implementação do Opt-in/Opt-out (Aceitar/Recusar) {#implementing-opt-in-opt-out}

O proprietário do site precisa implementar um componente de opção de recusa, de acordo com as diretrizes a seguir.

Essas diretrizes implementam a opção de aceitação como padrão. Assim, um visitante do site deve concordar claramente, antes que quaisquer Dados pessoais sejam armazenados na persistência do navegador (lado do cliente).

* O componente de opt out (recusar) deve ser incluído sempre que o componente ContextHub for incluído.
* Os termos e condições relacionados ao GDPR do site devem ser exibidos para o visitante do site, para que eles possam:

   * Aceitar
   * Rejeitar
   * alterar a opção anterior

* Se um visitante aceitar os termos e condições do site, o cookie de opção de recusa do ContextHub deverá ser removido:

  ```java
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Se um visitante não aceitar os termos e condições do site, o cookie de opção de recusa do ContextHub deverá ser definido:

  ```java
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* Para verificar se o ContextHub está sendo executado no modo de recusa, a seguinte chamada deve ser feita no console do navegador:

  ```java
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Visualização da persistência do ContextHub {#previewing-persistence-of-contexthub}

Para visualizar a persistência usada pelo ContextHub, um usuário pode:

* Use o console do navegador; por exemplo:

   * Chrome:

      * Abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento de sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence

   * Firefox:

      * Abra Ferramentas do desenvolvedor > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento de sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence

   * Safari:

      * Abra Preferências > Avançado > Mostrar menu Desenvolvedor na barra de menus
      * Abra Desenvolver > Mostrar console do JavaScript

         * Console > Armazenamento > Armazenamento local > (site) > ContextHubPersistence
         * Console > Armazenamento > Armazenamento de sessão > (site) > ContextHubPersistence
         * Console > Armazenamento > Cookies > (site) > ContextHubPersistence

   * Internet Explorer:

      * Abra Ferramentas do desenvolvedor > Console

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie

* Use a API do ContextHub no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     O armazenamento do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.

Por exemplo, para exibir dados armazenados em localStorage:

Para visualizar a persistência usada pelo ContextHub, um usuário pode:

* Use o console do navegador:

   * Chrome - abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence

   * Firefox - abra Ferramentas do desenvolvedor > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento de sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence

* Use a API do ContextHub no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     O armazenamento do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.

Por exemplo, para exibir dados armazenados em localStorage:

```java
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Limpando a persistência do ContextHub {#clearing-persistence-of-contexthub}

Para limpar a persistência do ContextHub:

* Para eliminar a persistência de armazenamentos carregados no momento:

  ```java
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* Para eliminar uma camada de persistência específica; por exemplo, sessionStorage:

  ```java
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* Para eliminar todas as camadas de persistência do ContextHub, o código apropriado deve ser chamado para todas as camadas:

   * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
