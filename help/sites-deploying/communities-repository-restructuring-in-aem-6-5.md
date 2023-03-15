---
title: Reestruturação do repositório para AEM Communities no 6.4
seo-title: Repository Restructuring for AEM Communities in 6.4
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura de repositório no AEM 6.4 para Comunidades.
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

# Reestruturação do repositório para AEM Communities no 6.5 {#repository-restructuring-for-aem-communities-in}

Conforme descrito no pai [Reestruturação do repositório no AEM 6.4](/help/sites-deploying/repository-restructuring.md) , os clientes que atualizam para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações do repositório que afetam a solução da AEM Communities. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com a atualização 6.5**

* [Modelos de notificação por email](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurações de assinatura](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes da atualização futura**

* [Configurações de marcação](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Designs clássicos do console do Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurações de logon do facebook Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurações de opções de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurações de logon do pinterest Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurações de pontuação](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurações de logon do twitter Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
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
   <td><strong>Novas localizações</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>A migração manual é necessária se você deseja migrar para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Gerenciador de configuração do Granite para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> para <code>true</code> no "<code>/libs/settings/community/subscriptions</code>" e adicione um <code>nt:unstructured</code> nó filho.</p> </td>
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
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>A migração manual é necessária se você deseja migrar para o novo caminho em "<code>/apps/settings</code>". Você pode usar o Gerenciador de configuração do Granite para executar a migração.</p> <p>Você pode executar a migração definindo a propriedade <code>mergeList</code> para <code>true</code> no "<code>/libs/settings/community/subscriptions</code>" e adicione um <code>nt:unstructured</code> nó filho.</p> </td>
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
   <td><strong>Novas localizações</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td>Uma tarefa de Migração preguiçosa está disponível para limpar as Configurações das comunidades.<br /> <p>A tarefa move palavras de observação de <code>/etc/watchwords</code> para <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se palavras de ordem personalizadas forem armazenadas no SCM, elas deverão ser implantadas em <code>/apps/settings/...</code> e você deve garantir que não haja sobreposição <code>/conf/global/settings/...</code> configuração que teria prioridade.</p> <p>A tarefa de migração é removida <code>/etc</code> locais.</p> </td>
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
   <td><strong>Novas localizações</strong></td>
   <td><p><strong>Regras de emblema:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imagens do emblema:</strong></p> <p>Para imagens padrão: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imagens personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>É necessária a migração manual.</p> <p>Se a instância personalizou as regras de classificação/pontuação, não há uma maneira automatizada de colocar todas as regras em um compartimento. Precisa de informações do cliente em qual conf bucket (global ou específico do site) você deseja usar para seu site.</p> <p>Nenhuma interface de usuário disponível para configurar a marcação e a pontuação de um site.</p> <p>Para alinhar com a nova estrutura de repositório:</p>
    <ol>
     <li>Criar um bucket de contexto de site usando o <strong>Navegador de configuração</strong> under <strong>Ferramentas</strong></li>
     <li>Ir para a raiz do Site</li>
     <li>Definir <code>cq:confproperty</code> para o caminho do bucket onde deseja armazenar todas as suas configurações. O mesmo pode ser definido por meio do site <strong>Assistente de Edição - Definir entrada de configuração de nuvem</strong>.</li>
     <li>Mover regras de classificação e regras de pontuação relevantes de <code>/etc/community/*</code> ao bucket de contexto do site criado na etapa anterior.</li>
     <li>Ajuste as regras de classificação e as propriedades de regras de pontuação na raiz do site para ter referências relativas a novos locais de regras.
      <ol>
       <li>Por exemplo, se a propriedade de <code>cq:conf = /conf/we-retail</code>, em seguida <code>badgingRules [] = community/badging/rules</code> se as regras agora forem movidas para este novo bucket.</li>
      </ol> </li>
     <li>Da mesma forma, ajuste as referências às regras de pontuação em um nó de regra de classificação para ter um caminho relativo.</li>
    </ol> <p> </p> <p>Finalmente, limpe removendo o recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Designs clássicos do console do Communities {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
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

### Configurações de logon do facebook Social {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer nova configuração da Facebook Cloud deve ser migrada para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o Novo local.
      <ol>
       <li>Recrie manualmente as novas configurações de logon do Facebook Social por meio da interface do usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon do Facebook Social</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas configurações da Facebook Cloud do local anterior para o novo local adequado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova configuração de logon do Facebook Social definindo a variável <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto na Nova Localização.</li>
     <li>Desassocie o Cloud Service do Facebook Connect herdado de qualquer raiz de site do AEM Communities atualizada para fazer referência ao novo local.</li>
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
   <td><strong>Novas localizações</strong></td>
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

### Configurações de logon do pinterest Social {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer nova configuração da Pinterest Cloud deve ser migrada para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o Novo local.
      <ol>
       <li>Recrie manualmente as novas configurações de logon do Pinterest Social por meio da interface do usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon do Pinterest Social</strong>.<br /> ou</li>
       <li>Copie quaisquer novas configurações da Pinterest Cloud do local anterior para o novo local apropriado em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova Configuração de logon do Pinterest Social usando as configurações da <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto na Nova Localização.</li>
     <li>Desassocie o Cloud Service do Pinterest Connect herdado de qualquer raiz de site do AEM Communities atualizada para fazer referência ao novo local.</li>
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
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Para se alinhar com a nova estrutura do repositório, as regras de pontuação podem ser armazenadas em <code>/apps/settings/</code> ou /<code>conf/.../settings</code></p>
    <ol>
     <li>Para <code>/apps/settings</code>, funcionaria como regras globais ou padrão gerenciadas no SCM.</li>
    </ol> <p>Criar configurações sensíveis ao contexto em <code>/conf/</code> usando o CRXDELite:</p>
    <ol>
     <li>Crie as configurações no <code>/conf/.../settings</code> localização<br /> </li>
     <li>O site das Comunidades deve ter o <code>cq:conf </code>conjunto de propriedades.
      <ol>
       <li>Se não <code>cq:conf</code> for definida, as regras de pontuação serão lidas diretamente do caminho especificado para a propriedade '<code>scoringRules</code>No nó raiz do site, por exemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpeza: Remover o recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações de logon do twitter Social {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>Qualquer nova configuração da Twitter Cloud deve ser migrada para o novo local.</p>
    <ol>
     <li>Migre as configurações existentes no Local anterior para o Novo local.
      <ol>
       <li>Recrie manualmente as novas configurações de logon do Twitter Social por meio da interface do usuário de criação de AEM em <strong>Ferramentas &gt; Cloud Services &gt; Configuração de logon do Twitter Social</strong>.<br /> ou <br /> </li>
       <li>Copie quaisquer novas configurações da Twitter Cloud do local anterior para o novo local adequado, em <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Atualize qualquer raiz do site do AEM Communities para fazer referência à nova configuração de logon do Twitter Social definindo a variável <code>[cq:Page]/jcr:content@cq:conf</code> para o caminho absoluto na Nova Localização.</li>
     <li>Desassocie o Cloud Service do Twitter Connect herdado de qualquer raiz de site do AEM Communities atualizada para fazer referência ao novo local.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Localização anterior</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Novas localizações</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Orientação relativa à reestruturação</strong></td>
   <td><p>O Adobe forneceu um utilitário de migração em:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Os modelos personalizados existentes seriam movidos para <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
