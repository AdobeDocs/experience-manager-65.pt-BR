---
title: '[!DNL Adobe Experience Manager] 6.5 Notas de versão anteriores do Service Pack.'
description: Notas de versão para [!DNL Adobe Experience Manager] 6.5 Service Packs.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 5db4dd7ccc7d722f0503b22fdd5ff9e5508be4ea
workflow-type: tm+mt
source-wordcount: '11482'
ht-degree: 26%

---


# Correções e Feature Packs incluídos em Pacotes de serviço anteriores {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

O Adobe Experience Manager 6.5.5.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização geral do lançamento do 6.5 em **abril de 2019**. Ele pode ser instalado no Adobe Experience Manager 6.5.

Alguns dos principais recursos e melhorias introduzidos na versão [!DNL Adobe Experience Manager] 6.5.5.0 incluem:

* O acesso anônimo ao CRXDE Lite não é permitido. Em vez disso, os usuários são direcionados para a tela de logon. Consulte [Desenvolvimento com CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Personalize os nomes das colunas exibidas na [!DNL Adobe Experience Manager] Caixa de entrada.

* Aprimoramento da acessibilidade em várias áreas da Gestão de conteúdo da Web para Experience Manager (WCM), como o Editor de páginas, Componentes principais, RTE e a interface do usuário de administração.

* Salve um [!DNL Interactive Communication] como rascunho.

* Suporte para [!DNL Oracle WebLogic 12] Experience Manager Forms em JEE.

* Aprimoramento da manipulação de exceções no fluxo da interface [!DNL Adobe Experience Manager Assets] do usuário.

* Para obter o URL de publicação do Dynamic Media Scene7, um novo método `getRemoteAssetPublishURL` é adicionado à `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` interface.

* [Aprimoramentos](#assets-6550) de acessibilidade em conformidade [!DNL Adobe Experience Manager Assets] com as Diretrizes de acessibilidade do conteúdo da Web (WCAG).

* Remoção da integração do Compartilhamento de pacotes do Adobe Experience Manager.

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
* A verificação de integridade do Dispatcher exibe uma mensagem de `Invalid cookie header` aviso nos arquivos de registro (NPR-33629).
* XSS refletido em PreferencesServlet (NPR-33438).
* Os usuários anônimos podem acessar os recursos do CRXDE Lite (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Os usuários do Windows de [!DNL Experience Manager desktop app] são aconselhados a atualizar para o aplicativo de [desktop versão 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) para acessar o repositório DAM na [!DNL Adobe Experience Manager 6.5.5.0] instância. Como eles podem encontrar problemas ao acessar o repositório DAM na instância [!DNL Adobe Experience Manager] 6.5.5.0 usando o aplicativo desktop versão 2.0.2.

**Aprimoramentos de acessibilidade nos ativos Experience Manager**

* Agora é possível colocar o foco do teclado na lista [!UICONTROL Comentários] e na opção clicável para [!UICONTROL Criar] comentários da versão em [!UICONTROL Criar nova versão] no painel Ativos da [!UICONTROL Linha] do tempo (NPR-33424).

* Agora é possível acessar a opção Configurações [!UICONTROL de] Visualização para ativos e alterar configurações na caixa de diálogo Configurações [!UICONTROL de] Visualização usando teclas de teclado (NPR-33420).

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

* A caixa de lista e muitos outros elementos da interface do usuário agora estão acessíveis para usuários que não visualizam o leitor de tela, e as seguintes informações sobre eles são anunciadas pelos leitores de tela (NPR-33040):

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

* [!UICONTROL A opção start] na caixa de diálogo [!UICONTROL Criar fluxo de trabalho] para ativos em uma coleção está desativada, impedindo assim que o fluxo de trabalho seja acionado (NPR-32471).

* Ao usar o pop-up em cascata em schemas de metadados, ao selecionar e salvar uma opção suspensa que contém um apóstrofo (do menu suspenso filho), a opção de apóstrofo selecionada desaparece após reabrir [!UICONTROL Propriedades] do ativo (NPR-32649).

* [!UICONTROL A tarefa] de sincronização do Asset Insights será interrompida e falhará se encontrar entradas inválidas (no lado do Analytics) em vez de mover-se para a próxima entrada (NPR-32674).

* O giroscópio não é funcional, pois os sensores de movimento são desativados por padrão nos navegadores móveis no visualizador panorâmico (CQ-4272937).

* [!UICONTROL O Assistente de configuração] de ativos conectados falha ao funcionar com o erro 404, ao instalar a versão 6.5.3 na versão 6.5.1 (NPR-32730).

* Durante o processo de gravação XMP, todas as propriedades personalizadas de metadados de namespace alteram o prefixo de namespace personalizado para ns2 em vez do prefixo de namespace configurado (NPR-32748).

* O carregamento lento não é acionado e somente 100 ativos são exibidos ao selecionar para revisar as tarefas da caixa de entrada de notificações (NPR-32750).

* `NullPointerException` for observado devido a preferências de nó ausentes no perfil de usuário recém-criado (SAML/SSO). Esse erro impede que usuários recém-conectados usem a [!DNL Adobe Experience Manager Stock] integração (NPR-32777).

* Os avisos transversais são observados nos registros ao abrir uma coleção inteligente que contém mais de 10.000 ativos (NPR-32980).

* Os nomes dos ativos são alterados para minúsculas ao mover ativos de uma pasta para outra no modo de execução [!DNL Adobe Experience Manager] do Dynamic Media Scene7 (NPR-32995).

* Um ativo pesquisado não pode ser excluído depois de navegar para suas propriedades a partir dos resultados da pesquisa e voltar para os resultados da pesquisa para excluí-lo (NPR-32998).

* [!UICONTROL A opção Próxima] permanece desativada ao selecionar a pasta de destino na interface [!UICONTROL Mover ativos] (NPR-33356).

* [!UICONTROL A opção Próxima] não está ativada na seleção do nó pai (onde a pasta filho único está visível) e na seleção da pasta filho (NPR-33275).

* As permissões de check-in e check-out são desativadas no Adobe Asset Link (AAL) para usuários com permissão de exclusão, mesmo se outras permissões, como ler, criar ou modificar, forem concedidas (NPR-33272).

* As execuções de Recorte inteligente não estão disponíveis na caixa de diálogo de download de ativos (NPR-33167).

* Exceção observada em registros ao abrir o painel de execuções para um PDF em uma pasta com perfil de recorte inteligente (CQ-4294201).

* As predefinições de imagem não publicam, se o modo [!UICONTROL de sincronização de Mídia] dinâmica estiver desativado por padrão no Experience Manager com o modo de execução do Dynamic Media Scene7 (CQ-4294200).

* O processamento de ativos enquanto o carregamento em massa fica travado e a instância do fluxo de trabalho mostra instâncias presas do ativo de atualização do DAM (CQ-4293916).

* A criação de uma configuração de Dynamic Media no Experience Manager funciona, mas na interface do usuário nada acontece ao selecionar Salvar (CQ-4292442).

* A pré-visualização de ativos de vídeo F4V não está funcionando na reprodução progressiva no Safari/Mac (CQ-4289844).

* A pasta extra é criada ao recortar inteligente um ativo que está dentro de uma pasta pai com `.` caractere de ponto em seu nome (CQ-4289337).

* A miniatura está quebrada e o banner de processamento de vídeo não é exibido quando um vídeo é copiado (CQ-4284125).

* O visualizador dimensional exibe incorretamente miniaturas vazias no Firefox para alguns modelos com visualizações de câmera vazias (CQ-4283447).

* Problemas de desempenho corrigidos na versão 6.5.5.0 são (CQ-4279206):

   * O carregamento de binários grandes leva muito tempo para os servidores de processamento de imagem de Dynamic Media.

   * O tempo de geração de miniaturas no Experience Manager aumenta devido à arquitetura do Dynamic Media Scene7.

* Problemas de migração do Dynamic Media Scene7 falham para clientes com um grande número de ativos (CQ-4279206).

* O layout do visualizador do vídeo 360 será quebrado se `setVideo` for usado e o vídeo será mudado para baixo ao usar `video= modifier` (CQ-4263201).

* Uma mensagem de erro é exibida durante a instalação do pacote Experience Manager SDL (NPR-33175).

* Vulnerabilidade SSRF no Experience Manager (NPR-33435).

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
* A integração com a Adobe Target não funciona no [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Ao configurar o Adobe Target, os campos [!UICONTROL Empresa] e Conjunto [!UICONTROL de] relatórios não aparecem ao selecionar uma fonte de relatórios (NPR-32502).
* Ao exportar [!DNL Experience Fragments] usando E/S de Adobe, metadados como Produto de origem não são exportados para o Adobe Target (NPR-32159).
* Os usuários autorizados do IMS no grupo de administração de Experience Manager local não podem criar ou modificar configurações do IMS (NPR-33045).
* A página de configurações de inicialização de Adobe não exibe todos os registros (NPR-33011).
* Os usuários do grupo de autores de conteúdo não podem editar as propriedades de um componente Adobe Target devido ao erro de JavaScript (NPR-32996).
* Scripts entre sites para JSON (NPR-32744).

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
* Se um administrador configurar [!DNL Experience Manager Assets] 6.5.4 com o Brand Portal por meio do Console do desenvolvedor do Adobe, o [!DNL Brand Portal] usuário não poderá publicar o ativo de uma pasta de contribuição de [!DNL Brand Portal] para [!DNL Experience Manager] (NPR-33046).
* Replicação de duplicado das pastas pai que causam conflitos (NPR-33001).

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
* Problema de script entre sites (NPR-33203).

### Fluxo de trabalho {#workflow-6550}

* A opção [!UICONTROL Linha] do tempo no painel esquerdo leva mais tempo para carregar do que o esperado (NPR-32851).
* Após reiniciar uma instância do Experience Manager, o email para a tarefa de revisão de uma coleção inclui um link de carga incorreto (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>O Experience Manager Service Pack não inclui correções para [!DNL Forms]. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o AEM Forms no JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gerenciamento de correspondência: A ordem dos ativos em uma área do público alvo é embaralhada após a submissão de uma carta (NPR-33359, NPR-33153).
* Forms adaptável: Quando um usuário edita um formulário adaptável, a opção Fluxo de trabalho [!UICONTROL do] Start disponível no menu Informações [!UICONTROL da] página não funciona (NPR-33004).
* Forms adaptável: O usuário não pode salvar um formulário adaptável com mais de um anexo (NPR-32997).
* Forms adaptável: A alteração do layout do painel em um formulário adaptável resulta em um erro (CQ-4293880).
* Forms adaptável: Uma nova linha de uma string em um dicionário de formulários adaptáveis adiciona `&#xa;` caracteres ao dicionário (NPR-33266).
* Acessibilidade adaptativa ao Forms: Quando um usuário pré-visualização um formulário adaptável como um formulário HTML, o campo Assinatura [!UICONTROL em] script não consegue manter o foco da guia (NPR-33159).
* Acessibilidade adaptativa ao Forms: As mensagens de erro exibidas ao enviar um formulário adaptável não vinculam a um `aria-describedBy` atributo (NPR-33071).
* Acessibilidade adaptativa ao Forms: Os campos marcados como obrigatórios em um formulário adaptável não têm o atributo obrigatório definido como True no schema de acessibilidade ARIA (NPR-33070).
* Serviço PDFG: Quando um usuário converte um arquivo de texto em PDF, os caracteres japoneses não são renderizados corretamente (NPR-33238).
* Serviço PDFG: `CreatePDF` falha ao converter um arquivo PDF em formato OCR PDF (NPR-32994).
* Serviço PDFG: Falha na conversão de PDF para a 200ª instância de um [!DNL OpenOffice] documento (NPR-32766).
* BackendIntegration: As solicitações do modelo de dados de formulário falham, pois o token de atualização expira devido ao estado inativo incorreto (NPR-33169).
* Designer: Os leitores de tela executam a ordem de tabulação com base na ordem geográfica padrão em vez da ordem de tabulação personalizada definida no arquivo XDP (NPR-32160).
* Designer: Se a opção de marcação estiver ativada, a borda do subformulário desaparecerá na saída PDF gerada (NPR-32778).
* XSS armazenado com o GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

O Adobe Experience Manager 6.5.4.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e desempenho, estabilidade, melhorias de segurança, lançadas desde a disponibilização geral do lançamento do 6.5 em **abril de 2019**. Ele pode ser instalado no Adobe Experience Manager 6.5.

Alguns dos principais recursos e melhorias introduzidos no Adobe Experience Manager 6.5.4.0 incluem:

* O Adobe Experience Manager Assets agora está configurado com o Brand Portal por meio do Console de E/S do Adobe.

* Uma nova etapa [Gerar saída](../forms/using/aem-forms-workflow-step-reference.md) imprimível agora está disponível para workflows Adobe Experience Manager Forms.

* [Suporte](../forms/using/resize-using-layout-mode.md) para várias colunas no modo de layout para formulários adaptáveis e Comunicações interativas.

* Suporte para [Rich Text](../forms/using/designing-form-template.md) em formulários HTML5.

* [Aprimoramentos](new-features-latest-service-pack.md#accessibility-enhancements) de acessibilidade nos ativos Experience Manager.

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.8.

* Agora é possível sincronizar subárvores de conteúdo seletivo para o modo *Mídia* dinâmica - Scene7 em vez de todos os disponíveis em `content/dam`.

* A integração do modelo de dados de formulário com o serviço da Web SOAP agora oferece suporte a grupos de escolha ou atributos em elementos.

* A entrada ou saída SOAP e estruturas de dados complexas agora suportam Substituição de Grupo Dinâmico.

Para obter uma lista completa dos recursos e dos principais destaques introduzidos nos service packs mais recentes, consulte [Novidades dos service packs](new-features-latest-service-pack.md)Adobe Experience Manager 6.5.

### Sites {#sites-fixes}

* Quando um URL de uma página do Adobe Experience Manager Sites contém dois pontos (`:`) ou símbolo de porcentagem (`%`), o navegador para de responder e picos de uso da CPU (NPR-32369, NPR-31918).

* Quando uma página Sites de Experience Manager é aberta para edição e um componente é copiado, a ação de colar permanece indisponível para alguns espaços reservados (NPR-32317).

* Quando o assistente Gerenciar publicação é aberto, um Fragmento de experiência vinculado a um Componente principal não é exibido nas listas de referências publicadas (NPR-32233).

* A visão geral da Live Copy na interface do usuário de toque demora muito mais do que a interface clássica para renderizar (NPR-32149).

* Quando a hora do servidor e a hora da máquina estiverem em fusos horários diferentes, a hora de publicação programada exibe a hora do servidor na interface do usuário de toque, enquanto na interface clássica, a hora da máquina é exibida (NPR-32077).

* Falha do Sites Experience Manager ao abrir uma página com um sufixo no URL (NPR-32072).

* Quando um usuário edita um Fragmento de conteúdo, uma variação excluída do Fragmento de conteúdo é restaurada (NPR-32062).

* Os usuários podem salvar um Fragmento de conteúdo sem fornecer informações nos campos obrigatórios (NPR-31988).

* kernel.js e ui.js não são pré-cumpridos ou armazenados em cache. Leva a mais tempo na renderização de páginas (NPR-31891).

* Quando PageEventAuditListener está ativado, o comprimento da fila de confirmação aumenta. Isso afeta o desempenho de muitas operações, como publicação em massa, navegação, movimentação de ativos em massa (NPR-31890).

* Quando os Fragmentos de experiência são arrastados, é observado um tempo de resposta elevado (NPR-31878).

* Quando você seleciona a opção Arrastar o componente aqui no espaço reservado de uma grade responsiva, uma solicitação de GET é enviada e a solicitação resulta em erro HTTP 403 (NPR-31845).

* Ao mover o conteúdo dentro da mesma pasta, a opção de movimentação de página é desativada (NPR-31840).

* No modo de estrutura de modelos editáveis, a lista de componentes permitidos no container de layout exibe resultados incorretos. Somente os componentes com caixa de diálogo de design são exibidos no container de layout (NPR-31816).

* Quando uma página tem permissões somente leitura para um usuário, a opção de propriedades Abrir fica visível em sites.html, mas não no editor.html (NPR-31770).

* Quando um usuário clica no botão Criar, a opção de página não está disponível (NPR-31756).

* Não é possível sincronizar a campanha na campanha Adobe que contém o componente de importador de design OOTB (pronto para uso) (NPR-31728).

* Quando você tenta alterar uma lista de marcador para lista numerada, somente os dois primeiros itens da lista são alterados (NPR-31636).

* Quando uma página não é criada e o nó filho é selecionado, a caixa de diálogo de seleção ainda exibe o nó inicial. Quando a página é criada e o usuário clica em navegar, a página redireciona para o nó raiz em vez do nó criado (NPR-31618).

* A caixa de diálogo de configuração da visualização não funciona corretamente para o recurso de fluxo de trabalho de personalização da Caixa de entrada (NPR-32503 e NPR-32492).

* Uma mensagem de erro é exibida ao exibir informações do fluxo de trabalho usando a Caixa de entrada (CQ-4282168).

### Assets {#assets-6540-enhancements}

* O botão para acionar o fluxo de trabalho na página de coleta de ativos está desativado (NPR-32471).

* Uma pasta sem nome é criada no SPS (Scene7 Publishing System) ao mover um ativo de uma pasta para outra no Experience Manager com a configuração do Dynamic Media Scene7 (NPR-32440).

* A ação para mover todos os ativos (usando Selecionar tudo e mover) para uma pasta que contém os ativos publicados falha com erro (NPR-32366).

* Falha na geração da execução de ativos com ${extension} (NPR-32294).

* Os URLs do histórico de versões são exibidos no campo Referenciado por na página Propriedade dos ativos (NPR-31889).

* O arquivo ZIP baixado do DAM não pode ser aberto usando o WinZip (NPR-32293).

* As permissões originais de uma pasta são atualizadas quando as Configurações da pasta são abertas para alterar o título da pasta ou a imagem em miniatura e salvas (NPR-32292).

* O ícone de calendário para ativação programada não é exibido na coluna Status (na interface clássica da lista de ativos DAM) para ativos cuja ativação está programada para uma data e hora posteriores (NPR-32291).

* A criação de fragmentos usando modelos de fragmento fornece erro ao pesquisar coleções durante o processo de criação de fragmento (NPR-32290).

* Vários query de pesquisa são disparados quando várias tags são selecionadas do filtro de pesquisa (NPR-32143).

* A interface do usuário do Experience Manager Assets exibe nomes de arquivo truncados quando ativos com mais de 50 caracteres no nome do arquivo são carregados (NPR-32054).

* Todas as caixas de seleção no painel Filtro são apagadas quando a primeira e a segunda caixas de seleção são apagadas, quando as caixas de seleção de nível dois da árvore de caixas de seleção no Adobe Stock foram selecionadas (NPR-31919).

* A pesquisa de Arquivos e Pastas usando aspectos Omnisearch dá exceção (NPR-31872).

* O realce de campo para seleção obrigatória de campo no editor de metadados não é removido mesmo depois de selecionar o campo obrigatório, quando as regras de dependência são definidas no formulário de schema de metadados correspondente (NPR-31834).

* Os nomes completos das tags de nível de folha (da hierarquia de tags) não são exibidos na página Propriedades do ativo (NPR-31820).

* O uso do comando back da página Propriedades do ativo no navegador Safari dá um erro (NPR-31753).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário (NPR-31307).

* A página de detalhes de ativos de ativos PDF não mostra botões de ação exceto Para coleção e Adicionar representação no Experience Manager em execução no modo de execução do Dynamic Media Scene7 (CQ-4286705).

* Os ativos demoram muito para serem processados pelo processo de upload em lote do Scene7 (CQ-4286445).

* O botão Salvar não importa o Conjunto Remoto quando o usuário não tiver feito nenhuma alteração no Editor de Conjunto no Cliente de Mídia Dinâmica (CQ-4285690).

* A miniatura de ativos 3D não é informativa quando um modelo 3D suportado é assimilado ao Experience Manager (CQ-4283701).

* O status não processado da predefinição do visualizador de vídeo de recorte inteligente aparece duas vezes no texto do banner ao lado do nome predefinido (CQ-4283517).

* Altura incorreta do container de um modelo 3D carregado visualizado no visualizador 3D é observada na página de detalhes do ativo (CQ-4283309).

* O Editor de carrossel não abre no IE 11 no modo Experience Manager Dynamic Media Hybrid (CQ-4255590).

* O foco do teclado fica travado no menu suspenso Email na caixa de diálogo Download, nos navegadores Chrome e Safari (NPR-32067).

* A caixa de seleção Sincronizar todo o conteúdo não está ativada por padrão ao tentar adicionar a configuração da nuvem DM no Experience Manager (CQ-4288533).

### Interface do usuário do Foundation {#foundation-ui-6540}

* O controle do mouse muda para o campo de filtro anterior em vez de permanecer no campo de filtro existente enquanto pesquisa ativos usando o painel Filtro (NPR-32538).

* Marcação de plataforma: Pesquise por tags digitando nos campos de tag mostra tags fora dos limites raiz e não respeita a propriedade `rootPath` dos campos de tag (NPR-31895).

* Interface do usuário da plataforma: O navegador de caminho quebra se um caminho inválido for adicionado no campo de texto (NPR-31884).

* A notificação fica oculta atrás de um menu fixo na seleção da página (NPR-31628).

### Plataforma {#platform-sling-6540}

* (HTL) Os sublinhados substituem dois pontos na seção de caminho do URL (NPR-32231).

### Projetos {#projects-6540}

* O botão Criar não estará visível para o usuário mesmo se ele tiver permissão para criar um projeto na subpasta (NPR-31832).

### Tradução de projetos {#projects-translation-6540}

* A criação do projeto de tradução quebra a interface quando a opção Aparar espaços é ativada em `Apache Sling JSP Script Handler` (NPR-32154).

* Erro na interface do usuário e exceção de ponto nulo em registros de erros é observada quando qualquer tag, a ser traduzida, é adicionada a um projeto de tradução (NPR-31896).

### Integrações {#integrations-6540}

* A geração do URL da biblioteca de inicialização é baseada somente em `path` e `library_name` valores da API de inicialização e não se baseia no `library_path` valor (NPR-31550).

* Uma mensagem de erro é exibida durante o processamento de itens relacionados ao LiveFyre (FYR-12420).

* ReportSuitesServlet está vulnerável a SSRF (NPR-32156).

### Editor de modelos WCM {#wcm-template-editor-6540}

* No modo de estrutura de modelos editáveis, a lista de componentes permitidos no container de layout não exibe o componente de botão de link (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Erro ao selecionar uma sobreposição e depois selecionar a grade responsiva Arraste os componentes aqui (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* Falha na configuração da nuvem de públicos alvos com o erro de obtenção de mboxes (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Os usuários do Brand Portal não conseguem publicar os ativos da pasta de contribuição [!DNL Assets] na atualização para E/S do Adobe no Experience Manager 6.5.4 (CQDOC-15655). Para uma correção imediata no Experience Manager 6.5.4, é recomendável [baixar a correção](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e instalá-la na instância do autor.

* Os valores de pop-up de schema de metadados não estão visíveis nas propriedades do ativo (CQ-4283287).

* O subesquema de metadados não exibe guias com base no tipo MIME nas propriedades do ativo (CQ-4283288).

* Cancelar a publicação do schema de metadados preenche uma mensagem de erro, embora o schema seja removido do backend.

* A imagem de pré-visualização não é exibida para um ativo publicado (CQ-4285886).

* O usuário não pode publicar ou cancelar a publicação de ativos contendo aspas simples no nome (CQ-4272686).

* Os termos e condições não são exibidos durante o download de vários ativos (CQ-4281224).

* Pequenas vulnerabilidades de segurança abordadas.

### Communities {#communities-6540}

* O formulário Criar membro é exibido como uma página em branco (NPR-31997).

* O usuário não pode visualização o relatório do Analytics na instância do autor (NPR-30913).

### Oak - Indexação e Query {#oak-indexing-6540}

* Os documentos do MS Word e do MS Excel, que contêm imagem JPEG, quando analisados com o analisador Tika não conseguem analisar e o erro de classe não encontrada é observado (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>O Experience Manager Service Pack não inclui correções para o Experience Manager Forms. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o Adobe Experience Manager Forms no JEE. Para obter mais informações, consulte [Instalar o add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms e [instalar o Experience Manager Forms no JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Gerenciamento de correspondência: As letras exibem caracteres extras após o envio aos workflows do processo de publicação (NPR-32626).

* Gerenciamento de correspondência: As letras exibem um espaço reservado suspenso como um componente de texto após a submissão a workflows pós-processo (NPR-32539).

* Gerenciamento de correspondência: Os valores padrão definidos no modelo de letra não são exibidos no modo de Pré-visualização (NPR-32511).

* Forms móvel: O botão Enviar é exibido como expandido em tamanho ao renderizar um formulário XDP em uma versão HTML (NPR-32514).

* Serviços do documento: Problemas de acesso ao URL para Cartas e outras páginas após a aplicação do Service Pack 2 (NPR-32508, NPR-32509).

* Serviços do documento: Se o número de transações em um servidor exceder um limite específico, a conversão de HTML em PDF falhará e as configurações de tipo de arquivo serão removidas do [!DNL Forms] servidor (NPR-32204).

* Forms adaptável: A ferramenta de acessibilidade do navegador relata falhas em formulários adaptáveis de acordo com as diretrizes WCAG2 Nível AA (NPR-32312, NPR-32309, CQ-4285439).

* Forms adaptável: A ferramenta de acessibilidade do navegador Chrome informa uma falha de prática recomendada (NPR-32310).

* Forms adaptável: Problemas de tradução ao configurar um formulário adaptável incorporado em uma página Sites de Experience Manager (NPR-32168).

* Bancada: Uma mensagem de erro é exibida ao usar a operação Obter propriedades do PDF para o serviço Utilitários do PDF (NPR-32150).

* Segurança do documento: Um arquivo PDF protegido falha ao abrir offline com a opção DisableGlobalOfflineSynchronizationData definida como True (NPR-32078).

* Designer: Se a opção de marcação estiver ativada, a borda do subformulário desaparecerá na saída PDF gerada (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se houver células unidas em uma tabela, o teste de acessibilidade falhará para o arquivo PDF de saída convertido de um formulário XDP usando o serviço de saída (CQ-4285372).

* JEE de base: Se um servidor Experience Manager Forms for desconectado de um cluster, problemas de cache impedirão que ele se reconecte ao servidor (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral da versão 6.5 em **abril de 2019**. It can be installed on top of [!DNL Adobe Experience Manager] 6.5.

Alguns destaques principais desta versão do Service pack:

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.6.

* [!DNL Experience Manager Assets] agora suporta arquivos ZIP criados com o algoritmo Deflate64.

* A nova coluna para a data criada, que é classificável, foi adicionada na visualização de lista DAM e nos resultados da pesquisa de ativos na visualização de listas.

* A classificação de ativos com base na coluna Nome foi ativada na visualização de Lista.

* [!DNL Dynamic Media] agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso orientado por aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena.

* [!DNL Dynamic Media] suporta a criação de imagens inteligentes.

* Capacidade de [definir preferências de Ausência Temporária](../forms/using/configure-out-of-office-settings.md) em [!DNL Experience Manager] workflows.

* Capacidade de [compartilhar itens](../forms/using/configure-shared-queues-osgi.md) de Caixa de entrada ou Caixa de entrada com outros usuários em [!DNL Experience Manager] workflows.

* Capacidade de [gerar Comunicações interativas no modo](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Lote.

* Versão atualizada do jQuery fornecido no ContextHub para 3.4.1.

### Assets {#assets-6530-enhancements}

**Aprimoramentos do produto**

* [!DNL Experience Manager Assets] agora suporta arquivos ZIP criados com o algoritmo Deflate64 (NPR-27573).

* Nova coluna para a data criada, que é classificável, é adicionada na visualização de lista DAM e nos resultados da pesquisa de ativos na visualização de lista (NPR-31312).

* Na visualização da lista, os usuários podem classificar a lista de ativos usando a coluna [!UICONTROL Nome] (NPR-31299).

* Os arquivos GLB, GLTF, OBJ e STL podem ser visualizados na página Detalhes [!UICONTROL do] ativo no DAM (CQ-4282277).

* `ReplicationOnModifyListener` O evento é acionado para nós de segmentos durante o carregamento de segmentos em [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso acionado pelo aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena (CQ-4278995).

* [!DNL Dynamic Media] suporta Smart Imaging (CQ-4222249).

* A visualização de pesquisa ou navegação é definida como a visualização padrão no seletor do Foundation se os parâmetros do query forem transmitidos na solicitação (NPR-31601).

**Correções**

* Os metadados de alguns documentos PDF não são atualizados e salvos no PDF quando seu título é modificado (NPR-31629).

* O compartilhamento de ativos não funciona para um ativo que tem um caractere de adição (`+`) no nome do arquivo (NPR-31547).

* As edições no formulário de pesquisa padrão Assets Admin Search Rail não funcionam como esperado (NPR-31502).

* As sugestões não são exibidas ao usar o Omnisearch em ativos visualização para pesquisar ativos (NPR-31496).

* As referências de ativos em coleções não são atualizadas quando os ativos referenciados são movidos para outro local, nos casos em que os mesmos ativos são referenciados por coleção diferente por usuários diferentes (NPR-31486).

* As tags IPTC do duplicado são adicionadas aos metadados do ativo (NPR-31328).

* A contagem de resultados da pesquisa não é atualizada corretamente quando uma pesquisa é acionada a partir do painel de filtros (NPR-31316).

* Todas as caixas de seleção são desmarcadas ao desmarcar as caixas de seleção de segundo nível no filtro Tipo de arquivo, e o texto na barra de pesquisa não está sincronizado com as propriedades selecionadas ou desmarcadas (NPR-31287).

* Não é possível remover todos os membros (utilizadores/grupos) da seção Membros de uma pasta; ao tentar remover todos os usuários, o usuário conectado é adicionado à lista (NPR-31171).

* Os ativos com o símbolo de adição (`+`) no nome do arquivo não podem ser excluídos (NPR-31162).

* O menu suspenso Criar, que está visível no menu superior ao selecionar uma pasta, não mostra a opção &quot;Pasta&quot; como uma opção de criação (NPR-30877).

* A seleção de pasta Criar > item de ação FileUpload está ausente quando a ACL para Negar `jcr:removeChildNodes` e `jcr:removeNode` no caminho é aplicada para um usuário (NPR-30840).

* Workflows DAM entram em estado obsoleto quando determinados ativos mp4 são carregados, fazendo com que todos os workflows restantes entrem em estado obsoleto (NPR-30662).

* Erro de falta de memória é observado quando um grande arquivo PDF (de vários Gigabytes) é carregado no DAM e seus subativos são processados (NPR-30614).

* A movimentação em massa de ativos está falhando e exibindo a mensagem de aviso (NPR-30610).

* Os nomes dos ativos são alterados para letras minúsculas ao mover ativos de uma pasta para outra em [!DNL Experience Manager] execução no modo [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Ocorreu um erro ao editar um conjunto de imagens remoto, para a imagem que reside na pasta com o mesmo nome que o nome da empresa do Scene7 (NPR-31340).

* [!DNL Dynamic Media] ativos que contêm referências não estão sendo publicados (NPR-31180).

* Os uploads do modo [!DNL Dynamic Media]7-Scene7 para [!DNL Dynamic Media Classic] estão demorando muito para serem concluídos (NPR-31048).

* O ponto de acesso adicionado a um ativo de imagem não é visível por meio do Visualizador de imagem interativo na página de detalhes do ativo (NPR-30979).

* Grandes trabalhos de sling são criados e o banner Processamento é reexibido quando as ações realizadas em ativos [!DNL Experience manager Assets] são passadas para a Scene7 (NPR-30947).

* O conflito ocorre ao criar uma Cópia de idioma dos ativos e os ativos não são carregados para a Scene7 (NPR-30932).

* As renderizações dinâmicas baixadas da [!DNL Experience Manager] execução no modo [!DNL Dynamic Media]Híbrido estão quebradas (elas são do tipo de texto com o conteúdo &quot;não é possível localizar a imagem&quot; em vez do tipo de conteúdo de imagem) (NPR-30876).

* [!DNL Dynamic Media] O fluxo de trabalho Codificar vídeo está falhando ao gerar miniatura para o vídeo que é migrado do modo [!DNL Dynamic Media Classic] para o [!DNL Dynamic Media]Scene7 no Adobe Experience Manager (CQ-4282011).

* IpsApiException observado ao migrar ativos de uma instância para outra usando IDs de empresa da Scene7 diferentes (CQ-4280548).

* A miniatura de ativos 3D não é informativa quando um modelo 3D suportado é assimilado [!DNL Experience Manager] (CQ-4283701).

* Os botões de rolagem são exibidos no visualizador, se um ativo 3D tiver poucas visualizações de câmera (CQ-4283322).

* Altura incorreta do container de um modelo 3D carregado visualizado no DimensionalViewer na página Detalhes do ativo (CQ-4283309).

* Os vídeos não podem ser reproduzidos com o SmartCropVideoViewer no Internet Explorer 11 e no Safari (CQ-4281422).

* O uso do botão mover para mover vários ativos, de uma pasta para outra, falha ao [!DNL Experience Manager] executar no modo de execução [!DNL Dynamic Media]Scene7 (CQ-4280384).

* Vídeo distorcido é visto nos detalhes do ativo quando o tipo MIME é diferente de MP4 (CQ-4279704).

* Os vídeos recém-ingeridos em pastas com perfil de vídeo permanecem no estado de processamento mesmo após a porcentagem de codificação ser concluída para 100% (CQ-4279389).

* Mover ativos de uma pasta cria um grande número de tarefas sling (chamadas de API da Scene7) do que o ideal (CQ-4278664).

* Os nomes do conjunto de imagens são alterados para minúsculas no Scene7, quando o conjunto de imagens (ou conjunto de imagens) é criado e nomeado com a convenção de nomenclatura apropriada no DAM (CQ-4281112).

* O Scene7 Migrator define o estado de publicação incorretamente (CQ-4263492).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário em Fragmentos de conteúdo (CQ-4282898).

* Os arquivos PDF não são indexados e o conteúdo não é pesquisável (CQ-4278916).

* Erro &quot;Grupo não listado pelo seletor de usuários: esperado &quot;falso para igual a verdadeiro&quot; é observado ao adicionar o Grupo de usuários fechado com diferentes `principalName` e `authorizableId` (CQ-4278177).

* A Visualização da coluna da interface do usuário do Assets está mostrando todos os caminhos, independentemente do caminho raiz do locatário específico (CQ-4278175).

* A pesquisa do seletor de ativos não está funcionando como esperado (CQ-4275886).

* Os Workflows de execução estão com falha (CQ-4271928).

* A Expurgação de Evento DAM exclui os dados mais recentes (`maxSavedActivities`) do evento e armazena os dados criados anteriormente (NPR-31336).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário (NPR-31307).

* A barra de ações e a contagem de ativos não são atualizadas ao selecionar todos e depois desmarcar alguns itens (pastas/ativos individuais) na interface de usuário do toque (NPR-31118).

* Uma exceção é exibida durante [!DNL Experience Manager] a pesquisa para obter detalhes de um ativo (CQ-4283569).

### Sites {#sites}

* Se a herança do LiveCopy for quebrada, as páginas de Live Copy exibirão links de cópia de idioma em vez de links do LiveCopy (NPR-30980).
* Para um novo Blueprint, se o número de registros for superior a 40, somente os primeiros 40 registros serão exibidos. O Blueprint exibe linhas em branco para o restante dos registros (NPR-31182).
* Quando um usuário adiciona caracteres japoneses ou coreanos na propriedade de descrição de um menu, o menu exibe caracteres distorcidos para o texto em japonês e coreano (NPR-31331).
* O Editor de Rich Text (RTE) não permite inserir uma Tabela incorporada como um item de lista (NPR-30879).
* Fora da caixa, andaime do Editor de Rich Text (RTE). aplica o tamanho da fonte embutida a elementos, inesperadamente (NPR-31284).
* Quando um usuário foca nos campos do painel à esquerda e usa um atalho do teclado para colar o conteúdo, ele cola o conteúdo da área de transferência do editor de páginas em vez do conteúdo copiado dos campos do painel à esquerda (NPR-31172).
* Quando um usuário adiciona um campo Upload de arquivo a um campo múltiplo, o caminho da imagem é armazenado no nó do componente em vez do nó de vários campos (NPR-30882).
* A `ResponsiveGridExporter` API não retorna a `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` interface. O `com.day.cq.wcm.foundation.model.impl` pacote é declarado como um pacote privado (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* Quando uma página que contém alguns Fragmentos de experiência é aberta no modo não editor (no Autor sem o `editor.html` prefixo e `wcmmode=disabled`, ou no Editor)., a solicitação termina no código de erro de status HTTP `500` (NPR-30743).
* Os usuários não podem alterar sua senha e acessar sua página do perfil (NPR-31161).

### Pesquisa e interface do usuário {#ui-interface-and-search}

* Ao alternar da visualização do cartão para a visualização da lista em uma página de resultados de pesquisa, há um atraso antes que a página possa ser rolada (NPR-31286).

* A caixa de seleção [!UICONTROL Selecionar tudo] está oculta na visualização de lista na interface do [!DNL Sites] usuário (NPR-31614).

* A contagem [!UICONTROL Selecionar tudo] em uma página de resultados de pesquisa está incorreta (NPR-31120).

* O editor de metadados exibe tags que não existem (NPR-31119).

### Tradução {#translation}

* Dois pop-ups de calendário são exibidos ao selecionar a opção Data de vencimento em um trabalho de tradução (NPR-31270).

### Plataforma {#platform}

* A opção de tipo Mime no console da Web não funciona (NPR-31108).

* O certificado do cliente não é aceito ao configurar o logon único (NPR-31165).

* As atualizações na configuração de tamanho do buffer do serviço HTTP baseado em Java não são salvas (NPR-30925).

* O QueryBuilder agora suporta orderby `fn:name()` em query xpath (NPR-31322).

* A árvore de ativação do duplicado é criada ao atualizar da versão [!DNL Experience Manager] 6.3 (NPR-31513).

* As solicitações encaminhadas não preservam cabeçalhos de resposta que são definidos durante a autenticação Sling (NPR-30013).

* A pesquisa nos componentes do seletor não funciona (NPR-31692).

* Um erro é exibido ao anexar um arquivo ZIP a uma [!DNL Experience Manager Communities] publicação devido a diferentes versões do pacote Apache POI e Apache Tika (NPR-31018).

* O `org.apache.sling.distribution.api` pacote está oculto no gerenciador de configuração e, portanto, não está disponível para pacotes personalizados (NPR-31720).

### Projetos {#projects}

* A alternância de visualizações de calendário não funciona (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Aprimoramentos do produto**

* O fluxo de trabalho de importação da Origem de ativos no [!DNL Experience Manager Assets] é modificado para buscar apenas os ativos recém-criados de [!DNL Brand Portal] para [!DNL Experience Manager]e ignorar os ativos que já existem na pasta NEW para evitar a replicação (CQ-4278527).

**Correções**

* O ícone incorreto é exibido ao criar uma nova pasta Contribuição no recurso Origem de ativos (CQ-4282825).
* Ao criar uma nova pasta de contribuição, uma ou ambas as subpastas (NOVO e COMPARTILHADO) não aparecem na pasta de contribuição (CQ-4282424).
* O sistema lança uma exceção se o usuário tentar republicar a pasta Contribuição de [!DNL Experience Manager] para [!DNL Brand Portal] depois de receber novos ativos na pasta Contribuição do [!DNL Brand Portal] fim (CQ-4279740).
* A criação da pasta Contribuição em uma pasta Contribuição (pasta aninhada) é proibida para evitar a complexidade (CQ-4278391).
* O sistema lança uma exceção ao carregar a lista do [!DNL Brand Portal] usuário (arquivo .csv) importada do [!DNL Experience Manager] Admin Console. Somente os campos Email, Nome e Sobrenome no arquivo .csv são obrigatórios (CQ-4278390).

### Communities {#communities-6530}

**Correções**

* Os links rápidos para gerenciar grupos (Abrir/Editar/Publicar/Excluir grupos) não estão visíveis para os administradores da Comunidade (Administrador de grupo/Administrador de site) (NPR-31627).
* Um blog enviado não é exibido, a menos que a página seja atualizada/recarregada manualmente (NPR-31599).
* O query JCR usado pelo recurso &quot;Menções&quot; diferencia maiúsculas de minúsculas e demora muito para retornar os resultados (NPR-31475).
* [!DNL Experience Manager] 6.5 O arquivo UberJar lança uma exceção, `cq-social-translation` o pacote está faltando no arquivo [!DNL Experience Manager] 6.5 UberJar (NPR-31186).
* As bibliotecas de Jackson Databind foram atualizadas para a versão 2.9.9.3 para endereçar novas vulnerabilidades (NPR-30967).
* Os títulos Atividades e Notificações são inconsistentes (NPR-30941).
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Atualizações de índice Lucene fazendo com que o servidor do autor fique lento (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] O Service Pack não inclui correções para [!DNL Experience Manager Forms]. Eles são entregues usando um pacote complementar separado do Forms. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. Para obter mais informações, consulte [Instalar o add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms e [instalar o Experience Manager Forms no JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Pacote complementar do Forms {#forms-add-on-package-6530}

**Formulários adaptáveis**

* As strings contêm a chave do dicionário ao localizar formulários adaptáveis (NPR-31110).

**Comunicação interativa**

* **MissingNode.toString()** retorna resultados imprecisos após atualizar as bibliotecas Jackson para 2.10.0 (NPR-31549).

* O editor de texto remove aleatoriamente caracteres de espaço do texto copiado do Microsoft Word (NPR-31113).

**Gerenciamento de correspondência**

* Legendas e dicas de ferramentas não são exibidas ao migrar letras do LiveCycle ES4SP1 para [!DNL Experience Manager] 6.5 (NPR-31615).

* **A formatação do fluxo de texto não é mais exibida uma mensagem de erro compatível** ao salvar letras como rascunhos (NPR-30463).

**Fluxo de trabalho**

* O fluxo de trabalho do OSGi falha devido à utilização de 100% da CPU (NPR-31233).

**Formulários HTML5**

* Gerar a visualização HTML5 de um formulário XDP mostra uma oscilação ao adicionar instâncias de um formulário secundário (NPR-30909).

#### Instalador do Forms em JEE {#forms-jee-installer-6530}

**Forms - Serviços de documentos**

* O serviço Web SOAP que usa MTOM em um projeto .NET exibe exceções para a chamada AssemblerServiceClient e métodos HtmlToPDF2 (NPR-4281771).

* Vulnerabilidade de segurança 2012-5784 e 2014-3596 encontrada com o jar AXIS 1.4 e correção fornecida com o jar [](https://helpx.adobe.com/br/aem-forms/quick-fixes/6-5/jee-patch-0014.html) AXIS 1.4.1 (NPR-31015).

**Foundation JEE**

* A configuração de ação não carrega os nomes de processo para Chamar uma ação de envio de Forms Workflow (NPR-31478).

### Feature Packs incluídos {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Suporte da Forms para o Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral do [!DNL Adobe Experience Manager] 6.5 em **abril de 2019**. It can be installed on top of [!DNL Experience Manager] 6.5.

Alguns destaques principais desta versão do Service pack:

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.3.
* Adição de uma propriedade de configuração para permitir a exportação de Fragmentos de experiência diretamente para espaços de trabalho definidos pelo usuário do [!DNL Adobe Target].
* Os usuários do Assets podem pesquisar imagens visualmente semelhantes. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [pesquisa visual](../assets/search-assets.md#visualsearch).

* Aprimoramento da funcionalidade Ativos conectados para adicionar suporte à busca de documentos a partir de implantações remotas do DAM. Os autores do site agora podem pesquisar e filtrar tipos de documentos compatíveis no Localizador de conteúdo. Os documentos remotos podem ser adicionados ao Componente de download em páginas da Web. Consulte [usar ativos conectados](../assets/use-assets-across-connected-assets-instances.md).

* Aprimorarfiltros do tipo Document com mais tipos MIME para suportar opções de vários valores.
* Introdução de um fluxo de trabalho externo de reprocessamento para oferecer suporte a vários recursos.
* Desempenho otimizado [!DNL Dynamic Media] usando filtros de ativos padrão para replicação.
* Restauração das opções de edição de cortar/girar ativos para o DMS7.
* Implementação de uma opção para silenciar um vídeo quando carregado no VideoPlayer.
* Correção para garantir que a exibição da coluna da interface do usuário do ativo mostre somente conteúdo específico do locatário.
* Correção para permitir que as alterações de acordeão de estilo reflitam nos resultados de pesquisa.

### Assets {#assets}

**Aprimoramentos do produto**

* Aprimoramento da funcionalidade Ativos conectados para adicionar suporte à busca de documentos a partir de implantações remotas do DAM. Os autores do site agora podem pesquisar e filtrar tipos de documentos compatíveis no Localizador de conteúdo. Os documentos remotos podem ser adicionados ao Componente de download em páginas da Web. Hotfix do CQ-4270245. Consulte [usar ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets]Os usuários do podem pesquisar imagens visualmente semelhantes. [!DNL Experience Manager]O exibe as imagens com tags inteligentes do repositório DAM que são semelhantes a uma imagem selecionada pelo usuário. Consulte [pesquisa visual](../assets/search-assets.md#visualsearch).

**Correções**

* Os caminhos de ativos nos metadados de URLs e de pastas gerados pela API ACP não são codificados por URL. GRANITE-26198: Hotfix do CQ-4271814
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989: Hotfix do CQ-4270467
* Interface do usuário para toque: Durante o assistente de gerenciamento de publicação, as referências são adicionadas após a página no corpo da solicitação de publicação, fazendo com que todos os ativos sejam publicados após a página e, quando a página for renderizada, alguns dos ativos na instância de publicação serão perdidos. NPR-29985: Hotfix do CQ-4270724
* O recurso Ativo não relacionado não funciona para ativos relacionados que têm caracteres especiais (caracteres que se tornam codificados por URI) no nome. NPR-30387: Hotfix do CQ-4274446
* Ao editar um fragmento do conteúdo, a versão é criada com o usuário errado.
* Falha durante a criação de coleções no sistema baseado em Locatário. NPR-30114: Hotfix do CQ-4272948
* A exibição em coluna da interface do usuário do ativo não respeita o caminho DAM raiz do locatário atual, mas acessa todos os caminhos DAM do locatário. NPR-30636: Hotfix do CQ-4275481
* Possível ataque de script entre sites (XSS) por meio da janela de alerta de arquivo restrito, pois a imagem injetada pode ser vista. NPR-30617: Hotfix do CQ-4270133
* MultiTenant: Os locatários que salvam as propriedades da pasta observam o prompt de sucesso e a mensagem de erro que descreve a ação não foi bem-sucedida. &quot;Não é possível editar as propriedades. Permissões insuficientes.&quot; Os confundido. NPR-30545: Hotfix do CQ-4275333
* A caixa de diálogo do seletor de ativos não permite a seleção de ativos. Portanto, não é possível atualizar a fonte usando a funcionalidade de substituição da fonte relacionada. NPR-30502: Hotfix do CQ-4275029
* [!UICONTROL Fluxo de trabalho do Ativo] de atualização do DAM - no estado obsoleto ao carregar arquivos mp4 de tamanho grande. NPR-30480: Hotfix do CQ-4271352
* A funcionalidade Criar tarefa de revisão não funciona devido a uma carga nula que faz com que todas as ações subsequentes relacionadas à tarefa de revisão falhem. NPR-30468: Hotfix do CQ-4274263
* Problema de conectividade com o Adobe Smart Tag por meio do Datapower. NPR-30026: Hotfix do CQ-4269457
* A exibição em coluna da interface do usuário do Assets emite um erro ao tentar abrir os filtros que saíram do painel. NPR-30501: Hotfix do CQ-4273862
* Ao adicionar grupos sincronizados do LDAP nas propriedades de Grupo de usuários fechado (CUG) de uma Pasta de ativos, o grupo não é salvo e recuperado. NPR-30615: Hotfix do CQ-4274689
* Os campos de estilo de pesquisa e orientação de filtros não aplicam o valor preenchido automaticamente à consulta de pesquisa. NPR-30620: Hotfix do CQ-4275724
* O link de compartilhamento de ativos de uma pasta com espaço e o caractere &quot;&amp;&quot; no nome exibe cartões cinza em branco para alguns ativos. NPR-30557: Hotfix do CQ-4270187
* O formulário de esquema de metadados da pasta não detecta automaticamente o tipo de dados e, portanto, não cria o TypeHint relacionado no envio do formulário. NPR-30599: Hotfix do CQ-4275227
* As opções de edição Recortar e Girar do ativo estão desativadas na interface do usuário de criação do DMS7. NPR-30118: Hotfix do CQ-4273221
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080, NPR-30492: Hotfix do CQ-4273651
* Adding the [!DNL Dynamic Media]–Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641: Hotfix do CQ-4275962
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490: Hotfix do CQ-4273614
* [!DNL Dynamic Media]: Adicionados filtros padrão para excluir ativos de serem replicados para o nó de [!DNL Experience Manager] publicação. NPR-30538: Hotfix do CQ-4274678
* Introdução de um fluxo de trabalho externo de reprocessamento para suporte a vários recursos de forma a permitir a pasta como uma carga. O fluxo de trabalho tem duas etapas: reprocessa ativos não manuseados pelo mapa de metadados para a próxima etapa e recarrega todos os ativos não manuseados para S7 em um único trabalho IPS. For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489: Hotfix do CQ-4272903
* Carregar um CSV incorreto após o CSV correto apaga o CSV correto. Hotfix do CQ-4277694, CQ-4277814
* O ícone incorreto específico das pastas de contribuição a serem removidas. Hotfix do CQ-4277580
* Ao selecionar um usuário no seletor de usuários da guia Contribuição do ativo, o nome do usuário não aparece na tabela e a caixa de diálogo Excluir usuário na página de propriedades mostra o texto errado. Hotfix do CQ-4277875
* Os contribuidores não podem ser adicionados à pasta de contribuição do ativo no seletor de usuários ao selecionar o usuário e clicar em adicionar. Hotfix do CQ-4277824, CQ-4278087
* A pesquisa por nome de usuário em letras minúsculas não funciona no seletor de usuários. Hotfix do CQ-4277958, CQ-4277930
* Os não administradores podem publicar ativos em uma nova pasta de uma pasta de contribuição de ativos. Hotfix do CQ-4278200
* O dam-user (não administrador) não tem a opção de adicionar contribuidores à pasta de contribuição do ativo. Hotfix do CQ-4278192
* O botão &quot;Criar&quot; está visível na pasta Contribuição do ativo. Hotfix do CQ-4277560
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. Hotfix do CQ-4273864
* Se o usuário tiver uma ID de email em letras maiúsculas, os usuários não poderão fazer check-in nos ativos cujo check-out foi feito anteriormente. Hotfix do CQ-4276575
* A operação Excluir se aplica somente às predefinições selecionadas e, se a tela atualizar automaticamente a lista após a operação, ela mostrará outras predefinições que já foram atualizadas. Hotfix do CQ-4261461
* Configuring [!DNL Dynamic Media] Cloud Services in [!DNL Dynamic Media]–Hybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. Hotfix do CQ-4249780
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. Hotfix do CQ-4276763
* O conteúdo gerado pelo usuário é exibido incorretamente no painel Filtro de pesquisa. Hotfix do CQ-4273875
* A opção Localizar semelhante não está disponível para imagens TIFF. Hotfix do CQ-4278238
* Implementação da opção para silenciar o vídeo quando carregado no VideoPlayer. Hotfix do CQ-4266465
* Visualizadores - Visualizador de vídeo: poster=none funciona incorretamente no caso de um vídeo externo ser usado. Hotfix do CQ-4265536
* O ícone Aguardar fica visível durante a reprodução do vídeo nos navegadores IE11 e MS Edge. Hotfix do CQ-4251539
* Os arquivos README dos visualizadores 3.8 e 5.13 não são atualizados e contêm informações de versões anteriores. Hotfix do CQ-4273737
* O Fragmento do conteúdo recebe controle de versão mesmo antes de salvar as alterações. NPR-30616: Hotfix do CQ-4273088
* Substitua Asset#getMetadata(String) por Asset#getMetadataValueFromJcr(String) no processo de miniatura. NPR-30491: Hotfix do CQ-4273067
* O upload do jpg causa várias instâncias da mensagem: &quot;ReplicateOnModifyWorker Replicating UPDATED&quot; para cada ativo, causando degradação do desempenho.
* Descompactar o arquivo zip usando o recurso &#39;Extrair arquivo&#39; causa problemas nas pastas cujo nome contém a porcentagem (%) no título. NPR-29990: Hotfix do CQ-4270467

### Sites {#sites-6520}

* Se a herança do LiveCopy for quebrada, as páginas de Live Copy exibirão links de cópia de idioma em vez de links do LiveCopy (NPR-30980).
* Para um novo Blueprint, se o número de registros for superior a 40, somente os primeiros 40 registros serão exibidos. O Blueprint exibe linhas em branco para o restante dos registros (NPR-31182).
* O plug-in do Editor de Rich Text (RTE) do componente de texto exibe caracteres distorcidos para o texto em japonês e coreano (NPR-31331).
* O Editor de Rich Text (RTE) não permite inserir uma Tabela incorporada como um item de lista (NPR-30879).
* O Editor de Rich Text (RTE) é aplicado inesperadamente ao tamanho da fonte em linha aos elementos (NPR-31284).
* Quando um usuário foca nos campos do painel esquerdo e usa o atalho do teclado para colar o conteúdo, ele cola o conteúdo da área de transferência do editor de páginas em vez do conteúdo copiado dos campos do painel esquerdo (NPR-31172).
* Quando um usuário adiciona um campo Upload de arquivo a um campo múltiplo, o caminho da imagem é armazenado no nó do componente em vez do nó de vários campos (NPR-30882).
* A `ResponsiveGridExporter` API não retorna a `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` interface. O `com.day.cq.wcm.foundation.model.impl` pacote é declarado como pacote privado (NPR-31398).
* Quando uma página que contém alguns Fragmentos de experiência é aberta no modo não editor (no Autor sem o `editor.html` prefixo e `wcmmode=disabled`, ou no Editor), a solicitação termina no código de erro de status HTTP 500 (NPR-30743).

### WCM - Editor de páginas {#wcm-page-editor-6520}

**Aprimoramentos do produto**

* Aprimorarfiltros do tipo Document com mais tipos MIME para suportar opções de vários valores. Hotfix do CQ-4270694

### Gerenciamento de fragmentos de conteúdo {#content-fragment-management-6520}

* A consulta usada pela interface do usuário de modelos do Fragmento do conteúdo é muito lenta e, eventualmente, resulta em um erro. Hotfix do CQ-4270807

### IU - Foundation {#ui-foundation}

* Os atalhos são acionados o que impede que o usuário use &#39;m,&#39; &#39;p,&#39; &#39;e&#39; em interfaces do usuário específicas. NPR-30355: Hotfix do GRANITE-26346
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509: Hotfix do CQ-4274716
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104: Hotfix do GRANITE-26344

### Tradução {#translation-6520}

* Problema de tradução - somente alguns componentes estão sendo traduzidos pela tradução automática. NPR-30079: Hotfix do CQ-4273764

### Plataforma {#platform-6520}

* [!DNL Experience Manager]O remetente de email padrão do não pode enviar emails para um servidor SMTP remoto por TLS v1.2. NPR-30476: Hotfix do GRANITE-26605

### Projetos {#projects-6520}

* Os valores dam:folderThumbnailPaths não são atualizados e exibem miniaturas antigas mesmo depois de excluir os ativos dentro da pasta. NPR-30424: Hotfix do CQ-4273667
* Ao concluir a opção &quot;mover&quot;, o Título e o Nome do ativo permanecem inalterados. NPR-30647: Hotfix do CQ-4276265

### Communities {#communities-6520}

* O Diagnóstico de sincronização do usuário está completamente quebrado e falha ao funcionar. NPR-30004, NPR-29943: Hotfix do CQ-4270287, CQ-4271348

### Sling {#sling}

* A atualização da instância de 6.3.3.2 para 6.5 resulta em configurações OSGi duplicadas. NPR-30130: Hotfix do CQ-4274016

### Integração {#integration}

* O conteúdo personalizado não é exibido corretamente na instância de publicação até a reinicialização da instância. NPR-30377: Hotfix do CQ-4273706
* Ao configurar o Launch em um site, o endereço da biblioteca tem uma barra (/) anexada, sempre causando intervenção manual. NPR-30694: Hotfix do CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] O Service Pack não inclui correções para [!DNL Experience Manager Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Pacote complementar do Forms {#forms-add-on-package}

**Integração back end**

* Não é possível configurar o Modelo de dados de formulário usando um URL com balanceamento de carga hospedado no AWS. NPR-30123: Hotfix do CQ-4273359
* Ao criar o Modelo de Dados de Formulário (FDM) com a Linguagem de Definição de Serviço da Web (WSDL), a mensagem de erro `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` é retornada: NPR-30477: Hotfix para CQ-4272921

**Gerenciamento de correspondência**

* &quot;A execução Criar interface do usuário de correspondência (CCR UI) falha intermitentemente com o erro abaixo no console:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Comunicação interativa**

* Um campo marcado como obrigatório no modelo de dados de formulário é exibido conforme solicitado em Criar interface do usuário de correspondência (CCR UI). NPR-30623: Hotfix do CQ-4274902

**Forms - Fluxo de trabalho**

* Variáveis de saída não mapeadas em Pastas vigiadas causam falha na chamada. Hotfix do CQ-4264451

**Formulários HTML5**

* Quando o código personalizado ou o projeto é implantado pela segunda vez, a página não é renderizada e o seguinte erro ocorre:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Hotfix do CQ-4272509

* Ao usar o NonVisual Desktop Access no modo Procurar para ler um formulário HTML5, o navegador Chrome lê &quot;gráfico&quot; antes de cada Gráfico de vetor escalonável (SVG) no design do formulário. NPR-30449: Hotfix do CQ-4274732

#### Instalador do Forms JEE {#forms-jee-installer}

**Forms - Segurança de documentos**

* A aplicação de uma assinatura com carimbo de data e hora falha com erro: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: erro de chamada. NPR-30820: Hotfix do CQ-4275852

**Forms - Serviços de documentos**

* Se &quot;SubmitURL&quot; contiver um E comercial (&amp;), aparecerão erros de análise no registro quando a solicitação POST for feita para renderpdf servlet. NPR-30865: Hotfix do CQ-4278232

**Forms - Foundation JEE**

* O serviço HTMLtoPDF não mostra maxReuseCount no console JMX. NPR-30134, NPR-30304: Hotfix do CQ-4273763
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Hotfix do CQ-4273217

### Feature Packs incluídos {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Adição de uma propriedade de configuração para permitir a exportação de Fragmentos de experiência diretamente para espaços de trabalho definidos pelo usuário do [!DNL Adobe Target]. NPR-29189: Hotfix do CQ-4249782

#### Forms - Serviços de documentos {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759: Hotfix do CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 é uma versão importante que inclui correções e melhorias de desempenho, estabilidade, segurança e essenciais para o cliente lançadas desde a disponibilização geral do [!DNL Adobe Experience Manager] 6.5 em *abril de 2019.*[!DNL Experience Manager] Ele pode ser instalado por cima do 6.5.

Alguns destaques principais desta versão do Service pack:

* Habilitação da inclusão do estado da interface do usuário dinâmica em eventos de rastreamento como atributos personalizados.
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. Para obter mais informações, consulte [Configurar quebra automática de texto em japonês](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Ativos

* Atualização da interface DAM DMGGateway para oferecer suporte a várias peças S3. NPR-29740: Hotfix do CQ-4226303
* A pré-visualização de execuções gera `Only empty tenantId is currently supported` erro após a atualização para [!DNL Experience Manager] 6.5. NPR-29986: Hotfix para CQ-4272353
* A caixa de diálogo Excluir não está visível para permitir a exclusão de trabalhos. NPR-29720: Hotfix do CQ-4271074
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627: Hotfix do CQ-4264929
* VersioningTimelineEventProvider deve fornecer a versão raiz juntamente com o nó do tipo nt: version. Hotfix do GRANITE-26063
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. Hotfix do CQ-4265131
* A Live Copy recupera o status incorreto se a fonte for editada. Hotfix do CQ-4265451
* Ativação do suporte Multi-Site Manager no [!DNL Experience Manager Assets]. Hotfix do CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] deve exibir uma entrada adicional para a versão atual do ativo no histórico da linha do tempo, exibindo o comentário de check-in mais recente do [!DNL Adobe Asset Link]. Hotfix do CQ-4262864
* A Linha do tempo do fragmento do conteúdo exibe uma mensagem de erro quando as propriedades estão ausentes. Hotfix do CQ-4272560
* Um problema com o reprodutor de vídeo do Scene 7 quando expandido para tela cheia. Hotfix do CQ-4266700
* ZoomVerticalViewer: os botões de deslocamento não devem ser exibidos se um único ativo de imagem for usado. Hotfix do CQ-4264795
* A exclusão de um nó secundário na live copy deve desanexar o liveRelationship. Hotfix do CQ-4270395
* O esquema de metadados contém apenas itens da configuração global, e não os itens do locatário ativo. O valor de URL formPath é revertido para o padrão mesmo quando alterado. NPR-29945: Hotfix do CQ-4262898
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510: Hotfix do CQ-4268659

### Sites

* Propriedades vazias e várias propriedades não se propagam a partir do blueprint durante o lançamento. A redefinição da live copy com blueprint não funciona em componentes. NPR-29253: Hotfix do CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537: Hotfix do CQ-4266129
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785: Hotfix do CQ-4265090
* A página restaurada com o Timewarp deve se referir à imagem correta no momento do controle de versão. NPR-29431: Hotfix do CQ-4262638
* Um problema com a herança dos nós do Sistema de estilo do pai para o filho. NPR-29516: Hotfix do CQ-4270330
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211: Hotfix do CQ-4266630
* A miniatura renderizada no Fragmento do conteúdo mostra a representação interna do calendário do campo Data e hora. NPR-29531: Hotfix do CQ-4269362
* Abrir a guia de permissões na implementação do Coral2 não mostra os botões. Hotfix do CQ-4269419

### Commerce

* ConstraintViolationException, ao executar migração de conteúdo lento para comércio eletrônico. NPR-29247: Hotfix do CQ-4264383

### Gerenciamento de fragmentos de conteúdo

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Hotfix do CQ-4270266

### Fragmentos de experiência

* Exportar [!DNL Experience Manager] fragmentos de experiência para [!DNL Adobe Target]. Hotfix do CQ-4265469
* A exportação de Fragmentos de experiência para o público alvo falha com a imagem inteligente. Hotfix do CQ-4269606

* O usuário atinge um beco sem saída quando tenta mover os Fragmentos de experiência pelo Omnisearch na exibição de cartão. Hotfix do CQ-4263848

### WCM - Editor de páginas

* Script entre sites (XSS) refletido ao usar um seletor inválido. Hotfix do CQ-4270397

### Replicação

* Os dados fornecidos pelo usuário não são escapados na saída no componente `cq/replication/components/agent`, resultando em uma vulnerabilidade de script entre sites (XSS). Hotfix do CQ-4266263

### Fluxo de trabalho

* Campo de seletor de calendário do participante na caixa de diálogo quebrado. NPR-29727: Hotfix do CQ-4270423

### WCM - Editor SPA

* Ativação da busca de conteúdo pré-renderizado a partir de um endpoint remoto. Hotfix do CQ-4270238
* Avisos em registros ao abrir uma Página de modelo SPA renderizada no lado do servidor. Hotfix do CQ-4270238

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. Hotfix do CQ-4271410

### Integração

* As credenciais do BrightEdge falham com erro de conexão. NPR-29168: Hotfix do CQ-4265872

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176: Hotfix do CQ-4265782/CQ-4266153

### Interface do usuário

* Adição de suporte para rastrear estados dinâmicos de interface do usuário como atributos personalizados ao rastrear determinados eventos na API de rastreamento de base. Hotfix do GRANITE-26283
* Não é possível definir o recurso de rastreamento no botão Enviar. Hotfix do GRANITE-26326
* O assistente não pode definir o recurso de rastreamento no botão Enviar. NPR-29995, NPR-30025: Hotfix do CQ-4264289

### Communities

* Não é possível alinhar novos selos na lista suspensa da página de perfil do membro. NPR-29381: Hotfix do CQ-4267987
* Os visitantes e membros, sem privilégios de moderador, podem ver publicações não aprovadas/pendentes ao colar o URL. NPR-29724: Hotfix do CQ-4271124, CQ-4271441
* É observado um tempo de resposta alto de 40 a 50 segundos no logon do usuário na Comunidade. NPR-29677: Hotfix do CQ-4269444

### Replicação

* O componente Replication Agent é susceptível a uma vulnerabilidade que exibe informações confidenciais para usuários não autorizados. NPR-29611: Hotfix do GRANITE-25070

* Vazamento de sessão durante o OAuth em cada replicação no [!DNL Brand Portal]. NPR-30001: Hotfix do GRANITE-26196

### Projetos

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819: Hotfix do CQ-4271118

### Plataforma

* HtmlLibraryManager exclui todo o conteúdo de crx-quickstart na invalidação do cache. NPR-29863: Hotfix do GRANITE-26197

### Felix

* Os detalhes de uso de memória não sãp exibidos no console do sistema ao usar o Java11\. NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* Apenas OSGI: Habilitado o suporte para criar arquivos PDF estáticos usando o Forms Service.
* Ativação das permissões no XMLForm.exe para administradores e usuários raiz.
* Ativação de suporte para ADFS v3.0 para integração local do Dynamics.

#### Pacote complementar do Forms

**Integração de backend**

* Falha ao obter a Linguagem de definição do serviço da Web (WSDL). NPR-29944: Hotfix do CQ-4270777
* When [!DNL Experience Manager Forms] is installed on IBM WebSphere, creating a form data model based on SOAP fails. Hotfix do CQ-4251134
* Ativação de suporte para o Ative Diretory Federation Services (ADFS) v3.0 para integração local do Microsoft Dynamics. Hotfix do CQ-4270586
* Quando o título de uma fonte de dados é alterado, o modelo de dados do formulário não exibe o título atualizado. Hotfix do CQ-4265599
* Se o nome de uma entidade ou atributo contiver hífen ou espaço, o expressão não avaliará essas entidades e atributos. Hotfix do CQ-4225129

* A saída incorreta é observada quando um dois pontos está presente na saída da string primitiva. Hotfix do CQ-4260825

* Mesmo quando nenhum conteúdo é esperado da saída da API REST, a operação de chamada do modelo de dados de formulário emite um erro. Hotfix do CQ-4268828

**Formulários adaptáveis**

* Não é possível adicionar uma nova instância no Fragmento de formulário adaptável durante o carregamento lento. NPR-29818: Hotfix do CQ-4269875
* Verifique se o componente não registra ou exibe algum erro nos modelos de Documento de registro. Hotfix do CQ-4272999
* Adição de suporte para desativar o editor de layout para Adaptive Forms. Hotfix do CQ-4270810
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. Hotfix do CQ-4269463
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. Hotfix do CQ-4264414, CQ-4264914

* Problemas de desempenho quando o aplicativo Adaptive Forms é usado com um conjunto de dados grande. . Hotfix do CQ-4235310

* Quando acessado por meio de uma conta anônima em uma instância de publicação, o script GuideRuntime não é carregado. Hotfix do CQ-4268679

**Forms - Comunicação interativa**

* O modelo de comunicação interativa não lista componentes de cabeçalho e rodapé na lista de componentes permitidos. Hotfix do CQ-4237895
* Ao criar um modelo de impressão de comunicação interativa contendo um campo de imagem, o título do gráfico é definido como em branco. Hotfix do CQ-4264772
* A cor da linha de um gráfico, quando excluída, é definida como indefinida. Hotfix do CQ-4264762
* As alterações na camada de layout feitas no Fragmento do Documento desaparecem ao executar manter as alterações sincronizadas. Hotfix do CQ-4266054
* O elemento do modelo de dados de formulário dentro de um Fragmento do documento vinculado a um campo de texto não mostra o ícone de herança e permite combinação. Hotfix do CQ-4261089
* A API de renderização do Canal de impressão não tem a opção de transferir dados como parâmetro na API. Hotfix do CQ-4263540
* As configurações do agente não estão visíveis, pois a caixa de seleção Editável pelo agente fica desmarcada quando o tipo de vínculo é alterado do fragmento de texto para Nenhum/Objeto de modelo de dados para o campo/variável String. Hotfix do CQ-4261953
* No envio da interface do agente, o arquivo json de dados da Web resultante armazena informações para campos não vinculados cancelados por herança. Hotfix do CQ-4265621

**Forms - Fluxo de trabalho**

* Quando um formulário é reenviado da caixa de saída do aplicativo Adaptive Forms, isso resulta em perda de dados. NPR-28345: Hotfix do CQ-4260929
* Os documentos não são fechados ao salvar em casos não variáveis. Hotfix do CQ-4269784
* O aplicativo Adaptive Forms deixou de oferecer suporte ao Microsoft Windows 8.1. Hotfix do CQ-4265274
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. Hotfix do CQ-4265578

* Ativação das opções de pré-preenchimento para o canal de impressão de comunicação interativa na tarefa Atribuir. Hotfix do CQ-4265577
* Os usuários não poderão visualizar uma tarefa compartilhada até que se tornem membros do grupo ao qual a tarefa está atribuída. Hotfix do CQ-4248733
* Salvar ou enviar aplicativos JEE no aplicativo Adaptive Form está bloqueado no Windows. Hotfix do CQ-4268704
* O modelo de dados de formulário associado à variável do modelo de dados de formulário não é visível. Hotfix do CQ-4266554
* Não há suporte para a variável de status de assinatura do documento usando o suporte à variável. Hotfix do CQ-4266312
* Os envios a partir do espaço de trabalho falham com um caractere de trema. Hotfix do CQ-4263172
* Em uma configuração atualizada, se o fluxo de trabalho for aberto para edição, um erro será exibido em vez do nome do fluxo de trabalho na interface do usuário da pasta monitorada (UI). Hotfix do CQ-4238579

**Forms - Gerenciamento**

* Quando uma extensão diferente de xsd ou schema.json é carregada, o upload não ocorre e nenhuma mensagem de erro é gerada. Hotfix do CQ-4266716

**Forms - Gerenciamento de correspondência**

* [!DNL Experience Manager Forms] 6.5 Falha ao criar interface de usuário de correspondência (CCR UI) ao abrir a correspondência criada com [!DNL Experience Manager Forms] 6.3. Hotfix para CQ-4266392
* A função de soma no XDP não funcionará se o tipo de dados DDE for do tipo número. Hotfix do CQ-4227403
* Faz com que a lógica de invalidação do cache na memória seja atualizada porque, quando um ativo é publicado, o horário da última modificação não é atualizado. Hotfix do CQ-4250465
* Não é possível publicar o fragmento do documento, DD &amp; Letters. Hotfix do CQ-4272893

#### Instalador do Forms JEE

**Gerador de PDF**

* Os arquivos CAD para conversão em PDF falham com o JDK de 64 bits. NPR-29924, NPR-29925: Hotfix do CQ-4272113
* Substituição do nome de PhantomJS para WebToPDF para conversão de HTML em PDF. NPR-29933: Hotfix do CQ-4234545
* Um erro é gerado ao converter o arquivo zip em PDF. Hotfix do CQ-4268628

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. Hotfix do CQ-4272923, CQ-4271002

**Forms - Segurança de documentos**

* A Assinatura digital com o Módulo de segurança de hardware (HSM) não está funcionando no OSGi Linux no Java 11 e Java 8\. NPR-29838: Hotfix do CQ-4270441
* A assinatura digital com o Módulo de segurança de hardware (HSM) não está funcionando no JEE Linux e em todos os servidores de aplicativos compatíveis, ou seja, JBoss e Webphere. NPR-29839: Hotfix do CQ-4266721
* A verificação de assinaturas em um PDF usando o PDF Advanced Electronic Signatures (PAdES) gera InvalidOperationException. NPR-29842: Hotfix do CQ-4244837
* Adição do suporte à Extensão de segurança de documento para o Office 2019\. Hotfix do CQ-4254369, CQ-4259764

**Forms - Serviços de documentos**

* Falha na conversão de PDF em PDF/A-1b com o campo Formulário sem dict de aparência. NPR-29940: Hotfix do CQ-4269618

* OSGi: Não é possível determinar o número de páginas geradas durante a renderização. NPR-28922: Hotfix do CQ-4270870
* Ativado o suporte para arquivos PDF estáticos usando o Forms Service em [!DNL Experience Manager Forms OSGi]. NPR-28572: Hotfix do CQ-4270869
* Não é possível alterar as permissões em XMLForm.exe. NPR-29828, NPR-29237: Hotfix do Q-4267080
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332: Hotfix do CQ-4271002

**Forms - Foundation JEE**

* O pdfg_srt indisponível em artefatos finais faz com que o instalador falhe. NPR-29854: Hotfix do CQ-4270137
* LCBackupMode.sh não está funcionando. NPR-29840: Hotfix do CQ-4269424
* A referência de porta UDP deve ser removida da interface do usuário (UI) do WebSphere. Hotfix do CQ-4264782

### Feature Packs incluídos

#### Ativos - Incluídos

* Ativação do suporte Multi-Site Manager no [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: Hotfix do CQ-4259922

#### Sites - Incluídos

* Exportar [!DNL Experience Manager] fragmentos de experiência para [!DNL Adobe Target]. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Hotfix do CQ-4265469

#### Forms - Serviços de documentos - Incluído

* Somente OSGi: Adicionado um novo atributo PAGECOUNT no Serviço de Saída e Forms. NPR-28922: Hotfix do CQ-4270870
* Somente OSGi: Habilitado o suporte para criar arquivos PDF estáticos usando o Forms Service. NPR-28572: Hotfix do CQ-4270869
* Ativação das permissões no XMLForm.exe para administradores e usuários raiz. NPR-29237: Hotfix do CQ-4267080

### Pacotes de conteúdo e pacotes OSGi

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[Obter arquivo](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[Obter arquivo](assets/6_5-content-package-list.txt)
