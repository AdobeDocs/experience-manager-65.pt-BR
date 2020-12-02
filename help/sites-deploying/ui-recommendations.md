---
title: Interface do usuário Recommendations para clientes
seo-title: Interface do usuário Recommendations para clientes
description: Uma lista de recomendações relacionadas às interfaces do usuário clássica e otimizada ao toque.
seo-description: Uma lista de recomendações relacionadas às interfaces do usuário clássica e otimizada ao toque.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---


# Interface do usuário Recommendations para clientes{#user-interface-recommendations-for-customers}

A Adobe Experience Manager vem com duas interfaces de usuário - a interface de usuário de Experience Cloud unificada (também conhecida como interface de usuário habilitada para toque) e a interface de usuário clássica.

Este documento tem como objetivo orientar os clientes para fazerem uma escolha sobre qual interface usar, dependendo de sua situação.

Termos de interesse:

* **Interface de usuário (ou interface de usuário padrão)Interface de usuário**
moderna que foi introduzida na versão 5.6.0 como uma pré-visualização de tecnologia e estendida em versões subsequentes. Ele é baseado na experiência unificada do usuário para o Adobe Experience Cloud, anteriormente conhecida como interface habilitada para toque ou interface de usuário para toque.

* **Interface clássica**
UIUser baseada na tecnologia ExtJS que foi introduzida com o CQ 5.1 em 2008.

* **Site**
AdminCapabilities para gerenciar a hierarquia do site (mover, ativar, referências gerenciadas) e criar novas páginas.

* **Criação**
de páginaCapacidades para adicionar/editar o conteúdo de uma página.

* **DAM/Assets**
AdminCapacidades para gerenciar ativos digitais (incluindo imagens, vídeo, documentos, downloads).

* ****
ContextHubCapacidades para agregação de informações sobre o visitante e usá-lo para vários fins. Fornece uma interface de usuário para simular pessoas que visitam o site. A partir do AEM 6.2, o ContextHub substituiu a tecnologia anterior, o Client Context.

## Geral {#general}

Nos últimos anos, a Adobe atualizou todas as soluções da Adobe Experience Cloud com uma interface de usuário unificada. Os usuários nas soluções de Experience Cloud desfrutam de uma experiência consistente com padrões comuns sobre como usar e operar os aplicativos. Com cada versão, o Adobe refinou sua interface de usuário com base no feedback dos clientes que trabalham nas várias soluções.

A interface de usuário original para Adobe Experience Manager (anteriormente conhecida como CQ5), apresentada em 2008 e usada pelos clientes que executam as versões 5.0-5.6.1, está presente no AEM 6.5. Isso garante que os clientes possam atualizar para a versão 6.5 e se beneficiar de uma plataforma atualizada com novos recursos, além de continuar usando a mesma interface do usuário.

A Adobe recomenda que os clientes planejem mudar para a nova interface do usuário em 2018/19. Isso pode ser feito durante a atualização para o 6.5 - ou em projetos separados após a atualização, o que incluiria os ajustes necessários nas caixas de diálogo de personalizações e componentes.

A interface clássica foi substituída pela AEM 6.4 e o Adobe não pretende fazer mais aprimoramentos na interface clássica. Observe que a interface do usuário clássica permanece completamente compatível mesmo enquanto obsoluta.

### Regras e Recommendations {#rules-and-recommendations}

Veja a seguir uma lista de recomendações do Gerenciamento de produtos para Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Meu projeto...</th>
   <th>Recomendações</th>
  </tr>
  <tr>
   <td>Está apenas começando a usar o Adobe Experience Manager.</td>
   <td>Use a interface padrão.</td>
  </tr>
  <tr>
   <td><p>Usou AEM há algum tempo.</p> <p>Utilizou a interface do produto predefinida e desenvolveu componentes personalizados para os sites.<br /> </p> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Usar a interface padrão para administração do site, ativos, ... etc.<br /> </li>
     <li>Configure a ação "Editar página" para abrir o Editor de página da interface clássica. Consulte <a href="#selecting-your-ui">Selecionar a interface do usuário</a>.</li>
    </ol> <p>Em seguida, numa segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato de caixa de diálogo Coral 3. O Adobe recomenda usar a <a href="/help/sites-developing/dialog-conversion.md">Ferramenta de conversão de caixa de diálogo</a> para atualizar os componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Criou um site que usa o ClientContext com integrações.<br /> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Usar a interface padrão para administração do site, ativos, ... etc.</li>
     <li>Configure a ação "Editar página" para abrir o Editor de página da interface clássica. Consulte <a href="#selecting-your-ui">Selecionar a interface do usuário</a>.</li>
    </ol> <p>Em seguida, numa segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato de caixa de diálogo Coral 3. O Adobe recomenda usar a <a href="/help/sites-developing/dialog-conversion.md">Ferramenta de conversão de caixa de diálogo</a> para atualizar os componentes.</li>
     <li>Configure o ContextHub (a substituição do ClientContext) e atualize os modelos de página para usar o ContextHub. Observe que o ContextHub tem um modo de compatibilidade que permite carregar ClientContexts personalizados.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Usou CQ/AEM há muitos anos.</p> <p>Ampliou a interface do usuário do produto (por exemplo, Administrador do site) e criou componentes com diálogos de edição abrangentes.</p> </td>
   <td><p>Atualize para a versão 6.5 e configure a interface clássica como padrão para a criação de página para todos os usuários. Consulte <a href="#selecting-your-ui">Selecionar a interface do usuário</a>.</p> <p>Em seguida, start um projeto para aplicar a personalização e otimizar as caixas de diálogo de componentes no formato Coral 3. Consulte <a href="#resources-to-help">Recursos para Ajuda</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Perguntas frequentes {#faq}

Consulte o artigo da Base de conhecimento, [Perguntas frequentes sobre criação de interface de usuário para toque](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obter detalhes; incluindo quaisquer informações sobre o agendamento de desaprovação para a interface clássica.

### Selecionar a interface do usuário {#selecting-your-ui}

Consulte [Selecionar a interface do usuário](/help/sites-authoring/select-ui.md) para obter informações sobre como configurar seu sistema, conforme necessário.

### Status da interface de usuário habilitada para toque {#touch-enabled-ui-status}

Para obter detalhes sobre os aprimoramentos feitos na interface habilitada para toque no AEM 6.5, consulte [Novidades](/help/release-notes/release-notes.md#what-s-new) nas Notas de versão.

Uma visão geral completa consulte a página [Status do recurso da interface de usuário de toque](/help/release-notes/touch-ui-features-status.md)

### Recursos para a Ajuda {#resources-to-help}

Para obter informações gerais sobre a manipulação básica:

* [Criar páginas](/help/sites-authoring/page-authoring.md).

Para obter informações detalhadas sobre o desenvolvimento:

* [Arquitetura](/help/sites-developing/touch-ui-concepts.md) da interface habilitada para toque.
* Use a [ferramenta Conversão de diálogo](/help/sites-developing/dialog-conversion.md) para converter as caixas de diálogo Editar componentes da interface clássica para a interface habilitada para toque.

* [Estrutura da interface de usuário](/help/sites-developing/touch-ui-structure.md) habilitada para toque.

* [Personalizar os consoles na interface](/help/sites-developing/customizing-consoles-touch.md)  habilitada para toque (inclui código de amostra).

* [Personalizar a criação de página na interface](/help/sites-developing/customizing-page-authoring-touch.md)  habilitada para toque (inclui código de amostra).

* [AEM Sessão Gem na personalização](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html) ativada por toque.
* [Documentação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) da interface do usuário Granite.

