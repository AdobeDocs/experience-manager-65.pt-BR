---
title: 'Notas de versão do AEM 6.5 Service Pack '
description: Notas de versão específicas do Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 11%

---


# Notas de versão do Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | **Adobe Experience Manager 6.5** |
|---|---|
| Versão | 6.5.5.0 |
| Tipo | Lançamento do Service Pack |
| Data | 04 de junho de 2020 |
| URL de download | [Compartilhamento](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0)de pacotes, distribuição de [software ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## O que está incluído no Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

O Adobe Experience Manager 6.5.5.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e desempenho, estabilidade, melhorias de segurança, lançadas desde a disponibilização geral da versão 6.5 em **abril de 2019**. Ele pode ser instalado na parte superior do Adobe Experience Manager (AEM) 6.5.

Alguns recursos e aprimoramentos principais introduzidos no AEM 6.5.5.0 incluem:

* Personalizar os nomes das colunas exibidas na Caixa de entrada do AEM.

* Melhorando a acessibilidade em várias áreas na Gestão de conteúdo da Web do AEM (WCM), como o Editor de páginas, Componentes principais, RTE e a interface de usuário do Administrador.

* Salvar uma comunicação interativa como rascunho.

* Suporte para [!DNL Oracle WebLogic 12] o AEM Forms em JEE.

* A manipulação de exceções agora é aprimorada no fluxo da interface do usuário [!DNL Adobe Experience Manager] do Assets.

* Um novo método `getRemoteAssetPublishURL` `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` é adicionado à interface para obter o URL de publicação do Dynamic Media Scene7.

* [Aprimoramentos](#assets-6550-changes) de acessibilidade em [!DNL Adobe Experience Manager] Ativos, em conformidade com as Diretrizes de acessibilidade de conteúdo da Web (WCAG).

* Remoção da integração do Compartilhamento de pacotes com o Adobe Experience Manager.

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.22.3.

Para obter uma lista completa dos recursos, dos principais destaques, dos principais recursos introduzidos no Service Pack 5 do AEM 6.5, consulte [Novidades do Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

A seguir está a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.5.0.

### Sites {#sites-6550}

* O AEM Sites fornece uma opção para publicar ou cancelar a publicação de uma página de seu alias. A opção não funciona (NPR-33415).
* Quando um container de layout é excluído de um modelo que contém vários modelos, o modelo não é renderizado corretamente (NPR-33347).
* Quando uma página do AEM Sites faz parte de um grande conjunto de conteúdo com várias cópias online, a pré-visualização do histórico de versão da página não é carregada (NPR-33311).
* Quando você usa o comando Mover para renomear uma página do AEM Sites, o título da página não é atualizado (NPR-33264).
* Quando você move as páginas pela visualização da coluna, as colunas desaparecem (NPR-33216).
* Quando o nome de um componente local em uma cópia de idioma é idêntico ao nome de um componente no blueprint e o componente é lançado do blueprint, o termo _msm_move não é adicionado ao nome do componente local (NPR-33208).
* O servlet Redirecionamento de página anexa .html a um URL do AEM Sites onde ResourceType não é cq:Page (NPR-33176).
* Ao colar uma subárvore, não há opção para decidir se as subpáginas correspondentes devem ser coladas ou não (NPR-33149).
* O número de resultados em usos ativos de um componente é limitado ao número 49 (NPR-33058).
* Quando você baseia um Fragmento de conteúdo em um schema e ele contém uma área de texto obrigatória ou um campo de caminho, o Fragmento de conteúdo não é salvo (NPR-33007).
* Ao criar um componente personalizado usando o componente de fragmento de experiência pronto para uso e usá-lo nas páginas do AEM Sites, o AEM não exibe referências (uso) para o componente personalizado (NPR-32852).
* Ao renomear uma pasta com um grande número de referências, muitas referências à pasta não são atualizadas (NPR-32765).
* Quando você ativa a opção de edição de origem, ela fica disponível para opções de tela cheia em linha, mas permanece ausente na caixa de diálogo de edição e nas opções de tela cheia do editor de rich text (NPR-32763).
* Se você tiver um campo múltiplo e ele contiver um campo obrigatório (como um menu suspenso ou um campo de caminho) nas propriedades da página de um blueprint, quando uma página que contém esse campo múltiplo for distribuída, as propriedades da página da live copy não serão salvas. (NPR-32751)
* Os leitores de tela não podem usar a estrutura de cabeçalho para navegar em uma página. Além disso, a guia Componentes tem o rótulo errado (NPR-32648).
* Quando start de paginação, o Seletor de fragmentos de experiência não carrega todos os itens (NPR-32605).
* As permissões do autor para ler, modificar, criar e excluir cópias online são revogadas. Cada autor tinha que fornecer permissões de leitura e modificação explícitas para mover páginas em um Blueprint (NPR-32550).
* Os autores de conteúdo não conseguem criar o Launch para uma página que tenha uma integração com o Adobe Analytics (NPR-32548).
* Quando um usuário retoma a herança com a sincronização, a cópia online da página pai não é sincronizada com o blueprint e exibe um status incorreto (NPR-32500).
* A página do editor do AEM Sites leva mais de 15 segundos para ser carregada (NPR-32413).
* Determinados campos não exibem a opção Cancelar herança (NPR-32362).
* Quando você seleciona um caminho para um componente de Fragmento de experiência e seleciona a caixa de seleção Abrir caixa de diálogo de seleção, você não navega até o caminho selecionado no Navegador de caminhos (NPR-32308).
* Ao atualizar do AEM 6.2 para o AEM 6.5, o componente Parsys dos modelos estáticos não é exibido corretamente. A altura do componente Parsys é definida como 0 e os componentes dentro dele não são visíveis. (NPR-33663).
* Quando um usuário copia e cola um Container de layout na mesma página, os componentes em um Container de layout não são exibidos (NPR-33648).
* A verificação de integridade do Dispatcher exibe uma mensagem de `Invalid cookie header` aviso nos arquivos de registro (NPR-33629).

### Ativos {#assets-6550-changes}

**Aprimoramentos de acessibilidade nos ativos Experience Manager**

* Agora é possível colocar o foco do teclado na lista [!UICONTROL Comentários] e na opção clicável para [!UICONTROL Criar] comentários da versão em [!UICONTROL Criar nova versão] no painel Ativos da [!UICONTROL Linha] do tempo (NPR-33424).

* Agora é possível acessar a opção Configurações [!UICONTROL de] Visualização para ativos e alterar configurações na caixa de diálogo Configurações [!UICONTROL de] Visualização usando teclas de teclado (NPR-33420).

* A caixa de lista suspensa da caixa de combinação (em vários campos em páginas diferentes) agora mostra as entradas como uma lista de opções que podem ser anunciadas pelos leitores de tela (NPR-33516).

* A funcionalidade de classificação dos cabeçalhos classificáveis (na visualização da lista, na visualização da [!UICONTROL Linha] do tempo e na página [!UICONTROL Gerenciar publicação] ) agora é anunciada pelos leitores de tela e os controles de classificação nos cabeçalhos das colunas são acessíveis usando o teclado (NPR-32979).

* Os elementos clicáveis (como cartões de comentário, atualizações de versão, caixas de combinação e ícones de divisa de menus) agora são focalizáveis e acionáveis usando o teclado (NPR-33514).

* A funcionalidade (ou finalidade de ação) dos ícones de insights (para uso, impressões e cliques) na Visualização [!UICONTROL do] Insights agora são anunciados corretamente pelos leitores de tela (NPR-33513).

* Campos de formulário somente leitura (por exemplo, campos desativados na guia  Básica de [!UICONTROL Propriedades]de ativos) agora são focalizáveis usando o teclado (NPR-33493, CQ-4273031).

* Rótulos em vários campos de entrada agora são rótulos permanentes (portanto acessíveis) e não apenas rótulos de espaço reservado, que desapareceram quando o texto foi digitado (NPR-33475).

* Níveis de cabeçalho diferentes (como títulos de página e cabeçalhos de seção) agora são percebidos como cabeçalhos com níveis diferentes para usuários de leitores de tela (NPR-33471).

* Elementos interativos da interface do usuário, como links e opções (no cabeçalho e nas opções de zoom da página de ativos, navegação de pastas), agora são acessíveis usando um teclado (NPR-33468, CQ-4271412).

* Os indicadores de progresso [!UICONTROL Opções], [!UICONTROL Escopo]e [!UICONTROL Workflows] na página [!UICONTROL Gerenciar publicação] agora são lidos corretamente pelos leitores de tela como indicadores de progresso, em vez de guias (NPR-33416).

* A cor dos ícones de classificação de estrelas (como na seção [!UICONTROL Classificação] da guia [!UICONTROL Avançado] em [!UICONTROL Propriedades] do ativo ou na visualização do cartão) é alterada para que o contraste adequado seja visível aos usuários com visão limitada e sem percepção de cor (NPR-33414).

* A seta para cima ao lado do campo [!UICONTROL Comentário] na página de detalhes dos ativos agora pode ser acessada usando teclas do teclado (NPR-33397).

* Os estados expandidos e recolhidos da caixa de diálogo [!UICONTROL Tags] em [!UICONTROL Propriedades] do ativo e navegação do painel esquerdo (na interface do usuário do ativo) agora são anunciados corretamente pelos leitores de tela (NPR-33396).

* Os títulos de todas as páginas navegadas em [!DNL Adobe Experience Manager] Ativos agora são exclusivos (NPR-33343).

* Ao navegar pela estrutura da árvore, vários elementos do controle de visualização da árvore agora são anunciados corretamente pelos leitores de tela (NPR-33304).

* Diferentes versões de ativos na visualização da [!UICONTROL Linha] do tempo na página de detalhes de ativos agora estão acessíveis usando teclas de teclado (NPR-33283).

* Os nomes das sugestões de pesquisa que aparecem na caixa de combinação Omnisearch são anunciados pelos leitores de tela ao usar a funcionalidade de pesquisa (NPR-33280).

* Os elementos clicáveis e [!UICONTROL Ir para o link] no painel [!UICONTROL Referências] agora são anunciados pelos leitores de tela como elementos clicáveis (NPR-33278).

* As informações de estrutura de tabela (como linha 1, célula 1, tabela) da caixa de diálogo [!UICONTROL Compartilhar link] não são mais anunciadas pelos leitores de tela quando a caixa de diálogo é aberta (NPR-33268).

* A finalidade de vários elementos da caixa de combinação (como campo Caminho e opção para abrir a caixa de diálogo Seleção na guia Básica das Propriedades do ativo) agora são anunciados corretamente pelos leitores de tela (NPR-33235).

* As informações de que as linhas na tabela visualização da lista são selecionáveis agora são comunicadas aos usuários do leitor de tela quando o foco do teclado está sobre eles. Essas informações são anunciadas quando o mouse é posicionado sobre as linhas (NPR-33234).

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

* A finalidade do ícone [!UICONTROL x] na opção de remover as tags atualmente selecionadas também é anunciada juntamente com o número de tags selecionadas (CQ-4273017).

* Os ícones e imagens decorativos agora são ignorados pelos leitores de tela para evitar confusão para usuários sem visão usando leitores de tela (CQ-4272944).

**Problemas corrigidos nos ativos do Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Os ativos fornecem correções para os seguintes problemas:

* [!UICONTROL A opção Start] na caixa de diálogo [!UICONTROL Criar fluxo de trabalho] para ativos em uma coleção está desativada, impedindo assim que o fluxo de trabalho seja acionado (NPR-32471).

* Ao usar o menu suspenso em cascata em schemas de metadados, ao selecionar e salvar uma opção suspensa contendo um apóstrofo (do menu suspenso filho), a opção de apóstrofo selecionada desaparece após reabrir [!UICONTROL Propriedades] do ativo (NPR-32649).

* [!UICONTROL A tarefa] de sincronização do Asset Insights será interrompida e falhará se encontrar entradas inválidas (no lado do Analytics) em vez de mover-se para a próxima entrada (NPR-32674).

* O giroscópio não é funcional, pois os sensores de movimento são desativados por padrão nos navegadores móveis no visualizador panorâmico (CQ-4272937).

* [!UICONTROL O Assistente de configuração] de ativos conectados falha ao funcionar com o erro 404, ao instalar a versão 6.5.3 na versão 6.5.1 (NPR-32730).

* Durante o processo de gravação de retorno XMP, todas as propriedades de metadados de namespace personalizados alteram o prefixo de namespace personalizado para ns2 em vez do prefixo de namespace configurado (NPR-32748).

* O carregamento lento não é acionado e somente 100 ativos são exibidos ao selecionar para revisar as tarefas da caixa de entrada de notificações (NPR-32750).

* `NullPointerException` for observado devido a preferências de nó ausentes no perfil de usuário recém-criado (SAML/SSO). Esse erro impede que usuários recém-conectados usem a [!DNL Adobe Experience Manager Stock] integração (NPR-32777).

* Os avisos transversais são observados nos registros ao abrir uma coleção inteligente que contém mais de 10.000 ativos (NPR-32980).

* Os nomes dos ativos são alterados para minúsculas ao mover ativos de uma pasta para outra no modo de execução [!DNL Adobe Experience Manager] do Dynamic Media Scene7 (NPR-32995).

* Um ativo pesquisado não pode ser excluído depois de navegar para suas propriedades a partir dos resultados da pesquisa e voltar para os resultados da pesquisa para excluí-lo (NPR-32998).

* [!UICONTROL A opção Próxima] permanece desativada ao selecionar a pasta de destino na interface [!UICONTROL Mover ativos] (NPR-33356).

* [!UICONTROL A opção Próxima] não está ativada na seleção do nó pai (onde a pasta filho único está visível) e na seleção da pasta filho (NPR-33275).

* As permissões de check-in e check-out são desativadas no Adobe Asset Link (AAL) para usuários com permissão de exclusão, mesmo se outras permissões, como ler, criar ou modificar, forem permitidas para eles (NPR-33272).

* As execuções de Recorte inteligente não estão disponíveis na caixa de diálogo de download de ativos (NPR-33167).

* Exceção observada em registros ao abrir o painel de execuções para um PDF em uma pasta com perfil de recorte inteligente (CQ-4294201).

* As predefinições de imagem não publicam, se o modo [!UICONTROL de sincronização de Mídia] dinâmica estiver desativado por padrão no AEM com o modo de execução Dynamic Media Scene7 (CQ-4294200).

* O processamento de ativos enquanto o carregamento em massa fica travado e a instância do fluxo de trabalho mostra instâncias presas do ativo de atualização do DAM (CQ-4293916).

* Criar uma configuração de Dynamic Media no AEM funciona, mas na interface do usuário nada acontece ao selecionar Salvar (CQ-4292442).

* A Pré-visualização de ativos de vídeo f4v não está funcionando na reprodução progressiva no Safari/Mac (CQ-4289844).

* A pasta extra é criada ao recortar inteligente um ativo que está dentro de uma pasta pai com `.` caractere de ponto em seu nome (CQ-4289337).

* A miniatura está quebrada e o banner de processamento de vídeo não é exibido quando um vídeo é copiado (CQ-4284125).

* O visualizador dimensional exibe incorretamente miniaturas vazias no Firefox para alguns modelos com visualizações de câmera vazias (CQ-4283447).

* Problemas de desempenho corrigidos na versão 6.5.5.0 são (CQ-4279206):

   * O carregamento de binários grandes leva muito tempo para os servidores de processamento de imagem de Dynamic Media.

   * O tempo de geração de miniaturas no AEM aumenta devido à arquitetura do Dynamic Media Scene7.

* Problemas de migração do Dynamic Media Scene7 falham para clientes com um grande número de ativos (CQ-4279206).

* O layout do visualizador do vídeo 360 será quebrado se `setVideo` for usado e o vídeo será mudado para baixo ao usar `video= modifier` (CQ-4263201).

* Uma mensagem de erro é exibida durante a instalação do pacote SDL AEM (NPR-33175).

### Plataforma {#platform-6550}

* O [!DNL Sling] filtro não será chamado se a entrada do `sling:match` mapa for criada em `/etc/maps` (NPR-33362).
* O AEM trava devido a falha de segmentação com [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] pacote principal ausente do arquivo jar uber do AEM (NPR-32848).
* O CRXDE Lite não carrega conteúdo para usuários sem permissão de LEITURA na `jcr:primaryType` propriedade de um nó (NPR-32611).
* [!DNL Granite] o scheduler da tarefa de manutenção é reinicializado com muita frequência durante as implantações do AEM (CQ-4294627).
* Quando um query SQL é executado por um tempo maior, por exemplo, 7 horas, o AEM deixa de responder (NPR-33044).

### Interface do usuário {#ui-6550}

* A seleção de botões de opção não persiste em um campo múltiplo (NPR-33309).
* O limite de carregamento lento não funciona para a visualização da lista (NPR-33124).
* A página de resultados do Omnisearch não exibe uma mensagem se não houver correspondências (NPR-32974).
* O filtro Omnisearch retorna todas as correspondências em `/content` nós ignorando o local selecionado (NPR-32849).

### Integrações {#integrations-6550}

* O cache interno é apagado quando uma página com um componente de Público alvo da Adobe é publicada (NPR-33162).
* A integração com o Público alvo da Adobe não funciona no [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Ao configurar o Adobe Público alvo, os campos [!UICONTROL Empresa] e Conjunto [!UICONTROL de] relatórios não aparecem ao selecionar uma fonte de relatórios (NPR-32502).
* Ao exportar fragmentos de experiência usando a E/S da Adobe, metadados como Produto de origem não são exportados para o Adobe Público alvo (NPR-32159).
* Os usuários autorizados do IMS no grupo de administração local do AEM não podem criar ou modificar configurações do IMS (NPR-33045).
* A página de configurações do Adobe Launch não exibe todos os registros (NPR-33011).
* Os usuários do grupo de autores de conteúdo não podem editar as propriedades de um componente de Público alvo da Adobe devido ao erro de JavaScript (NPR-32996).

### Projetos de tradução {#translation-6550}

* As tags traduzidas não são importadas para o AEM a partir de serviços de tradução de terceiros (NPR-33154).
* A página de configuração de tradução exibe um provedor de tradução incorreto que o usado para a tradução (NPR-32971).
* Adicionar uma pasta de fragmento de experiência a um projeto de tradução existente cria um novo projeto (NPR-32843).
* Um `NullPointerException` erro é visto nos registros ao executar um trabalho de tradução (NPR-32628).

### WCM {#wcm-6550}

* Editor de páginas - O Editor de [!DNL Sites] páginas não permite que os usuários somente do teclado pulem para o conteúdo principal em vez de deslocar o foco da guia por todas as opções disponíveis no cabeçalho (CQ-4293883).
* Editor de páginas - Os painéis que usam o componente Bem e incluem dados salvos não são exibidos devido a atualizações em [!DNL Chrome] e [!DNL Firefox] versões (CQ-4292995).
* MSM - A exclusão de um componente da página não exclui o componente da versão publicada da página (CQ-4292360).

### Brand Portal {#assets-brand-portal-6550}

* Remover um schema de metadados publicado [!DNL Brand Portal] resulta em um erro (CQ-4292063).
* Se um administrador configurar [!DNL Experience Manager Assets] 6.5.4 com o Brand Portal via Adobe Developer Console, o [!DNL Brand Portal] usuário não poderá publicar o ativo de uma pasta de contribuição de [!DNL Brand Portal] para [!DNL Experience Manager]. (NPR-33046).
* Replicação de Duplicado das pastas pai que causam conflitos (NPR-33001).

### Communities {#communities-6550}

* Não é possível excluir um cartão no console de moderação usando a opção de menu de edição rápida (NPR-33117).
* Ocorre um erro ao acessar a página [!UICONTROL Atividade Stream] (NPR-33146).
* Grupos excluídos na instância do autor não são removidos de todas as instâncias de publicação (NPR-33199).
* Após a criação de um novo grupo, os autores não são redirecionados para a seção Grupo [!UICONTROL da] Comunidade no [!DNL Internet Explorer] 11 (NPR-33205).
* O acesso a uma mensagem na Caixa de entrada do AEM não altera o status da mensagem para Lido (NPR-32764).
* Editar um [!DNL Communities] grupo e alterar a imagem em miniatura não atualiza a imagem em miniatura do grupo (NPR-32599).
* Um usuário não pode enviar um email para outro usuário em uma comunidade (NPR-32598).
* Um blog enviado não é exibido até que o usuário atualize a página (NPR-32391).
* Ao criar uma versão de notificações e subscrições de Conteúdo gerado pelo usuário (UGC), uma ID incorreta da página de origem é armazenada (CQ-4279355, CQ-4289703).

### Fluxo de trabalho {#workflow-6550}

* A opção [!UICONTROL Linha] do tempo no painel esquerdo leva mais tempo para carregar do que o esperado (NPR-32851).
* Após reiniciar uma instância do AEM, o email para a tarefa de revisão de uma coleção inclui um link de carga incorreto (NPR-32774).

### Forms {#forms-6550}

>[!NOTE]
>
>O AEM Service Pack não inclui correções para o AEM Forms. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o AEM Forms no JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

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

* AEM 6.5.5.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* O download do Service Pack está disponível no Compartilhamento de pacotes da Adobe, que pode ser acessado diretamente da instância do AEM 6.5.
* Em uma implantação com MongoDB e várias instâncias, instale o AEM 6.5.5.0 em uma das instâncias do autor usando o Gerenciador de pacotes.
* Antes de instalar, faça um instantâneo ou um backup atualizado da sua instância do AEM.
* Reinicie a instância antes da instalação. Embora isso seja necessário apenas quando a instância ainda está no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior), é recomendável se a instância estava em execução por um período mais longo.

>[!NOTE]
>
>A Adobe não recomenda remover ou desinstalar o pacote AEM 6.5.5.0.

### Instale o Service Pack {#install-service-pack}

Execute as seguintes etapas para instalar o Service Pack em uma instância do AEM 6.5 existente:

1. Clique no link Compartilhamento [de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0) pacotes ou Distribuição [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) software para baixar o pacote.

1. Abra o Gerenciador [de](http://localhost:4502/crx/packmgr/index.jsp) pacotes e clique em **Carregar pacote** para fazer upload do pacote.

1. Selecione o nome do pacote e clique em **Instalar**.

>[!NOTE]
>
>**A caixa de diálogo na interface do usuário do Gerenciador de pacotes às vezes sai imediatamente durante a instalação da versão 6.5.5.0**
>
>Portanto, é recomendável aguardar a estabilização dos registros de erros antes de acessar a instância. O usuário deve aguardar os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Geralmente isso acontece no Safari, mas pode acontecer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente o AEM 6.5.5.0 em uma instância em execução:

A. Coloque o pacote na `../crx-quickstart/install ` pasta enquanto o servidor estiver disponível on-line. O pacote é instalado automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/pt/crx/2-3/how_to/package_manager.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>O AEM 6.5.5.0 não oferece suporte à instalação do Bootstrap.

**Validar instalação**

1. A página Informações do produto (/system/console/ productinfo) exibe a string da versão atualizada `Adobe Experience Manager, Version 6.5.5.0` em Produtos instalados.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. The OSGI bundle `org.apache.jackrabbit.oak-core` is on version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms. As correções do AEM Forms são entregues por meio de um pacote complementar separado.

1. Verifique se você instalou o AEM Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções no AEM Forms em JEE são entregues por meio de um instalador separado.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/br/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

The UberJar for AEM 6.5.5.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

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
| Integrações | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Com a integração do AEM e do Público alvo atualizada no AEM 6.5 para suportar a API do Público alvo Standard, que usa autenticação por meio do Adobe IMS e E/S, e a função crescente do Adobe Launch para instrumentar páginas do AEM para análise e personalização, o assistente de opção de participação se tornou funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e integrações de E/S da Adobe por meio dos respectivos serviços em nuvem do AEM |

## Problemas conhecidos {#known-issues}

* Se você estiver instalando [!DNL Experience Manager] 6.5.5.0 com [!DNL Java] 11, reinicie o servidor após instalar o Service Pack. Não é necessário reiniciar se você estiver instalando o Service Pack com [!DNL Java] 8.

* Se uma pasta na hierarquia for renomeada [!DNL Experience Manager Assets] e a pasta aninhada que contém um ativo for publicada, o título da pasta não será atualizado [!DNL Brand Portal][!DNL Brand Portal] até que a pasta raiz seja publicada novamente.

* A atualização da [!DNL chrome] versão 83 está causando um problema na criação de pacotes. Use outros navegadores disponíveis, como [!DNL Internet Explorer] e [!DNL Firefox], ou outras opções de instalação de pacote padrão do AEM para resolver o problema.

* Não é possível enviar um email para o servidor SMTP remoto usando o remetente de email padrão do AEM, pois ele permite apenas a comunicação usando TLS v1.2. Remova o pacote `javax.mail:mail:1.5.0-b01` de `system/console` e atualize os pacotes para resolver o problema.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Se o assistente de configuração [!UICONTROL de ativos] conectados retornar uma mensagem de erro 404 após a instalação, reinstale manualmente os pacotes `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` pacotes usando o Gerenciador de pacotes.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do AEM 6.5.x.x:
   * &quot;Quando a integração do Target é configurada no AEM usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granito/operações/manutenção.
   * A validação do lado do servidor do Formulário adaptável falha quando funções de agregação, como SUM, MAX e MIN são usadas. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Não foram encontradas janelas de manutenção em granito/operações/manutenção.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.

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

