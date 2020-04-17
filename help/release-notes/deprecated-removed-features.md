---
title: Recursos obsoletos e removidos
description: Notas de versão específicas de recursos obsoletos e removidos do Adobe Experience Manager 6.5.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 4be5286858b255a30983b5987ac54c4e71dd4f2f

---


# Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

As seguintes regras se aplicam para comunicar a remoção/substituição iminente das funcionalidades do AEM:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Embora obsoletos, os recursos ainda estão disponíveis, mas não serão aprimorados.
1. A remoção de funcionalidades obsoletas ocorrerá assim que possível na versão principal seguinte. A data definida para a remoção será anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoleto no AEM 6.5. Normalmente, os recursos são, em primeiro lugar, marcados como obsoletos, com remoção planejada para uma versão futura, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação no momento, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

<table>
 <tbody>
  <tr>
   <td><b>Área</b></td>
   <td><b>Recurso</b></td>
   <td><b>Substituição</b></td>
  </tr>
  <tr>
   <td>Integração da Creative Cloud</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">O AEM para o compartilhamento</a> de pastas da Creative Cloud foi introduzido no AEM 6.2 como uma forma de fornecer aos usuários criativos acesso aos ativos do AEM, para que possam abri-los em aplicativos CC e carregar novos arquivos ou salvar alterações no AEM. Uma nova funcionalidade lançada no aplicativo da Creative Cloud, o Adobe Asset Link, fornece uma experiência de usuário melhor e acesso avançado a ativos do AEM diretamente do Photoshop, InDesign e Illustrator.</p> <p>A Adobe não planeja fazer aprimoramentos adicionais ao AEM para a integração do Compartilhamento de pastas da Creative Cloud. Embora o recurso esteja incluído no AEM, os clientes são recomendados a suar soluções de substituição.</p> </td>
   <td>Recomenda-se que os clientes alternem para os novos recursos de integração da Creative Cloud, incluindo o Adobe Asset Link ou o aplicativo de desktop do AEM. Revise as <a href="/help/assets/aem-cc-integration-best-practices.md">Práticas recomendadas de integração do AEM e Creative Cloud</a> para obter mais detalhes.</td>
  </tr>
  <tr>
   <td>Ativos</td>
   <td>
    <ol>
     <li>O AssetDownloadServlet é desabilitado por padrão para as instâncias de publicação. Para obter mais detalhes, consulte <a href="/help/sites-administering/security-checklist.md">Lista de verificação de segurança do AEM</a>.</li>
     <li>Se um usuário não tiver permissões suficientes (leitura e gravação) em /content/dam/collections, não poderá criar uma Coleção.</li>
    </ol> </td>
   <td>
    <ol>
     <li>Configuração descrita na <a href="/help/sites-administering/security-checklist.md">Lista de verificação de segurança do AEM</a>.</li>
     <li>Respeita a configuração do controle de acesso de usuário e garante as permissões apropriadas.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search&amp;Promote</td>
   <td><p>A integração com o Adobe Search &amp; Promote está obsoleta.</p> <p>A Adobe não planeja fazer melhorias à integração do Search &amp; Promote. Observe que a integração do Search &amp; Promote permanece compatível ainda que obsoleta.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Gerente de marcas DTM</td>
   <td>A integração com o DTM (Dynamic Tag Manager) está obsoleta.</td>
   <td>Alterne para usar o Adobe Experience Platform Launch como um gerenciador de marcas</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Com a adição da capacidade do·AEM se conectar ao serviço do Adobe Target usando a API do Adobe Target Standard (Rest API) baseada en Adobe I/O no AEM 6.5, a API (XML) do Target Classic será descontinuada.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">Reconfigure a integração para usar a nova API</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Usar a integração baseada em mbox.js com o Adobe Target no AEM está obsoleto.</td>
   <td>Alternar para usar at.js 1.x</td>
  </tr>
  <tr>
   <td>Comércio</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> foi fornecido em 2018 como um conjunto de microserviços para permitir a integração entre o AEM e os mecanismos de comércio.</p> <p>Depois que a Adobe adquiriu a Magento em meados de 2018, a Adobe decidiu alterar sua abordagem por dois motivos: </p> <p><strong>1.</strong> A Magento tem seu próprio conjunto de APIs de comércio (REST e GraphQL) e não é uma boa prática manter dois conjuntos de APIs </p> <p><strong>2.</strong> As tendências de mercado indicaram que os clientes estavam se movendo para o GraphQL, porque é uma forma mais eficiente de consultar dados. Em 2019, a Adobe lançou a nova Commerce Integration Framework usando as APIs GraphQL da Magento como fonte de verdade.</p> <p>A Adobe não planeja fazer nenhum investimento adicional em CIF REST. Os clientes são altamente aconselhados a usar a solução de substituição.</p> </td>
   <td><p>Para integrações AEM-Magento, mude para <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF Archetype</a>e <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF Componentes principais</a></p> <p>Consulte Integração do <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEM e do Magento usando a Commerce Integration Framework</a> para obter mais informações.</p> <p>O apoio à integração de terceiros (que não o Magento) com a nova abordagem está no nosso roteiro.</p> </td>
  </tr>
  <tr>
   <td>Componentes (AEM Sites)</td>
   <td><p>A Adobe não planeja fazer aprimoramentos adicionais à maioria dos componentes de base armazenados em /libs/foundation/components.</p> <p>Procure pela propriedade <strong>cq:deprecated</strong> e <strong>cq:deprecatedReason</strong> na pasta de componente.</p> <p>O AEM 6.5 inclui os componentes básicos, e os clientes que atualizam de versões anteriores podem continuar usando-os como estão. Além disso, os componentes básicos permanecem totalmente compatíveis enquanto estão sendo descontinuados. </p> </td>
   <td>Recomenda-se que os clientes usem os componentes principais para projetos futuros. Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>Componentes (AEM Sites)</td>
   <td>Os componentes do Importador de design /libs/wcm/designimporter/components foram marcados como obsoletos a partir da versão 6.5. A Adobe não planeja fazer aprimoramentos adicionais a essa implementação do importador de design.</td>
   <td>A Adobe planeja fornecer uma implementação de backup alternativa do caso de uso em versões futuras.</td>
  </tr>
  <tr>
   <td>Componentes (AEM Forms)</td>
   <td><p>A etapa de assinatura permite que os usuários verifiquem e assinem um formulário adaptável. Em versões anteriores, a etapa de assinatura podia usar os componentes Assinatura do Adobe Sign e da Assinatura de script como campos de assinatura. No AEM 6.5 Forms, a experiência de assinatura baseada em Assinatura de script da Etapa de assinatura está obsoleta.</p> </td>
   <td>
    <ul>
     <li>Se você tiver realizado uma instalação nova:
      <ul>
       <li>Use a experiência de assinatura baseada no Adobe Sign em uma etapa de assinatura em um formulário adaptável.</li>
       <li>Use o componente de Assinatura de script independente em um formulário adaptável, comunicação interativa e formulários HTML5.</li>
      </ul> </li>
     <li>Se você tiver atualizado de uma versão anterior para o AEM 6.5 Forms:<br />
      <ul>
       <li>Continue usando a experiência de assinatura baseada em assinatura de script da Etapa de assinatura com formulários que já usam o recurso.<br /> </li>
       <li>Use o componente de assinatura independente Scribble ou a experiência de assinatura baseada no Adobe Sign em uma etapa de assinatura ao criar um novo formulário. </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Estrutura de descarregamento do Granite</p> <p>A Adobe não planeja fazer aprimoramentos adicionais à estrutura de descarregamento introduzida na versão 5.6.1 para externalizar processamento do ativo. </p> </td>
   <td>A Adobe está trabalhando em uma estrutura de descarregamento nativa de nuvem de última geração.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Hobbes.js</p> <p>A Adobe não planeja fazer mais aprimoramentos na estrutura de teste da interface do usuário do hobbes.js.</p> </td>
   <td>A Adobe recomenda que os clientes usem a automação Selenium.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>biblioteca do cliente da interface do usuário do jQuery</p> <p>A Adobe não planeja manter e atualizar a biblioteca do cliente da interface do usuário do jQuery que é enviada como parte da distribuição (Quickstart)</p> </td>
   <td>A Adobe recomenda que os clientes que ainda precisam da interface do usuário do jQuery para obter o código a fim de adicioná-lo à base de códigos do projeto.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Biblioteca do cliente jQuery Animation (granite.jquery.animation)</p> <p>A Adobe não planeja manter e atualizar a biblioteca do cliente de animação do jQuery que é enviada como parte da distribuição (Quickstart)</p> </td>
   <td>A Adobe recomenda que os clientes que ainda precisam de jQuery Animations para seus códigos adicionem-na à base de códigos do projeto.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Biblioteca do cliente do Handlebars</p> <p>A Adobe não planeja manter e atualizar a biblioteca do cliente do Handlebars que é enviada como parte da distribuição (Quickstart)</p> </td>
   <td>A Adobe recomenda que os clientes que ainda precisam de handlebars para seus códigos adicionem-nos à base de códigos do projeto.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Biblioteca do cliente do Lawnchair</p> <p>A Adobe não planeja manter e atualizar a biblioteca do cliente do Lawnchair que é enviada como parte da distribuição (Quickstart)</p> </td>
   <td>A Adobe recomenda que os clientes que ainda precisam do Lawndish para obter seu código adicionem-no à base de códigos do projeto.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Biblioteca do cliente do Granite.Sling.js</p> <p>A Adobe não planeja aprimorar a biblioteca do cliente do Granite.Sling.js que é enviada como parte da distribuição (Quickstart)</p> </td>
   <td>A Adobe recomenda que os clientes que confiam na capacidade da biblioteca reformem seu código para não mais usá-lo.</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td>Usar a YUI para compactar/diminuir as bibliotecas do cliente do Javascript. A Adobe não planeja atualizar a biblioteca YUI. Até o AEM 6.4, o padrão do YUI era minimizar o JavaScript com a opção de alternar para o Google Closure Compiler (GCC). Ao iniciar o AEM 6.5, o GCC é o padrão.</td>
   <td>A Adobe recomenda que os clientes que atualizam para o AEM 6.5 mudem para o GCC para sua implementação</td>
  </tr>
  <tr>
   <td>Desenvolvedores</td>
   <td><p>Editor de caixa de diálogo da interface do usuário clássica no CRXDE lite</p> <p>A Adobe não planeja aprimorar o editor de caixa de diálogo da interface do usuário clássica que é enviado como parte da distribuição (Quickstart)</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Forms</td>
   <td><p>A integração do AEM Forms com o AEM Mobile&lt; está obsoleta </p> </td>
   <td>Nenhuma substituição </td>
  </tr>
 </tbody>
