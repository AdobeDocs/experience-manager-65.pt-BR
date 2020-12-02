---
title: Reestruturação do repositório para AEM Communities no 6.4
seo-title: Reestruturação do repositório para AEM Communities no 6.4
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.4 para Comunidades.
seo-description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.4 para Comunidades.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# Reestruturação do repositório para AEM Communities em 6.5 {#repository-restructuring-for-aem-communities-in}

Conforme descrito na página pai [Reestruturação do repositório AEM 6.4](/help/sites-deploying/repository-restructuring.md), os clientes que atualizam para AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a Solução AEM Communities. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com atualização 6.5**

* [Modelos de notificação por email](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurações de subscrição](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes da atualização futura**

* [Configurações de marcação](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Designs de console das Comunidades clássicas](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurações de logon do Facebook Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurações de opções de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurações de logon do Pinterest Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurações de Pontuação](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurações de logon do Twitter Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Misc](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Com a atualização 6.5 {#with-upgrade}

### Modelos de notificação por email {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>A migração manual é necessária se você deseja mover para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Gerenciador de configurações do Granite para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> como <code>true</code> no nó "<code>/libs/settings/community/subscriptions</code>" e adicionar um nó filho <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de subscrição {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>A migração manual é necessária se você deseja mover para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Gerenciador de configurações do Granite para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> como <code>true</code> no nó "<code>/libs/settings/community/subscriptions</code>" e adicionar um nó filho <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de palavras de observação {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>Uma tarefa de migração lenta está disponível para limpar as Configurações das comunidades.<br /> <p>A Tarefa move palavras de observação de <code>/etc/watchwords</code> para <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se palavras de observação personalizadas forem armazenadas no SCM, elas deverão ser implantadas em <code>/apps/settings/...</code> e você deverá garantir que não haja uma configuração <code>/conf/global/settings/...</code> sobreposta que tenha prioridade.</p> <p>A tarefa de migração remove <code>/etc</code> locais.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

## Antes da atualização futura {#prior-to-upgrade}

### Configurações de marcação {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><strong>Regras do selo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imagens de emblema:</strong></p> <p>Para imagens padrão: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imagens personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>A migração manual é necessária.</p> <p>Se a sua instância personalizou as regras de marcação/pontuação, não há uma maneira automatizada de colocar todas as regras em um bucket. Necessita de entradas de clientes em qual conf bucket (global ou específico do site) você deseja usar para o seu site.</p> <p>Nenhuma interface de usuário disponível para configurar a identificação e a pontuação de um site.</p> <p>Para alinhar com a nova estrutura do repositório:</p>
    <ol>
     <li>Crie um bucket de contexto de site usando o <strong>Navegador de Configuração</strong> em <strong>Ferramentas</strong></li>
     <li>Ir para a raiz do Site</li>
     <li>Defina <code>cq:confproperty</code> como o caminho do compartimento onde deseja armazenar todas as configurações. O mesmo pode ser definido pelo site <strong>Assistente de edição - Definir entrada de configuração de nuvem</strong>.</li>
     <li>Mova as regras de identificação e as regras de pontuação relevantes de <code>/etc/community/*</code> para o grupo de contexto do site criado na etapa anterior.</li>
     <li>Ajuste as propriedades Regras de marcação e Regras de pontuação na raiz do site para ter referências relativas a novos locais de regras.
      <ol>
       <li>Por exemplo, se a propriedade de <code>cq:conf = /conf/we-retail</code>, então <code>badgingRules [] = community/badging/rules</code> se as regras forem movidas para esse novo bucket.</li>
      </ol> </li>
     <li>Da mesma forma, ajuste as referências às regras de pontuação em um nó de regra de identificação para ter um caminho relativo.</li>
    </ol> <p> </p> <p>Finalmente, limpe removendo o recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Designs do console das Comunidades clássicas {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon do Facebook Social {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as novas configurações da nuvem do Facebook devem ser migradas para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o novo local.
      <ol>
       <li>Recrie manualmente as novas Configurações de logon do Facebook Social por meio da interface de usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon social do Facebook</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas Configurações da nuvem do Facebook do Local anterior para o Novo local apropriado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site da AEM Communities para fazer referência à nova Configuração de logon social do Facebook definindo a propriedade <code>[cq:Page]/jcr:content@cq:conf</code> como o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service legado do Facebook Connect de qualquer raiz do site da AEM Communities atualizada para fazer referência ao novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de opções de idioma {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>N/A<br /> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon do Pinterest Social {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as novas configurações da Pinterest Cloud devem ser migradas para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o novo local.
      <ol>
       <li>Recrie manualmente as novas Configurações de logon do Pinterest Social por meio da interface de usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon social do Pinterest</strong>.<br /> ou</li>
       <li>Copie quaisquer novas configurações da Pinterest Cloud do local anterior para o novo local apropriado em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site da AEM Communities para fazer referência à nova Configuração de logon do Pinterest Social definindo a propriedade <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service do Pinterest Connect herdado de qualquer raiz do site da AEM Communities atualizada para fazer referência ao novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de Pontuação {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para alinhar com a nova estrutura do repositório, as regras de pontuação podem ser armazenadas em <code>/apps/settings/</code> ou /<code>conf/.../settings</code></p>
    <ol>
     <li>Para <code>/apps/settings</code>, isso atuaria como regras globais ou padrão gerenciadas no SCM.</li>
    </ol> <p>Crie configurações sensíveis ao contexto em <code>/conf/</code> usando CRXDELite:</p>
    <ol>
     <li>Crie as configurações no <code>/conf/.../settings</code> local <br /> desejado </li>
     <li>O site de comunidades deve ter a propriedade <code>cq:conf </code>definida.
      <ol>
       <li>Se nenhum <code>cq:conf</code> estiver definido, as regras de pontuação serão lidas diretamente do caminho especificado para a propriedade '<code>scoringRules</code>' no nó raiz do site, por exemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpeza: Remover o recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon do Twitter Social {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Todas as novas configurações da nuvem do Twitter devem ser migradas para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o novo local.
      <ol>
       <li>Recrie manualmente as novas Configurações de login social do Twitter por meio da interface de usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de login social do Twitter</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas Configurações da nuvem do Twitter de Local anterior para o Novo local apropriado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site da AEM Communities para fazer referência à nova Configuração de logon social do Twitter definindo a propriedade <code>[cq:Page]/jcr:content@cq:conf</code> como o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service herdado do Twitter Connect de qualquer raiz do site da AEM Communities atualizada para fazer referência ao novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Diversos {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>O Adobe disponibilizou um utilitário de migração em:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Os modelos personalizados existentes serão movidos para <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

