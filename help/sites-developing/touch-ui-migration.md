---
title: Migração para a interface de toque
description: Saiba mais sobre a migração do Adobe Experience Manager para a interface para toque e como ela afeta você.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 5%

---

# Migração para a interface de toque{#migration-to-the-touch-ui}

A partir da versão 6.0, o Adobe Experience Manager (AEM) apresentou uma nova interface de usuário chamada de *interface habilitada para toque* (também conhecido simplesmente como *interface de toque*). Ele está alinhado à Adobe Experience Cloud e às diretrizes gerais da interface do usuário do Adobe. Essa se tornou a interface padrão no AEM, com a interface herdada, orientada para desktop, chamada de *IU clássica*.

Se você tem usado o AEM com a interface clássica, execute uma ação para migrar sua instância. Esta página serve como um trampolim, fornecendo links para recursos individuais.

>[!NOTE]
>
>Esse projeto de migração pode ter impacto significativo na sua instância. Consulte [Gerenciamento de projetos - Práticas recomendadas](/help/managing/best-practices.md) para obter as diretrizes recomendadas.

## Noções básicas {#the-basics}

Ao migrar, esteja ciente das principais diferenças a seguir entre a interface clássica e a interface para toque:

<table>
 <tbody>
  <tr>
   <td>IU Clássica</td>
   <td>Interface de usuário habilitada para toque</td>
  </tr>
  <tr>
   <td>É descrito no repositório JCR como uma estrutura de nós. Cada nó que representa um elemento da interface do usuário é chamado de um <em>Widget ExtJS</em> e renderizado no lado do cliente por <code>ExtJS</code>.</td>
   <td>Também descrito no repositório JCR como uma estrutura de nós. No entanto, nesse caso, cada nó se refere a um tipo de recurso Sling (componente Sling), responsável pela renderização. Portanto, a interface do usuário é (basicamente) renderizada no lado do servidor.</td>
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
     <li>As peças imperativas são incorporadas diretamente usando ouvintes ou gerenciadas em clientlibs.</li>
    </ul> </td>
   <td><p>Localização do JavaScript:</p>
    <ul>
     <li>Partes imperativas não podem ser incorporadas na definição do diálogo; separação de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Manipulação de eventos:</p>
    <ul>
     <li>Os widgets de diálogo fazem referência direta ao código JavaScript.</li>
    </ul> </td>
   <td><p>Manipulação de eventos:</p>
    <ul>
     <li>O JavaScript observa eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Renderização feita pelo cliente:
    <ul>
     <li>O cliente cria dinamicamente os componentes da interface.</li>
     <li>Definição de componente (Pull) de solicitações do cliente (como JSON) do servidor.</li>
    </ul> </td>
   <td>Renderização feita pelo servidor:
    <ul>
     <li>O cliente solicita páginas junto com a interface relacionada.</li>
     <li>O servidor envia (push) a interface do usuário como documentos de HTML; usando componentes de Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Em outras palavras, migrar uma seção da interface do usuário da interface clássica para a interface do usuário de toque significa portar um *Widget ExtJS* para um *Componente do Sling*. Para facilitar isso, a interface de toque é baseada na estrutura da interface de usuário do Granite, que já fornece alguns componentes do Sling para a interface de usuário (conhecidos como componentes da interface de usuário do Granite).

Antes de começar, verifique o status e as recomendações relacionadas:

* [Status dos recursos da interface de toque](/help/release-notes/touch-ui-features-status.md)
* [Interface do usuário do Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

As noções básicas para o desenvolvimento da interface para toque fornecem uma base sólida:

* [Conceitos da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estrutura da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-structure.md)

## Migração da criação de página {#migrating-page-authoring}

As caixas de diálogo são um fator importante ao migrar seus componentes:

* [Desenvolvimento de componentes do AEM](/help/sites-developing/developing-components.md) (com a interface habilitada para toque)
* [Migração de um componente clássico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Ferramentas de modernização do AEM](/help/sites-developing/modernization-tools.md) - para ajudá-lo a converter as caixas de diálogo dos componentes da interface clássica para a interface de toque

   * Há uma camada de compatibilidade na interface para toque para abrir uma caixa de diálogo da interface clássica em um &quot;invólucro da interface para toque&quot;, mas essa funcionalidade é limitada e não é recomendada para longo prazo.

* [Personalização de campos de caixa de diálogo na interface para toque](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Criação de um novo componente de campo da interface de usuário do Granite](/help/sites-developing/granite-ui-component.md)
* [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md) (com a interface habilitada para toque)

## Migração de Consoles {#migrating-consoles}

Você também pode personalizar os consoles:

* [Personalização dos Consoles](/help/sites-developing/customizing-consoles-touch.md) (para a interface habilitada para toque)

## Considerações relacionadas {#related-considerations}

Embora não esteja diretamente relacionado a uma migração para a interface de toque, há problemas relacionados que merecem ser considerados ao mesmo tempo, pois também são uma prática recomendada:

* [Modelos](/help/sites-developing/templates.md) - [Modelos editáveis](/help/sites-developing/page-templates-editable.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR)

>[!NOTE]
>
>Consulte também [Desenvolvimento - Práticas recomendadas](/help/sites-developing/best-practices.md).

## Recursos adicionais {#further-resources}

Para obter informações completas sobre o desenvolvimento do AEM, consulte a coleta de recursos em:

* [Guia do usuário para desenvolvimento](/help/sites-developing/home.md)
* [Documentação da interface de usuário do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Sites Tutorials e vídeos](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [Introdução ao desenvolvimento do AEM Sites - Tutorial de WKND](/help/sites-developing/getting-started.md)
* [Gems AEM](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=en)
* [Ferramentas de Modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>As Ferramentas de Modernização do AEM são um esforço da comunidade e não são suportadas ou garantidas pelo Adobe.
