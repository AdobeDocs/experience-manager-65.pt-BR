---
title: Perguntas frequentes sobre AEM
description: Use essas Perguntas frequentes para entender, configurar e solucionar problemas ou fluxos de trabalho comuns no AEM.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# Perguntas frequentes sobre AEM {#aem-faqs}

Saber as respostas para alguns problemas de solução de problemas e configuração do AEM.

## Sites {#sites}

### Como configurar a distribuição sem binários? {#how-do-i-configure-binary-less-distribution}

A distribuição sem binários tem suporte para implantações em um armazenamento de dados compartilhado e envolve agentes que usam o construtor de pacotes do exportador do pacote de Distribuição com base no Cofre (PID de fábrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`).

Com o modo sem binários ativado, os pacotes de conteúdo distribuídos contêm referências a binários, em vez dos binários reais.

#### Como habilitar a distribuição sem binários? {#how-do-i-enable-binary-less-distribution}

Para habilitar a distribuição sem binários, implante com um armazenamento de blob compartilhado.
Verifique a propriedade `useBinaryReferences` na configuração OSGI com o PID de fábrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* que seu agente está usando.

#### Como ativar permissões ao criar uma Cópia de idioma para autores de conteúdo no AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Para criar o recurso de cópia de idioma, os autores de conteúdo precisam de permissões no local `/content/projects`.

Se também for necessário que os autores gerenciem projetos, a solução alternativa é adicionar o autor ao grupo `projects-administrators`.

#### Como alterar o formato ao criar uma Cópia de idioma para um projeto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Crie uma raiz de idioma e uma cópia de idioma dentro da raiz antes de criar um projeto de tradução.

Por exemplo,
Crie uma raiz de idioma em `/content/geometrixx` com o nome como `fr_LU` (e o título como francês (Luxemburgo)). Posteriormente, crie uma cópia de idioma da página no painel de referências e navegue até a opção `Create structure only` em `Create & Translate`. Por fim, crie um projeto de tradução e adicione a cópia de idioma ao trabalho de tradução.

Para obter detalhes, consulte os recursos adicionais abaixo:

* [Preparação do conteúdo para tradução](/help/sites-administering/tc-prep.md)
* [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md)

#### Como auditar recursos do AEM, como tentativas de logon e ACL ou alterações de permissão? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

O AEM introduziu a capacidade de registrar alterações administrativas para melhorar a solução de problemas e a auditoria. Por padrão, as informações são registradas no arquivo `error.log`. Para facilitar o monitoramento, é recomendável que eles sejam redirecionados para um arquivo de log separado.
Para redirecionar a saída para um arquivo de log separado, consulte [Como auditar operações de gerenciamento de usuários no AEM](/help/sites-administering/audit-user-management-operations.md).

#### Como habilitar o SSL por padrão? {#how-to-enable-ssl-by-default}

O Adobe Experience Manager (AEM) 6.4 é fornecido com o assistente para SSL e oferece uma interface do usuário para configurar o suporte a Jetty e Granite Jetty SSL.

Para habilitar o SSL por padrão, consulte [SSL por padrão](/help/sites-administering/ssl-by-default.md).

#### Qual é a arquitetura recomendada ao usar os Serviços de conteúdo do AEM de um aplicativo móvel, idealmente o React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Os Content Services são baseados nos Modelos Sling e os desenvolvedores do AEM devem fornecer um pojo Modelo Sling para cada componente exportado.

Para entender como consumir serviços de conteúdo AEM por meio de um aplicativo React, consulte o [Tutorial de Introdução ao AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html).

Além disso, se os desenvolvedores quiserem exportar uma árvore de componentes, eles também poderão implementar as interfaces `ComponentExporter` e `ContainerExporter` e usar o `ModelFactory` para iterar sobre os componentes filhos e retornar sua representação de modelo. Consulte os recursos abaixo:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Como desativar o pop-up de pesquisa AEM 6.4? {#how-to-disable-aem-survey-pop-up}

Você pode aderir à coleção de estatísticas de uso usando a interface para toque ou o Console da Web. Para obter instruções detalhadas, consulte [Aceitar a coleção de estatísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Há um bom recurso que destaca os principais recursos para atualizar para o AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Consulte [Entendendo os motivos para atualização do AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html), que descreve o detalhamento de alto nível dos principais recursos para clientes que consideram atualizar para a versão mais recente do Adobe Experience Manager.

## Ativos {#assets}

### Por que o fluxo de trabalho do Assets se repete ao carregar arquivos MP4 (por exemplo, usando o método arrastar e soltar )? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Se o usuário, que faz upload dos arquivos de filme, não tiver permissões de exclusão no nó do ativo, os nós do bloco de exclusão falharão e o upload será reiniciado.

#### Quais são as configurações padrão para configurações prontas para uso ao criar uma Cópia de idioma? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Ao criar uma cópia de idioma por meio da interface para toque (**Referências** > **Atualizar cópia de idioma**), uma nova pasta do DAM é criada no novo idioma e os ativos são referenciados a partir daí.

Essa é a configuração padrão para configurações iniciais. Você pode definir **Traduzir Página Assets** = **Não traduzir** em Configurações de tradução.
Para AEM 6.4, **Ferramentas** > **Cloud Service** > **Serviços de tradução em nuvem**.

#### Como desativar um componente AEM que causa crescimento exponencial do AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Você pode desativar o Desativador de componentes OSGi. Para usar este serviço, consulte [Desabilitador de Componente OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Como solução alternativa, você também pode desabilitar manualmente o componente por meio da interface do usuário ou por meio de um comando `curl` (exemplo abaixo), após cada reinicialização do AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Como personalizar o admin consoles? {#how-to-customize-admin-consoles}

O AEM fornece vários mecanismos para permitir que você personalize os consoles e a funcionalidade de criação de página da sua instância de criação. Para saber como criar um console personalizado e personalizar um modo de exibição padrão para um console, consulte [Personalizando os Consoles](/help/sites-developing/customizing-consoles-touch.md).

#### Qual é a diferença entre os componentes baseados em CoralUI 2 e CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Um novo conjunto de componentes do Sling do Granite UI Foundation é criado para Coral3 e está localizado em [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Há um conjunto para componentes baseados em CoralUI 2 e um conjunto para componentes baseados em CoralUI 3. O novo conjunto não será apenas uma cópia e colagem do conjunto antigo, mas será limpo (por exemplo, dinamização, remoção de recursos obsoletos). Portanto, recomenda-se que uma página use apenas o conjunto baseado em CoralUI 3 ou CoralUI 2.

Para saber mais detalhes, consulte o [Guia de migração para o CoralUI com base em 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Como personalizar o componente de pesquisa no AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Para saber mais sobre o aumento/classificação de pesquisa e outras informações de implementação, consulte [Guia de implementação de pesquisa simples](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

A implementação de pesquisa simples são os materiais do laboratório AEM Search Demystified de 2017.

#### É possível criar um plug-in para WordPress que permite que um cliente acesse o Seletor de ativos Adobe para selecionar imagens? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sim, um cliente usando WordPress pode usar o Seletor de ativos Adobe para selecionar imagens de seu servidor AEM Assets para adicionar a publicações em seu site WordPress.

Consulte [Seletor de ativos](../assets/search-assets.md#assetpicker) para obter mais informações.
