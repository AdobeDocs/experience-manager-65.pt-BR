---
title: Notas de versão gerais do  [!DNL Adobe Experience Manager] 6.5
description: Notas do [!DNL Adobe Experience Manager] 6.5 descrevendo as informações da versão, as novidades, como instalar e as listas de alterações detalhadas.
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '4493'
ht-degree: 2%

---

# Notas de Versão Gerais do [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] |
|---|---|
| Versão | 6,5 |
| Tipo | Versão Principal |
| Data de disponibilidade geral | 8 de abril de 2019 |
| Atualizações recomendadas | Consulte [atualizações recentes sobre o AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR). |

### Trivia {#trivia}

O ciclo de lançamento desta versão do [!DNL Adobe Experience Manager] começou em 4 de abril de 2018, passou por 23 iterações de controle de qualidade e correção de erros e terminou em 28 de março de 2019. O número total de problemas relacionados ao cliente, incluindo aprimoramentos e novos recursos corrigidos nesta versão, é 1345.

O [!DNL Adobe Experience Manager] 6.5 está disponível ao público desde 8 de abril de 2019.

![Tela de Login do AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novidades {#what-s-new}

O [!DNL Adobe Experience Manager] 6.5 é uma versão de atualização para a base de código [!DNL Adobe Experience Manager] 6.4. Ele fornece funcionalidades novas e aprimoradas, correções essenciais para o cliente, melhorias de alta prioridade para o cliente e correções gerais de erros voltadas para a estabilização do produto. Ele também inclui versões do Service Pack do [!DNL Adobe Experience Manager] 6.4 até o SP4.

A lista abaixo fornece uma visão geral, enquanto as páginas subsequentes listam os detalhes completos.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

A plataforma do [!DNL Adobe Experience Manager] 6.5 se baseia nas versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e do Repositório de Conteúdo Java™: Apache Jackrabbit Oak 1.10.2.

O Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo de servlet.

#### Suporte para Java™  {#java-support}

* Novo suporte para Java™ 11 e o já compatível Java™ 8.
* Para obter o desempenho ideal, substitua os valores de GC padrão por outros valores. Para obter mais informações, consulte a seção [instalar e atualizar](/help/sites-deploying/custom-standalone-install.md).
* As atualizações de manutenção do Java™ 11 e do Java™ 8 são distribuídas pelo Adobe para uso do cliente em projetos relacionados ao AEM, quando não estiverem disponíveis publicamente no Oracle.

#### Desenvolvimento em Java™ {#java-development}

* Agora existem [duas versões do Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), uma versão recomendada com interfaces públicas que não estão marcadas para descontinuação e uma versão que inclui interfaces marcadas para descontinuação.

#### Interface do usuário {#user-interface}

Várias melhorias foram feitas na interface do usuário para torná-la mais produtiva e fácil de usar.

* Nova interface do usuário de gerenciamento de permissões para usuários e grupos.
* As Exibições de coluna agora também carregam apenas entradas que estão visíveis na tela e só carregam mais quando o usuário está começando a rolar a tela. A Lista e a Visualização de cartão já faziam isso desde a versão 6.0 (aprimorada no 6.4).
* As Exibições de coluna agora incluem o status do fluxo de trabalho para páginas/ativos quando aplicável.
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) é uma maneira rápida de executar uma ação com todas as páginas/ativos na mesma pasta.
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) tenta executar a ação em todas as páginas/ativos, não apenas no que foi carregado. Uma caixa de diálogo de aviso será exibida se a ação não for atualizada para lidar com Ações em massa.

>[!CAUTION]
>
>O Adobe não planeja fazer mais melhorias na interface clássica. O AEM 6.5 tem a interface clássica incluída e os clientes que estão atualizando de versões anteriores podem continuar usando-a como está. A interface clássica permanece totalmente compatível enquanto é descontinuada. [Leia mais](/help/sites-deploying/ui-recommendations.md).

#### Pesquisa e indexação {#indexing-and-search}

* A pesquisa no Oak agora é compatível com facetas dinâmicas. Por exemplo, o painel de filtro na pesquisa de ativos mostra o número estimado de resultados.
* O QueryBuilder foi estendido para fornecer resultados com facetas dinâmicas.

#### Atualizar {#upgrade}

* O upgrade direto no local para AEM 6.5 é compatível com clientes que executam AEM 6.2, 6.3 e 6.4. Os clientes que usam o 5.x ou 6.0/6.1 e desejam usar a atualização no local precisam primeiro atualizar para o 6.4. Em seguida, atualize para o 6.5 ou atualize por meio da transferência do conteúdo entre as instâncias diretamente para o AEM 6.5.
* O procedimento de atualização permanece basicamente o mesmo no 6.5.
* Continuamos a oferecer suporte aos recursos Compatibilidade com versões anteriores, Avaliação de complexidade de atualização e Atualizações sustentáveis introduzidos no 6.4. Sempre que necessário, foram feitas atualizações específicas para cada versão nessas áreas.
* O empacotamento do Detector de padrões agora está simplificado. Há um pacote que avalia as atualizações para a versão 6.5 das versões de origem disponíveis.
* Para obter detalhes sobre o procedimento de atualização, consulte a [documentação de atualização](/help/sites-deploying/upgrade.md).

#### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor de Modelo de Fluxo de Trabalho introduzido na versão 6.4 foi aprimorado para incluir mais operações, como Copiar e Publish, suporte a Variáveis em etapas de Fluxo de Trabalho e divisões `OR` e `AND` aprimoradas.

#### Repositório {#repository}

* A base do Adobe Experience Manager 6.5 é a partir das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e do repositório de conteúdo Java™: Apache Jackrabbit Oak 1.10.2.
* Para obter uma visão geral dos problemas corrigidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>A nova versão do Tar de segmento do Oak, presente desde o AEM 6.3, requer uma migração de repositório. Esta etapa é obrigatória se você estiver atualizando de uma versão mais antiga do TarMK ou quiser alternar o novo Tar de segmento de outro tipo de persistência. Para obter mais informações sobre quais são os benefícios do novo Segment Tar, consulte as [Perguntas frequentes sobre a migração para o Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Adição das bibliotecas de utilitários OSGi Promises e Converter.

#### Segurança {#security}

* Adição da expiração de senha para o usuário administrador.

#### Servidor Web {#web-server}

* A distribuição Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo de servlet (AEM 6.4 enviado com a 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Aplicativos gerenciados de página única {#managed-single-page-apps}

O Editor de páginas adiciona a capacidade de editar conteúdo em contexto e compor/layout dentro de experiências renderizadas no lado do cliente (também conhecido [como Editor de SPA](/help/sites-developing/spa-architecture.md)). Os aplicativos de página única existentes criados com o React ou o Angular de estrutura do JavaScript podem ser estendidos com o SDK SJ do AEM para se tornarem editáveis para os profissionais.

Enviado pela primeira vez como parte do AEM 6.4 SP2, com AEM 6.5 o suporte para SPA obtém as seguintes capacidades:

* Usar o Editor de modelos para editar e configurar as partes editáveis do AEM do SPA
* Use o Gerenciamento de vários sites para criar experiências de país, franquias ou SPA com rótulo branco

#### Gerenciamento de conteúdo headless {#headless-content-management}

O AEM pode veicular o conteúdo em vários formatos e a partir de vários níveis da pilha. Alguns já existem desde 2008 com o [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e o [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). O Content Services ([Exportador de Modelo do Sling](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=pt-BR)) foi introduzido no AEM 6.3 e é o método usado pelo AEM SJ SDK para hidratar aplicativos de página única. A [API HTTP para o Assets](/help/assets/mac-api-assets.md) é uma API CRUD, que foi estendida para AEM 6.5.

Novos recursos da API HTTP:

* Adição do suporte a [Fragmento de Conteúdo à API HTTP para o Assets](/help/assets/assets-api-content-fragments.md) criar, atualizar, ler e excluir fragmentos.
* Exponha listas de Fragmentos de Conteúdo pelos Serviços de Conteúdo com o [Componente Principal da Lista de Fragmentos de Conteúdo](https://www.aemcomponents.dev).
* [Biblioteca de Componentes Principais](https://www.aemcomponents.dev) que mostra a saída JSON do Content Services padrão para cada componente

#### Complemento do Screens {#screens-add-on}

Projete, entregue e otimize experiências com eficiência em todas as exibições digitais, desde quiosques interativos até sinalização digital.

* Unifique experiências e conteúdo em ambientes digitais e na loja com a reutilização aprimorada de conteúdo
* Simplificação da criação e dos fluxos de trabalho de aprovação/publicação com suporte para lançamentos
* Editar e fornecer experiências interativas avançadas usando o Editor de SPA
* Uso de Lançamentos para planejar alterações futuras de conteúdo para conteúdo de sinalização
* Reprodução medida em um canal de sequência
* Criar automaticamente a estrutura do projeto usando um arquivo de origem, como uma planilha do Excel
* Suporte expandido para reprodutor de mídia com operação online e offline robusta (Sincronização inteligente) capaz de escalar até mesmo para as maiores redes de sinalização.
* Personalize por local ou configuração do conteúdo acionado por dados usando espaços reservados dinâmicos.
* Insights unificados impulsionados pela integração do Adobe Analytics no AEM Screens Player

Para obter mais detalhes sobre as alterações no AEM Screens, consulte as Notas de versão no [Guia do Usuário do AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=pt-BR).

#### Desenvolvimento de componentes e modelos {#component-amp-template-development}

* Maven Project Archetype 18+ para novos projetos, consulte [GitHub para notas de versão](https://github.com/adobe/aem-project-archetype/releases).
* Arquétipo de projeto Maven de aplicativo de página única 1.0.6+ para novos projetos, consulte [GitHub para notas de versão](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versão 1.4, consulte [GitHub das notas de versão](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operador &quot;in&quot; para sequências, matrizes e objetos:

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * Declarações de variável com data-sly-set :

     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Listar e repetir parâmetros de controle: início, etapa, fim:

     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para data-sly-unwrap:

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * Suporte para números negativos

* Componentes principais 2.3.2+, consulte [GitHub para notas de versão](https://github.com/adobe/aem-core-wcm-components/releases).
* Sistema de grade para o Contêiner de layout, consulte [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: tornou o Google Closure Compiler padrão para a minificação do JavaScript clientlibs (o padrão antigo era Yahoo YUI) e atualizou o Google Closure Compiler para a versão v20190121
* Editor de modelos e políticas

   * Criar e editar modelos para aplicativos de página única que estão usando o SDK JS (também chamado de Editor de SPA)

* Consulte o site de referência We.Retail 4.0, consulte [GitHub para obter as notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de ferramentas para atualizar sites existentes para usar os recursos mais recentes do editor, consulte [repositório do GitHub](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>O AEM inclui a versão 1.12.4 da biblioteca jQuery para fornecer compatibilidade máxima com o código personalizado existente. As modificações foram feitas pelo Adobe para solucionar problemas conhecidos de segurança.

#### Administração do site {#site-administration}

* O painel [Referência](/help/sites-authoring/author-environment-tools.md#references) tem uma nova seção para listar links internos que apontam para a página selecionada. Isso é útil ao planejar colocar uma página offline ou excluí-la - para ver quais páginas precisam ser ajustadas antes de colocá-las offline.
* A [exibição de lista](/help/sites-authoring/basic-handling.md#list-view) tem uma nova coluna de fluxo de trabalho que mostra o status quando a página está em um fluxo de trabalho.
* Nas [propriedades de página](/help/sites-authoring/editing-page-properties.md), agora é possível procurar ativos existentes ao atribuir uma Miniatura à página (guia Miniatura).

#### Editor de página {#page-editor}

* Permitir a edição em contexto e a composição de experiências de aplicativo de página única criadas com componentes do lado do cliente do React e do Angular que estão usando o SDK JS (também chamado de Editor de SPA)
* O modo andaime só é exibido se a página tiver uma página de andaime configurada.

#### Fragmentos de conteúdo e editor {#content-fragments-amp-editor}

* Novo painel [Anotações](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) no Editor de fragmento de conteúdo para fazer comentários gerais e ver comentários feitos no texto (também exibido no painel Linha do tempo)
* Capacidade de definir o tipo de conteúdo padrão de um elemento de texto multilinha em um [modelo de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-models.md) como texto simples, rich text ou marcação
* Adicionar [comentário/anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selecionando texto no RTE (modo de exibição em tela inteira)
* [Comparar versões](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) lado a lado de um Fragmento de conteúdo por meio do painel de Referência
* O Relatório de download de ativos agora mostra os Fragmentos de conteúdo de acordo
* Adicione o suporte a [Fragmento de Conteúdo à API HTTP do Assets](/help/assets/assets-api-content-fragments.md) via /api.json. Existem APIs para criar, atualizar, ler e excluir fragmentos de conteúdo.

#### Fragmentos de experiência {#experience-fragments}

* A indexação dos [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md) foi aprimorada; portanto, o conteúdo foi encontrado na pesquisa de páginas em que estão sendo usados.
* A opção [Exportar para o Target](/help/sites-administering/experience-fragments-target.md) agora permite enviar o Fragmento de experiência como JSON (o padrão é HTML) ou ambos.

#### Tradução {#translation}

* Simplifique a criação de projetos de tradução usando Projetos principais.
* Simplifique a execução de projetos de tradução definindo trabalhos de tradução para o status aprovado por padrão.
* Permite a atualização de páginas traduzidas com alterações na Memória de tradução de terceiros.
* Permitir a exportação de trabalhos de tradução no formato JSON.
* Atualize a integração do Microsoft® Translation para usar a API V3.

#### Gerenciamento de vários sites (MSM) {#multi-site-management-msm}

* Para configurações de implantação que usam PushOnModify, melhor manipulação da operação de movimentação de página para evitar estado inconsistente.
* A criação de uma página dentro da estrutura do livecopy cria uma página independente por padrão.
* Usar recursos do MSM em aplicativos de página única que estejam usando o SDK JS (também chamado de Editor de SPA)

#### Lançamentos {#launches}

* Novo fluxo de trabalho de revisão e aprovação para lançamentos e capacidade de promover somente páginas de lançamento aprovadas
* Adicionada a opção [na interface para optar por excluir a Inicialização logo após a etapa de promoção](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Simulação e direcionamento de conteúdo {#content-targeting-simulation}

* A camada de dados do ContextHub e o mecanismo de regras do lado do cliente JavaScript foram atualizados para usar o jQuery 3 por padrão.

#### AEM e ADOBE TARGET {#aem-amp-adobe-target}

>[!CAUTION]
>
>Atualmente:
>
>* Somente `at.js 1.x` será suportado se você estiver usando o Adobe Target como mecanismo de direcionamento dentro do console Atividades do AEM.
>
>* Há suporte para `at.js. 1.x` e `at.js 2.x` se estiver usando a exportação de Fragmento de experiência para o Target e executando Atividades no console do Target.

* A integração do Adobe Target agora usa a API do Target Standard. As versões anteriores do AEM usam a API HTTP do Target Classic, que agora está obsoleta.
* O Adobe Target `mbox.js` versão 63 está incluído. A Adobe recomenda que você alterne a implementação para `at.js` v1.x.
* A versão 1.5.0 de `at.js` foi incluída. A Adobe recomenda que você use o [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) para provisionar a versão `at.js` v1.x para o site.

#### AEM e ADOBE ANALYTICS {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 está incluído. A Adobe recomenda que você alterne a implementação para `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 está incluído. A Adobe recomenda que você use o [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) para provisionar o AppMeasurement.js para o site.

#### AEM e COMMERCE {#aem-commerce}

As melhorias no Commerce integration framework estão em um ciclo de liberação mais rápido desde o AEM 6.4. Saiba mais sobre a [Integração do AEM e do Adobe Commerce usando o Commerce integration framework](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html?lang=pt-BR).

#### Complemento de comunidades {#communities-add-on}

Para obter a versão mais recente, consulte a seção [Implantação de comunidades](/help/communities/deploy-communities.md) da documentação.

##### Melhorias no engajamento da comunidade {#enhancements-to-community-engagement}

**Suporte a @Mentions**
O AEM Communities agora permite que os usuários registrados marquem (mencionem) outros membros registrados para chamar a atenção deles, no Conteúdo gerado pelo usuário. Os membros marcados (mencionados) são notificados, com deep link para o Conteúdo Gerado pelo Usuário correspondente. Os usuários podem, no entanto, optar por desativar/ativar as notificações da Web e por email.

![No suporte para menções](/help/release-notes/assets/at-mentions.png)

Os usuários da comunidade não precisam pesquisar seu nome, sobrenome ou nome de usuário para ver se alguém entrou em contato com eles ou precisa de sua atenção. Além disso, permite que os autores do UGC busquem resposta de usuários registrados específicos que podem resolver melhor o problema e adicionar entradas.

Os administradores da comunidade precisam **Habilitar a Menção** em componentes da comunidade para permitir que os usuários registrados usem a funcionalidade nesses componentes.

**Mensagens de grupo**

Os membros da comunidade registrados agora podem enviar mensagens diretas em massa para grupos por meio de uma única composição de email, em vez de enviar a mesma mensagem individualmente para os membros do grupo. Para permitir [mensagens de grupo](/help/communities/configure-messaging.md), habilite ambas as instâncias do [Serviço de Operações de Mensagens](/help/communities/messaging.md#group-messaging).

![Mensagem de grupo](/help/release-notes/assets/group-messaging.png)

##### Aprimoramentos na moderação em massa {#enhancements-to-bulk-moderation}

Filtros personalizados na moderação em massa

[Filtros personalizados](/help/communities/moderation.md#custom-filters) agora podem ser desenvolvidos e adicionados à interface de moderação em massa.

Um [projeto de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) que demonstra a filtragem por meio de marcas está disponível no [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Este projeto pode ser usado como base para desenvolver filtros personalizados análogos.

![Filtros personalizados](/help/release-notes/assets/custom-tag-filter.png)

**Exibição de lista na Moderação em massa**

A nova Exibição de lista com interface aprimorada foi fornecida em moderação em massa para exibir entradas de Conteúdo gerado pelo usuário.

![Moderação em massa na exibição de lista](/help/release-notes/assets/list-view-moderation.png)

##### Melhorias no gerenciamento de site e de grupo {#enhancements-to-site-and-group-management}

**Administradores de site e de grupo do lado do autor**

Communities, AEM 6.5 em diante, permite a administração descentralizada (e gestão) de diferentes sites comunitários e grupos/grupos aninhados. Organizações que hospedam vários sites da comunidade e grupos aninhados agora podem selecionar membros para funções de administrador no lado do autor no momento da criação do site (e do grupo).

![Administrador do site](/help/release-notes/assets/site-admin.png)

Os administradores do site podem criar um grupo em qualquer nível de hierarquia e se tornar os administradores padrão. Esses administradores podem ser removidos posteriormente por outros administradores de grupo. Os administradores de grupo podem gerenciar o grupo G1 e criar um subgrupo aninhado em G1.

##### Melhorias na ativação {#enhancements-to-enablement}

**Suporte ao SCORM 2017.1**

A funcionalidade de habilitação das Comunidades AEM 6.5 dá suporte ao mecanismo [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) do Modelo de Referência de Objeto de Conteúdo Compartilhável.

* Suporte para navegação por teclado em componentes de ativação
* Os componentes de ativação (por exemplo, Catálogo e reprodução do curso, Atribuições, Biblioteca de arquivos) no AEM Communities suportam a navegação pelo teclado para acessibilidade aprimorada.

##### Outras melhorias {#other-enhancements}

* Suporte a Solr 7
* As comunidades AEM 6.5 oferecem suporte à versão Apache Solr 7.0 da plataforma de pesquisa ao configurar o MSRP e o DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

O AEM 6.5 apresenta os seguintes recursos e melhorias para aumentar a produtividade de usuários do AEM, funções do DAM e funções criativas e de marketing associadas.

#### Integração com [!DNL Adobe Creative Cloud] e fluxos de trabalho criativos {#integration-with-adobe-creative-cloud-and-creative-workflows}

O [!DNL Adobe Experience Manager] oferece várias formas de integração com o [!DNL Adobe Creative Cloud] e de compartilhamento de ativos para uso em fluxos de trabalho nos quais as equipes criativas, de marketing ou comerciais colaborem estreitamente. O [!DNL Experience Manager] 6.5 continua a aprimorar a integração e a simplifica ainda mais para expor mais oportunidades e simplificar os métodos existentes.

Leia para conhecer os recursos e integrações específicos do [!DNL Experience Manager] 6.5 que você pode usar para oferecer melhor suporte aos casos de uso da velocidade do conteúdo.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] fortalece a colaboração entre profissionais de criação e marketing no processo de criação de conteúdo. Os criadores podem acessar o conteúdo armazenado em [!DNL Experience Manager Assets], sem sair dos aplicativos com os quais estão mais familiarizados. Os profissionais de criação podem navegar, pesquisar, sair e fazer check-in de ativos sem problemas usando o painel no aplicativo nos aplicativos [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] é parte da oferta [Creative Cloud para empresa](https://www.adobe.com/br/creativecloud/business/enterprise.html). Para obter mais informações sobre ele, incluindo a configuração necessária da sua implantação do [!DNL Experience Manager], consulte [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

![Pesquisar ativos no Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### Integração do [!DNL Adobe Stock] {#stock}

Sua organização pode usar o plano corporativo [!DNL Adobe Stock] no [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos de criação e marketing. Você pode encontrar, visualizar e licenciar rapidamente os ativos do [!DNL Adobe Stock] que foram salvos no Experience Manager, usando os poderosos recursos DAM do [!DNL Experience Manager].

O serviço [!DNL Adobe Stock] fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos 3D de alta qualidade, com curadoria e isentos de royalties para todos os seus projetos criativos.

Para obter mais informações, consulte [Usar ativos do Adobe Stock no Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Visualizar imagem e licença do Adobe Stock no Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figura: visualize a imagem e a licença do [!DNL Adobe Stock] em [!DNL Experience Manager Assets].*

![Pesquisar e filtrar as imagens licenciadas do Adobe Stock no Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figura: Pesquise e filtre as [!DNL Adobe Stock] imagens licenciadas em [!DNL Experience Manager].*

##### Referências dinâmicas em [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] usados em [!DNL Adobe InDesign] arquivos são dinâmicos. As referências são atualizadas automaticamente se os ativos referenciados forem movidos para o repositório. Para obter mais informações, consulte [como gerenciar ativos compostos](/help/assets/managing-linked-subassets.md).

#### Recursos do Brand Portal {#brand-portal-capabilities}

O [!DNL Experience Manager Assets Brand Portal] ajuda você a adquirir, controlar com eficácia e distribuir com segurança os ativos aprovados para fornecedores/agências externos e usuários de negócios internos em todos os dispositivos. Ele ajuda a melhorar a eficiência do compartilhamento de ativos, acelera o lançamento dos ativos no mercado e elimina o risco de uso fora de conformidade e acesso não autorizado.

Para obter mais informações, consulte [Novidades no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=pt-BR).

#### Connected Assets {#connectedassets}

Em grandes empresas, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais necessários residem em diferentes silos.

O [!DNL Experience Manager Sites] oferece recursos para criar páginas da Web e o [!DNL Experience Manager Assets] é o sistema de Gerenciamento de Ativos Digitais (DAM) que fornece os ativos necessários para sites. [!DNL Experience Manager] agora dá suporte ao caso de uso acima integrando [!DNL Sites] e [!DNL Assets]. Consulte [como configurar e usar o recurso Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

![Arraste um ativo de uma implantação do [!DNL Experience Manager] em uma página [!DNL Sites] de uma implantação do [!DNL Experience Manager] diferente](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figura: arraste um ativo de uma implantação do [!DNL Experience Manager] em uma página do [!DNL Sites] em uma implantação do [!DNL Experience Manager] diferente.*

#### Dynamic Media {#dynamic-media}

O [!DNL Dynamic Media] fornece criação e entrega aprimoradas de mídia avançada no [!DNL Experience Manager Assets] para impulsionar experiências de última geração que são imersivas e personalizadas. Ao fazer upload de um único ativo principal de alta qualidade e usar a renderização de nuvem e visualizadores avançados do Adobe, você pode fornecer qualquer combinação de representações dinamicamente para oferecer suporte à estratégia de mídia de sua organização.

Para obter mais detalhes sobre os novos recursos do [!DNL Dynamic Media], consulte as [Notas de Versão do Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Suporte a vídeo 360 {#video-support}

Gerencie seus arquivos de 360 vídeos diretamente no [!DNL Experience Manager] usando os visualizadores de última geração para fornecer experiências de RV para desktops, dispositivos móveis e headsets de RV. Para obter mais informações, consulte [Usando Vídeo 360](/help/assets/360-video.md).

##### Miniaturas de vídeo personalizadas {#custom-video-thumbnails}

Agora é possível personalizar as miniaturas dos ativos de vídeo usando quadros do próprio vídeo ou outro conteúdo armazenado no DAM. Para obter instruções adicionais, consulte [Sobre miniaturas de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Aprimoramentos de acessibilidade {#accessibility-enhancements}

[!DNL Dynamic Media] visualizadores agora oferecem suporte para recursos de acessibilidade aprimorados, como suporte para Aria, leitores de tela e texto alternativo. Para obter detalhes adicionais, consulte [Guia de Referência de Visualizadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Aprimoramento da experiência de pesquisa {#experience-enhancement-for-searching}

A partir do [!DNL Experience Manager] 6.5, os profissionais de marketing poderão descobrir os ativos desejados mais rapidamente na página de resultados da pesquisa. Os aspectos de pesquisa são atualizados com o número de ativos mesmo antes da aplicação do filtro de pesquisa. Ver a contagem esperada em relação ao filtro ajuda os usuários a navegar pelos resultados da pesquisa com eficiência. Para obter mais informações, consulte [Pesquisar ativos no Experience Manager](/help/assets/search-assets.md).

![Veja o número de ativos sem filtrar os resultados da pesquisa nas facetas de pesquisa](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: veja o número de ativos sem filtrar os resultados da pesquisa nas facetas de pesquisa.*

#### Aprimoramento de usabilidade {#usability-enhancement}

Agora é possível selecionar todos os ativos carregados em uma pasta ou em um resultado de pesquisa de uma só vez. Ele ajuda você a gerenciar vários ativos rapidamente. A caixa de seleção seleciona todos os ativos que se encaixam no cenário, digamos um resultado de pesquisa, e não apenas os ativos que estão visíveis na interface do [!DNL Experience Manager].

![Use a opção Selecionar tudo para selecionar todos os ativos carregados com um único clique.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figura: use a opção Selecionar tudo para selecionar todos os ativos carregados com um único clique.*

#### Aprimoramentos de metadados {#metadata-enhancements}

O [!DNL Assets] permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta. Agora é possível atribuir um esquema de metadados de pasta a uma pasta existente ou ao criar uma pasta. Para obter mais informações, consulte [Esquema de metadados de pasta](/help/assets/metadata-config.md#folder-metadata-schema).

Ao especificar metadados em cascata, as opções podem ser carregadas de um arquivo JSON no tempo de execução, digamos, em vez de digitar manualmente no formulário. Para obter mais informações, consulte [metadados em cascata](/help/assets/metadata-schemas.md#cascading-metadata).

#### Melhorias nos relatórios {#reporting-enhancements}

Os Fragmentos de conteúdo e os compartilhamentos de link estão incluídos no relatório baixado agora. Para obter mais informações, consulte [relatórios do Assets](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

O AEM 6.5 Forms traz vários novos recursos e melhorias. Os destaques incluem:

* Relatórios de transação para rastrear o número de formulários enviados, documentos processados e documentos renderizados
* Melhorias de usabilidade nas comunicações interativas
* Assinaturas digitais em nuvem em formulários adaptáveis
* Incorpore formulários adaptáveis e comunicações interativas em um aplicativo de página única (SPA) do AEM Sites.
* Suporte para variáveis em fluxos de trabalho do AEM
* Suporte a padrões de exibição de dados em comunicações interativas
* Classificação de formulários adaptáveis e tabelas de comunicação interativas
* Validação automatizada de dados de entrada em modelos de dados de formulário

Consulte o [Resumo dos novos recursos e melhorias no AEM 6.5 Forms](/help/forms/using/whats-new.md) para obter informações sobre recursos novos e aprimorados e recursos de documentação.

### Usar o desenvolvimento com foco no cliente {#use-customer-focused-development}

A Adobe está usando um modelo de desenvolvimento focado no cliente que permite que os clientes contribuam para todos os estágios do processo de desenvolvimento, durante a especificação, o desenvolvimento e o teste. Nossos agradecimentos vão para todos os clientes e parceiros que contribuíram neste processo.

O Adobe tem os procedimentos e processos em vigor para permitir a coleta, a priorização e o rastreamento da resolução de erros focada no cliente e o desenvolvimento de solicitações de aprimoramento. O [Portal de suporte do Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) está integrado ao Sistema de Aperfeiçoamento de Adobe e Rastreamento de Falhas. As dúvidas do cliente são identificadas e resolvidas pela equipe de Suporte ao cliente, quando possível. Quando encaminhadas para P&amp;D, todas as informações do cliente são capturadas e usadas para priorização e geração de relatórios. No desenvolvimento, é dada prioridade ao suporte pago, aos problemas de garantia e aos aprimoramentos pagos pelo cliente.

Esse processo de priorização produziu mais de 750 alterações focadas no cliente corrigidas no AEM 6.5.

## Lista de arquivos que fazem parte da versão {#list-of-files-that-are-part-of-the-release}

**Fundação**

* Quickstart Autônomo: `cq-quickstart-6.5.0.jar`.
* Início Rápido do Servidor de Aplicativos: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou posterior para os vários servidores e plataformas da Web. Consulte [link de download](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in para Eclipse IDE ([leia mais e baixe](/help/sites-developing/aem-eclipse.md))

* Extensão para o Editor de Código de Colchetes ([leia mais e baixe](/help/sites-developing/aem-brackets.md))
* Dependências Maven/Gradle ([link de download](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Componentes principais ([projeto do GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implementação de referência do We.Retail ([leia mais](/help/sites-developing/we-retail.md))
* Arquétipos de projeto Maven:

   * para sites de pilha completa: [projeto do GitHub](https://github.com/adobe/aem-project-archetype)
   * para aplicativos de página única com React/Angular: [projeto do GitHub](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens Players para várias plataformas de destino ([download](https://download.macromedia.com/screens/))

* Modelos de linguagem de conteúdo inteligente. O idioma inglês é pré-instalado - mais idiomas podem ser baixados

   * [Alemão](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Espanhol](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italiano](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Francês](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Conjunto de ferramentas de Modernização de AEM, por exemplo, Ferramenta de conversão de caixa de diálogo. ([Projeto do GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Pacote para adicionar Rasterizador de PDF aprimorado ([leia mais](/help/assets/aem-pdf-rasterizer.md))
* Pacote para adicionar suporte estendido a imagem RAW ([leia mais](/help/assets/camera-raw.md))

**Forms**

* [Pacotes para recursos do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [SDK do cliente OSGi do AEM Forms](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Idiomas {#languages}

A interface do usuário do está disponível nos seguintes idiomas:

* Inglês
* Alemão
* Francês
* Espanhol
* Italiano
* Português do Brasil
* Japonês
* Chinês Simplificado
* Chinês tradicional (suporte limitado)
* Coreano

O [!DNL Experience Manager] 6.5 foi certificado para CITS GB18030-2005 para usar o Padrão de Codificação Chinês.

## Instalar e atualizar {#install-update}

Para obter os requisitos de instalação, consulte [instruções de instalação](/help/sites-deploying/custom-standalone-install.md).

Para obter instruções detalhadas, consulte [documentação de atualização](/help/sites-deploying/upgrade.md).

## Plataformas compatíveis {#supported-platforms}

Encontre a matriz completa de plataformas compatíveis, incluindo o nível de suporte em [requisitos técnicos de AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>O Oracle foi transferido para um modelo de Suporte a longo prazo (LTS) para produtos Oracle Java™ SE. O Java™ 9 e 10 são versões não-LTS do Oracle. Consulte o [roteiro de suporte do Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html). O Adobe oferece suporte a versões LTS do Java™ para executar AEM somente na produção. O Java™ 11 é a versão recomendada para uso com AEM 6.5.

## Recursos obsoletos e removidos {#deprecated-and-removed-features}

O Adobe avalia constantemente os recursos do produto e, com o passar do tempo, os substitui por versões mais potentes ou decide reimplementar determinadas partes com o objetivo de prepará-las de maneira mais apropriada às expectativas ou extensões futuras.

Para [!DNL Adobe Experience Manager] 6.5, [leia a lista de recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md). A página também contém um pré-anúncio das alterações futuras e um aviso importante para os clientes que atualizam de versões anteriores.

## Problemas conhecidos {#known-issues}

### Platform {#platform}

* É relatado um problema em que o CRX-Quickstart e seu conteúdo são excluídos.

  Em cada uma dessas ações, verifique se a propriedade `htmllibmanager.fileSystemOutputCacheLocation` não é uma cadeia de caracteres vazia:

   1. Chamando `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Atualização para o AEM 6.5.
   3. Execução de &quot;migração de conteúdo lento&quot; no AEM 6.5.

  Um artigo da [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) está disponível com mais detalhes e a solução alternativa para esse problema.

* Se você estiver usando o JDK 11 com a instância AEM 6.5, algumas páginas podem ser exibidas em branco após a implantação de alguns pacotes. A seguinte mensagem de erro é exibida no arquivo de log:

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

Para resolver esse erro:

1. Pare a instância do AEM. Vá para `<aem_server_path_on_server>crx-quickstart\conf` e abra o arquivo `sling.properties`. O Adobe recomenda fazer um backup desse arquivo.

1. Pesquisar por `org.osgi.framework.bootdelegation=`. Adicione as propriedades `jdk.internal.reflect,jdk.internal.reflect.*` para exibir o resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Salve o arquivo e reinicie a instância do AEM.

### Sites {#sites}

* **Trabalhando com Versões de Página**: [Se uma página tiver sido movida, você não poderá mais executar uma visualização em nenhuma versão feita antes da movimentação](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Ativos {#assets}

* **Pesquisa:** A pesquisa não resultará em nenhum retorno se a cadeia de caracteres de pesquisa contiver espaços à esquerda ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadados de pasta**: depois de adicionar um botão de opção, o campo de ID e Valor não é renderizado conforme esperado e a funcionalidade de exclusão não funciona. (CQ-4261144)
* Ao renomear um ativo, não é possível usar um espaço em branco no nome do ativo. (CQ-4266403)

### Forms {#forms}

* Quando o AEM Forms é instalado no sistema operacional Linux®, a Assinatura digital com o Módulo de segurança de hardware não funciona. (CQ-4266721)
* (Somente no AEM Forms no WebSphere®) A opção **Forms Workflow** > **Pesquisa de Tarefas** não retornará nenhum resultado se você pesquisar por um **Administrador** com **Nome de Usuário** como critério de pesquisa. (CQ-4266457)

* A AEM Forms não consegue converter arquivos TIF e TIFF com compactação JPEG em Documentos PDF. (CQ-4265972)
* As opções **Scanner do AEM Forms Assets** e **Migração de Carta para Comunicação Interativa** não funcionam na página **Migração do AEM Forms**. (CQ-4266572)

* (Somente JBoss® 7) Quando você atualiza de uma versão anterior para o AEM 6.5 Forms e a versão anterior tinha processos (.lca) que criaram e usaram uma cópia do processo de envio ou renderização padrão, o HTML5 Forms usando esses processos (.lca) não executa as ações necessárias. (CQ-4243928)
* Em um formulário adaptável, quando um serviço de modelo de dados de formulário é chamado do editor de regras para atualizar dinamicamente valores do componente de escolha de imagem, os valores do componente de escolha de imagem não são atualizados. (CQ-4254754)
* O instalador do AEM Forms Designer requer a versão de 32 bits do [pacote de tempo de execução redistribuível do Visual C++ 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) e [pacotes de tempo de execução redistribuíveis do Visual C++ 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Verifique se os pacotes de tempo de execução redistribuíveis mencionados anteriormente estão instalados antes de iniciar a instalação. (CQ-4265668)

* O PDF Generator não oferece suporte à autenticação baseada em cartão inteligente. Quando um administrador habilita a Política de Grupo `Interactive Logon: Require Smart card` em um servidor Windows, todos os usuários existentes do PDF Generator são invalidados.

* Quando um formulário adaptável é configurado para atualizar dinamicamente os valores de um componente e a instância de publicação que hospeda o formulário é acessada por meio do Dispatcher, a funcionalidade para atualizar dinamicamente os valores de um campo deixa de funcionar. Para resolver o problema, na instância de publicação, abra o CRXDE, navegue até `/libs/fd/af/runtime/clientlibs/guideChartReducer` e crie a propriedade listada abaixo.

   * Nome: allowProxy
   * Tipo: Booleano
   * Valor: verdadeiro
   * Protegido: Falso
   * Obrigatório: Falso
   * Múltiplo: Falso
   * Criado Automaticamente: Falso

  A propriedade permite que as bibliotecas de clientes na pasta de tempo de execução acessem proxies. (CQ-4268679)

* Quando o AEM Forms for iniciado, o aviso `SAX Security Manager could not be setup` será exibido.
* Ao abrir um PDF protegido com o AEM Forms Document Security em um Apple iOS ou iPadOS executando a versão 20.10.00 do Adobe Acrobat Reader
* Quando você envia um formulário contendo um campo de upload de HTML padrão de um dispositivo Apple iOS, às vezes, o conteúdo do arquivo não é enviado e um arquivo de 0 bytes é recebido na outra extremidade. O Apple iOS 15.1 fornece uma correção para o problema.

## Download e suporte do produto (sites restritos) {#product-download-and-support-restricted-sites}

Os seguintes sites estão disponíveis somente para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do Produto em licensing.adobe.com](https://licensing.adobe.com/).

* Atualizações, patches e pacotes de produtos para funcionalidade adicional na [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).

* [Suporte ao Cliente via Admin Console](https://adminconsole.adobe.com/). Para obter mais informações, consulte [Nova experiência de suporte ao cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).
