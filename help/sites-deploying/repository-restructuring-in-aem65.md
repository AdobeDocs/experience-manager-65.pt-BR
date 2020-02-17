---
title: Reestruturação do repositório no AEM 6.5
seo-title: Reestruturação do repositório no AEM 6.5
description: Saiba mais sobre a reestruturação do repositório no AEM 6.5
seo-description: Saiba mais sobre a reestruturação do repositório no AEM 6.5
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# Reestruturação do repositório no AEM 6.5 {#repository-restructuring-in-aem}

## Introdução {#introduction}

Antes do AEM 6.5, o código do cliente era implantado em áreas imprevisíveis do JCR que estavam sujeitas a alterações nas atualizações. Por isso, era comum que as versões formais do AEM (versões principais, pacotes de recursos, pacotes de serviços ou hotfixes) substituíssem o código, a configuração ou o conteúdo personalizado. Além disso, as alterações no cliente às vezes sobrescrevem o código de produto ou conteúdo do AEM, quebrando a funcionalidade do produto.

Estes conflitos nem sempre foram resolvidos automaticamente, exigindo tempo de processamento significativo para sinalizar, e exigiu intervenção humana para resolver, cuja resolução nem sempre foi clara. Ao delinear claramente as hierarquias para o código de produto e o código do cliente do AEM, esses conflitos podem ser evitados.

Para esse fim, a partir do AEM 6.5 e para continuar em versões futuras, o conteúdo está sendo reestruturado `/etc` para outras pastas no repositório, juntamente com diretrizes sobre qual conteúdo vai para onde, respeitando as seguintes regras de alto nível:

* O código de produto AEM sempre será colocado em `/libs`, o que não deve ser substituído pelo código personalizado
* O código personalizado deve ser colocado em `/apps`, `/content`e `/conf`

Este artigo é organizado em três seções, representando o tipo de conteúdo que foi removido de `/etc`:

1. Configuração
1. Bibliotecas do lado do cliente
1. Diversos

Cada seção inclui:

* uma tabela com os locais reestruturados e contexto adicional. Em breve, espera-se que as tabelas sejam formatadas em uma estrutura mais plana para melhorar a legibilidade.
* uma estratégia de extensibilidade que permite ao código personalizado estender com êxito o código de aplicativo AEM que reside em `/libs`.

## Compatibilidade com versões anteriores {#backwards-compatibility}

Na maioria dos casos, a compatibilidade com versões anteriores dos locais antigos é mantida após a atualização para o AEM 6.5. Isso é feito pela preservação e observância dos locais antigos por código de produto, além dos novos locais adicionados. Na maioria dos casos, a lógica condicional é usada para verificar se a pasta herdada existe e para ler o conteúdo desse local em vez do novo local.

Em sua própria linha do tempo após a atualização 6.5, os clientes são incentivados a remover os locais antigos para que o conteúdo nos novos locais seja usado. As tabelas abaixo incluem instruções para aderir à nova estrutura de conteúdo por local.

>[!NOTE]
>
>Uma instância atualizada no local incluirá locais de conteúdo antigos, além dos novos locais. Uma nova instalação do desenvolvedor incluirá apenas os novos locais.

## Como ler as tabelas {#how-to-read-the-tables}

A tabela em cada seção inclui:

* a solução AEM (sites, ativos, formulários etc.) para a qual este conteúdo é relevante
* a localização antiga (6.4 e anterior)
* a nova localização 6.5
* Instruções para alinhar com a nova estrutura de conteúdo. Por exemplo, pode ser necessário executar um script ou mover arquivos manualmente nas semanas ou meses após uma atualização 6.5
* A abordagem usada pelo AEM para manter a compatibilidade retroativa de locais de conteúdo antigos para clientes que atualizam para o AEM 6.5 de uma versão anterior

## Configuração {#configuration}

Os locais de conteúdo desta seção geralmente referem-se ao conteúdo que reside em uma `/settings` pasta em `/libs`, `/apps`ou `/conf`.

### Estratégia de extensibilidade {#extensibility-strategy}

Em geral, mas com algumas exceções, o conteúdo desta seção pode ser estendido usando o recurso Configuração [](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) sensível ao contexto do Apache Sling.

Resumindo, a Configuração sensível ao contexto permite que o conteúdo em uma parte do repositório seja sobreposto várias vezes pelo conteúdo em outras partes do repositório. Por exemplo, o conteúdo em `/libs` pode ser sobreposto pelo conteúdo em `/apps`, que pode ser sobreposto pelo conteúdo em `/conf`. Além disso, o conteúdo em uma pasta global em `/conf` pode ser sobreposto por um &quot;locatário&quot; ou &quot;site&quot; específico (por exemplo, `/conf/we-retail/settings`).

