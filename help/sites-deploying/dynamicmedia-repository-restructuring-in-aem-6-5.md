---
title: Restruturação do repositório do Dynamic Media no Adobe Experience Manager 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no Experience Manager 6.5 para Dynamic Media.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Restruturação do repositório do Dynamic Media no Adobe Experience Manager 6.5 {#dynamic-media-repository-restructuring-in-aem}

Conforme descrito na página pai [Reestruturação do repositório no Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que estão atualizando para o Experience Manager 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam o Dynamic Media. Algumas alterações exigem esforço de trabalho durante o processo de atualização do Experience Manager 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Antes de uma atualização futura**

* [Configurações personalizadas de codificação de vídeo adaptável](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Configuração em nuvem do Dynamic Media (DMS7)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Configuração de Cloud Service Dynamic Media (DM Hybrid)](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - Configuração de Cloud Service do YouTube](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Diversos](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## Antes de uma atualização futura {#prior-to-upgrade}

### Configurações personalizadas de codificação do vídeo adaptável  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Você pode executar o script de migração a seguir para migrar para o novo local:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Como alternativa, você pode editar a configuração na interface do usuário do Experience Manager e as alterações são salvas no novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuração em nuvem do Dynamic Media (DMS7) {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>O cliente pode executar um script de migração neste local:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Reinicie o pacote OSGi do Dynamic Media.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Configuração de Cloud Service Dynamic Media (DM Hybrid) {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Você pode executar o script de migração abaixo para alinhar-se ao modelo mais recente:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - Configuração de Cloud Service do YouTube  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>1. Desfaça a publicação de todos os vídeos do YouTube<br /> 2. Crie a Configuração do YouTube usando a nova Interface para toque (de <code>/conf</code>), incluindo a cópia de todos os Canais do local antigo<br /> 3. Publish todos os vídeos de volta para o YouTube.</p> <p>Esse workflow resulta em novos URLs do YouTube. Se você não cancelar a publicação antes de criar uma configuração do YouTube com interface para toque, terá vários URLs do YouTube listados em Propriedades, pois os Canais recriados serão publicados novamente, se houver a chance. Essa funcionalidade significa que você tem URLs inúteis listados em Propriedades.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diversos {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>O cliente pode executar o script de migração abaixo.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>Como alternativa, você pode editar a configuração na interface do usuário do Experience Manager e as alterações são salvas no novo local.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>O cliente pode executar o script de migração abaixo.</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>
