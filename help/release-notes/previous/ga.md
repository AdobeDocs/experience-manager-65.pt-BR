---
title: Notas de versão gerais para [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] 6.5 notas descrevendo as informações da versão, novidades, como instalar e listas detalhadas de alterações."'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 58%

---

# Notas de versão gerais para [!DNL Adobe Experience Manager] 6,5{#general-release-notes-for-adobe-experience-manager}

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] |
|---|---|
| Versão | 6.5 |
| Tipo | Versão Principal |
| Data de disponibilidade geral | 8 de abril de 2019 |
| Atualizações recomendadas | Consulte [AEM atualizações recentes](https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html). |

### Trívia {#trivia}

O ciclo de lançamento desta versão do [!DNL Adobe Experience Manager] a partir de 4 de abril de 2018, passou por 23 iterações de garantia de qualidade e correção de erros, terminando em 28 de março de 2019. O número total de problemas relatados por clientes incluindo melhorias e novos recursos corrigidos nesta versão é de 1345.

[!DNL Adobe Experience Manager] O 6.5 está disponível por completo desde 8 de abril de 2019.

![Tela de logon do AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novidades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 é uma versão de atualização para o [!DNL Adobe Experience Manager] 6.4 base de código. Ele fornece funcionalidades novas e melhoradas, correções essenciais para o cliente, melhorias de alta prioridade para o cliente e correções gerais de bugs voltadas para a estabilização do produto. Também inclui [!DNL Adobe Experience Manager] 6.4 Versões do Service Pack até o SP4.

A lista abaixo fornece uma visão geral, enquanto as páginas subsequentes listam os detalhes completos.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

A plataforma de [!DNL Adobe Experience Manager] 6.5 build sobre as versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e do repositório de conteúdo Java: Apache Jackrabbit Oak 1.10.2.

O Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo servlet.

#### Suporte ao Java  {#java-support}

* Novo suporte para o Java 11, bem como o Java 8 já compatível.
* Para melhor desempenho, substitua os valores GC padrão por outros valores. Para obter mais informações, consulte o [instalar e atualizar](/help/sites-deploying/custom-standalone-install.md) seção.
* As atualizações de manutenção do Java 11 e Java 8 são distribuídas pelo Adobe para o uso do cliente em projetos relacionados ao AEM, quando não disponibilizadas publicamente no Oracle.

#### Java Development {#java-development}

* Agora há [duas versões do Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), uma versão recomendada com interfaces públicas que não estão marcadas para descontinuação, bem como uma versão que inclui interfaces marcadas para descontinuação.

#### Interface do usuário {#user-interface}

Vários aprimoramentos foram feitos à interface do usuário para torná-la mais produtiva e fácil de usar.

* Nova interface do usuário de gerenciamento de permissões para usuários e grupos.
* As exibições em coluna agora também só carregam entradas visíveis na tela e só carregam mais quando o usuário começa a rolar. A exibição em lista e cartão já faziam isso desde a versão 6.0 (aprimorado na 6.4).
* As exibições em coluna agora incluem o status de fluxo de trabalho de páginas/ativos, quando aplicável.
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) é uma forma rápida de executar uma ação com todas as páginas/ativos na mesma pasta.
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) tenta executar a ação para todas as páginas/ativos, não só nos que foram carregados. Uma caixa de diálogo de aviso será exibida se a ação não for atualizada para lidar com Ações em massa.

>[!CAUTION]
>
>A Adobe não planeja fazer aprimoramentos adicionais à interface do usuário clássica. O AEM 6.5 tem a interface do usuário clássica incluída, e os clientes que atualizam de versões anteriores podem continuar a usando da mesma forma. Observe que a interface do usuário clássica permanece completamente compatível mesmo enquanto obsoluta. [Leia mais](/help/sites-deploying/ui-recommendations.md).

#### Pesquisa e indexação {#indexing-and-search}

* A pesquisa no Oak agora suporta aspectos dinâmicos. Por exemplo, o painel de filtros na pesquisa de ativos mostra a quantidade estimada de resultados.
* O QueryBuilder foi expandido para fornecer resultados com aspectos dinâmicos.

#### Atualização {#upgrade}