Normalmente, a Configuração sensível ao contexto é usada como uma estratégia para estender as configurações de recursos, mas há casos em que ela é usada por outros tipos de conteúdo.

A tabela abaixo inclui uma coluna adicional chamada &quot;Tipo de configuração&quot; para explicar até que ponto uma configuração pode ser sobreposta. Estes são detalhes adicionais sobre esses tipos de configuração:

**sem reconhecimento de contexto**

* Os recursos podem estar em estruturas de pastas sensíveis ao contexto (como `/libs/settings`), mas sempre referenciados pelo caminho absoluto, de modo que o reconhecimento do contexto não esteja em vigor.
* Os recursos podem estar em qualquer lugar. Por exemplo, as licenças DRM do Assets podem estar em `/content/my-customer/licenses/creative-commons.html`
* Exemplos:

   * Scripts de fluxo de trabalho -> `/apps/settings/workflow/scripts/noop.ecma`
   * Licenças DRM de ativos -> `/apps/settings/dam/drm/my-license`

**somente global**

* Recurso com apenas configuração global
* Como ponto de referência, tome a precedência das configurações neste exemplo: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* O AEM oferece suporte somente à configuração global e não a configurações locatárias
* O AEM sempre começará a procurar configurações no nível /conf/global primeiro

* Exemplos:

   * Inicializadores do fluxo de trabalho -> `/libs/settings/workflow/launcher`
   * Modelos do fluxo de trabalho -> `/conf/global/settings/workflow/models`

**sensível a inquilinos**

* Para configurações com reconhecimento de locatário, consulte este exemplo para obter a precedência dos caminhos de configuração: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, onde we-retail é o nome do inquilino. As configurações com reconhecimento de locatários também suportam sublocatários.

