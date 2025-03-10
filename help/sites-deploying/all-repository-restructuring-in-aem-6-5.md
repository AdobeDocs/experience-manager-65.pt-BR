---
title: Reestruturação do repositório comum no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura do repositório no AEM 6.5, que são comuns para todas as áreas do AEM.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
solution: Experience Manager, Experience Manager Sites
feature: Upgrading
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2694'
ht-degree: 2%

---

# Reestruturação do repositório comum no AEM 6.5 {#common-repository-restructuring-in-aem}

Conforme descrito na página pai [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que estão atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que podem afetar todas as soluções. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com Atualização 6.5**

* [Configurações do ContextHub](#contexthub-6.5)
* [Instâncias do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelos do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Inicializadores do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Scripts de fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Antes de uma atualização futura**

* [Configurações do ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Designs de Cloud Service clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Designs de painéis clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Designs de relatórios clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Designs padrão](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Ponto de extremidade do Adobe DTM JavaScript](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Ponto de extremidade do gancho da Web do Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tarefas da Caixa de entrada](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurações do blueprint do gerenciador de vários sites](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurações de gadget do painel de projetos AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modelo de e-mail de notificação de replicação](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Tags](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Idiomas para tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Regras de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Biblioteca cliente do widget de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console da Web de ativação da árvore](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Service do conector de tradução do fornecedor](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modelos de email de notificação de fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Com atualização para 6.5 {#with-upgrade}

### Configurações do ContextHub {#contexthub-6.5}

A partir do AEM 6.4, não há configuração padrão do ContextHub. Portanto, no nível raiz do site, um `cq:contextHubPathproperty` deve ser definido para indicar qual configuração deve ser usada.

1. Navegue até a raiz do site.
1. Abra as propriedades de página da página raiz e selecione a guia Personalization.
1. No campo Caminho do Contexthub, insira seu próprio caminho de configuração do ContextHub.

Além disso, na configuração do ContextHub, `sling:resourceType` precisa ser atualizado para ser relativo e não absoluto.

1. Abra as propriedades do nó de configuração do ContextHub no CRX DE Lite, por exemplo, `/apps/settings/cloudsettings/legacy/contexthub`
1. Alterar `sling:resourceType` de `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` para `granite/contexthub/cloudsettings/components/baseconfiguration`

Ou seja, o `sling:resourceType` da configuração do ContextHub deve ser relativo em vez de absoluto.

### Modelos do fluxo de trabalho {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer modelo de fluxo de trabalho novo ou modificado deve ser migrado para /conf/global/workflow/models.</p>
    <ol>
     <li>Implante os Modelos de fluxo de trabalho modificados em uma instância de desenvolvimento local do AEM 6.5, de modo que eles existam no local Anterior.</li>
     <li>Edite o modelo de fluxo de trabalho usando o Editor de modelo de fluxo de trabalho do AEM em AEM &gt; Ferramentas &gt; Fluxo de trabalho &gt; Modelos.</li>
     <li>Ao migrar modelos de fluxo de trabalho modificados e fornecidos pelo AEM
      <ol>
       <li>Com o Editor de modelos de fluxo de trabalho aberto, modifique o URL de endereço do navegador e substitua o segmento de caminho /libs/settings/workflow/models por /etc/workflow/models.
        <ul>
         <li>Por exemplo, altere: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> para <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Habilite o modo Editar no Editor de modelo de fluxo de trabalho que copiará a definição do Modelo de fluxo de trabalho para /conf/global/workflow/models.</li>
     <li>Selecione o botão Sincronizar para sincronizar as alterações no Modelo de fluxo de trabalho de tempo de execução em /var/workflow/models.</li>
     <li>Exporte o Modelo de fluxo de trabalho (/conf/global/workflow/models/&lt;workflow-model&gt;) e o Modelo de fluxo de trabalho em tempo de execução (/var/workflow/models/&lt;workflow-model&gt;) e integre-se ao projeto do AEM.
      <ol>
       <li>Por exemplo, exportar:
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> e </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do modelo de fluxo de trabalho ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Assim, todas as personalizações de modelos de fluxo de trabalho fornecidos pelo AEM persistentes no local anterior devem ser movidas para /conf/global/settings/workflow/models se forem retidas, caso contrário, elas serão substituídas pela definição de Modelo de fluxo de trabalho fornecida pelo AEM em /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Instâncias do fluxo de trabalho {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Nenhuma ação é necessária para alinhar com o Novo local.</p> <p>As Instâncias de fluxo de trabalho históricas podem continuar residindo no Local anterior com segurança, e novas Instâncias de fluxo de trabalho serão criadas no Novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Qualquer referência de caminho explícita em
    O código <code>
     custom
    </code> para o Local Anterior também deve contabilizar o Novo Local. Recomenda-se que esse código seja refatorado para usar as APIs de fluxo de trabalho do AEM.</td>
  </tr>
 </tbody>
</table>

### Inicializadores do fluxo de trabalho {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer Inicializador de Fluxo de Trabalho novo ou modificado deve ser migrado para <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copie todas as configurações novas ou modificadas do Inicializador do Fluxo de Trabalho do Local Anterior para o Novo Local (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do Iniciador do fluxo de trabalho ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Assim, todas as personalizações do Iniciador de Fluxo de Trabalho fornecidas pelo AEM que persistam no local Anterior devem ser movidas para o Novo Local (<code>/conf/global/settings/workflow/launcher</code>), caso contrário, serão substituídas pela definição do Iniciador de Fluxo de Trabalho fornecida pelo AEM em <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts de fluxo de trabalho {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer scripts de fluxo de trabalho novos ou modificados devem ser migrados para o Novo local e os Modelos de fluxo de trabalho de referência devem ser atualizados para refletir o Novo local.</p>
    <ol>
     <li>Copie todos os Scripts de Fluxo de Trabalho novos ou modificados do Local Anterior para o Novo Local.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> deve ser mantido no SCM.</li>
      </ul> </li>
     <li>Atualize todas as referências aos Scripts de fluxo de trabalho no Local anterior em Modelos de fluxo de trabalho para apontar para Novos locais.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>O AEM 6.4 SP1, quando é liberado, faz com que essa reestruturação possa ser adiada até o 6.5
     <code>
      upgrade
     </code>.</p> <p>Se a atualização para o AEM 6.4 antes do lançamento do AEM 6.4 SP1, essa reestruturação deve ser realizada como parte do projeto de atualização. Sem fazer isso, editar e salvar as Etapas do fluxo de trabalho que fazem referência a scripts no Local anterior removerá completamente a referência de Script de fluxo de trabalho da Etapa do fluxo de trabalho, e somente os Scripts de fluxo de trabalho em Novos locais estarão disponíveis na lista suspensa de seleção de script.</p> </td>
  </tr>
 </tbody>
</table>

## Antes de uma atualização futura {#prior-to-upgrade}

### Configurações do ContextHub {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer configurações novas ou modificadas do ContextHub devem ser migradas para o novo local e as páginas do AEM Sites de referência devem ser atualizadas para refletir o novo local.</p>
    <ol>
     <li>Copie todas as configurações novas ou modificadas do ContextHub do local anterior para o novo local.</li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo de AEM.
      <ol>
       <li><strong>Hierarquias de página do AEM Sites via AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
      </ol> </li>
     <li>Desassocie quaisquer configurações herdadas do ContextHub migradas das hierarquias de conteúdo do AEM acima.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Designs de Cloud Service clássicos {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local Anterior para o Novo Local (<code>/apps</code>).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de Clientes</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências para o Local Anterior no <span class="code">
       <code>
        cq
       </code>:
       Propriedade <code>
        designPath
       </code></span>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras de Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução através de caixas de diálogo de design.</p>
    <ul>
     <li>Não mova designs habilitados para o autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Designs de painéis clássicos {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de Clientes</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local anterior na
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras de Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução através de caixas de diálogo de design.</p>
    <ul>
     <li>Não mova designs habilitados para o autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Designs de relatórios clássicos {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de Clientes</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local anterior na
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras de Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução através de caixas de diálogo de design.</p>
    <ul>
     <li>Não mova designs habilitados para o autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Designs padrão {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de Clientes</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local anterior na
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras de Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução através de caixas de diálogo de design.</p>
    <ul>
     <li>Não mova designs habilitados para o autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Ponto de extremidade do Adobe DTM JavaScript {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Nenhuma ação necessária.</p> <p>O local público anterior atua como um endpoint de proxy para o novo local privado.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Ponto de extremidade do gancho da Web do Adobe DTM {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Nenhuma ação necessária.</p> <p>O local público anterior atua como um endpoint de proxy para o novo local privado.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Tarefas da Caixa de entrada {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>Use a <strong>Tarefa de Manutenção de Limpeza da Caixa de Entrada</strong> para remover tarefas antigas do local anterior, conforme necessário.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nenhuma ação é necessária para migrar tarefas para o novo local.</p>
    <ul>
     <li>As tarefas presentes no Local anterior continuam disponíveis e funcionando.</li>
     <li>Novas tarefas são criadas no Novo local.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurações do blueprint do gerenciador de vários sites {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>Local anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>
    <ol>
     <li>Copiar configurações personalizadas de <code>/etc/blueprints</code> para <code>/apps/msm</code>.</li>
     <li>Remover <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Configurações de gadget do painel de projetos AEM {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer configurações de gadget do painel de projetos AEM novas ou modificadas devem ser migradas para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Copie todas as configurações de gadget do painel de projetos AEM novas ou modificadas do local anterior para o novo local (<code>/apps</code>).
      <ol>
       <li>Não copie Configurações de Gadget do Painel de Projetos AEM não modificadas, pois elas agora existem no novo local (<code>/libs</code>).</li>
      </ol> </li>
     <li>Atualize todos os modelos de Projetos AEM que fazem referência ao Local anterior para apontar para o novo local apropriado.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Se o pacote de compatibilidade com AEM 6.4 for aplicado, será necessário executar as atividades de alinhamento do repositório no momento da remoção do pacote de compatibilidade.</td>
  </tr>
 </tbody>
</table>

### Modelo de e-mail de notificação de replicação {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Todos os Modelos de Email de Notificação de Replicação novos ou modificados devem ser migrados para o novo local (<code>/apps</code>)</p>
    <ol>
     <li>Copie todos os Modelos de Email de Notificação de Replicação novos ou modificados do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Remova todos os Modelos de E-mail de Notificação de Replicação migrados do local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os únicos modelos de e-mail de notificação de replicação compatíveis são os novos locais.</p> <p>A resolução do Modelo de E-mail de Notificação de Replicação ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Tags {#tags}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Todas as Marcas devem ser migradas para <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copie todas as tags do local anterior para o novo local.</li>
     <li>Remover todas as tags do local anterior.</li>
     <li>Por meio do Console da Web do AEM, reinicie o pacote OSGi de Marcação do Comunicado do Dia 5 em <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> para que o AEM reconheça que o Novo Local contém conteúdo e deve ser usado.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Reiniciar o pacote OSGi de marcação do comunicado do dia registrará somente o Novo local como a raiz da tag se o Local anterior estiver vazio.</p> <p>As referências ao local anterior continuarão a funcionar após a migração para novo local para todas as funcionalidades que usam a API TagManager do AEM para resolução de tags.</p> <p>Qualquer código personalizado que referencie explicitamente o caminho <code>/etc/tags</code> deve ser atualizado para <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span> ou, de preferência, reescrito para usar a API Java do TagManager, junto com essa migração.</p> </td>
  </tr>
 </tbody>
</table>

### Cloud Services de tradução {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer novo Cloud Service de tradução deve ser migrado para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migrar configurações existentes no local anterior para o novo local.
      <ul>
       <li>Recrie manualmente novas configurações de Cloud Service de tradução por meio da interface de criação do AEM em <strong>Ferramentas &gt; Cloud Service &gt; Cloud Service de tradução</strong>.<br /> OU </li>
       <li>Copie quaisquer novas configurações de Cloud Service de tradução do local anterior para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo de AEM.
      <ol>
       <li>Hierarquias de página do AEM Sites via <strong>AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
       <li>Hierarquias de Fragmento de experiência AEM por meio de <strong>Fragmentos de experiência AEM &gt; Fragmento de experiência &gt; Propriedades &gt; Guia Cloud Service &gt; Configuração na nuvem</strong>.</li>
       <li>Hierarquias de pasta de fragmento de experiência AEM por meio de <strong>Fragmentos de experiência AEM &gt; Pasta &gt; Propriedades &gt; Guia Cloud Service &gt; Configuração na nuvem</strong>.<br /> </li>
       <li>Hierarquias de pastas do AEM Assets via <strong>AEM Assets &gt; Pasta &gt; Propriedades da Pasta &gt; Guia Cloud Service &gt; Configuração</strong>.</li>
       <li>Projetos AEM via <strong>Projetos AEM &gt; Projeto &gt; Propriedades do projeto &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
      </ol> </li>
     <li>Desassocie qualquer Cloud Service de tradução herdada migrada das hierarquias de conteúdo AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução de Cloud Service de tradução ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Os Cloud Service de tradução migrados devem ser compatíveis com o AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Idiomas para tradução {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Todas as definições de Idioma de Tradução novas ou modificadas exigem uma migração de todas as definições de Idioma de Tradução para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Se qualquer adição ou modificação tiver sido feita às definições de Idioma de Tradução, copie todas as definições de Idioma de Tradução do local anterior para o novo local (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do caminho do idioma de tradução ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Esta resolução não oferece suporte a uma sobreposição de mesclagem, o que significa que o caminho resolvido deve conter todos os Idiomas com suporte e não herdará Idiomas com suporte de resoluções de ordem mais alta.</p> </td>
  </tr>
 </tbody>
</table>

### Regras de tradução {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Um arquivo XML de Regras de Tradução modificado deve ser migrado para o novo local (<code>/apps</code> ou <code>/conf/global</code>).</p> <p>1. Copie o arquivo XML de regras de tradução modificado do local anterior para o novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução XML das regras de tradução de replicação ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Biblioteca cliente do widget de tradução {#translation-widget-client-library}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para qualquer design gerenciado em SCM e não gravado no tempo de execução por meio de caixas de diálogo de design.</p>
    <ol>
     <li>Copie os designs do Local anterior para o Novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca de Clientes</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local anterior na
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de cliente (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize as regras de Dispatcher do AEM para permitir o fornecimento de Bibliotecas de clientes por meio do /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Para qualquer design que NÃO seja gerenciado no SCM e modificado em tempo de execução através de caixas de diálogo de design.</p>
    <ul>
     <li>Não mova designs habilitados para o autor de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Console da Web de ativação da árvore {#tree-activation-web-console}

| **Local anterior** | `/etc/replication/treeactivation` |
|---|---|
| **Novo(s) local(is)** | `/libs/replication/treeactivation` |
| **Orientação sobre reestruturação** | Nenhuma ação necessária. |
| **Notas** | O Console da Web de Ativação de Árvore agora está disponível por meio de **Ferramentas > Implantação > Replicação > Ativar Árvore**. |

{style="table-layout:auto"}

### Cloud Service do conector de tradução do fornecedor {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Qualquer novo Cloud Service do Conector de tradução do fornecedor deve ser migrado para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre as configurações existentes no local anterior para o novo local.
      <ul>
       <li>Crie manualmente novas configurações do Cloud Service do Conector de tradução do fornecedor por meio da interface de criação do <strong>AEM em Ferramentas &gt; Cloud Service &gt; Cloud Service de tradução</strong>.<br /> OU </li>
       <li>Copie quaisquer novas configurações de Cloud Service do Conector de tradução do fornecedor do local anterior para o novo local (<code>/apps</code>, <code>/conf/global </code>ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo de AEM.
      <ol>
       <li>Hierarquias de página do AEM Sites via <strong>AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
       <li>Hierarquias de Fragmento de experiência AEM por meio de <strong>Fragmentos de experiência AEM &gt; Fragmento de experiência &gt; Propriedades &gt; Guia Cloud Service &gt; Configuração na nuvem</strong>.</li>
       <li>Hierarquias de pasta de fragmento de experiência AEM por meio de <strong>Fragmentos de experiência AEM &gt; Pasta &gt; Propriedades &gt; Guia Cloud Service &gt; Configuração na nuvem</strong>.</li>
       <li>Hierarquias de pastas do AEM Assets via <strong>AEM Assets &gt; Pasta &gt; Propriedades da Pasta &gt; Guia Cloud Service &gt; Configuração</strong>.</li>
       <li>Projetos AEM via <strong>Projetos AEM &gt; Projeto &gt; Propriedades do projeto &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
      </ol> </li>
     <li>Desassocie qualquer Cloud Service de tradução herdada migrada das hierarquias de conteúdo AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução de Cloud Service de tradução ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Modelos de email de notificação de fluxo de trabalho {#workflow-notification-email-templates}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Todos os Modelos de Email de Notificação de Fluxo de Trabalho modificados devem ser migrados para o Novo Local (<code>/conf/global</code>).</p>
    <ol>
     <li>Copie todos os modelos de e-mail de notificação de workflow modificados do local anterior para o novo local.</li>
     <li>Remova os modelos de email de notificação de fluxo de trabalho migrados do local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do Modelo de email de notificação do fluxo de trabalho ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Pacotes de Fluxo de Trabalho {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Os pacotes de fluxos de trabalho existentes no local anterior devem ser migrados para o novo local.</p>
    <ol>
     <li>Remova todos os pacotes de fluxo de trabalho no local anterior que não são referenciados por outro conteúdo e que, de outra forma, não são necessários.</li>
     <li>Mova todos os pacotes de fluxo de trabalho no local anterior que não são referenciados por outro conteúdo, mas que são necessários no novo local.</li>
     <li>Deixe todos os pacotes de fluxo de trabalho referenciados por outro conteúdo no local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os pacotes de fluxo de trabalho criados por meio do console Miscadmin da interface clássica são mantidos no local anterior, enquanto todos os outros são mantidos no novo local.</p> <p>Os pacotes de fluxos de trabalho armazenados nos locais anterior ou inferior podem ser gerenciados por meio do console Miscadmin da interface clássica.</p> </td>
  </tr>
 </tbody>
</table>
