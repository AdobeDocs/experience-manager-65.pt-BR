---
title: Recursos obsoletos e removidos na versão Adobe Experience Manager 6.5.
description: Notas de versão específicas para recursos obsoletos e removidos do Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 191c4b02274ca7e3e9d4622b72cd585870581f47
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 10%

---

# Recursos obsoletos e removidos {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

A Adobe avalia as funcionalidades do produto constantemente, para reinventar ou substituir recursos mais antigos por alternativas mais modernas, de forma a melhorar o valor do cliente em geral, sempre sob considerações cuidadosas de compatibilidade com versões anteriores.

Para comunicar a remoção ou substituição iminente dos recursos do Adobe Experience Manager (AEM), as seguintes regras se aplicam:

1. O anúncio sobre a descontinuidade é oferecido primeiro. Embora obsoletos, os recursos ainda estão disponíveis, mas não estão aprimorados.
1. A remoção de recursos obsoletos ocorre na versão principal a seguir, o mais tardar. A data de destino real para remoção será anunciada posteriormente.

Esse processo oferece ao usuário ao menos um ciclo de versão para adaptar sua implementação a uma nova versão ou sucessor de uma funcionalidade descontinuada, antes da remoção.

## Recursos obsoletos {#deprecated-features}

Esta seção lista os recursos e funcionalidades marcados como obsoletos com o AEM 6.5. Geralmente, os recursos planejados para remoção em uma versão futura são definidos como obsoletos primeiro, com uma alternativa fornecida.

Os clientes são instruídos a analisar se usam o recurso/funcionalidade em sua implementação atual, bem como a planejar a alteração de sua implementação para usar a alternativa fornecida.

