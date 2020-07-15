---
title: Notas de versão do Service Pack do Adobe Experience Manager 6.5
description: Notas de versão específicas do Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a599a1c75a1933d6b21e60e96485f43a0aedd679
workflow-type: tm+mt
source-wordcount: '4496'
ht-degree: 6%

---


# Notas de versão do Service Pack do Adobe Experience Manager 6.5 {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.5.0 |
| Tipo | Lançamento do Service Pack |
| Data | 04 de junho de 2020 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## O que está incluído na Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

O Adobe Experience Manager 6.5.5.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização geral do lançamento do 6.5 em **abril de 2019**. Ele pode ser instalado na parte superior do Adobe Experience Manager 6.5.

Alguns dos principais recursos e melhorias introduzidos no Adobe Experience Manager 6.5.5.0 incluem:

* Personalize os nomes das colunas exibidas na Caixa de entrada do Adobe Experience Manager.

* Aprimoramento da acessibilidade em várias áreas da Gestão de conteúdo da Web para Experience Manager (WCM), como o Editor de páginas, Componentes principais, RTE e a interface de usuário do Administrador.

* Salve um [!DNL Interactive Communication] como rascunho.

* Suporte para [!DNL Oracle WebLogic 12] formulários Experience Manager em JEE.

* Aprimoramento da manipulação de exceções no fluxo da interface [!DNL Adobe Experience Manager Assets] do usuário.

* Para obter o URL de publicação do Dynamic Media Scene7, um novo método `getRemoteAssetPublishURL` é adicionado à `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` interface.

