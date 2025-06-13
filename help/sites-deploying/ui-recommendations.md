---
title: Recomendações da interface do usuário para clientes
description: Uma lista de recomendações relacionadas às interfaces do usuário clássicas e otimizadas para toque.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Recomendações da interface do usuário para clientes{#user-interface-recommendations-for-customers}

O Adobe Experience Manager vem com duas interfaces: a interface unificada do Experience Cloud (também conhecida como interface habilitada para toque) e a interface clássica.

Este documento tem como objetivo orientar os clientes a fazer uma escolha sobre qual interface do usuário usar, dependendo de sua situação.

Condições de interesse:

* **IU (ou IU padrão)**
Interface do usuário moderna, introduzida na versão 5.6.0 como pré-visualização de tecnologia e estendida em versões subsequentes. Ela se baseia na experiência unificada do usuário para o Adobe Experience Cloud, anteriormente conhecida como interface habilitada para toque ou interface de toque.

* **Interface clássica**
Interface do usuário baseada na tecnologia ExtJS introduzida com o CQ 5.1 em 2008.

* **Administrador do Site**
Recursos para gerenciar a hierarquia do site (mover, ativar, referências gerenciadas) e criar novas páginas.

* **Criação de página**
Recursos para adicionar/editar o conteúdo de uma página.

* **Administrador do DAM/Assets**
Recursos para gerenciar ativos digitais (incluindo imagens, vídeo, documentos, downloads).

* **ContextHub**
Recursos para agregar informações sobre o visitante e usá-las para vários propósitos. Fornece uma interface para simular pessoas que visitam o site. A partir do AEM 6.2, o ContextHub substituiu a tecnologia anterior, Client Context.

## Geral {#general}

Nos últimos anos, a Adobe atualizou todas as soluções da Adobe Experience Cloud com uma interface de usuário unificada. Os usuários nas soluções da Experience Cloud desfrutam de uma experiência consistente com padrões comuns sobre como usar e operar os aplicativos. A cada versão, a Adobe refinou sua interface do usuário com base no feedback dos clientes que trabalham nas várias soluções.

A interface original do Adobe Experience Manager (anteriormente conhecida como CQ5), introduzida em 2008 e usada por clientes que executam as versões 5.0 a 5.6.1, está presente no AEM 6.5. Isso garante que os clientes possam atualizar para o 6.5 e se beneficiar de uma plataforma atualizada com novos recursos, usando a mesma interface do usuário.

A Adobe recomenda que os clientes planejem mudar para a nova interface em 2018/19. Isso pode ser feito durante a atualização para a versão 6.5 ou em projetos separados após a atualização, o que incluiria os ajustes necessários nas personalizações e nas caixas de diálogo de componentes.

A interface clássica foi descontinuada pelo AEM 6.4 e a Adobe não planeja fazer mais melhorias na interface clássica. Observe que a interface clássica permanece totalmente compatível enquanto estiver sendo descontinuada.

### Regras e recomendações {#rules-and-recommendations}

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
   <td><p>Usa o AEM há algum tempo.</p> <p>Usou a interface do usuário do produto pronta para uso e desenvolveu componentes personalizados para os sites.<br /> </p> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Use a interface padrão para administração do site, ativos, .. etc.<br /> </li>
     <li>Configure a ação "Editar página" para abrir o Editor de páginas da interface clássica. Consulte <a href="#selecting-your-ui">Selecionando sua interface</a>.</li>
    </ol> <p>Em seguida, em uma segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato da caixa de diálogo Coral 3. A Adobe recomenda usar as <a href="/help/sites-developing/modernization-tools.md">Ferramentas de Modernização do AEM</a> para atualizar os componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Criou um site que usa o ClientContext com integrações.<br /> </td>
   <td>
    <ol>
     <li>Atualização para 6.5</li>
     <li>Use a interface padrão para administração do site, ativos, .. etc.</li>
     <li>Configure a ação "Editar página" para abrir o Editor de páginas da interface clássica. Consulte <a href="#selecting-your-ui">Selecionando sua interface</a>.</li>
    </ol> <p>Em seguida, em uma segunda fase:</p>
    <ol>
     <li>Atualize as caixas de diálogo dos componentes para usar o formato da caixa de diálogo Coral 3. A Adobe recomenda usar as <a href="/help/sites-developing/modernization-tools.md">Ferramentas de Modernização do AEM</a> para atualizar os componentes.</li>
     <li>Configure o ContextHub (a substituição do ClientContext) e atualize os modelos de página para usar o ContextHub. O ContextHub tem um modo de compatibilidade que permite carregar lojas ClientContext personalizadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>A usa o CQ/AEM há muitos anos.</p> <p>O estendeu a interface do usuário do produto (por exemplo, Administrador do site) e criou componentes com caixas de diálogo de edição abrangentes.</p> </td>
   <td><p>Atualize para a versão 6.5 e configure a interface clássica como padrão para a criação de página para todos os usuários. Consulte <a href="#selecting-your-ui">Selecionando sua interface</a>.</p> <p>Em seguida, inicie um projeto para aplicar a personalização e otimizar as caixas de diálogo do componente no formato Coral 3. Consulte <a href="#resources-to-help">Recursos para obter ajuda</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Seleção da interface do usuário {#selecting-your-ui}

Consulte [Selecionando a Interface do Usuário](/help/sites-authoring/select-ui.md) para obter informações sobre como configurar o sistema conforme necessário.

### Status da interface de usuário habilitada para toque {#touch-enabled-ui-status}

Para obter detalhes sobre os aprimoramentos feitos na interface habilitada para toque no AEM 6.5, consulte [Novidades](/help/release-notes/release-notes.md#what-s-new) nas Notas de versão.

Uma visão geral completa veja a página [Status do Recurso da Interface para Toque](/help/release-notes/touch-ui-features-status.md)

### Recursos para ajudar {#resources-to-help}

Para obter informações de fundo sobre o manuseio básico:

* [Páginas de Criação](/help/sites-authoring/page-authoring.md).

Para obter informações detalhadas sobre desenvolvimento:

* [Arquitetura de interface habilitada para toque](/help/sites-developing/touch-ui-concepts.md).
* Use as [Ferramentas de Modernização do AEM](/help/sites-developing/modernization-tools.md) para converter as caixas de diálogo de Edição de componente da interface clássica para a interface habilitada para toque.

* [Estrutura da interface habilitada para toque](/help/sites-developing/touch-ui-structure.md).

* [Personalizando os consoles na interface habilitada para toque](/help/sites-developing/customizing-consoles-touch.md) (inclui código de exemplo).

* [Personalizando a criação de página na interface habilitada para toque](/help/sites-developing/customizing-page-authoring-touch.md) (inclui código de exemplo).

* [Documentação da interface do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