</table>

## Recursos removidos {#removed-features}

Esta seção lista recursos e recursos que foram removidos do AEM 6.5. As versões anteriores tinham esses recursos marcados como obsoletos.

| Área | Recurso | Substituição |
|--- |--- |--- |
| Mapa de Atividades do Analytics | A versão do Mapa de Atividades incluída no AEM. | Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM. Use o plug-in [Activity Map fornecido pelo Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integrações | A integração do ExactTarget foi removida da distribuição padrão (Início rápido) e não está mais disponível. | Nenhuma substituição |
| Integrações | A integração da API do Salesforce Force foi removida da distribuição padrão (Quickstart) e agora é um pacote adicional de instalação do PackageShare. | O recurso ainda está disponível. |
| Forms | O suporte para o serviço Adobe Central Migration Bridge foi removido, uma vez que o produto Adobe Central não é mais compatível. | Nenhuma substituição |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nenhuma substituição |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nenhuma substituição |
| Forms | A atualização de hop único do LiveCycle ES4 SP1 para o AEM 6.5 Forms no JEE não está disponível | Consulte os caminhos [de atualização](../forms/using/upgrade.md) disponíveis na documentação de atualização do AEM Forms. |
| Desenvolvedores | Firebug Lite foi removido da distribuição padrão (Quickstart) | Use os consoles de desenvolvedor integrados do navegador |
| Desenvolvedores | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Nenhuma substituição |
| Ativos | O recurso de descarregamento de Ativos foi removido do AEM 6.5 | Nenhuma substituição |
| Cache | `system/console/slingjsp` for removido não estiver mais disponível no AEM 6.5. | Classes e cache leve são armazenados no pacote Apache Sling Commons FileSystem ClassLoader. Você pode verificar o número do pacote no console da Web do AEM e remover a pasta de cache diretamente do sistema de arquivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Anúncio prévio da próxima versão {#pre-announcement-for-next-release}

Esta seção é usada para anunciar previamente as alterações na versão futura, que não estão obsoletas, mas afetará os clientes. Elas são fornecidas para propósito de planejamento.

| Área | Recurso | Anúncio |
|--- |--- |--- |
| Foundation | Estrutura da interface do usuário | A Adobe está planejando descontinuar os componentes do Coral UI 2 em 2019. O Coral UI 3 foi introduzido no AEM 6.2, e o AEM 6.5 é baseado completamente no Coral 3. A Adobe recomenda que clientes e parceiros tenha interfaces do usuário integradas com o Coral 2 para refatorá-las para o Coral 3. A Adobe está fornecendo uma ferramenta para converter caixas de diálogo do Coral 2 para o Coral 3 - [Leia mais](/help/sites-developing/dialog-conversion.md). |