* [Aprimoramentos](#assets-6550) de acessibilidade em conformidade [!DNL Adobe Experience Manager Assets] com as Diretrizes de acessibilidade do conteúdo da Web (WCAG).

* Remoção da integração do Compartilhamento de pacotes no Adobe Experience Manager.

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.22.3.

Para obter uma lista completa dos recursos, destaques principais, recursos principais introduzidos no Experience Manager 6.5 service pack 5, consulte [Novidades do Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

A seguir está a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites fornece uma opção para publicar ou cancelar a publicação de uma página de seu alias. A opção não funciona (NPR-33415).
* Quando um container de layout é excluído de um modelo que contém vários modelos, o modelo não é renderizado corretamente (NPR-33347).
* Quando uma página Sites Experience Manager faz parte de um grande conjunto de conteúdo com várias cópias online, a pré-visualização do histórico de versão da página falha ao carregar (NPR-33311).
* Quando você usa o comando Mover para renomear uma página Sites de Experience Manager, o título da página não é atualizado (NPR-33264).
* Quando você move as páginas pela visualização da coluna, as colunas desaparecem (NPR-33216).
* Quando o nome de um componente local em uma cópia de idioma é idêntico ao nome de um componente no blueprint e o componente é lançado do blueprint, o termo não `_msm_moved` é adicionado ao nome do componente local (NPR-33208).
* O servlet de Redirecionamento de página anexa .html a um URL de Sites de Experience Manager, onde ResourceType não está `cq:Page` (NPR-33176).
* Ao colar uma subárvore, não há opção para decidir se as subpáginas correspondentes devem ser coladas ou não (NPR-33149).
* O número de resultados em usos ativos de um componente é limitado ao número 49 (NPR-33058).
* Quando você baseia um Fragmento de conteúdo em um schema e ele contém uma área de texto obrigatória ou um campo de caminho, o Fragmento de conteúdo não é salvo (NPR-33007).
* Quando você cria um componente personalizado usando o componente padrão do Fragmento de experiência e o usa em páginas Sites Experience Manager, o Experience Manager não exibe referências (uso) para o componente personalizado (NPR-32852).
* Ao renomear uma pasta com um grande número de referências, muitas referências à pasta não são atualizadas (NPR-32765).
* Quando você ativa a opção de edição de origem, ela fica disponível para opções de tela cheia em linha, mas permanece ausente na caixa de diálogo de edição e nas opções de tela cheia do editor de rich text (NPR-32763).
* Se você tiver um campo múltiplo e ele contiver um campo obrigatório (como um menu suspenso ou um campo de caminho) nas propriedades da página de um blueprint, quando uma página que contém esse campo múltiplo for distribuída, as propriedades da página da live copy não serão salvas (NPR-32751).
* Os leitores de tela não podem usar a estrutura de cabeçalho para navegar em uma página. Além disso, a guia Componentes tem o rótulo errado (NPR-32648).
* Quando start de paginação, o Seletor de fragmentos de experiência não carrega todos os itens (NPR-32605).
* As permissões do autor para ler, modificar, criar e excluir cópias online são revogadas. Cada autor tinha que fornecer permissões de leitura e modificação explícitas para mover páginas em um Blueprint (NPR-32550).
* Os autores de conteúdo não conseguem criar o Launch para uma página que tenha uma integração com o Adobe Analytics (NPR-32548).
* Quando um usuário retoma a herança com a sincronização, a cópia online da página pai não é sincronizada com o blueprint e exibe um status incorreto (NPR-32500).
* A página do editor de Sites Experience Manager demora mais de 15 segundos para carregar (NPR-32413).
* Determinados campos não exibem a opção Cancelar herança (NPR-32362).
* Quando você seleciona um caminho para um componente de Fragmento de experiência e seleciona a caixa de seleção Abrir caixa de diálogo de seleção, você não navega até o caminho selecionado no Navegador de caminhos (NPR-32308).
* Quando você atualiza do Experience Manager 6.2 para o Experience Manager 6.5, o componente Parsys dos modelos estáticos não é exibido corretamente. A altura do componente Parsys está definida como 0 e os componentes dentro dele não estão visíveis (NPR-33663).
* Quando um usuário copia e cola um Container de layout na mesma página, os componentes em um Container de layout não são exibidos (NPR-33648).
* A verificação de integridade do Dispatcher exibe a mensagem de `Invalid cookie header` aviso nos arquivos de registro (NPR-33629).

### [!DNL Assets] {#assets-6550}

**Aprimoramentos de acessibilidade nos ativos Experience Manager**

* Agora é possível colocar o foco do teclado na lista [!UICONTROL Comentários] e na opção clicável para [!UICONTROL Criar] comentários da versão em [!UICONTROL Criar nova versão] no painel Ativos da [!UICONTROL Linha] do tempo (NPR-33424).

* Agora é possível acessar a opção Configurações [!UICONTROL de] Visualização para ativos e alterar configurações na caixa de diálogo Configurações [!UICONTROL de] Visualização usando teclas do teclado (NPR-33420).

* O pop-up da caixa de lista da caixa de combinação (em vários campos em páginas diferentes) agora mostra as entradas como uma lista de opções que podem ser anunciadas pelos leitores de tela (NPR-33516).

* A funcionalidade de classificação dos cabeçalhos classificáveis (na visualização da lista, na visualização da [!UICONTROL Linha] do tempo e na página [!UICONTROL Gerenciar publicação] ) agora é anunciada pelos leitores de tela e os controles de classificação nos cabeçalhos das colunas são acessíveis usando o teclado (NPR-32979).

* Os elementos clicáveis, como cartões de comentário, atualizações de versão, caixas de combinação e ícones de divisa de menus, agora podem ser focados e interagir com o uso de um teclado (NPR-33514).

* A funcionalidade (ou finalidade de ação) dos ícones de insights (para uso, impressões e cliques) na Visualização [!UICONTROL do] Insights agora são anunciados corretamente pelos leitores de tela (NPR-33513).

* Campos de formulário somente leitura (por exemplo, campos desativados na guia  Básica de [!UICONTROL Propriedades]de ativos) agora são focalizáveis usando o teclado (NPR-33493, CQ-4273031).

* Rótulos em vários campos de entrada agora são rótulos permanentes (portanto acessíveis) e não apenas rótulos de espaço reservado, que desapareceram quando o texto foi digitado (NPR-33475).

* Níveis de cabeçalho diferentes (como títulos de página e cabeçalhos de seção) agora são percebidos como cabeçalhos com níveis diferentes para usuários de leitores de tela (NPR-33471).

* Elementos interativos da interface do usuário, como links e opções (no cabeçalho e nas opções de zoom da página de ativos, navegação de pastas), agora são acessíveis usando um teclado (NPR-33468, CQ-4271412).

* Os indicadores de progresso [!UICONTROL Opções], [!UICONTROL Escopo]e [!UICONTROL Workflows] na página [!UICONTROL Gerenciar publicação] agora são lidos corretamente pelos leitores de tela como indicadores de progresso, em vez de guias (NPR-33416).

* A cor dos ícones de classificação de estrelas (como na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] em [!UICONTROL Propriedades] do ativo ou na visualização do cartão) é alterada para que o contraste adequado seja visível aos usuários com visão limitada e sem percepção de cor (NPR-33414).

* A seta para cima ao lado do campo [!UICONTROL Comentário] na página de detalhes dos ativos agora pode ser acessada usando teclas do teclado (NPR-33397).

* Os estados expandidos e recolhidos da caixa de diálogo [!UICONTROL Tags] em [!UICONTROL Propriedades] do ativo e navegação do painel esquerdo (na interface do usuário do ativo) agora são anunciados corretamente pelos leitores de tela (NPR-33396).

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* Ao navegar pela estrutura de árvore, vários elementos do controle de visualização de árvore são anunciados corretamente pelos leitores de tela (NPR-33304).

* Diferentes versões de ativos na visualização da [!UICONTROL Linha] do tempo na página de detalhes de ativos agora estão acessíveis usando teclas de teclado (NPR-33283).

* Os nomes das sugestões de pesquisa que aparecem na caixa de combinação Omnisearch são anunciados pelos leitores de tela ao usar a funcionalidade de pesquisa (NPR-33280).

* Os elementos clicáveis e [!UICONTROL Ir para o link] no painel [!UICONTROL Referências] agora são anunciados pelos leitores de tela como elementos clicáveis (NPR-33278).

* As informações de estrutura de tabela (como linha 1, célula 1, tabela) da caixa de diálogo [!UICONTROL Compartilhar link] não são mais anunciadas pelos leitores de tela quando a caixa de diálogo é aberta (NPR-33268).

* A finalidade de vários elementos da caixa de combinação (como campo Caminho e opção para abrir a caixa de diálogo Seleção na guia Básica das Propriedades do ativo) agora são anunciados corretamente pelos leitores de tela (NPR-33235).

* As informações de que as linhas na tabela visualização da lista são selecionáveis agora são comunicadas aos usuários do leitor de tela quando o foco do teclado está sobre eles. Quando um ponteiro passa pelas linhas, os leitores de tela anunciam as informações (NPR-33234).

* As opções (com [!UICONTROL x]) para remover cada uma das tags selecionadas abaixo do campo [!UICONTROL Tags] na guia [!UICONTROL Básico] de [!UICONTROL Propriedades] agora estão acessíveis aos leitores de tela (NPR-33206).

* O seletor de datas do calendário agora é focalizável e acionável usando o teclado por usuários de leitores de tela e usuários de teclado com visão (NPR-33200).

* A alternância entre a visualização da lista e a visualização da placa agora expõe corretamente sua funcionalidade (de ajuste do visualização) ao leitor de tela (NPR-33069).

* O menu no painel esquerdo agora está acessível. A funcionalidade e o propósito de expandir o menu são anunciados adequadamente pelos leitores de tela (NPR-33068).

* A caixa de Lista e muitos outros elementos da interface do usuário agora estão acessíveis para usuários que não visualizam a tela, e as seguintes informações sobre eles são anunciadas pelos leitores de tela (NPR-33040):

   * se a entrada do usuário é necessária em um elemento antes do envio do formulário.
   * se um elemento não é editável.
   * se um widget está selecionado ou não.

* A opção de abrir a barra lateral do filtro agora pode ser acessada usando o teclado (NPR-32842, CQ-4273018).

* O controle de caixa de seleção no cabeçalho da coluna da visualização de lista agora está acessível e a finalidade de usar o controle é anunciada pelos leitores de tela (NPR-32722, NPR-33005).

* Rótulos para os campos de horas (HH) e minutos (mm) no seletor de datas do calendário agora são rótulos permanentes em vez de rótulos de espaço reservado, e não desaparecem quando o usuário digita texto nesses campos (NPR-32720).

* O texto dos links de notificações (que aparecem depois de clicar no ícone de sino) agora é anunciado aos usuários de leitores de tela, que usam a guia para acessar cada link (NPR-32645).

* [!UICONTROL As opções Selecionar], [!UICONTROL Baixar], [!UICONTROL Propriedades]e [!UICONTROL Mais ações] em cartões de ativos na Visualização [!UICONTROL do] Insights agora estão acessíveis usando o teclado (NPR-32609).

* O conteúdo oculto visualmente (como o conteúdo da barra de menus do cabeçalho nos resultados da pesquisa) não é mais anunciado pelos leitores de tela quando acessados usando o teclado (NPR-32606).

* A finalidade das etiquetas nos controles para ir para os meses seguinte e anterior no seletor de datas do calendário agora é anunciada pelos leitores de tela (NPR-32604).

* Os ícones de classificação de estrelas agora são focalizáveis e acionáveis usando teclas de teclado (NPR-32513).

* A funcionalidade para controlar o volume do vídeo agora está acessível por meio da guia (para focalizar no controle deslizante do volume) e das teclas de seta (para ajustar o volume) no teclado (NPR-32065).

* A finalidade dos campos de entrada de limite inferior ([!UICONTROL De]) e limite superior ([!UICONTROL To]) do filtro Tamanho do arquivo agora é anunciada para usuários leitores de tela sem visão (NPR-32064).

* O menu [!UICONTROL Idiomas] no formulário [!UICONTROL Criar e traduzir] agora está acessível aos leitores de tela no modo de navegação (CQ-4293906).

* O painel [!UICONTROL Referências] agora está acessível com os seguintes aprimoramentos (NPR-33261, CQ-4293798):

   * No modo de navegação, o foco do leitor de tela não se move mais para campos de edição ocultos em Referências [!UICONTROL ao]site, Referências [!UICONTROL ao]ativo, [!UICONTROL Cópias]e Referências [!UICONTROL ao] formulário.

   * Os leitores de tela agora anunciam a função dos elementos Referências [!UICONTROL do] site e Cópias [!UICONTROL de] idioma.

   * O foco dos leitores de tela no modo de navegação muda em uma sequência significativa para vários elementos.

* [!UICONTROL A página do Editor] de Schemas de metadados e seus elementos agora estão acessíveis usando o teclado e são compatíveis com o leitor de tela (CQ-4290962, CQ-4272953).

* A finalidade do `X` símbolo para remover as tags selecionadas agora é anunciada pelos leitores de tela, juntamente com o número de tags selecionadas (CQ-4273017).

* Para evitar confusão para usuários sem visão usando leitores de tela, ícones decorativos e imagens agora são ignorados pelos leitores de tela (CQ-4272944).

**Problemas corrigidos nos ativos Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Os ativos fornecem correções para os seguintes problemas:

* [!UICONTROL A opção Start] na caixa de diálogo [!UICONTROL Criar fluxo de trabalho] para ativos em uma coleção está desativada, impedindo assim que o fluxo de trabalho seja acionado (NPR-32471).

* Ao usar o pop-up em cascata em schemas de metadados, ao selecionar e salvar uma opção suspensa que contém um apóstrofo (do menu suspenso filho), a opção de apóstrofo selecionada desaparece após reabrir [!UICONTROL Propriedades] do ativo (NPR-32649).

* [!UICONTROL A tarefa] de sincronização do Asset Insights será interrompida e falhará se encontrar entradas inválidas (no lado do Analytics) em vez de mover-se para a próxima entrada (NPR-32674).

* O giroscópio não é funcional, pois os sensores de movimento são desativados por padrão nos navegadores móveis no visualizador panorâmico (CQ-4272937).

* [!UICONTROL O Assistente de configuração] de ativos conectados falha ao funcionar com o erro 404, ao instalar a versão 6.5.3 na versão 6.5.1 (NPR-32730).

* Durante o processo de gravação de retorno XMP, todas as propriedades de metadados de namespace personalizados alteram o prefixo de namespace personalizado para ns2 em vez do prefixo de namespace configurado (NPR-32748).

* O carregamento lento não é acionado e somente 100 ativos são exibidos ao selecionar para revisar as tarefas da caixa de entrada de notificações (NPR-32750).

* `NullPointerException` for observado devido a preferências de nó ausentes no perfil de usuário recém-criado (SAML/SSO). Esse erro impede que usuários recém-conectados usem a [!DNL Adobe Experience Manager Stock] integração (NPR-32777).

* Os avisos transversais são observados nos registros ao abrir uma coleção inteligente que contém mais de 10.000 ativos (NPR-32980).

* Os nomes dos ativos são alterados para minúsculas ao mover ativos de uma pasta para outra no modo de execução Dynamic Media Scene7 (NPR-32995). [!DNL Adobe Experience Manager]

* Um ativo pesquisado não pode ser excluído depois de navegar para suas propriedades a partir dos resultados da pesquisa e voltar para os resultados da pesquisa para excluí-lo (NPR-32998).

* [!UICONTROL A opção Próxima] permanece desativada ao selecionar a pasta de destino na interface [!UICONTROL Mover ativos] (NPR-33356).

* [!UICONTROL A opção Próxima] não está ativada na seleção do nó pai (onde a pasta filho único está visível) e na seleção da pasta filho (NPR-33275).

* As permissões de check-in e check-out são desativadas no Adobe Asset Link (AAL) para usuários com permissão de exclusão, mesmo se outras permissões, como ler, criar ou modificar, forem concedidas (NPR-33272).

* As execuções de Recorte inteligente não estão disponíveis na caixa de diálogo de download de ativos (NPR-33167).

* Exceção observada em registros ao abrir o painel de execuções para um PDF em uma pasta com perfil de recorte inteligente (CQ-4294201).

* As predefinições de imagem não publicam, se o modo [!UICONTROL de sincronização] Dynamic Media estiver desativado por padrão no Experience Manager com o modo de execução Dynamic Media Scene7 (CQ-4294200).

* O processamento de ativos enquanto o upload em massa fica travado e a instância do fluxo de trabalho mostra instâncias presas do ativo de atualização do DAM (CQ-4293916).

* A criação de uma configuração Dynamic Media no Experience Manager funciona, mas na interface do usuário nada acontece ao selecionar Salvar (CQ-4292442).

* A Pré-visualização de ativos de vídeo F4V não está funcionando na reprodução progressiva no Safari/Mac (CQ-4289844).

* A pasta extra é criada ao recortar inteligente um ativo que está dentro de uma pasta pai com `.` caractere de ponto em seu nome (CQ-4289337).

* A miniatura está quebrada e o banner de processamento de vídeo não é exibido quando um vídeo é copiado (CQ-4284125).

* O visualizador dimensional exibe incorretamente miniaturas vazias no Firefox para alguns modelos com visualizações de câmera vazias (CQ-4283447).

* Problemas de desempenho corrigidos na versão 6.5.5.0 são (CQ-4279206):

   * Leva muito tempo para carregar binários grandes para os servidores de processamento de imagem da Dynamic Media.

   * O tempo de geração de miniaturas no Experience Manager aumenta devido à arquitetura Dynamic Media Scene7.

* Os problemas de migração do Dynamic Media Scene7 falham para clientes com um grande número de ativos (CQ-4279206).

* O layout do visualizador do vídeo 360 será quebrado se `setVideo` for usado e o vídeo será mudado para baixo ao usar `video= modifier` (CQ-4263201).

* Uma mensagem de erro é exibida durante a instalação do pacote Experience Manager SDL (NPR-33175).

### Plataforma {#platform-6550}

* O [!DNL Sling] filtro não será chamado se a entrada do `sling:match` mapa for criada em `/etc/maps` (NPR-33362).
* Falha de Experience Manager devido a falha de segmentação com [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacote principal ausente do arquivo Experience Manager uberjar (NPR-32848).
* O CRXDE Lite não carrega conteúdo para usuários sem permissão de leitura na `jcr:primaryType` propriedade de um nó (NPR-32611).
* [!DNL Granite] o scheduler da tarefa de manutenção é reinicializado com muita frequência durante implantações de Experience Manager (CQ-4294627).
* Quando um query SQL é executado por um longo tempo, por exemplo, 7 horas, o Experience Manager para de responder (NPR-33044).

### Interface do usuário {#ui-6550}

* A seleção de botões de opção não persiste em um campo múltiplo (NPR-33309).
* O limite de carregamento lento não funciona para a visualização da lista (NPR-33124).
* A página de resultados do Omnisearch não exibe uma mensagem se não houver correspondências (NPR-32974).
* O filtro Omnisearch retorna todas as correspondências em `/content` nós ignorando o local selecionado (NPR-32849).

### Integrações {#integrations-6550}

* O cache interno é apagado quando uma página com um componente Adobe Target é publicada (NPR-33162).
* A integração com o Adobe Target não funciona no [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Ao configurar o Adobe Target, os campos [!UICONTROL Empresa] e Conjunto [!UICONTROL de] relatórios não aparecem ao selecionar uma fonte de relatórios (NPR-32502).
* Ao exportar [!DNL Experience Fragments] usando a E/S da Adobe, metadados como Produto de origem não são exportados para o Adobe Target (NPR-32159).
* Os usuários autorizados do IMS no grupo de administração de Experience Manager local não podem criar ou modificar configurações do IMS (NPR-33045).
* A página de configurações do Adobe Launch não exibe todos os registros (NPR-33011).
* Os usuários do grupo de autores de conteúdo não podem editar as propriedades de um componente Adobe Target devido ao erro de JavaScript (NPR-32996).

### Projetos de tradução {#translation-6550}

* As tags traduzidas não são importadas para o Experience Manager de serviços de tradução de terceiros (NPR-33154).
* A página de configuração de tradução exibe um provedor de tradução incorreto que o usado para a tradução (NPR-32971).
* Adicionar uma pasta de fragmento de experiência a um projeto de tradução existente cria um novo projeto (NPR-32843).
* Um `NullPointerException` erro é visto nos registros ao executar um trabalho de tradução (NPR-32628).

### WCM {#wcm-6550}

* Editor de páginas - O Editor de [!DNL Sites] páginas não permite que os usuários somente do teclado pulem para o conteúdo principal em vez de deslocar o foco da guia por todas as opções disponíveis no cabeçalho (CQ-4293883).
* Editor de páginas - Os painéis que usam o componente Bem e incluem dados salvos não são exibidos devido a atualizações em [!DNL Chrome] e [!DNL Firefox] versões (CQ-4292995).
* MSM - A exclusão de um componente da página não exclui o componente da versão publicada da página (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Remover um schema de metadados publicado [!DNL Brand Portal] resulta em um erro (CQ-4292063).
* Se um administrador configurar [!DNL Experience Manager Assets] 6.5.4 com o Brand Portal via Adobe Developer Console, o [!DNL Brand Portal] usuário não poderá publicar o ativo de uma pasta de contribuição de [!DNL Brand Portal] para [!DNL Experience Manager] (NPR-33046).
* Replicação de Duplicado das pastas pai que causam conflitos (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Não é possível excluir um cartão no console de moderação usando a opção de menu de edição rápida (NPR-33117).
* Ocorre um erro ao acessar a página [!UICONTROL Atividade Stream] (NPR-33146).
* Grupos excluídos na instância do autor não são removidos de todas as instâncias de publicação (NPR-33199).
* Após a criação de um novo grupo, os autores não são redirecionados para a seção Grupo [!UICONTROL da] Comunidade no [!DNL Internet Explorer] 11 (NPR-33205).
* O acesso a uma mensagem na Caixa de entrada do Experience Manager não altera o status da mensagem para Lido (NPR-32764).
* Editar um [!DNL Communities] grupo e alterar a imagem em miniatura não atualiza a imagem em miniatura do grupo (NPR-32599).
* Um usuário não pode enviar um email para outro usuário em uma comunidade (NPR-32598).
* Um blog enviado não é exibido até que o usuário atualize a página (NPR-32391).
* Ao criar uma versão de notificações e subscrições de Conteúdo gerado pelo usuário (UGC), uma ID incorreta da página de origem é armazenada (CQ-4279355, CQ-4289703).

### Fluxo de trabalho {#workflow-6550}

* A opção [!UICONTROL Linha] do tempo no painel esquerdo leva mais tempo para carregar do que o esperado (NPR-32851).
* Após reiniciar uma instância do Experience Manager, o email para a tarefa de revisão de uma coleção inclui um link de carga incorreto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>O Experience Manager Service Pack não inclui correções para [!DNL Forms]. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o AEM Forms no JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gerenciamento de correspondência: A ordem dos ativos em uma área do público alvo é embaralhada após a submissão de uma carta (NPR-33359, NPR-33153).
* Formulários adaptativos: Quando um usuário edita um formulário adaptável, a opção Fluxo de trabalho [!UICONTROL do] Start disponível no menu Informações [!UICONTROL da] página não funciona (NPR-33004).
* Formulários adaptativos: O usuário não pode salvar um formulário adaptável com mais de um anexo (NPR-32997).
* Formulários adaptativos: A alteração do layout do painel em um formulário adaptável resulta em um erro (CQ-4293880).
* Formulários adaptativos: Uma nova linha de uma string em um dicionário de formulários adaptáveis adiciona `&#xa;` caracteres ao dicionário (NPR-33266).
* Acessibilidade aos formulários adaptáveis: Quando um usuário pré-visualização um formulário adaptável como um formulário HTML, o campo Assinatura [!UICONTROL em] script não consegue manter o foco da guia (NPR-33159).
* Acessibilidade aos formulários adaptáveis: As mensagens de erro exibidas ao enviar um formulário adaptável não vinculam a um `aria-describedBy` atributo (NPR-33071).
* Acessibilidade aos formulários adaptáveis: Os campos marcados como obrigatórios em um formulário adaptável não têm o atributo obrigatório definido como True no schema de acessibilidade ARIA (NPR-33070).
* Serviço PDFG: Quando um usuário converte um arquivo de texto em PDF, os caracteres japoneses não são renderizados corretamente (NPR-33238).
* Serviço PDFG: `CreatePDF` falha ao converter um arquivo PDF em formato OCR PDF (NPR-32994).
* Serviço PDFG: Falha na conversão de PDF para a 200ª instância de um [!DNL OpenOffice] documento (NPR-32766).
* BackendIntegration: As solicitações do modelo de dados de formulário falham, pois o token de atualização expira devido ao estado inativo incorreto (NPR-33169).
* Designer: Os leitores de tela executam a ordem de tabulação com base na ordem geográfica padrão em vez da ordem de tabulação personalizada definida no arquivo XDP (NPR-32160).
* Designer: Se a opção de marcação estiver ativada, a borda do subformulário desaparecerá na saída PDF gerada (NPR-32778).

## Install 6.5.5.0 {#install}

**Requisitos de configuração**

* AEM 6.5.5.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* O download do service pack está disponível na Distribuição [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)software da Adobe.
* Em uma implantação com MongoDB e várias instâncias, instale o AEM 6.5.5.0 em uma das instâncias do autor usando o Gerenciador de pacotes.
* Antes de instalar, faça um instantâneo ou um backup atualizado da sua instância do AEM.
* Reinicie a instância antes da instalação. Embora isso seja necessário apenas quando a instância ainda está no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior), é recomendável se a instância estava em execução por um período mais longo.

>[!NOTE]
>
>A Adobe não recomenda remover ou desinstalar o pacote Adobe Experience Manager 6.5.5.0.

### Instale o Service Pack {#install-service-pack}

Execute as seguintes etapas para instalar o Service Pack em uma instância existente do Adobe Experience Manager 6.5:

1. Baixe o service pack da [Software Distribution (Distribuição](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip)de software).

1. Abra o Gerenciador de pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote. Para saber como usá-lo, consulte [Gerenciador](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)de pacotes.

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Package Manager sai durante a instalação do service pack. A Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Instalação automática**

Há duas maneiras de instalar automaticamente o Adobe Experience Manager 6.5.5.0 em uma instância em funcionamento:

A. Coloque o pacote na `../crx-quickstart/install` pasta quando o servidor estiver disponível on-line. O pacote é instalado automaticamente.

B. Use a API [HTTP do Gerenciador](https://docs.adobe.com/content/docs/pt/crx/2-3/how_to/package_manager.html)de pacotes. Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.5.0 não suporta a instalação do Bootstrap.

**Validar instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.5.0)` em Produtos instalados.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. The OSGI bundle `org.apache.jackrabbit.oak-core` is version 1.22.3 or higher (Use Web Console: `/system/console/bundles`).

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

### Instale o pacote de complementos Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms. Correções no Adobe Experience Manager Forms são entregues por meio de um pacote complementar separado.

1. Verifique se você instalou o Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalar formulários Adobe Experience Manager no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções no Adobe Experience Manager Forms em JEE são entregues por meio de um instalador separado.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/br/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.5.0 está disponível no repositório [do](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)Adobe Public Maven.

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Recursos obsoletos {#removed-deprecated-features}

Esta seção lista recursos e recursos que foram marcados como obsoletos com o AEM 6.5.5.0. Os recursos que estão planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma opção alternativa a ser usada.

Recomenda-se que os clientes revisem se utilizam o recurso ou a capacidade em sua implantação atual e façam planos para alterar sua implementação para usar a opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | A tela Aceitação **[!UICONTROL de]** AEM cloud services está obsoleta. Com a integração do AEM e do Público alvo atualizada no AEM 6.5 para suportar a API do Target Standard, que usa autenticação por meio do Adobe IMS e E/S, e a função crescente do Adobe Launch para instrumentar páginas do AEM para análise e personalização, o assistente de opção de participação se tornou funcionalmente irrelevante. | Configure as conexões do sistema, a autenticação do Adobe IMS e as integrações de E/S da Adobe por meio dos respectivos AEM cloud services. |
| Conectores | O Adobe JCR Connector para Microsoft SharePoint 2010 e Microsoft SharePoint 2013 foi descontinuado para o AEM 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* Se você estiver instalando [!DNL Experience Manager] 6.5.5.0 com [!DNL Java] 11, reinicie o servidor após instalar o Service Pack. Não é necessário reiniciar se você estiver instalando o Service Pack com [!DNL Java] 8.

* Se uma pasta na hierarquia for renomeada [!DNL Experience Manager Assets] e a pasta aninhada que contém um ativo for publicada, o título da pasta não será atualizado [!DNL Brand Portal][!DNL Brand Portal] até que a pasta raiz seja publicada novamente.

* Ao instalar o AEM 6.5.5.0, a atualização da [!DNL Chrome] versão 83 está causando um problema na criação de pacotes. Use outros navegadores disponíveis, como [!DNL Internet Explorer] e [!DNL Firefox], ou outras opções de instalação de pacote padrão do AEM para resolver o problema. O problema é resolvido após a instalação do AEM 6.5.5.0.

* Não é possível enviar um email para o servidor SMTP remoto usando o remetente de email padrão do AEM, pois ele permite apenas a comunicação usando TLS v1.2. Remova o pacote `javax.mail:mail:1.5.0-b01` de `system/console` e atualize os pacotes para resolver o problema.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Se o assistente de configuração [!UICONTROL de ativos] conectados retornar uma mensagem de erro 404 após a instalação, reinstale manualmente os pacotes `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` pacotes usando o Gerenciador de pacotes.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do AEM 6.5.x.x:
   * &quot;Quando a integração do Target é configurada no AEM usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granito/operações/manutenção.
   * A validação do lado do servidor do Formulário adaptável falha quando funções de agregação, como SUM, MAX e MIN são usadas. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Não foram encontradas janelas de manutenção em granito/operações/manutenção.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner que pode ser comprado.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no AEM 6.5.5.0:

* [Lista de pacotes OSGi incluídos no AEM 6.5.5.0](assets/6550_bundles.txt)

* [Lista de pacotes de conteúdo incluídos no AEM 6.5.5.0](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

Estes sites estão disponíveis somente para clientes. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o suporte](https://docs.adobe.com/content/help/en/customer-one/using/home.html)ao cliente Para obter mais informações sobre como acessar o portal de suporte, consulte [Acesso ao portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de suporte.

>[!MORELIKETHIS]
>
>* [Notas de versão do AEM 6.5](/help/release-notes/release-notes.md)
>* [Página do produto AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentação do AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

