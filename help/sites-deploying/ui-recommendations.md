---
title: Recomendações da interface do usuário para clientes
seo-title: Recomendações da interface do usuário para clientes
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

---


# Recomendações da interface do usuário para clientes{#user-interface-recommendations-for-customers}

O Adobe Experience Manager vem com duas interfaces de usuário - a interface de usuário unificada da Experience Cloud (também conhecida como interface de usuário habilitada para toque) e a interface de usuário clássica.

Este documento destina-se a orientar os clientes para fazerem uma escolha sobre qual interface usar, dependendo de sua situação.

Termos de interesse:

* **Interface de usuário (ou interface de usuário padrão)Interface de usuário** moderna que foi introduzida na versão 5.6.0 como uma visualização de tecnologia e estendida em versões subsequentes. Ele se baseia na experiência unificada do usuário para a Adobe Experience Cloud, anteriormente conhecida como interface habilitada para toque ou interface de usuário para toque.

* **Interface clássica do** usuário com base na tecnologia ExtJS que foi introduzida com o CQ 5.1 em 2008.

* **Recursos de administração** do site para gerenciar a hierarquia do site (mover, ativar, referências gerenciadas) e criar novas páginas.

* **Recursos de criação** de página para adicionar/editar o conteúdo de uma página.

* **DAM/Assets Admin** Capacidades para gerenciar ativos digitais (incluindo imagens, vídeo, documentos, downloads).

* **ContextHub** Capacidades para agregar informações sobre o visitante e usá-las para vários fins. Fornece uma interface de usuário para simular pessoas visitando o site. A partir do AEM 6.2, o ContextHub substituiu a tecnologia anterior, Contexto do cliente.

## Geral {#general}

Nos últimos anos, a Adobe atualizou todas as soluções da Adobe Experience Cloud com uma interface de usuário unificada. Os usuários nas soluções da Experience Cloud desfrutam de uma experiência consistente com padrões comuns sobre como usar e operar os aplicativos. Com cada versão, a Adobe refinou sua interface de usuário com base no feedback dos clientes que trabalham nas várias soluções.

A interface de usuário original do Adobe Experience Manager (anteriormente conhecida como CQ5), apresentada em 2008 e usada pelos clientes que executam as versões 5.0 a 5.6.1, está presente no AEM 6.5. Isso garante que os clientes possam atualizar para a versão 6.5 e se beneficiar de uma plataforma atualizada com novos recursos, além de continuar usando a mesma interface do usuário.

A Adobe recomenda que os clientes planejem mudar para a nova interface do usuário em 2018/19. Isso pode ser feito durante a atualização para o 6.5 - ou em projetos separados após a atualização, o que incluiria os ajustes necessários nas caixas de diálogo de personalizações e componentes.

A interface clássica foi substituída pelo AEM 6.4 e a Adobe não planeja fazer mais aprimoramentos na interface clássica. Observe que a interface do usuário clássica permanece completamente compatível mesmo enquanto obsoluta.

### Regras e recomendações {#rules-and-recommendations}

Esta é uma lista de recomendações do Gerenciamento de produtos para o Adobe Experience Manager 6.5:

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
   <td><p>Usou o AEM há algum tempo.</p> <p>Utilizou a interface do produto pronta para uso e desenvolveu componentes personalizados para os sites.<br /> </p> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Usar a interface padrão para administração do site, ativos, ... etc.<br /> </li>
     <li>Configure a ação "Editar página" para abrir o Editor de página da interface clássica. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>Em seguida, numa segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato de caixa de diálogo Coral 3. A Adobe recomenda usar a Ferramenta <a href="/help/sites-developing/dialog-conversion.md">de conversão de</a> caixa de diálogo para atualizar os componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Criou um site que usa o ClientContext com integrações.<br /> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Usar a interface padrão para administração do site, ativos, ... etc.</li>
     <li>Configure a ação "Editar página" para abrir o Editor de página da interface clássica. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>Em seguida, numa segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato de caixa de diálogo Coral 3. A Adobe recomenda usar a Ferramenta <a href="/help/sites-developing/dialog-conversion.md">de conversão de</a> caixa de diálogo para atualizar os componentes.</li>
     <li>Configure o ContextHub (a substituição para ClientContext) e atualize os modelos de página para usar o ContextHub. Observe que o ContextHub tem um modo de compatibilidade que permite carregar armazenamentos personalizados do ClientContext.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Usou o CQ/AEM há muitos anos.</p> <p>Ampliou a interface do usuário do produto (por exemplo, Administrador do site) e criou componentes com diálogos de edição abrangentes.</p> </td>
   <td><p>Atualize para a versão 6.5 e configure a interface clássica como padrão para a criação de página para todos os usuários. See <a href="#selecting-your-ui">Selecting Your UI</a>.</p> <p>Em seguida, inicie um projeto para aplicar a personalização e otimizar as caixas de diálogo de componentes no formato Coral 3. Consulte <a href="#resources-to-help">Recursos para obter ajuda</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Perguntas frequentes {#faq}

Consulte o artigo da Base de conhecimento, Perguntas frequentes [sobre criação de interfaces de](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)toque, para obter detalhes; incluindo quaisquer informações sobre o agendamento de desaprovação para a interface clássica.

### Selecting Your UI {#selecting-your-ui}

Consulte [Seleção da interface do usuário](/help/sites-authoring/select-ui.md) para obter informações sobre como configurar seu sistema, conforme necessário.

### Status da interface de usuário habilitada para toque {#touch-enabled-ui-status}

Para obter detalhes sobre os aprimoramentos feitos na interface habilitada para toque no AEM 6.5, consulte [Novidades](/help/release-notes/release-notes.md#what-s-new) nas Notas de versão.

Uma visão geral completa consulte a página Status [do recurso da interface de](/help/release-notes/touch-ui-features-status.md) toque

### Recursos para Ajuda {#resources-to-help}

Para obter informações gerais sobre a manipulação básica:

* [Criar páginas](/help/sites-authoring/page-authoring.md).

Para obter informações detalhadas sobre o desenvolvimento:

* [Arquitetura](/help/sites-developing/touch-ui-concepts.md)da interface habilitada para toque.
* Use a ferramenta [Conversão de](/help/sites-developing/dialog-conversion.md) diálogo para converter as caixas de diálogo Editar do componente da interface clássica para a interface habilitada para toque.

* [Estrutura da interface de usuário](/help/sites-developing/touch-ui-structure.md)habilitada para toque.

* [Personalizar os consoles na interface](/help/sites-developing/customizing-consoles-touch.md) habilitada para toque (inclui código de amostra).

* [Personalizar a criação de página na interface](/help/sites-developing/customizing-page-authoring-touch.md) habilitada para toque (inclui código de amostra).

* [Sessão Gem do AEM na personalização](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)habilitada para toque.
* [Documentação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)da interface do usuário Granite.

