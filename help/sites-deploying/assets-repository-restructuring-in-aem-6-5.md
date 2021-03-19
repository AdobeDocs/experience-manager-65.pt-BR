---
title: Reestruturação do repositório de ativos no AEM 6.5
seo-title: Reestruturação do repositório de ativos no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 para Assets.
seo-description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.5 para Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 2%

---


# Reestruturação do repositório de ativos no AEM 6.5 {#assets-repository-restructuring-in-aem}

Conforme descrito na página principal [Reestruturação do Repositório AEM 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que atualizam para AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações do repositório que afetam a solução da AEM Assets. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com a atualização 6.5**

* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Antes da atualização futura**

* [Modelo de Notificação por E-mail de Evento de Ativo/Coleta](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Designs clássicos de compartilhamento de ativos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Baixar modelo de notificação por email de ativos](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Exemplo de licenças DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Modelo de Notificação por Correio Eletrônico de Partilha de Ligações](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [Scripts de fluxo de trabalho do InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configurações de transcodificação de vídeo](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Com a atualização 6.5 {#with-upgrade}

### Diversos {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Se qualquer código personalizado depender desse local (ou seja, o código dependa explicitamente desse caminho), então o código deve ser atualizado para usar o novo local antes da atualização; Idealmente, as APIs do Java são usadas quando disponíveis para reduzir as dependências em qualquer caminho específico no JCR.</p> <p>Local temporário para armazenar o arquivo zip para download pelo cliente. Não há necessidade de atualizar desde quando o cliente solicita o download do ativo. Ele gerará um arquivo no novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

## Antes da atualização futura {#prior-to-upgrade}

### Modelo de Notificação de Evento de Ativo/Coleta {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Se os modelos de email tiverem sido modificados pelo cliente, execute as seguintes ações para alinhar-se à nova estrutura de repositório:</p>
    <ol>
     <li>O modelo de email <code>/libs/settings/dam/notification</code> deve ser copiado de <strong><code>/etc/notification/email/default</code></strong> para <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Como o destino está em<strong> <code>/apps</code></strong> essa alteração deve ser mantida no SCM.</li>
      </ol> </li>
     <li>Remova a pasta: <strong><code>/etc/dam/notification/email/default</code></strong> depois que os modelos de email dentro dele tiverem sido movidos.<br />
      <ol>
       <li>Se nenhuma atualização for feita no modelo de email em<strong> <code>/etc/notification/email/default</code></strong>, a pasta poderá ser removida, pois o modelo de email original existe em <strong><code>/libs/settings/notification/email/default</code></strong> como parte da instalação AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Designs clássicos de compartilhamento de ativos {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para quaisquer Designs gerenciados no SCM e não gravados em tempo de execução por meio de caixas de diálogo de design, execute as seguintes ações para alinhar ao modelo mais recente:</p>
    <ol>
     <li>Copie os designs do local anterior para o novo local em <code>/apps</code>.</li>
     <li>Converta qualquer CSS, JavaScript e recursos estáticos no Design em uma <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Biblioteca do cliente</a> com <code>allowProxy = true</code>.</li>
     <li>Atualize referências ao Local anterior na propriedade <code>cq:designPath</code> por meio de <strong>AEM &gt; Administrador do DAM &gt; Página de compartilhamento de ativos &gt; Propriedades da página &gt; Guia Avançado &gt; Campo de design</strong>.</li>
     <li>Atualize quaisquer páginas que façam referência ao local anterior para usar a nova categoria Biblioteca de clientes . Isso requer a atualização do código de implementação da página .</li>
     <li>Atualize as regras do Dispatcher para permitir o serviço de bibliotecas de clientes por meio do servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Para quaisquer Designs que não sejam gerenciados no SCM e tempo de execução modificado por meio de Caixas de Diálogo de Design, não mova designs autoráveis de <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Baixar modelo de notificação de e-mail de ativo {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Se os modelos de email (<strong>downloadasset</strong> ou <strong>transientworkflowcompleted</strong>) tiverem sido modificados, siga o procedimento abaixo para alinhar-se à nova estrutura:</p>
    <ol>
     <li>O modelo de email atualizado deve ser copiado de <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> para <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Como o destino está em<strong> <code>/apps</code></strong> essa alteração deve ser mantida no SCM.</li>
      </ol> </li>
     <li>Remova a pasta: <code>/etc/dam/workflow/notification/email/downloadasset </code>depois que os modelos de email dentro dele tiverem sido movidos.<br />
      <ol>
       <li>Se nenhuma atualização for feita no modelo de email em<strong> <code>/etc</code></strong>, a pasta poderá ser removida, pois o modelo de email original existe em <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> como parte da instalação AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Embora <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> seja suportado tecnicamente para a pesquisa (tem precedência antes de /apps por meio da pesquisa usual do Sling CAConfig, mas depois de <code>/etc</code>), o modelo pode ser colocado em <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. No entanto, isso não é recomendado, pois não há interface do usuário de tempo de execução para facilitar a edição do template de email.</td>
  </tr>
 </tbody>
</table>

### Exemplo de licenças de DRM {#example-drm-licenses}

| **Localização anterior** | `/etc/dam/drm/licenses/` |
|---|---|
| **Novas localizações** | `/libs/settings/dam/drm` |
| **Orientação relativa à reestruturação** | N/D |
| **Notas** | N/D |

### Modelo de Notificação por Correio Eletrônico de Partilha de Ligação {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Se o modelo de email tiver sido modificado pelo cliente, para alinhar-se à nova estrutura do repositório:</p>
    <ol>
     <li>O modelo de email atualizado deve ser copiado de <strong><code>/etc/dam/adhocassetshare</code></strong> para <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Como o destino está em<strong> <code>/apps</code></strong> essa alteração deve ser mantida no SCM.</li>
      </ol> </li>
     <li>Remova a pasta: <strong><code>/etc/dam/adhocassetshare</code></strong> depois que os modelos de email dentro dele tiverem sido movidos.<br />
      <ol>
       <li>Se nenhuma atualização for feita no modelo de email em<strong> <code>/etc</code></strong>, a pasta poderá ser removida, pois o modelo de email original existe em <strong><code>/libs/settings/dam/adhocassetshare</code></strong> como parte da instalação AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Embora <code>/conf/global/settings/dam/adhocassetshare</code> seja suportado tecnicamente para a pesquisa (tem precedência antes de <code>/apps</code> por meio da pesquisa Sling CAConfig usual, mas depois de <code>/etc</code>), o modelo pode ser colocado em <code>/conf/global/settings/dam/adhocassetshare</code>. No entanto, isso não é recomendado, pois não há interface do usuário de tempo de execução para facilitar a edição do modelo de email</td>
  </tr>
 </tbody>
</table>

### Scripts de Fluxo de Trabalho do InDesign {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para Alinhar com a nova estrutura de repositório:</p>
    <ol>
     <li>Copiar todos os scripts personalizados ou modificados de <strong><code>/etc/dam/indesign/scripts</code></strong> para <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>Somente copiar scripts novos ou modificados como scripts não modificados fornecidos pelo AEM estarão disponíveis via <strong><code>/libs/settings</code></strong> no AEM 6.5</li>
      </ol> </li>
     <li>Localize todos os modelos de fluxo de trabalho que usam a etapa WF do processo de extração de mídia e
      <ol>
       <li>Para cada instância da Etapa do fluxo de trabalho, atualize os caminhos na configuração para apontar explicitamente para os scripts adequados em<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> ou <strong><code>/libs/settings/dam/indesign/scripts</code></strong> conforme apropriado.</li>
      </ol> </li>
     <li>Remova<strong> <code>/etc/dam/indesign/scripts</code></strong> totalmente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>É recomendável que os scripts personalizados sejam armazenados em <code>/apps</code>, pois esse é o local onde o código deve ser armazenado.</td>
  </tr>
 </tbody>
</table>

### Configurações de transcodificação de vídeo {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>As personalizações no nível do projeto precisam ser recortadas e coladas em caminhos equivalentes <code>/apps</code> ou <code>/conf</code>, conforme aplicável.</p> <p>Para alinhar-se à estrutura do repositório do AEM 6.4:</p>
    <ol>
     <li>Copie quaisquer configurações de vídeo modificadas de <code>/etc/dam/video</code> para <code>/apps/settings/dam/video</code></li>
     <li>Remover <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurações de predefinição do visualizador {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para a predefinição do visualizador pronta para uso, ela só estará disponível no novo local.</p> <p>Para a predefinição do Visualizador personalizado:</p>
    <ul>
     <li>será necessário executar um script de migração para mover o nó de <code>/etc</code> para <code>/conf</code>. O script está localizado em <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>ou você pode editar a configuração e elas serão salvas automaticamente no novo local.</li>
    </ul> <p>Observe que não é necessário ajustar o código copyURL/embed para apontar para <code>/conf</code>. A solicitação existente para <code>/etc</code> será redirecionada para o conteúdo correto de <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Diversos {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Ajuste quaisquer referências para apontar para os novos recursos em <code>/libs</code> usando o prefixo de proxy <code>/etc.clientlibs/</code> permitido.</p> <p>Por fim, limpe removendo as pastas das clientlibs migradas <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

