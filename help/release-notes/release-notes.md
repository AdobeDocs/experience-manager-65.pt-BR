---
title: Notas de versão gerais do Adobe Experience Manager 6.5
description: As notas o Adobe Experience Manager 6.5 que descrevem as informações da versão, novidades, como instalar e listas detalhadas de modificação.
uuid: b916624e-9486-4391-8c6f-cb4045e78490
contentOwner: chuesler
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 7d3ceccb-4f00-4e11-9c9f-6de46a455e02
docset: aem65
translation-type: tm+mt
source-git-commit: 23dfcc944a83dd683078cfe00f85c4cc734e7752
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 81%

---


# Notas de versão gerais do Adobe Experience Manager 6.5{#general-release-notes-for-adobe-experience-manager}

## Informações da versão {#release-information}

<table>
 <tbody>
  <tr>
   <th>Produto</th>
   <td>Adobe Experience Manager<br /> </td>
  </tr>
  <tr>
   <th>Versão</th>
   <td>6.5</td>
  </tr>
  <tr>
   <th>Tipo</th>
   <td>Versão Principal</td>
  </tr>
  <tr>
   <th>Data de disponibilidade geral</th>
   <td>8 de abril de 2019<br /> </td>
  </tr>
  <tr>
   <th>Atualizações recomendadas</th>
   <td>See <a href="https://helpx.adobe.com/br/experience-manager/aem-releases-updates.html">AEM Releases and Updates</a></td>
  </tr>
 </tbody>
</table>

### Trívia {#trivia}

O ciclo de versão desta versão do Adobe Experience Manager começou em 4 de abril de 2018, passou por 23 iterações de garantia de qualidade e correção de problemas, terminando em 28 de março de 2019. O número total de problemas relatados por clientes incluindo melhorias e novos recursos corrigidos nesta versão é de 1345.

O Adobe Experience Manager 6.5 está disponível por completo desde 8 de abril de 2019.

