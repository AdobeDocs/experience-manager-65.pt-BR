---
title: Reestruturação comum de repositório no AEM 6.5
seo-title: Reestruturação comum de repositório no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 que são comuns para todas as áreas de AEM.
seo-description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 que são comuns para todas as áreas de AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2722'
ht-degree: 2%

---


# Reestruturação comum do repositório no AEM 6.5 {#common-repository-restructuring-in-aem}

Conforme descrito na página principal [Reestruturação do Repositório AEM 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que atualizam para AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações do repositório que possivelmente afetarão todas as soluções. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com a atualização 6.5**

* [Configurações do ContextHub](#contexthub-6.5)
* [Instâncias do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelos do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Inicializadores do fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Scripts de fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Antes da atualização futura**

* [Configurações do ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Designs Cloud Services clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Designs de painéis clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Designs de relatórios clássicos](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Designs padrão](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Endpoint de JavaScript do Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Endpoint de gancho da Web do Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Tarefas da caixa de entrada](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurações do Blueprint do gerenciador de vários sites](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurações do Gadget do Painel de Projetos AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modelo de Correio Eletrônico de Notificação de Replicação](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Tags](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Cloud Services de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Idiomas de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Regras de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Biblioteca de clientes do widget de tradução](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console da Web de Ativação em Árvore](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Services do conector de tradução do fornecedor](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modelos de email de notificação de fluxo de trabalho](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Com a atualização 6.5 {#with-upgrade}

### Configurações do ContextHub {#contexthub-6.5}

A partir AEM 6.4, não há configuração padrão do ContextHub. Portanto, no nível raiz do site, um `cq:contextHubPathproperty` deve ser definido para indicar qual configuração deve ser usada.

1. Navegue até a raiz do site.
1. Abra as propriedades da página raiz e selecione a guia Personalization .
1. No campo Caminho do Contexthub , digite seu próprio caminho de configuração do ContextHub.

Além disso, na configuração do ContextHub, o `sling:resourceType` precisa ser atualizado para ser relativo e não absoluto.

1. Abra as propriedades do nó de configuração do ContextHub no CRX DE Lite, por exemplo `/apps/settings/cloudsettings/legacy/contexthub`
1. Altere `sling:resourceType` de `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` para `granite/contexthub/cloudsettings/components/baseconfiguration`

Ou seja, o `sling:resourceType` da configuração do ContextHub deve ser relativo em vez de absoluto.

### Modelos do fluxo de trabalho {#workflow-models}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer modelo de fluxo de trabalho novo ou modificado deve ser migrado para /conf/global/workflow/models.</p>
    <ol>
     <li>Implante os Modelos de fluxo de trabalho modificados em uma instância de desenvolvimento do AEM local 6.5, de modo que eles existam no local Anterior.</li>
     <li>Edite o modelo de fluxo de trabalho usando AEM Editor de modelo de fluxo de trabalho em AEM &gt; Ferramentas &gt; Fluxo de trabalho &gt; Modelos.</li>
     <li>Ao migrar modelos de fluxo de trabalho modificados fornecidos pelo AEM
      <ol>
       <li>Com o Editor de modelo de fluxo de trabalho aberto, modifique o URL de endereço do navegador e substitua o segmento de caminho /libs/settings/workflow/models por /etc/workflow/models.
        <ul>
         <li>Por exemplo, altere: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> para <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Ative o modo Editar no Editor de modelo de fluxo de trabalho, que copiará a definição do modelo de fluxo de trabalho para /conf/global/workflow/models.</li>
     <li>Toque no botão Sincronizar para sincronizar as alterações no Modelo de fluxo de trabalho em Tempo de execução em /var/workflow/models.</li>
     <li>Exporte o Modelo de fluxo de trabalho (/conf/global/workflow/models/&lt;workflow-model&gt;) e o Modelo de fluxo de trabalho em tempo de execução (/var/workflow/models/&lt;workflow-model&gt;) e integre o projeto AEM.
      <ol>
       <li>Por exemplo, exportar:
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> e </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do Modelo de Fluxo de Trabalho ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Assim, qualquer personalização de Modelos de Fluxo de Trabalho fornecidos AEM persistida no local Anterior deve ser movida para /conf/global/settings/workflow/models se quiserem ser retidos, caso contrário, serão substituídas pela definição de Modelo de Fluxo de Trabalho fornecida pelo AEM em /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Instâncias do fluxo de trabalho {#workflow-instances}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Nenhuma ação é necessária para alinhar com a Nova Localização.</p> <p>As Instâncias de Fluxo de Trabalho Históricas podem continuar residindo com segurança no Local Anterior, e novas Instâncias de Fluxo de Trabalho serão criadas no Novo Local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Quaisquer referências de caminho explícitas em
    <code>
     custom
    </code> código para o Local anterior também deve levar em conta o Novo local. É recomendável que esse código seja refatorado para usar as APIs do fluxo de trabalho do AEM.</td>
  </tr>
 </tbody>
</table>

### Inicializadores do fluxo de trabalho {#workflow-launchers}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer Iniciador de Fluxo de Trabalho novo ou modificado deve ser migrado para <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copie quaisquer configurações novas ou modificadas do Iniciador do fluxo de trabalho do Local anterior para Novo local (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do Iniciador de Fluxo de Trabalho ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Assim, qualquer personalização do Iniciador de Fluxo de Trabalho fornecido AEM persistida no local Anterior deve ser movida para o Novo Local (<code>/conf/global/settings/workflow/launcher</code> se for necessário reter, caso contrário, será substituída pela definição do Iniciador de Fluxo de Trabalho fornecida pelo AEM em <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts de fluxo de trabalho {#workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Quaisquer scripts de fluxo de trabalho novos ou modificados devem ser migrados para o novo local e os Modelos de fluxo de trabalho de referência atualizados para refletir o novo local.</p>
    <ol>
     <li>Copie quaisquer scripts de fluxo de trabalho novos ou modificados do local anterior para o novo local.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> deve ser mantido no SCM.</li>
      </ul> </li>
     <li>Atualize qualquer referência aos scripts de fluxo de trabalho no local anterior em modelos de fluxo de trabalho para apontar para os novos locais.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>AEM 6.4 SP1, quando é liberada, faz com que essa reestruturação possa ser adiada para 6.5
     <code>
      upgrade
     </code>.</p> <p>Se estiver atualizando para o AEM 6.4 antes do lançamento do AEM 6.4 SP1, essa reestruturação deverá ser executada como parte do projeto de atualização. Sem isso, editar e salvar as Etapas do fluxo de trabalho que fazem referência aos scripts no Local anterior removerá a referência do Script de fluxo de trabalho da Etapa do fluxo de trabalho totalmente, e somente os scripts de fluxo de trabalho em novos locais estarão disponíveis na lista suspensa de seleção de script.</p> </td>
  </tr>
 </tbody>
</table>

## Antes da atualização futura {#prior-to-upgrade}

### Configurações do ContextHub {#contexthub-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as configurações do ContextHub novas ou modificadas devem ser migradas para o novo local e as páginas do AEM Sites de referência devem ser atualizadas para refletir o novo local.</p>
    <ol>
     <li>Copie quaisquer configurações do ContextHub novas ou modificadas do local anterior para o novo local.</li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo AEM.
      <ol>
       <li><strong>Hierarquias de página do AEM Sites por meio de AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração</strong> da nuvem.</li>
      </ol> </li>
     <li>Desassocie qualquer configuração herdada do ContextHub migrada das hierarquias de conteúdo AEM mencionadas anteriormente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Designs Cloud Services Classic {#classic-cloud-services-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de Caixas de Diálogo de Design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (<code>/apps</code>).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualizar referências ao Local Anterior no <span class="code">
       <code>
        cq
       </code>:
       Propriedade <code>
        designPath
       </code></span>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de clientes (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize AEM regras do Dispatcher para permitir a veiculação de bibliotecas de clientes por meio da pasta /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Para qualquer Designs que NÃO seja gerenciado no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design.</p>
    <ul>
     <li>Não mova os Designs que podem ser do autor para fora de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Designs de painéis clássicos {#classic-dashboards-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de Caixas de Diálogo de Design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize referências ao Local anterior no
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de clientes (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize AEM regras do Dispatcher para permitir a veiculação de bibliotecas de clientes por meio da pasta /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Para qualquer Designs que NÃO seja gerenciado no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design.</p>
    <ul>
     <li>Não mova os Designs que podem ser do autor para fora de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Designs de relatórios clássicos {#classic-reports-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de Caixas de Diálogo de Design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize referências ao Local anterior no
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de clientes (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize AEM regras do Dispatcher para permitir a veiculação de bibliotecas de clientes por meio da pasta /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Para qualquer Designs que NÃO seja gerenciado no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design.</p>
    <ul>
     <li>Não mova os Designs que podem ser do autor para fora de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Designs padrão {#default-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de Caixas de Diálogo de Design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize referências ao Local anterior no
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de clientes (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize AEM regras do Dispatcher para permitir a veiculação de bibliotecas de clientes por meio da pasta /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Para qualquer Designs que NÃO seja gerenciado no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design.</p>
    <ul>
     <li>Não mova os Designs que podem ser do autor para fora de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Ponto de extremidade JavaScript do Adobe DTM {#adobe-dtm-javascript-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Nenhuma ação necessária.</p> <p>A localização anterior pública atua como um ponto de extremidade proxy para a nova localização privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint de gancho da Web do Adobe DTM {#adobe-dtm-web-hook-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Nenhuma ação necessária.</p> <p>A localização anterior pública atua como um ponto de extremidade proxy para a nova localização privada.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Tarefas da caixa de entrada {#inbox-tasks}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>Use a <strong>Tarefa de manutenção de limpeza da caixa de entrada</strong> para remover tarefas antigas do local anterior, conforme necessário.</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Nenhuma ação é necessária para migrar Tarefas para o novo local.</p>
    <ul>
     <li>As tarefas presentes no Local anterior continuam disponíveis e funcionam.</li>
     <li>Novas Tarefas são criadas no Novo Local.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurações do Blueprint do gerenciador de vários sites {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong><em></em>Localização anterior</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>
    <ol>
     <li>Copie configurações personalizadas de <code>/etc/blueprints</code> para <code>/apps/msm</code>.</li>
     <li>Remover <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurações do Gadget do Painel de Projetos AEM {#aem-projects-dashboard-gadget-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer configuração de gadget do painel de projetos nova ou modificada AEM deve ser migrada para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Copie todas as configurações de Gadget do Painel de AEM Projetos novas ou modificadas do local anterior para o novo local (<code>/apps</code>).
      <ol>
       <li>Não copie configurações de Gadget do Painel de Projetos não modificadas, pois elas agora existem no novo local (<code>/libs</code>).</li>
      </ol> </li>
     <li>Atualize qualquer modelo de Projetos AEM que referencie a Localização anterior para apontar para a nova localização apropriada.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Se o pacote de compatibilidade do AEM 6.4 for aplicado, será necessário executar as atividades de alinhamento do repositório no momento da remoção do pacote de compatibilidade.</td>
  </tr>
 </tbody>
</table>

### Modelo de Email de Notificação de Replicação {#replication-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer modelo de email de notificação de replicação novo ou modificado deve ser migrado para o novo local (<code>/apps</code>)</p>
    <ol>
     <li>Copie qualquer modelo de email de notificação de replicação novo ou modificado do local anterior para um novo local (<code>/apps</code>).</li>
     <li>Remova qualquer modelo de email de notificação de replicação migrado do local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os únicos novos modelos de email de notificação de replicação compatíveis são oferecer suporte a novas localidades.</p> <p>A resolução de Modelo de Email de Notificação de Replicação ocorre na seguinte ordem:</p>
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

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as tags devem ser migradas para <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copie todas as tags do local anterior para o novo local.</li>
     <li>Remova todas as tags do local anterior.</li>
     <li>Por meio do Console da Web AEM, reinicie o pacote OSGi de Marcação do Day Communique 5 em <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> para AEM reconhecer que o Novo local contém conteúdo e deve ser usado.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Reiniciar o pacote OSGi de Marcação de comunidade do dia registrará somente o Novo local como a raiz da tag se o Local anterior estiver vazio.</p> <p>As referências ao local anterior continuarão a funcionar após a migração para o novo local de todas as funcionalidades que usam AEM API do TagManager para resolução de tags.</p> <p>Qualquer código personalizado que faça referência explícita ao caminho <code>/etc/tags</code> deve ser atualizado para <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, ou preferencialmente reescrita para aproveitar a API Java do TagManager, em conjunto com essa migração.</p> </td>
  </tr>
 </tbody>
</table>

### Cloud Services de tradução {#translation-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer novo Cloud Services de Tradução deve ser migrado para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre as configurações existentes no local anterior para o novo local.
      <ul>
       <li>Recrie manualmente as novas configurações de Cloud Services de tradução por meio da interface de criação de AEM em <strong>Tools &gt; Cloud Services &gt; Translation Cloud Services</strong>.<br /> OU </li>
       <li>Copie quaisquer novas configurações de Cloud Services de Tradução do local anterior para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo AEM.
      <ol>
       <li>Hierarquias de página do AEM Sites por meio de <strong>AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
       <li>AEM hierarquias do Fragmento de experiência por meio de <strong>AEM Fragmentos de experiência &gt; Fragmento de experiência &gt; Propriedades &gt; Guia Cloud Services &gt; Configuração da nuvem</strong>.</li>
       <li>AEM hierarquias da pasta do fragmento de experiência por meio de <strong>AEM Fragmentos de experiência &gt; Pasta &gt; Propriedades &gt; Guia Cloud Services &gt; Configuração da nuvem</strong>.<br /> </li>
       <li>Hierarquias de pastas AEM Assets por meio de <strong>AEM Assets &gt; Pasta &gt; Propriedades da pasta &gt; Guia Cloud Services &gt; Configuração</strong>.</li>
       <li>AEM projetos por meio de <strong>AEM Projetos &gt; Projeto &gt; Propriedades do projeto &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
      </ol> </li>
     <li>Desassocie qualquer Cloud Services de Tradução herdada migrada das hierarquias de conteúdo AEM acima.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução de Cloud Services de tradução ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>Os Cloud Services de tradução migrados devem ser compatíveis com o AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Idiomas de tradução {#translation-languages}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer definição nova ou modificada de Idioma de tradução requer uma migração de todas as definições de Idioma de tradução para o novo local (<code>/apps</code>).</p>
    <ol>
     <li>Se alguma adição ou modificação tiver sido feita às definições de Idioma de Tradução, copie todas as definições de Idioma de Tradução do local anterior para o novo local (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução do caminho Idioma de Tradução ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Esta resolução não suporta uma sobreposição de mesclagem, o que significa que o caminho resolvido deve conter todos os Idiomas Suportados e não herdará os Idiomas Suportados das resoluções de ordem superior.</p> </td>
  </tr>
 </tbody>
</table>

### Regras de tradução {#translation-rules}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Um arquivo XML de regras de tradução modificado deve ser migrado para o novo local (<code>/apps</code> ou <code>/conf/global</code>).</p> <p>1. Copie o arquivo XML de regras de tradução modificado do local anterior para o novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução XML das Regras de Tradução de Replicação ocorre na seguinte ordem:</p>
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

### Biblioteca de cliente do widget de tradução {#translation-widget-client-library}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de Caixas de Diálogo de Design.</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local (/apps).</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize referências ao Local anterior no
      <code>
       cq
      </code>:
      Propriedade <code>
       designPath
      </code>.</li>
     <li>Atualize quaisquer Páginas que façam referência ao Local anterior para usar a nova categoria Biblioteca de clientes (isso requer a atualização do código de implementação da Página).</li>
     <li>Atualize AEM regras do Dispatcher para permitir a veiculação de bibliotecas de clientes por meio da pasta /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Para qualquer Designs que NÃO seja gerenciado no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design.</p>
    <ul>
     <li>Não mova os Designs que podem ser do autor para fora de <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Console da Web de Ativação em Árvore {#tree-activation-web-console}

| **Localização anterior** | `/etc/replication/treeactivation` |
|---|---|
| **Novas localizações** | `/libs/replication/treeactivation` |
| **Orientação relativa à reestruturação** | Nenhuma ação necessária. |
| **Notas** | O Console da Web de Ativação em Árvore agora está disponível por meio de **Ferramentas > Implantação > Replicação > Ativar árvore**. |

### Cloud Services do conector de tradução do fornecedor {#vendor-translation-connector-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer novo Cloud Services do Conector de tradução do fornecedor deve ser migrado para o novo local (<code>/apps</code>, <code>/conf/global</code> ou <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o Novo local.
      <ul>
       <li>Crie manualmente as novas configurações do Cloud Services do Conector de tradução do fornecedor por meio da <strong>AEM interface de criação em Ferramentas &gt; Cloud Services &gt; Cloud Services de tradução</strong>.<br /> OU </li>
       <li>Copie quaisquer novas configurações de Cloud Services do Conector de tradução do fornecedor do local anterior para o novo local (<code>/apps</code>, <code>/conf/global </code>ou <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associe as configurações de AEM aplicáveis às hierarquias de conteúdo AEM.
      <ol>
       <li>Hierarquias de página do AEM Sites por meio de <strong>AEM Sites &gt; Página &gt; Propriedades da página &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
       <li>AEM hierarquias do Fragmento de experiência por meio de <strong>AEM Fragmentos de experiência &gt; Fragmento de experiência &gt; Propriedades &gt; Guia Cloud Services &gt; Configuração da nuvem</strong>.</li>
       <li>AEM hierarquias da pasta do fragmento de experiência por meio de <strong>AEM Fragmentos de experiência &gt; Pasta &gt; Propriedades &gt; Guia Cloud Services &gt; Configuração da nuvem</strong>.</li>
       <li>Hierarquias de pastas AEM Assets por meio de <strong>AEM Assets &gt; Pasta &gt; Propriedades da pasta &gt; Guia Cloud Services &gt; Configuração</strong>.</li>
       <li>AEM projetos por meio de <strong>AEM Projetos &gt; Projeto &gt; Propriedades do projeto &gt; Guia Avançado &gt; Configuração da nuvem</strong>.</li>
      </ol> </li>
     <li>Desassocie qualquer Cloud Services de Tradução herdada migrada das hierarquias de conteúdo AEM acima.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução de Cloud Services de tradução ocorre na seguinte ordem:</p>
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

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer modelo de email de notificação de fluxo de trabalho modificado deve ser migrado para o Novo local (<code>/conf/global</code>).</p>
    <ol>
     <li>Copie todos os Modelos de email de notificação de fluxo de trabalho modificados do local anterior para o novo local.</li>
     <li>Remova Modelos de email de notificação de fluxo de trabalho migrados do local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>A resolução de Modelo de Email de Notificação de Workflow ocorre na seguinte ordem:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Pacotes de Fluxo de Trabalho {#workflow-packages}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Os pacotes de fluxo de trabalho existentes no local anterior devem ser migrados para o novo local.</p>
    <ol>
     <li>Remova todos os pacotes de fluxo de trabalho no local anterior que não estejam referenciados por outro conteúdo e que, de outra forma, não sejam necessários.</li>
     <li>Mova todos os pacotes de fluxo de trabalho no local anterior que não sejam referenciados por outro conteúdo, mas que, de outra forma, sejam necessários no novo local.</li>
     <li>Deixe quaisquer Pacotes de fluxo de trabalho referenciados por outro conteúdo no local anterior.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td><p>Os pacotes de fluxo de trabalho criados por meio do console Miscadmin da interface clássica são mantidos no local anterior, enquanto todos os outros são mantidos no novo local.</p> <p>Os pacotes de fluxo de trabalho armazenados nos locais anteriores ou inferiores podem ser gerenciados por meio do console Miscadmin da interface clássica.</p> </td>
  </tr>
 </tbody>
</table>

