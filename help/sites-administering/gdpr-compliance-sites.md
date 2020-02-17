---
title: AEM Sites - Prontidão do RGPD
seo-title: AEM Sites - Prontidão do RGPD
description: Saiba mais sobre os detalhes de Prontidão do RGPD para os sites AEM.
seo-description: Saiba mais sobre os detalhes de Prontidão do RGPD para os sites AEM.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Sites - Prontidão do RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>O RGPD é utilizado como exemplo nas seções abaixo, mas os detalhes abrangidos são aplicáveis a todas as normas de proteção de dados e privacidade; como o RGPD, o CCPA, etc.

O Regulamento Geral da União Europeia sobre a Proteção de Dados relativo aos direitos de privacidade dos dados entra em vigor em maio de 2018.

O AEM Sites está pronto para ajudar os clientes com suas obrigações de conformidade com o RGPD. Esta página orienta os clientes pelos procedimentos para lidar com solicitações do RGPD no AEM Sites. Ela descreve a localização dos dados privados armazenados e como removê-los manualmente ou com código.

Para obter mais informações, consulte a página do [RGPD no Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte Prontidão [do](/help/managing/data-protection-and-privacy.md) AEM GDPR para obter mais detalhes.

## Servidor do autor {#author-server}

As contas de usuário e o conteúdo UGC no servidor autor são abordados na documentação [do](/help/managing/data-protection-and-privacy.md)Platform GDPR.

## Servidor de publicação {#publish-server}

As contas de usuário usadas para autenticar visitantes no site e o conteúdo UGC no servidor de publicação são abordados na documentação [do](/help/managing/data-protection-and-privacy.md)Platform GDPR.

Por padrão, os componentes do AEM Sites não armazenam dados de formulário inseridos pelos visitantes no servidor de publicação. É recomendável encaminhar os dados para um sistema de terceiros ou para o Adobe Campaign para processamento adicional.

## Inclusão/recusa {#opt-in-opt-out}

O AEM tem um serviço [de opção de não participação de](/help/sites-developing/cookie-optout.md) cookie que pode ser usado para gerenciar a opção de participação/não participação dos usuários.

## Insights aprimorados pelo Analytics {#enhanced-insights-by-analytics}

O AEM Sites inclui uma integração opcional com o Enhanced Insights pelo Analytics que usa a funcionalidade no serviço sob demanda do Adobe Analytics.

Para obter mais informações sobre como gerenciar solicitações de sujeitos de dados do RGPD relacionadas ao Adobe Analytics, consulte [Adobe Analytics e RGPD](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/).

## Personalização aprimorada pelo Target {#enhanced-personalization-by-target}

O AEM Sites inclui uma integração opcional com a Personalização aprimorada pelo Target que usa a funcionalidade no serviço sob demanda do Adobe Target.

Para obter mais informações sobre como gerenciar solicitações de pessoas com dados do RGPD relacionadas ao Adobe Target, consulte [Adobe Target - Privacidade e Regulamento](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)geral de proteção de dados.

## ContextHub {#contexthub}

O AEM fornece uma camada de dados opcional com o [ContextHub](/help/sites-developing/contexthub.md). Isso mantém os dados específicos do visitante no navegador, a serem usados para personalização baseada em regras.

Por padrão, esses dados de visitante não são armazenados no AEM; O AEM envia regras para a camada de dados para tomar decisões de personalização no navegador.

>[!NOTE]
>
>Antes do Adobe CQ 5.6, o ClientContext (uma versão anterior do ContextHub) enviava os dados para o servidor, mas não os armazenava.
>
>O Adobe CQ 5.5 e versões anteriores agora são EOL e não são abordados nesta documentação.

### Implementação da aceitação/não participação {#implementing-opt-in-opt-out}

O proprietário do site precisa implementar um componente de opção de não participação de acordo com as diretrizes a seguir.

Essas diretrizes implementam o opt-in como padrão. Assim, um visitante do site deve concordar claramente, antes que qualquer dado pessoal seja armazenado na persistência do navegador (do lado do cliente).

* O componente de opção de não participação deve ser incluído toda vez que o componente ContextHub for incluído.
* Os termos e condições relacionados com o RGPD para o sítio web devem ser apresentados ao visitante do sítio, permitindo-lhe:

   * accept
   * rejeição
   * alterar sua escolha anterior

* Se um visitante do site aceitar os termos e condições do site, o cookie de opção de não participação do ContextHub deverá ser removido:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se um visitante do site não aceitar os termos e condições do site, o cookie de opção de não participação do ContextHub deverá ser definido:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para verificar se o ContextHub está sendo executado no modo de não participação, a seguinte chamada deve ser feita no console do navegador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Visualização da persistência do ContextHub {#previewing-persistence-of-contexthub}

Para visualizar a persistência usada pelo ContextHub, o usuário pode:

* Use o console do navegador; por exemplo:

   * Chrome:

      * Abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento da sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Firefox:

      * Abra Ferramentas do desenvolvedor > Armazenamento:

         * Armazenamento local > (site) > ContextHubPersistence
         * Armazenamento da sessão > (site) > ContextHubPersistence
         * Cookies > (site) > SessionPersistence
   * Safari:

      * Abrir Preferências > Avançado > Mostrar menu Revelação na barra de menus
      * Abrir Revelação > Mostrar JavaScript Console

         * Console > Armazenamento > Armazenamento local > (site) > ContextHubPersistence
         * Console > Armazenamento > Armazenamento da sessão > (site) > ContextHubPersistence
         * Console > Armazenamento > Cookies > (site) > ContextHubPersistence
   * Internet Explorer:

      * Abra Ferramentas do desenvolvedor > Console

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* Use a API ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      O repositório do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para exibir dados armazenados em localStorage:

Para visualizar a persistência usada pelo ContextHub, o usuário pode:

* Use o console do navegador:

   * Chrome - abra Ferramentas do desenvolvedor > Aplicativo > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento da sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence
   * Firefox - abra Ferramentas do desenvolvedor > Armazenamento:

      * Armazenamento local > (site) > ContextHubPersistence
      * Armazenamento da sessão > (site) > ContextHubPersistence
      * Cookies > (site) > SessionPersistence


* Use a API ContextHub, no console do navegador:

   * O ContextHub fornece as seguintes camadas de persistência de dados:

      * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      O repositório do ContextHub define qual camada de persistência será usada, portanto, para exibir o estado atual da persistência, todas as camadas devem ser verificadas.


Por exemplo, para exibir dados armazenados em localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Limpando a persistência do ContextHub {#clearing-persistence-of-contexthub}

Para limpar a persistência do ContextHub:

* Para eliminar a persistência dos armazenamentos atualmente carregados:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Para limpar uma camada de persistência específica; por exemplo, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Para limpar todas as camadas de persistência do ContextHub, o código apropriado deve ser chamado para todas as camadas:

   * ContextHub.Utils.Persistence.Modes.LOCAL (padrão)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

