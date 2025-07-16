---
title: Notas de versão do  [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista de alterações detalhada para o [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 80482da847b86c91963dbb0d37375e370a503588
workflow-type: tm+mt
source-wordcount: '6643'
ht-degree: 1%

---

# Notas de Versão do Service Pack Mais Recente do [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 22 de maio de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de desempenho, estabilidade e segurança lançadas desde a disponibilização inicial do 6.5, em abril de 2019. [Instalar este Service Pack](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principais recursos e melhorias

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

Os principais recursos e aprimoramentos desta versão incluem:

* [Hiperlinks acessíveis com estilo de texto misto em PDFs estáticos](https://helpx.adobe.com/content/dam/help/pt-br/experience-manager/6-5/forms/pdf/using-designer.pdf): os hiperlinks que contêm estilos de texto misto em PDFs estáticos agora são marcados como um único elemento acessível. Esse aprimoramento simplifica a estrutura da árvore de tags, melhora a navegação do leitor de tela e oferece suporte a uma melhor conformidade com acessibilidade.

* [Matriz de Plataforma com Suporte Atualizada](/help/forms/using/aem-forms-jee-supported-platforms.md)

  A versão mais recente apresenta atualizações na matriz de plataformas compatíveis, garantindo a compatibilidade com as tecnologias mais recentes.

   * Cliente do gerenciador de conteúdo IBM® 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Driver JDBC do Microsoft® SQL Server 12.8

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bits) 

* [Componente de anexo de arquivo protegido](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): como medida de segurança, o componente agora impede o envio de arquivos com extensões modificadas que tentam ignorar as verificações de tipo de arquivo permitidas. Esses arquivos são bloqueados durante o envio para garantir que somente tipos de arquivos válidos sejam aceitos.

* FORMS-20533: o AEM Forms agora inclui uma atualização da versão do Struts 2.5.33 para 6.x para o componente de formulários. Isso fornece alterações do Struts que não estavam incluídas no SP23. O suporte foi adicionado por meio de um [Hotfix](/help/release-notes/aem-forms-hotfix.md) que você pode [baixar e instalar](/help/release-notes/aem-forms-hotfix.md) para adicionar suporte à versão mais recente do Struts.

* FORMS-20532: O AEM Forms agora inclui uma atualização da versão do Struts 2.5.33 para 6.x para o componente de saída. Isso fornece alterações do Struts que não estavam incluídas no SP23. O suporte foi adicionado por meio de um [Hotfix](/help/release-notes/aem-forms-hotfix.md) que você pode [baixar e instalar](/help/release-notes/aem-forms-hotfix.md) para adicionar suporte à versão mais recente do Struts.

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Correção de problemas no Service Pack 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Acessibilidade {#sites-accessibility-6523}

* As seções de tela de desenho nas páginas do Editor do AEM agora oferecem suporte à acessibilidade total do teclado. Os usuários podem ativar títulos de seção e editar botões usando apenas o teclado, sem depender do mouse. Essa atualização garante a conformidade com a WCAG 2.1.1 e melhora a usabilidade entre componentes (como Teaser, Imagem, Carrossel, Layout, Timewarp e Modais de anotação). (SITES-25256) <!-- 6.5 LTS SP1 -->
* Correção de um problema de acessibilidade no Editor de páginas do AEM, em que o foco do teclado era redefinido inesperadamente para o início da barra de ferramentas Demográfica após a ativação de botões como Persona, Carrinho ou Abandonado. O foco agora permanece no botão ativado para oferecer suporte à navegação consistente do teclado e aos fluxos de trabalho do leitor de tela. (SITES-25306)
* Correção de um problema crítico de acessibilidade no Editor de páginas do AEM, em que os elementos da tela de desenho em várias caixas de diálogo e modais (por exemplo, painel de ativos ou pré-visualização de layout) não podiam ser operados usando apenas um teclado. Todos os elementos interativos da tela agora oferecem suporte à navegação somente pelo teclado, garantindo a conformidade com o critério de sucesso 2.1.1 da WCAG 2.1 (SITE-25256)
* Correção de um problema de acessibilidade na interface do Administrador do Sites, em que itens de lista interativos na janela Criar pop-up usavam funções ARIA incorretas. Elementos que se comportavam como links receberam `role="listitem"` em vez de `role="menuitem"`, violando padrões de design ARIA e leitores de tela confusos. As atualizações garantem que todos os componentes da lista sigam as funções semânticas apropriadas para um melhor suporte à tecnologia de assistência e teclado. (SITES-24493)
* Correção de um problema de associação de rótulo de acessibilidade para os campos de título de página e tags. Agora, a interface do AEM associa corretamente os rótulos de acessibilidade aos campos &quot;Título&quot; e &quot;Título da página&quot; ao usar leitores de tela como JAWS. A correção garante a leitura adequada do rótulo e melhora a conformidade com a ADA na criação de páginas, propriedades e fluxos de trabalho de movimentação. (SITES-27149)
* Correção de um problema de acessibilidade com a identificação da tabela na caixa de diálogo de permissões. A tabela de permissões no AEM agora usa funções e atributos ARIA corretos para garantir que leitores de tela como o JAWS a identifiquem corretamente como uma tabela. A correção melhora a conformidade de acessibilidade e garante que os usuários recebam navegação precisa e anúncios de conteúdo. (SITES-27140)
* Corrigido o rótulo visual ausente para campos de entrada de comentários na linha do tempo. Correção da falta de rótulos visuais para os campos de entrada &quot;comentário&quot; na seção de linha do tempo para melhorar a acessibilidade. A atualização garante que os leitores de tela possam anunciar com precisão os rótulos de campo. Essa experiência melhora a navegação e o envio de formulários para todos os usuários, especialmente aqueles que dependem de tecnologias assistivas. (SITES-26903)
* Correção da acessibilidade do teclado para o botão de reticências nos comentários da linha do tempo. Ativação da navegação pelo teclado para o botão de reticências (três pontos) ao lado dos comentários na seção Linha do tempo. Agora os usuários podem acessar e interagir com o botão usando a tecla de guia, melhorando a acessibilidade para usuários que dependem da navegação somente pelo teclado. (SITES-26891)
* Anúncios de NVDA/Narrador aprimorados para resultados de pesquisa em caixas de diálogo de seleção. Atualização da caixa de diálogo Abrir seleção para anunciar se os resultados da pesquisa são encontrados ou não ao usar leitores de tela, como NVDA ou Narrador. Essa melhoria ajuda os usuários que dependem de tecnologias assistivas a entender o resultado de suas ações de pesquisa sem precisar de confirmação visual. (SITES-26883)
* Função ARIA corrigida para o ícone de reticências ao lado do campo de entrada de comentário. Atualização do ícone de reticências (três pontos) ao lado do campo de entrada de comentário para usar a função ARIA correta, garantindo que os leitores de tela possam identificar com precisão o elemento. Essa melhoria melhora a conformidade de acessibilidade e melhora a experiência para usuários que dependem de tecnologias assistivas. (SITES-26881)
* Correção de atributos ARIA inválidos em componentes da interface do usuário Coral. Atualização dos componentes da interface do Coral para garantir que todos os atributos ARIA usem valores válidos, melhorando a conformidade com a acessibilidade. Especificamente, foram solucionados casos em que valores inválidos como `aria-modal="dialog"` eram atribuídos incorretamente. Esse aprimoramento permite que os leitores de tela interpretem os elementos da caixa de diálogo corretamente, melhorando a acessibilidade para usuários que dependem de tecnologias assistivas. (SITES-26873)
* Visibilidade e dicas de ferramentas aprimoradas para ícones em cenários de Refluxo. O comportamento Reflow foi aprimorado para garantir que as dicas de ferramentas sejam exibidas corretamente para os ícones **Download**, **Reprocessar ativos** e **Check-out**. Foco em um problema de acessibilidade em que os ícones e seus rótulos se tornaram invisíveis quando a janela de visualização foi redimensionada ou as configurações de zoom do navegador foram alteradas. Essa correção oferece suporte a usuários com pouca visão, mantendo a visibilidade e fornecendo descrições apropriadas dos ícones durante o Refluxo. (SITES-26871)

#### Interface do usuário do administrador{#sites-adminui-6523}

Correção da exceção do Serviço de URL do Editor Universal com pontos de extremidade Externalizer ausentes. O Serviço de URL do Editor Universal agora lida com pontos de extremidade ausentes do autor, publicação ou Externalizador local sem lançar exceções. Os usuários administradores podem abrir o Editor de páginas com êxito mesmo quando algumas configurações do Externalizador estão incompletas. (SITES-28877) <!-- LTS -->

#### IU Clássica{#sites-classicui-6523}

* Um problema nas caixas de diálogo da interface clássica em que alternar um botão ocultava uma área de texto e não exibia novamente em cliques subsequentes. A correção garante que a área de texto reapareça corretamente quando alternada, restaurando o comportamento esperado e evitando interrupções nos workflows dinâmicos da caixa de diálogo. (SITES-30230)
* Corrigida a funcionalidade do localizador de ativos de imagem da interface clássica corrompida após a atualização do Service Pack 22. O localizador de ativos de imagem da interface clássica agora lida corretamente com nomes de ativos que contêm espaços ou caracteres especiais. Essa atualização garante que o localizador de ativos codifique os nomes de arquivo corretamente, evitando falhas de pesquisa e permitindo que os autores localizem e selecionem ativos de imagem sem erros. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Correção de falha no teste de validação para `DeleteVariationIT.testUpdateBasic`. O teste `DeleteVariationIT.testUpdateBasic` não falha mais durante a execução da validação do Service Pack. A correção corrige um problema de mapeamento de texto ausente na lógica de manipulação de JSON, garantindo a estabilidade do teste e evitando interrupções desnecessárias do teste. (SITES-28022)
* O AEM agora impede a degradação do desempenho causada por metadados malformados do XMP em ativos de imagem. O Assets que contém nomes de propriedade XMP inválidos ou não compatíveis, como aqueles com segmentos numéricos ou estruturas não qualificadas, não aciona mais logs de aviso repetidos durante o processamento. O sistema filtra metadados problemáticos para garantir que a assimilação e a validação de ativos estejam completas sem erros. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - Editor de fragmentos{#sites-fragments-editor-6523}

Outros autores ainda podem publicar fragmentos de conteúdo mesmo quando outro autor faz o check-out, o que é contrário ao comportamento pretendido do recurso de check-out. Essa correção impede que outros usuários vejam ou usem os botões de publicação na interface de criação quando é feito o check-out de um fragmento de conteúdo. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6523}

Correção de GraphQL QueryValidationError com esquemas de Fragmento de conteúdo. A atualização do pacote `cq-dam-cfm-graphql` corrige erros de validação de esquema ao usar referências de Fragmento de conteúdo. A correção garante que as consultas do GraphQL funcionem corretamente sem exigir realinhamento manual do esquema ou republicação após as implantações do pacote. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Console de componentes{#sites-component-console-6523}

Melhorias no carregamento da página &quot;Uso de componentes em tempo real&quot;. Otimiza a página &quot;Componentes em tempo real de uso&quot; no AEM para impedir que linhas vazias apareçam ao percorrer grandes conjuntos de dados. Os usuários que carregam componentes com extensas referências de uso agora podem experimentar carregamento de dados contínuo sem lacunas desnecessárias ou entradas vazias. Essa experiência melhora a navegação da página, a precisão do rastreamento e a eficiência do gerenciamento nos relatórios de uso do componente. (SITES-26454)

#### Infraestrutura principal{#sites-core-backend-6523}

* Correção de uma falha na listagem de ativos do Localizador de conteúdo causada por nomes de ativos inválidos. O Localizador de conteúdo agora lida corretamente com nomes de ativos com caracteres não codificáveis. A listagem de ativos no Editor de páginas não falha mais ou lança exceções ao encontrar ativos com nomes problemáticos. (SITES-28722)
* Um problema em que o componente `SearchPathLimiter` gerou entradas de log em excesso imprimindo mensagens no nível ERROR para cada invocação. Esse comportamento começou após o Service Pack 17 e levou a preocupações de desempenho devido a volumes de log extremamente altos. A correção reduz o nível de log para DEBUG, reduzindo significativamente o ruído do log e melhorando a eficiência do monitoramento e do diagnóstico do sistema. (SITES-29835)
* Metadados XMP formatados incorretamente dispararam um erro durante o processamento de ativos de imagem no `ValidationDataServlet`. A correção garante a conformidade do manuseio de metadados e evita a análise redundante de propriedades inválidas. (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lançamentos{#sites-launches-6523}

* Correção de uma exibição incorreta da data de lançamento entre 25 e 31 de dezembro. A interface do usuário de Inicializações agora exibe datas entre 25 de dezembro e 31 de dezembro com o ano correto. A correção garante que as datas não mostrem mais incorretamente o ano seguinte, evitando confusão durante o planejamento e o agendamento da campanha. (SITES-28706)
* Correção de modelos AEM Launch corrompidos após a atualização do Service Pack 22. Os modelos do AEM Launch agora são carregados corretamente após uma atualização do Service Pack 22. A correção corrige dados inválidos nas configurações internas do Launch, permitindo que os usuários visualizem, editem e criem Lançamentos sem erros ou campos ausentes. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Editor de página{#sites-pageeditor-6523}

* Correção do problema de carregamento do AssetPicker nas resoluções de tela inferiores. O AssetPicker agora carrega ativos corretamente quando os usuários rolam por resoluções de tela mais baixas (1728×1117 ou menores). Os usuários não experimentam mais ativos ausentes durante a rolagem, melhorando o gerenciamento de ativos em diferentes pontos de interrupção de dispositivos. (SITES-28065)
* Correção de um anúncio de leitor de tela ausente para ações de bloqueio e desbloqueio de página. O Editor de páginas agora anuncia a mensagem &quot;Informações: a página foi bloqueada/desbloqueada&quot; corretamente quando os usuários ativam o botão bloquear/desbloquear. A correção melhora a conformidade com a acessibilidade e garante que os usuários de leitores de tela recebam atualizações dinâmicas durante a edição da página. (SITES-27143)
* Comportamento do foco do teclado aprimorado para ações de componentes na criação de AEM. Navegação aprimorada do teclado na ferramenta Autor do AEM para garantir que o foco permaneça no componente recém-criado ou selecionado após ações como Configurar, Excluir ou Converter. Anteriormente, o foco era deslocado para a parte superior da página, causando problemas de conformidade de acessibilidade. Essa atualização melhora a experiência do usuário para usuários de teclado e de tecnologia assistiva. Ela faz isso mantendo a progressão lógica do foco no fluxo de trabalho de edição. (SITES-26549)
* Navegação de guias aprimorada nas caixas de diálogo do Autor. Melhora a navegação do teclado nas caixas de diálogo do Autor do AEM, permitindo que os usuários continuem avançando depois de atingir a caixa de edição Descrição. Anteriormente, o trapping de foco no campo Descrição bloqueava mais navegação sem usar combinações de teclas especiais. A atualização garante que os usuários possam percorrer os campos facilmente usando apenas a tecla Tab, melhorando a conformidade de acessibilidade e a experiência do usuário. (SITES-26524)
* Uma regressão foi introduzida no AEM 6.5 Service Pack 22 que impedia que os usuários incluíssem espaços nos títulos do Launch. A correção restaura a capacidade de usar espaços, permitindo que as equipes definam e organizem nomes do Launch de forma mais flexível, em conformidade com o comportamento esperado. (SITES-29414)
* Correção de um problema de redimensionamento para componentes dentro de Contêineres de layout após ocultar/reexibir ações. O Editor de páginas agora calcula corretamente os valores da coluna depois de ocultar e reexibir um Contêiner de layout. Os usuários podem redimensionar componentes sem erros, e as colunas são exibidas corretamente durante as ações de redimensionamento. (SITES-28463)
* Correção do deslocamento incorreto do botão Árvore de conteúdo no Editor de páginas. Agora, o Editor de páginas posiciona corretamente o botão de configuração da Árvore de conteúdo na caixa de diálogo &quot;Teaser principal&quot; pretendida, em vez da seção errada. A correção atualiza o CSS da caixa de diálogo Árvore de Conteúdo para usar `top:0` em vez de `bottom:0`, garantindo o posicionamento adequado do botão. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Editor de rich text{#sites-rte-6523}

Corrigir marcas inesperadas `<br>` no Editor de Rich Text com modo de colagem de texto sem formatação. O Editor de Rich Text agora manipula corretamente as operações de cortar e colar ao usar texto simples `defaultPasteMode`. A correção impede a inserção de tags `<br>` inesperadas quando os usuários recortam e colam texto dentro de campos RTE, garantindo uma formatação limpa durante a edição de conteúdo. (SITES-27780)

#### Editor universal {#sites-universal-editor-6523}

* Quando várias solicitações contendo o parâmetro de consulta são enviadas para o AEM, o cookie de token de logon pode não ser retornado a tempo, o que pode resultar em falha de logon. (SITES-30659) <!-- LTS -->
* Para garantir compatibilidade e suporte com manipuladores SAML, você deve configurar a propriedade `service.ranking` para que o manipulador `Query Token Auth` execute *antes* do manipulador `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Os seguintes problemas ocorrem na página Navegação no Local [!DNL AEM] (6.5.22.0) depois de selecionar ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets ]**, navegar até a pasta**[!UICONTROL  Pesquisar Adobe Stock ]**e selecionar uma imagem de estoque:
   * A imagem de estoque selecionada não pode ser licenciada e salva porque clicar em **[!UICONTROL Licenciar e salvar]** exibe uma lista suspensa vazia.
   * Selecionar a imagem do Stock ou inserir novamente a URL da página de estoque redireciona para a página inicial [!DNL AEM], impedindo o acesso à imagem do Adobe Stock. (ASSETS-48687)
* Problemas ao gerenciar pastas se o nome da pasta incluir um `/` em seu nome na página de Navegação no Local [!DNL AEM] (6.5.22.0). (ASSETS-46740)
* Em [!DNL AEM] 6.5, a página de detalhes do ativo não é carregada da exibição ![Coleção](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Coleções ]**devido ao alto uso de memória. (ASSETS-46738)
* Problemas de integração com o serviço [!DNL InDesign] as `Day CQ DAM Mime Type OSGI` identificam incorretamente [!DNL InDesign] arquivos como `x-adobe-indesign` em vez de `x-indesign`. (ASSETS-45953)
* Vazamento de sessão [!DNL AEM 6.5.21] rastreado até a etapa de fluxo de trabalho predefinida **[!UICONTROL Publicação agendada no Brand Portal]**. (ASSETS-44104)
* **[!UICONTROL Erros de Falta de Memória (OOM)]** são exibidos em [!DNL AEM] ao processar e publicar imagens. Esse problema ocorreu devido a métodos obsoletos em fluxos de trabalho, como **[!DNL Dam Asset update]** e **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Depois de fazer uma pequena alteração, como atualizar o título, você reabre e salva novamente o **[!DNL Connected Assets configuration]** na instância do Sites local. A instância remota perde a conexão com a instância local. Como resultado, não é possível estabelecer comunicação com a instância local do Sites. (ASSETS-44484)
* Em [!DNL AEM 6.5.21], quando um carregamento de ativo na exibição de lista é cancelado e um segundo carregamento é executado, [!DNL AEM] exibe um erro **[!UICONTROL 0 de NaN ativos carregados]**. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

Adição de uma propriedade de metadados (`jcr:content/metadata/dam:scene7SmartCropStatus`) aos ativos para identificar gerações de Recorte inteligente com falha. Permite pesquisa, filtragem e reprocessamento eficientes de ativos com problemas de Recorte inteligente por meio de fluxos de trabalho manuais ou automatizados. (ASSETS-46237)

#### [!DNL Dynamic Media] - Modo Híbrido {#assets-dm-hybrid-6523}

##### Dynamic Media - Pacote complementar híbrido (AEM 6.5.23 e posterior)

A partir do AEM 6.5 Service Pack 23, um novo pacote complementar está disponível para Dynamic Media - Modo híbrido. Este pacote inclui o pacote `cq-scene7-imaging` especificamente compatível com o modo de execução Dynamic Media - Híbrido.

**Correção de chave incluída**

Correção de um problema no Dynamic Media - Implantações híbridas em que as atualizações do parâmetro `catalog.expiration` em `/conf/global/settings/dam/dm/imageserver` não eram refletidas nas URLs do servidor ou do autor, apesar da replicação ser bem-sucedida sem erros. A atualização garante valores de expiração consistentes entre o CRX/DE, a resposta do servidor e os URLs de entrega pública. Por sua vez, melhora o comportamento do cache e a confiabilidade das transformações de imagem. (ASSETS-44837)

**Considerações importantes**

* O conjunto `cq-scene7-imaging` na instalação base do AEM 6.5.23 (e posterior) é *não compatível* com o Dynamic Media - modo de execução híbrido.
* A instalação do Service Pack 23 (e posterior) sozinha *não atualiza automaticamente* o pacote `cq-scene7-imaging` existente nas instâncias do AEM configuradas para Dynamic Media - Híbrido (modo de execução `-r dynamicmedia`).

**Quando instalar o pacote complementar Híbrido**

* Ao atualizar diretamente para o AEM 6.5.23 (e posterior) do AEM 6.5.19 ou anterior.
* Quando precisar de correções específicas para o Dynamic Media - funcionalidade híbrida.
* Ao implantar uma nova instância do Dynamic Media - Hybrid diretamente do AEM 6.5 GA (Disponibilidade geral) para o Service Pack 23 (e posterior).

**Baixar pacote complementar híbrido**

O pacote complementar Híbrido está disponível publicamente na Distribuição de software da Adobe a partir de quinta-feira, 22 de maio de 2025, com o lançamento oficial do AEM 6.5.23. Os usuários podem encontrá-lo pesquisando pelo **Pacote Complementar Híbrido do Dynamic Media do AEM 6.5** na Distribuição do Software.


### [!DNL Forms]{#forms-6523}

#### Designer do Forms

* Quando um usuário exporta os dados de uma PDF baseada em XFA usando a exportDataAPI, o XML resultante mostra discrepâncias quando comparado aos dados XML exportados manualmente usando o Acrobat Reader. Valores de alguns campos estavam ausentes na saída em comparação à saída gerada pelo Acrobat Reader. (LC-3922791)

* No AEM Forms 6.5.22.0, gerar uma PDF marcada com o Serviço de Saída no Workbench adiciona uma marca de rótulo inesperada sob a marca de referência em um item de índice. (LC-3922756)

* Quando um usuário coloca legendas de campo com alinhamento inferior ou direito no AEM Forms Designer, a árvore de tags inclui somente a legenda sem o valor correspondente, resultando em marcação de acessibilidade incompleta. (LC-3922619)

* Ao atualizar do AEM Forms 6.5 Service Pack 6 para o AEM Forms Service Pack 20, os códigos QR em PDFs gerados tornam-se ilegíveis. O texto alternativo para os códigos QR também falha no teste de acessibilidade, afetando a compatibilidade do leitor de tela. (LC-3922551)

* Quando um usuário renderiza uma correspondência na interface do usuário do agente no AEM Forms Service Pack 18, o conteúdo não é exibido corretamente devido à API FormService.render(). (LC-3922461)

#### Forms

* No AEM Forms, ativar a opção &quot;Permitir rich text para título&quot; no painel raiz faz com que a opção &quot;Excluir título do documento de registro&quot; em um painel aninhado oculte incorretamente o título do painel raiz. Isso é feito no documento de registro gerado. (FORMS-19696)

* O sistema ignora o `sling:resourceType` personalizado atribuído por meio de `aem:afProperties` em um esquema JSON no AEM 6.5. O tipo de recurso personalizado é ignorado durante a renderização. (FORMS-19691)

* Quando um usuário envia um Formulário adaptável com anexos pré-preenchidos usando URIs, o envio do formulário falha com uma NullPointerException devido à ausência de dados binários. (FORMS-19371) (FORMS-19486)

* Quando um usuário carrega uma PDF na seção &quot;Forms e documentos&quot; no AEM 6.5 Forms, o recurso de linha do tempo para de funcionar. (FORMS-19407)(FORMS-19234)

* Quando um usuário faz upload de arquivos usando o componente de anexo de arquivo pronto para uso (OOTB) no AEM Forms, as vulnerabilidades de segurança são identificadas. Este problema pode levar à intercepção potencial do processo de envio por entidades não autorizadas. (FORMS-19271)

* Quando um usuário configura um Formulário adaptável pronto para uso no AEM Forms para gerar um Documento de registro (DoR) automaticamente, o campo &quot;Título&quot; nas Propriedades de documento do Acrobat Reader não exibe o título do Documento capturado. Por padrão, o título do formulário não é exibido no lugar do nome do arquivo. (FORMS-19263)

* Quando um usuário abre uma Comunicação interativa na interface do usuário do agente, os dados preenchidos previamente não podem ser completamente apagados; após a remoção, eles são automaticamente preenchidos com os mesmos dados. (FORMS-19151)

* Quando um usuário pré-visualiza um campo de data na interface do usuário do agente, a data é alterada inesperadamente. Esse problema ocorre devido a discrepâncias de fuso horário entre a configuração UTC da VM e a interpretação da data pelo sistema. (FORMS-19115)

* Quando um usuário envia um formulário, os anexos de arquivo podem ser duplicados, resultando em vários uploads do mesmo arquivo. (FORMS-19045)(FORMS-19051)

* A adição de coordenadores a conjuntos de políticas na Segurança de documentos do AEM 6.5 falha em ambientes de produção e inferiores. (FORMS FORMS-18603, FORMS-18212, 19697)

* Quando um usuário clica no &quot;datepicker-calendar-icon&quot; no modo de desktop com um campo vazio no AEM Forms Service Pack 22, ocorre um erro devido à variável _$focusDate indefinida, interrompendo os scripts personalizados associados. (FORMS-18483)(FORMS-18268)

* No AEM Forms Service Pack 19 (6.5.19.0), quando um cliente visualiza uma correspondência, o campo &quot;Valor em palavras&quot; não exibe ou atualiza os valores numéricos corretamente, resultando em alinhamento incorreto e espaços ausentes no conteúdo. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004)

* Quando um cliente visualiza uma carta salva no AEM Forms 6.5 SP19 no RHEL, o conteúdo fica desalinhado, espaços são perdidos e caracteres inesperados como &quot;x&quot; são exibidos. (FORMS-18422)(FORMS-17641)

* Quando um usuário navega entre guias no AEM Forms, selecionar componentes na primeira guia deixa de responder. (FORMS-18345)

* No AEM Forms 6.5.21.0, quando um usuário converte um arquivo HTML em PDF usando a opção WebToPDF, o PDF de saída não tem a seção de cabeçalho, incluindo marcas de metadados e título. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)

* No SDK do AEM JEE Process Manager, quando um usuário chama o método retryAction(long actionOid), o sistema tenta novamente incorretamente a primeira ação encontrada na tabela tb_action_instance. Esse fluxo de trabalho ocorre mesmo quando uma ID de ação específica é fornecida ou quando a ID é nula, resultando em comportamento não intencional. (FORMS-18187)

* Depois de atualizar para o SP22, um usuário encontra problemas em que as funcionalidades de rascunho e envio salvas falham sem exibir nenhuma mensagem de erro. (FORMS-18069)

* No AEM 6.5.21.0, a transição de componentes de base baseados em XSD para componentes principais impede a implementação de referências entre arquivos em esquemas JSON, afetando a migração Adaptive Forms. (FORMS-18065)

* Quando um usuário pré-visualiza uma correspondência na interface do usuário do agente, o campo de data mostra um valor incorreto devido a problemas de conversão de tempo da IC. Essas discrepâncias surgem das diferenças de fuso horário entre o ambiente da VM e a interpretação de hora do sistema (UTC versus hora local). (FORMS-17988) (FORMS-17248)

* Quando um usuário pré-visualiza cartas usando modelos de Aviso IC no AEM Forms, os tempos de geração do PDF variam significativamente, de 1,5 segundos a mais de 10 segundos, mesmo no mesmo servidor. Essa inconsistência afeta os workflows críticos para os negócios. (FORMS-17951)

* Quando um usuário vincula um objeto de assinatura escritas em um formulário adaptável a um XDP usando a opção &quot;Fontes de dados&quot;, as alterações não podem ser salvas. O motivo é devido a erros persistentes de validação na taxa de proporção, mesmo ao usar valores válidos. (FORMS-17587)

* Quando um usuário usa um XDP específico com muitos campos ocultos para fragmentos de documento, o AEM cria nós do CRX com a propriedade `cm:optional` definida como false, o que causa falha no envio da IC (Comunicação interativa). (FORMS-17538)

* No AEM Forms 6.5.19.0, quando um cliente pré-visualiza uma correspondência, o campo da caixa numérica falha ao tratar corretamente os valores negativos quando os limites de dígitos para Lead e Frac são definidos. Esse problema ocorre devido ao uso de parseFloat, que trata o sinal de menos como parte do número. (FORMS-17451)

* No AEM Forms 6.5, quando uma correspondência é visualizada, o uso do curinga &quot;*&quot; no arquivo Adobe.json é notado, gerando preocupação sobre sua finalidade e possível modificação. (FORMS-17317)

* Quando um usuário usa um leitor de tela no `Apply for a Fixed Rate Saver joint account`, os cabeçalhos são anunciados incorretamente como `clickable`, causando problemas de acessibilidade. (FORMS-17038)

* Quando um formulário é incorporado, o iframe gerado não tem um atributo de título, resultando em um problema de conformidade de acessibilidade. (FORMS-17010)

* Baixar um formulário usando a interface do usuário do Forms Manager sempre inclui dependências associadas, como temas e fragmentos. (FORMS-15811)

* Quando um usuário acessa o formulário em dispositivos móveis (iOS e Android™), os botões &quot;próximo&quot; e &quot;anterior&quot; na primeira página são desativados. No entanto, o leitor de tela não as identifica como desativadas. (FORMS-15773)

* Quando um usuário salva um formulário grande com fragmentos e carregamento lento ativado, ele não recupera rascunhos, interrompendo o fluxo de trabalho. (FORMS-19890, FORMS-19808)

#### FORMS JEE

* Quando um usuário reconfigura o banco de dados no AEM Forms, a conexão falha devido a parâmetros codificados. (FORMS-19568, FORMS-17621)

* Quando um usuário configura o AEM 6.5 com o MySQL 8.4 usando o método turnkey parcial, o LiveCycle Configuration Manager (LCM) não reconhece o driver de conector MySQL necessário. Isso causa falha no teste e na configuração da conexão do banco de dados. (FORMS-19442)

* Quando um usuário executa o LCM com JDBC 12.8.1 no JRE 11 em um ambiente JEE, a configuração falha devido a problemas de incompatibilidade. (FORMS-19276)

* Quando um usuário abre uma tarefa no AEM no local, o sistema executa o Perfil de ação de início do Workspace em vez do Perfil de usuário atribuído. (FORMS-19065)

* Quando um usuário usa o método retryAction(long actionOid) no AEM JEE Process Manager, ocorre um comportamento inesperado. (FORMS-18357)(FORMS-18187)

* No AEM Forms 6.5.21.0, a conversão PDFG falha com o seguinte erro: (FORMS-16851)(FORMS-14613)

#### Forms Captcha {#forms-captcha-6523}

* Melhoria no alerta do reCAPTCHA no Adaptive Forms ao atualizar códigos de erro de envio para 400. Além disso, alertas de registro refinados para distinguir entre tempos limite, expirações e falhas de detecção de bot, melhorando a precisão da solução de problemas e a observação do sistema. (FORMS-19240)
* Fechou uma instância `ResourceResolver` não fechada em `ReCaptchaConfigurationServiceImpl` para evitar possíveis vazamentos de recursos e melhorar a estabilidade do sistema ao usar integrações reCAPTCHA no AEM Forms. (FORMS-19242)
* Manuseio de configuração de CAPTCHA aprimorado para o AEM Forms, garantindo as associações de configuração corretas para cada formulário quando houver várias entradas na pasta `/conf/global`. Impede o uso não intencional de configurações incorretas de CAPTCHA quando o contêiner de configuração não está explicitamente selecionado. (FORMS-19239)

<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### Foundation {#foundation-6523}

* Correção de um problema nos Banners de alerta Coral em que a cor do texto aparecia branca em vez de preta após a atualização para o Service Pack 21. Garante que o estilo correto seja aplicado para manter o contraste adequado e a legibilidade das mensagens de alerta na interface. (NPR-42359)
* Adição de suporte para integração OAuth na configuração de Tags inteligentes para alinhar-se à desativação do JWT (JSON Web Token). Garante a funcionalidade contínua dos recursos de Tags inteligentes usando métodos de autenticação atualizados. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Correção de uma NullPointerException que ocorria ao carregar arquivos de chave privada em um campo de propriedade do tipo binário no CRX, restaurando a compatibilidade presente pelo Service Pack 16. Habilita workflows de upload de arquivo principal seguro no AEM Managed Services sem erros de servidor ou interrupção nos processos de renovação do certificado. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* Correção de ciclos de dependência OSGi entre os serviços de script do Apache Sling que causavam atrasos ou falhas ao carregar páginas do HTML após a atualização para o Service Pack 21. Atualização das referências de serviço internas para eliminar dependências cíclicas envolvendo `SightlyScriptingEngineFactory` e componentes relacionados, melhorando a confiabilidade e o comportamento de inicialização do mecanismo de script. (GRANITE-56808)
* Atualização do JS Use scripts no Apache Sling para carregar somente sob demanda, em vez de imediatamente na inicialização, eliminando a contenção de thread e reduzindo o risco de os servidores de publicação ficarem sem resposta quando carregados. Essa alteração melhora a estabilidade do servidor e os tempos de resposta durante cenários de alto tráfego, evitando o bloqueio de recursos causado pela resolução antecipada de scripts. (GRANITE-56611)
* Correção de um problema no AEM Omnisearch onde espaços reservados para campos de entrada são exibidos incorretamente como rótulos, resultando em confusão visual. Garante a renderização adequada de espaços reservados em campos de filtro, mantendo um comportamento de formulário consistente e acessível. (GRANITE-51791)
* Correção de um erro de servidor acionado ao selecionar mais de 30 CFMs (modelos de fragmento de conteúdo) com referências de vários campos no editor de modelo de Fragmento de conteúdo. O componente de sugestão de filtro foi aprimorado para oferecer suporte a operações POST. Essa capacidade permite o manuseio adequado de grandes conjuntos de referência durante a criação de fragmentos de conteúdo e melhora a estabilidade para configurações de modelo de alto volume. (GRANITE-57164)
* Solução de um problema nos CFMs em que clicar em Fechar para uma caixa de seleção alterava seu estado involuntariamente. Estilos atualizados para restringir a ativação de cliques estritamente ao elemento de caixa de seleção, evitando interações acidentais do usuário e melhorando a usabilidade e a acessibilidade do formulário. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Solução de um problema em que a validação SNI bloqueava chamadas de API por HTTPS para clientes do AEM que usavam configurações SSL do Dispatcher com cabeçalhos de host personalizados. Introduz uma opção para desabilitar a validação de SNI como parte da configuração do Jetty, habilitando a compatibilidade com configurações específicas de proxy reverso onde `mod_proxy` não é viável. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Platform{#foundation-platform-6523}

* Correção de um comportamento inconsistente de mesclagem de tags, garantindo que o valor da tag mesclada sempre fosse exibido corretamente nos ativos, independentemente de as tags serem criadas em linha ou pelo método de criação de tag padrão. Impede que valores residuais de `EN:title` campos substituam a exibição de marca mesclada. (CQ-4358812)
* Correção da codificação repetida de caracteres de E comercial em valores de tag na caixa de diálogo de edição de tag. Evita que entidades &quot;&amp;&quot; extras sejam anexadas a cada salvamento, garantindo que os valores de tag permaneçam limpos e consistentes em todas as edições e evitando erros de exibição no conteúdo criado. (CQ-4359048)
* Correção de um erro `ClassCastException` que impede a entrega de emails no envio do Formulário adaptável no AEM 6.5 em execução no WebSphere®. A correção permite a transmissão de email com êxito, garantindo a compatibilidade entre `com.sun.mail.handlers.text_plain` e `java.activation.DataContentHandler`, alinhando com a configuração do manipulador de email esperada pelos ambientes do WebSphere®. (NPR-42500)
* Tratamento de erros aprimorado no Gerenciador de pacotes, garantindo que o AEM exiba uma mensagem clara quando a instalação falhar e a resposta do erro estiver vazia. Essa correção evita falhas silenciosas e auxilia na depuração mais rápida durante a implantação de pacotes. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Tradução{#foundation-translation-6523}

Correção de um problema de NullPointerException (NPE) acionado ao atualizar Fragmentos de conteúdo em fluxos de trabalho usando **Atualizar Cópia de Idioma**. Essa correção garante que os workflows não entrem em um estado de falha ou permaneçam presos em um estado de execução ao editar o conteúdo vinculado às referências de tradução. (NPR-42115)

#### Interface do usuário{#foundation-ui-6523}

Adiciona os atributos `title` ausentes aos botões da caixa de diálogo Coral UI, como **Concluído** e **Cancelar** nas caixas de diálogo de edição de componentes para melhorar a acessibilidade e habilitar a validação automatizada. Garante que os botões retenham os atributos esperados na renderização de marcação, evitando falhas nos testes de interface do usuário com base no Selenium. (NPR-42412)

#### WCM{#foundation-wcm-6523}

Correção de um problema que impedia a adição de páginas a trabalhos de tradução ao usar a **Atualização de Cópia de Idioma** em ambientes com o Service Pack 19 ou posterior. Garante que os fluxos de trabalho de tradução continuem conforme o esperado, permitindo a transferência adequada de página entre cópias de idioma sem intervenção manual. (CQ-4357929)

#### Fluxo de trabalho{#foundation-workflow-6523}

Solução de um problema no `EmailNotificationServiceProcessor` em que o método `getSegmentId` retornava `null` após a implantação de hotfix, causando falha nos acionadores de email durante o processamento do fluxo de trabalho. Restaura a lógica correta de resolução de ID de segmento, garantindo que o processador recupere os `SegmentInfo` valores necessários para suportar fluxos de trabalho de notificação por email em instâncias do AEM. (CQ-4359755)


## Instalar [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 requer [!DNL Experience Manager] 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível na [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) da Adobe.
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.23.0 em uma das instâncias do Autor usando o Gerenciador de Pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> A Adobe não recomenda que você remova ou desinstale o pacote [!DNL Experience Manager] 6.5.23.0. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository`, caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].

1. Baixe o Service Sack de [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Repositório de Dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes sai durante a instalação do Service Pack. A Adobe recomenda aguardar a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no navegador do [!DNL Safari], mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.23.0 não oferece suporte à instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (6.5.23.0)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi estão **[!UICONTROL ATIVOS]** ou **[!UICONTROL FRAGMENTOS]** no Console OSGi (Use o Console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.20 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para o Forms [!DNL Experience Manager]{#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o Service Pack no Experience Manager Forms, consulte [instruções de instalação do Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>O recurso de formulários adaptáveis, disponível no [Início rápido do AEM 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager{#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [Fragmento de conteúdo do Experience Manager com o pacote de índice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam.

A falha na instalação deste pacote pode resultar em consultas lentas ou com falha do GraphQL.

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar{#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.23.0 está disponível no [repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal foi renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como valor, para a tag `dependency`.



## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md/) para obter uma lista detalhada de todos os recursos obsoletos ou removidos do AEM 6.5.

### Editor SPA {#spa-editor}

[O Editor de SPA](/help/sites-developing/spa-overview.md) foi descontinuado para novos projetos a partir da versão 6.5.23 do AEM 6.5. O Editor SPA permanece compatível com projetos existentes, mas não deve ser usado para novos projetos.

Os editores preferidos para gerenciar conteúdo headless no AEM agora são:

* [O Editor Universal](/help/sites-developing/universal-editor/introduction.md) para edição visual.
* [O Editor de Fragmento de Conteúdo](/help/sites-developing/universal-editor/introduction.md) para edição baseada em formulário.

## Problemas conhecidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problema com o pacote de scripts JSP no AEM 6.5.21-6.5.23 e AEM 6.5 LTS GA**
AEM 6.5.21, 6.5.22, 6.5.23 e AEM 6.5 LTS GA são fornecidos com o pacote `org.apache.sling.scripting.jsp:2.6.0`, que contém um problema conhecido. O problema normalmente ocorre em carga alta quando a instância do AEM lida com muitas solicitações simultâneas.

  Quando esse problema ocorrer, uma das seguintes exceções poderá aparecer nos logs de erros junto com referências a `org.apache.sling.scripting.jsp:2.6.0`:

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Quando esse erro ocorre, o único método de recuperação é reiniciar a instância do AEM.

  Entre em contato com o Suporte ao cliente da Adobe e consulte esta nota de versão para obter uma resolução.

* **Relacionado ao Oak**
A partir do Service Pack 13 e superior, o seguinte log de erros começou a aparecer, afetando o cache de persistência:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Para resolver essa exceção, faça o seguinte:

   1. Excluir as duas pastas a seguir de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale o Service Pack ou reinicie o Experience Manager as a Cloud Service.
Novas pastas de `cache` e `diff-cache` são criadas automaticamente e você não tem mais uma exceção relacionada a `mvstore` em `error.log`.

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Uma consulta GraphQL pode usar o índice `damAssetLucene` em vez do índice `fragments`. Essa ação pode resultar em consultas GraphQL que falham ou demorar muito para ser executada.

  Para corrigir o problema, `damAssetLucene` deve ser configurado para incluir as duas propriedades a seguir em `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Após alterar a definição do índice, é necessária uma reindexação (`reindex` = `true`).

  Após essas etapas, as consultas do GraphQL devem ser executadas mais rapidamente.

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas. Falha na consulta em segundo plano. Ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se você atualizar sua instância do [!DNL Experience Manager] de 6.5.0 para 6.5.4 para o Service Pack mais recente no Java™ 11, verá `RRD4JReporter` exceções no arquivo `error.log`. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia no [!DNL Assets] e publicar uma pasta aninhada no [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : Nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão da alteração de registro não registrada.

* A partir do AEM 6.5.15, o Mecanismo Rhino JavaScript fornecido pelo pacote ```org.apache.servicemix.bundles.rhino``` tem um novo comportamento de elevação. Os scripts que usam o modo estrito (```use strict;```) devem declarar suas variáveis corretas. Caso contrário, eles não serão executados e acabarão gerando um erro de tempo de execução.

* A instalação de marcação relacionada ao conteúdo pronto para uso por meio de um pacote de atualização oficial redefine a propriedade languages do nó `/content/cq:tags` para o padrão. Essa ação é verdadeira para Service Packs, Service Packs de segurança, Pacotes de recursos estendidos, Pacotes de recursos cumulativos, patches e assim por diante. Portanto, é necessário adicioná-lo das propriedades antes da instalação.

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6523}

A visualização dos fragmentos de conteúdo falha devido à proteção do DoS para uma grande árvore de fragmentos. Consulte o artigo [KB sobre as opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6523}

>[!NOTE]
>
> Não atualize para o Service Pack 6.5.23.0 devido a problemas que não têm hotfixes disponíveis, pois isso pode causar erros inesperados. Atualize para o Service Pack 6.5.23.0 somente após os hotfixes necessários serem lançados.

* Quando um usuário atualiza o Struts do AEM Service Pack 2.5.x para o AEM Forms Service Pack 6.x, a interface de políticas não exibe todas as configurações, como a opção de adicionar uma marca d&#39;água. Você pode [baixar e instalar o Hotfix](/help/release-notes/aem-forms-hotfix.md) para resolver o problema.  (FORMS-20203)
* Depois de atualizar para o AEM Forms Service Pack 6.5.23.0, o serviço de conversão de ImageToPDF falha com o erro (FORMS-20360):
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp``` Você pode [baixar e instalar o Hotfix](/help/release-notes/aem-forms-hotfix.md) para resolver o problema.

* Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` na pasta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), execute as seguintes etapas para resolver o problema:

   1. Pare os localizadores, se eles estiverem em execução.
   2. Pare o servidor do AEM.
   3. Vá para o `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Remova todos os arquivos de correção Geode, exceto `geode-*-1.15.1.2.jar`. Confirme se apenas os jars Geode com `version 1.15.1.2` estão presentes.
   5. Abra o prompt de comando no modo de administrador.
   6. Instale o patch Geode usando o arquivo `geode-*-1.15.1.2.jar`.

* Se um usuário tentar visualizar um rascunho de carta com dados XML salvos, ele fica preso no estado `Loading` para algumas cartas específicas. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)
* Quando os usuários atualizaram do AEM 6.5 Forms Service Pack 18 ou 19 para o Service Pack 20 ou 21, encontraram um erro de compilação JSP. Esse erro os impedia de abrir ou criar formulários adaptáveis. Isso também causava problemas com outras interfaces do AEM. Essas interfaces incluíam o Editor de páginas, a interface do AEM Forms, o editor de fluxo de trabalho e a interface da Visão geral do sistema. (FORMS-15256)

  Se você enfrentar esse problema, execute as seguintes etapas para resolvê-lo:
   1. Navegue até o diretório `/libs/fd/aemforms/install/` no CRXDE.
   2. Exclua o pacote com o nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie o servidor do AEM.

* Depois de atualizar para o AEM Forms Service Pack 20 (6.5.20.0) com o Complemento do Forms, as configurações que dependem do Adobe Analytics Cloud Service herdado usando a autenticação baseada em credencial param de funcionar. Esse problema impedia que as regras do Analytics fossem executadas corretamente. Para baixar e instalar o hotfix, consulte o artigo [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)
* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, o símbolo de moeda (como cifrão $) é exibido de forma inconsistente para todos os valores do campo. Aparece para valores até 999, mas está ausente para valores de 1000 e superiores. (FORMS-16557)
* Quaisquer modificações no XDP de fragmentos de layout aninhados em uma comunicação interativa não são refletidas no editor IC. (FORMS-16575)
* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, alguns valores calculados não são exibidos corretamente. (FORMS-16603)
* Quando a carta é exibida na Visualização de impressão, o conteúdo é alterado. Ou seja, alguns espaços desaparecem e determinadas letras são substituídas por `x`. (FORMS-15681)
* Quando um usuário configura uma instância do WebLogic 14c, o serviço PDFG no AEM Forms Service Pack 21 (6.5.21.0) no JEE executado no JBoss® falha devido a conflitos do carregador de classe envolvendo a biblioteca SLF4J. O erro é exibido da seguinte maneira (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* FORMS-20478: Ao tentar converter arquivos TIFF tipo 7/8 para o PDF, o processo de conversão falha com o erro &quot;ALC-PDG-001-000-Image2Pdf conversion failed, cause by: com/sun/image/codec/jpeg/JPEGCodec&quot; and &quot;ALC-PDG-016-003-An unknown/unexpected error occurred during PDF post-processing.&quot; O sistema tenta novamente usando o decodificador TM ImageIO TIFF, mas não conclui o trabalho. Você pode [baixar e instalar o hotfix](/help/release-notes/aem-forms-hotfix.md) para corrigir o problema.


## Pacotes OSGi e pacotes de conteúdo incluídos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de Conteúdo incluídos nesta versão do Service Pack do [!DNL Experience Manager] 6.5:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de Pacotes de Conteúdo incluídos no Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites estão disponíveis somente para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Contate o Suporte ao Cliente da Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Inscreva-se para obter atualizações de produto prioritárias da Adobe](https://www.adobe.com/subscription/priority-product-update.html)