| Área | Destaque | Substituição | Versão (SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | O serviço **Configuração de Sondagem Gerenciada do AEM do Adobe**: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | O serviço **Importador de Sling de Relatórios do Analytics Adobe AEM**. Consulte Conectando ao Adobe Analytics e Criando Estruturas - [Configurando o Intervalo de Importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | AtiveMQ no Adobe Experience Manager (AEM). O AtiveMQ foi usado para comunicação entre duas instâncias do AEM Publish. | A Adobe recomenda que os clientes agora usem um balanceador de carga. | 6.5.18.0 |
| Propriedades dos Fragmentos de experiência para **Status da rede social**. |   | 6.5.11.0 |
| [!DNL Sites] | Modelos de fragmentos de conteúdo, para criar fragmentos de conteúdo simples. | [Fragmentos de conteúdo estruturado com base em modelo](/help/assets/content-fragments/content-fragments-models.md) agora. | 6.5.11.0 |
| integração de Creative Cloud | O compartilhamento de pasta AEM para Creative Cloud foi introduzido no AEM 6.2. Ele fornece uma maneira de conceder aos usuários criativos acesso a ativos do AEM, para que eles possam abri-los em aplicativos do [!DNL Creative Cloud] e carregar novos arquivos ou salvar alterações no AEM. Um novo recurso lançado no aplicativo Creative Cloud, o Adobe Asset Link, fornece uma melhor experiência de usuário e acesso mais eficiente a ativos do AEM diretamente do Photoshop, do InDesign e do Illustrator. O Adobe não pretende fazer mais melhorias na integração entre AEM e Compartilhamento de pastas Creative Cloud. Embora o recurso esteja incluído no AEM, os clientes são aconselhados a usar soluções de substituição. | Os clientes são aconselhados a alternar para novos recursos de integração de Creative Cloud, incluindo o aplicativo de desktop Adobe Asset Link ou AEM. |  |
| Ativos | `AssetDownloadServlet` está desabilitado por padrão para as instâncias de publicação. Para obter mais detalhes, consulte [lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). | Configuração descrita em [lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md). |  |
| Integrações | A tela **[!UICONTROL Experience Manager Cloud Service Opt-In]** está obsoleta, pois a integração [!DNL Experience Manager] e [!DNL Adobe Target] foi atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Ele oferece suporte à crescente função do Adobe Launch de instrumentar [!DNL Experience Manager] páginas para análise e personalização. O assistente de aceitação é funcionalmente irrelevante. | Configure as conexões do sistema, a autenticação do Adobe IMS e as integrações do [!DNL Adobe I/O Runtime] por meio dos respectivos serviços de nuvem [!DNL Experience Manager]. | 6.5.7.0 |
| Conectores | O Conector JCR do Adobe para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |  |
| Gerenciador dinâmico de tags (DTM) | A integração com o DTM está obsoleta. | Alterne para usar o Adobe Experience Platform Launch como um gerenciador de tags. |   |
| Adobe Target | Com a adição da capacidade de o AEM se conectar ao serviço do Adobe Target usando a API do Adobe Target Standard (API Rest) com base em [!DNL Adobe I/O] no AEM 6.5, o modo da API do Target Classic (XML) foi descontinuado. | Reconfigure a integração para [usar a nova API](/help/sites-administering/target.md). |  |
| Adobe Target | O uso da integração baseada em `mbox.js` com o Adobe Target no AEM está obsoleto. | Alternar para usar `at.js` 1.x. |  |
| Commerce | O [CIF REST](https://github.com/adobe/commerce-cif-api) foi fornecido em 2018 como um conjunto de microsserviços para habilitar integrações entre o AEM e mecanismos de comércio. Depois que a Adobe adquiriu a Adobe Commerce (anteriormente Magento) em meados de 2018, a Adobe decidiu mudar sua abordagem por dois motivos. O Commerce tem seu próprio conjunto de APIs do Commerce (REST e GraphQL) e não é uma boa prática manter dois conjuntos de APIs. As tendências de mercado indicaram que os clientes estavam migrando para o GraphQL, porque essa é uma maneira mais eficiente de consultar dados. Em 2019, o Adobe lançou o novo Commerce integration framework usando as APIs GraphQL da Commerce como fonte da verdade. A Adobe não planeja fazer mais nenhum investimento no CIF REST. Os clientes são aconselhados a usar a solução de substituição. | Para integrações AEM-Commerce, mude para o [Arquétipo de AEM CIF AEM CIF](https://github.com/adobe/aem-cif-project-archetype) e o [Componentes principais](https://github.com/adobe/aem-core-cif-components). Consulte Integração com AEM e Adobe Commerce [usando Commerce integration framework](/help/commerce/cif/integrating/magento.md). O suporte para integrações de terceiros (diferentes da Commerce) com a nova abordagem está no roteiro do Adobe. |  |
| Componentes (AEM Sites) | O Adobe não pretende fazer melhorias adicionais na maioria dos Componentes de base armazenados no `/libs/foundation/components`. Procure as propriedades `cq:deprecated` e `cq:deprecatedReason` na pasta de componentes. O AEM 6.5 tem os Componentes de base incluídos, e os clientes que estão atualizando de versões anteriores podem continuar usando-os como estão. Além disso, os Componentes de base são compatíveis, embora tenham se tornado obsoletos. | A Adobe recomenda usar os Componentes principais para projetos futuros. Os sites existentes podem permanecer como estão ou usar o [Conjunto de ferramentas de Modernização de AEM](https://github.com/adobe/aem-modernize-tools) para refatorar o site para usar os Componentes principais. |  |
| Componentes (AEM Sites) | Os Componentes do Importador de Design `/libs/wcm/designimporter/components` foram marcados como obsoletos a partir da versão 6.5. A Adobe não planeja fazer melhorias adicionais nessa implementação do importador de design. | O Adobe planeja fornecer uma implementação alternativa do caso de uso em versões futuras. |  |
| Foundation | Estrutura de descarregamento do Granite. A Adobe não planeja fazer mais melhorias na estrutura de descarregamento introduzida no CQ 5.6.1 para externalizar o processamento de ativos. | O Adobe está trabalhando em uma estrutura de descarregamento nativa em nuvem de próxima geração. |  |
| Desenvolvedores | `Hobbes.js`. O Adobe não planeja fazer mais melhorias na estrutura de testes da interface do usuário `hobbes.js`. | A Adobe recomenda que os clientes usem a automação Selenium. |  |
| Desenvolvedores | Biblioteca do cliente da interface do usuário do jQuery. O Adobe não planeja manter e atualizar a biblioteca do cliente da interface do usuário jQuery fornecida como parte da distribuição (Início rápido). | A Adobe recomenda que os clientes que ainda exigem a interface do usuário do jQuery para seus códigos a adicionem em sua base de código do projeto. |  |
| Desenvolvedores | Biblioteca cliente jQuery Animation (`granite.jquery.animation`). O Adobe não planeja manter e atualizar a biblioteca do cliente jQuery Animation fornecida como parte da distribuição (Início rápido). | A Adobe recomenda que os clientes que ainda exigem Animações jQuery para seu código o adicionem em sua base de código do projeto. |  |
| Desenvolvedores | Biblioteca cliente Handlebars. O Adobe não planeja fazer manutenção e atualização adicionais na biblioteca do cliente Handlebar fornecida como parte da distribuição (Quickstart). | A Adobe recomenda que os clientes que ainda exigem `Handlebars` para seu código o adicionem em sua base de código do projeto. |  |
| Desenvolvedores | Biblioteca cliente Lawnchair. O Adobe não planeja fazer manutenção e atualização adicionais da biblioteca do cliente Lawnchair enviada como parte da distribuição (Quickstart). | A Adobe recomenda que os clientes que ainda exigem o código do Lawnchair o adicionem à base de código do projeto. |  |
| Desenvolvedores | Biblioteca cliente `Granite.Sling.js`. O Adobe não planeja aprimorar ainda mais a biblioteca do cliente Granite.Sling.js fornecida como parte da distribuição (Início rápido). | A Adobe recomenda que os clientes que dependem da capacidade da biblioteca refatorem seu código para não usá-lo mais. |  |
| Desenvolvedores | Utilização da interface do usuário do para compactar/minificar bibliotecas de clientes do JavaScript. O Adobe não planeja atualizar ainda mais a biblioteca YUI. Até o AEM 6.4, a YUI era padrão para minificar o JavaScript com a opção de alternar para o Google Closure Compiler (GCC). A partir do AEM 6.5, o GCC é o padrão. | A Adobe recomenda que os clientes que atualizam para AEM 6.5 mudem para GCC para implementação |  |
| Desenvolvedores | Editor de diálogo da interface clássica no CRXDE Lite. O Adobe não planeja aprimorar ainda mais o Editor de diálogo da interface clássica fornecido como parte da distribuição (Quickstart) | Nenhuma substituição disponível. |  |
| Forms | A integração do AEM Forms com o AEM Mobile está obsoleta. | Não há Substituição disponível. |
| Desenvolvedores | Editor de diálogo da interface clássica no CRXDE Lite. O Adobe não planeja aprimorar ainda mais o Editor de diálogo da interface clássica fornecido como parte da distribuição (Quickstart) | Nenhuma substituição disponível. |  |
| Desenvolvedores | Biblioteca cliente Lodash/underscore. O Adobe não planeja fazer manutenção e atualização adicionais da biblioteca do cliente Lodash/underscore fornecida como parte da distribuição (Início rápido). | A Adobe recomenda que os clientes que ainda exigem Lodash/underline para seu código o adicionem à base de código do projeto. |  |

## Recursos removidos {#removed-features}

Esta seção lista os recursos e funcionalidades removidos do AEM 6.5. As versões anteriores tinham esses recursos marcados como obsoletos.

| Área | Destaque | Substituição | Versão (SP) |
|--- |--- |--- |--- |
| Commerce | AEM O CIF Classic foi removido. | AEM Você deve migrar para o [CIF](/help/commerce/cif/migration.md). Se você ainda precisar do CIF Classic, um pacote de compatibilidade foi criado, [entre em contato com o Suporte ao Cliente do Adobe](https://experienceleague.adobe.com/pt-br?support-solution=General#support). | 6.5.22.0 |
| Integração com [!DNL Experience Cloud] | Você pode sincronizar seus ativos com o [!DNL Experience Cloud] usando uma configuração via [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] era anteriormente chamado [!DNL Adobe Experience Cloud]. | Se tiver alguma dúvida, [contate o Suporte ao Cliente do Adobe](https://experienceleague.adobe.com/pt-br?support-solution=General#support). |  |
| Activity Map do Analytics | A versão do Activity Map que está incluída no AEM. | Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM. Use o [plug-in do ActivityMap fornecido pela Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR). |  |
| Integrações | A integração do ExactTarget foi removida da distribuição padrão (Quickstart) e não está mais disponível. | Sem substituição. |  |
| Integrações | A integração da API Salesforce Force foi removida da distribuição padrão (Quickstart) e agora é um pacote extra a ser instalado da [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). | O recurso ainda está disponível. |
| Forms | O suporte para o serviço Adobe Central Migration Bridge foi removido porque o produto Adobe Central não é mais suportado. | Sem substituição. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Sem substituição. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sem substituição |  |
| Forms | O upgrade de hop único do LiveCycle ES4 SP1 para o AEM 6.5 Forms no JEE não está disponível | Consulte [caminhos de atualização disponíveis](../forms/using/upgrade.md) na documentação de atualização do AEM Forms. |  |
| Forms | Remoção do suporte a cluster baseado em UPD do AEM Forms no JEE | Você pode usar somente clustering baseado em TCP no AEM Forms no JEE. Se você atualizar um servidor multicast UDP de uma versão anterior para AEM 5.5 Forms no JEE, execute configurações manuais para alternar para o cluster gemfire baseado em TCP. Para obter instruções detalhadas, consulte [Atualizar para formulários AEM 6.5 no JEE](../forms/using/upgrade-forms-jee.md) |  |
| Desenvolvedores | O Firebug Lite foi removido da distribuição padrão do (Quickstart) | Usar os consoles de desenvolvedor integrados do navegador |
| Desenvolvedores | Remova o suporte a `customJavaScriptPath` no Gerenciador de biblioteca de cliente HTML. | Sem substituição |  |
| [!DNL Assets] | O recurso de descarregamento de ativos foi removido em [!DNL Adobe Experience Manager] 6.5. | Nenhuma substituição disponível. |  |
| Cache | `system/console/slingjsp` foi removido e não está mais disponível no AEM 6.5. | As classes e o cache Slightly são armazenados no pacote Apache Sling Commons FileSystem ClassLoader. Você pode verificar o número do pacote no Console da Web AEM e remover a pasta de cache diretamente do sistema de arquivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Remoção do suporte ao pacote ativemq e de suas configurações relacionadas. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
