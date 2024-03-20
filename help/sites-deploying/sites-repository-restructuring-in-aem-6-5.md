---
title: Reestruturação do repositório de sites no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura do repositório no AEM 6.5 para Sites.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 1%

---

# Reestruturação do repositório de sites no AEM 6.5 {#sites-repository-restructuring-in-aem}

Conforme descrito no pai [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) , os clientes que estiverem atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a solução da AEM Sites. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com atualização para 6.5**

* [Segmentos ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Antes de uma atualização futura**

* [Bibliotecas de clientes do Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Designs Clássicos de Word para Página da Web do Microsoft](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurações do emulador de dispositivo móvel](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurações do blueprint do gerenciador de vários sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurações de implantação do gerenciador de vários sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modelo de e-mail de notificação de eventos de página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Scaffolding da página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Grade responsiva LESS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Designs de modelos estáticos](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Bibliotecas de clientes de integração do Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliotecas de clientes do WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Com atualização para 6.5 {#with-upgrade}

### Segmentos ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Se algum segmento novo ou modificado do ContextHub for editado no controle do código-fonte em vez de ser editado no AEM, ele deverá ser migrado para o novo local:</p>
    <ol>
     <li>Copie todos os segmentos do ContextHub novos ou modificados do local anterior para o novo local apropriado (/<code>apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Atualizar referências a segmentos do ContextHub no local anterior para os segmentos do ContextHub migrados nos novos locais (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>A consulta do QueryBuilder a seguir localiza todas as referências aos segmentos do ContextHub nos Locais anteriores.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Isso pode ser executado via <a href="/help/sites-developing/querybuilder-api.md" target="_blank">Interface do usuário do depurador AEM QueryBuilder</a>. Observe que esta é uma consulta de percurso, portanto, não a execute em relação à produção e garanta limites de percurso ajustados conforme necessário.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os segmentos do ContextHub persistiram na exibição do local anterior como somente leitura no <strong>AEM &gt; Personalização &gt; Públicos</strong>.</p> <p>Se os segmentos do ContextHub forem editáveis no AEM, eles devem ser migrados para o novo local (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>). Quaisquer novos segmentos do ContentHub criados no AEM serão mantidos no novo local (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p> <p>As Propriedades da página do AEM Sites permitem apenas o Local anterior (<code>/etc</code>) ou um único local novo (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>) para serem selecionados, portanto, os Segmentos do ContextHub devem ser migrados de acordo.</p> <p>Todos os segmentos do ContextHub não utilizados dos sites de referência do AEM podem ser removidos e não migrados para o Novo local:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Observação: se o ClientContext estiver em uso, é recomendável converter para o ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de uma atualização futura {#prior-to-upgrade}

### Bibliotecas de clientes do Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas bibliotecas de clientes deve fazer referência à biblioteca do cliente por categoria, e não por caminho:</p>
    <ol>
     <li>Todas as referências à Biblioteca do cliente por caminho no Local anterior devem ser atualizadas para uso <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Estrutura de referência da Biblioteca do cliente AEM</a>.</li>
     <li>Se a estrutura de referência da Biblioteca do cliente AEM não puder ser usada, o caminho absoluto das Bibliotecas do cliente poderá ser referenciado por meio do servlet AEM Client Library Proxy.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A edição dessas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca do cliente, visite cada <code>cq:ClientLIbraryFolder</code> nó via CRXDELite e inspecione a propriedade categories.</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Designs Clássicos de Word para Página da Web do Microsoft {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (<code>/apps</code>).</li>
     <li>Converter qualquer CSS, JavaScript e recursos estáticos no Design em um <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize as referências para o Local anterior na propriedade cq:designPath.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras do Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do <code>/etc.clientlibs/</code> servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução via caixas de diálogo de design:</p>
    <ul>
     <li>Não remova os designs editáveis do <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações do emulador de dispositivo móvel {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>Quaisquer novas configurações do emulador de dispositivo móvel devem ser migradas para o novo local.
    <ol>
     <li>Copie todas as novas configurações do emulador de dispositivo móvel do local anterior para o novo local (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Para quaisquer Páginas do AEM Sites que dependam dessas Configurações do emulador de dispositivo móvel, atualize o do <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> nó: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ móvel/grupos/responsivo ]</span></li>
     <li>Para todos os Modelos editáveis que dependem dessas Configurações do emulador de dispositivo móvel, atualize os Modelos editáveis, apontando para a <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> para o Novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução Configurações do emulador do dispositivo móvel ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Configurações do blueprint do gerenciador de vários sites {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/apps/msm</code> (Configurações do blueprint do cliente)</p> <p><code>/libs/msm</code> (Configurações do blueprint prontas para uso do Screens, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer configurações de blueprint do gerenciador de vários sites novas ou modificadas devem ser migradas para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Copie todas as configurações de blueprint do gerenciador de vários sites novas ou modificadas do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Remova todas as configurações de blueprint do gerenciador de vários sites migradas do local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Todas as configurações de blueprint do gerenciador de vários sites fornecidas pelo AEM existem no novo local em <code>/libs</code>.</p> <p>O conteúdo não faz referência às Configurações azuis do gerenciador de vários sites, portanto, não há referências de conteúdo a serem ajustadas.</p> </td>
  </tr>
 </tbody>
</table>

### Configurações de implantação do gerenciador de vários sites {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer configurações de implementação de gerenciador de vários sites novas ou modificadas devem ser migradas para o novo local.</p>
    <ol>
     <li>Copie todas as configurações de implantação do gerenciador de vários sites novas ou modificadas do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Atualize todas as referências nas Páginas AEM para as Configurações de implantação do gerenciador de vários sites no local anterior, para apontar para seus equivalentes nos Novos locais (<code>/libs</code> ou <code>/apps</code>).</li>
    </ol> <p>Remova as Configurações de implantação do gerenciador de vários sites migradas do local anterior.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Falha ao remover as configurações de implantação do gerenciador de vários sites migradas do local anterior resulta na exibição de opções de implantação duplicadas para autores de AEM.</td>
  </tr>
 </tbody>
</table>

### Modelo de e-mail de notificação de eventos de página {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Os únicos novos Modelos de e-mail de notificação de eventos de página compatíveis são os novos locais.</p> <p>A resolução do Modelo de e-mail de evento de página ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Todos os modelos de e-mail de notificação de eventos de página novos ou modificados devem ser migrados para o novo local em <code>/apps</code>:</p>
    <ol>
     <li>Copie todos os modelos de e-mail de notificação de eventos de página novos ou modificados do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Remova todos os modelos de e-mail de notificação de eventos de página migrados do local anterior.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Scaffolding da página {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>O scaffolding criado no Local anterior usa a estrutura de scaffolding herdada e não pode ser migrado para o Novo local. Para alinhar com o novo local, qualquer andaime herdado deve ser recriado usando a estrutura de andaime compatível.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Grade responsiva LESS {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer referência ao Local anterior em arquivos LESS personalizados deve ser atualizada para importar do Novo Local.</p>
    <ul>
     <li>Atualize qualquer arquivo LESS personalizado que faça referência a grid_base.less no Local anterior para fazer referência ao novo local.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Referência a um não existente <code>grid_base.less</code> O arquivo faz com que o Modo de layout da página e o Editor de modelo não funcionem e causa uma interrupção no layout da página.</td>
  </tr>
 </tbody>
</table>

### Designs de modelos estáticos {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (<code>/apps</code>).</li>
     <li>Converter qualquer CSS, JavaScript e recursos estáticos no Design em um <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local anterior na <code>cq:designPath</code> propriedade via <strong>AEM &gt; Sites &gt; Páginas do site personalizadas &gt; Propriedades da página &gt; Guia Avançado &gt; Campo de design</strong>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras do Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do <code>/etc.clientlibs/</code> servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução via caixas de diálogo de design:</p>
    <ul>
     <li>Não remova os designs editáveis do <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>A abordagem recomendada é criar AEM Sites e Páginas usando Modelos editáveis que usam Conteúdo e políticas de estrutura no lugar de Designs.</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Bibliotecas de clientes de integração do Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas bibliotecas de clientes deve fazer referência à biblioteca do cliente por categoria, e não por caminho.</p>
    <ol>
     <li>Todas as referências à Biblioteca do cliente por caminho no Local anterior devem ser atualizadas para uso <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Estrutura de referência da Biblioteca do cliente AEM</a>.</li>
     <li>Se a estrutura de referência da Biblioteca do cliente AEM não puder ser usada, o caminho absoluto das Bibliotecas do cliente poderá ser referenciado por meio do servlet AEM Client Library Proxy:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A edição dessas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca do cliente, visite cada nó cq:ClientLIbraryFolder via CRXDELite e inspecione a propriedade categories:</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliotecas de clientes do WCM Foundation {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas bibliotecas de clientes deve fazer referência à biblioteca do cliente por categoria, e não por caminho.</p>
    <ol>
     <li>Todas as referências à Biblioteca do cliente por caminho no Local anterior devem ser atualizadas para uso <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Estrutura de referência da Biblioteca do cliente AEM</a>.</li>
     <li>Se a estrutura de referência da Biblioteca do cliente AEM não puder ser usada, o caminho absoluto das Bibliotecas do cliente poderá ser referenciado por meio do servlet AEM Client Library Proxy.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A edição dessas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca do cliente, visite cada <code>cq:ClientLIbraryFolder</code> por meio do CRXDELite e inspecione a propriedade categories:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
