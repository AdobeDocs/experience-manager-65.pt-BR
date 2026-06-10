---
title: Notas de versão do  [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista de alterações detalhada para o [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: e8b2b6b52c4071aa90fddaf2cd19fec1236b8472
workflow-type: tm+mt
source-wordcount: '8148'
ht-degree: 3%

---

# Notas de Versão do Service Pack Mais Recente do [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Resumo da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do pacote de serviços |
| Data | 21 de maio de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

O Experience Manager 6.5.25.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de desempenho, estabilidade e segurança incorporadas à base 6.5, disponível desde abril de 2019.

Esta versão do service pack oferece 275 portas traseiras em Sites, Assets e Foundation, incluindo correções críticas de erros e fortalecimento da segurança. A versão também aprimora a acessibilidade na criação de sites com navegação extensa pelo teclado, gerenciamento de foco, semântica ARIA, melhorias no contraste de cores e dimensionamento do target de toque que se alinham aos padrões WCAG.

O Crosswalk está disponível por padrão nesta versão, eliminando a necessidade de um pacote ou configuração separados após a instalação.

As portas traseiras de segurança solucionam as vulnerabilidades XSS e melhoram o manuseio de metadados de ativos compartilhados.

Os fragmentos de conteúdo e a API do GraphQL também recebem melhorias de confiabilidade, abrangendo referências de imagens incorporadas, tratamento de consultas persistentes e localização do editor.


<!-- UPDATE FOR EACH NEW RELEASE -->

### Principais recursos e aprimoramentos do Forms

* [Conversões de PDF Generator multithread](/help/forms/using/install-configure-document-services.md#windows-only-enable-multi-threaded-pdf-generator-conversions): adição de suporte para executar conversões simultâneas do Microsoft Word (doc/docx) e do Excel (xls/xlsx) quando o AEM Forms é executado como um serviço do Windows em uma única conta de usuário configurada.

* [Favoritos hierárquicos para PDFs baseados em XFA](https://helpx.adobe.com/content/dam/help/pt-br/experience-manager/6-5/forms/pdf/using-designer.pdf): o Serviço de Saída e o AEM Forms Designer agora geram hierarquias de favoritos estruturadas em PDFs estáticos, interativos e simples, baseados em XFA. Os marcadores seguem os níveis de cabeçalho (H1-H6) definidos nas propriedades de Acessibilidade de caixas de texto, de modo que as entradas H2-H6 são aninhadas sob o pai correto em vez de serem exibidas em paralelo.

* [Detalhes do nível de formulário nos logs de transação do JEE](/help/forms/using/transaction-report-overview-jee.md#form-level-details-transaction-log-jee): o AEM Forms no JEE agora registra detalhes do nível de formulário em `transaction_log.log` para cada transação, além de informações existentes sobre serviço e operação. Os administradores podem correlacionar dados de relatórios de transações com formulários específicos ao analisar envios, representações e conversões. (FORMS-21574)

* [Matriz de Plataforma com Suporte Atualizada](/help/forms/using/aem-forms-jee-supported-platforms.md): o AEM Forms no JEE Service Pack 6.5.25.0 adiciona suporte para compatibilidade com as seguintes tecnologias mais recentes:
   * JBoss® Enterprise Application Platform (EAP) 7.4.23
   * Cliente do gerenciador de conteúdo IBM® 8.7
   * AEM Forms Designer no Terminal Server 2025 do Microsoft® Windows



## Correção de problemas no Service Pack 25 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### Acessibilidade {#sites-accessibility-6525}

* Os controles de arrastar e soltar da linha da tabela na exibição de lista do Sites agora funcionam com a navegação pelo teclado. Os usuários de leitor de tela e teclado podem reordenar linhas e receber feedback durante a ação. (SITES-24946)

* A barra de ferramentas Editar layout agora apresenta rótulos de tela e de tablet menores em uma sequência significativa de leitores de tela. Os usuários ouvem os rótulos com as medidas da régua relacionadas em vez de ouvi-los fora de ordem. (SITES-25291)
* O modal Popover de amostras agora gerencia o foco corretamente quando aberto no modal de anotação. O foco começa no cabeçalho modal em vez de mover diretamente para o botão de amostra selecionado. (SITES-25275)
* O modal Teaser agora oferece uma maneira acessível de mover a caixa de diálogo com um teclado. Os usuários não precisam mais de um mouse para reposicionar o modal na página. (SITES-25226)
* A Exibição de cartão melhora a acessibilidade, removendo o comportamento desnecessário da grade ARIA. Os usuários de leitores de tela recebem informações de cartão mais claras sem controles de navegação por grade que não correspondem ao layout visual. (SITES-24933)
* As dicas de ferramentas no modal Excluir agora são exibidas de forma consistente após ações de focalização repetidas. Os usuários podem mover o ponteiro para fora e retornar ao ícone para ler a dica de ferramenta novamente. (SITES-24778)
* O painel esquerdo agora recebe o foco na ordem esperada depois que os usuários o abrem da página inicial do Sites. Os usuários de leitores de teclado e de tela podem passar do botão de configuração para o conteúdo do painel sem pular a área expandida. (SITES-24754)
* O gerenciamento de foco agora funciona de forma consistente na caixa de diálogo modal Carrossel. Os usuários de teclado e leitor de tela podem iniciar no cabeçalho modal e retornar ao controle original depois de fechar a caixa de diálogo. (SITES-24716)
* A caixa de diálogo Seleção de link agora retorna o foco para o controle que a abriu depois que os usuários fecharam a caixa de diálogo. Os usuários de teclado e leitor de tela não perdem mais seu lugar depois de fechar a caixa de diálogo. (SITES-24707)
* O modal Imagem não move mais o foco para a primeira guia ou ponto de referência da página principal quando os autores abrem ou fecham a caixa de diálogo. Primeiro, o foco é movido para o cabeçalho da caixa de diálogo e, em seguida, retorna ao controle que abriu a caixa de diálogo. (SITES-24693)
* O Painel de referências agora gerencia o foco corretamente quando uma caixa de diálogo modal é aberta. Os usuários de teclado e leitor de tela permanecem dentro da caixa de diálogo até que ela seja fechada e, em seguida, continuam a navegação sem perder o contexto. (SITES-24683)
* O modal de Seleção de caminho do hiperlink não move mais o foco para o campo ou controle errado quando os autores o abrem ou fecham. O foco começa no cabeçalho modal e retorna ao botão que abriu a modal. (SITES-24672)
* O modal Teaser não move mais o foco para a primeira guia ou parte superior da página quando os autores a abrem ou fecham. O foco agora segue o fluxo da caixa de diálogo esperado e reduz anúncios desnecessários do leitor de tela. (SITES-24522)

* O botão Bloquear do Editor de páginas agora fornece feedback mais preciso do leitor de tela. Os leitores de tela usam o atributo de título quando disponível, o que reduz os anúncios detalhados para autores que usam tecnologia assistiva. (SITES-41431)
* A navegação pelo teclado agora ignora o conteúdo oculto. Os usuários podem percorrer elementos visíveis da interface sem que o foco mude para o conteúdo que não podem ver. (SITES-41430)
* O foco do teclado agora retorna ao elemento de acionamento depois que os usuários fecham uma sobreposição. O Editor de páginas não envia mais o foco de volta para a sobreposição, o que melhora a navegação para os usuários do teclado. (SITES-40819)
* A barra de ferramentas do Editor de páginas agora exibe rótulos, como dicas de ferramentas, quando os usuários navegam por itens da barra de ferramentas com um teclado. Os usuários podem entender cada ação da barra de ferramentas à medida que o foco se move de um item para outro. (SITES-40751)
* Passar o mouse sobre os itens do Navegador de componentes não remove mais o foco de um componente de Texto ativo. Os autores podem editar o texto sem interrupção, e o foco do teclado permanece previsível. (SITES-35370)
* Agora, os leitores de tela anunciam com mais clareza o botão de direção de classificação Modal de pesquisa. O rótulo do botão não repete mais a mesma direção e descreve melhor o comportamento de alternância. (SITES-25534)
* O modal de pesquisa agora mostra um indicador visual para a opção selecionada na caixa de listagem Alterar arquivo ou pasta. Os usuários podem identificar a opção de navegação estrutural atual sem depender apenas do foco. (SITES-25532)
* O modal de Pesquisa agora aumenta o contraste do rótulo Classificar por. O texto atende aos requisitos de acessibilidade e melhora a legibilidade para usuários com pouca visão. (SITES-25531)
* Os botões de seleção de dispositivo agora expõem as informações corretas do estado atual na barra de ferramentas Editar layout. Os usuários de leitores de tela podem identificar o dispositivo ativo sem ouvir o status de alternância enganosa. (SITES-25524)
* A navegação pelo teclado e pelo leitor de tela agora fecha o menu da Caixa de entrada quando o foco sai dele. Os usuários evitam o estado confuso em que o menu permanece aberto enquanto o foco se move para outro lugar. (SITES-25518)
* A navegação pelo teclado e pelo leitor de tela agora fecha o menu Ajuda quando o foco sai dele. O foco não se move mais para o conteúdo fora do menu enquanto o menu permanece aberto. (SITES-25517)
* A página inicial dos fragmentos de conteúdo agora fornece um rótulo acessível consistente para guias de barra lateral. O NVDA anuncia o rótulo da guia corretamente quando os usuários navegam pelos controles da guia. (SITES-25509)
* As opções focadas no menu Informações da página agora atendem aos requisitos mínimos de contraste. O contraste aprimorado ajuda os usuários com pouca visão a identificar o item de menu ativo. (SITES-25321)
* A navegação pelo teclado agora ignora controles ocultos na barra de ferramentas Demográfica recolhida. O foco permanece em elementos interativos visíveis, o que melhora a ordem de navegação na Visualização de layout. (SITES-25304)
* O botão Girar dispositivo agora oferece um feedback mais claro do leitor de tela na barra de ferramentas Editar layout. Os leitores de tela anunciam a orientação atual e a ação que a altera. (SITES-25292)
* A barra de ferramentas Editar layout agora exibe um estado limpo selecionado para o botão Área de trabalho. A opção Desktop corresponde aos outros botões do dispositivo e facilita a identificação da exibição ativa. (SITES-25290)
* A barra de ferramentas Editar layout agora rotula a região da régua para tecnologias assistivas. Os usuários de leitores de tela não encontram mais valores de medida sem rótulo durante a edição do layout. (SITES-25287)
* A barra de ferramentas Editar layout agora exibe o rótulo completo do botão iPhone 8 Plus no estado desmarcado. O rótulo não fica mais truncado quando há espaço suficiente ao redor do botão. (SITES-25284)
* O problema relatado descrevia um indicador de foco na barra de ferramentas Editar layout que parecia abranger vários controles de dispositivo. A preocupação se concentrava em usuários de teclado que poderiam perder o controle ativo quando o contorno de foco incluísse botões adjacentes. O problema estava funcionando como projetado. (SITES-25283)
* O problema relatado descrevia os botões Modal de anotação que anunciavam a Anotação antes de cada rótulo de botão. A preocupação se concentrou na saída pouco clara do leitor de tela para ações como Anotar, Amostras e Excluir. (SITES-25277)
* O texto do botão Anotação agora usa contraste suficiente no Modal de anotação. Essa atualização melhora a legibilidade para usuários com pouca visão e oferece suporte aos requisitos de contraste da WCAG. (SITES-25267)
* Os leitores de tela agora recebem atualizações de status quando os usuários filtram a lista Inserir novo componente. O modal anuncia as alterações do resultado para que os usuários entendam que a lista foi alterada enquanto digitavam. (SITES-25251)
* O problema registrado descreveu a semântica de cabeçalho ausente para o título Modal da anotação. A preocupação se concentrou na navegação do leitor de tela e na capacidade de entender a estrutura modal. (SITES-25248)
* Os níveis de cabeçalho no painel lateral do Editor de páginas agora seguem uma hierarquia de conteúdo mais clara. A seção do Painel esquerdo não é mais exibida como o cabeçalho da página principal das tecnologias assistivas. (SITES-25222)
* O botão Editar no painel esquerdo do Assets agora tem um destino de toque maior. Os usuários com necessidades de mobilidade podem ativar o botão mais facilmente e evitar controles próximos. (SITES-25221)
* O painel esquerdo do Assets agora identifica quando o botão Editar abre uma nova guia do navegador. Os usuários podem antecipar a alteração de navegação em vez de perder o contexto inesperadamente. (SITES-25220)
* Agora os títulos de componentes são exibidos corretamente quando os usuários aplicam maior espaçamento do texto. O painel lateral preserva rótulos legíveis e oferece suporte aos requisitos de espaçamento de texto da WCAG. (SITES-25219)
* O campo de filtro em Componentes do painel lateral agora expõe um nome acessível adequado. Essa atualização ajuda os usuários de leitores de tela a identificar o campo sem depender do texto do espaço reservado. (SITES-25212)
* O problema relatado descrevia uma sequência de foco ilógica no modo de anotação. Usuários de teclado relataram ter perdido a barra de ferramentas de anotação, a menos que usassem Shift+Tab após ativar o modo. (SITES-24996)
* A Tela do editor expõe seu título de barra superior como um cabeçalho. Os leitores de tela podem anunciar o título com a estrutura correta, o que melhora a navegação e a compreensão da página. (SITES-24993)
* O relatório de acessibilidade observou contraste insuficiente para a mensagem de status de carregamento que aparece enquanto os usuários trocam de exibição. A preocupação se concentrou na legibilidade para usuários com pouca visão ou daltonismo. (SITES-24991)
* O relatório de acessibilidade observou que os links de cartão incluíam texto não descritivo. A preocupação se concentrou em ajudar os usuários de leitores de tela a entender cada destino de link sem contexto extra. (SITES-24975)
* A exibição em lista dos sites agora exibe o texto da Live Copy com maior contraste. A atualização melhora a legibilidade para autores com pouca visão e para usuários que trabalham em condições de tela brilhante. (SITES-24956)
* A navegação pelo teclado agora move o foco para o menu Emulador depois que os usuários o expandem. Esse comportamento ajuda os usuários de leitor de tela e teclado a acessarem as opções de menu na ordem esperada. (SITES-24954)
* A exibição em lista do Sites agora melhora a visibilidade dos botões de arrastar e soltar em linhas de tabela. Os autores podem identificar o controle mais facilmente ao reordenar o conteúdo. (SITES-24951)
* Um cartão não expõe mais o link de imagem e o link de cabeçalho como links separados quando compartilham o mesmo destino. A atualização reduz a verbosidade do leitor de tela e melhora a eficiência da navegação. (SITES-24947)
* Agora, os botões do menu de cabeçalho usam atributos de acessibilidade mais precisos. Os leitores de tela anunciam os botões como controles expansíveis em vez de controles de abertura de caixas de diálogo. (SITES-24742)
* A Caixa de entrada agora marca links relacionados com a marcação de lista semântica. Os usuários de leitores de tela podem entender o número e o agrupamento de links da Caixa de entrada com mais facilidade. (SITES-24730)
* Agora, os rótulos do botão Cabeçalho evitam nomes detalhados acessíveis. Os usuários de leitores de tela recebem anúncios mais claros sem informações de função duplicadas do texto do ícone. (SITES-24715)
* O botão Relatório de CSV agora fornece feedback mais claro sobre o comportamento da nova guia. Os usuários podem entender que selecionar o botão abre uma nova guia do navegador antes de ativá-lo. (SITES-24704)
* As caixas de diálogo modais agora usam marcação de acessibilidade mais precisa para controles de cabeçalho. Os botões Ajuda e Alternar tela cheia permanecem como controles interativos e não são mais exibidos como cabeçalhos para leitores de tela. (SITES-24696)
* O ponto de referência do Trilho de filtros agora usa um rótulo distinto que identifica sua finalidade. Os usuários de leitores de tela podem navegar pelas páginas com vários pontos de referência semelhantes com mais confiança. (SITES-24686)
* As mensagens do Painel de referências agora oferecem melhor legibilidade para usuários que dependem de contraste de texto suficiente. O problema relatado envolvia mensagens de seleção e seleção múltipla que apareciam muito claras contra seus planos de fundo. (SITES-24666)
* O modal de Pesquisa agora fornece destinos de toque maiores para os botões Remover localização e Fechar. Essa alteração ajuda os usuários com tremores nas mãos, espasmos ou visão baixa a ativar o controle pretendido. (SITES-24530)
* O link do cabeçalho do Adobe Experience Manager foi relatado como usando um atributo ARIA incorreto. Os testes confirmaram que o link controla o conteúdo expansível, de modo que o estado acessível existente permaneça apropriado. (SITES-24528)
* O indicador de foco do botão Subtítulo não aparece mais cortado na lista Componentes. A estrutura visível ajuda os usuários de teclado a rastrear sua posição no editor. (SITES-24503)
* Um problema relatado descrevia uma alternativa em texto ausente para o ícone de dica de ferramenta de informações no painel Componentes. O problema não se reproduziu, mas a revisão confirmou que os ícones informativos devem expor um nome claro e acessível. (SITES-24500)
* O Editor de páginas não expõe mais vários pontos de referência de região com o mesmo rótulo. Cada ponto de referência agora tem um nome acessível exclusivo, de modo que os usuários de leitores de tela podem identificar a região atual. (SITES-24497)
* O controle Alterar arquivo ou pasta agora separa o rótulo de controle de suas informações de estado. Os usuários de leitores de tela ouvem um nome mais curto e mais claro ao navegar pelo controle de cabeçalho. (SITES-24496)
* Os controles interativos na tabela Administrador do fragmento de conteúdo agora oferecem suporte à navegação padrão do teclado. Os usuários de teclado podem ir até botões e links em vez de descobrí-los somente por meio da navegação com a tecla de seta. (SITES-24285)
* A interface do administrador do Sites agora trata os ícones de Globo decorativos corretamente para leitores de tela. Os ícones usam texto alternativo vazio para que os usuários ouçam somente o conteúdo significativo da interface. (SITES-3057)

#### Interface do usuário do administrador{#sites-adminui-6525}

O console Sites agora mostra corretamente as configurações de coluna da **Exibição de lista** salvas. As colunas selecionadas permanecem marcadas quando os autores reabrem a caixa de diálogo de configurações e a contagem de colunas ativas permanece precisa. (SITES-38576)

#### IU Clássica{#sites-classicui-6525}

As caixas de diálogo do componente Texto da interface clássica agora exibem o conteúdo do Editor de Rich Text (RTE) como texto formatado em vez de HTML bruto. Os autores podem editar o texto existente sem alternar para o modo Source ou remover a marcação manualmente. (SITES-38709)

#### Console de componentes{#sites-component-console-6525}

* Os usuários agora podem pesquisar o console Componentes com caracteres localizados ou multibyte. O console também mostra um rótulo **Remover** localizado em vez da cadeia de caracteres em inglês não traduzida. (SITES-39747)
* A página Propriedades do componente agora localiza cadeias de caracteres em Ferramentas > Componentes > Propriedades do componente. Os usuários não verão mais rótulos em inglês não traduzidos nas interfaces de criação localizadas. (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

O Assets Search agora responde corretamente quando os usuários selecionam ou alteram filtros. O conjunto de resultados filtrado é atualizado conforme esperado, o que restaura o refinamento de pesquisa confiável no console do Assets. (SITES-38686)

#### [!DNL Content Fragments] — Admin{#sites-admin-6525}

* A exibição em lista do Assets agora mostra uma dica de ferramenta Retirado por localizada para fragmentos de conteúdo bloqueados. Essa correção melhora a consistência da localização quando os autores revisam as linhas do fluxo de trabalho. (SITES-42531)

* O AEM agora localiza o rótulo Principal na caixa de diálogo de download do Fragmento de conteúdo. A correção mantém o fluxo de trabalho de download consistente em locais que não estejam em inglês. (SITES-42534)
* O AEM agora traduz o rótulo de status `Later` quando os autores agendam a publicação de Fragmento de conteúdo do Assets. Essa correção mantém a coluna Publicado consistente em todas as interfaces localizadas. (SITES-42532)
* A criação de fragmentos de conteúdo agora exibe uma mensagem de validação localizada quando os autores inserem caracteres inválidos no campo Título. A caixa de diálogo não mostra mais a cadeia de caracteres &quot;Nome inválido fornecido&quot; deslocalizada. (SITES-19796)
* A página Editar fragmento do conteúdo agora usa rótulos localizados para Tags e Coleções. Os autores veem nomes de campos traduzidos em vez de cadeias de caracteres em inglês não localizadas. (SITES-977)

#### [!DNL Content Fragments] — Editor de fragmentos{#sites-fragments-editor-6525}

* O conteúdo associado no Editor de fragmento de conteúdo agora mostra a sequência localizada correta quando os autores removem o conteúdo de uma coleção. A caixa de diálogo não substitui mais o nome do conteúdo por indefinido. (SITES-33675)
* O Editor de fragmento de conteúdo agora exibe um rótulo Geral traduzido para guias sem um espaço reservado configurado. Interfaces localizadas não mostram mais a sequência de caracteres em inglês não traduzida nessa área do editor. (SITES-30715)
* O seletor de Referência de conteúdo no Editor de fragmento de conteúdo agora mostra rótulos localizados para tipos de ativos permitidos. As interfaces localizadas não exibem mais nomes de tipo em inglês para categorias de ativos compatíveis. (SITES-29699)

#### [!DNL Content Fragments] — API GraphQL {#sites-graphql-api-6525}

* As respostas JSON do GraphQL agora incluem referências de imagem incorporadas de campos de Rich Text de fragmento de conteúdo quando os nomes de arquivo do DAM contêm espaços ou caracteres não ASCII. Essa correção ajuda os aplicativos a renderizar imagens referenciadas sem exigir que os autores renomeiem ativos. (SITES-42191)
* As respostas do GraphQL para fragmentos de conteúdo agora lidam com consultas persistentes de maneira mais confiável. As atualizações corrigem cabeçalhos de cache duplicados, melhoram o tratamento de variáveis codificadas e retornam respostas mais claras para conteúdo ausente ou consultas com falha. (SITES-40159)
* As consultas persistentes do GraphQL agora são executadas sem mensagens de ERRO e AVISO desnecessárias nos logs. O AEM manipula corretamente as variáveis codificadas, de modo que consultas bem-sucedidas não criam mais `PersistedQueryServlet` entradas enganosas. (SITES-39354)

* A caixa de diálogo Editar endpoint do GraphQL agora localiza suas cadeias de caracteres de interface. Os usuários não veem mais o esquema não traduzido do GraphQL que é retirado da mensagem de configuração nas interfaces localizadas. (SITES-34018)

#### [!DNL Content Fragments] — Editor de consultas GraphQL{#sites-graphql-query-editor-6525}

Os usuários agora podem abrir o Editor de consultas GraphQL quando o nome do navegador de configuração selecionado contiver caracteres CJK ou cirílicos. O editor exibe consultas persistentes para o endpoint em vez de mostrar um erro. (SITES-31616)

#### [!DNL Content Fragments] - Modelos e Editor de modelos{#sites-models-model-editor-6525}

* Os usuários agora veem uma mensagem de validação localizada no Editor de modelos de fragmentos de conteúdo quando um valor selecionado precisa de um tipo de modelo válido. O editor não exibe mais a mensagem em inglês não traduzida em interfaces localizadas. (SITES-41117)
* O painel de filtro Modelo de fragmento de conteúdo agora localiza suas cadeias de caracteres de status e título. Os usuários não verão mais rótulos não traduzidos, como Título do modelo, Status, Rascunho, Ativado e Desativado. (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

O ContextHub agora é carregado sem um erro do JavaScript que interrompeu a personalização. Teasers e outras experiências personalizadas podem ser renderizados corretamente nas páginas afetadas. (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### Componentes principais{#sites-core-components-6525}

* O AEM não gera mais erros ThumbnailServlet repetidos quando uma solicitação é direcionada a um recurso DAM ausente. O servlet interrompe o processamento após o redirecionamento, o que impede que as entradas de NullPointerException inundem o log de erros. (SITES-41238)
* O AEM não sinaliza mais os campos opcionais da caixa de diálogo, conforme necessário, quando os autores reabrem as caixas de diálogo do componente. A caixa de diálogo mantém a validação focada em campos que realmente exigem entrada, o que evita erros enganosos no nível de guia. (SITES-40449)

* O AEM inclui várias correções de segurança com suporte retroativo que fortalecem os sites e os componentes relacionados do Cloud Services. Essas correções reduzem o risco de script entre sites e melhoram a manipulação de solicitações nos caminhos de criação afetados. (SITES-38314)
* A caixa de diálogo de configuração do componente Imagem v3 agora localiza cadeias de caracteres no Editor de páginas. Os autores não veem mais rótulos não traduzidos ao configurar componentes de Imagem em interfaces localizadas. (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### Crosswalk {#sites-crosswalk-6525}

* O Crosswalk não requer mais pacote separado e configuração após a instalação. O AEM inclui os pacotes necessários, pacotes de conteúdo, usuários do sistema, mapeamentos de usuários de serviço e opções de recursos no pacote pronto para uso. (SITES-41417)
* Os fluxos de trabalho do Crosswalk agora funcionam com o suporte necessário para cq-wcm-core no AEM 6.5. Os autores podem usar as ações Criar modelo e Abrir editor universal sem atualizações do pacote principal separadas. (SITES-37666)

#### Fragmentos de experiência{#sites-experiencefragments-6525}

O AEM agora carrega os modelos corretos quando os autores criam variações de Fragmento de experiência e rolam pela tela além dos primeiros 40 resultados. O Seletor de modelos mantém o caminho do Fragmento de experiência selecionado durante a paginação. (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### Lançamentos{#sites-launches-6525}

* A Linha do tempo do Sites agora localiza a mensagem que aparece quando o AEM cria uma versão antes de promover uma inicialização. Os usuários não verão mais a cadeia de caracteres em inglês não traduzida nas interfaces localizadas. (SITES-39157)
* A lista Inicializações agora exibe a descrição correta para inicializações criadas sem modelo ou herança da live copy. Os usuários não verão mais o rótulo Modelo substituído enganoso. (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### Localização{#sites-localization-6525}

* As propriedades do componente de Texto nos Fragmentos de experiência agora usam rótulos localizados. O menu Formatar não mostra mais cadeias de caracteres não localizadas para opções de parágrafo, cabeçalho, aspas ou texto pré-formatado. (SITES-15091)

* O texto de status do modelo agora está alinhado corretamente em **Ferramentas** > **Geral** > **Modelos**. Os rótulos de status atualizados, ativados e publicados aparecem em uma linha horizontal. (SITES-36797)
* A caixa de diálogo Mover página agora mostra o rótulo Selecionar data e hora completo. O rótulo não fica mais truncado em interfaces localizadas, como francês. (SITES-36795)
* A seção Assets no Editor de modelo agora mostra um rótulo Tags traduzido. As interfaces de criação localizadas apresentam rótulos consistentes durante a configuração do modelo. (SITES-33770)
* As descrições da Política da página agora são renderizadas corretamente no Editor de modelo. Os usuários podem ler a orientação completa de Classes CSS padrão sem texto truncado na guia Estilos. (SITES-29724)
* O Editor de modelo agora exibe um erro localizado quando um autor tenta arrastar um componente para um modelo excluído. A mensagem não é mais exibida como uma string não traduzida &quot;durante o processamento&quot;. (SITES-19313)
* O rótulo &quot;Direcionado&quot; na janela Configuração do teaser agora é exibido com texto localizado. A seção Hiperlink não mostra mais a cadeia de caracteres em inglês em locais que não sejam em inglês. (SITES-18622)
* A caixa de diálogo Iniciar fluxo de trabalho no Editor de páginas agora exibe rótulos de ação de fluxo de trabalho localizados. Os autores não veem mais cadeias de caracteres em inglês para opções de fluxo de trabalho. As opções incluem ações de aprovação, publicação, solicitação e cancelamento da publicação. (SITES-18103)
* O menu suspenso Pai no painel de edição Separador agora exibe cadeias de caracteres localizadas sem truncamento. Os autores podem revisar o rótulo completo ao configurar o componente. (SITES-17480)
* O Editor de páginas agora exibe rótulos localizados para &quot;Largura total&quot; e &quot;Largura fixa&quot; no menu Estilos do componente de Contêiner. Os autores que usam localidades compatíveis não verão mais essas cadeias de caracteres em inglês. (SITES-17478)
* Os autores agora podem ler a dica de ferramenta completa na área Propriedades de navegação do console Modelos. A interface do usuário mantém a dica de ferramenta alinhada e impede o truncamento de texto durante a edição do modelo. (SITES-15480)
* Os autores agora podem ler a etiqueta completa &quot;Forms e documentos usando modelo&quot; no painel lateral Referências. O console Modelos não corta mais a cadeia de caracteres para localidades compatíveis. (SITES-13167)
* A visualização Referências agora usa texto localizado para a mensagem de erro de atualização. Os autores veem mensagens traduzidas quando o AEM não pode atualizar a lista de referências. (SITES-13102)
* A validação de formulário agora identifica o campo que contém um valor de tempo inválido. O modal Distorção de tempo exibe mensagens de erro mais claras para que os autores possam corrigir o campo Horas ou Minutos afetados. (SITES-10980)
* O console Modelos agora exibe um rótulo Assets localizado na caixa de diálogo Selecionar imagem. O rótulo aparece corretamente quando os autores procuram ativos nas propriedades do modelo. (SITES-8113)

#### MSM: Live Copies{#sites-msm-live-copies-6525}

* A Visão geral da Live Copy agora localiza formatos de data na visualização Status do relacionamento. Os campos L **Última Modificação do Source da Live Copy**, **Última Modificação da Live Copy** e **Última implantação** mostram datas que correspondem à localidade do usuário. (SITES-40756)
* O MSM agora registra mais detalhes sobre eventos de push-na-modificação. As informações adicionadas sobre o evento ajudam as equipes a rastrear a atividade de implantação e identificar a origem de alterações inesperadas na página. (SITES-38029)

#### Editor de página{#sites-pageeditor-6525}

* Agora os autores podem criar tags que incluem letras maiúsculas ou espaços e aplicá-las durante o salvamento da primeira Página Propriedades. O AEM cria a tag e grava o valor correto nos metadados da página durante a mesma operação. (SITES-42550)

* Os autores agora podem criar fragmentos de conteúdo em pastas DAM cujos nomes contêm um apóstrofo. O AEM manipula o caminho da pasta codificada corretamente e não aciona mais uma NullPointerException durante a criação. (SITES-38653)

* O AEM agora oferece suporte às ações de copiar e colar para componentes de Fragmento de conteúdo configurados no Editor de páginas. O componente retém a referência do fragmento de conteúdo, de modo que os autores podem duplicar o conteúdo sem recriação manual. (SITES-41586)
* O Editor de páginas agora exibe as dicas de ferramentas de descrição do primeiro campo corretamente nas caixas de diálogo do componente. Descrições longas permanecem visíveis, de modo que os autores podem revisar as instruções de campo sem perder texto na parte superior da dica de ferramenta. (SITES-39937)
* Agora, os autores podem abrir a caixa de diálogo Link do editor de rich text ao usar AEM sobre HTTP. A correção restaura a edição de links para ambientes locais que não usam HTTPS. (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### Editor universal {#sites-universal-editor-6525}

* Por padrão, o Editor universal não é mais aberto no modo de Visualização. O AEM envia os usuários para o ambiente de produção do Editor universal, a menos que eles solicitem explicitamente o comportamento de visualização. (SITES-37193)
* O Universal Editor agora abre no modo Visualização para ambientes de desenvolvimento, desenvolvimento rápido e preparo do AEM. O comando Abrir usa o comportamento de visualização correto para instâncias de não produção. (SITES-33839)

### [!DNL Assets] {#assets-6525}

* A biblioteca cliente Meus compartilhamentos agora lida com dados de título de ativo compartilhado com segurança antes de adicioná-los à marcação de página. As páginas de compartilhamento geradas não expõem mais os usuários à injeção de script por meio de metadados de ativos manipulados. (ASSETS-60898)

* O licenciamento do Adobe Stock agora funciona corretamente na interface do usuário do Assets. O botão Licença não permanece mais desativado depois que o AEM carrega o perfil do ativo de estoque e os dados de direito. (ASSETS-62610)
* A notificação de expiração de ativos pronta para uso agora lida corretamente com datas de quase expiração. Emails de lembrete são executados quando o tempo restante atinge o limite configurado, em vez de ignorar ativos com um prazo de oito dias. (ASSETS-57857)

* O AEM Assets agora restaura a navegação pelo teclado depois que os usuários escolhem uma pesquisa salva. A interface permite que os usuários saiam da lista suspensa sem atualizar ou reiniciar a visualização do Assets. (ASSETS-52061)

* O fluxo de trabalho de download do Admin View agora preserva os nomes de arquivo ZIP corretamente. O download de um ativo ZIP não produz mais um nome de arquivo com uma extensão .zip dupla. (ASSETS-62207)
* O fluxo de trabalho de referência do Assets agora lida corretamente com espaços nos nomes de arquivo. As atualizações de ativos relacionados não falham mais quando um nome de arquivo selecionado inclui um ou mais espaços. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

A lista suspensa Legendas e faixas de áudio agora mostra o árabe como um idioma compatível no Dynamic Media. Essa atualização permite que os usuários adicionem faixas de legendas em árabe sem soluções alternativas personalizadas. (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

* A visualização de Comunicações interativas agora carrega o conteúdo corretamente após o AEM Forms Service Pack 6.5.24.0. O texto não é mais carregado lentamente com espaços ausentes, portanto, a visualização corresponde ao conteúdo criado e permanece mais fácil de ler. (FORMS-25346)
* Os detalhes da validação agora aparecem nos componentes principais do Adaptive Forms após configurar um Padrão de validação e salvar o formulário. O padrão permanece visível na interface de criação do. (FORMS-25236)
* Agora a geração de documentos lida corretamente com fragmentos XDP (Extensible Forms Description Language) aninhados nos ambientes do AEM Forms 6.5 Service Pack 23 e do AEM Forms Service Pack 6.5.24.0. (FORMS-25234)
* O texto localizado fora dos fragmentos de formulário agora é exibido no idioma correto durante a revalidação do lado do servidor do Adaptive Forms usando o mecanismo Rhino. O texto não reverte mais para o idioma padrão após o envio. (FORMS-25224)
* O Serviço de Saída não trava mais com um erro de instrução Ilegal no Red Hat Enterprise Linux (RHEL) 8 após a atualização para o AEM Forms Service Pack 6.5.24.0. O processamento da geração de documentos e da saída de formulários foi concluído sem interrupções abruptas do serviço. (FORMS-25192)
* Painéis e conteúdo adicionados dinamicamente usando a função addInstance() no Adaptive Forms agora aparecem quando o número inicial de instâncias é definido como 0. (FORMS-25169, FORMS-25124)
* As traduções do Chinês tradicional (Hong Kong) agora são exibidas corretamente nos ambientes Autor e Publicação após a atualização para o AEM Forms Service Pack 6.5.24.0. O conteúdo localizado em zh-HK não aparece mais no idioma errado ou retorna às cadeias de caracteres padrão inesperadamente. (FORMS-25042)
* A navegação pelo teclado no campo Assinatura escritas no Adaptive Forms agora move o foco consistentemente para dentro e para fora da área de assinatura enquanto navega pelo formulário. (FORMS-25011)
* Os arquivos WSDL (Web Services Description Language) agora são carregados corretamente na etapa Chamar serviço Web durante as operações de configuração e atualização. (FORMS-24992, FORMS-24789, FORMS-24188)
* Os rascunhos de letras agora mantêm quebras de linha quando as condições são aplicadas aos fragmentos de texto. O conteúdo multilinha não aparece mais como uma única linha contínua. (FORMS-24602)
* Os fluxos de trabalho do Adobe Sign no AEM Forms no Adobe Managed Services (AMS) não param mais quando a resposta de status de assinatura não é retornada após atingir a etapa do Adobe Sign. (FORMS-24514)
* A conversão do PDF (HTML para Portable Document Format) não atinge mais o tempo limite intermitentemente no AEM Forms Service Pack 6.5.24.0, inclusive em trabalhos de conversão maiores ou complexos. (FORMS-23978)
* O Gerenciamento do modo de backup seguro na interface do usuário do administrador agora funciona corretamente após a instalação do patch AEMForms-6.5.0-0112. Os usuários podem desativar ou desativar o Modo de Backup Seguro quando a opção estiver disponível. (FORMS-23976, FORMS-23718)
* A pesquisa da fonte de dados do modelo de dados de formulário não falha mais ou exibe tags brutas de HTML (HyperText Markup Language) nos resultados da pesquisa. Os resultados mostram texto legível. (FORMS-23875)
* As funções personalizadas agora são carregadas no tempo de execução quando o Adaptive Forms é incorporado nas páginas do Sites usando as versões dos componentes principais com suporte no AEM Forms Service Pack 6.5.24.0. (FORMS-23802)
* As regras numéricas das Comunicações interativas agora avaliam os valores corretamente ao analisar com a biblioteca atualizada Sling Commons JavaScript Object Notation (JSON). Os campos numéricos lidam com as alterações de análise BigDecimal de forma consistente. (FORMS-23733)
* O comportamento do Documento de registro agora é consistente ao trabalhar na versão 6.5.0 e versões posteriores. A saída de formulários e o processamento relacionado se alinham ao comportamento esperado de ambientes mais recentes. (FORMS-23338)

#### FORMS JEE {#forms-jee-6525}

* A inicialização do aplicativo não falha mais ao carregar o componente de registro com uma classe não encontrada para o erro org.owasp.esapi.reference.JavaLogFactory. Os ambientes afetados são inicializados corretamente sem a necessidade de reinicialização ou reconfiguração do serviço. (FORMS-25348)
* A inicialização é concluída com êxito após a aplicação do Service Pack 25. O processo de inicialização do sistema não falha mais antes que a inicialização termine. (FORMS-25347)
* Os componentes do Core Portable Document Format (PDF) (CPDF) agora são criados e executados corretamente em ambientes Linux sem parar inesperadamente durante a execução. (FORMS-25115)
* A decodificação do código de barras não falha mais com erros DecodingException ao processar determinados arquivos Portable Document Format (PDF) durante a extração do código de barras. (FORMS-23534, FORMS-23449)

#### Designer do Forms {#forms-designer-6525}

* A saída ExportData agora corresponde aos dados do formulário ao usar ExportData na versão 6.5. Os campos XML (Extensible Markup Language) exportados se alinham aos valores mostrados nos formulários originais. (LC-3922791)
* O Serviço de Saída agora gera marcas de acessibilidade corretas em arquivos PDF (Portable Document Format) criados no AEM Forms Service Pack 6.5.22.0. As tecnologias assistivas leem o conteúdo na ordem correta sem ignorar os elementos. (LC-3922756)
* O Serviço de saída agora reflete os estados de campo ocultos ou desativados corretamente ao nivelar formulários em Formato de Documento Portátil (PDF) com a marcação ativada. (LC-3922708)
* Os campos com legendas inferiores no Workbench agora recebem a marcação correta, o que melhora a consistência e a acessibilidade em documentos gerados. (LC-3922619)
* Os códigos QR em formulários permanecem verificáveis após a atualização para o AEM Forms Service Pack 6.5.20.0. Os scanners padrão leem de forma confiável os códigos QR gerados. (LC-3922551)
* A renderização do Forms Service agora produz saída consistente ao usar entrada idêntica em service packs diferentes. Os valores renderizados não diferem mais entre o AEM Forms Service Pack 6.5.17.0 e o AEM Forms Service Pack 6.5.18.0. (LC-3922461)
* Os documentos do PDF/A gerados a partir de modelos de Pacote de dados XML (XDP) agora renderizam corretamente os estilos de borda do Quadrado Aberto. A aparência do campo de formulário corresponde ao layout projetado. (LC-3922180)
* Os envios em formato Plano de Documento Portátil (PDF) agora retêm dados em todas as seções. Os valores inseridos permanecem no documento nivelado final. (LC-3922008)
* Os arquivos PDF (Portable Document Format) estáticos convertidos não geram mais várias tags de link de um único link no modelo XDP original. (LC-3921997)
* A exportação de envios do AEM Forms agora inclui todos os campos nos arquivos de saída exportados. (LC-3921983)


### Foundation {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

A inicialização agora conecta o serviço CredentialsSupport corretamente para autenticação baseada em Felix. Isso evita erros de dependência que podem afetar a autenticação de token durante a inicialização do AEM. (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

A edição de arquivos JSP agora funciona conforme esperado no CRXDE Lite após as atualizações do AEM 6.5. O editor CodeMirror carrega o conteúdo do arquivo em vez de deixar a guia JSP em branco. (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### Localização{#foundation-localization-6525}

* A caixa de diálogo de upload de certificado em Segurança > Armazenamento de confiança agora mostra rótulos de formato de dados localizados. Os usuários não veem mais rótulos em inglês não localizados ao adicionar um certificado. (NPR-43412)

* A caixa de diálogo Criar KeyStore agora alinha o botão Cancelar aos outros botões da caixa de diálogo. O layout do botão permanece consistente e não muda mais para fora do alinhamento. (NPR-43291)
* A caixa de diálogo Verificar em **Segurança** > A **Configurações do Adobe IMS** agora exibe o texto de confirmação localizado. As mensagens de verificação e exclusão não aparecem mais como cadeias de caracteres em inglês não localizadas. (NPR-43289)
* Os rótulos localizados da interface do usuário agora aparecem corretamente nas caixas de diálogo afetadas e na guia Armazenamento de chaves. Os valores de rótulo ARIA usam strings traduzidas e os rótulos de campo de senha são exibidos sem truncamento. (NPR-43285)
* O fluxo de trabalho Criar novo usuário agora mostra erros de validação localizados para caracteres inválidos. Os usuários recebem uma mensagem clara e traduzida em vez de uma cadeia de caracteres IllegalArgumentException não localizada. (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Platform{#foundation-platform-6525}

* O botão Mostrar referências da tag agora exibe o número de referências da tag selecionada. Essa atualização ajuda os usuários a entender o uso de tags sem navegação extra. (CQ-4355509)
* A caixa de diálogo Mover em Marcação agora posiciona as mensagens de validação corretamente. O texto de erro não cobre mais o ícone de caminho de pesquisa quando os usuários enviam a caixa de diálogo com um campo obrigatório vazio. (CQ-4353009)

#### Segurança{#foundation-security-6525}

A AEM agora inclui na lista de permissões palavras-chave adicionais que contêm segredo do cliente. A criação de configurações não falha mais quando as integrações compatíveis usam esses padrões de nomenclatura de segredo do cliente. (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### Tradução{#foundation-translation-6525}

As contagens de status do projeto de tradução agora são atualizadas corretamente após a atualização. Os autores podem revisar valores de rascunho, em andamento e concluídos sem depender de metadados desatualizados do comportamento anterior do service pack. (NPR-43418)

#### Interface do usuário{#foundation-ui-6525}

* Os URLs de console do Sites inseridos manualmente agora são resolvidos para a página ou o caminho da pasta desejado. A hierarquia de conteúdo permanece consistente após a atualização e não retorna mais ao URL de base. (NPR-43688)
* O conjunto de testes do Adobe CRX Package Manager não falha mais após uma instância do AEM 6.5 LTS SP1 ser atualizada para o LTS SP2. O teste do servlet de lista de miniaturas agora é concluído conforme esperado. (NPR-43534)

* A árvore de conteúdo do console Sites agora é carregada de forma consistente após cada atualização do navegador. Os autores não verão mais um painel em branco à esquerda ou uma mensagem &quot;Não há item&quot; quando o conteúdo existir. (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### Fluxo de trabalho{#foundation-workflow-6525}

* O editor do modelo de fluxo de trabalho agora valida corretamente os caminhos do modelo de fluxo de trabalho específicos do locatário. Os clientes que armazenam modelos de fluxo de trabalho em caminhos /conf no nível do locatário podem editar esses modelos sem movê-los para caminhos de configuração global. (GRANITE-65376)

* O editor do modelo de fluxo de trabalho agora normaliza os caminhos de arquivo do Windows durante a validação do caminho. Os autores podem editar modelos de fluxo de trabalho em servidores Windows sem erros de acesso que bloqueiam atualizações de modelo. (GRANITE-63692)
* A criação da tarefa agora inclui validação do lado do servidor para datas de vencimento. Os usuários não podem criar tarefas com uma data de vencimento anterior à data de início, o que mantém os dados da tarefa da caixa de entrada consistentes. (CQ-4362253)
* A criação de namespace agora lida com o texto localizado corretamente. Os usuários podem inserir caracteres não latinos no campo Título e criar o namespace sem um erro de validação. (CQ-4355587)

## Instalar [!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0 requer [!DNL Experience Manager] 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível na [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) da Adobe.
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.25.0 em uma das instâncias do Autor usando o Gerenciador de Pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> A Adobe não recomenda que você remova ou desinstale o pacote [!DNL Experience Manager] 6.5.25.0. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository`, caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].

1. Baixe o Service Pack de [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Repositório de Dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes sai durante a instalação do Service Pack. A Adobe recomenda aguardar a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no navegador do [!DNL Safari], mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.25.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.25.0 não oferece suporte à instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (6.5.25.0)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

O UberJar para [!DNL Experience Manager] 6.5.25.0 está disponível no [repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal foi renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como valor, para a tag `dependency`.



## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md) para obter uma lista detalhada de todos os recursos obsoletos ou removidos do AEM 6.5.

### Suporte a Fragmento de conteúdo na API REST do AEM Assets {#cf-support-assets-rest-api}

O AEM 6.5 LTS SP2 fornece OpenAPIs modernas para gerenciamento de fragmentos de conteúdo e modelos. Portanto, os pontos de acesso mais antigos de suporte a fragmentos de conteúdo na API REST do AEM Assets agora estão obsoletos.

A Adobe pretende manter esses endpoints mais antigos disponíveis até um anúncio do fim da vida útil. A Adobe não planeja melhorias adicionais para os pontos de acesso obsoletos.

### Editor SPA {#spa-editor}

[O Editor de SPA](/help/sites-developing/spa-overview.md) foi descontinuado para novos projetos a partir da versão 6.5.25 do AEM 6.5. O Editor SPA permanece compatível com projetos existentes, mas não deve ser usado para novos projetos.

Os editores preferidos para gerenciar conteúdo headless no AEM agora são:

* [O Editor Universal](/help/sites-developing/universal-editor/introduction.md) para edição visual.
* [O Editor de Fragmento de Conteúdo](/help/sites-developing/universal-editor/introduction.md) para edição baseada em formulário.

## Problemas conhecidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

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

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas. Falha na consulta em segundo plano; a funcionalidade não funciona.
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

* A partir do AEM 6.5.15, o Mecanismo Rhino JavaScript fornecido pelo pacote `org.apache.servicemix.bundles.rhino` tem um novo comportamento de elevação. Os scripts que usam o modo estrito (`use strict;`) devem declarar suas variáveis corretas. Caso contrário, eles não serão executados e acabarão gerando um erro de tempo de execução.

* A instalação de marcação relacionada ao conteúdo pronto para uso por meio de um pacote de atualização oficial redefine a propriedade languages do nó `/content/cq:tags` para o padrão. Essa ação é verdadeira para Service Packs, Service Packs de segurança, Pacotes de recursos estendidos, Pacotes de recursos cumulativos, patches e assim por diante. Portanto, é necessário adicioná-lo das propriedades antes da instalação.

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6525}

A visualização dos fragmentos de conteúdo falha devido à proteção do DoS para uma grande árvore de fragmentos. Consulte o artigo [KB sobre as opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6525}

* **FORMS-14521** Se um usuário tentar visualizar um rascunho de carta com dados XML salvos, ele ficará preso no estado `Loading` para algumas cartas específicas.
* **FORMS-16603** Na Visualização de Impressão da Interface do Usuário do Agente de Comunicações Interativas, alguns valores calculados não são exibidos corretamente.
* **FORMS-15681** Quando a correspondência é exibida na Visualização de Impressão, o conteúdo é alterado; alguns espaços desaparecem e determinadas correspondências são substituídas por `x`.
* **FORMS-15428** Depois de atualizar para o AEM Forms Service Pack 20 (6.5.20.0) com o Complemento do Forms, as configurações que dependem do Adobe Analytics Cloud Service herdado usando a autenticação baseada em credencial param de funcionar. Esse problema impedia que as regras do Analytics fossem executadas corretamente.
* **FORMS-16557** Na Visualização de Impressão da Interface do Usuário do Agente de Comunicações Interativas, o símbolo de moeda (como cifrão $) é exibido de forma inconsistente para todos os valores de campo. Aparece para valores até 999, mas está ausente para valores de 1000 e superiores.
* **FORMS-16575** Quaisquer modificações no XDP de fragmentos de layout aninhados em uma Comunicação Interativa não são refletidas no editor IC.
* **FORMS-21378** Quando a validação no lado do servidor (SSV) estiver habilitada, os envios de formulários poderão falhar. Se você encontrar esse problema, entre em contato com o Suporte da Adobe para obter assistência.
* **FORMS-23722** Quando um formulário contendo o campo **Anexo de Arquivo** que usa `bindref` é enviado a um Fluxo de Trabalho do AEM com uma etapa **Atribuir Tarefa**, os anexos não são exibidos. Como resultado, eles não aparecem quando a tarefa é aberta da Caixa de entrada. Os arquivos são salvos corretamente no repositório, mas a interface do usuário da etapa Atribuir tarefa não exibe os anexos.
* **FORMS-23802** As funções personalizadas não são carregadas na pré-visualização ou publicação quando um Formulário adaptável é inserido em uma página do Sites. Esse problema ocorre quando a versão da biblioteca do **aem-forms-core-component** é anterior à 1.1.76. Você pode ver um erro como `InvalidFormContainerException: No form container found` nos logs. Para resolver esse problema, [baixe e instale o hotfix](/help/release-notes/aem-forms-hotfix.md) para AEM Forms SP24 (AddOn 6.0.1454).

#### Problemas conhecidos com Hotfixes disponíveis {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

Os seguintes problemas têm uma correção disponível para download e instalação. Você pode [baixar e instalar o Hotfix](/help/release-notes/aem-forms-hotfix.md) para resolver estes problemas:

* **FORMS-23881** Em implantações do AEM Forms JEE configuradas com o instalador completo do 6.5.23.0, o Serviço de Saída não processa solicitações quando um arquivo XCI personalizado é fornecido na invocação. Para resolver esse problema, instale o AEM 6.5.25.0 Forms Service Pack mais recente do portal [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* **FORMS-23789** (somente AEM Forms no JEE): os usuários tiveram problemas com o Log4j no AEM Forms no JEE SP24, causando interrupções no registro e monitoramento para clientes corporativos. Para resolver esse problema, [baixe e instale o hotfix](/help/release-notes/aem-forms-hotfix.md) para AEM Forms no JEE Service Pack 6.5.25.0.
* **FORMS-23802** As funções personalizadas não são carregadas na visualização ou publicação quando o formulário está em uma página do Sites com uma versão mais antiga do componente principal do aem Forms (&lt;1.1.76). Para resolver esse problema, instale o [AEM Forms AddOn hotfix 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.
* **FORMS-23789** (somente AEM Forms no JEE): os usuários tiveram problemas com o Log4j no AEM Forms no JEE SP24, causando interrupções no registro e monitoramento para clientes corporativos. Para resolver esse problema, [baixe e instale o hotfix](/help/release-notes/aem-forms-hotfix.md) para AEM Forms no JEE Service Pack 6.5.25.0.
* **FORMS-23802** As funções personalizadas não são carregadas na visualização ou publicação quando o formulário está em uma página do Sites com uma versão mais antiga do componente principal do aem Forms (&lt;1.1.76). Para resolver esse problema, instale o [AEM Forms AddOn hotfix 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.
* O AEM Forms agora inclui uma atualização da versão do Struts 2.5.33 para 6.x para o componente de formulários. Essa atualização fornece alterações do Struts que não foram incluídas no SP24. O suporte foi adicionado por meio de um [Hotfix](/help/release-notes/aem-forms-hotfix.md) que você pode baixar e instalar para adicionar suporte à versão mais recente do Struts.
* **FORMS-14926** Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` na pasta `<AEM_Forms_Installation>/lib/caching/lib`, execute as seguintes etapas para resolver o problema:

   1. Pare os localizadores, se eles estiverem em execução.
   2. Pare o servidor do AEM.
   3. Vá para o `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Remova todos os arquivos de correção Geode, exceto `geode-*-1.15.1.2.jar`. Confirme se apenas os jars Geode com `version 1.15.1.2` estão presentes.
   5. Abra o prompt de comando no modo de administrador.
   6. Instale o patch Geode usando o arquivo `geode-*-1.15.1.2.jar`.

* **FORMS-15256** Quando os usuários atualizaram do AEM 6.5 Forms Service Pack 18 ou 19 para o Service Pack 20 ou 21, eles encontraram um erro de compilação de JSP. Esse erro os impedia de abrir ou criar formulários adaptáveis. Isso também causava problemas com outras interfaces do AEM. Essas interfaces incluíam o Editor de páginas, a interface do AEM Forms, o editor de fluxo de trabalho e a interface da Visão geral do sistema.

  Se você enfrentar esse problema, execute as seguintes etapas para resolvê-lo:
   1. Navegue até o diretório `/libs/fd/aemforms/install/` no CRXDE.
   2. Exclua o pacote com o nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie o servidor do AEM.

* **FORMS-23703** Quando a regra `contains` é configurada sem um valor padrão, a validação do Server Side para um Formulário adaptável falha. Você pode instalar a última versão do [AEM Forms 6.5.25.0 Service Pack](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) para corrigir o problema.
* **GRANITE-63681** A configuração padrão do sistema bloqueia as palavras-chave e os padrões regex necessários, o que impede a autenticação dos conectores do Modelo de Dados de Formulário. Para resolver o problema, baixe e instale o hotfix do [link](/help/release-notes/aem-forms-hotfix.md).
* A **conversão de FORMS-23979** de HTML para PDF (PDFG) pode apresentar tempos limite intermitentes. Posteriormente, uma versão mais recente do complemento do Forms para SP24 foi lançada, que inclui a correção. Se você encontrar esse problema, atualize seu ambiente para o [complemento mais recente do Forms lançado para 6.5.25.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).
* **FORMS-23717** Depois de atualizar para o **AEM Forms6.5.25.0**, o `server.log` e o `error.log` podem ser inundados com mensagens de AVISO repetidas, como *Falha na criação de fábrica do analisador seguro* ou *Não há suporte para o atributo de segurança ...*. Os logs podem aumentar em cerca de **5-10 linhas por segundo** (centenas de MB por hora), o que pode preencher o disco e bloquear a implantação da produção.

Para reduzir o volume de log, defina o nível de log de `com.adobe.util.XMLSecurityUtil` como `ERROR` na configuração do servidor de aplicativos ou por meio do argumento JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Essa funcionalidade apenas oculta as mensagens e não corrige a causa subjacente.

* **FORMS-23875** Na pesquisa do Modelo de dados de formulário, a interface do usuário exibe uma marca HTML mesmo quando uma entidade relevante está ausente. Para resolver o problema, baixe e instale o hotfix do [link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Pacotes da OSGi e pacotes de conteúdo inclusos{#osgi-bundles-and-content-packages-included}

Os arquivos zip a seguir contêm os documentos de texto que listam os pacotes OSGi e os Pacotes de Conteúdo incluídos nesta versão do Service Pack do [!DNL Experience Manager] 6.5:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de Pacotes de Conteúdo incluídos no Experience Manager 6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites estão disponíveis somente para clientes do. Se você for cliente e precisar de acesso, entre em contato com o seu gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Fale com o suporte ao cliente da Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Inscreva-se para obter atualizações de produto prioritárias da Adobe](https://www.adobe.com/subscription/priority-product-update.html)



