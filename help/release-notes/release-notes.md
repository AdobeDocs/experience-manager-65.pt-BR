---
title: Notas de versão do  [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista de alterações detalhada para o [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 1fb7c9b718896b18471b2bd86fab3c351d50312e
workflow-type: tm+mt
source-wordcount: '8932'
ht-degree: 5%

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
| Versão | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do pacote de serviços |
| Data | 26 de novembro de 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## O que está incluído em [!DNL Experience Manager] 6.5.24.0 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de desempenho, estabilidade e segurança lançadas desde a disponibilização inicial do 6.5, em abril de 2019. [Instalar este Service Pack](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!--
## Key features and enhancements
-->




## Correção de problemas no Service Pack 24 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* Depois de atualizar para a versão 6.5.23.0, classificar pastas por data de modificação no Modo de Exibição de Cartão causou dificuldades em localizar ativos modificados recentemente para implantações locais. (ASSETS-56946)
* Entradas repetidas de log de aviso são geradas durante as execuções do programador. (ASSETS-52554)
* A classificação de títulos não está funcionando na Exibição de lista. (ASSETS-50716)
* A janela Propriedades da coleção não fecha mesmo depois de clicar no botão Cancelar. (ASSETS-48504)

* Erro *URL inválida* ao tentar anotar ativos no AEM 6.5.22. (NPR-42684)
* O formulário do Editor de metadados Assets não é reinicializado após executar ações relacionadas ou não relacionadas. (ASSETS-52207)
* Quando os ativos do DAM remoto são ressincronizados ao local do Sites, o status publicado dos ativos é atualizado incorretamente para `Not published`. (ASSETS-48958)
* Problemas encontrados durante a atualização do SP23 para a versão 6.5 LTS. (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### Acessibilidade {#sites-accessibility-6524}

* A caixa de diálogo **Alternar formato de exibição** agora dá suporte à operação completa do teclado. O foco não ignora mais o botão **Exibir Configurações**, e as chaves padrão (`Tab`, `Enter`, `Space`) funcionam de forma consistente. (SITES-24306)
* Usuários de teclado podem remover as tags de status publicadas sem o mouse. O foco vai para cada marca e a ativação funciona com `Enter`/`Space` e Backspace/Delete. Agora o controle de tag se comporta como um botão, o que melhora o feedback do leitor de tela e atende ao teclado WCAG 2.1.1. (SITES-24491)
* O painel Filtros flui responsivamente em visores estreitos. Os controles de seleção e os resultados ficam dentro da janela de visualização com 400% de zoom, eliminando a rolagem horizontal e o corte de conteúdo. (SITES-24708)
* O AEM restaura o acesso completo do teclado aos botões Redefinir, Personalizar e Dispositivo do ContextHub. Teclas de tabulação e seta alcançam cada controle, mostram um indicador de foco visível e ativam ações com `Enter` ou `Space`. Os leitores de tela anunciam rótulos claros. (SITES-24939)
* A entrada de data e o seletor permanecem totalmente visíveis em 320 px. O modal do Timewarp usa dimensionamento responsivo, de modo que o controle não é mais recortado ou desaparece na menor janela de visualização. (SITES-24962)
* O painel de Referências agora é compatível com zoom de 400% do navegador sem perder acesso ao conteúdo. O painel usa dimensionamento responsivo em vez de uma largura fixa, de modo que os itens permanecem visíveis e selecionáveis em 1280×1024. (SITES-24972)
* Agora o Painel de filtros funciona com zoom de 400%. O painel é redimensionado com unidades relativas e não bloqueia ou oculta os controles de filtro. Os usuários podem visualizar e selecionar cada opção de filtro sem rolagem horizontal ou destinos de ocorrência recortados. (SITES-24981)
* Os usuários de teclado podem operar menus de formatação no modal Teaser. Pressionar `Enter` ou `Space` em **Lista** ou **Formato de parágrafo** abre as opções pop-up, teclas de seta para navegar e `Enter` aplica a seleção. O `Escape` fecha o menu e restaura o foco para o controle de acionamento, produzindo um fluxo de trabalho consistente da barra de ferramentas. (SITES-25235)
* O popover do seletor de cores de amostra agora permanece dentro do visor a 320 px. O popover mostra todas as linhas coloridas e oferece suporte à rolagem, para que os autores possam selecionar qualquer amostra em telas pequenas. (SITES-25274)
* Os menus suspensos da barra de ferramentas demográfica agora funcionam totalmente com o teclado. A abertura de um menu move o foco para a primeira opção, as teclas de seta navegam na lista e Esc/Tab fecham ou avançam sem descarregar o foco na barra de ferramentas. Os itens interativos usam a semântica adequada para que o NVDA e outros leitores anunciem as opções corretamente. (SITES-25310)
* Adicionar componente na árvore de conteúdo funciona conforme projetado no AEM 6.5 SP24. O erro inicial veio da falta de permissões de autor em uma configuração local, não do AEM. Os autores com direitos de edição podem ativar o botão e adicionar componentes por teclado ou mouse. (SITES-25312)
* O acesso ao teclado e ao leitor de tela na barra de ferramentas Demográfica agora funciona de forma confiável. Os autores que usam o NVDA podem percorrer **Commerce**, **Persona** e 88 com setas, observar comentários de foco claros e entender qual guia está ativa. (SITES-25326)

* O link **Pular para conteúdo** agora move o foco do teclado para o cabeçalho do conteúdo principal. O foco permanece visível em um destino identificado exclusivamente, de modo que os leitores de tela anunciam a seção correta. A alteração atende à WCAG 2.4.1 e 2.4.3. (SITES-24061)
* A navegação pelo teclado na árvore da página inicial do Sites segue uma sequência lógica após usar **Selecionar tudo**. O foco move de **Selecionar tudo** para o próximo controle (Abrir painel esquerdo), em vez de voltar para o início da página. (SITES-24307)
* Os títulos das seções e controles de edição no editor de sites respondem ao foco e à ativação do teclado. Os usuários de teclado revelam o mesmo título e ações que antes apareciam apenas ao passar o mouse. (SITES-24479)
* Os botões no editor de sites expõem nomes descritivos em vez de rótulos genéricos ou ausentes. As tecnologias assistivas anunciam a ação correta, o que melhora a clareza e reduz os erros de clique. (SITES-24480)
* Os leitores de tela recebem uma mensagem de &quot;Carregamento&quot; falada enquanto a exibição do Sites é atualizada. A atualização adiciona uma região ativa de status dedicada e grava a mensagem nela programaticamente, o que confirma o progresso sem mover o foco. (SITES-24481)
* O painel lateral do Assets agora inclui um controle **Fechar** limpo e retorna o foco ao botão de alternância. Os usuários de teclado e leitor de tela descartam o painel imediatamente, em vez de navegar por todos os controles. A alteração reduz os pressionamentos de tecla e corresponde ao comportamento esperado do painel. (SITES-24489)
* A lista da guia ARIA no Editor de páginas inclui um nome descritivo. Agora, os leitores de tela identificam o controle como uma lista de guias e leem o rótulo correto, permitindo que os usuários encontrem o conjunto correto de guias e se movam entre elas de maneira confiável. (SITES-24492)
* A pesquisa no painel lateral do Editor agora anuncia resultados para leitores de tela. À medida que os usuários digitam, uma mensagem de status em tempo real informa o número de correspondências e atualizações sem mover o foco. Os usuários de teclado descobrem os resultados imediatamente. (SITES-24506)
* A seleção de linha na Exibição de lista melhora para usuários da tecnologia assistiva. A caixa de seleção expõe um nome significativo derivado da linha Título, de modo que os anúncios permanecem breves e descrevem a ação corretamente. (SITES-24514)
* Nomes de acessibilidade corrigidos do Modo de Exibição de Lista. A tabela remove `aria-label` de elementos não interativos e atribui o rótulo ao link ou botão acionável. Os usuários de leitores de tela agora ouvem rótulos precisos e não duplicados na coluna. (SITES-24515)
* O cabeçalho fixo parou de ocultar a caixa de diálogo modal do teaser durante o uso de zoom elevado. O conteúdo permanece legível e utilizável em 200% e 400% de zoom, com fluxo vertical e sem seções recortadas. (SITES-24523)
* Digitar no campo de pesquisa não aciona mais um anúncio prematuro do primeiro resultado ou uma ativação acidental. A experiência agora anuncia uma mensagem de status concisa com a contagem de resultados, enquanto o foco permanece no campo até que o usuário navegue para a lista. (SITES-24658)
* O campo Texto alternativo na caixa de diálogo de hiperlink do editor de texto agora expõe um rótulo programático. Os leitores de tela anunciam &quot;Texto alternativo&quot; para o campo e o foco chega ao controle nomeado corretamente. Essa correção melhora a navegação para usuários de teclado e fala. (SITES-24675)
* Adição de uma mensagem de status em tempo real ao painel Referências para que as tecnologias assistivas anunciem as alterações imediatamente. Selecionar vários itens aciona uma mensagem clara sobre a disponibilidade de referência, o que impede alterações de estado silenciosas e reduz ações repetidas. (SITES-24678)
* A caixa de diálogo Imagem agora anuncia seu estado de carregamento por meio de uma região ARIA ativa. Os leitores de tela ouvem a mensagem &quot;Loading, please wait&quot; (Carregando, aguarde) enquanto o ponteiro do mouse aparece. É uma atualização pronta quando o conteúdo é concluído, para que os usuários saibam quando podem interagir. (SITES-24697)
* A caixa de diálogo Link selection agora expõe uma região ativa que anuncia os resultados da pesquisa. Os leitores de tela ouvem o status &quot;resultados atualizados&quot; após cada pesquisa sem mover o foco, para que os usuários obtenham uma confirmação clara de que a pesquisa foi concluída. (SITES-24700)
* A caixa de diálogo de seleção de Link agora reflui a 320 px. Todos os campos e ações permanecem visíveis e utilizáveis, e a barra de rolagem horizontal não é mais exibida. (SITES-24709)
* A caixa de diálogo Seleção de link agora usa o mesmo rótulo para o texto na tela e o nome acessível em cada item da árvore. Os leitores de tela anunciam cada item enquanto se movem com as teclas de seta, incluindo o último nível, eliminando nós silenciosos e nomes incompatíveis. (SITES-24710)
* Alterar filtros agora relata seu estado como expandido ou recolhido. O botão alterna `aria-expanded` em sincronia com o painel de filtros e expõe um único nome limpo (&quot;Alterar filtros&quot;), removendo o confuso &quot;filtro?&quot; anúncio. Os usuários de leitores de tela podem prever o resultado da ativação do controle. (SITES-24713)
* Os cabeçalhos modais não abrangem mais o conteúdo a 320 px de largura. O cabeçalho sai do estado fixo e o corpo da caixa de diálogo rola, de modo que todos os campos e botões de ação permanecem visíveis e utilizáveis. Os usuários do teclado podem alcançar todos os controles sem perder o foco. (SITES-24718)
* Os links de Navegação do aplicativo agora expõem a semântica de link adequada. Os leitores de tela anunciam cada item como um link em vez de um item de lista, o que melhora a navegação pelo teclado e o controle de voz. O container de lista mantém a semântica da lista, enquanto os links permanecem como destinos focalizáveis. (SITES-24719)
* O status dos resultados agora anuncia aos leitores de tela quando os filtros são alterados. O NVDA lê a contagem de &quot;X de Y resultados&quot; e a mensagem &quot;nenhum resultado&quot;. O status de paginação usa uma região ativa que é atualizada no local, de modo que os usuários ouvem a confirmação sem mudar o foco. (SITES-24720)
* O botão de rotação na caixa de diálogo Carrossel agora anuncia um nome único e conciso para os leitores de tela. O controle não repete mais o rótulo do grupo e o rótulo de entrada, o que reduz a verbosidade e a confusão para os usuários do NVDA. (SITES-24725)
* A lista de pesquisa do menu Ajuda expõe a semântica adequada. O contêiner apresenta uma lista e cada resultado permanece um link sem uma função conflitante. O NVDA e o JAWS anunciam os links com precisão e a navegação permanece consistente. (SITES-24729)
* O Adobe corrigiu o pop-up de amostra de cor nas Preferências do usuário para que o NVDA anuncie a amostra em foco, não a amostra selecionada anteriormente. Os usuários de teclado ouvem nomes de cores precisos ao percorrerem a lista e podem confirmar a seleção correta. (SITES-24739)
* O NVDA agora lê a Descrição completa no diretório Árvore. O painel de detalhes expõe o texto multilinha como um valor e o vincula ao rótulo do campo. Os usuários do teclado ouvem o texto completo enquanto percorrem os campos somente leitura com a tecla tab. (SITES-24780)
* O diretório da árvore agora anuncia a data de Modificação. O NVDA lê a data quando o foco é movido para a coluna Modificado. A grade vincula cada data ao nome do item para que os usuários ouçam o arquivo e sua última atualização. (SITES-24782)
* O modo de visualização agora atende às preferências de espaçamento de texto do usuário. A tela reflete as alterações de letra, palavra e altura de linha em todo o conteúdo visualizado. O texto não fica mais fixo ou corta enquanto o espaçamento aumenta. Usuários de teclado e com pouca visão leem o conteúdo sem quebras no layout. (SITES-24936)
* O AEM corrige a ordem das guias nas páginas do Assets Editor. A tabulação agora se move dos controles de cabeçalho para os botões do hub de contato e, finalmente, para as ferramentas da tela em uma sequência clara. Os leitores de tela seguem a mesma ordem, o que remove confusão e acelera a navegação pelo teclado. (SITES-24937)
* O AEM adiciona um nome programático à barra de menu Ações do cartão. Os leitores de tela anunciam o controle corretamente, e os usuários de fala podem direcioná-lo por nome. A navegação e o foco do teclado permanecem inalterados. (SITES-24938)
* Os menus de Exibição de cartão respeitam o aumento do espaçamento do texto. O item Mais ações cresce e não trunca mais os rótulos, incluindo a Publicação rápida. Os usuários que geram espaçamento entre letras, palavras ou linhas mantêm rótulos completos e acesso ao teclado. (SITES-24941)
* Removida a função &quot;apresentação&quot; que ocultava a tabela da página inicial do Sites da árvore de acessibilidade. A tabela é lida corretamente novamente. O NVDA e o JAWS detectam a tabela, reconhecem cabeçalhos e anunciam relações de cabeçalho durante a navegação de linha e coluna. (SITES-24942)
* A classificação do feedback na Exibição de lista é explícita e consistente. Após uma classificação, o cabeçalho expõe a ordem através de `aria-sort`. Ele anuncia a alteração, enquanto os cabeçalhos não classificados não reivindicam mais um estado, ajudando os usuários de leitores de tela a rastrear qual coluna controla a classificação. (SITES-24943)
* O cabeçalho Editar layout não expõe mais um botão **Editar** não funcional. O controle agora atua como um rótulo de status estático e permanece fora da ordem de tabulação, de modo que os usuários de teclado não desperdiçam um toque de tecla. Use **Selecione outro modo** para alterar modos, com comentários claros sobre o leitor de tela. (SITES-24950)
* A barra de ferramentas do emulador mostra nomes completos de dispositivos por padrão. O rótulo não trunca mais durante o carregamento, portanto, os usuários podem ler e selecionar dispositivos sem adivinhação. O texto é perfeitamente dimensionado em níveis de zoom e larguras estreitas. (SITES-24952)
* A barra de ferramentas do emulador cabe em pequenos visores. A 320 pixels, a lista de dispositivos e controla a exibição sem recorte, para que os usuários possam selecionar o Galaxy S7 e modelos mais recentes. O layout é dimensionado e envolvido para evitar rolagem horizontal mesmo com zoom de 400%. (SITES-24953)
* Os leitores de tela anunciam o dispositivo selecionado e suas medidas no Emulador. O NVDA interrompe a leitura do fluxo da régua; o botão do dispositivo usa uma descrição anexada para o texto da dica de ferramenta, o que reduz o ruído e orienta a navegação. (SITES-24955)
* A barra de filtros agora trata cada tag selecionada como um botão de ação. Limpar os nomes acessíveis e o manuseio de foco melhora os anúncios e o controle do teclado. (SITES-24980)
* Atualizações de status no anúncio da exibição de filtro Administração de sites para os leitores de tela. Quando os usuários alternam entre Cartão/Lista enquanto os itens são carregados, o NVDA agora fala a mensagem &quot;Aguarde&quot; em uma região ativa. Essa orientação evita cliques extras e confusão. (SITES-24992)
* O foco do teclado agora se move em uma ordem lógica quando os usuários expandem o painel esquerdo. O foco muda diretamente do botão do painel esquerdo para o conteúdo expandido, eliminando a necessidade de rastrear retroativamente ou ignorar elementos. Essa alteração melhora a acessibilidade para usuários de leitores de tela e teclado. (SITES-24998)
* O feedback do leitor de tela para o botão **Editar** agora corresponde ao controle. A ativação do botão anuncia a ação Editar em vez de uma mensagem de pré-visualização, o que melhora a clareza e reduz os erros de entrada para usuários que não usam mouse. (SITES-25208)
* A ação de confirmação na caixa de diálogo Teaser anuncia corretamente aos leitores de tela. O controle relata &quot;Confirmar&quot;, não a descrição do ícone, fornecendo orientação clara aos usuários de teclado e leitor de tela. (SITES-25223)
* O botão Ajuda agora expõe um nome acessível claro. Os leitores de tela anunciam &quot;Ajuda&quot; em vez de uma descrição detalhada do ícone. Os usuários entendem a ação e podem encontrar assistência mais rapidamente. (SITES-25224)
* O modal do Timewarp exibe um anel de foco limpo nos links **`Set Date`** e **Sair do Timewarp**. Os usuários que fazem a guia veem exatamente onde o foco vai parar e evitam ações não intencionais. O anel mantém pelo menos 3:1 de contraste com o plano de fundo. (SITES-25232)
* Agora, os leitores de tela anunciam os controles Anotar e Fechar anotação com precisão na barra de ferramentas Anotação. O NVDA não diz mais &quot;Botão de visualização pressionado&quot;, o que induziu os autores em erro e sugeriu a ação errada. O anúncio corresponde ao botão pressionado e mantém o workflow limpo. (SITES-25234)
* A navegação pelo teclado na barra de ferramentas de anotação se comporta de forma consistente. O foco não salta mais para Sair ao abrir o modo e, em vez disso, se move para o controle inicial para adicionar anotações. Os usuários navegam pelos controles em sequência sem tabulação reversa. (SITES-25241)
* A visualização em tela pequena funciona conforme esperado no modal Teaser. A caixa de diálogo não cria mais uma barra de rolagem horizontal a 320 px e a barra de ferramentas permanece acessível sem se deslocar lateralmente. Esta atualização ajuda os usuários com pouca visão que dão zoom na página. (SITES-25242)
* A visualização em tela pequena funciona conforme esperado no modal Imagem. A caixa de diálogo não cria mais uma barra de rolagem horizontal a 320 px e as ferramentas de imagem permanecem acessíveis sem movimentação lateral. Essa atualização melhora a navegação para usuários com pouca visão que ampliam a página. (SITES-25244)
* O modal Pesquisar respeita as configurações de espaçamento de texto do usuário. A elevação da altura da linha, o espaçamento entre parágrafos, o espaçamento entre letras ou o espaçamento entre palavras não corta mais o texto ou sobrepõe a árvore. O conteúdo reflui para valores da WCAG 1.4.12 e permanece totalmente legível. (SITES-25245)
* O modal Pesquisar agora se ajusta a telas pequenas sem sobrepor o diretório da árvore em 320 px. O conteúdo reflui dentro da caixa de diálogo, mantém somente a rolagem vertical e mantém os controles visíveis. Essa correção melhora a legibilidade e a navegação pelo teclado e se alinha à WCAG Reflow. (SITES-25246)
* O estouro modal do carrossel não força mais a rolagem horizontal em larguras no tamanho do telefone. O componente se adapta a 320 px, preserva o fluxo vertical e mantém os controles visíveis. A alteração melhora a legibilidade e o acesso ao teclado durante a criação. (SITES-25254)
* Os fluxos de trabalho de anotação não perdem mais o foco. O modal coloca o foco inicial em um cabeçalho significativo, impede que o foco pule para fora da caixa de diálogo e restaura o foco para o acionador após a demissão. A saída do leitor de tela permanece concisa e relevante. (SITES-25257)
* A caixa de diálogo **Excluir Anotação** agora trata o foco do teclado corretamente. A abertura da caixa de diálogo move o foco para seu cabeçalho para o contexto do leitor de tela, e seu fechamento envia o foco de volta para o botão **Excluir Anotação** que a iniciou. Os usuários não pousam mais em controles não relacionados ou atrás do modal. (SITES-25258)
* O Seletor de datas do Timewarp agora gerencia o foco corretamente. Pressionar `Esc` retorna o foco ao botão **Seletor de Data** e escolher uma data move o foco para o campo de entrada vinculado. Os usuários de teclado e leitor de tela mantêm o contexto e não aterrissam atrás do modal. (SITES-25264)
* Os leitores de tela anunciam as ações corretas para os botões **Anotar** e **Fechar Anotação**. O NVDA não diz mais &quot;Botão de visualização pressionado&quot;; ele anuncia o nome do botão para que os usuários saibam quando o modo de anotação começa ou termina. (SITES-25268)
* O modal Anotação agora mostra uma ação limpar **Enviar**. Os autores podem adicionar um comentário e enviá-lo com o botão de ícone de caneta ou descartar a modal com `Esc`, sem adivinhar o fluxo. (SITES-25269)
* A entrada de anotação inclui botões de ação explícitos. A caixa de diálogo expõe **Enviar** para salvar a anotação e **Cancelar** para fechá-la, acessível pelo teclado e anunciada pela tecnologia assistiva. Os autores não precisam mais depender de clicar fora da caixa de diálogo ou pressionar apenas `Esc` para concluir. (SITES-25281)
* O modo Anotação agora mantém o foco do teclado na sobreposição e sua barra de ferramentas. A página por trás da sobreposição não recebe mais o foco quando os autores pressionam Tab, para que os usuários permaneçam orientados e possam navegar pelas anotações sem pular para o conteúdo subjacente. (SITES-25282)
* O seletor de dispositivos em Editar layout funciona conforme projetado. Quando duas opções de dispositivo têm larguras semelhantes (por exemplo, iPhone 8 Plus ao lado do Galaxy 7), o botão selecionado mostra uma dica de ferramenta para revelar o rótulo completo enquanto ambos os botões permanecem visíveis e acessíveis. (SITES-25285)
* Com 200% de zoom, a opção Editar layout não ultrapassa mais a página. A barra de ferramentas é totalmente renderizada e expõe a rolagem horizontal quando necessário, restaurando o acesso a controles ocultos anteriormente para usuários com pouca visão. (SITES-25288)
* A ordem de tabulação na Visualização de layout agora se move da barra de ferramentas principal diretamente para a barra de ferramentas Demográfica. Usuários de teclado e leitor de tela podem atravessar controles em uma sequência previsível em vez de pular para a barra de ferramentas secundária. A alteração está alinhada à Ordem de foco da WCAG 2.4.3. (SITES-25305)
* Aplicar zoom à página para 200% não oculta mais parte da barra de ferramentas Demográfica. A seção da barra de ferramentas gerencia o estouro e fornece rolagem em sua própria região, mantendo cada controle visível e operável em alta ampliação. (SITES-25309)
* As entradas de texto na barra de ferramentas Demografia agora expõem nomes acessíveis adequados. Cada campo inclui uma ID exclusiva com um rótulo programático, para que os leitores de tela anunciem a finalidade do campo e os usuários possam navegar por rótulo. O rótulo visível fica perto do controle para melhorar a legibilidade de baixa visão. (SITES-25316)
* O botão Editar agora anuncia a ação correta para leitores de tela na barra de ferramentas secundária. Ao ativá-lo, lê-se &quot;Editar&quot; em vez do &quot;Botão Visualizar pressionado&quot;, que remove a confusão durante a navegação pelo teclado. (SITES-25320)
* O controle deslizante do Carrinho da barra de ferramentas Demografia agora expõe um nome acessível adequado. Os leitores de tela anunciam que o &quot;Total do carrinho&quot; e as ferramentas de entrada de fala podem direcionar o controle por nome, melhorando a conformidade com a WCAG 4.1.2 (nome, função, valor). (SITES-25322)
* O controle deslizante da barra de ferramentas Demografia agora mantém o foco quando os autores alteram o valor com as teclas de seta. O foco não salta mais para o botão do carrinho, portanto, os usuários de teclado ajustam o valor continuamente e os leitores de tela anunciam cada alteração. (SITES-25324)
* Pesquisar Assets agora Reflow limpo em 320 px (zoom de aproximadamente 400%). O modal mantém os cabeçalhos, campos e ações legíveis e não sobrepostos, de modo que os autores podem pesquisar sem rolagem horizontal. (SITES-25330)
* O painel Assets no editor segue uma sequência de foco lógica. Usuários do teclado percorrem cada miniatura e podem acessar os controles de saída do painel. A alteração remove falhas e melhora a conformidade com a WCAG 2.4.3. (SITES-25360)
* O AEM atualiza os botões **Listas** e **Parágrafos** no editor de rich text do modal Teaser para expor seu estado expandido e recolhido. Os botões agora alternam `aria-expanded` e anunciam a alteração de estado aos leitores de tela. Os autores recebem feedback claro e evitam adivinhações antes de abrir ou fechar os menus de formato. (SITES-25365)
* O AEM anuncia o estado de carregamento no modal Teaser. O modal agora expõe uma mensagem de status em tempo real enquanto o conteúdo é carregado, de modo que o NVDA e o JAWS falam &quot;Carregando, aguarde.&quot; Os autores devem receber feedback claro e evitar interagir com a caixa de diálogo antes que ela esteja pronta. (SITES-25366)
* Melhora as mensagens de status na guia Ativo da caixa de diálogo Seleção de link. Quando ocorre um erro, o componente injeta uma atualização de status legível e mantém o foco do teclado estável, permitindo que o NVDA/JAWS informe os usuários imediatamente. (SITES-25368)
* O comportamento da interface do usuário no painel Nota foi corrigido para janelas de visualização muito estreitas. Em 320 px, o título e o controle Adicionar colidiram anteriormente; a barra de ferramentas agora reflui e preserva uma separação clara entre os elementos. Os autores podem operar os controles sem perda de informação ou função. (SITES-25376)
* Correção de um estado de erro persistente na guia **Links e ações** da caixa de diálogo **Teaser**. Depois que os autores habilitam o **Call to action** e corrigem campos em branco ou inválidos, a guia apaga o estilo e o ícone do erro e remove o `aria-invalid`. Os leitores de tela não anunciam mais um erro depois que os campos são validados. (SITES-25527)
* O tratamento de erros no Sites Admin Forms agora atende às expectativas de acessibilidade. Quando a validação falha, a página mostra o erro imediatamente, altera o foco para um destino de mensagem utilizável e expõe o texto para leitores de tela, como JAWS. (SITES-27138)
* A criação de uma pasta no Sites agora mostra uma janela de confirmação clara. O JAWS anuncia a mensagem por meio da região ao vivo, para que os autores recebam feedback imediato e acessível após a ação. (SITES-27141)
* Correção de uma lacuna de acessibilidade em que as imagens nas caixas de diálogo de criação eram renderizadas sem texto alternativo. A caixa de diálogo agora fornece texto alternativo descritivo onde necessário e alternativo vazio para elementos puramente visuais, restaurando o comportamento compatível para JAWS e outros leitores de tela. (SITES-27153)
* Tratamento de erros aprimorado nas caixas de diálogo de criação. Quando ocorre um erro de configuração, a interface do usuário mostra texto explícito e aciona um anúncio de leitor de tela por meio de uma região de alerta. Os autores recebem feedback imediato e podem corrigir o problema sem perder o contexto. (SITES-27155)
* Correção de um defeito de acessibilidade de Reflow no Administrador do Sites. Com o zoom de 400% do navegador, os controles de grade e barra de ferramentas se sobrepõem e enviam as ações principais para fora da tela, o que bloqueava a navegação pelo teclado e o uso do leitor de tela. O layout agora flui corretamente para que os botões de pesquisa, filtro e ação permaneçam visíveis e operáveis com zoom de 400%. (SITES-27238)
* Correção de baixo contraste na mensagem de status de bloqueio mostrada no fluxo de trabalho Bloquear/Desbloquear página. A mensagem agora atende a uma proporção de 4,5:1, melhorando a legibilidade e a conformidade com a ADA para os autores. (SITES-27270)
* Nomes acessíveis foram adicionados aos ícones de marca de seleção na caixa de diálogo **Permissões efetivas**. O JAWS agora anuncia os ícones e seu significado, melhorando a navegação pelo teclado e a conformidade com a ADA. (SITES-27272)
* A navegação do cabeçalho oculto aceitou o foco e confundiu os usuários com visão e leitores de tela. A atualização desativa o foco em controles recolhidos e expõe apenas itens visíveis. A navegação permanece previsível e atende à WCAG 2.4.3. (SITES-35224)

* Correção dos ícones de miniatura da pasta no Administrador de sites para que se comportassem como imagens decorativas. A atualização remove a função de imagem e aplica texto alternativo vazio, de modo que a tecnologia assistiva ignora os ícones e lê somente rótulos significativos. (SITES-2852)
* O Adobe aumentou o contraste de cores para o texto Referências na página inicial do Sites. O texto agora atende à WCAG 2.1 AA com uma proporção de pelo menos 4,5:1 e lê claramente sobre temas claros e telas brilhantes. (SITES-24755)
* O marco do painel de Referências agora anuncia seu nome aos leitores de tela. A região expõe um `aria-label` exclusivo (&quot;Painel de referências&quot;), que melhora a navegação de pontos de referência e a distingue de outras regiões. (SITES-24973)
* O RTE de Descrição bloqueou a navegação da guia para frente e interrompeu o fluxo de diálogo. A correção restaura o movimento padrão do teclado. Os autores continuam além do campo com uma única guia e mantêm a ordem de seleção previsível. (SITES-35228)
* Os controles de criação não tinham nomes acessíveis e texto de ícone bruto exposto, o que confundia o JAWS. A correção adiciona rótulos ARIA explícitos e funções padrão. Os anúncios parecem corretos e estão alinhados às expectativas de acessibilidade. (SITES-35227)
* A lista suspensa Categorias não tinha um rótulo específico, então o JAWS falou um &quot;menu de botão de imagens&quot; genérico. A atualização nomeia o controle como &quot;Categorias&quot; e define sua função. Os usuários de leitores de tela ouvem um rótulo preciso e compreendem as opções disponíveis. (SITES-35226)
* A caixa de diálogo Propriedades exibia uma grade de dados que os leitores de tela tratavam como texto simples. O JAWS e o NVDA perderam o foco e não anunciaram linhas e colunas. A correção adiciona a semântica de tabela real e as funções ARIA. Agora, os leitores de tela reconhecem a tabela e rastreiam o foco corretamente. (SITES-35225)
* O editor de texto do Fragmento de conteúdo foi carregado com uma barra de ação truncada. Os ícones foram recortados e o menu de estouro ficou inacessível. A atualização corrige o layout para que a barra de ferramentas completa permaneça visível e acessível. (SITES-33005)
* Os campos de formulário da guia Básico não mostram texto de erro útil. O formulário agora exibe mensagens claras e integradas e as vincula ao campo para leitores de tela. Os usuários de teclado e tecnologia assistiva recebem orientação imediata para corrigir a entrada. (SITES-32480)
* O Multicampo usado em um componente personalizado expôs botões de ícone não rotulados e ordem de tabulação inconsistente. JAWS/NVDA anunciaram apenas controles de &quot;botão&quot; ou ignorados, que bloquearam a operação do teclado. A atualização fornece nomes descritivos para Adicionar, Remover e Mover, normaliza paradas de tabulação e anuncia atualizações de lista para atender às expectativas da ADA. (SITES-30660)
* A Publicação rápida agora retorna uma notificação de sucesso clara. A caixa de diálogo é fechada, uma notificação confirma a ação e os leitores de tela anunciam a mensagem para que os autores não percam o resultado. (SITES-26912)
* Nenhuma alteração necessária. A Adobe analisou a alegação de que o ícone de pesquisa se sobrepõe ao texto nas proximidades. O cabeçalho incluía um rótulo adicionado pelo cliente; o baunilla AEM renderiza apenas o ícone. Uma instância limpa mostra o layout correto com 100% de zoom, portanto, o erro foi fechado como fora de escopo. (SITES-26910)
* Criar temas de página não oculta mais o estado de foco. Os estilos Aquático e Deserto renderizam um realce consistente na guia **Básico** e nas guias adjacentes durante a navegação pelo teclado. Essa alteração restaura o feedback de foco previsível e perceptível para usuários com pouca visão. (SITES-26907)



#### Interface do usuário do administrador{#sites-adminui-6524}

Os usuários de leitores de tela não receberam ajuda de navegação na grade **Blueprint do Sistema de Catálogo**. JAWS só anunciou a posição da célula e depois ficou em silêncio. A versão adiciona orientação e funções acessíveis, permitindo que o JAWS leia o contexto da lista, o item selecionado e os controles de seta/espaço necessários. (SITES-30661)

#### IU Clássica{#sites-classicui-6524}

As caixas de seleção da interface clássica perderam os rótulos e exibiam opções em branco. As caixas de diálogo também exibiam HTML codificado como `<br>`. A atualização restaura os rótulos da caixa de seleção e decodifica a marcação para que as caixas de diálogo sejam lidas corretamente. (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] - Administrador{#sites-admin-6524}

Os parênteses no nome de um Fragmento de conteúdo faziam com que o painel Referências relatasse incorretamente o uso. Os autores viram 0 mesmo quando outros fragmentos fizeram referência a ele. A correção corrige a análise de caminho para &quot;(&quot; e &quot;)&quot; e exibe a contagem e as entradas diferentes de zero adequadas. (SITES-35078)


#### [!DNL Content Fragments] - Editor de fragmentos{#sites-fragments-editor-6524}

* O cancelamento da publicação falhou para fragmentos de conteúdo cujo caminho DAM continha parênteses. O assistente Gerenciar publicação reescreveu &quot;(&quot; e &quot;)&quot; e quebrou o caminho do ativo. A correção preserva os caracteres e resolve o item correto, de modo que a ação de cancelamento da publicação é concluída. (SITES-35077)
* Editar um fragmento de conteúdo e voltar para a lista do Assets ocultava o fragmento ou a pasta inteira. Falha ao atualizar a lista após fechar o editor. A correção agora atualiza a lista de forma confiável e mantém o fragmento editado visível sem um recarregamento permanente. (SITES-35374)

* O Editor de Fragmento de Conteúdo falhou ao abrir o Seletor de ativos Polaris porque os escopos IMS necessários foram removidos. A correção restaura os escopos mínimos e restabelece a conexão de Delivery. A navegação e a seleção de ativos funcionam novamente, sem erros HTTP 500. (SITES-35837)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6524}

Após cada implantação, consultas válidas do GraphQL começaram a retornar `GraphQL_QueryValidationError`. O endpoint manteve um esquema obsoleto até que as equipes liberassem caches ou reiniciassem. A correção atualiza o esquema do GraphQL e o registro de consulta persistente durante a implantação, restaurando respostas normais imediatamente. (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

O ContextHub não injeta mais uma segunda cópia do jQuery nas páginas de publicação. A biblioteca de cliente do mecanismo de segmento elimina a dependência cq.shared que extraía o jQuery 1.12.4, de modo que os sites carregam um jQuery consistente e o código front-end funciona de forma confiável. (SITES-30404)

#### Fragmentos de experiência{#sites-experiencefragments-6524}

* Os Fragmentos de experiência agora localizam o aviso mostrado quando não existe nenhuma configuração do Adobe Target. A mensagem é exibida no local do autor em vez de inglês, portanto, as etapas de exportação e ativação são lidas corretamente para equipes globais. (SITES-11868)
* Publicar uma variação de Fragmento de experiência agora mostra uma mensagem de erro localizada quando nenhum serviço em nuvem é anexado à variação. A mensagem é exibida na interface do usuário no idioma do usuário, em vez de uma string somente em inglês. (SITES-20293)
* A exportação de um Fragmento de experiência para o Target falhou com `Attempt to modify attribute at illegal index: -1`. A instrumentação de vitais da Web entrou em conflito com o exportador e corrompeu a manipulação de atributos. A correção consolida o processamento do atributo e remove esse conflito. As exportações foram bem-sucedidas e o fragmento é renderizado no Target. (SITES-31891)

* As propriedades do Fragmento de experiência agora localizam a guia **Referências**. Rótulos e títulos de coluna, como &quot;Página&quot;, &quot;Caminho da página&quot; e &quot;Título da variação&quot;, são exibidos no idioma do autor. Essa alteração remove strings somente em inglês e mantém a exibição de propriedades consistente para equipes globais. (SITES-11203)
* As **Variações** > **Criar fluxo de trabalho** agora mostram o texto completo da tradução. A caixa de diálogo lida com longas cadeias de caracteres de localidade, ajustando e dimensionando o conteúdo corretamente, eliminando rótulos recortados ou de corte. (SITES-19304)
* As propriedades do Fragmento de experiência agora localizam os rótulos de status da Mídia social. Os autores visualizam valores de status como Postado e Não postado no idioma selecionado em todas as localidades. Essa alteração remove cadeias de caracteres somente em inglês que causaram confusão durante a revisão. (SITES-20014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### Lançamentos{#sites-launches-6524}

* A exclusão de um Launch muito grande congelou o repositório. O trabalho enfileirou muitas remoções e deixou outras solicitações sem efeito. A correção agora faz com que os lotes sejam excluídos e gerem aproveitamentos entre partes, de modo que a limpeza é concluída enquanto o sistema permanece responsivo. (SITES-32004)

* Configuração do Launch > Propriedades mostra os menus suspensos Empresa e Propriedade em funcionamento. **Salvar** e **Fechar** respeitam os campos concluídos, e a validação de Título não dispara mais erros na Empresa ou na Propriedade. (CQ-4359853)
* Verificações necessárias na Configuração IMS são executadas na atualização, não apenas na criação. Valores vazios em campos como ID do cliente ou Segredo do cliente exibem um erro e param o salvamento até que um valor válido seja inserido, impedindo a reutilização do valor anterior. (CQ-4359938)
* A criação do Launch mostra cadeias de caracteres de erro e validação traduzidas. Mensagens somente em inglês para falhas de criação e páginas de origem ausentes não são mais exibidas. Os autores veem comentários claros e corretos quanto ao local durante a configuração do Launch. (SITES-13085)
* Inicie a promoção atualiza as propriedades de página `jcr:title`, `jcr:description` e `cq:redirectTarget` na página de origem. A alteração remove as exclusões de propriedade na configuração de implantação do MSM e na lógica do fluxo de trabalho. Campanhas, traduções e SEO mantêm títulos, descrições e redirecionamentos consistentes. (SITES-34509)
* A ação de inicialização ignorava o escopo e incluía páginas que compartilhavam o mesmo pai como a seção de destino. A atualização impõe limites de subárvore e promove somente a página escolhida e seus descendentes. Páginas não relacionadas mantêm o conteúdo existente. (SITES-34344)
* Correção da promoção automática do Launch aninhado que parava em Autor e ignorava o nível de Publicação. A promoção automática para uma inicialização secundária publica as páginas atualizadas para os editores configurados e conclui a Inicialização completa conforme programado. (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM: Live Copies{#sites-msm-live-copies-6524}

* Uma implantação no nível da pasta não conseguiu criar live copies para os Fragmentos de experiência nessa pasta. Implantações individuais funcionavam, o que causava a quebra de fluxos de trabalho em massa. A alteração alinha a implantação da pasta ao comportamento da página e propaga relações e referências pela subárvore. (SITES-35161)
* Depois de excluir um componente em uma Live Copy, **Habilitar herança** foi interrompido com um erro de JavaScript e o componente permaneceu ausente até uma segunda tentativa. A atualização corrige a recarga pós-excluída para carregar os parâmetros corretos e substitui a chamada de alerta obsoleta. A caixa de diálogo é aberta corretamente e a herança é restaurada na primeira tentativa. (SITES-31387)
* O Assistente de Implantação aceitou **Depois** sem data. Os autores avançaram e criaram uma implantação sem um agendamento. A atualização impõe a seleção de data e exibe um prompt claro. A ação **Continuar** permanece desabilitada até que exista uma data. (SITES-31374)


#### Editor de página{#sites-pageeditor-6524}

* A abertura da árvore de conteúdo em uma página com um Contêiner do Personalization retornou um painel vazio e um erro de referência nula do console. Os autores não puderam escolher ou configurar os componentes. A atualização remove o erro e reativa as interações da árvore e do componente. (SITES-34336)
* A alternância do modo quebrado do AEM 6.5 SP23 no Editor de páginas. Clicar em **Layout**, **Desenvolvedor** ou **Direcionamento** deixou o editor preso no modo **Editar** e acionou um console `TypeError`. A atualização restaura as alterações no modo da barra de ferramentas e limpa o erro. (SITES-34536)
* O Editor de páginas saiu do ponto de inserção quando os autores adicionaram componentes em contêineres longos. A atualização ajusta o tempo de sobreposição e o manuseio de rolagem. A visualização ocupa seu lugar e o novo componente permanece à vista e pronto para ser configurado. (SITES-32621)
* Os rótulos de tag personalizados falharam no Editor de páginas, e a interface sempre exibia &quot;Tags&quot;. O predicado agora avalia `fieldLabel` primeiro e `labelText` segundo e, em seguida, aplica o padrão. Os autores veem o rótulo que definiram. (SITES-32278)
* Cancelar o filtro Localização em Sites desalinhou o ícone OmniSearch e o sobrepôs ao texto de espaço reservado. O ícone se tornou inclicável. A correção realinha o ícone e restaura a área de ocorrência, de modo que o mouse e o teclado acionam a pesquisa. (SITES-30946)
* Escolher Desenvolvedor deixou a página em um estado ruim e bloqueou a criação nessa página. O painel desapareceu e a interface parou de responder. A atualização repara a lógica de alternância de modo e o manuseio de cache, mantendo a página editável e mostrando os dados do desenvolvedor imediatamente. (SITES-30922)
* Clicar em **Limpar** em **Inserir novo componente** não removeu a consulta de pesquisa e deixou a lista filtrada para um único item (Acordeão). A correção redefine a consulta e atualiza a lista. Todos os componentes permitidos aparecem novamente. (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### Editor de rich text{#sites-rte-6524}

* Em tela cheia, o editor de rich text ocultava o resultado da Verificação ortográfica atrás da caixa de diálogo quando não havia erros. A atualização traz o painel de resultados para a frente e mantém as mensagens e sugestões visíveis. Os autores revisam e aceitam correções sem sair da tela cheia. (SITES-32366)
* Agora, as imagens do editor de rich text seguem o alinhamento selecionado. Os autores definem à esquerda, ao centro ou à direita na caixa de diálogo de imagem, e o editor aplica essa escolha de forma consistente na saída. A alteração também estabiliza a caixa de diálogo Texto alternativo, para que o texto alternativo e o alinhamento sejam salvos e persistam em reedições. (SITES-30634)

#### Editor universal {#sites-universal-editor-6524}

A configuração do Manipulador de autenticação de token de consulta confundiu os usuários porque os rótulos não correspondiam aos campos. A interface do usuário retirou o texto do caminho e exibiu os nomes errados. A correção restaura rótulos claros e precisos para as opções de classificação de serviço e token de consulta. (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* A opção **Selecionar miniatura** para vídeos agora se comporta corretamente no AEM Assets - Dynamic Media. O clique abre a caixa de diálogo e permite a seleção de uma miniatura do Assets, eliminando o comportamento anterior de clique-morto e removendo a limitação somente à extração de quadros de vídeo. (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

>[!NOTE]
>
>As correções no Forms [!DNL Experience Manager] são entregues por meio de um pacote complementar separado uma semana após a data programada de lançamento do Service Pack [!DNL Experience Manager]. Nesse caso, os pacotes complementares serão lançados quinta-feira, 4 de dezembro de 2025. Além disso, uma lista de correções e aprimoramentos do Forms foi adicionada a esta seção.

<!--
#### Forms Designer 

#### Forms

#### Forms JEE 

#### Forms Captcha {#forms-captcha-6524} 

#### XMLFM {#forms-xmlfm-6524}

#### [!DNL Forms Designer] {#forms-designer-6524}

-->


### Foundation {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

Atualização do pacote Felix Web Console para incluir FELIX-6747. Esse patch corrige o tratamento de resposta que anteriormente quebrava a renderização e a autenticação da página no OSGi Web Console. O console é carregado de forma consistente e não lança mais entradas IllegalStateException nos logs. (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* Cadeias de caracteres brutas ou somente em inglês não aparecem mais na caixa de diálogo **Remover Controle de Acesso**. A caixa de diálogo apresenta conteúdo totalmente localizado nos idiomas compatíveis, para acessibilidade consistente. (GRANITE-48479)
* O ícone Ajuda agora expõe um rótulo conciso para tecnologias assistivas. O JAWS lê &quot;botão Ajuda&quot; e não adiciona mais palavras irrelevantes do tipo &quot;menu&quot;. Essa atualização traz o controle para a conformidade WCAG 4.1.2 e simplifica o uso do teclado e do leitor de tela. (GRANITE-55360)
* Restaure a fábrica do mecanismo de script HTL após eliminar um loop de dependência em serviços OSGi. Os ambientes são iniciados corretamente, a renderização HTL funciona em pods de autor e os administradores não encontram mais falhas de inicialização ou serviços de script ausentes. (GRANITE-58276)

* A caixa de pesquisa do cabeçalho não sobrepõe mais o ícone de lupa no texto do espaço reservado. O espaço reservado é exibido com o preenchimento adequado e permanece totalmente legível nos navegadores. (GRANITE-54391)
* Os autores veem rótulos legíveis nos campos de Preenchimento automático em vez de valores brutos na caixa de diálogo. A implementação mantém o valor persistente no JCR e melhora a clareza para configurações de seleção única e múltipla que originam opções dinamicamente. (GRANITE-57615)
* O modo de edição permanece funcional quando htmlLibraryManager.debug é definido como verdadeiro. A alteração restaura a resolução e o carregamento adequados da biblioteca do cliente, permitindo que os desenvolvedores usem as ferramentas de depuração do HTML Library Manager durante a criação. (GRANITE-58002)
* A página de edição do Agente de replicação não gera mais um erro JavaScript na interface clássica. A página abre, exibe todas as guias e salva as configurações do agente sem erros de console. (GRANITE-58302)
* Corrigida a agregação do status de integridade na Visão geral do sistema. A visualização agora é atualizada após a execução de verificações individuais e exibe as contagens certas. Os operadores veem &quot;OK&quot; quando as verificações de Segurança e Manutenção forem aprovadas, em vez de um banner incorreto &quot;2 erros&quot;. (GRANITE-61482)
* A execução do `CodeUpgradeTasks` foi interrompida durante as atualizações do AEM 6.5 LTS (Long Term Support). A atualização agora continua sem alterações ou reconfigurações do repositório acionadas por tarefa. Essa correção reduz o risco de atualização e evita tempo de inatividade evitável. (GRANITE-61486)
* Nas caixas de diálogo de criação, os campos obrigatórios agora mostram um erro de validação único e preciso. A mensagem usa o próprio rótulo do campo quando presente e retorna a um prompt genérico quando nenhum rótulo existe. Mensagens duplicadas e incompatíveis entre campos não são mais exibidas. (GRANITE-59531)
* A caixa de diálogo Assistente de criação de página agora revalida os campos obrigatórios em cada interação, incluindo alterações de guia e edições de vários campos. O botão **Criar** permanece desabilitado até que os autores concluam todas as entradas necessárias, e o assistente mostra erros em linha para valores ausentes. (GRANITE-58826)

#### Integrações{#foundation-integrations-6524}

A publicação das atividades do AEM Target não falha mais quando os autores definem datas de início e término. A integração envia carimbos de data e hora compatíveis com os padrões que incluem o fuso horário, de modo que o Target processa a carga da atividade e conclui a sincronização conforme esperado. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### Localização{#foundation-localization-6524}

* A localização em zh-CN remove uma frase ambígua no status de coleta de referência mostrado durante operações de ativos, como Mover. A interface do usuário agora exibe `正在获取对 [[0]] 项的引用`, fornecendo significado preciso e terminologia consistente. (CQ-4354648)
* Criar uma coleção inteligente não traduz mais palavras-chave de pesquisa salva na atualização. Os autores que inserem termos em inglês veem que esses mesmos termos são retidos e a coleção continua a retornar resultados consistentes. (NPR-43158)
* Corrigido o texto truncado da dica de ferramenta no painel Imagem. A descrição &quot;Exibir legenda como pop-up&quot; é renderizada completamente em todos os locais compatíveis, melhorando a orientação para autores que não estão em inglês. (SITES-10490)
* A exibição da Coluna do administrador de sites truncou os rótulos localizados em francês e espanhol. &quot;Hora de término&quot; e &quot;Hora de desligamento&quot; apareciam truncadas e não exibiam nenhuma dica de ferramenta. O Adobe corrigiu as traduções e restaurou a dica de ferramenta ao passar o mouse, portanto, os rótulos foram lidos na íntegra. (SITES-31318)
* A caixa de diálogo **Mover** no Sites mostrava chaves i18n brutas em vez de rótulos legíveis. Itens como &quot;Páginas de referência&quot;, &quot;Criado em&quot;, &quot;Criado por&quot; e &quot;Caminho&quot; pareciam distorcidos. A correção conecta a caixa de diálogo aos dicionários corretos e fornece traduções, com um fallback em inglês. (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Platform{#foundation-platform-6524}

* Os erros de validação agora mostram um texto descritivo claro em vez de apenas um ícone. Os leitores de tela anunciam a mensagem automaticamente quando ela é exibida, de modo que os usuários não precisam navegar até um ícone para saber o que deu errado. (CQ-4359152)


* Os rótulos de focalização na Barra de navegação não permanecem mais na tela depois que o cursor se move para fora do controle. A interface do usuário oculta essas dicas de ferramentas imediatamente quando o mouse é desfocado ou removido, evitando confusão visual e cliques incorretos. (CQ-4360030)
* No Sites, as ações da barra de ferramentas param de criar um segundo pop-up com cliques repetidos. O segundo clique fecha o pop-up existente e deixa apenas uma ocorrência visível, eliminando sobreposições e distrações. (CQ-4360038)
* O texto de direitos autorais desatualizado de 2024 não é mais exibido. A página de Logon e o pop-up **Ajuda** > **Sobre o AEM** são exibidos em 2025, e o AEM lê o ano de forma programática para evitar edições manuais. (CQ-4360042)
* Clicar em uma dica de ferramenta na barra de cabeçalho do AEM não aciona mais a ação subjacente. Os pop-ups são abertos somente quando os usuários clicam no botão real, impedindo caixas de diálogo acidentais ao interagirem com o texto da dica de ferramenta. (CQ-4360105)
* A sobreposição de ano não deixa mais texto de direitos autorais desatualizado. A tela de Logon e a caixa de diálogo **Ajuda** > **Sobre o AEM** derivam o ano do relógio do sistema e renderizam o valor atualizado sempre que a interface do usuário é carregada. (CQ-4360173)
* Agora, os pop-ups da barra de cabeçalho são alternados corretamente. Clicar na mesma ação (por exemplo, **Pesquisar** ou **Filtro**) fecha o pop-up aberto em vez de abrir outra sobreposição. A alteração impede pop-ups empilhados e retorna o foco ao controle de cabeçalho. (NPR-42891)
* A exibição do calendário de Projetos e Caixa de entrada é renderizada corretamente. A alternância de exibições não esvazia mais a página; o calendário é carregado e mostra os itens agendados. (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->


#### Sling{#foundation-sling-6524}

* Correção do comportamento de cache em páginas protegidas por SAML. O AEM adiciona o controle de cache correto e varia os metadados para sessões autenticadas, de modo que os proxies e a Dispatcher ignoram o armazenamento em cache de respostas personalizadas. O conteúdo anônimo ainda armazena em cache normalmente, enquanto as exibições conectadas permanecem específicas do usuário. (NPR-42640)

* A plataforma atualiza o mecanismo principal do Sling de 2.16.2 para 2.16.6. O mecanismo mais recente endurece a validação de entrada e estabiliza o processamento de solicitações sob carga. (NPR-43105)

#### Editor SPA {#foundation-spa-editor-6524}

A ativação das substituições do Sling Main Servlet **Check Content-Type** interrompeu `.model.json` exportações no AEM 6.5 SP21/22. As solicitações retornavam HTML ou erros porque o exportador invertia o tipo de cadeia intermediária. A correção emite JSON com o tipo correto desde o início, portanto, o `.model.json` funciona em ambientes de Autor e Publicação. (SITES-32634)


#### Tradução{#foundation-translation-6524}

* Adição de uma operação de reindexação para o status Projeto de tradução. Os administradores podem reconstruir o índice de apoio quando a visualização de status sair de sincronia, restaurando resultados e eliminando avisos de passagem do Oak. A página carrega mais rapidamente e mostra os estados atuais da tarefa. (NPR-42699)
* Correção de uma regressão em que as importações de XLIFF relatavam sucesso, mas deixavam os arquivos do dicionário JSON inalterados. As importações agora direcionam o caminho i18n correto e persistem as traduções, de modo que as viagens de ida e volta de localização sejam concluídas sem edições manuais. (NPR-42989)


* O XML de regras de tradução agora funciona conforme configurado. A estrutura de tradução respeita as regras de exceção e se aplica aos padrões `include` e `exclude` corretamente durante a criação do trabalho. As solicitações de tradução não enviam mais o conteúdo excluído. (NPR-42761)



#### Interface do usuário{#foundation-ui-6524}

* Correção de uma regressão na interface do usuário que desativava as entradas na caixa de diálogo Licença do Adobe Stock. A caixa de diálogo agora se comporta normalmente, aceita texto em campos obrigatórios e conclui o fluxo de licenciamento de ativos do Stock na exibição Detalhes do ativo. (NPR-42748)

* Correção da visibilidade do grupo no ambiente do autor. O console Grupos não pára mais com cerca de 41 resultados e retorna o conjunto completo de associações para cada usuário. Essa correção restaura o comportamento consistente após correções cumulativas e mantém a proteção de segurança atual. (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## Instalar [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0 requer [!DNL Experience Manager] 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível na [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) da Adobe.
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.24.0 em uma das instâncias do Autor usando o Gerenciador de Pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> A Adobe não recomenda que você remova ou desinstale o pacote [!DNL Experience Manager] 6.5.24.0. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository`, caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].

1. Baixe o Service Sack de [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Repositório de Dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes sai durante a instalação do Service Pack. A Adobe recomenda aguardar a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no navegador do [!DNL Safari], mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.24.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.24.0 não oferece suporte à instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (6.5.24.0)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

O UberJar para [!DNL Experience Manager] 6.5.24.0 está disponível no [repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal foi renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como valor, para a tag `dependency`.



## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md) para obter uma lista detalhada de todos os recursos obsoletos ou removidos do AEM 6.5.

### Editor SPA {#spa-editor}

[O Editor de SPA](/help/sites-developing/spa-overview.md) foi descontinuado para novos projetos a partir da versão 6.5.24 do AEM 6.5. O Editor SPA permanece compatível com projetos existentes, mas não deve ser usado para novos projetos.

Os editores preferidos para gerenciar conteúdo headless no AEM agora são:

* [O Editor Universal](/help/sites-developing/universal-editor/introduction.md) para edição visual.
* [O Editor de Fragmento de Conteúdo](/help/sites-developing/universal-editor/introduction.md) para edição baseada em formulário.

## Problemas conhecidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problema com o pacote de scripts JSP no AEM 6.5.21-6.5.24 e AEM 6.5 LTS GA**
O AEM 6.5.21 a 6.5.24 e o AEM 6.5 LTS GA são fornecidos com o pacote `org.apache.sling.scripting.jsp:2.6.0`, que contém um problema conhecido. O problema normalmente ocorre com cargas altas, quando a instância do AEM trata muitas solicitações simultâneas.

  Quando esse problema ocorre, uma das seguintes exceções pode aparecer nos logs de erros, junto com referências a `org.apache.sling.scripting.jsp:2.6.0`:

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Quando esse erro ocorre, o único método de recuperação é reiniciar a instância do AEM.

  Entre em contato com o suporte ao cliente na Adobe e consulte esta nota de versão para obter uma resolução.

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

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6524}

A visualização dos fragmentos de conteúdo falha devido à proteção do DoS para uma grande árvore de fragmentos. Consulte o artigo [KB sobre as opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6524}

>[!NOTE]
>
>Evite atualizar para o Service Pack 6.5.24.0 por problemas sem um hotfix disponível. Pode levar a erros inesperados. Atualize para o Service Pack 6.5.24.0 somente após os hotfixes necessários serem lançados.

#### Problemas com Hotfixes disponíveis {#aem-forms-issues-with-hotfixes}

Os seguintes problemas têm uma correção disponível para download e instalação. Você pode [baixar e instalar o Hotfix](/help/release-notes/aem-forms-hotfix.md) para resolver estes problemas:

* **FORMS-20203**: quando um usuário atualiza a estrutura do Struts da versão 2.5.x para 6.x, a interface do usuário Políticas no AEM Forms não exibe todas as configurações, como a opção de adicionar uma marca d&#39;água.

* **FORMS-20360**: depois de atualizar para o AEM Forms Service Pack 6.5.24.0, o serviço de conversão ImageToPDF falha com o erro:
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**: ao tentar converter arquivos TIFF do tipo 7/8 para o PDF, o processo de conversão falha com o erro &quot;Falha na conversão ALC-PDG-001-000-Image2Pdf, causada por: com/sun/image/codec/jpeg/JPEGCodec&quot; e &quot;ALC-PDG-016-003-Ocorreu um erro desconhecido/inesperado durante o pós-processamento do PDF.&quot; O sistema tenta novamente usando o decodificador TM ImageIO TIFF, mas não conclui o trabalho.

* **FORMS-14521**: se um usuário tentar visualizar um rascunho de carta com dados XML salvos, ele ficará preso no estado `Loading` para algumas cartas específicas.

* O AEM Forms agora inclui uma atualização da versão do Struts 2.5.33 para 6.x para o componente de formulários. Essa atualização fornece alterações do Struts que não foram incluídas no SP24. O suporte foi adicionado por meio de um [Hotfix](/help/release-notes/aem-forms-hotfix.md) que você pode baixar e instalar para adicionar suporte à versão mais recente do Struts.

#### Outros problemas conhecidos {#aem-forms-other-known-issues}

* Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` na pasta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), execute as seguintes etapas para resolver o problema:

   1. Pare os localizadores, se eles estiverem em execução.
   2. Pare o servidor do AEM.
   3. Vá para o `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Remova todos os arquivos de correção Geode, exceto `geode-*-1.15.1.2.jar`. Confirme se apenas os jars Geode com `version 1.15.1.2` estão presentes.
   5. Abra o prompt de comando no modo de administrador.
   6. Instale o patch Geode usando o arquivo `geode-*-1.15.1.2.jar`.

* Quando os usuários atualizaram do AEM 6.5 Forms Service Pack 18 ou 19 para o Service Pack 20 ou 21, encontraram um erro de compilação JSP. Esse erro os impedia de abrir ou criar formulários adaptáveis. Isso também causava problemas com outras interfaces do AEM. Essas interfaces incluíam o Editor de páginas, a interface do AEM Forms, o editor de fluxo de trabalho e a interface da Visão geral do sistema. (FORMS-15256)

  Se você enfrentar esse problema, execute as seguintes etapas para resolvê-lo:
   1. Navegue até o diretório `/libs/fd/aemforms/install/` no CRXDE.
   2. Exclua o pacote com o nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie o servidor do AEM.

* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, o símbolo de moeda (como cifrão $) é exibido de forma inconsistente para todos os valores do campo. Aparece para valores até 999, mas está ausente para valores de 1000 e superiores. (FORMS-16557)
* Quaisquer modificações no XDP de fragmentos de layout aninhados em uma comunicação interativa não são refletidas no editor IC. (FORMS-16575)
* Na Visualização de impressão da interface do usuário do Agente de comunicações interativas, alguns valores calculados não são exibidos corretamente. (FORMS-16603)
* Quando a carta é exibida na Visualização de impressão, o conteúdo é alterado. Ou seja, alguns espaços desaparecem e determinadas letras são substituídas por `x`. (FORMS-15681)
* **FORMS-15428**: depois de atualizar para o AEM Forms Service Pack 20 (6.5.20.0) com o Complemento do Forms, as configurações que dependem do Adobe Analytics Cloud Service herdado usando a autenticação baseada em credencial param de funcionar. Esse problema impedia que as regras do Analytics fossem executadas corretamente.

* Quando um usuário configura uma instância do WebLogic 14c, o serviço PDFG no AEM Forms Service Pack 21 (6.5.21.0) no JEE executado no JBoss® falha devido a conflitos do carregador de classe envolvendo a biblioteca SLF4J. O erro é exibido da seguinte maneira (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* FORMS-21378: quando a validação do lado do servidor (SSV) está ativada, os envios de formulário podem falhar. Se você encontrar esse problema, entre em contato com o Suporte da Adobe para obter assistência.



## Pacotes da OSGi e pacotes de conteúdo inclusos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de Conteúdo incluídos nesta versão do Service Pack do [!DNL Experience Manager] 6.5:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de Pacotes de Conteúdo incluídos no Experience Manager 6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites estão disponíveis somente para clientes do. Se você for cliente e precisar de acesso, entre em contato com o seu gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Fale com o suporte ao cliente da Adobe](https://experienceleague.adobe.com/pt-br/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65)
>* [Inscreva-se para obter atualizações de produto prioritárias da Adobe](https://www.adobe.com/subscription/priority-product-update.html)