![Tela de logon do AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novidades {#what-s-new}

O Adobe Experience Manager 6.5 é uma versão de atualização para o código de base do Adobe Experience Manager 6.4. Ele fornece funcionalidades novas e melhoradas, correções essenciais para o cliente, melhorias de alta prioridade para o cliente e correções gerais de bugs voltadas para a estabilização do produto. Além de incluir as versões do Adobe Experience Manager 6.4 Service Pack até o SP4.

A lista abaixo fornece uma visão geral - enquanto as páginas subsequentes listas os detalhes completos.

### Base do Experience Manager {#experience-manager-foundation}

Lista completa de alterações em [Base do AEM](/help/release-notes/wcm-platform.md).

A plataforma do Adobe Experience Manager 6.5 integrada na parte superior das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e o repositório de conteúdo do Java: Apache Jackrabbit Oak 1.10.2.

O Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo servlet.

#### Suporte ao Java  {#java-support}

* Novo suporte para o Java 11, bem como o Java 8 já compatível
* Para melhor desempenho, substitua os valores GC padrão por outros valores. Para obter informação, consulte a seção [Instalar e atualizar](/help/sites-deploying/custom-standalone-install.md).
* As atualizações de manutenção do Java 11 e Java 8 serão distribuídas pela Adobe para o uso dos clientes em projetos relacionados ao AEM, quando não disponibilizadas publicamente no Oracle

#### Java Development {#java-development}

* There are now [two versions of the Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), a recommended version with public interfaces that are not marked for deprecation, as well as a version that includes interfaces marked for deprecation.

#### Interface do usuário {#user-interface}

Vários aprimoramentos foram feitos à interface do usuário para torná-la mais produtiva e fácil de usar.

* Nova interface do usuário de gerenciamento de permissões para usuários e grupos
* As exibições em coluna agora também só carregam entradas visíveis na tela e só carregam mais quando o usuário começa a rolar. A exibição em lista e cartão já faziam isso desde a versão 6.0 (aprimorado na 6.4)
* As exibições em coluna agora incluem o status de fluxo de trabalho de páginas/ativos, quando aplicável
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) é uma forma rápida de executar uma ação com todas as páginas/ativos na mesma pasta
* A ação [Selecionar tudo](/help/sites-authoring/basic-handling.md#select-all) tenta executar a ação para todas as páginas/ativos, não só nos que foram carregados. Uma caixa de diálogo de aviso será exibida se a ação não tiver sido atualizada para tratar de ações em massa

>[!CAUTION]
>
>A Adobe não planeja fazer aprimoramentos adicionais à interface do usuário clássica. O AEM 6.5 tem a interface do usuário clássica incluída, e os clientes que atualizam de versões anteriores podem continuar a usando da mesma forma. Observe que a interface do usuário clássica permanece completamente compatível mesmo enquanto obsoluta. [Leia mais](/help/sites-deploying/ui-recommendations.md).

#### Pesquisar e indexar {#search-indexing}

* A pesquisa no Oak agora suporta aspectos dinâmicos. Por exemplo, o painel de filtros na pesquisa de ativos mostra a quantidade estimada de resultados.
* O QueryBuilder foi expandido para fornecer resultados com aspectos dinâmicos

#### Atualização {#upgrade}

* A atualização local direta para o AEM 6.5 é compatível com clientes que executam o AEM 6.2, 6.3 e 6.4. Clientes que usam a versão 5.x ou 6.0/6.1 e querem usar a atualização local devem atualizar para a versão 6.4 primeiro e, em seguida atualizar para a 6.5, ou atualizar por meio de transferência de conteúdos entre as instâncias diretamente para o AEM 6.5.

#### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor de modelo de fluxo de trabalho introduzido na versão 6.4 foi aprimorado para incluir operações como Copiar e publicar, Suporte à variável em etapas do fluxo de trabalho e divisões OR e AND aprimoradas.

### Sites do Experience Manager {#experience-manager-sites}

Full list of changes in [AEM Sites and Add-ons](/help/release-notes/sites.md).

#### Aplicativos de página única gerenciados {#managed-single-page-apps}

O Editor de página adiciona a capacidade de editar conteúdo no contexto e compor/fazer o layout dentro das experiências de renderização do lado do cliente (também chamado [Editor do SPA](/help/sites-developing/spa-architecture.md)). Aplicativos de página única existentes criados com a estrutura de Reação ou Angular do JavaScript podem ser exportados com o AEM SJ SDK para se tornarem editáveis para usuários.

Em primeiro lugar enviado como parte do AEM 6.4 SP2, com o AEM 6.5 o suporte ao SPA adquire as seguintes funcionalidades:

* Usar o editor de modelo para editar e configurar as partes editáveis do AEM do SPA
* Usar o gerenciamento de vários sites para criar país, franquia ou experiências SPA de marca branca

#### Gerenciamento de conteúdo sem periféricos {#headless-content-management}

O AEM tem a capacidade de fornecer conteúdo em vários formatos e de diferentes níveis de empilhamento. Alguns têm estado disponíveis desde 2008 com o [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) e o [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Os serviços de conteúdo ([Sling Model Exporter](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)) foi introduzido no AEM 6.3 e é o método usado pelo AEM SJ SDK para recuperar aplicativos de página única. A [API HTTP do Assets](/help/assets/mac-api-assets.md) é uma API CRUD, que foi estendida para o AEM 6.5.

Novos recursos da API HTTP:

* Adição do [Suporte de fragmento de conteúdo para a API HTTP do Assets](/help/assets/assets-api-content-fragments.md) para criar, atualizar, ler e excluir fragmentos.
* Expor listas dos fragmentos de conteúdo por meio dos serviços de conteúdo com o [Componente principal da lista de fragmentos de conteúdo](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Biblioteca de conteúdo principal](https://opensource.adobe.com/aem-core-wcm-components/library.html) que mostra a saída JSON padrão dos serviços de conteúdo de cada componente

#### Complemento do Screens {#screens-add-on}

Crie, entregue e otimize experiências com eficiência em todas as exibições digitais a partir de quiosques interativos para sinalização digital.

**Design**

* Unifique experiências e conteúdo digitais e locais com a reutilização de conteúdo aprimorada
* Criação e fluxos de trabalho de aprovação/publicação simplificados com suporte para inicializações
* Edite e entregue experiências interativas avançadas usando o Editor do SPA

**Entrega**

* Suporte ao reprodutor de mídia expandido com operação robusta online e offline (Sincronização inteligente) capaz de dimensionar para até as maiores redes de sinalização.

**Otimizar**

* Personalize por localização e configuração de dados usando espaços reservados dinâmicos.
* Informações unificadas orientadas pela integração do Adobe Analytics sobre o reprodutor do AEM Screens

For more details on changes to AEM Screens - see the Release Notes in the [AEM Screens User Guide](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).

### Experience Manager Assets {#experience-manager-assets}

Full list of changes in [AEM 6.5 Assets release notes](/help/release-notes/assets.md).

O AEM 6.5 apresenta as seguintes funcionalidades e aprimoramentos para aumentar a produtividade de usuários do AEM, funções do DAM, e funções de criação e marketing associadas.

#### Integração com a Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

A introdução do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html), uma experiência dentro do aplicativo para usuários criativos que trabalham em aplicativos da Adobe Creative Cloud, incluindo Photoshop, Illustrator e InDesign, simplifica a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. O aplicativo de desktop AEM continua a suportar as necessidades dos usuários que trabalham com ativos do AEM na área de trabalho, usando qualquer tipo de arquivo e qualquer aplicativo de desktop.

Além disso, o AEM integra com o Adobe Stock para ajudar a localizar, visualizar, licenciar e salvar ativos do Adobe Stock diretamente da interface do usuário na Web do AEM.

![Painel Link de ativos no Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Connected Assets {#connected-assets}

A capacidade dos ativos conectados é direcionada a implantações maiores com várias implantações de AEM Sites que precisam aproveitar ativos de uma implantação central do DAM AEM Assets. Ela permite melhorar a governança dos ativos gerenciados centralmente, permitindo a alta eficiência do fornecimento de ativos para as várias implementações de sites.

### Dynamic Media {#dynamic-media}

O Dynamic Media oferece a criação avançada de mídia avançada e entrega no AEM Assets para conduzir experiências de ponta que são imersivas e personalizadas. Com um único ativo principal de alta qualidade, você pode aproveitar nossa renderização avançada em nuvem, Corte inteligente e os melhores visualizadores para oferecer as experiências mais envolventes com o desempenho líder do setor.

Os novos recursos incluem:

* Suporte para vídeos de 360 e fones VR
* Miniaturas de vídeo personalizadas
* Suporte avançado à acessibilidade
* Proteção contra vinculação automática

#### Experiência do usuário e pesquisa {#user-experience-and-search}

Os aprimoramentos principais ajudam a localizar os ativos corretos mais rapidamente, fornecendo facetas dinâmicas de pesquisa, além de controlar com mais eficiência vários ativos fornecendo a capacidade de selecionar todos os ativos de qualquer pasta ou resultado de pesquisa.

### Adobe Experience Manager Forms {#experience-manager-forms}

O AEM 6.5 Forms traz vários novos recursos e melhorias. Os destaques incluem:

* Relatórios de transação para rastrear o número de formulários enviados, documentos processados e documentos renderizados
* Aprimoramentos de usabilidade para comunicações interativas
* Assinaturas digitais baseadas em nuvem em formulários adaptáveis
* Incorporação de formulários adaptáveis e comunicações interativas a aplicativos de página única (SPA) do AEM Sites.
* Suporte a variáveis em fluxos de trabalho do AEM
* Suporte ao padrão de exibição de dados em comunicações interativas
* Classificação de formulários adaptáveis e tabelas de comunicação interativas
* Validação automatizada de dados de entrada nos modelos de dados de formulário

See the [Summary of new features and enhancements in AEM 6.5 Forms](/help/forms/using/whats-new.md) for information about new and improved features and documentation resources.

### Comunidades do Experience Manager {#communitiesreleasenotes}

O AEM 6.5 adiciona novos recursos e melhorias às Comunidades. Os destaques desta versão são:

* Marcação de membro registrado (@menção) com suporte ao criar Conteúdo gerado pelo usuário.
* Conjunto de mensagens em massa direto a membros do grupo agora é suportado.
* Filtros personalizados desenvolvidos e adicionados na interface do usuário de moderação em massa. A [sample project](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) demonstrating filtering by tags can be used as a base to develop analogous custom filters.
* Nova exibição em lista fornecida com a interface do usuário aprimorada na moderação em massa.
* Administradores separados de diferentes sites de comunidade e grupos aninhados podem ser atribuídos, em vez de um único administrador de comunidade.
* Enablement functionality of AEM 6.5 Communities supports [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.
* Suporte à navegação por teclado em componentes de ativados para acessibilidade aprimorada.
* O Apache Solr 7.0 é compatível ao configurar o MSRP e o DSRP.

For detailed list of changes, see [AEM 6.5 Communities release notes](/help/release-notes/communities-release-notes.md).

### Experience Manager Livefyre {#experience-manager-livefyre}

É possível integrar o Livefyre com sua instância do AEM 6.5. As informações sobre como integrar o Livefyre com o AEM estão localizadas aqui:

* [Integração do Livefyre](https://helpx.adobe.com/experience-manager/6-4/help/sites-administering/livefyre.html)

### Aproveite o desenvolvimento voltado ao cliente {#leverage-customer-focused-development}

A Adobe está usando um modelo de desenvolvimento focado no cliente que permite aos clientes contribuir para todos os estágios do processo de desenvolvimento, durante a especificação, o desenvolvimento e o teste. Agradecemos a todos os clientes e parceiros neste processo.

A Adobe tem os procedimentos e processos estabelecidos para permitir a coleta, priorização e rastreamento de resolução de erros com foco no cliente e desenvolvimento de solicitação de melhoria. The [Adobe Marketing Cloud Support Portal](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) is integrated with the Adobe Enhancement &amp; Defect Tracking System. As perguntas do cliente são identificadas e resolvidas pelo Atendimento do cliente sempre que possível. Ao ser dimensionada ao P&amp;D, todas as informações do cliente são coletadas e usada para fins de priorização e relatório. A prioridade é concedida durante o processo de desenvolvimento para problemas de suporte pago e de garantia, além de e aprimoramentos do cliente pago.

Esse processo de priorização gerou a correção de mais de 750 alterações focadas no cliente no AEM 6.5.

## Lista de arquivos que fazem parte da versão {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Quickstart independente: cq-quickstart-6.5.0.jar
* Início rápido do servidor de aplicativos: cq-quickstart-6.5.0.war
* Dispatcher 4.3.2 ou posterior para os vários servidores da Web e plataformas ([link de download](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html))
* Plug-in para o Eclipse IDE ([leia mais e download](/help/sites-developing/aem-eclipse.md))

* Extensão do Editor de código de colchetes ([leia mais e download](/help/sites-developing/aem-brackets.md))
* Dependências de Maven/Gradle ([link de download](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/))

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

* [Pacotes para recursos do AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)
* [SDK do cliente OSGi do AEM Forms](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

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

O Experience Manager 6.5 foi certificado para GB18030-2005 CITS para usar o Padrão de codificação chinês.

## Instalar e atualizar {#install-update}

Consulte as [instruções de instalação](/help/sites-deploying/custom-standalone-install.md) para obter os requisitos de instalação.

Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.

## Plataformas compatíveis {#supported-platforms}

Consulte a matriz completa de plataformas suportadas, incluída. Nível de suporte nos [Requisitos técnicos do AEM 6.5](/help/sites-deploying/technical-requirements.md)

Oak MicroKernel forOak MicroKernel for

>[!NOTE]
>
>O Oracle migrou para um modelo de &quot;Suporte de longo prazo&quot; (LTS) dos produtos Oracle Java SE. Java 9 and 10 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). A adobe fornecerá apenas o suporte para versões LTS do Java para executar o AEM na produção. Portanto, o Java 11 é a versão recomendada para usar com o AEM 6.5.

## Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia constantemente as funcionalidades do produto e planeja substituí-las por versões mais potentes, ou decide reimplementar partes selecionadas para serem melhor preparadas para as expectativas ou extensões futuras.

Para o Adobe Experience Manager 6.5, [leia a lista de recursos obsoletos e funcionalidades removidas](/help/release-notes/deprecated-removed-features.md). A página também contém o anúncio prévio das alterações em um futuro próximo e um aviso importante para os clientes que atualizam de versões anteriores.

## Problemas conhecidos {#known-issues}

[Lista de problemas conhecidos](/help/release-notes/known-issues.md)

### Download e suporte ao produto (sites restritos) {#product-download-and-support-restricted-sites}

Estes sites estão disponíveis somente para clientes. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [](https://daycare.day.com) [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)

* [Atendimento ao cliente em daycare.day.com](https://daycare.day.com)

