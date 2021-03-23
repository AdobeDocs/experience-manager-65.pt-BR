---
title: Recursos obsoletos e removidos na versão 6.5 do Adobe Experience Manager.
description: Notas de versão específicas de recursos obsoletos e removidos do Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 43%

---


# Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

Para comunicar a remoção ou substituição iminente de recursos AEM, as seguintes regras se aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Embora obsoletos, os recursos ainda estão disponíveis, mas não são aprimorados.
1. A remoção de recursos obsoletos ocorre na seguinte versão principal, o mais tardar. A data definida para a remoção será anunciada.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades que foram marcados como obsoleto no AEM 6.5. Normalmente, os recursos são, em primeiro lugar, marcados como obsoletos, com remoção planejada para uma versão futura, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação no momento, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Área | Recurso | Substituição |
|---|---|---|
| Integração da Creative Cloud | O AEM ao Compartilhamento de pastas do Creative Cloud foi introduzido no AEM 6.2 como uma maneira de conceder aos usuários criativos acesso aos ativos do AEM, para que pudessem abri-los em aplicativos da CC e fazer upload de novos arquivos ou salvar alterações no AEM. Uma nova funcionalidade lançada no aplicativo da Creative Cloud, o Adobe Asset Link, fornece uma experiência de usuário melhor e acesso avançado a ativos do AEM diretamente do Photoshop, InDesign e Illustrator. A Adobe não planeja fazer aprimoramentos adicionais ao AEM para a integração do Compartilhamento de pastas da Creative Cloud. Embora o recurso esteja incluído no AEM, os clientes são recomendados a suar soluções de substituição. | Os clientes são aconselhados a alternar para novos recursos de integração do Creative Cloud, incluindo o Adobe Asset Link ou AEM aplicativo de desktop. Revise as Práticas recomendadas da integração de AEM e Creative Cloud para obter mais detalhes. |
| Ativos | `AssetDownloadServlet`O é desabilitado por padrão para as instâncias de publicação. Para obter mais detalhes, consulte [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). | Configuração descrita na [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). |
| Ativos | Se um usuário não tiver permissões suficientes (leitura e gravação) em `/content/dam/collections`, ele não poderá criar uma Coleção. | Respeita a configuração do controle de acesso de usuário e garante as permissões apropriadas. |
| Adobe Search&amp;Promote | A integração com o Adobe Search &amp; Promote está obsoleta. A Adobe não planeja fazer melhorias à integração do Search &amp; Promote. Observe que a integração do Search &amp; Promote permanece compatível ainda que obsoleta. |  |
| Gerente de marcas DTM | A integração com o DTM (Dynamic Tag Manager) está obsoleta. | Alterne para usar o Adobe Experience Platform Launch como um gerenciador de marcas. |
| Adobe Target | Com a adição da capacidade de AEM se conectar ao serviço do Adobe Target usando a API padrão do Adobe Target baseada em [!DNL Adobe I/O] (Rest API) no AEM 6.5, a maneira API clássica (XML) do Target está obsoleta. | Reconfigure a integração para [usar a nova API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Usar a integração baseada em `mbox.js` com o Adobe Target no AEM está obsoleto. | Alterne para usar `at.js` 1.x. |
| Commerce | [O ](https://github.com/adobe/commerce-cif-api) REST da CIF foi fornecido em 2018 como um conjunto de microsserviços para permitir integrações entre AEM e mecanismos de comércio. Depois que a Adobe adquiriu a Magento em meados de 2018, a Adobe decidiu mudar sua abordagem por dois motivos. O Magento tem seu próprio conjunto de APIs do Commerce (REST e GraphQL) e não é uma boa prática manter dois conjuntos de APIs. As tendências de mercado indicaram que os clientes estavam se aproximando do GraphQL, porque é uma maneira mais eficiente de consultar dados. Em 2019, o Adobe lançou a nova Estrutura de Integração do Commerce usando APIs GraphQL como a fonte da verdade. O Adobe não planeja fazer mais investimentos na CIF REST. É altamente recomendável que os clientes usem a solução de substituição. | Para integrações AEM-Magento, alterne para [AEM Arquétipo da CIF](https://github.com/adobe/aem-cif-project-archetype) e [AEM Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components). Consulte Integração de AEM e Magento [usando a Estrutura de Integração do Commerce](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). O suporte para integrações de terceiros (diferentes do Magento) com a nova abordagem está em nosso roteiro. |
| Componentes (AEM Sites) | A Adobe não planeja fazer aprimoramentos adicionais à maioria dos componentes de base armazenados em `/libs/foundation/components`. Procure a propriedade `cq:deprecated` e `cq:deprecatedReason` na pasta do componente. AEM 6.5 inclui os componentes de base, e os clientes que atualizam de versões anteriores podem continuar usando os componentes como estão. Além disso, os componentes de base são totalmente compatíveis, mesmo que obsoletos. | A Adobe recomenda usar os Componentes principais para projetos futuros. Os sites existentes podem permanecer como estão ou usar o [AEM Modernizar o conjunto de ferramentas](https://github.com/adobe/aem-modernize-tools) para refatorar o site para usar os Componentes principais. |
| Componentes (AEM Sites) | Os Componentes do Importador de Design `/libs/wcm/designimporter/components` foram marcados como obsoletos a partir da versão 6.5. O Adobe não planeja fazer aprimoramentos adicionais a essa implementação do importador de design. | O Adobe planeja fornecer uma implementação alternativa do caso de uso em versões futuras. |
| Foundation | Estrutura de descarregamento do Granite. O Adobe não planeja fazer aprimoramentos adicionais à estrutura de descarregamento que foi introduzida no CQ 5.6.1 para externalizar o processamento de ativos. | A Adobe está trabalhando em uma estrutura de descarregamento nativa de nuvem de última geração. |
| Desenvolvedores | `Hobbes.js`. O Adobe não planeja fazer aprimoramentos adicionais à estrutura de teste da interface do usuário `hobbes.js`. | O Adobe recomenda que os clientes usem a automação do Selenium. |
| Desenvolvedores | biblioteca do cliente da interface do usuário do jQuery. A Adobe não planeja manter e atualizar a biblioteca do cliente da interface do usuário do jQuery que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes ainda solicitem a interface do usuário do jQuery do seu código para adicioná-la à base de código do projeto. |
| Desenvolvedores | Biblioteca do cliente de animação do jQuery (`granite.jquery.animation`). A Adobe não planeja manter e atualizar a biblioteca do cliente de animação do jQuery que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes ainda solicitem as animações do jQuery do seu código para adicioná-las à base de código do projeto. |
| Desenvolvedores | Biblioteca do cliente do Handlebars. A Adobe não planeja manter e atualizar a biblioteca do cliente do Handlebars que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes ainda solicitem Handlebars do seu código para adicioná-lo à base de código do projeto. |
| Desenvolvedores | Biblioteca do cliente do Lawnchair. A Adobe não planeja manter e atualizar a biblioteca do cliente do Lawnchair que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes ainda solicitem o Lawnchair do seu código de forma a adicioná-lo à base de código do projeto. |
| Desenvolvedores | `Granite.Sling.js` biblioteca do cliente. A Adobe não planeja aprimorar a biblioteca do cliente do Granite.Sling.js que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes que dependem do recurso da biblioteca alterem o código para não mais usá-lo. |
| Desenvolvedores | Usar a YUI para compactar/diminuir as bibliotecas do cliente do Javascript. A Adobe não planeja atualizar a biblioteca YUI. Até o AEM 6.4, a YUI era padrão para diminuir o JavaScript com a opção de alternar para o Google Closure Compiler (GCC). Ao iniciar o AEM 6.5, o GCC é o padrão. | O Adobe recomenda que os clientes atualizem para o AEM 6.5 para alternar para o GCC para sua implementação |
| Desenvolvedores | Editor de caixa de diálogo da interface do usuário clássica no CRXDE lite. A Adobe não planeja aprimorar o editor de caixa de diálogo da interface do usuário clássica que é enviado como parte da distribuição (Quickstart) | Nenhuma substituição está disponível. |
| Forms | A integração do AEM Forms com o AEM Mobile está obsoleta. | Nenhuma substituição está disponível. |  | Desenvolvedores | Editor de caixa de diálogo da interface do usuário clássica no CRXDE lite. A Adobe não planeja aprimorar o editor de caixa de diálogo da interface do usuário clássica que é enviado como parte da distribuição (Quickstart) | Nenhuma substituição está disponível. |
| Desenvolvedores | Biblioteca do cliente Lodash/underscore. O Adobe não planeja manter e atualizar a biblioteca do cliente Lodash/underscore que é enviada como parte da distribuição (Quickstart) | O Adobe recomenda que os clientes ainda solicitem o Lodash/underscore para que seu código o adicione à base de código do projeto. |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades removidos do AEM 6.5. As versões anteriores tiveram esses recursos marcados como obsoletos.

| Área | Recurso | Substituição |
|--- |--- |--- |
| Analytics Activity Map | A versão do Activity Map está inclusa no AEM. | Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM. Use o plug-in [ActivityMap fornecido pelo Adobe Analytics](https://docs.adobe.com/content/help/br/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integrações | A integração do ExactTarget foi removida da distribuição padrão (Quickstart) e não está mais disponível. | Nenhuma substituição. |
| Integrações | A integração da API do Salesforce Force foi removida da distribuição padrão (Quickstart) e agora é um pacote extra para instalar a partir de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | O recurso ainda está disponível. |
| Forms | O suporte para o serviço Adobe Central Migration Bridge foi removido, uma vez que o produto Adobe Central não é mais compatível. | Nenhuma substituição. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nenhuma substituição. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nenhuma substituição |
| Forms | A atualização de salto único do LiveCycle ES4 SP1 para AEM 6.5 Forms no JEE não está disponível | Consulte [caminhos de atualização disponíveis](../forms/using/upgrade.md) na documentação de atualização do AEM Forms. |
| Forms | Remoção do suporte de cluster baseado em UPD do AEM Forms no JEE | Você pode usar somente o clustering baseado em TCP no AEM Forms no JEE. Se você atualizar um servidor multicast UDP de uma versão anterior para AEM 5.5 Forms no JEE, execute configurações manuais para alternar para o clustering gemfire baseado em TCP. Para obter instruções detalhadas, consulte [Atualizar para AEM formulários 6.5 no JEE](../forms/using/upgrade-forms-jee.md) |
| Desenvolvedores | Firebug Lite foi removido da distribuição padrão (Quickstart) | Use os consoles de desenvolvedor integrados do navegador |
| Desenvolvedores | Remova o suporte `customJavaScriptPath` no Gerenciador da biblioteca do cliente HTML. | Nenhuma substituição |
| [!DNL Assets] | O recurso de descarregamento de ativos é removido em [!DNL Adobe Experience Manager] 6.5. | Nenhuma substituição está disponível. |
| Cache | `system/console/slingjsp` for removido e não estiver mais disponível no AEM 6.5. | As classes e o cache Slightly são armazenados no pacote Apache Sling Commons FileSystem ClassLoader . Você pode verificar o número do pacote no Console da Web AEM e remover a pasta do cache diretamente do sistema de arquivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Pré-anúncio para a próxima versão {#pre-announcement-for-next-release}

Esta seção é usada para anunciar previamente as alterações futuras nas versões futuras. As alterações anunciadas ainda não estão em vigor, mas afetarão os clientes. Por exemplo, os recursos ainda não foram descontinuados, mas afetam os usuários após a descontinuação. Essas atualizações são fornecidas para fins de planejamento.

| Área | Recurso | Anúncio |
|--- |--- |--- |
| Foundation | Estrutura da interface do usuário | A Adobe está planejando descontinuar os componentes do Coral UI 2 em 2019. O Coral UI 3 foi introduzido no AEM 6.2, e o AEM 6.5 é baseado completamente no Coral 3. A Adobe recomenda que clientes e parceiros tenha interfaces do usuário integradas com o Coral 2 para refatorá-las para o Coral 3. A Adobe está fornecendo uma ferramenta para converter caixas de diálogo do Coral 2 para o Coral 3 - [Leia mais](/help/sites-developing/modernization-tools.md). |
