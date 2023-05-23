---
title: Reestruturação do repositório para o AEM Communities no 6.4
seo-title: Repository Restructuring for AEM Communities in 6.4
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.4 for Communities.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# Reestruturação do repositório para o AEM Communities no 6.5 {#repository-restructuring-for-aem-communities-in}

Conforme descrito no pai [Reestruturação do repositório no AEM 6.4](/help/sites-deploying/repository-restructuring.md) , os clientes que estiverem atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a solução da AEM Communities. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com atualização para 6.5**

* [Modelos de Notificação por Email](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurações de assinatura](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes de uma atualização futura**

* [Configurações de insígnias](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Designs do console do Communities clássico](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurações de logon social do facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurações de opções de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurações de logon social do pinterest](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurações de pontuação](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurações de logon social do twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Diversos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Com atualização para 6.5 {#with-upgrade}

### Modelos de Notificação por Email {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>A migração manual é necessária se você quiser mudar para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Granite Configuration Manager para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> para <code>true</code> no campo "<code>/libs/settings/community/subscriptions</code>"e adicionar um <code>nt:unstructured</code> nó filho.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de assinatura {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>A migração manual é necessária se você quiser mudar para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Granite Configuration Manager para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> para <code>true</code> no campo "<code>/libs/settings/community/subscriptions</code>"e adicionar um <code>nt:unstructured</code> nó filho.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de Watchwords {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>Uma tarefa de Migração lenta está disponível para limpar as Configurações de comunidades.<br /> <p>A tarefa move palavras de ordem de <code>/etc/watchwords</code> para <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se as palavras de ordem personalizadas forem armazenadas no SCM, elas deverão ser implantadas no <code>/apps/settings/...</code> e você deve garantir que não haja sobreposição de <code>/conf/global/settings/...</code> configuração que teria precedência.</p> <p>A tarefa de migração remove <code>/etc</code> locais.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

## Antes de uma atualização futura {#prior-to-upgrade}

### Configurações de insígnias {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><strong>Regras de medalha:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imagens da insígnia:</strong></p> <p>Para imagens padrão: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imagens personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>A migração manual é necessária.</p> <p>Se a instância tiver personalizado as regras de atribuição de tags/pontuação, não há uma maneira automatizada de colocar todas as regras em um intervalo. São necessárias entradas do cliente sobre qual período de configuração (global ou específico do site) você deseja usar para o site.</p> <p>Nenhuma interface do usuário disponível para configurar a medalha e a pontuação de um site.</p> <p>Para alinhar com a nova estrutura do repositório:</p>
    <ol>
     <li>Criar um bucket de contexto de site usando o <strong>Navegador de configuração</strong> em <strong>Ferramentas</strong></li>
     <li>Ir para a raiz do site</li>
     <li>Definir <code>cq:confproperty</code> ao caminho do bucket onde deseja armazenar todas as configurações. O mesmo pode ser definido pelo site <strong>Assistente de edição - Definir entrada de configuração na nuvem</strong>.</li>
     <li>Mover regras de medalha e regras de pontuação relevantes de <code>/etc/community/*</code> ao bucket de contexto do site criado na etapa anterior.</li>
     <li>Ajuste as regras de criação de selo e as propriedades das regras de pontuação na raiz do site para ter referências relativas aos novos locais de regras.
      <ol>
       <li>Por exemplo, se a propriedade para <code>cq:conf = /conf/we-retail</code>, depois <code>badgingRules [] = community/badging/rules</code> se as regras agora forem movidas para esse novo bucket.</li>
      </ol> </li>
     <li>Da mesma forma, ajuste as referências às regras de pontuação em um nó de regra de marcação para ter um caminho relativo.</li>
    </ol> <p> </p> <p>Por fim, limpe removendo o recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Designs do console do Communities clássico {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon social do facebook {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer novas Configurações de nuvem do Facebook devem ser migradas para o Novo local.</p>
    <ol>
     <li>Migre as configurações existentes no local anterior para o novo local.
      <ol>
       <li>Recriar manualmente novas configurações de logon social do Facebook por meio da interface de criação do AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon social do Facebook</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas configurações de nuvem do Facebook do local anterior para o novo local apropriado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova Configuração de logon social do Facebook definindo o <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service Facebook Connect herdado de qualquer raiz de site AEM Communities atualizada para fazer referência ao novo local.</li>
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
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td>N/A<br /> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon social do pinterest {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer novas Configurações de nuvem do Pinterest devem ser migradas para o Novo local.</p>
    <ol>
     <li>Migre as configurações existentes no local anterior para o novo local.
      <ol>
       <li>Recriar manualmente novas configurações de logon social do Pinterest por meio da interface de criação do AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon social do Pinterest</strong>.<br /> ou</li>
       <li>Copie quaisquer novas configurações de nuvem do Pinterest do local anterior para o novo local apropriado em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova Configuração de logon social do Pinterest por meio das configurações de <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service Pinterest Connect herdado de qualquer raiz de site AEM Communities atualizada para fazer referência ao novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de pontuação {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Para alinhar-se à nova estrutura do repositório, as regras de pontuação podem ser armazenadas no <code>/apps/settings/</code> ou /<code>conf/.../settings</code></p>
    <ol>
     <li>Para <code>/apps/settings</code>, isso atuaria como regras globais ou padrão gerenciadas no SCM.</li>
    </ol> <p>Criar configurações sensíveis ao contexto no <code>/conf/</code> usando CRXDELite:</p>
    <ol>
     <li>Crie as configurações no <code>/conf/.../settings</code> localização<br /> </li>
     <li>O site das comunidades deve ter o <code>cq:conf </code>propriedade definida.
      <ol>
       <li>Se não <code>cq:conf</code> for definido, as regras de pontuação serão lidas diretamente do caminho fornecido para a propriedade '<code>scoringRules</code>' no nó raiz do site, por exemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpeza: remover o recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon social do twitter {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>Quaisquer novas Configurações de nuvem do Twitter devem ser migradas para o Novo local.</p>
    <ol>
     <li>Migre as configurações existentes no local anterior para o novo local.
      <ol>
       <li>Recriar manualmente novas configurações de logon social do Twitter por meio da interface de criação do AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon social do Twitter</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas configurações de nuvem do Twitter do local anterior para o novo local apropriado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova Configuração de logon social do Twitter definindo o <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto no Novo local.</li>
     <li>Desassocie o Cloud Service Twitter Connect herdado de qualquer raiz de site AEM Communities atualizada para fazer referência ao novo local.</li>
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
   <td><strong>Local anterior</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Novos locais</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Orientações em matéria de reestruturação</strong></td>
   <td><p>o Adobe forneceu um utilitário de migração em:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Os modelos personalizados existentes seriam transferidos para <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
