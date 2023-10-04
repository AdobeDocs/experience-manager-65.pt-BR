---
title: Interface do usuário do Recommendations para clientes
seo-title: User Interface Recommendations for Customers
description: Uma lista de recomendações relacionadas às interfaces do usuário clássicas e otimizadas para toque.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Interface do usuário do Recommendations para clientes{#user-interface-recommendations-for-customers}

O Adobe Experience Manager vem com duas interfaces: a interface unificada do Experience Cloud (também conhecida como interface habilitada para toque) e a interface clássica.

Este documento tem como objetivo orientar os clientes a fazer uma escolha sobre qual interface do usuário usar, dependendo de sua situação.

Condições de interesse:

* **Interface do usuário (ou interface padrão)**
Interface do usuário moderna, introduzida na versão 5.6.0 como pré-visualização de tecnologia e estendida em versões subsequentes. Ela se baseia na experiência unificada do usuário para o Adobe Experience Cloud, anteriormente conhecida como interface habilitada para toque ou interface de toque.

* **Interface clássica**
Interface do usuário baseada na tecnologia ExtJS introduzida com o CQ 5.1 em 2008.

* **Administrador do site**
Recursos para gerenciar a hierarquia do site (mover, ativar, referências gerenciadas) e criar novas páginas.

* **Criação de página**
Recursos para adicionar/editar o conteúdo de uma página.

* **DAM/Administrador de ativos**
Recursos para gerenciar ativos digitais (incluindo imagens, vídeo, documentos, downloads).

* **ContextHub**
Recursos para agregar informações sobre o visitante e usá-las para vários propósitos. Fornece uma interface para simular pessoas que visitam o site. A partir do AEM 6.2, o ContextHub substituiu a tecnologia anterior, Client Context.

## Geral {#general}

Nos últimos anos, a Adobe atualizou todas as soluções da Adobe Experience Cloud com uma interface unificada. Os usuários nas soluções Experience Cloud desfrutam de uma experiência consistente com padrões comuns sobre como usar e operar os aplicativos. Com cada versão, a Adobe refinou sua interface de usuário com base no feedback dos clientes que trabalham nas várias soluções.

A interface de usuário original do Adobe Experience Manager (anteriormente conhecida como CQ5), introduzida em 2008 e usada por clientes que executam as versões 5.0 a 5.6.1, está presente no AEM 6.5. Isso garante que os clientes possam atualizar para o 6.5 e se beneficiar de uma plataforma atualizada com novos recursos, usando a mesma interface do usuário.

A Adobe recomenda que os clientes planejem mudar para a nova interface em 2018/19. Isso pode ser feito durante a atualização para a versão 6.5 ou em projetos separados após a atualização, o que incluiria os ajustes necessários nas personalizações e nas caixas de diálogo de componentes.

A interface clássica foi descontinuada com o AEM 6.4 e o Adobe não planeja fazer mais melhorias na interface clássica. Observe que a interface clássica permanece totalmente compatível enquanto estiver sendo descontinuada.

### Regras e Recommendations {#rules-and-recommendations}

Esta é uma lista de recomendações do Gerenciamento de produtos do Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Meu projeto...</th>
   <th>Recomendações</th>
  </tr>
  <tr>
   <td>Está começando a usar o Adobe Experience Manager.</td>
   <td>Use a interface padrão.</td>
  </tr>
  <tr>
   <td><p>Já usa AEM há algum tempo.</p> <p>Usou a interface do usuário do produto pronta para uso e desenvolveu componentes personalizados para os sites.<br /> </p> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Use a interface padrão para administração do site, ativos, .. etc.<br /> </li>
     <li>Configure a ação "Editar página" para abrir o Editor de páginas da interface clássica. Consulte <a href="#selecting-your-ui">Seleção da interface do usuário</a>.</li>
    </ol> <p>Em seguida, em uma segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato da caixa de diálogo Coral 3. O Adobe recomenda o uso de <a href="/help/sites-developing/modernization-tools.md">Ferramentas de modernização do AEM</a> para atualizar os componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Criou um site que usa o ClientContext com integrações.<br /> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Use a interface padrão para administração do site, ativos, .. etc.</li>
     <li>Configure a ação "Editar página" para abrir o Editor de páginas da interface clássica. Consulte <a href="#selecting-your-ui">Seleção da interface do usuário</a>.</li>
    </ol> <p>Em seguida, em uma segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato da caixa de diálogo Coral 3. O Adobe recomenda o uso de <a href="/help/sites-developing/modernization-tools.md">Ferramentas de modernização do AEM</a> para atualizar os componentes.</li>
     <li>Configure o ContextHub (a substituição do ClientContext) e atualize os modelos de página para usar o ContextHub. Observe que o ContextHub tem um modo de compatibilidade que permite carregar armazenamentos de ClientContexts personalizados.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Tem usado CQ/AEM por muitos anos.</p> <p>O estendeu a interface do usuário do produto (por exemplo, Administrador do site) e criou componentes com caixas de diálogo de edição abrangentes.</p> </td>
   <td><p>Atualize para a versão 6.5 e configure a interface clássica como padrão para a criação de página para todos os usuários. Consulte <a href="#selecting-your-ui">Seleção da interface do usuário</a>.</p> <p>Em seguida, inicie um projeto para aplicar a personalização e otimizar as caixas de diálogo do componente no formato Coral 3. Consulte <a href="#resources-to-help">Recursos para ajudar</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Perguntas frequentes {#faq}

Consulte o artigo da Base de conhecimento, [Perguntas frequentes sobre criação na interface para toque](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obter detalhes; incluindo informações sobre o agendamento de desativação da interface clássica.

### Seleção da interface do usuário {#selecting-your-ui}

Consulte [Seleção da interface do usuário](/help/sites-authoring/select-ui.md) para obter informações sobre como configurar seu sistema conforme necessário.

### Status da interface de usuário habilitada para toque {#touch-enabled-ui-status}

Para obter detalhes sobre as melhorias feitas na interface do usuário habilitada para toque no AEM 6.5, consulte [Novidades](/help/release-notes/release-notes.md#what-s-new) nas Notas de versão.

Uma visão geral completa consulte o [Status do recurso da interface de toque](/help/release-notes/touch-ui-features-status.md) página

### Recursos para ajudar {#resources-to-help}

Para obter informações de fundo sobre o manuseio básico:

* [Criação de páginas](/help/sites-authoring/page-authoring.md).

Para obter informações detalhadas sobre desenvolvimento:

* [Arquitetura de interface habilitada para toque](/help/sites-developing/touch-ui-concepts.md).
* Use o [Ferramentas de modernização do AEM](/help/sites-developing/modernization-tools.md) para converter as caixas de diálogo de edição do componente da interface clássica para a interface habilitada para toque.

* [Estrutura da interface habilitada para toque](/help/sites-developing/touch-ui-structure.md).

* [Personalização dos consoles na interface habilitada para toque](/help/sites-developing/customizing-consoles-touch.md) (inclui código de amostra).

* [Personalização da criação de página na interface habilitada para toque](/help/sites-developing/customizing-page-authoring-touch.md) (inclui código de amostra).

* [Documentação da interface de usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
