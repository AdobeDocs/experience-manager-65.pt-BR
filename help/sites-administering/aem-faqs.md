---
title: Perguntas frequentes sobre AEM
seo-title: AEM 6.4 frequently asked questions
description: Use essas perguntas frequentes para entender, configurar e solucionar problemas comuns de fluxos de trabalho ou problemas no AEM.
seo-description: Use these FAQs to understand, configure, and troubleshoot common workflows or issues in AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---

# Perguntas frequentes sobre AEM {#aem-faqs}

Saiba as respostas para alguns problemas de solução de problemas e configuração de AEM.

## Sites {#sites}

### Como configurar a distribuição sem código binário? {#how-do-i-configure-binary-less-distribution}

A distribuição sem binários é compatível com implantações em um armazenamento de dados compartilhado e envolve agentes que aproveitam o exportador de pacotes de distribuição baseado em Vault (PID de fábrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) construtor de pacotes.

Com o modo sem binário ativado, os pacotes de conteúdo distribuídos contêm referências a binários em vez dos binários reais.

#### Como ativar a distribuição sem código binário? {#how-do-i-enable-binary-less-distribution}

Para ativar a distribuição sem binário, implante com um repositório de blobs compartilhado.
Verifique a `useBinaryReferences` na configuração OSGI com o PID de fábrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* que seu agente está usando.

#### Como posso personalizar as mensagens de erro ao navegar pela hierarquia de página AEM console de sites? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Verifique o painel Rede (do navegador Chrome), onde uma configuração pessoal (JS não foi minimizado).

Visualize o `Initiator` para determinar qual foi o iniciador de uma solicitação. Ele fornece os arquivos e os números de linha de onde as chamadas de AJAX são feitas. Posteriormente, é possível rastrear a função de tratamento de erros e alterar a mensagem de erro de acordo com seu requisito.

#### Como ativar permissões ao criar uma Cópia de idioma para autores de conteúdo no AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Para criar o recurso de cópia de idioma, os autores de conteúdo precisam de permissões em `/content/projects` local.

Se for necessário que os autores gerenciem projetos também, a solução alternativa é adicionar o autor ao `project-administrators` grupo.

#### Como alterar o formato ao criar a Cópia de idioma para um projeto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Crie uma raiz de idioma e uma cópia de idioma dentro da raiz, antes de criar um projeto de tradução.

Por exemplo, crie uma raiz de idioma em `/content/geometrixx` com o nome como `fr_LU` (e o título como francês (Luxemburgo)). Posteriormente, crie uma cópia de idioma da página no painel de referências e navegue até `Create structure only` em `Create & Translate`. Por fim, crie um projeto de tradução e adicione a cópia de idioma ao trabalho de tradução.

Para obter detalhes, consulte os recursos adicionais abaixo:

* [Preparação do conteúdo para tradução](/help/sites-administering/tc-prep.md)
* [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md)

#### Como auditar AEM recursos como, tentativas de logon e alterações de ACL ou permissão? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM introduziu a capacidade de registrar alterações administrativas para obter uma melhor solução de problemas e auditoria. Por padrão, as informações são registradas no `error.log` arquivo. Para facilitar o monitoramento, é recomendável que ele seja redirecionado para um arquivo de log separado.
Para redirecionar a saída para um arquivo de log separado, consulte [Como auditar operações de gerenciamento de usuários no AEM](/help/sites-administering/audit-user-management-operations.md).

#### Como habilitar o SSL por padrão? {#how-to-enable-ssl-by-default}

O Adobe Experience Manager (AEM) 6.4 é fornecido com o assistente SSL e oferece uma interface de usuário para configurar o suporte a Jetty e Granite Jetty SSL.

Para ativar o SSL por padrão, consulte [SSL por padrão](/help/sites-administering/ssl-by-default.md).

#### Qual é a arquitetura recomendada ao usar os Serviços de conteúdo da AEM de um aplicativo móvel, idealmente React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Os Serviços de conteúdo são baseados nos Modelos do Sling e os desenvolvedores de AEM devem fornecer um trabalho de Modelo do Sling para cada componente que é exportado.

