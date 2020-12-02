---
title: Migração para a interface de usuário de toque
seo-title: Migração para a interface de usuário de toque
description: Migração para a interface de usuário de toque
seo-description: Migração para a interface de usuário de toque
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 6%

---


# Migração para a interface de usuário de toque{#migration-to-the-touch-ui}

A partir da versão 6.0, a Adobe Experience Manager (AEM) introduziu uma nova interface de usuário chamada *interface de usuário habilitada para toque* (também conhecida simplesmente como *interface de usuário de toque*). Ele está alinhado ao Adobe Marketing Cloud e às diretrizes gerais da interface do usuário do Adobe. Essa interface se tornou a interface padrão em AEM com a interface legada orientada para desktop, chamada *interface clássica*.

Se você tiver usado AEM com a interface clássica, precisará tomar medidas para migrar sua instância. Esta página tem como objetivo agir como trampolim, fornecendo links para recursos individuais.

>[!NOTE]
>
>Esse projeto de migração pode ter um impacto significativo em sua instância. Consulte [Gerenciar projetos - Práticas recomendadas](/help/managing/best-practices.md) para obter as diretrizes recomendadas.

## Noções básicas {#the-basics}

Ao migrar, você deve estar ciente das seguintes (principais) diferenças entre a interface clássica e a interface de toque:

<table>
 <tbody>
  <tr>
   <td>Interface do usuário clássica</td>
   <td>Interface do usuário habilitada para toque</td>
  </tr>
  <tr>
   <td>É descrito no repositório JCR como uma estrutura de nós. Todos os nós que representam um elemento da interface de usuário são chamados de <em>widget ExtJS</em> e renderizados no lado do cliente por <code>ExtJS</code>.</td>
   <td>Também descrito no repositório JCR como uma estrutura de nós. No entanto, nesse caso, cada nó se refere a um tipo de recurso Sling (componente Sling), que é responsável pela renderização. Portanto, a interface do usuário é (basicamente) renderizada no servidor.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>not used</li>
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
     <li>jcr:PrimaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Localização do Javascript:</p>
    <ul>
     <li>As peças imperiativas são incorporadas diretamente usando ouvintes ou gerenciadas em clientlibs.</li>
    </ul> </td>
   <td><p>Localização do Javascript:</p>
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
   <td>Renderização realizada pelo cliente:
    <ul>
     <li>O cliente cria dinamicamente os componentes da interface do usuário.</li>
     <li>A definição do componente de solicitações do cliente (Pull) (como JSON) do servidor.</li>
    </ul> </td>
   <td>Renderização realizada pelo servidor:
    <ul>
     <li>O cliente solicita páginas juntamente com a interface relacionada.</li>
     <li>O servidor envia (envia) a interface do usuário como documentos HTML; usando componentes da interface do usuário do Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Em outras palavras, a migração de uma seção da interface do usuário da interface clássica para a interface do usuário de toque significa portar um *widget ExtJS* para um *componente Sling*. Para facilitar isso, a interface de usuário de toque é baseada na estrutura da interface de usuário Granite, que já fornece alguns componentes Sling para a interface de usuário (conhecidos como componentes da interface de usuário Granite).

Antes do start, verifique o status e as recomendações relacionadas:

* [Status dos recursos da interface de toque](/help/release-notes/touch-ui-features-status.md)
* [Interface do usuário Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

As noções básicas para desenvolver a interface de usuário de toque fornecerão uma base sólida:

* [Conceitos da interface de usuário habilitada para toque AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estrutura da interface habilitada para toque AEM](/help/sites-developing/touch-ui-structure.md)

## Migração de criação de página {#migrating-page-authoring}

As caixas de diálogo são um fator importante ao migrar seus componentes:

* [Desenvolvimento de componentes](/help/sites-developing/developing-components.md)  AEM (com a interface habilitada para toque)
* [Migração de um componente clássico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Ferramenta](/help/sites-developing/dialog-conversion.md)  de conversão de diálogo - para ajudar a converter as caixas de diálogo dos componentes clássicos da interface do usuário para tocar na interface do usuário

   * Há uma camada de compatibilidade na interface de usuário de toque para abrir uma caixa de diálogo clássica dentro de um &quot;invólucro de interface de toque&quot;, mas isso tem funcionalidade limitada e não é recomendado para o longo prazo.

* [Personalização de campos de diálogo na interface de usuário de toque](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Criando um novo componente de campo da interface do usuário do Granite](/help/sites-developing/granite-ui-component.md)
* [Personalização da criação](/help/sites-developing/customizing-page-authoring-touch.md)  de página (com a interface habilitada para toque)

## Migração de consoles {#migrating-consoles}

Você também pode personalizar os consoles:

* [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md)  (para a interface habilitada para toque)

## Considerações relacionadas {#related-considerations}

Embora não estejam diretamente relacionados a uma migração para a interface de usuário de toque, há problemas relacionados que vale a pena considerar ao mesmo tempo, já que eles também são a prática recomendada:

* [Modelos](/help/sites-developing/templates.md)  - Modelos  [editáveis](/help/sites-developing/page-templates-editable.md)
* [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>Consulte também [Desenvolvimento - Práticas recomendadas](/help/sites-developing/best-practices.md).

## Outros recursos {#further-resources}

Para obter informações completas sobre o desenvolvimento AEM consulte a coleta de recursos em:

* [Guia do usuário de desenvolvimento](/help/sites-developing/home.md)
* [Documentação da interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 Tutorials e vídeos do Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [Introdução ao desenvolvimento do AEM Sites - Tutorial de WKND](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [Ferramentas de Modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM As Ferramentas de Modernização são um esforço comunitário e não são suportadas nem garantidas pela Adobe.

