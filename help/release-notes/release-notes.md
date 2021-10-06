---
title: Notas de versão gerais para [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager]As notas o 6.5 que descrevem as informações da versão, novidades, como instalar e listas detalhadas de modificação.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: f8fcfa9e09167cd4dbaafe938bcbe3ee6ece270f
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 67%

---

# Notas de versão gerais para [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] |
|---|---|
| Versão | 6.5 |
| Tipo | Versão Principal |
| Data de disponibilidade geral | 8 de abril de 2019 |
| Atualizações recomendadas | Consulte [AEM atualizações recentes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR). |

### Trívia {#trivia}

O ciclo de lançamento desta versão do [!DNL Adobe Experience Manager] começou em 4 de abril de 2018, passou por 23 iterações de garantia de qualidade e correção de problemas, terminando em 28 de março de 2019. O número total de problemas relatados por clientes incluindo melhorias e novos recursos corrigidos nesta versão é de 1345.

[!DNL Adobe Experience Manager] O 6.5 está disponível por completo desde 8 de abril de 2019.

![Tela de logon do AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Novidades {#what-s-new}

[!DNL Adobe Experience Manager] O 6.5 é uma versão de atualização da base de código do  [!DNL Adobe Experience Manager] 6.4. Ele fornece funcionalidades novas e melhoradas, correções essenciais para o cliente, melhorias de alta prioridade para o cliente e correções gerais de bugs voltadas para a estabilização do produto. Ele também inclui [!DNL Adobe Experience Manager] versões 6.4 do Service Pack até o SP4.

A lista abaixo fornece uma visão geral, enquanto as páginas subsequentes listam os detalhes completos.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

Lista completa de alterações em [Base do AEM](/help/release-notes/wcm-platform.md).

A plataforma de [!DNL Adobe Experience Manager] 6.5 integrada na parte superior das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e o repositório de conteúdo Java: Apache Jackrabbit Oak 1.10.2.

O Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo servlet.

#### Suporte ao Java  {#java-support}

* Novo suporte para o Java 11, bem como o Java 8 já compatível.
* Para melhor desempenho, substitua os valores GC padrão por outros valores. Para obter mais informações, consulte a seção [install and update](/help/sites-deploying/custom-standalone-install.md).
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

#### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor de modelo de fluxo de trabalho introduzido na versão 6.4 foi aprimorado para incluir operações como Copiar e publicar, Suporte à variável em etapas do fluxo de trabalho e divisões OR e AND aprimoradas.

### [!DNL Experience Manager] Sites {#experience-manager-sites}

Lista completa de alterações em [AEM Sites e complementos](/help/release-notes/sites.md).

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

**Design**

* Unifique experiências e conteúdo digitais e locais com a reutilização de conteúdo aprimorada
* Criação e fluxos de trabalho de aprovação/publicação simplificados com suporte para inicializações
* Edite e entregue experiências interativas avançadas usando o Editor do SPA

**Entrega**

* Suporte ao reprodutor de mídia expandido com operação robusta online e offline (Sincronização inteligente) capaz de dimensionar para até as maiores redes de sinalização.

**Otimizar**

* Personalize por localização e configuração de dados usando espaços reservados dinâmicos.
* Informações unificadas orientadas pela integração do Adobe Analytics sobre o reprodutor do AEM Screens

Para obter mais detalhes sobre alterações no AEM Screens - consulte as Notas de versão no [Guia do Usuário do AEM Screens](https://docs.adobe.com/content/help/br/experience-manager-screens/user-guide/aem-screens-introduction.html).

### [!DNL Experience Manager Assets] {#experience-manager-assets}

Lista completa de alterações nas [AEM notas de versão do Assets 6.5](/help/release-notes/assets.md).

O AEM 6.5 apresenta as seguintes funcionalidades e aprimoramentos para aumentar a produtividade de usuários do AEM, funções do DAM, e funções de criação e marketing associadas.

#### Integração com a Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

A introdução do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html), uma experiência dentro do aplicativo para usuários criativos que trabalham em aplicativos da Adobe Creative Cloud, incluindo Photoshop, Illustrator e InDesign, simplifica a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. AEM aplicativo de desktop continua a suportar as necessidades dos usuários que trabalham com ativos do AEM no desktop, usando qualquer tipo de arquivo e qualquer aplicativo de desktop.

Além disso, o AEM integra com o Adobe Stock para ajudar a localizar, visualizar, licenciar e salvar ativos do Adobe Stock diretamente da interface do usuário na Web do AEM.

![Painel Link de ativos no Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Connected Assets {#connected-assets}

O recurso Ativos conectados é direcionado a implantações maiores com várias implantações do AEM Sites que precisam aproveitar os ativos de uma implantação central do AEM Assets DAM. Ela permite melhorar a governança dos ativos gerenciados centralmente, permitindo a alta eficiência do fornecimento de ativos para as várias implementações de sites.

### Dynamic Media {#dynamic-media}

O Dynamic Media oferece a criação avançada de mídia avançada e entrega no AEM Assets para conduzir experiências de ponta que são imersivas e personalizadas. Com um único ativo principal de alta qualidade, você pode aproveitar nossa renderização avançada em nuvem, Corte inteligente e os melhores visualizadores para oferecer as experiências mais envolventes com o desempenho líder do setor.

Os novos recursos incluem:

* Suporte para vídeos de 360 e fones VR
* Miniaturas de vídeo personalizadas
* Suporte avançado à acessibilidade
* Proteção contra vinculação automática

#### Experiência do usuário e pesquisa {#user-experience-and-search}

Os aprimoramentos principais ajudam a localizar os ativos corretos mais rapidamente, fornecendo facetas dinâmicas de pesquisa, além de controlar com mais eficiência vários ativos fornecendo a capacidade de selecionar todos os ativos de qualquer pasta ou resultado de pesquisa.

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

Consulte o [Resumo dos novos recursos e melhorias no AEM 6.5 Forms](/help/forms/using/whats-new.md) para obter informações sobre recursos novos e aprimorados e recursos de documentação.

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

O AEM 6.5 adiciona novos recursos e melhorias às Comunidades. Os destaques desta versão são:

* Marcação de membro registrado (@menção) com suporte ao criar Conteúdo gerado pelo usuário.
* Conjunto de mensagens em massa direto a membros do grupo agora é suportado.
* Filtros personalizados desenvolvidos e adicionados na interface do usuário de moderação em massa. Um [projeto de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) demonstrando a filtragem por tags pode ser usado como base para desenvolver filtros personalizados análogos.
* Nova exibição em lista fornecida com a interface do usuário aprimorada na moderação em massa.
* Administradores separados de diferentes sites de comunidade e grupos aninhados podem ser atribuídos, em vez de um único administrador de comunidade.
* A funcionalidade de ativação de AEM 6.5 Comunidades suporta o mecanismo [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/).
* Suporte à navegação por teclado em componentes de ativados para acessibilidade aprimorada.
* O Apache Solr 7.0 é compatível ao configurar o MSRP e o DSRP.

Para obter uma lista detalhada das alterações, consulte as [Notas de versão do AEM 6.5 Communities](/help/release-notes/communities-release-notes.md).

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

É possível integrar o Livefyre com sua instância do AEM 6.5. Consulte [como integrar o Livefyre com AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html).

### Aproveite o desenvolvimento focado no cliente {#leverage-customer-focused-development}

A Adobe está usando um modelo de desenvolvimento focado no cliente que permite aos clientes contribuir para todos os estágios do processo de desenvolvimento, durante a especificação, o desenvolvimento e o teste. Agradecemos a todos os clientes e parceiros neste processo.

A Adobe tem os procedimentos e processos estabelecidos para permitir a coleta, priorização e rastreamento de resolução de erros com foco no cliente e desenvolvimento de solicitação de melhoria. O [Portal de suporte do Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) é integrado ao Sistema de aprimoramento do Adobe e rastreamento de falhas. Sempre que possível, as perguntas do cliente são identificadas e resolvidas pela equipe de Suporte ao cliente. Ao ser dimensionada ao P&amp;D, todas as informações do cliente são coletadas e usada para fins de priorização e relatório. A prioridade é dada em desenvolvimento para suporte pago, problemas de garantia e melhorias pagas pelo cliente.

Esse processo de priorização gerou a correção de mais de 750 alterações focadas no cliente no AEM 6.5.

## Lista de arquivos que fazem parte da versão {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Início rápido independente: `cq-quickstart-6.5.0.jar`.
* Início rápido do servidor de aplicativos: `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou posterior para os vários servidores da Web e plataformas. Consulte [link de download](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
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

**Ativos**

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

Para obter instruções detalhadas, consulte a [documentação de atualização](/help/sites-deploying/upgrade.md).

## Plataformas compatíveis {#supported-platforms}

Encontre a matriz completa de plataformas compatíveis, incluindo o nível de suporte em [AEM 6.5 requisitos técnicos](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>O Oracle foi transferido para um modelo de Suporte a longo prazo (LTS) para produtos Oracle Java SE. O Java 9 e 10 são versões não LTS do Oracle. Consulte [Roteiro de suporte do Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html). O Adobe fornece suporte para versões LTS do Java para executar somente AEM na produção. O Java 11 é a versão recomendada para usar com o AEM 6.5.

## Recursos obsoletos e removidos {#deprecated-and-removed-features}

A Adobe avalia constantemente as funcionalidades do produto e planeja substituí-las por versões mais potentes, ou decide reimplementar partes selecionadas para serem melhor preparadas para as expectativas ou extensões futuras.

Para [!DNL Adobe Experience Manager] 6.5, [leia a lista de recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md). A página também contém o anúncio prévio das alterações em um futuro próximo e um aviso importante para os clientes que atualizam de versões anteriores.

## Problemas conhecidos {#known-issues}

[Lista de problemas conhecidos](/help/release-notes/known-issues.md)

### Download e suporte ao produto (sites restritos) {#product-download-and-support-restricted-sites}

Os sites a seguir estão disponíveis somente para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/).

* Atualizações, patches e pacotes de produtos para funcionalidade adicional em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).

* [Suporte ao cliente via Admin Console](https://adminconsole.adobe.com/). Para obter mais informações, consulte [Nova experiência de Suporte ao Cliente do Adobe](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