Para entender como consumir AEM serviços de conteúdo de um aplicativo React, consulte [Introdução aos serviços de conteúdo AEM](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) tutorial.

Além disso, se os desenvolvedores quiserem exportar uma árvore de componentes, eles também poderão implementar o `ComponentExporter` e `ContainerExporter` além de usar `ModelFactory` para iterar sobre os componentes filho e retornar sua representação de modelo. Consulte os recursos abaixo:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling : Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Como desativar o pop-up de pesquisa do AEM 6.4? {#how-to-disable-aem-survey-pop-up}

Você pode aderir à coleção de estatísticas de uso usando a interface do usuário de toque ou o console da Web. Para obter instruções detalhadas, consulte [Aceitação na coleta de estatísticas de uso agregado](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Existe um bom recurso que destaca os principais recursos para atualizar para o AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Consulte [Entendendo os motivos para atualizar o AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) que descreve o detalhamento de alto nível dos principais recursos para clientes que consideram atualizar para a versão mais recente do Adobe Experience Manager.

## Assets {#assets}

### Por que o fluxo de trabalho de Ativos se repete ao fazer upload de arquivos MP4 (por exemplo, usando o método arrastar e soltar)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Se o usuário fizer upload dos arquivos de filme não tiver permissões de exclusão no nó do ativo, os nós de exclusão de segmento falharão e o upload será reiniciado.

#### Quais são as configurações padrão para configurações OTB ao criar a Cópia de idioma? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Ao criar uma cópia de idioma por meio da interface do usuário de toque (**Referências** -> **Atualizar Cópia de Idioma**), uma nova pasta DAM é criada no novo idioma e os ativos são referenciados a partir daí.

Essa é a configuração padrão para configurações OTB. Você pode definir **Traduzir ativos da página** = **Não traduzir** em Configurações de tradução.
Para AEM 6.4, **Ferramentas** > **Cloud Services** > **Serviços da nuvem de tradução**.

#### Como desabilitar um componente de AEM que causa crescimento exponencial para o AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Você pode desativar o Desativador do Componente OSGi. Para usar esse serviço, consulte [Desabilitador de Componente OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Como solução alternativa, você também pode desativar manualmente o componente por meio da interface do usuário ou por meio de um `curl` (exemplo abaixo), após cada reinicialização AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Como personalizar consoles de administração? {#how-to-customize-admin-consoles}

O AEM fornece vários mecanismos para permitir a personalização dos consoles e a funcionalidade de criação de página da sua instância de criação. Para saber como criar um console personalizado e personalizar uma visualização padrão para um console, consulte [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md).

#### Qual é a diferença entre os componentes baseados em CoralUI 2 e CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Um novo conjunto de componentes Sling da Fundação de interface do usuário do Granite é criado para o Coral3 e está localizado em [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Há um conjunto para componentes baseados em CoralUI 2 e um conjunto para componentes baseados em CoralUI 3. O novo conjunto não será apenas uma cópia e uma colagem do conjunto antigo, mas será limpo (por exemplo, simplificação, remoção de recurso obsoleto). Portanto, é recomendável que uma página use somente o conjunto com base em CoralUI 3 ou CoralUI 2.

Para saber mais detalhes, consulte [Guia de migração para o CoralUI baseado em 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Como personalizar o componente de pesquisa no AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Para saber mais sobre informações de reforço/classificação de pesquisa e implementação adicional, consulte [Guia de implementação de pesquisa simples](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

A implementação Simple search são os materiais do laboratório 2017 Summit AEM Search Demystified.

#### É possível criar um plug-in para o WordPress que permite que um cliente acesse o Seletor de ativo do Adobe para selecionar imagens? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sim, um cliente que usa o WordPress pode usar o Seletor de ativo do Adobe para selecionar imagens de seu servidor do AEM Assets para adicionar a postagens em seu site do WordPress.

Consulte [Seletor de ativos](../assets/search-assets.md#assetpicker) para obter mais informações.
