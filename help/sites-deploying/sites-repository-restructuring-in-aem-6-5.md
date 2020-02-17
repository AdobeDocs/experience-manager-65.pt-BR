---
title: Reestruturação do repositório do Sites no AEM 6.5
seo-title: Reestruturação do repositório do Sites no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 for Sites.
seo-description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 for Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Reestruturação do repositório do Sites no AEM 6.5 {#sites-repository-restructuring-in-aem}

Conforme descrito na página principal [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) , os clientes que atualizam para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a solução AEM Sites. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com atualização 6.5**

* [Segmentos ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Antes da atualização futura**

* [Bibliotecas de clientes do Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Designs clássicos do Microsoft Word para página da Web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurações do emulador de dispositivo móvel](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurações de Blueprint do Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurações de implantação do Multi-site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modelo de email de notificação de evento de página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Andaime da página](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Grade responsiva MENOS](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Modelos estáticos de modelos](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Bibliotecas do cliente de integração do Adobe Search and Promote](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Bibliotecas do cliente de integração do Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Bibliotecas de clientes do WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Com atualização 6.5 {#with-upgrade}

### Segmentos ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Se algum segmento novo ou modificado do ContextHub for destinado a ser editado no controle de origem em vez de ser editado no AEM, ele deverá ser migrado para o novo local:</p>
    <ol>
     <li>Copiar quaisquer segmentos do ContextHub novos ou modificados do local anterior para o novo local apropriado (/<code>apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Atualize as referências aos segmentos do ContextHub no local anterior para os segmentos do ContextHub migrados nos novos locais (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>A consulta do QueryBuilder a seguir localiza todas as referências aos segmentos do ContextHub nos locais anteriores.<br /> <br /><code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> Isso pode ser executado por meio da interface do usuário <br /> do Depurador do <a href="/help/sites-developing/querybuilder-api.md" target="_blank"></a>AEM QueryBuilder. Observe que esta é uma consulta transversal, portanto, não a execute na produção e verifique se os limites transversais estão ajustados conforme necessário.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os segmentos do ContextHub persistiram até o local anterior serem exibidos como somente leitura em <strong>AEM &gt; Personalização &gt; Públicos</strong>.</p> <p>Se os segmentos do ContextHub forem editáveis no AEM, eles deverão ser migrados para o novo local (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>). Todos os novos segmentos do ContentHub criados no AEM são persistentes para o novo local (<code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p> <p>As Propriedades da página do AEM Sites permitem apenas que o Local anterior (<code>/etc</code>) ou um único novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>) seja selecionado, portanto, os segmentos do ContextHub devem ser migrados de acordo.</p> <p>Todos os segmentos do ContextHub não utilizados dos sites de referência do AEM podem ser removidos e não migrados para o novo local:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Observação: Se ClientContext estiver em uso, é recomendável converter em ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Antes da atualização futura {#prior-to-upgrade}

### Bibliotecas de clientes do Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas Bibliotecas de clientes deve fazer referência à Biblioteca de clientes por categoria e não por caminho:</p>
    <ol>
     <li>Quaisquer referências à Biblioteca de clientes por caminho no Local anterior devem ser atualizadas para usar a estrutura de referência <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">da Biblioteca de clientes do</a>AEM.</li>
     <li>Se a estrutura de referência da Biblioteca do cliente do AEM não puder ser usada, o caminho absoluto das Bibliotecas do cliente poderá ser referenciado pelo servlet Proxy da biblioteca do cliente do AEM.
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
   <td><p>A edição destas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca de clientes, visite cada <code>cq:ClientLIbraryFolder</code> nó via CRXDELite e inspecione a propriedade category.</p>
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

### Designs clássicos do Microsoft Word para página da Web {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado no SCM e não gravado em tempo de execução por meio das Caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma Biblioteca <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">do</a> cliente com <code>allowProxy = true</code>.</li>
     <li>Atualize as referências ao Local anterior na propriedade cq:designPath.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca do cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras do AEM Dispatcher para permitir o serviço de bibliotecas do cliente por meio do servlet <code>/etc.clientlibs/</code> proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e tempo de execução modificado por meio das Caixas de diálogo de design:</p>
    <ul>
     <li>Não remova os Designs que podem ser criados para autores de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações do emulador de dispositivo móvel {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>Todas as novas configurações do emulador de dispositivos móveis devem ser migradas para o novo local.
    <ol>
     <li>Copie quaisquer novas Configurações do emulador de dispositivo móvel do local anterior para o novo local (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Para qualquer página do AEM Sites que dependa dessas configurações do emulador de dispositivos móveis, atualize o <span class="code">nó da página <code>
        jcr
       </code><code>
        :content
       </code></span> : <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Para qualquer Modelo editável que dependa dessas Configurações do emulador de dispositivo móvel, atualize os Modelos editáveis, apontando para <span class="code"><code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> para o novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução das Configurações do emulador de dispositivo móvel ocorre na seguinte ordem:</p>
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

### Configurações de Blueprint do Multi-site Manager {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/apps/msm</code> (Configurações de Blueprint do cliente)</p> <p><code>/libs/msm</code> (Configurações do out of the Box Blueprint para Screens, Comércio)</p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as configurações Blueprint do Multi-site Manager novas ou modificadas devem ser migradas para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Copie quaisquer Configurações Blueprint do Gerenciador de vários sites novas ou modificadas do Local anterior para o novo local (<code>/apps</code>).</li>
     <li>Remova todas as configurações de Blueprint do Multi-site Manager migradas do Local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Todas as Configurações de Blueprint do Gerenciador de vários sites fornecidas pelo AEM existem no novo local em <code>/libs</code>.</p> <p>O conteúdo não faz referência às Configurações azuis do Multi-site Manager, portanto, não há referências de conteúdo para ajustar.</p> </td>
  </tr>
 </tbody>
</table>

### Configurações de implantação do Multi-site Manager {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Quaisquer Configurações de implantação do Multi-site Manager novas ou modificadas devem ser migradas para o novo local.</p>
    <ol>
     <li>Copie quaisquer Configurações de implantação do Multi-site Manager novas ou modificadas do Local anterior para o novo local (<code>/apps</code>).</li>
     <li>Atualize quaisquer referências em Páginas AEM para Configurações de implantação do Multi-site Manager no Local anterior, para apontar para seus homólogos em Novos locais (<code>/libs</code> ou <code>/apps</code>).</li>
    </ol> <p>Remova as Configurações de implantação do Multi-site Manager migradas do Local anterior.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Falha ao remover as Configurações de implantação do Multi-site Manager migradas do Local anterior resulta em opções de implantação duplicadas exibidas aos autores do AEM.</td>
  </tr>
 </tbody>
</table>

### Modelo de email de notificação de evento de página {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Os únicos modelos de e-mail de notificação de evento de página suportados são para suportar novas localidades.</p> <p>A resolução do modelo de e-mail do evento da página ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Todos os modelos de e-mail de notificação de evento de página novos ou modificados devem ser migrados para o novo local em <code>/apps</code>:</p>
    <ol>
     <li>Copie todos os modelos de e-mail de notificação de evento de página novos ou modificados do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Remova todos os modelos de e-mail de notificação de evento de página migrados do local anterior.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Andaime da página {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><span class="code">/libs/settings/ <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/ <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>Os andaimes criados no Local anterior usam a estrutura de andaimes herdada e não podem ser migrados para o novo local. Para alinhar com o novo local, qualquer Andaime herdado deve ser redesenvolvido usando a estrutura Scaffolding compatível.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Grade responsiva MENOS {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Quaisquer referências ao Local anterior em arquivos MENOS personalizados devem ser atualizadas para importar do Novo local.</p>
    <ul>
     <li>Atualize quaisquer arquivos LESS personalizados que façam referência a grid_base.less no Local anterior para fazer referência ao novo local.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>A referência a um <code>grid_base.less</code> arquivo não existente resulta no Modo de layout da página e no Editor de modelos que não funcionam, além de uma interrupção no layout da página.</td>
  </tr>
 </tbody>
</table>

### Modelos estáticos de modelos {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado no SCM e não gravado em tempo de execução por meio das Caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma Biblioteca <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">do</a> cliente com <code>allowProxy = true</code>.</li>
     <li>Atualize as referências ao Local anterior na <code>cq:designPath</code> propriedade por meio de <strong>AEM &gt; Sites &gt; Páginas personalizadas do site &gt; Propriedades da página &gt; Guia Avançado &gt; Campo</strong>de design.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca do cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras do AEM Dispatcher para permitir o serviço de Bibliotecas do cliente por meio do servlet <code>/etc.clientlibs/</code> proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e tempo de execução modificado por meio das Caixas de diálogo de design:</p>
    <ul>
     <li>Não remova os Designs que podem ser criados para autores de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>A abordagem recomendada é criar sites e páginas do AEM usando modelos editáveis que usam conteúdo de estrutura e políticas em vez de designs.</td>
  </tr>
 </tbody>
</table>

### Bibliotecas do cliente de integração do Adobe Search and Promote {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas Bibliotecas de clientes deve fazer referência à Biblioteca de clientes por categoria e não por caminho.</p>
    <ol>
     <li>Quaisquer referências à Biblioteca de clientes por caminho no Local anterior devem ser atualizadas para usar a estrutura de referência <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">da Biblioteca de clientes do</a>AEM.</li>
     <li>Se a estrutura de referência da Biblioteca de clientes do AEM não puder ser usada, o caminho absoluto das Bibliotecas de clientes poderá ser referenciado pelo servlet Proxy da biblioteca de clientes do AEM:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A edição destas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca de clientes, visite cada nó cq:ClientLIbraryFolder via CRXDELite e inspecione a propriedade de categorias:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Bibliotecas do cliente de integração do Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas Bibliotecas de clientes deve fazer referência à Biblioteca de clientes por categoria e não por caminho.</p>
    <ol>
     <li>Quaisquer referências à Biblioteca de clientes por caminho no Local anterior devem ser atualizadas para usar a estrutura de referência <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">da Biblioteca de clientes do</a>AEM.</li>
     <li>Se a estrutura de referência da Biblioteca de clientes do AEM não puder ser usada, o caminho absoluto das Bibliotecas de clientes poderá ser referenciado pelo servlet Proxy da biblioteca de clientes do AEM:</li>
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
   <td><p>A edição destas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca de clientes, visite cada nó cq:ClientLIbraryFolder via CRXDELite e inspecione a propriedade de categorias:</p>
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
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer uso personalizado dessas Bibliotecas de clientes deve fazer referência à Biblioteca de clientes por categoria e não por caminho.</p>
    <ol>
     <li>Quaisquer referências à Biblioteca de clientes por caminho no Local anterior devem ser atualizadas para usar a estrutura de referência <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">da Biblioteca de clientes do</a>AEM.</li>
     <li>Se a estrutura de referência da Biblioteca do cliente do AEM não puder ser usada, o caminho absoluto das Bibliotecas do cliente poderá ser referenciado pelo servlet Proxy da biblioteca do cliente do AEM.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A edição destas bibliotecas de clientes nunca foi suportada.</p> <p>Para obter as categorias da Biblioteca de clientes, visite cada <code>cq:ClientLIbraryFolder</code> nó via CRXDELite e inspecione a propriedade de categorias:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

