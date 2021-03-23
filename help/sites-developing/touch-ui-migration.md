---
title: Migração para a interface de toque
seo-title: Migração para a interface de toque
description: Migração para a interface de toque
seo-description: Migração para a interface de toque
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---


# Migração para a interface de toque{#migration-to-the-touch-ui}

A partir da versão 6.0, o Adobe Experience Manager (AEM) introduziu uma nova interface de usuário chamada de *interface habilitada para toque* (também conhecida simplesmente como *interface de toque*). Ele está alinhado à Adobe Marketing Cloud e às diretrizes gerais da interface do usuário do Adobe. Essa interface se tornou a interface padrão no AEM com a interface herdada orientada para desktop, chamada de *interface clássica*.

Se você tem usado AEM com a interface clássica, será necessário tomar medidas para migrar sua instância. Esta página destina-se a atuar como um trampolim, fornecendo links para recursos individuais.

>[!NOTE]
>
>Esse projeto de migração pode ter um impacto significativo na sua instância. Consulte [Gerenciamento de projetos - Práticas recomendadas](/help/managing/best-practices.md) para obter as diretrizes recomendadas.

## Noções básicas {#the-basics}

Ao migrar, você deve estar ciente das seguintes (principais) diferenças entre a interface clássica e a interface de toque:

<table>
 <tbody>
  <tr>
   <td>Interface do usuário clássica</td>
   <td>Interface do usuário habilitada para toque</td>
  </tr>
  <tr>
   <td>É descrito no repositório JCR como uma estrutura de nós. Todos os nós que representam um elemento da interface do usuário são chamados de <em>Widget ExtJS</em> e renderizados no lado do cliente por <code>ExtJS</code>.</td>
   <td>Também descrito no repositório JCR como uma estrutura de nós. No entanto, nesse caso, cada nó se refere a um tipo de recurso Sling (componente Sling), que é encarregado de sua renderização. Portanto, a interface do usuário é (basicamente) renderizada no lado do servidor.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>não usado</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>usado</li>
     <li>por exemplo<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Nós de diálogo:</p>
    <ul>
     <li>Nome: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nós de diálogo:</p>
    <ul>
     <li>Nome: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Localização do JavaScript:</p>
    <ul>
     <li>As partes imperativas são diretamente incorporadas usando ouvintes ou gerenciadas em clientlibs.</li>
    </ul> </td>
   <td><p>Localização do JavaScript:</p>
    <ul>
     <li>As partes imperativas não podem ser incorporadas na definição da caixa de diálogo; separação de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Tratamento de eventos:</p>
    <ul>
     <li>Os widgets de diálogo fazem referência diretamente ao código Javascript.</li>
    </ul> </td>
   <td><p>Tratamento de eventos:</p>
    <ul>
     <li>O Javascript observa eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Renderização feita pelo cliente:
    <ul>
     <li>O cliente cria dinamicamente os componentes da interface do usuário.</li>
     <li>Definição de componente Solicitações de cliente (Pull) (como JSON) do servidor.</li>
    </ul> </td>
   <td>Renderização feita pelo servidor:
    <ul>
     <li>O cliente solicita páginas junto com a interface relacionada.</li>
     <li>O servidor envia (envia) a interface do usuário como documentos HTML; usando componentes de Coral UI.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Em outras palavras, migrar uma seção da interface do usuário clássica para a interface de toque significa portar um *widget ExtJS* para um *Componente Sling*. Para facilitar isso, a interface do usuário de toque é baseada na estrutura da interface do usuário do Granite, que já fornece alguns componentes do Sling para a interface do usuário (conhecidos como componentes da interface do usuário do Granite).

Antes de começar, verifique o status e as recomendações relacionadas:

* [Status dos recursos da interface de toque](/help/release-notes/touch-ui-features-status.md)
* [Recommendations da interface do usuário para clientes](/help/sites-deploying/ui-recommendations.md)

As noções básicas para desenvolver a interface do usuário de toque fornecerão uma base sólida:

* [Conceitos da interface de usuário habilitada para toque do AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estrutura da interface de usuário habilitada para toque do AEM](/help/sites-developing/touch-ui-structure.md)

## Migração de criação de página {#migrating-page-authoring}

As caixas de diálogo são um fator importante ao migrar seus componentes:

* [Desenvolvimento de componentes de AEM](/help/sites-developing/developing-components.md)  (com a interface habilitada para toque)
* [Migração de um componente clássico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Ferramentas de Modernização do AEM](/help/sites-developing/modernization-tools.md)  - para ajudá-lo a converter as caixas de diálogo dos componentes da interface clássica para a interface do usuário de toque

   * Há uma camada de compatibilidade na interface do usuário de toque para abrir uma caixa de diálogo da interface do usuário clássica em um &quot;invólucro da interface do usuário de toque&quot;, mas isso tem funcionalidade limitada e não é recomendado para o longo prazo.

* [Personalização de campos de diálogo na interface do usuário de toque](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Criação de um novo componente de campo da interface do usuário do Granite](/help/sites-developing/granite-ui-component.md)
* [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md)  (com a interface habilitada para toque)

## Migrando Consoles {#migrating-consoles}

Você também pode personalizar os consoles:

* [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md)  (para a interface habilitada para toque)

## Considerações relacionadas {#related-considerations}

Embora não estejam diretamente relacionadas a uma migração para a interface de toque, há problemas relacionados que vale a pena considerar ao mesmo tempo, pois também são prática recomendada:

* [Modelos](/help/sites-developing/templates.md)  - Modelos  [editáveis](/help/sites-developing/page-templates-editable.md)
* [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Consulte também [Desenvolvimento - Práticas recomendadas](/help/sites-developing/best-practices.md).

## Recursos adicionais {#further-resources}

Para obter informações completas sobre o desenvolvimento AEM consulte a coleta de recursos em:

* [Guia do usuário de desenvolvimento](/help/sites-developing/home.md)
* [Documentação da interface de usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites - Tutorials e vídeos](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Introdução ao desenvolvimento do AEM Sites - Tutorial de WKND](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Ferramentas de Modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM As Ferramentas de Modernização são um esforço da comunidade e não são compatíveis ou garantidas pelo Adobe.