* O AEM suporta configurações tenantizadas. Respeita a propriedade `cq:conf` na hierarquia
* Exemplos:

   * Modelos editáveis -> `/conf/we-retail/settings/wcm/templates`
   * Configurações da nuvem -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>Solução</strong></td>
   <td><strong>Local anterior</strong><br /> </td>
   <td><strong>Nova localização</strong></td>
   <td><strong>Tipo de configuração sensível ao contexto</strong><br /> </td>
   <td><strong>Abordagem de compatibilidade com versões anteriores</strong></td>
   <td><strong>Requisitos para alinhar ao modelo mais recente</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>sensível a inquilinos</td>
   <td><p>Serviços de nuvem herdados.</p> <p>Persistente em uma atualização no local. Código para listar e ler ainda presentes no AEM como um fallback.</p> </td>
   <td>O utilitário de migração de conteúdo lento pode ser acionado pela interface do usuário de migração do Forms para converter automaticamente no novo caminho.<br /> </td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>sensível a inquilinos</td>
   <td><p>Serviços de nuvem herdados.</p> <p>Persistente em uma configuração atualizada no local. Código para listar e ler ainda presentes no AEM como um fallback.</p> </td>
   <td>O utilitário de migração de conteúdo lento pode ser acionado pela interface do usuário de migração do Forms para converter automaticamente no novo caminho.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>sensível a inquilinos</td>
   <td>As estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas estruturas OOTB.</td>
   <td>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>sensível a inquilinos</td>
   <td>As estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas estruturas OOTB.</td>
   <td>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>sem reconhecimento de contexto</td>
   <td>As estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas estruturas OOTB.</td>
   <td>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>sensível a inquilinos</td>
   <td>As estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas estruturas OOTB.</td>
   <td><p>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</p> <p>Ao executar o fluxo de trabalho personalizado de ingestão de ativos, ainda existem referências ao local antigo em /etc. na Configuração do processo de extração de mídia. Juntamente com a mudança dos scripts para /etc para os caminhos /apps e /conf equivalentes, os argumentos do processo de Extração de mídia personalizados precisam ser alterados de caminhos absolutos para relativos, para acomodar as alterações.</p> <p>Para obter mais informações, consulte <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">esta página</a>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>sensível a inquilinos</td>
   <td>Estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas, desde as primeiras.</td>
   <td>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>sensível a inquilinos</td>
   <td>Estruturas de conteúdo herdado são respeitadas com prioridade mais alta do que as novas, desde as primeiras.</td>
   <td>As personalizações de nível de projeto precisam ser recortadas e coladas nos caminhos equivalentes <code>/apps</code> ou <code>/conf</code> , conforme aplicável.</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>sem reconhecimento de contexto</td>
   <td><p>Os Serviços de Consumo estão cientes da localização antiga.</p> <p>As configurações do local herdado são consideradas</p> </td>
   <td><br /> Mova o conteúdo personalizado de <code>/etc/design</code> para <code>/apps/settings/wcm/design</code> alinhamento com a nova estrutura do repositório. No futuro, considere atualizar seus sites para usar a funcionalidade de modelos editáveis, que substitui a necessidade do modo de design e, portanto, deste conteúdo.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>sem reconhecimento de contexto</td>
   <td>Os componentes no local antigo em <code>/etc/scaffolding</code> continuarão a funcionar, mas foram descontinuados.</td>
   <td>A Adobe recomenda que você use os novos componentes do suporte sob o novo local.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm para configurações de tela e blueprint de comércio</p> <p> </p> </td>
   <td>sem reconhecimento de contexto</td>
   <td><p>Os Serviços de Consumo estão cientes da localização antiga.</p> <p>As configurações do local herdado são consideradas.</p> </td>
   <td>As configurações precisam ser copiadas para os novos locais.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>sensível a inquilinos</td>
   <td>O recurso aproveita o Configuration Manager e ainda oferece suporte ao local antigo como fallback.</td>
   <td>
    <ol>
     <li>Realocar as configurações de <code>/etc</code> para <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>Em seguida, atualize a referência no conteúdo da seguinte maneira:</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/A</td>
   <td><p>Os serviços de consumo estão cientes da localização antiga.</p> <p>Se as configurações forem detectadas no local herdado, elas serão usadas.</p> </td>
   <td>Para alinhar com o novo modelo, as configurações precisam ser criadas nos novos locais, e os antigos em <code>/etc</code> devem ser excluídos.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>sensível a inquilinos</td>
   <td><p>Segmentos do local antigo:</p>
    <ul>
     <li>Permaneça no modo somente leitura no console de público-alvo.</li>
     <li>Ainda carregado na página (se o caminho especificado estiver selecionado em Propriedades da <strong>página &gt; Personalização &gt; Caminho</strong>do segmento).</li>
     <li>Pode ser usado para direcionamento de conteúdo.</li>
    </ul> </td>
   <td>Você pode usar a Ferramenta <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">de migração de</a> segmentos para migrar para o novo local.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/A</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>O código está ciente da localização do modelo antigo. Os modelos existentes continuarão a ser referenciados e lidos/gravados de <code>/etc</code>.</p> <p><br /> Para modelos de e-mail, se o cliente já tivesse seus modelos personalizados em outro caminho, configurando o caminho raiz <strong></strong> Modelos na Configuração <strong>de resposta de e-mail do</strong> AEM Communities, ele permaneceria como está.</p> </td>
   <td><p>Um utilitário <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">de</a> migração pode se alinhar ao modelo mais recente de modelos de AEM Communities.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>Regras do selo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imagens de emblema:</strong></p> <p>As imagens fora da caixa no local antigo em <code>/etc/community/badging/images</code> são movidas para <code>/libs/community/badging/images </code> </p> <p> </p> <p>As imagens personalizadas são movidas para <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>sensível a inquilinos</td>
   <td><p>O código está ciente dos caminhos antigos de identificação.</p> <p><br /> Ele verificará primeiro a existência de caminhos<br /> antigos. Se não estiverem presentes, usará os novos caminhos.</p> </td>
   <td><p>A migração manual é necessária para alinhar ao modelo mais recente. Siga as etapas abaixo para conseguir isso:</p>
    <ol>
     <li>Criar um bucket de contexto de site usando o navegador de configuração em <strong>Ferramentas</strong></li>
     <li>Ir para a raiz do site</li>
     <li>Defina a <code>cq:conf</code> propriedade como o caminho do bucket no qual você deseja armazenar todas as configurações. O mesmo pode ser definido pelo Assistente de edição de <strong>site - Definir entrada</strong>de configuração da nuvem e salvar as alterações</li>
     <li>Mover as regras de identificação e as regras de pontuação relevantes do bucket de contexto do site criado na etapa anterior <code>etc/community/*</code></li>
     <li>Ajuste as propriedades <code>badgingRules</code> e <code>scoringRules</code> na raiz do site para ter referências relativas aos novos locais de regras. Por exemplo, se <code>cq:conf</code> estiver definido como <code>/conf/we-retail</code>, o valor para <code>badgingRules</code> será <code>community/badging/rules</code> se as regras forem movidas para esse novo bucket</li>
     <li>Da mesma forma, ajuste as referências às regras de pontuação em um nó de regra de identificação para ter um caminho relativo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>sensível a inquilinos</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>O código está ciente dos caminhos antigos de identificação.</p> <p><br /> Ele verificará primeiro a existência de caminhos<br /> antigos. Se não estiverem presentes, usará os novos caminhos.</p> </td>
   <td><p>As etapas de migração manual são necessárias para alinhar-se ao modelo mais recente.</p> <p>As etapas são as mesmas nas regras de identificação acima.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>sem reconhecimento de contexto</td>
   <td><p>Essas configurações não são compatíveis com versões anteriores. Consulte a coluna "Requisitos para alinhar ao modelo mais recente" para obter etapas sobre como migrar para os novos locais.<br /> </p> <br /> </td>
   <td><p>É necessária uma migração manual para alinhar ao modelo mais recente. Você pode usar o Gerenciador de configurações do Granite para mover as configurações para o novo caminho em <code>/apps/settings</code>.</p> <p>Portanto, é necessário definir a <code>mergeList</code> propriedade como true no <code>/libs/settings/community/subscriptions</code> nó e adicionar um nó <code>nt:unstructured</code> filho.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>sem reconhecimento de contexto</td>
   <td>Essas configurações não são compatíveis com versões anteriores. Consulte a coluna "Requisitos para alinhar ao modelo mais recente" para obter etapas sobre como migrar para os novos locais.</td>
   <td><p>É necessária uma migração manual para alinhar ao modelo mais recente. Você pode usar o Gerenciador de configurações do Granite para mover as configurações para o novo caminho em <code>/apps/settings</code>.</p> <p>Portanto, é necessário definir a <code>mergeList</code> propriedade como true no <code>/libs/settings/community/subscriptions</code> nó e adicionar um nó <code>nt:unstructured</code> filho.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>global</td>
   <td>Essas configurações são compatíveis com versões anteriores. Se os caminhos antigos forem detectados, eles serão usados. Caso contrário, os novos caminhos terão prioridade.</td>
   <td><p>A Tarefa de migração de conteúdo lento está disponível no formato <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Para obter mais informações, consulte a documentação <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migração</a>preguiçosa.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/A</td>
   <td>Essas configurações são compatíveis com versões anteriores. Se os caminhos antigos forem detectados, eles serão usados. Caso contrário, os novos caminhos terão prioridade.</td>
   <td><p>A Tarefa de migração de conteúdo lento está disponível no formato <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>As palavras de observação terão de ser movidas manualmente de <code>/etc/watchwords</code> para <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>global</td>
   <td><p>O local herdado é usado se estiver presente e nenhuma configuração existe em <code>/libs</code> ou <code>/conf</code>.</p> <p>Ao editar modelos de fluxo de trabalho OTB, é necessário criar sobreposições sensíveis ao contexto em <code>/conf</code> para permitir que elas sejam modificáveis.</p> <p>A exportação do pacote precisa incluir o modelo em <code>/libs</code> ou <code>/conf</code> e o modelo de tempo de execução em <code>/var/workflow/models.</code></p> </td>
   <td><p>Os modelos recém-criados serão criados no <code>/conf/global/settings</code> local.</p> <p>Todas as edições feitas <code>/etc</code> ou que <code>/libs</code> exijam a criação explícita de uma substituição <code>/conf/global/settings</code> antes da edição podem ser feitas. O botão Editar precisa ser selecionado e fará com que a substituição seja criada e a edição permitida <code>/conf</code> .</p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>global</td>
   <td>O local herdado é usado se estiver presente e nenhuma configuração<br /> existe em <code>/libs</code> ou <code>/conf</code> locais. Desta forma, os lançadores personalizados são preservados.</td>
   <td><p>As configurações de iniciador recém-criadas ou editadas estão localizadas no <code>/conf</code> local.</p> <p>Todos os lançadores devem ser movidos do <code>/etc</code> local herdado para<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>global</td>
   <td>O local herdado é usado se estiver presente e nenhuma configuração<br /> existe em <code>/libs</code> ou <code>/conf</code> locais. Desta forma, os modelos de fluxo de trabalho personalizados são preservados.</td>
   <td><p>Todos os modelos de fluxo de trabalho devem ser movidos do <code>/etc</code> local herdado para <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>sem reconhecimento de contexto</td>
   <td><p>Para compatibilidade com versões anteriores, o local herdado é usado, se houver.</p> <p>Anteriormente, os modelos prontos para uso tinham que ser substituídos editando-os em <code>/etc</code>. Agora, substituir deve ser armazenado em <code>/conf/global</code>.</p> </td>
   <td>Para obter mais informações, consulte a documentação Fluxo de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>sensível a inquilinos</td>
   <td>Serviços de nuvem herdados. Será mantida em uma configuração atualizada no local. O código para listá-los e lê-los ainda está presente no produto como um fallback.</td>
   <td><p>Para mover configurações de nuvem para <code>/conf</code>, você pode:</p>
    <ul>
     <li>Crie configurações usando a nova interface<br /> de toque ou<br /> </li>
     <li>Copiar as configurações de <code>/etc/cloudservices/translation</code> para seus respectivos novos locais</li>
    </ul> <p>Quando isso for feito, as configurações precisarão ser associadas a Sites por meio de <strong>Sites &gt; Propriedades</strong> na interface do usuário.</p> <p><em>Observação: Os conectores de tradução devem ser compatíveis com o AEM 6.5 para que isso funcione.</em></p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>sensível a inquilinos</td>
   <td>Serviços de nuvem herdados. Será mantida em uma configuração atualizada no local. O código para listá-los e lê-los ainda está presente no produto como um fallback.</td>
   <td><p>Para mover configurações de nuvem para <code>/conf</code>, você pode:</p>
    <ul>
     <li>Crie configurações usando a nova interface de usuário de toque ou<br /> </li>
     <li>Copiar configurações mais antigas de <code>/etc/cloudservices/translation</code> para seus respectivos novos locais</li>
    </ul> <p>Quando isso for feito, as configurações precisarão ser associadas a Sites por meio de <strong>Sites &gt; Propriedades</strong> na interface do usuário.</p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>sensível a inquilinos</td>
   <td><p>As entradas existentes em <code>/etc</code> permanecem em vigor na atualização da instância.</p> <p>O acesso à interface do usuário de configurações de nuvem após a atualização copiará as configurações de nuvem existentes para a nova estrutura do repositório, preservando o conteúdo existente para compatibilidade com versões anteriores.</p> </td>
   <td><p>Os modelos de conteúdo são os mesmos, somente o local foi alterado para alinhar-se às configurações sensíveis ao contexto.</p> <p>A tarefa <a href="/help/sites-deploying/lazy-content-migration.md">Migração</a> lenta que abrange essas configurações de nuvem executará as seguintes ações:</p>
    <ul>
     <li>Copiar configurações da nuvem existentes em <code>/etc/cloudsettings</code> para <code>/conf/global/settings/cloudsettings</code></li>
     <li>Remover todos os filhos de <code>/etc/cloudsettings</code></li>
    </ul> <p>Entretanto, há etapas manuais que são necessárias após a atualização e antes de executar as tarefas de migração lenta:</p>
    <ul>
     <li>Todas as referências que apontam para <code>/etc/cloudsettings/*</code> a necessidade de atualização para apontar para <code>/conf/global</code></li>
    </ul> <p>Advertência:</p>
    <ul>
     <li>O <code>/etc/cloudsettings</code> contêiner precisa ser preservado</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>somente global</td>
   <td><p>Configuração da nuvem para Dynamic Media - a configuração do Scene7 (<code>dynamicmedia_scene7</code> modo de execução) permanecerá no mesmo local. O processo está funcionando como está. Se você precisar ajustar o valor de configuração da nuvem, há duas opções para fazer isso:</p>
    <ol>
     <li>Atualize uma configuração existente por meio da antiga interface de usuário de configuração em nuvem.</li>
     <li>Crie uma nova configuração de nuvem por meio da nova interface do usuário de toque. Isto terá uma precedência maior do que a anterior.</li>
    </ol> </td>
   <td><p>Para alinhar ao modelo mais recente, é necessário executar o script localizado em:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>somente global</td>
   <td><p>As predefinições do visualizador OOTB estarão disponíveis somente no novo local, enquanto a predefinição do visualizador personalizado ainda estará em vigor <code>/etc</code> até que uma modificação seja realizada.</p> <p>Depois de modificado, ele será salvo no novo local por meio da Migração lenta. O servidor de imagem incorporado verificará o caminho herdado e o novo caminho ao receber uma solicitação. Portanto, não há necessidade de alterar o código incorporado ou URL.</p> </td>
   <td><p>A predefinição do visualizador out of the box só estará disponível no novo local. Para a predefinição do visualizador personalizado, é necessário executar o script de migração neste local:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>Semelhante ao caso de compatibilidade com versões anteriores, não é necessário ajustar o copyURL/código incorporado para apontar para <code>/conf</code>. A solicitação existente para <code>/etc</code> será roteada novamente sob o capô para o conteúdo correto de <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>somente global</td>
   <td>A macro em <code>/etc</code> ainda é válida. Se modificá-lo, o nó modificado será movido para o novo local em <code>/conf</code> uma tarefa de Migração lenta.</td>
   <td><p>É necessário executar o script de migração neste local:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/A</td>
   <td><p>O perfil de vídeo predefinido será removido sem atualizar a propriedade de pastas de ativos para vincular ao perfil.</p> <p>O processo de codificação tem uma tradução integrada entre o antigo e o novo local. Ele converterá o caminho antigo para procurar no novo caminho de perfil.</p> </td>
   <td>Nenhuma alteração é necessária.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>somente global</td>
   <td><p>O perfil de vídeo personalizado será mantido como está até que você o modifique.</p> <p>Em seguida, ele será movido para o novo local por meio de uma tarefa de Migração com preguiça. Isso é semelhante ao vídeo predefinido na codificação da consulta. O processo de codificação tem um tradutor de caminho incorporado para procurar primeiro o local antigo e depois o novo local para o perfil de vídeo.</p> </td>
   <td><p>Para alinhar ao modelo mais recente, é possível executar o script de migração em:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>somente global</td>
   <td><p>Essa configuração de nuvem para a configuração híbrida do Dynamic Media (<code>dynamicmedia</code> modo de execução) permanecerá no mesmo local. O processo está funcionando como está. Se precisar ajustar o valor de configuração, você pode fazer isso de duas maneiras.</p>
    <ol>
     <li>Atualize uma configuração existente por meio da interface de usuário de configuração da nuvem antiga.</li>
     <li>Crie uma nova configuração de nuvem por meio da nova interface de usuário de toque. Isto terá uma precedência maior do que a anterior.</li>
    </ol> </td>
   <td><p>É necessário executar o script de migração para alinhar ao modelo mais recente. Você pode encontrar o script neste local:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>somente global</td>
   <td><p>A configuração da nuvem para a configuração do DM-Youtube permanecerá no mesmo local. O processo está funcionando como está. Se precisar ajustar o valor de configuração da nuvem, você pode fazer isso de duas formas:</p>
    <ol>
     <li>Atualize uma configuração existente por meio da antiga interface do usuário de configuração da nuvem.</li>
     <li>Crie uma nova configuração de nuvem por meio da interface do usuário do novo toque. Isto terá uma precedência maior do que a anterior.</li>
    </ol> </td>
   <td><p>Você pode executar um script de migração para alinhar com o modelo mais recente. O script pode ser encontrado neste local:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>somente global</td>
   <td>Nenhuma ação necessária.</td>
   <td><p>Você pode executar um script de migração para alinhar ao modo mais recente. O script pode ser encontrado neste local:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>somente global</td>
   <td>Os modelos em <code>/etc/notification/email/default/</code> têm precedência sobre os em <code>/libs/settings/notification-templates</code>.</td>
   <td>Para alinhar ao modelo mais recente, você pode criar novos modelos em <code>/apps/settings/notification-templates</code> e executar novas modificações nele.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/A</td>
   <td><p>Os Serviços de Consumo estão cientes da localização antiga.</p> <p>Se as configurações forem detectadas no local herdado, elas serão usadas.</p> </td>
   <td>Para alinhar com o novo modelo, as configurações precisam ser criadas nos novos locais, e os antigos em <code>/etc</code> devem ser excluídos.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>sem reconhecimento de contexto</td>
   <td>Um aviso é que os idiomas personalizados precisam ser adicionados à lista.<br /> </td>
   <td>Sobrepor e atualizar a nova lista com outros idiomas (se houver). Como alternativa, copiar a lista antiga para o <code>/apps</code> local também funcionaria.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>somente global</td>
   <td>Será persistente em uma configuração atualizada no local. Código para listá-los e lê-los ainda presentes no produto.</td>
   <td>Para persistir as alterações, copie o arquivo XML de <code>/etc</code> para <code>/libs</code> ou <code>/conf</code>. Como alternativa,<strong> </strong>remova o arquivo de <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## Bibliotecas do lado do cliente {#client-side-libraries}

[As bibliotecas](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) do lado do cliente são javascript e código CSS processado no navegador.

### Estratégia de extensibilidade {#extensibility-strategy-1}

O AEM fornece uma estrutura de extensibilidade para anexar vários arquivos JavaScript. Qualquer arquivo com a mesma propriedade &quot;categorias&quot; será anexado, permitindo que o código personalizado estenda o código AEM que está em `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>Solução</strong></td>
   <td><strong>Local anterior</strong><br /> </td>
   <td><strong>Nova localização</strong></td>
   <td><strong>Abordagem de compatibilidade com versões anteriores</strong></td>
   <td><strong>Requisitos para alinhar ao modelo mais recente</strong></td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>Clientlib herdado que será mantido em uma instância que foi atualizada por meio de uma atualização no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<strong><code>replaces</code></strong>" para evitar a mesclagem de clientlibs antigos e novos.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>Clientlibs herdados que serão mantidos em uma instância que foi atualizada por meio de uma atualização no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<strong><code>replaces</code></strong>" para evitar a mesclagem de clientlibs antigos e novos.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>Clientlibs legados. Será mantida em uma instância que foi atualizada por meio de uma atualização no local. Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<strong><code>replaces</code></strong>" para evitar a mesclagem de clientlibs antigos e novos.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>Isso não apresenta mais como parte do pacote pronto para uso do AEM 6.5.</td>
   <td><p>Temas predefinidos em Formulários adaptáveis.</p> <p>Será persistente em uma configuração atualizada no local.</p> </td>
   <td>Isso é parcialmente gerado pelo usuário. Isso será entregue como um pacote de conteúdo de referência com o <code>aem-forms-reference-themes</code> nome.</td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>Clientlibs legados. Será mantida em uma instância que foi atualizada por meio de uma atualização no local. Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<strong><code>replaces</code></strong>" para evitar a mesclagem de clientlibs antigos e novos.</td>
   <td>Nenhuma ação necessária.<p> </p> </td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>Clientlibs herdados do Analytics e do Target que não devem ser consumidos diretamente. </td>
   <td>Após a atualização foi limpa usando um filtro de limpeza.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>Clientlibs herdados têm nomes de categoria de cliente diferentes.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>Estas são as clientlibs herdadas. Eles serão mantidos em uma configuração atualizada no local. Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<code>replaces</code>" para evitar a mesclagem de clientlibs antigos e novos.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>Estas são as clientlibs herdadas. Será persistente em uma configuração atualizada no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>Estas são as clientlibs herdadas. Será persistente em uma configuração atualizada no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>Estas são as clientlibs herdadas. Será persistente em uma configuração atualizada no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>Estas são as clientlibs herdadas. Será persistente em uma configuração atualizada no local.</p> <p>Os novos clientlibs têm os mesmos nomes de categoria.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>Os novos clientlibs têm os mesmos nomes de categoria.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>Clientlibs legados. Será persistente em uma configuração atualizada no local. Os novos clientlibs têm os mesmos nomes de categoria junto com a propriedade "<strong>replace</strong>" para evitar a mesclagem de clientlibs antigos e novos.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>Em uma atualização no local, o arquivo herdado (/etc/clientlibs/wcm/..._) permanecerá e não será removido automaticamente, portanto, as referências ao arquivo herdado /etc/clientlibs/wcm/foundation/grid/grid_base.less continuarão sendo armazenadas.</p> <p><em>Observe que o é um caso incomum em que esse arquivo MENOS é referenciado pelo caminho absoluto por meio das instruções LESS @import e NOT pela categoria clientlib.</em></p> <p>Se o cliente MENOS referenciando o "grid_base.less" estiver apontando para um arquivo não existente, o modo Layout do modelo editável se quebrará e quaisquer ajustes feitos com ele não estarão presentes (ou seja, todos os componentes terão a largura total da página).</p> </td>
   <td>Atualize quaisquer referências no código personalizado (isto é, em qualquer arquivo MENOS que faça referência ao arquivo grid_base.less movido) para apontar para o novo local e remover o local herdado.</td>
  </tr>
 </tbody>
</table>

Estas são outras reestruturações que não se enquadram nas seções anteriores.

### Estratégia de extensibilidade {#extensibility-strategy-2}

Consulte cada linha de tabela para ver qualquer modelo de extensibilidade suportado. O conteúdo desta seção normalmente não é estendido.

## Diversos {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>Solução</strong></td>
   <td><strong>Local anterior</strong><br /> </td>
   <td><strong>Nova localização</strong></td>
   <td><strong>Abordagem de compatibilidade com versões anteriores</strong></td>
   <td><strong>Requisitos para alinhar ao modelo mais recente</strong></td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>Modelos OOTB herdados do AEM Forms Portal. Esses modelos permanecerão em /etc após uma configuração atualizada no local.</p> <p>Na lista de modelos, a palavra<em> "obsoleto</em>" será adicionada ao título do modelo para diferenciá-los com os modelos mais recentes.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Formulários AEM</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>Arquivos de anotação herdados do Gerenciamento de correspondência. Não era para ser consumido diretamente. Será limpo após a atualização usando um filtro de limpeza.</td>
   <td>Local herdado limpo após atualização usando um filtro de limpeza.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>A API do Tag Manager suporta o legado e o novo local. Quando o componente OSGi de fábrica do Gerenciador de tags do JCR é iniciado, ele detecta se está sendo executado em uma instância atualizada ou herdada e usa o local apropriado.<br /> </td>
   <td><p>Para alinhar corretamente com o novo modelo:</p>
    <ol>
     <li>Substitua as referências ao modelo antigo (<code>/etc/tags</code>) pelo novo (<code>/content/cq:tags</code>) usando a variável <code>tagID.</code></li>
     <li>Faça logon no CRXDE Lite</li>
     <li>Mover as tags de <code>/etc/tags</code> para <code>/content/cq:tags</code></li>
     <li>Reinicie o componente OSGi <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Localização antiga usada no processamento<br /> de fluxos de trabalho em voo. Os novos fluxos de trabalho usam o novo local em <code>/var.</code></td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>As Etapas do modelo de fluxo de trabalho existente que fazem referência a scripts de fluxo de trabalho no local herdado em <code>/etc/workflow/scripts</code> continuarão a apontar para esses scripts após a atualização e serão executadas corretamente.</p> <p>Observe a interface do usuário do AEM para criar as etapas do fluxo de trabalho" (Processo, Divisões, etc.) não lista mais os scripts <code>/etc/workflow/scripts</code> na lista suspensa usada para selecionar para scripts de fluxo de trabalho.</p> </td>
   <td><p>Fluxos de trabalho que aproveitam esses scripts continuarão funcionando como esperado se a etapa do processo de fluxo de trabalho associado não for editada no AEM.</p> <p>No entanto, para obter compatibilidade total com versões anteriores, inclusive quando as etapas são editadas, é necessária uma ação manual do cliente após a atualização:</p>
    <ul>
     <li>Os scripts devem ser movidos de <code>/etc/workflow/scripts</code> para <code>/apps/workflow/scripts.</code></li>
     <li>Quaisquer<strong> </strong>referências a <code>/etc/workflow/scripts</code> nas etapas do modelo de fluxo de trabalho devem ser atualizadas para fazer referência ao novo <code>/apps/workflow/scripts</code> local.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>A página do utilitário ClassicUI permanece em vigor na atualização.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Ativos AEM</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>Local temporário para reter arquivos zip gerados para a invocação de ação de download do AEM Assets.</p> <p>Não há necessidade de atualização, pois quando o cliente solicita o download do ativo, ele gerará o arquivo no novo local.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>O conteúdo antigo permanece ativo e utilizável após a atualização.</p> <p>Uma tarefa de Migração lenta é fornecida para migração para o novo local.</p> </td>
   <td><p>A migração é realizada por meio de uma tarefa de Migração com preguiça: <code>CQ64CommerceMigrationTask.</code></p> <p>Ele executa as seguintes etapas:</p>
    <ul>
     <li>Ajusta referências do local antigo para apontar para o novo local</li>
     <li>Move o conteúdo do local antigo para o novo local</li>
     <li><p>Remove o local antigo para eventualmente ativar o uso do novo local em todo o sistema</p> </li>
    </ul> <p>Os locais abrangidos pela tarefa são:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment methods<br /> </li>
     <li>/etc/commerce/Shipping-methods<br /> </li>
    </ul> <p>Para catálogos maiores, é recomendável executar a tarefa de migração de comércio individualmente, transmitindo a seguinte propriedade do sistema Java para o AEM:</p>
    <ul>
     <li>nome da propriedade: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>valor da propriedade: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>Após a migração, o AEM requer uma reinicialização.</p> </td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>O conteúdo antigo permanece ativo e utilizável após a atualização.</p> <p>Uma tarefa de Migração lenta é fornecida para migração para o novo local.</p> </td>
   <td>Consulte a descrição acima para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>O conteúdo antigo permanece ativo e utilizável após a atualização.</p> <p>Uma tarefa de Migração lenta é fornecida para migração para o novo local.</p> </td>
   <td>Consulte a descrição acima para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>Nenhuma ação necessária.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>O conteúdo antigo permanece ativo e utilizável após a atualização.</p> <p>Uma tarefa de Migração lenta é fornecida para migração para o novo local.</p> </td>
   <td>Consulte a descrição acima para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Comércio AEM</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>O conteúdo antigo permanece ativo e utilizável após a atualização.</p> <p>Uma tarefa de Migração lenta é fornecida para migração para o novo local.</p> </td>
   <td>Consulte a descrição acima para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>Novas tarefas são criadas em <code>/var/taskmanagement</code></p> <p>As tarefas existentes no local herdado ainda estarão visíveis na caixa de entrada do AEM.</p> </td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>Os pacotes AEM criados por meio do Gerenciador de pacotes AEM ainda são armazenados em <code>/etc/workflow/packages.</code></p> <p>Outros pacotes criados pelo AEM Sites e fluxos de trabalho continuam sendo armazenados em<code>/var/workflow/packages.</code></p> <p>Os pacotes encontrados em ambos <code>/etc/workflow/packages</code> e ainda <code>/var/workflow/packages</code> podem ser editados pelo Gerenciador de pacotes do AEM. </p> </td>
   <td><p>Nenhuma ação necessária.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Novas instâncias de fluxo de trabalho serão criadas <code>/var</code> automaticamente em.</td>
   <td>Nenhuma ação necessária.</td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Novo local para conteúdo de feed do Search and Promote.</p> <p>O URL antigo continua funcionando e a solicitação é encaminhada por um ServletFilter para o novo local.</p> </td>
   <td><br /> Nenhuma ação necessária. <br /> </td>
  </tr>
  <tr>
   <td>Todos os pacotes</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>Novo local para o DTM Web-Hooks.</p> <p>O URL antigo continua funcionando e a solicitação é encaminhada por um ServletFilter para o novo local.</p> </td>
   <td><br /> Nenhuma ação necessária. <br /> </td>
  </tr>
 </tbody>
</table>

