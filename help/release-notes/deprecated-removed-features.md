---
title: Recursos obsoletos e removidos na versão Adobe Experience Manager 6.5.
description: Notas de versão específicas de recursos obsoletos e removidos do Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 1e6feac534fe990d614997c4bd3ab999a4a8d479
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 45%

---


# Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

Para comunicar a remoção ou substituição iminente de recursos AEM, as seguintes regras se aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Embora obsoletos, os recursos ainda estão disponíveis, mas não são aprimorados.
1. A remoção de recursos obsoletos ocorre na versão principal a seguir, o mais tardar. A data definida para a remoção será anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoleto no AEM 6.5. Normalmente, os recursos são, em primeiro lugar, marcados como obsoletos, com remoção planejada para uma versão futura, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação no momento, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Área | Recurso | Substituição |
|---|---|---|
| Integração da Creative Cloud | O AEM ao compartilhamento de pastas do Creative Cloud foi introduzido no AEM 6.2 como uma forma de fornecer aos usuários criativos acesso aos ativos do AEM, para que eles pudessem abri-los em aplicativos CC e carregar novos arquivos ou salvar as alterações no AEM. Uma nova funcionalidade lançada no aplicativo da Creative Cloud, o Adobe Asset Link, fornece uma experiência de usuário melhor e acesso avançado a ativos do AEM diretamente do Photoshop, InDesign e Illustrator. A Adobe não planeja fazer aprimoramentos adicionais ao AEM para a integração do Compartilhamento de pastas da Creative Cloud. Embora o recurso esteja incluído no AEM, os clientes são recomendados a suar soluções de substituição. | Recomenda-se que os clientes alternem para os novos recursos de integração de Creative Cloud, incluindo o Adobe Asset Link ou AEM aplicativo de desktop. Consulte Práticas recomendadas de integração de AEM e Creative Cloud para obter mais detalhes. |
| Ativos | `AssetDownloadServlet`O é desabilitado por padrão para as instâncias de publicação. Para obter mais detalhes, consulte [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). | Configuração descrita na [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). |
| Ativos | Se um usuário não tiver permissões suficientes (leitura e gravação) em `/content/dam/collections`, ele não poderá criar uma Coleção. | Respeita a configuração do controle de acesso de usuário e garante as permissões apropriadas. |
| Adobe Search&amp;Promote | A integração com o Adobe Search &amp; Promote está obsoleta. A Adobe não planeja fazer melhorias à integração do Search &amp; Promote. Observe que a integração do Search &amp; Promote permanece compatível ainda que obsoleta. |  |
| Gerente de marcas DTM | A integração com o DTM (Dynamic Tag Manager) está obsoleta. | Alterne para usar o Adobe Experience Platform Launch como um gerenciador de marcas. |
| Adobe Target | Com a adição da capacidade do·AEM se conectar ao serviço do Adobe Target usando a API do Adobe Target Standard (Rest API) baseada en Adobe I/O no AEM 6.5, a API (XML) do Target Classic será descontinuada. | Reconfigure a integração para [usar a nova API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | O uso da integração baseada em `mbox.js` com a Adobe Target no AEM está obsoleto. | Mude para usar `at.js` 1.x. |
| Commerce | [CIF ](https://github.com/adobe/commerce-cif-api) REST foi fornecido em 2018 como um conjunto de microserviços para permitir a integração entre AEM e motores de comércio. Após a Adobe ter adquirido a Magento em meados de 2018, a Adobe decidiu mudar sua abordagem por duas razões. A Magento tem seu próprio conjunto de APIs de comércio (REST e GraphQL) e não é uma boa prática manter dois conjuntos de APIs. As tendências de mercado indicaram que os clientes estavam se movendo para o GraphQL, porque é uma forma mais eficiente de consultar dados. Em 2019, a Adobe lançou o novo Commerce Integration Framework usando o GraphQL APIs como a fonte da verdade. A Adobe não pretende efetuar qualquer investimento adicional em CIF REST. Os clientes são altamente aconselhados a usar a solução de substituição. | Para integrações AEM-Magento, alterne para [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) e [AEM CIF Componentes Principais](https://github.com/adobe/aem-core-cif-components). Consulte Integração AEM e Magento [usando a Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). O suporte para integrações de terceiros (que não sejam Magento) com a nova abordagem está em nosso roteiro. |
| Componentes (AEM Sites) | A Adobe não planeja fazer aprimoramentos adicionais à maioria dos componentes de base armazenados em `/libs/foundation/components`. Procure as propriedades `cq:deprecated` e `cq:deprecatedReason` na pasta do componente. AEM 6.5 inclui os componentes básicos, e os clientes que atualizam de versões anteriores podem continuar a usá-los como estão. Além disso, os Componentes básicos são completamente suportados mesmo se estiverem obsoletos. | A Adobe recomenda usar os Componentes principais para projetos futuros. Os sites existentes podem permanecer como estão ou usar o [AEM Modernizar o Suite de Ferramentas](https://github.com/adobe/aem-modernize-tools) para refatorar o site para usar os Componentes Principais. |
| Componentes (AEM Sites) | Os componentes do Importador de design `/libs/wcm/designimporter/components` foram marcados como obsoletos, começando em 6.5. A Adobe não pretende introduzir novas melhorias na aplicação do importador de desenhos ou modelos. | A Adobe planeja fornecer uma implementação alternativa do caso de uso em versões futuras. |
| Foundation | Estrutura de descarregamento do Granite. O Adobe não planeja fazer mais aprimoramentos na estrutura de descarga que foi introduzida no CQ 5.6.1 para externalizar o processamento de ativos. | A Adobe está trabalhando em uma estrutura de descarregamento nativa de nuvem de última geração. |
| Desenvolvedores | `Hobbes.js`. O Adobe não pretende efetuar mais melhorias na estrutura de teste da interface do usuário `hobbes.js`. | A Adobe recomenda que os clientes usem a automação Selenium. |
| Desenvolvedores | biblioteca do cliente da interface do usuário do jQuery. A Adobe não planeja manter e atualizar a biblioteca do cliente da interface do usuário do jQuery que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes que ainda precisam da interface do usuário do jQuery para obter o código a fim de adicioná-lo à base de códigos do projeto. |
| Desenvolvedores | Biblioteca do cliente jQuery Animation (`granite.jquery.animation`). A Adobe não planeja manter e atualizar a biblioteca do cliente de animação do jQuery que é enviada como parte da distribuição (Quickstart) | A Adobe recomenda que os clientes que ainda precisam de jQuery Animations para seus códigos adicionem-na à base de códigos do projeto. |
| Desenvolvedores | Biblioteca do cliente do Handlebars. A Adobe não planeja manter e atualizar a biblioteca do cliente do Handlebars que é enviada como parte da distribuição (Quickstart) | A Adobe recomenda que os clientes que ainda precisam de handlebars para seus códigos adicionem-nos à base de códigos do projeto. |
| Desenvolvedores | Biblioteca do cliente do Lawnchair. A Adobe não planeja manter e atualizar a biblioteca do cliente do Lawnchair que é enviada como parte da distribuição (Quickstart) | A Adobe recomenda que os clientes que ainda precisam da LawnPresident para seus códigos adicionem o código à base de códigos do projeto. |
| Desenvolvedores | `Granite.Sling.js` biblioteca cliente. A Adobe não planeja aprimorar a biblioteca do cliente do Granite.Sling.js que é enviada como parte da distribuição (Quickstart) | A Adobe recomenda que os clientes que confiam na capacidade da biblioteca reformem seu código para não mais usá-lo. |
| Desenvolvedores | Usar a YUI para compactar/diminuir as bibliotecas do cliente do Javascript. A Adobe não planeja atualizar a biblioteca YUI. Até AEM 6.4, a IU era o padrão para minimizar o JavaScript com a opção de alternar para o Google Closure Compiler (GCC). Ao iniciar o AEM 6.5, o GCC é o padrão. | A Adobe recomenda que os clientes que atualizam para o AEM 6.5 mudem para o GCC para sua implementação |
| Desenvolvedores | Editor de caixa de diálogo da interface do usuário clássica no CRXDE lite. A Adobe não planeja aprimorar o editor de caixa de diálogo da interface do usuário clássica que é enviado como parte da distribuição (Quickstart) | Não há substituição disponível. |
| Forms | A integração do AEM Forms com o AEM Mobile está obsoleta. | Nenhuma substituição está disponível. |  | Desenvolvedores | Editor de caixa de diálogo da interface do usuário clássica no CRXDE lite. A Adobe não planeja aprimorar o editor de caixa de diálogo da interface do usuário clássica que é enviado como parte da distribuição (Quickstart) | Não há substituição disponível. |
| Desenvolvedores | Biblioteca de cliente Lodash/underscore. O Adobe não pretende manter e atualizar ainda mais a biblioteca do cliente Lodash/underscore que é enviada como parte da distribuição (Início rápido) | A Adobe recomenda que os clientes que ainda precisam do Lodash/underscore para seus códigos adicionem-no à base de códigos do projeto. |

## Recursos removidos {#removed-features}

Esta seção lista recursos e recursos que foram removidos da AEM 6.5. As versões anteriores tinham esses recursos marcados como obsoletos.

| Área | Recurso | Substituição |
|--- |--- |--- |
| Analytics Activity Map | A versão do Activity Map está inclusa no AEM. | Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM. Use o plug-in [ActivityMap fornecido pela Adobe Analytics](https://docs.adobe.com/content/help/br/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integrações | A integração do ExactTarget foi removida da distribuição padrão (Início rápido) e não está mais disponível. | Nenhuma substituição. |
| Integrações | A integração da API do Salesforce Force foi removida da distribuição padrão (Quickstart) e agora é um pacote extra para instalação de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | O recurso ainda está disponível. |
| Forms | O suporte para o serviço Adobe Central Migration Bridge foi removido, uma vez que o produto Adobe Central não é mais compatível. | Nenhuma substituição. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nenhuma substituição. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nenhuma substituição |
| Forms | A atualização de hop único do LiveCycle ES4 SP1 para o AEM 6.5 Forms no JEE não está disponível | Consulte [caminhos de atualização disponíveis](../forms/using/upgrade.md) na documentação de atualização do AEM Forms. |
| Forms | Remoção do suporte a cluster baseado em UPD da AEM Forms no JEE | Você pode usar somente clustering baseado em TCP no AEM Forms em JEE. Se você atualizar um servidor de multicast UDP de uma versão anterior para o AEM 5.5 Forms no JEE, execute configurações manuais para alternar para o cluster de gemfire baseado em TCP. Para obter instruções detalhadas, consulte [Atualizar para formulários AEM 6.5 no JEE](../forms/using/upgrade-forms-jee.md) |
| Desenvolvedores | Firebug Lite foi removido da distribuição padrão (Quickstart) | Use os consoles de desenvolvedor integrados do navegador |
| Desenvolvedores | Remova o suporte `customJavaScriptPath` no Gerenciador de biblioteca do cliente HTML. | Nenhuma substituição |
| [!DNL Assets] | O recurso de descarregamento de ativos é removido em [!DNL Adobe Experience Manager] 6.5. | Não há substituição disponível. |
| Cache | `system/console/slingjsp` for removido não estiver mais disponível no AEM 6.5. | Classes e cache leve são armazenados no pacote Apache Sling Commons FileSystem ClassLoader. Você pode verificar o número do pacote no Console da Web AEM e remover a pasta de cache diretamente do sistema de arquivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Pré-lançamento para a próxima versão {#pre-announcement-for-next-release}

Esta seção é usada para anunciar previamente as alterações futuras nas versões futuras. As mudanças anunciadas ainda não são eficazes, mas afetarão os clientes. Por exemplo, os recursos ainda não estão obsoletos, mas afetam os usuários após a desaprovação. Essas atualizações são fornecidas para fins de planejamento.

| Área | Recurso | Anúncio |
|--- |--- |--- |
| Fundação | Estrutura da interface do usuário | A Adobe está planejando descontinuar os componentes do Coral UI 2 em 2019. O Coral UI 3 foi introduzido no AEM 6.2, e o AEM 6.5 é baseado completamente no Coral 3. A Adobe recomenda que clientes e parceiros tenha interfaces do usuário integradas com o Coral 2 para refatorá-las para o Coral 3. A Adobe está fornecendo uma ferramenta para converter caixas de diálogo do Coral 2 para o Coral 3 - [Leia mais](/help/sites-developing/dialog-conversion.md). |