* A atualização local direta para o AEM 6.5 é compatível com clientes que executam o AEM 6.2, 6.3 e 6.4. Clientes que usam a versão 5.x ou 6.0/6.1 e querem usar a atualização local devem atualizar para a versão 6.4 primeiro e, em seguida atualizar para a 6.5, ou atualizar por meio de transferência de conteúdos entre as instâncias diretamente para o AEM 6.5.
* O procedimento de atualização permanece amplamente o mesmo no 6.5.
* Ainda oferecemos suporte à compatibilidade com versões anteriores, à avaliação de complexidade da atualização e aos recursos de atualizações sustentáveis inseridos na versão 6.4. Foram feitas atualizações específicas da versão a essas áreas onde foi necessário.
* O empacotamento de detector de padrão foi simplificado, e haverá um pacote que avalia atualizações no 6.5 para as versões de origem disponíveis.
* Para obter detalhes sobre o procedimento de atualização, consulte o [documentação de atualização](/help/sites-deploying/upgrade.md).

#### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor de modelo de fluxo de trabalho introduzido na versão 6.4 foi aprimorado para incluir mais operações como Copiar e publicar, Suporte à variável nas etapas do fluxo de trabalho e melhorias `OR` e `AND` divisões.

#### Repositório {#repository}

* A base do Adobe Experience Manager 6.5 integrada na parte superior das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e o repositório de conteúdo do Java: Apache Jackrabbit Oak 1.10.2.
* Para obter uma visão geral dos problemas corrigidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>A nova versão do Oak Segment Tar presente desde o AEM 6.3 exige uma migração de repositório. Esta etapa é obrigatória se você estiver atualizando de uma versão mais antiga do TarMK ou quiser alternar o novo segmento de Tar de outro tipo de persistência. Para obter mais informações sobre quais são os benefícios do novo Tar de segmento, consulte o [Perguntas frequentes sobre a migração para o Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Adição de bibliotecas do utilitário de promessas e conversor do OSGi.

#### Segurança {#security}

* Adição de expiração de senha para o usuário administrador.

#### Servidor Web {#web-server}

* A distribuição do Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo de servlet (AEM 6.4 enviado com 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Aplicativos de página única gerenciados {#managed-single-page-apps}

O Editor de página adiciona a capacidade de editar conteúdo no contexto e compor/fazer o layout dentro das experiências de renderização do lado do cliente (também chamado [Editor do SPA](/help/sites-developing/spa-architecture.md)). Aplicativos de página única existentes criados com a estrutura de Reação ou Angular do JavaScript podem ser exportados com o AEM SJ SDK para se tornarem editáveis para usuários.

Em primeiro lugar enviado como parte do AEM 6.4 SP2, com o AEM 6.5 o suporte ao SPA adquire as seguintes funcionalidades:

* Usar o editor de modelo para editar e configurar as partes editáveis do AEM do SPA
* Usar o gerenciamento de vários sites para criar país, franquia ou experiências SPA de marca branca

#### Gerenciamento de conteúdo sem periféricos {#headless-content-management}

O AEM tem a capacidade de fornecer conteúdo em vários formatos e de diferentes níveis de empilhamento. Alguns têm estado disponíveis desde 2008 com o [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e o [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Os serviços de conteúdo ([Sling Model Exporter](https://docs.adobe.com/content/help/pt-BR/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) foi introduzido no AEM 6.3 e é o método usado pelo AEM SJ SDK para recuperar aplicativos de página única. A [API HTTP do Assets](/help/assets/mac-api-assets.md) é uma API CRUD, que foi estendida para o AEM 6.5.

Novos recursos da API HTTP:

* Adição do [Suporte de fragmento de conteúdo para a API HTTP do Assets](/help/assets/assets-api-content-fragments.md) para criar, atualizar, ler e excluir fragmentos.
* Expor listas dos fragmentos de conteúdo por meio dos serviços de conteúdo com o [Componente principal da lista de fragmentos de conteúdo](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Biblioteca de conteúdo principal](https://opensource.adobe.com/aem-core-wcm-components/library.html) que mostra a saída JSON padrão dos serviços de conteúdo de cada componente

#### Complemento do Screens {#screens-add-on}

Crie, entregue e otimize experiências com eficiência em todas as exibições digitais a partir de quiosques interativos para sinalização digital.

* Unifique experiências e conteúdo digitais e locais com a reutilização de conteúdo aprimorada
* Criação e fluxos de trabalho de aprovação/publicação simplificados com suporte para inicializações
* Edite e entregue experiências interativas avançadas usando o Editor do SPA
* Uso de Lançamentos para planejar futuras alterações de conteúdo para o conteúdo de sinalização
* Reprodução medida em um canal de sequência
* Criar automaticamente a estrutura do projeto usando um arquivo de origem, como uma planilha do Excel
* Suporte ao reprodutor de mídia expandido com operação robusta online e offline (Sincronização inteligente) capaz de dimensionar para até as maiores redes de sinalização.
* Personalize por localização e configuração de dados usando espaços reservados dinâmicos.
* Informações unificadas orientadas pela integração do Adobe Analytics sobre o reprodutor do AEM Screens

Para obter mais detalhes sobre alterações no AEM Screens - consulte as Notas de versão na seção [Guia do usuário do AEM Screens](https://docs.adobe.com/content/help/pt-BR/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### Desenvolvimento de componentes e modelos {#component-amp-template-development}

* Maven Project Archetype 18+ para novos projetos, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Maven Project Archetype 1.0.6+ de aplicativo de página única para novos projetos, consulte o [Github para obter notas de versão](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versão 1.4, consulte o [Github para obter notas de versão](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operador &quot;in&quot; para strings, arrays e objetos:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Declarações de variável com data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Parâmetros de controle de lista e repetição: begin, step, end:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para data-sly-unwrap:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Suporte para números negativos

* Componentes principais 2.3.2+, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Sistema de grade para Contêiner de layout, consulte o [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: tornou o Google Closure Compiler padrão para minificação de clientlibs do JavaScript (o padrão antigo era Yahoo YUI) e atualizou o Google Closure Compiler para a versão v20190121
* Editor de modelo e políticas

   * Crie e edite modelos para aplicativos de página única que estão usando o JS SDK (também chamado de Editor do SPA)

* We.Retail 4.0 de referência do Site, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de ferramentas para atualizar sites existentes para aproveitar os recursos mais recentes do editor, consulte [Repositório Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM inclui a versão 1.12.4 da biblioteca jQuery para fornecer compatibilidade máxima com o código personalizado existente. As modificações foram feitas pela Adobe para solucionar problemas de segurança conhecidos.

#### Administração de site {#site-administration}

* O painel de [Referências](/help/sites-authoring/author-environment-tools.md#references) tem uma nova seção para listar links internos que apontam para a página selecionada. Isso é útil ao planejar usar ou excluir uma página offline, para ver quais páginas precisam ser ajustadas antes de torná-las offline.
* A [exibição em lista](/help/sites-authoring/basic-handling.md#list-view) tem uma nova coluna de fluxo de trabalho que mostra o status quando a página está em um fluxo de trabalho no momento.
* Nas [propriedades de página](/help/sites-authoring/editing-page-properties.md), agora é possível procurar ativos existentes ao atribuir uma Miniatura à página (guia Miniatura).

#### Editor de página {#page-editor}

* Permita a edição e composição em contexto de experiências de aplicativo de página única criadas com componentes do lado do cliente de Reação e Angular que estão aproveitando o JS SDK (também chamado de Editor do SPA)
* O Modo de estrutura é mostrado somente se a página tiver uma página de estrutura configurada.

#### Fragmentos de conteúdo e editor {#content-fragments-amp-editor}

* Novo painel de [Anotações](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) no Editor de fragmentos de conteúdo para fazer comentários gerais e ver os comentários que fazem no texto (também mostrar no trilho da Linha do tempo)
* Capacidade de definir o tipo de conteúdo padrão de um elemento de texto de várias linhas em um [Modelo do fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) para texto simples, rich text ou marcação
* Adicione [comentários/anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selecionando o texto na RTE (exibição em tela inteira)
* [Compare versões](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) de um fragmento de conteúdo lado a lado por meio do painel de Referências
* O Relatório de download de ativos agora mostra fragmentos de conteúdo corretamente
* Adicione o [suporte de fragmento de conteúdo à API HTTP do Assets](/help/assets/assets-api-content-fragments.md) por meio do /api.json. Há APIs para criar, atualizar, ler e excluir os fragmentos de conteúdo.

#### Fragmentos de experiência {#experience-fragments}

* Aprimoramento da indexação dos [fragmentos da experiência](/help/sites-authoring/experience-fragments.md), para que seu conteúdo seja encontrado na pesquisa por páginas em que estão sendo usados
* A opção [Exportar para o Target](/help/sites-administering/experience-fragments-target.md) agora permite enviar o Fragmento da experiência como JSON (o padrão é HTML) ou ambos

#### Tradução {#translation}

* Simplifique a criação de projetos de tradução usando os mestres de projeto
* Simplifique a execução de projetos de tradução definindo tarefas de tradução para o status aprovado por padrão
* Permitir atualização de páginas traduzidas com alterações na memória de tradução de terceiros
* Permitir exportar tarefas de tradução no formato JSON
* Atualize a integração do Microsoft Translation para usar a API V3

#### Gerenciamento de vários sites (MSM) {#multi-site-management-msm}

* Para configurações de roll-out que usam PushOnModify, melhor manuseio da operação de movimentação de página para evitar o estado inconsistente
* Criar uma nova página dentro da estrutura livecopy agora criará uma página autônoma por padrão
* Use recursos do MSM nos aplicativos de página única que estão usando o JS SDK (também chamado Editor do SPA)

#### Lançamentos {#launches}

* Novo fluxo de trabalho de revisão e aprovação para inicializações, e a capacidade de promover apenas as páginas de inicialização aprovadas
* Adição da [opção na interface do usuário para escolher excluir o Launch logo após a etapa de promoção](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Direcionamento e simulação de conteúdo {#content-targeting-simulation}

* A camada de dados do ContextHub e o mecanismo de regras do cliente do Javascript foram atualizados para usar o jQuery 3 por padrão.

#### AEM e Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Atualmente:
>
>* Somente `at.js 1.x` O é compatível se você estiver usando o Adobe Target como seu mecanismo de direcionamento no console Atividades do AEM.
>
>* Ambos `at.js. 1.x` e `at.js 2.x` são compatíveis se você estiver usando a exportação do Fragmento de experiência para o Target e executar Atividades no console do Target.


* A integração do Adobe Target agora pode usar a API padrão do Target. As versões anteriores do AEM usam a API HTTP clássica do Target, que agora está obsoleta.
* Adobe Target `mbox.js` A versão 63 está incluída. O Adobe recomenda alternar a implementação para `at.js` v1.x.
* `at.js` A versão 1.5.0 já está incluída. O Adobe recomenda usar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) à disposição `at.js` v1.x no site.

#### AEM e Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 está incluído. O Adobe recomenda que você altere a implementação para `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 está incluído. O Adobe recomenda usar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para provisionar o AppMeasurement.js no site.

#### AEM e comércio {#aem-commerce}

As melhorias na Estrutura de integração do Commerce estão em um ciclo de lançamento mais rápido desde a AEM 6.4. [Saiba mais aqui](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Complemento do Communities {#communities-add-on}

Para obter a versão mais recente, consulte [Implantação de comunidades](/help/communities/deploy-communities.md) da documentação.

##### Melhorias na participação da comunidade {#enhancements-to-community-engagement}

**Suporte a @Mentions**
O AEM Communities agora permite que usuários registrados marquem (mencionem) outros membros registrados para chamar sua atenção, em Conteúdo gerado pelo usuário. Os membros marcados (mencionados) são então notificados, com links para o Conteúdo gerado pelo usuário. No entanto, os usuários podem optar por desabilitar/habilitar as notificações da Web e de email.

![Suporte em menções](/help/release-notes/assets/at-mentions.png)

Os usuários da comunidade não precisam procurar seu nome, sobrenome ou nome de usuário para ver se alguém contatou eles ou precisa de sua atenção. Além disso, ele permite que os autores UGC procurem respostas de usuários registrados específicos que podem atender melhor o problema e adicionar entradas.

Os administradores da comunidade precisam **Ativar menção** em componentes da comunidade para permitir que usuários registrados usem a funcionalidade desses componentes.

**Mensagens em grupo**

Membros registrados da comunidade agora podem enviar mensagens diretas em massa para grupos por meio de uma única composição de email, em vez de enviar a mesma mensagem individualmente aos membros do grupo. Para permitir [mensagem em grupo](/help/communities/configure-messaging.md), habilite as duas instâncias do [Serviço de operações de mensagens](/help/communities/messaging.md#group-messaging).

![Mensagem em grupo](/help/release-notes/assets/group-messaging.png)

##### Aprimoramentos na moderação em massa {#enhancements-to-bulk-moderation}

Filtros personalizados na moderação em massa

[Filtros personalizados](/help/communities/moderation.md#custom-filters) agora pode ser desenvolvida e adicionada à interface do usuário de moderação em massa.

Um [projeto de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) que demonstra a filtragem por meio de marcas está disponível no [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Esse projeto pode ser usado como base para desenvolver filtros personalizados análogos.

![Filtros personalizados](/help/release-notes/assets/custom-tag-filter.png)

**Exibição em lista na moderação em massa**

Uma nova exibição em lista com interface do usuário aprimorada foi oferecida na moderação em massa para exibir entradas de Conteúdo gerado pelo usuário.

![Moderação em massa na exibição em lista](/help/release-notes/assets/list-view-moderation.png)

##### Melhorias no gerenciamento de site e de grupos {#enhancements-to-site-and-group-management}

**Site do lado do autor e administradores de grupo**

As comunidades, do AEM 6.5 em diante, permitem a administração descentralizada (e gerenciamento) de diferentes sites e grupos de comunidades/ grupos aninhados. As organizações que hospedam vários sites de comunidade e grupos aninhados agora podem selecionar membros para funções de administrador no lado do autor no momento de criação do site (e grupo).

![Administrador de site](/help/release-notes/assets/site-admin.png)

Os administradores de sites podem criar um grupo em qualquer nível de hierarquia e se tornar os administradores padrão. Posteriormente, esses administradores podem ser removidos por outros administradores de grupo. Os administradores de grupo podem gerenciar o grupo G1 e criar um subgrupo aninhado em G1.

##### Melhorias na ativação {#enhancements-to-enablement}

**Suporte SCORM 2017.1**

A funcionalidade de ativação do AEM 6.5 Communities suporta o modelo de referência de objeto de conteúdo compartilhável [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motor.

* Suporte à navegação por teclado em componentes de ativação
* Os componentes de ativação (por exemplo, Catálogo e reprodução do curso, atribuições, biblioteca de arquivos) no AEM Communities suportam a navegação pelo teclado para melhorar a acessibilidade.

##### Outras melhorias {#other-enhancements}

* Suporte ao Solr 7
* AEM Comunidades 6.5 oferece suporte à versão Apache Solr 7.0 da plataforma de pesquisa ao configurar o MSRP e o DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

O AEM 6.5 apresenta as seguintes funcionalidades e aprimoramentos para aumentar a produtividade de usuários do AEM, funções do DAM, e funções de criação e marketing associadas.

#### Integração com [!DNL Adobe Creative Cloud] e fluxos de trabalho criativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]O oferece várias maneiras de se integrar à e compartilhar ativos para uso em fluxos de trabalho nos quais as equipes criativas e de marketing ou empresas colaboram ativamente. [!DNL Adobe Creative Cloud] [!DNL Experience Manager]O 6.5 continua a melhorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Leia para conhecer os recursos e integrações específicos do [!DNL Experience Manager] 6.5 que você pode usar para suportar melhor seus casos de uso de velocidade de conteúdo.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. Os criadores podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem deixar os aplicativos com os quais estão mais familiarizados. Os criadores podem navegar, pesquisar, sair e fazer check-in de ativos com facilidade usando o painel no aplicativo em [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] aplicativos.

[!DNL Adobe Asset Link] faz parte de [Creative Cloud para empresas](https://www.adobe.com/br/creativecloud/business/enterprise.html) oferta. Para obter mais informações sobre isso, incluindo a configuração necessária de [!DNL Experience Manager] implantação, consulte [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

![Pesquisar ativos no Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] integração {#stock}

Sua organização pode usar o [!DNL Adobe Stock] plano corporativo dentro [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing. Você pode encontrar, visualizar e licenciar rapidamente [!DNL Adobe Stock] ativos que são salvos no Experience Manager, usando os poderosos recursos do DAM de [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties.

Para obter mais informações, consulte [Usar ativos do Adobe Stock no Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Visualizar imagem e licença do Adobe Stock no Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: Visualizar [!DNL Adobe Stock] imagem e licença de dentro [!DNL Experience Manager Assets].*

![Pesquise e filtre as imagens licenciadas do Adobe Stock no Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: Pesquise e filtre as [!DNL Adobe Stock] imagens em [!DNL Experience Manager].*

##### Referências dinâmicas em [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] usado em [!DNL Adobe InDesign] os arquivos são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados se moverem no repositório. Para obter mais informações, consulte [como gerenciar ativos compostos](/help/assets/managing-linked-subassets.md).

#### Recursos do Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] ajuda você a adquirir com facilidade, controlar efetivamente e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários corporativos internos entre dispositivos. Ele ajuda a melhorar a eficiência de compartilhamento de ativos, acelera o tempo de marketing de ativos e elimina o risco de uso que não está em conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

#### Connected Assets {#connectedassets}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de site e os ativos digitais necessários residem em silos diferentes.

[!DNL Experience Manager Sites]O oferece recursos para criar páginas da Web e o é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites.[!DNL Experience Manager Assets] [!DNL Experience Manager] O agora é compatível com o caso de uso acima, integrando [!DNL Sites] e [!DNL Assets]. Consulte [como configurar e usar o recurso Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

![Arrastar um ativo de um [!DNL Experience Manager] implantação em um [!DNL Sites] de uma página diferente [!DNL Experience Manager] implantação](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: Arrastar um ativo de um [!DNL Experience Manager] implantação em um [!DNL Sites] em uma página diferente [!DNL Experience Manager] implantação.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] fornece criação avançada de mídia avançada e entrega no [!DNL Experience Manager Assets] para impulsionar experiências de ponta que são imersivas e personalizadas. Ao fazer upload de um único ativo principal de qualidade e usar a renderização avançada em nuvem e os visualizadores do Adobe, você pode fornecer qualquer combinação de representações dinamicamente para dar suporte à estratégia de mídia de sua organização.

Para obter mais detalhes sobre novos [!DNL Dynamic Media] recursos, consulte [Notas de versão da Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Suporte para vídeo 360 {#video-support}

Gerencie seus arquivos de vídeo 360 diretamente no [!DNL Experience Manager] usando os visualizadores de ponta para fornecer experiências VR a desktops, dispositivos móveis e headsets VR. Para obter mais informações, consulte [Usar vídeo 360](/help/assets/360-video.md).

##### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter mais instruções, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Aprimoramentos de acessibilidade {#accessibility-enhancements}

[!DNL Dynamic Media] os visualizadores agora oferecem suporte para recursos de acessibilidade aprimorados, como suporte para Aria, leitores de tela e texto alternativo. Para obter mais detalhes, consulte [Guia de referência de visualizadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Aprimoramento da experiência de pesquisa {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partir da versão 6.5, os profissionais de marketing podem descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada contra o filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos no Experience Manager](/help/assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados de pesquisa nos aspectos de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Veja o número de ativos sem filtrar os resultados da pesquisa nos aspectos de pesquisa.*

#### Aprimoramento da usabilidade {#usability-enhancement}

Agora é possível selecionar todos os ativos carregados em uma pasta ou de um resultado de pesquisa de uma só vez. Isso ajuda a gerenciar vários ativos rapidamente. A caixa de seleção seleciona todos os ativos que se encaixam no cenário, digamos um resultado de pesquisa e não apenas os ativos que estão visíveis na variável [!DNL Experience Manager] interface.

![Use a opção Selecionar tudo para selecionar todos os ativos carregados com um clique.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figura: Use a opção Selecionar tudo para selecionar todos os ativos carregados com um clique.*

#### Aprimoramentos de metadados {#metadata-enhancements}

[!DNL Assets] permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/metadata-config.md#folder-metadata-schema).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [metadados em cascata](/help/assets/metadata-schemas.md#cascading-metadata).

#### Aprimoramentos de relatórios {#reporting-enhancements}

Os Fragmentos de conteúdo e compartilhamentos de link agora estão incluídos no relatório baixado. Para obter mais informações, consulte [Relatórios de ativos](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

O AEM 6.5 Forms traz vários novos recursos e melhorias. Os destaques incluem:

* Relatórios de transação para rastrear o número de formulários enviados, documentos processados e documentos renderizados
* Aprimoramentos de usabilidade para comunicações interativas
* Assinaturas digitais baseadas em nuvem em formulários adaptáveis
* Incorporação de formulários adaptáveis e comunicações interativas a aplicativos de página única (SPA) do AEM Sites.
* Suporte a variáveis em fluxos de trabalho do AEM
* Suporte ao padrão de exibição de dados em comunicações interativas
* Classificação de formulários adaptáveis e tabelas de comunicação interativas
* Validação automatizada de dados de entrada nos modelos de dados de formulário

Consulte a [Resumo dos novos recursos e melhorias no AEM 6.5 Forms](/help/forms/using/whats-new.md) para obter informações sobre recursos novos e aprimorados e recursos de documentação.

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

É possível integrar o Livefyre com sua instância do AEM 6.5. Consulte [como integrar o Livefyre com o AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### Aproveite o desenvolvimento focado no cliente {#leverage-customer-focused-development}

A Adobe está usando um modelo de desenvolvimento focado no cliente que permite aos clientes contribuir para todos os estágios do processo de desenvolvimento, durante a especificação, o desenvolvimento e o teste. Agradecemos a todos os clientes e parceiros neste processo.

A Adobe tem os procedimentos e processos estabelecidos para permitir a coleta, priorização e rastreamento de resolução de erros com foco no cliente e desenvolvimento de solicitação de melhoria. O [Portal de suporte Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) O é integrado ao Sistema de aprimoramento de Adobe e rastreamento de problemas. Sempre que possível, as perguntas do cliente são identificadas e resolvidas pela equipe de Suporte ao cliente. Ao ser dimensionada ao P&amp;D, todas as informações do cliente são coletadas e usada para fins de priorização e relatório. A prioridade é dada em desenvolvimento para suporte pago, problemas de garantia e melhorias pagas pelo cliente.

Esse processo de priorização gerou a correção de mais de 750 alterações focadas no cliente no AEM 6.5.

## Lista de arquivos que fazem parte da versão {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Início rápido independente: `cq-quickstart-6.5.0.jar`.
* Início rápido do servidor de aplicativos: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou posterior para os vários servidores da Web e plataformas. Consulte [link de download](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in para o Eclipse IDE ([leia mais e download](/help/sites-developing/aem-eclipse.md))

* Extensão do Editor de código de colchetes ([leia mais e download](/help/sites-developing/aem-brackets.md))
* Dependências de Maven/Gradle ([link de download](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componentes principais ([projeto do GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementação de referência We.Retail ([leia mais](/help/sites-developing/we-retail.md))
* Arquétipos de projeto do Maven:

   * para sites de pilha completos: [projeto do GitHub](https://github.com/adobe/aem-project-archetype)
   * para aplicativos de página única com estrutura de Reação/Angular: [projeto do GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Reprodutores do AEM Screens para várias plataformas de destino ([download](https://download.macromedia.com/screens/))

* Modelos de linguagem de conteúdo inteligente. O inglês está pré-instalado - mais idiomas podem ser baixados

   * [Alemão](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Espanhol](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francês](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Conjunto de ferramentas de modernização do AEM, por exemplo, a ferramenta de Conversão de diálogo. ([projeto do GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Pacote para adicionar PDF avançado ([leia mais](/help/assets/aem-pdf-rasterizer.md))
* Pacote para adicionar suporte de imagem RAW estendido ([leia mais](/help/assets/camera-raw.md))

**Forms**

* [Pacotes para recursos do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Idiomas {#languages}

A interface de usuário está disponível nos idiomas a seguir:

* Inglês
* Alemão
* Francês
* Espanhol
* Italiano
* Português do Brasil
* Japonês
* Chinês simplificado
* Chinês tradicional (suporte limitado)
* Coreano

[!DNL Experience Manager]O 6.5 foi certificado para GB18030-2005 CITS para usar o Padrão de codificação chinês.

## Instalar e atualizar {#install-update}

Para obter os requisitos de configuração, consulte [instruções de instalação](/help/sites-deploying/custom-standalone-install.md).

Para obter instruções detalhadas, consulte [documentação de atualização](/help/sites-deploying/upgrade.md).

## Plataformas compatíveis {#supported-platforms}

Encontre a matriz completa de plataformas compatíveis, incluindo suporte em [AEM 6.5 requisitos técnicos](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>O Oracle foi transferido para um modelo de Suporte a longo prazo (LTS) para produtos Oracle Java SE. O Java 9 e 10 são versões não LTS do Oracle. Consulte [Roteiro de suporte do Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html). O Adobe fornece suporte para versões LTS do Java para executar somente AEM na produção. O Java 11 é a versão recomendada para usar com o AEM 6.5.

## Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia constantemente as funcionalidades do produto e planeja substituí-las por versões mais potentes, ou decide reimplementar partes selecionadas para serem melhor preparadas para as expectativas ou extensões futuras.

Para [!DNL Adobe Experience Manager] 6.5. [leia a lista de recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md). A página também contém o anúncio prévio das alterações em um futuro próximo e um aviso importante para os clientes que atualizam de versões anteriores.

## Problemas conhecidos {#known-issues}

### Plataforma {#platform}

* Um problema é reportado onde o CRX-Quickstart e seu conteúdo são excluídos.

   Em cada uma dessas ações, verifique se a propriedade `htmllibmanager.fileSystemOutputCacheLocation` não é uma string vazia:

   1. Chamada `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Atualização para o AEM 6.5.
   3. Execução de &quot;migração de conteúdo lento&quot; no AEM 6.5.

   A [Base de dados de conhecimento](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) o artigo está disponível com mais detalhes e a solução alternativa para esse problema.

* Se você estiver usando o JDK 11 com AEM instância 6.5, algumas páginas poderão ser exibidas em branco após a implantação de alguns pacotes. A seguinte mensagem de erro é exibida no arquivo de log:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Para resolver este erro:

1. Pare a instância de AEM. Ir para `<aem_server_path_on_server>crx-quickstart\conf` e abra o `sling.properties` arquivo. O Adobe recomenda fazer um backup desse arquivo.

1. Pesquisar `org.osgi.framework.bootdelegation=`. Adicionar `jdk.internal.reflect,jdk.internal.reflect.*` propriedades para exibir o resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salve o arquivo e reinicie a instância de AEM.

### Sites {#sites}

* **Trabalhar com versões de página**: [Se uma página tiver sido movida, você não poderá mais executar uma visualização em nenhuma versão anterior à movimentação](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **Pesquisar:** A pesquisa não resulta em retornos se a string de pesquisa contiver espaço à esquerda ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadados de pasta**: depois de adicionar um botão de escolha, os campos ID e Valor não são renderizados como esperado e a funcionalidade de exclusão não funciona. (CQ-4261144)
* Ao renomear um ativo, não é possível usar um espaço em branco no nome do ativo. (CQ-4266403)

### Forms {#forms}

* Quando o AEM Forms é instalado no sistema operacional Linux, a assinatura digital com o módulo de segurança de hardware não funciona. (CQ-4266721)
* (AEM Forms somente na WebSphere) A opção **Fluxo de trabalho de formulários** > **Pesquisa de tarefas** não retorna nenhum resultado se você pesquisar por um **Administrador** com o **nome de usuário** como o critério de pesquisa. (CQ-4266457)

* O AEM Forms não converte arquivos TIF e TIFF com compactação JPEG para Documentos PDF. (CQ-4265972)
* As opções **Scanner de ativos do AEM Forms** e **Carta para migração de comunicação interativa** não funcionam na página **Migração do AEM Forms**. (CQ-4266572)

* (Somente JBoss 7) Quando você atualiza de uma versão anterior para AEM 6.5 Forms e a versão anterior tinha processos (.lca) que criaram e usaram uma cópia do processo de envio ou renderização padrão, o HTML5 Forms que usa esses processos (.lca) não executa as ações necessárias. (CQ-4243928)
* Em um formulário adaptável, quando um serviço de modelo de dados do formulário é chamado a partir do editor de regras para atualizar valores dinamicamente do componente de escolha de imagem, os valores do componente de escolha de imagem não são atualizados. (CQ-4254754)
* O instalador do AEM Forms Designer requer a versão de 32 bits do [Pacote de tempo de execução redistribuível do Visual C++ 2012](https://support.microsoft.com/pt-br/help/2977003/the-latest-supported-visual-c-downloads) e [Pacotes de tempo de execução redistribuíveis do Visual C++ 2013](https://support.microsoft.com/pt-br/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Certifique-se de que os pacotes de tempo de execução redistribuíveis mencionados acima estão instalados antes de iniciar a instalação. (CQ-4265668)

* O Gerador de PDF não suporta autenticação baseada em smart card.  Quando um administrador ativa a Política de Grupo `Interactive Logon: Require Smart card` em um servidor Windows, todos os usuários existentes do PDF Generator são invalidados.

* Quando um formulário adaptável é configurado para atualizar dinamicamente valores de um componente e a instância de publicação que hospeda o formulário é acessada por meio do distribuidor, a funcionalidade para atualizar dinamicamente os valores de um campo para de funcionar. Para resolver o problema, na instância de publicação, abra o CRXDE, navegue até `/libs/fd/af/runtime/clientlibs/guideChartReducer`e crie a propriedade listada abaixo.

   * Nome: allowProxy
   * Tipo: booliano
   * Valor: true
   * Protegido: false
   * Obrigatório: false
   * Vários: false
   * Criado automaticamente: Falso

   A propriedade habilita as bibliotecas de clientes na pasta de tempo de execução para acessar proxies. (CQ-4268679)

* Quando o AEM Forms for iniciado, a variável `SAX Security Manager could not be setup` for exibido.
* Ao abrir um PDF protegido com a Segurança de documento da AEM Forms em um Apple iOS ou iPadOS executando a versão 20.10.00 do Adobe Acrobat Reader.
* Às vezes, ao enviar um formulário contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 bytes é recebido na outra extremidade. O Apple iOS 15.1 fornece uma correção para o problema.

## Download e suporte ao produto (sites restritos) {#product-download-and-support-restricted-sites}

Os sites a seguir estão disponíveis somente para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/).

* Atualizações, patches e pacotes de produtos para obter funcionalidade adicional em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).

* [Suporte ao cliente via Admin Console](https://adminconsole.adobe.com/). Para obter mais informações, consulte [Nova experiência de suporte ao cliente do Adobe](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
