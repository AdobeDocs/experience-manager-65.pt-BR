---
title: Notas de versão para [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre versões, novidades, instruções de instalação e uma lista de alterações detalhada para o [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 56b13809475a59f188750b86503e316e69171fe1
workflow-type: tm+mt
source-wordcount: '7273'
ht-degree: 2%
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
| Versão | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do pacote de serviços |
| Data | 12 de novembro de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

O Experience Manager 6.5.26.0 inclui novos recursos, importantes melhorias solicitadas por clientes e correções de erros. Ele também inclui melhorias de acessibilidade, localização, desempenho, estabilidade e segurança incorporadas à base 6.5, disponível desde abril de 2019.

Os principais destaques do Service Pack 26 incluem o seguinte:

* Segurança. Duas correções críticas fecham uma vulnerabilidade de injeção de modelo do lado do servidor no Editor de metadados e violações de script entre sites (XSS) nos servlets da interface Coral.
* Conformidade com o C2PA. O Assets agora detecta credenciais do C2PA e assina representações geradas pelo fluxo de trabalho Atualizar ativo. A assinatura é executada localmente em cada instância e a infraestrutura de assinatura dedicada ou de propriedade do cliente não é compatível.
* Acessibilidade. Mais de 25 correções ajudam o Editor de páginas e o console Sites a atender aos requisitos de contraste, teclado e leitor de tela da WCAG.
* Localização. Dezenas de correções traduzem strings e corrigem problemas de layout em sites, Assets, segurança e operações.
* Confiabilidade. Correções abordam a contenção de bloqueio do GraphQL em instâncias de publicação, implantações MSM, ações da barra de ferramentas do Editor de rich text e ativação de página na interface clássica.
* Analytics. A integração do Launch usa a API do Adobe Analytics 2.0 antes do fim da vida útil do Analytics 1.4 em 31 de agosto de 2026.


<!-- UPDATE FOR EACH NEW RELEASE -->

## Correção de problemas, melhorias e aprimoramentos no Service Pack 26 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### Acessibilidade {#sites-accessibility-6526}

* Os autores podem adicionar, mover e remover componentes usando apenas o teclado. A interação de arrastar e soltar exigia um ponteiro, portanto, falhou no critério Teclado da WCAG 2.1.1. O editor agora fornece o pop-up Inserir componente, Recortar e Colar e Excluir como equivalentes operáveis pelo teclado. (SITES-25359)

* Os autores agora podem ver o botão Formatar (&quot;T&quot;) ativo no menu em linha do componente Texto. Depois que os autores aplicaram a formatação em negrito ou itálico, o ícone de botão ficou escuro contra um plano de fundo cinza escuro e perdeu a taxa de contraste mínima de 4.5:1 da WCAG 2.1 AA. O CSS atualizado clareia o ícone, o que restaura o contraste fornecido pelos service packs anteriores. (SITES-51864)

* A guia Assets no Editor de páginas agora exibe uma cadeia de caracteres traduzida no menu suspenso Selecionar componentes depois de escolher Parágrafos na lista suspensa Imagens. Anteriormente, a sequência &quot;OTHER&quot; aparecia em inglês porque não existia isso nos recursos de localização. O dicionário atualizado fornece a tradução em todas as localidades. (SITES-24525)




* O iframe do ContextHub no Editor de páginas agora tem um atributo de título descritivo. Anteriormente, o elemento `contexthub-ui-iframe` não tinha título, portanto, os usuários de leitores de tela não o identificavam quando o foco era movido para ele. O título agora aparece em todas as páginas e visualizações do Editor, incluindo Tela, Painel lateral e Visualização de layout. (SITES-24650)
* O botão Filtros no painel Filtro do console Sites não adiciona rótulos visíveis acima dos campos Pesquisas salvas e Selecionar diretório de pesquisa. Uma auditoria relatou que os rótulos apareciam quando o foco saía do botão, quando uma tecla era pressionada ou quando o botão era clicado. Os testes não reproduziram o comportamento, portanto, nenhuma alteração foi necessária. (SITES-24706)
* Os links na Navegação de aplicativo do console Sites agora se destacam mais claramente. O texto do link atendia à taxa de contraste de 4.5:1, mas a espessura fina da fonte e o tamanho pequeno dificultavam a visualização dos links. Um peso da fonte maior e um tamanho maior facilitam a leitura do texto para usuários com deficiências visuais. (SITES-24723)
* Os leitores de tela não anunciam mais &quot;em branco&quot; antes do conteúdo da dica de ferramenta no modal Preferências do usuário. Anteriormente, o ícone de informações usava `role="tooltip"` com uma referência a `aria-labelledby`, portanto, o NVDA lia um rótulo vazio primeiro. O ícone agora usa `role="button"` e uma `aria-label` de &quot;informações&quot;, e a alteração se aplica aos componentes de formulário do Coral que compartilham o padrão. (SITES-24732)
* O botão Excluir no modal Excluir agora atende ao requisito de contraste de 4.5:1 da WCAG 1.4.3. Anteriormente, o texto branco em um plano de fundo vermelho apresentava uma proporção de 3,9:1 depois que os autores selecionavam um item e clicavam em Excluir na barra de ferramentas de ação. A cor do botão mais escuro torna o rótulo legível para autores com deficiências visuais. (SITES-24772)
* O cabeçalho Referências no painel Referências do console Sites agora usa um elemento de cabeçalho em vez de um `div`. Anteriormente, os leitores de tela não anunciavam o texto como um cabeçalho, portanto, os usuários não conseguiam navegar pelos cabeçalhos. O cabeçalho também aparece na parte superior da visualização inicial de Referências. (SITES-24967)
* O indicador de foco para botões de acordeão no painel Filtro do console Sites agora atende ao requisito de contraste de 3:1 da WCAG 1.4.11. Anteriormente, o indicador azul mostrava uma proporção de 2.3:1 em relação ao plano de fundo, o que dificultava a localização do botão Acordeão Tags para os usuários de teclado. A cor atualizada oferece aos usuários do teclado uma indicação de foco clara. (SITES-24986)
* O indicador de foco para botões de opção no painel de filtro do console Sites agora atende ao requisito de contraste de 3:1 da WCAG 1.4.11. Anteriormente, o indicador de azul claro mostrava uma relação de 1,7:1 em relação ao plano de fundo. Os usuários de teclado agora podem rastrear sua posição na opção Data de modificação. (SITES-24987)
* O botão Selecionar ao lado dos campos Caminho e Tags no painel lateral do Editor de páginas não usa mais um ícone de caixa de seleção. Anteriormente, o ícone sugeria uma alternância, mas a ativação do botão abria uma modal que contém o Diretório da árvore. O botão Selecionar agora comunica sua função corretamente e o mesmo se aplica aos modais Imagem e Teaser. (SITES-25210)
* Os leitores de tela agora ignoram as imagens em miniatura de ativos no painel lateral do Editor de páginas. Anteriormente, cada imagem trazia um texto alternativo que duplicava o nome do ativo visível, de modo que os usuários ouviam o mesmo texto duas vezes. Um atributo `alt` vazio marca a imagem como decorativa e mantém o nome no título do cartão. (SITES-25213)
* Os leitores de tela reconhecem a lista Componentes do painel lateral como uma lista. Uma auditoria relatou os itens como elementos não relacionados, mas o teste confirmou que a marcação usa um elemento de lista e itens de lista. Nenhuma alteração de código foi necessária. (SITES-25214)
* Os ícones de informações dos componentes no painel lateral do Editor de páginas são maiores e mais fáceis de ver. Antes, os ícones usavam um tamanho extrapequeno de cerca de 12 pixels, algo que os usuários com deficiências visuais não viam bem. Os ícones agora usam o tamanho médio.(SITES-25217)
* O indicador de foco no botão Amostra no modal Anotação agora se destaca do botão. Anteriormente, o indicador correspondia à cor da amostra. Isso dificultava que os usuários de teclado vissem qual botão tinha foco. Um deslocamento fornece ao indicador contraste suficiente contra o plano de fundo e o mantém claramente visível. (SITES-25253)
* O campo Data no modal do Timewarp não carrega mais `aria-haspopup="dialog"`. Anteriormente, os leitores de tela anunciavam que o campo abria uma caixa de diálogo, embora não abra. A remoção do atributo fornece aos usuários de leitores de tela informações precisas. (SITES-25263)
* Os rótulos de texto na barra de ferramentas Demografia, como &quot;Recomendado&quot;, agora atendem ao requisito de contraste 4.5:1 da WCAG 1.4.3. Anteriormente, o texto cinza em um plano de fundo cinza escuro apresentava uma proporção de 2,8:1 no modo de Visualização. Texto mais escuro ou mais claro, dependendo do plano de fundo, torna cada rótulo legível. (SITES-25307)
* O indicador de foco nos botões Commerce, Persona e Dispositivo na barra de ferramentas Demografia agora atende ao requisito de contraste de 3:1 da WCAG 1.4.11. Anteriormente, o indicador mostrava uma proporção de 1,9:1 em relação ao plano de fundo da barra de ferramentas. Os usuários de teclado agora podem rastrear sua posição. (SITES-25308)
* O texto que os autores digitam nos campos de texto da barra de ferramentas Demografia agora atende ao requisito de contraste de 4.5:1 da WCAG 1.4.3. Anteriormente, o texto branco em um plano de fundo cinza produzia uma proporção de 2.9:1 em campos, como o campo suspenso de perfil `displayName` no modo de Visualização. As cores atualizadas tornam os valores digitados legíveis para autores com deficiências visuais. (SITES-25318)
* Agora os leitores de tela leem a dica de ferramenta de descrição quando o foco atinge as caixas de seleção nas caixas de diálogo Teaser, Imagem e Carrossel. Anteriormente, o texto não tinha associação programática com a caixa de seleção, portanto, os usuários não conseguiam ouvir a instrução. Um atributo `aria-describedby` agora vincula cada caixa de seleção à sua descrição. (SITES-25364)
* Agora, os leitores de tela anunciam qual botão Formatos de parágrafo está ativo no Editor de Rich Text. Anteriormente, selecionar uma opção na lista não dava à tecnologia de assistência nenhuma indicação da opção atual. O botão ativo agora carrega `aria-current="true"`, e a opção de Destino de hiperlink ativa carrega `aria-selected="true"`. (SITES-25367)
* Os botões Classificar no cabeçalho da tabela da Exibição de lista do console Sites agora atendem ao requisito de contraste de 3:1 da WCAG 1.4.11. Anteriormente, os ícones cinza-claro mostravam uma proporção de 1,5:1 em relação ao plano de fundo do cabeçalho. A cor do ícone mais escuro torna os botões visíveis para autores com deficiências visuais. (SITES-25372)
* A guia Assets no painel lateral do Editor de páginas não é mais recarregada quando o foco é movido para o campo Filtro. Anteriormente, tabular no campo vazio acionava um recarregamento e os leitores de tela anunciavam uma mensagem de carregamento toda vez. A guia agora é recarregada somente depois de alterar o valor do filtro e pressionar Enter. (SITES-25377)
* O ícone de amostra selecionado no modal Anotação agora atende ao requisito de contraste de 3:1 da WCAG 1.4.11. Anteriormente, a marca de seleção branca mostrava uma proporção tão baixa quanto 1,58:1 em relação às amostras amarela, laranja e verde. O ícone atualizado fornece aos autores com deficiências visuais um indicador claro. (SITES-25523)
* A lista Componentes no painel lateral Editor de páginas não focaliza mais o teclado. Os usuários do teclado selecionam e movem componentes com os controles na janela de conteúdo, de modo que a lista do painel lateral repete a função. Uma nota no filtro de componentes informa aos usuários de teclado onde localizar os controles. (SITES-40752)


#### Interface do usuário do administrador{#sites-adminui-6526}


#### IU Clássica{#sites-classicui-6526}

* Os autores podem ativar as páginas novamente no console Sites da Interface Clássica (`siteadmin.html`). Anteriormente, o botão Ativar página exibia um ponteiro de &quot;Carregamento&quot; indefinidamente e nunca acionava a replicação, pois um script de rastreamento com falha travava o manipulador de cliques. O manipulador de cliques agora é executado sem erros e conclui a ativação. (SITES-52165)
* O código do idioma indonésio agora é exibido como ID nas propriedades da Cópia de idioma. Anteriormente, o painel Referências mostrava o código herdado EM para páginas na raiz de idioma indonésio. A atualização do pacote cq-wcm-core corrige o valor, de modo que o código corresponde ao padrão ISO. (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] - Editor de fragmento{#sites-fragments-editor-6526}

* O botão Editar fragmento de conteúdo é exibido imediatamente para cada referência de vários campos no editor de Fragmento de conteúdo. Anteriormente, o botão ficava oculto até que os autores salvassem o fragmento principal e nada fazia depois de abrirem o Navegador de caminho. O editor agora cria a lista de ações na primeira renderização, de modo que os autores abrem fragmentos referenciados sem etapas adicionais. (SITES-43733)

* Caracteres chineses, japoneses e coreanos não são mais exibidos em itálico no espaço reservado da caixa de diálogo Criar fragmento de conteúdo. Anteriormente, o estilo em itálico era aplicado aos caracteres CJK em **Assets** > **Arquivos**, o que dificultava a leitura do texto. Os estilos atualizados ignoram itálico para idiomas CJK. (SITES-43548)
* O editor de Fragmento de conteúdo valida os campos corretamente após a atualização da interface do usuário do Granite. Uma alteração recente na interface do usuário do Granite causou uma regressão, portanto, as bibliotecas de clientes do editor não correspondem mais ao novo comportamento de validação. As bibliotecas e os testes adaptados resolvem a incompatibilidade. (SITES-46650)


#### [!DNL Content Fragments] — API GraphQL {#sites-graphql-api-6526}

* As consultas do GraphQL em fragmentos de conteúdo agora reconhecem referências RemoteRef ao Dynamic Media com OpenAPI Assets. Anteriormente, as consultas falhavam com um &quot;Erro de validação de consulta persistente&quot; e não retornavam dados de ativos quando o AEM 6.5 Sites consumia o AEM as a Cloud Service Assets. As respostas agora incluem a ID do repositório e a ID do ativo, para que os clientes possam criar URLs de entrega. (SITES-48507)

* As instâncias de publicação permanecem responsivas durante o tráfego intenso de GraphQL. A contenção de bloqueio em `GraphQLServiceImpl` atrasou as threads de processamento de solicitações nos métodos de esquema, o que atrasou as solicitações e exigiu reinicializações. A sincronização aprimorada resolve a restrição do desempenho e mantém a disponibilidade de sites e aplicativos móveis. (SITES-48699)

* A mensagem na página Pontos de extremidade do GraphQL permanece localizada após o recarregamento da página. Anteriormente, a mensagem &quot;Nenhum endpoint foi encontrado&quot; aparecia em seu idioma ao criar e excluir endpoints, mas era revertida para inglês após um recarregamento. A página agora carrega a cadeia de caracteres traduzida em cada visita. (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] - Modelos e Editor de modelos{#sites-models-model-editor-6526}

* As miniaturas dos modelos de fragmento de conteúdo são exibidas em **Ferramentas** > **Geral** > **Modelos de fragmentos de conteúdo** quando o nome da configuração contém caracteres localizados, como &quot;español テスト&quot;. Anteriormente, a miniatura carregada não era exibida porque os caracteres causavam um erro no caminho. O tratamento atualizado codifica o nome corretamente. (SITES-39242)

* A sequência de caracteres Rótulo de campo na tela Editor de modelos de fragmento de conteúdo agora é exibida no idioma do usuário. Anteriormente, o rótulo ficava em inglês depois que os autores arrastavam um componente para a tela e ele era traduzido somente depois que salvavam e reabriam o modelo. O rótulo agora é traduzido imediatamente, correspondendo ao painel Propriedades. (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### Infraestrutura principal{#sites-core-backend-6526}

* A ativação de página programada por meio do Momento de ligar/desligar agora é executada somente quando necessário. `OnOffTriggerProcessor` acionou anteriormente a replicação e a invalidação de cache com muita frequência, o que forçou os autores a republicar o conteúdo manualmente. A correção com suporte elimina o processamento desnecessário e restaura a publicação agendada confiável. (SITES-48483)

* O upload de arquivos funciona para ativos remotos do Gerenciamento de ativos de última geração em vários campos. Anteriormente, o upload falhava quando os autores escolhiam um ativo remoto para um campo dentro de vários campos. A atualização dos Componentes principais restaura o fluxo de upload, de modo que o campo aceite o ativo. (SITES-44266)


#### Componentes principais{#sites-core-components-6526}

* O Seletor de ativos remotos mantém a imagem de cada item de vários campos separada. Anteriormente, selecionar uma imagem em um item de vários campos a aplicava a todos os outros itens e a referência de ativo remoto não era salva. Cada item agora mantém sua própria seleção, e a referência persiste depois que você salva a caixa de diálogo. (SITES-42376)

* Esta versão inclui correções com suporte para o Commerce, Componentes principais, Componentes de base (herdados), Inicializações e Live Copies do MSM. As correções abordam vulnerabilidades de segurança, violações de script entre sites (XSS), comportamento de upload de arquivos e comportamento da Live Copy. Os backports trazem o AEM 6.5 e o AEM 6.5 LTS em conformidade com as correções enviadas anteriormente no AEM as a Cloud Service. (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Headless - Administrador {#sites-headless-admin-6526}

Aprimoramento: a visualização de Visualização no Administrador headless agora passa o caminho de variação selecionado para o componente de visualização. Essa alteração garante que as visualizações de fragmentos de conteúdo com várias variações carreguem o conteúdo da variação correta. A matriz `draftFragmentIds` inclui o parâmetro de variação. (SITES-42714)


#### Lançamentos{#sites-launches-6526}

* As entradas de linha do tempo para inicializações promovidas agora são exibidas no idioma do usuário. Anteriormente, as sequências &quot;Versão criada de&quot; e &quot;antes de promover o lançamento&quot; permaneciam em inglês depois que os autores promoviam um lançamento e abriam a Linha do tempo do site no Sites. Os recursos atualizados fornecem as traduções em todas as localidades. (SITES-13389)
* O espaço reservado Selecionar caminho do Launch Source no painel Filtro de inicializações é exibido por completo. Anteriormente, o texto era cortado em interfaces localizadas, como francês, italiano e português, porque não se encaixava no campo. O layout atualizado mostra o espaço reservado completo. (SITES-42792)
* A coluna Data de ativação em Ferramentas > Sites > Inicializações não mostra mais AM ou PM nos locais alemão, francês, espanhol, italiano, português do Brasil e chinês tradicional. Anteriormente, a coluna usava um formato de 12 horas que não correspondia a essas localidades. A coluna agora exibe o formato de 24 horas. (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### Localização{#sites-localization-6526}

* As cadeias de caracteres nas páginas de Relatórios de Integridade em **Ferramentas** > **Operações** agora são exibidas no idioma do usuário. Anteriormente, as mensagens para Caminho de pesquisa de recursos, Manutenção, Fila de replicação, Erros de log, Pacotes ativos e Desempenho da solicitação permaneciam em inglês. Os recursos atualizados do i18n fornecem as traduções e um arquivo de fallback mantém as cadeias de caracteres disponíveis. (NPR-44279)

* A mensagem de erro &quot;Configurações do &#39;Caminho JSON&#39; são ignoradas quando a opção &#39;Adicionar manualmente&#39; está marcada&quot; agora é exibida no idioma do usuário no console **Ferramentas** > **Assets** > **Esquemas de metadados**. Anteriormente, a mensagem permanecia em inglês depois que os autores adicionavam um elemento suspenso, selecionavam Adicionar por meio do caminho JSON e alternavam para Adicionar manualmente. Os recursos atualizados fornecem as traduções. (ASSETS-31575)
* A cadeia de caracteres &quot;promovida&quot; nas marcas **Assets** > **Gerenciar** agora é exibida no idioma do usuário. Anteriormente, a cadeia de caracteres permanecia em inglês ao passar o mouse sobre uma tag inteligente depois de selecionar Promover. Os recursos atualizados fornecem a tradução em todas as localidades. (ASSETS-36070)
* O rótulo do botão Adicionar não sobrepõe mais o botão em **Propriedades da pasta** > **Contribuição de ativos**. Anteriormente, o texto colidia com o botão nas interfaces em alemão, italiano e português do Brasil depois de criar uma pasta com a configuração &quot;Contribuição de ativos&quot;. Os estilos atualizados fornecem espaço suficiente para os rótulos traduzidos mais longos. (ASSETS-36746)
* Os títulos das colunas na Exibição em lista do Assets agora são exibidos horizontalmente na interface japonesa. Anteriormente, os títulos apareciam verticalmente na Exibição de lista em **Assets** > **Arquivos** e na exibição de cartão do editor de fragmento de conteúdo. O pacote `cq-dam-content` atualizado corrige a direção do texto.(ASSETS-43105)
* O status da publicação &quot;Programado para mais tarde&quot; na exibição de coluna do Assets agora é exibido no idioma do usuário. Anteriormente, a sequência de caracteres permanecia em inglês depois que os autores selecionavam um ativo, escolheram **Gerenciar publicação**, selecionaram a opção **Mais tarde**, adicionaram uma data e publicaram. O pacote `cq-dam-content` atualizado fornece as traduções em todas as localidades. (ASSETS-43307)
* As cadeias de caracteres na guia **Configuração de Tags Inteligentes** agora são exibidas na íntegra para francês e português brasileiro. Anteriormente, o texto era cortado depois que você clicava em **Criar** em **Ferramentas** > **Serviços da nuvem** > **Marca inteligente**. Para ler o texto sem uma dica de ferramenta, use a atualização de CSS que fornece espaço suficiente. (ASSETS-68045)
* A string &quot;Predicado da propriedade de valor do multicaminho&quot; no painel de pesquisa do administrador do Assets agora é exibida no idioma do usuário. Anteriormente, a sequência de caracteres permaneceu em inglês quando os administradores editaram o formulário de pesquisa em **Ferramentas** > **Geral** > **Pesquisa** formulários e arrastaram o predicado para o formulário. O pacote `cq-dam-content` atualizado fornece as traduções.(CQ-4336103)
* Os rótulos de anúncios na visualização Projetos agora são exibidos no idioma do usuário. Anteriormente, o botão Ações em cada bloco de projeto não tinha um nome acessível, e a ação Configurar bloco usava um rótulo inglês embutido em código enquanto os rótulos irmãos eram localizados. O script de bloco atualizado fornece um rótulo localizado para ambas as ações. (CQ-4352359)
* As coleções inteligentes com caracteres chineses, japoneses ou coreanos no nome agora são salvas corretamente. Anteriormente, o salvamento de uma coleção de **Assets** > **Arquivos** > **Filtro** falhou com &quot;Falha ao salvar pesquisa - Solicitação inválida, não é permitido duplicar a coleção&quot; quando o nome continha caracteres CJK. A verificação duplicada agora compara os títulos da coleção em vez dos nomes dos nós, de modo que as coleções com títulos CJK diferentes não entrem em conflito. (GRANITE-62592)
* A lista suspensa de País/Região em **Segurança** > **Usuários** > **Criar** agora classifica os nomes em ordem alfabética no idioma do usuário. Anteriormente, a lista classificava nomes em ordem inglesa enquanto exibia nomes localizados, então os países apareciam fora de ordem em locais como japonês. O pacote `com.adobe.granite.security.content` atualizado foi classificado com regras de reconhecimento de local. (GRANITE-67789)
* O aviso de isenção de responsabilidade na Tarefa de manutenção do AuditLog em **Ferramentas** > **Operações** > **Manutenção** agora é exibido no idioma do usuário. Anteriormente, o aviso sobre a limpeza de logs de auditoria e os requisitos de conformidade permanecia em inglês depois que os usuários clicavam no ícone de aviso na janela Manutenção semanal. Os recursos atualizados fornecem a tradução em todas as localidades. (NPR-44189)
* Os nomes de permissão em **Segurança** > **Permissões** > **Exibição de Auditoria** agora são exibidos no idioma do usuário. Anteriormente, os nomes apareciam em inglês porque as traduções estavam ausentes. O pacote `com.adobe.granite.platform.i18n` atualizado os fornece. (NPR-44477)
* A caixa de diálogo Verificar integridade em **Segurança** > **Configurações do Adobe IMS** agora é exibida no idioma do usuário. Anteriormente, a caixa de diálogo mostrava strings em inglês em interfaces localizadas porque as traduções estavam ausentes. O pacote `com.adobe.granite.platform.i18n` atualizado os fornece. (NPR-44479)
* As cadeias de caracteres na ferramenta Diagnóstico de Sincronização de Usuário em **Ferramentas** > **Operações** > **Diagnóstico** agora são exibidas no idioma do usuário. Anteriormente, a ferramenta mostrava texto em inglês em interfaces localizadas. O pacote `com.adobe.granite.platform.i18n` atualizado fornece as traduções. (NPR-44481)
* Os fluxos de configuração agora mostram mensagens de erro amigáveis no idioma do usuário. Anteriormente, falhas nas páginas de configuração do AEM produziam texto técnico ou não traduzido. O pacote `com.adobe.granite.ui.content` atualizado trata dos erros e fornece mensagens localizadas. (NPR-44840)
* A mensagem de erro que aparece ao alterar propriedades de um grupo excluído em **Segurança** > **Grupos** agora é exibida no idioma do usuário. Anteriormente, a mensagem permanecia em inglês para interfaces localizadas. O pacote `com.adobe.granite.security.content` atualizado fornece as traduções. (NPR-44841)
* A mensagem de erro &quot;Algo deu errado ao salvar as alterações no grupo!&quot; agora é exibido no idioma do usuário no console **Segurança** > **Grupos** > **Editar grupo**. Anteriormente, a mensagem ficava em inglês para interfaces localizadas. O pacote `com.adobe.granite.security.content` atualizado fornece as traduções. (NPR-44842)
* Caracteres chineses, japoneses e coreanos não são mais exibidos em itálico na mensagem de erro do ícone da Caixa de entrada. Anteriormente, o estilo em itálico distorcia os caracteres e tornava o texto mais difícil de ler. O pacote `com.adobe.granite.ui.coralui3` atualizado remove o estilo desses idiomas. (NPR-44843)
* Os números em **Operações** > **Monitoramento** agora seguem o formato de localidade do usuário. Anteriormente, a página mostrava números em um formato fixo, independentemente do idioma da interface. O pacote `com.adobe.granite.monitoring.dashboard` atualizado aplica os separadores e o formato corretos. (NPR-44844)
* A guia Explicar consulta agora mostra a &quot;ferramenta Query Builder Debugger&quot;. no idioma do usuário. Anteriormente, o texto do link estava ausente em interfaces localizadas porque a cadeia de caracteres não era externalizada. O pacote `com.adobe.granite.monitoring.dashboard` atualizado o restaura. (NPR-44845)
* O texto na caixa de diálogo Ferramenta de depuração do Query Builder agora é exibido no idioma do usuário na guia Explicar consulta. Anteriormente, várias cordas ficavam em inglês porque não eram externalizadas. O pacote `cq-platform-content` atualizado fornece as traduções. (NPR-44846)
* O texto da página Resultado da verificação de consistência agora é exibido no idioma do usuário. Anteriormente, várias cadeias de caracteres apareciam em inglês porque não eram externalizadas. O pacote `com.adobe.granite.operations.ui.core` atualizado fornece as traduções. (NPR-44847)
* O Gráfico de monitoramento agora exibe rótulos de mês e semana no idioma do usuário. Anteriormente, os rótulos eram codificados em inglês, portanto, o gráfico ignorava o local da interface. O pacote `com.adobe.granite.monitoring.dashboard` atualizado externaliza as cadeias de caracteres, e as traduções agora aparecem. (NPR-44848)
* A lista suspensa de País/Região em **Segurança** > **Usuários** > **Criar** agora classifica as entradas corretamente. Anteriormente, os nomes de países localizados apareciam na ordem errada para alguns idiomas. O pacote `com.adobe.granite.security.content` atualizado aplica a classificação com reconhecimento de localidade. (NPR-44942)
* As dicas de ferramentas na caixa de diálogo do componente Botão agora são exibidas no idioma do usuário. Anteriormente, o texto informativo para os campos de texto do botão, link, ícone, HTML ID e `aria-label` permanecia em inglês, mesmo que as cadeias de caracteres existissem no serviço de localização. O dicionário atualizado fornece as traduções em todas as localidades com suporte. (SITES-7579)
* As dicas de ferramenta na seção Propriedades do componente Lista de fragmentos de conteúdo agora são exibidas no idioma do usuário. Anteriormente, o texto de informações dos campos Modelo de fragmento de conteúdo, Tags, Número máximo de itens, Caminho principal, Ordem de classificação e Ordenar por permaneciam em inglês. O dicionário atualizado fornece traduções para todas as localidades com suporte. (SITES-14969)
* Os links de Ajuda dos Componentes principais no Editor de modelo agora abrem páginas de documentação localizadas. Anteriormente, selecionar Ajuda na caixa de diálogo de configuração do componente abria a página em inglês, independentemente do idioma da interface. Os URLs atualizados agora direcionam os usuários para a página de sua localidade. (SITES-15058)
* As dicas de ferramentas de informações na caixa de diálogo Fragmento do conteúdo agora são exibidas no idioma do usuário. Anteriormente, o texto da dica de ferramenta para os modos Elemento de texto único e Vários elementos e para o caminho do Fragmento de conteúdo permanecia em inglês. Um dicionário atualizado fornece traduções para todas as localidades. (SITES-17333)
* Mensagens de erro no editor de política de componentes do Editor de modelos agora aparecem no idioma do usuário. Anteriormente, as mensagens &quot;O recurso {} não era modificável&quot; e &quot;Não é possível criar nó em&quot; permaneciam em inglês quando os autores editavam uma política de componente ou criavam uma nova. Os recursos atualizados fornecem traduções para todas as localidades compatíveis. (SITES-17475)
* A guia Assets no Editor de páginas agora exibe uma cadeia de caracteres traduzida no menu suspenso Selecionar componentes depois de escolher Parágrafos na lista suspensa Imagens. Anteriormente, a sequência &quot;OTHER&quot; aparecia em inglês porque não existia isso nos recursos de localização. O dicionário atualizado fornece a tradução em todas as localidades. (SITES-21481)
* As dicas de ferramentas Informações na caixa de diálogo Configurar componente do Editor de páginas não mostram mais uma quebra de linha extra. Anteriormente, as dicas de ferramentas para componentes, como o Visualizador do PDF e a Barra de progresso, estavam dispersas em várias localidades. Agora as dicas de ferramentas são quebradas corretamente e a hifenização de palavras funciona conforme esperado. (SITES-38567)
* A dica de ferramenta &quot;para sair do editor de texto, pressione a tecla Esc&quot; agora aparece no idioma do usuário na caixa de diálogo de configuração do componente de Texto. Anteriormente, a cadeia de caracteres era exibida em inglês porque não era exibida nos recursos de localização. A dica de ferramenta agora é traduzida em todas as localidades. (SITES-43186)
* O rótulo ESTRUTURA no Editor de modelo agora aparece no idioma do usuário. Anteriormente, o rótulo permanecia em inglês quando os autores abriam um modelo de formulário adaptável, pois a sequência de caracteres estava ausente nos recursos de localização. O rótulo agora é traduzido em todas as localidades. (SITES-43599)


#### MSM: Live Copies{#sites-msm-live-copies-6526}

* A caixa de diálogo Implantação do MSM carrega a lista de live copy novamente após uma atualização. Anteriormente, um `NullPointerException` em `AsyncOperationServlet.doGet` interrompeu a caixa de diálogo em um ponteiro, portanto, os autores falharam ao selecionar localidades de destino ou iniciar a implantação. Um pacote `com.adobe.granite.jobs.async` atualizado lida com os dados de trabalho ausentes e conclui a solicitação. (SITES-43116)
* A implantação na barra de ferramentas editável em uma página de blueprint funciona novamente. A ação da barra de ferramentas falhou com &quot;Não é possível ler propriedades de indefinido (lendo &#39;doRollout&#39;)&quot; porque a biblioteca cliente `MSM.Rollout` não foi carregada. A página atualizada agora carrega a biblioteca, de modo que o trabalho de implantação começa e as alterações chegam às live copies. (SITES-46052)

* A desativação em lote de uma página do blueprint e suas páginas secundárias não envia mais eventos de implantação duplicados. Quando você desativava um pai e seus filhos em uma solicitação, o sistema de replicação emitia cinco eventos em vez de três e cada página filho era implantada duas vezes. A desduplicação no gerenciador de implantação agora envia uma implantação por página, de modo que as live copies não recebem pacotes redundantes. (SITES-44988)


#### Editor de página{#sites-pageeditor-6526}

* O estilo selecionado permanece realçado na caixa de diálogo de seleção de estilo do Editor de páginas depois de rolar a lista. Anteriormente, um estilo era destacado ao escolhê-lo, mas o destaque desaparecia ao clicar na barra de rolagem. Essa regressão começou após o SP22 e a caixa de diálogo agora mantém visível o estado selecionado. (SITES-30874)

* Os autores podem editar páginas no modo Layout quando os componentes principais e secundários definem diferentes pontos de interrupção responsivos. A função getResponsiveCssClasses falhou anteriormente com um TypeError em componentes que omitiam a largura de telefone/cq:responsive. A função agora retorna aos valores disponíveis e continua a renderização. (SITES-46681)
* As taxas de corte personalizadas agora são carregadas no modo de edição em linha híbrido para componentes com vários destinos de queda de imagem. Anteriormente, o Editor de imagens inicializava um ipeConfig genérico para todos os destinos de soltar, de modo que o editor mostrava somente as taxas padrão e ignorava as taxas de aspecto de cada destino. O editor agora lê a configuração do destino de soltar selecionado, e o recorte se aplica nas exibições em linha e em tela cheia. (SITES-45771)
* Pressionar Backspace no Editor de Rich Text não adiciona estilos incorporados extras ao texto. Um cliente relatou que a remoção de uma quebra de linha após o texto em negrito adicionou style=&quot;font-size: 0.8125rem; background-color: transparent;&quot; à tag em negrito. O teste no pacote de serviços mais recente falhou ao reproduzir o comportamento, portanto, nenhuma alteração foi necessária. (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### Editor de rich text{#sites-rte-6526}

* Os botões da barra de ferramentas do Editor de Rich Text funcionam no modo de Visualização responsiva e Layout. Anteriormente, os botões eram realçados quando clicados, mas a seleção permanecia inalterada e nenhuma caixa de diálogo era aberta. O script do editor atualizado aplica a formatação, correspondendo ao comportamento no modo Editar. (SITES-44233)
* Os autores podem adicionar símbolos de moeda e marca comercial aos componentes de Texto sem perdê-los. O plug-in Caracteres especiais inseriu os símbolos, mas eles eram exibidos em branco no editor e na saída publicada. O manuseio corrigido renderiza cada símbolo conforme inserido. (SITES-46532)
* O ícone Tela cheia na barra de ferramentas do Editor de rich text expande o editor novamente. Anteriormente, clicar no ícone no componente Texto principal não fazia nada e o editor ficava em seu tamanho incorporado. Os autores agora têm um espaço de trabalho focado para conteúdo de formulário longo na edição em linha e em caixa de diálogo. (SITES-46396)


#### Interface do administrador do site{#sites-admin-ui-6526}

Reverter um ativo para uma versão anterior atualiza a miniatura do cartão. Uma alteração na codificação de URL na biblioteca do cliente Linha do tempo causou uma incompatibilidade de caminho, portanto, a pesquisa de cartão falhou e a miniatura permaneceu obsoleta. Corresponder aos caminhos codificados e brutos restaura a atualização. (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### Extensões de fluxo de trabalho {#sites-workflow-extensions-6526}

Exibir carga agora abre o editor de pacote da interface para toque para fluxos de trabalho que Gerenciar publicação inicia para várias páginas. Anteriormente, a ação abria o editor de pacotes da interface clássica obsoleta, mesmo que os autores iniciassem o fluxo de trabalho na interface para toque. Agora os autores inspecionam o conteúdo sem sair da interface para toque. (SITES-40928)


### [!DNL Assets] {#assets-6526}

* Aprimoramento: o AEM Assets 6.5 inclui suporte à conformidade da Coalition for Content Provenance and Authenticity (C2PA) para conteúdo de IA gerativa. O fluxo de trabalho Atualizar ativo detecta credenciais C2PA, extrai os metadados e assina as representações que o fluxo de trabalho regenera. A assinatura é executada localmente em cada instância do AEM, de modo que os clientes não precisam de infraestrutura de assinatura dedicada. (ASSETS-75868)

* Aprimoramento da documentação: a nova documentação pública explica como personalizar o pipeline de processamento de ativos, mantendo a conformidade C2PA. A documentação aborda como posicionar a etapa Detectar credencial C2PA antes das etapas de representação e como a assinatura é executada localmente em cada instância do AEM. A documentação também declara a limitação da infraestrutura de assinatura dedicada ou de propriedade do cliente. (ASSETS-76100)
* O menu suspenso Ajuda no cabeçalho do shell agora permanece aberto quando você passa o mouse sobre os links nos ambientes do AEM 6.5 SP26. Anteriormente, a lista suspensa era fechada quando o ponteiro do mouse entrava na lista, portanto os autores não clicavam nos links Documentação, Comunidade ou suporte. O pacote `com.adobe.granite.ui.content` atualizado adia a verificação de foco, de modo que o menu fecha somente quando o foco realmente sai. (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* Novo recurso: suporte para tags de acessibilidade em listas em Rich Text. Anteriormente, as tags de lista apareciam na árvore de tags de acessibilidade somente quando o modelo seguia uma estrutura específica. A solicitação foi fechada como uma duplicata de um tíquete relacionado que fornece o recurso. (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### Foundation {#foundation-6526}

* A cadeia de caracteres &quot;País/Região&quot; na caixa de diálogo **Segurança** > **Usuários** > **Criar** do usuário agora aparece no idioma do usuário. Anteriormente, o rótulo permanecia em inglês para interfaces localizadas. O pacote `com.adobe.granite.security.content` atualizado fornece as traduções. (NPR-43882)
* O menu suspenso Ajuda no cabeçalho do shell agora permanece aberto quando você passa o mouse sobre os links nos ambientes do AEM 6.5 SP26. Anteriormente, a lista suspensa era fechada quando o ponteiro do mouse entrava na lista, portanto os autores não clicavam nos links Documentação, Comunidade ou suporte. O pacote `com.adobe.granite.ui.content` atualizado adia a verificação de foco, de modo que o menu fecha somente quando o foco realmente sai. (NPR-44686)
* Melhoria: A consulta `HtmlLibraryManagerImpl` agora inclui uma marca de tipo de nó para que a consulta sempre use o índice esperado. O serviço também registra um ERRO quando não encontra bibliotecas de clientes, o que alerta os administradores sobre o problema. A atualização acumula a versão do pacote `com.adobe.granite.clientlibs` no service pack. (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### Autenticação {#foundation-authentication-6526}

Salvar e fechar no editor de usuários agora retorna aos resultados da pesquisa atual. Anteriormente, depois que os autores pesquisavam um segundo usuário no Omnisearch, editavam as propriedades e clicavam em Salvar e fechar, a página abria as propriedades do primeiro usuário. O script UserProperties.js atualizado restaura a navegação esperada. (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* O espaço reservado &quot;Modelo de fragmento de conteúdo&quot; no filtro Omnisearch do Assets agora é exibido na íntegra. Anteriormente, o texto era cortado depois que você ia para o Assets, clicava no ícone Filtros ou Pesquisar e expandia o campo Modelo de fragmento de conteúdo. O estilo atualizado oferece espaço suficiente ao espaço reservado. (GRANITE-54387)
* A lista suspensa Ajuda no cabeçalho do shell agora permanece aberta quando você move o ponteiro sobre seus links. Anteriormente, a lista suspensa era fechada assim que o ponteiro entrava na lista de links de Documentação, Comunidade e suporte, o que tornava os links inacessíveis com o mouse. O manipulador de foco agora adia sua verificação para o próximo quadro de animação, de modo que passar o mouse não conta mais como o foco saindo do menu. (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Integrações do Launch{#foundation-launch-integrations-6526}

Melhoria: a integração do Adobe Analytics com o Adobe Experience Manager Launch usa a API do Analytics 2.0. A API do Analytics 1.4 chegará ao fim da vida útil em 31 de agosto de 2026. A migração mantém os relatórios e as integrações do Launch funcionando após essa data. (CQ-4365074, CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Platform{#foundation-platform-6526}

* O link Ajuda no rodapé da página de logon do AEM agora abre uma página de trabalho. Anteriormente, o link apontava para um URL marketing.adobe.com que não existe mais. A configuração do rodapé agora usa a URL da [documentação do Adobe Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager). (NPR-44388)
* Aprimoramento: uma solicitação do cliente solicitou a API Graph do Microsoft como alternativa ao SMTP quando o AEM envia email. O tíquete foi resolvido como uma duplicata, pois outro tíquete já implementa o fluxo da API gráfica. O SMTP com OAuth 2.0 permanece disponível para clientes que precisam sair da autenticação básica SMTP. (GRANITE-57478)

* As cadeias de caracteres na caixa de diálogo Permissões Efetivas agora estão alinhadas corretamente no Navegador **Ferramentas** > **Geral** > **Configuração**. Anteriormente, uma string era exibida fora de linha depois de selecionar uma pasta, clicar em Propriedades e em Permissões efetivas. As regras de layout atualizadas restauram o alinhamento. (CQ-4359166)


#### Projetos {#foundation-projects-6526}

A string &quot;Selecionar diretório raiz&quot; na caixa de diálogo Selecionar dicionário i18n agora é exibida por completo. Anteriormente, o texto era cortado em várias interfaces localizadas depois que você criava um projeto de tradução e adicionava um dicionário i18n. O pacote `cq-projects-translation-content` atualizado fornece à cadeia de caracteres espaço suficiente. (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### Tradução{#foundation-translation-6526}

As opções de estilo do componente Lista agora são exibidas no idioma do usuário. Anteriormente, cadeias de caracteres como Bloco e Grade permaneciam em inglês no menu Estilos depois que os autores adicionavam o componente Lista a um Fragmento de experiência. Os recursos atualizados fornecem as traduções, incluindo as interfaces coreana, chinês simplificado e chinês tradicional. (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### Fluxo de trabalho{#foundation-workflow-6526}

Melhoria: o Editor de páginas da interface para toque agora renderiza a Árvore de conteúdo e oferece suporte à edição de componentes de Definição de recursos em páginas de pacote de fluxo de trabalho. Anteriormente, as páginas em `/etc/workflow/packages/` que **Gerenciar Publicação** > **Publicar Mais Tarde** cria não mostravam nenhuma Árvore de Conteúdo no painel esquerdo, e os autores falharam ao editar os componentes de Definição de Recursos. Agora, os aprovadores inspecionam páginas e ativos em uma carga de fluxo de trabalho na interface para toque, correspondendo ao comportamento da interface clássica. (GRANITE-65620)

## Instalar [!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0 requer [!DNL Experience Manager] 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do Service Pack está disponível na [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) da Adobe.
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.26.0 em uma das instâncias do Autor usando o Gerenciador de Pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> A Adobe recomenda que você não remova ou desinstale o pacote [!DNL Experience Manager] 6.5.26.0. Para reverter, se necessário, crie um backup do `crx-repository` antes de instalar o pacote. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar o Service Pack em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].

1. Baixe o Service Pack de [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para obter mais informações, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Repositório de Dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Gerenciador de pacotes é fechada durante a instalação do Service Pack. A Adobe recomenda que você aguarde os logs de erro pararem de mudar antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de confirmar se a instalação foi bem-sucedida. Este problema ocorre no navegador [!DNL Safari], mas pode ocorrer ocasionalmente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar o [!DNL Experience Manager] 6.5.26.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.26.0 não oferece suporte à instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (6.5.26.0)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi estão **[!UICONTROL ATIVOS]** ou **[!UICONTROL FRAGMENTOS]** no Console OSGi (Use o Console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.20 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para o Forms [!DNL Experience Manager]{#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o Service Pack no Experience Manager Forms, consulte [instruções de instalação do Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>O recurso de formulários adaptáveis, disponível no [Início rápido do AEM 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager{#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [Fragmento de conteúdo do Experience Manager com o pacote de índice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos usados.

A falha na instalação desse pacote resulta em consultas lentas ou com falha do GraphQL.

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar{#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.26.0 está disponível no [repositório central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/). <!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
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
     Novas pastas para `cache` e `diff-cache` são criadas automaticamente e você não tem mais uma exceção relacionada a `mvstore` no `error.log`.

* Atualize suas consultas do GraphQL que usaram um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Uma consulta GraphQL usa o índice `damAssetLucene` em vez do índice `fragments`. Essa ação resulta em consultas do GraphQL que falham ou demoram muito para serem executadas.

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

  Após essas etapas, as consultas do GraphQL são executadas com velocidade aprimorada.

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas. Falha na consulta em segundo plano; a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se você atualizar sua instância do [!DNL Experience Manager] de 6.5.0 para 6.5.4 para o Service Pack mais recente no Java™ 11, verá `RRD4JReporter` exceções no arquivo `error.log`. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Os seguintes erros e mensagens de aviso são exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
  * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
  * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
  * `com.adobe.granite.maintenance.impl.TaskScheduler` : Nenhuma janela de manutenção encontrada em `granite/operations/maintenance`.
  * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão da alteração de registro não registrada.

* A partir do AEM 6.5.15, o Mecanismo Rhino JavaScript fornecido pelo pacote `org.apache.servicemix.bundles.rhino` tem um novo comportamento de elevação. Os scripts que usam o modo estrito (`use strict;`) devem declarar suas variáveis corretas. Caso contrário, eles não serão executados e acabarão gerando um erro de tempo de execução.

* A instalação de marcação relacionada ao conteúdo padrão por meio de um pacote de atualização oficial redefine a propriedade languages do nó `/content/cq:tags` para o padrão. Essa ação é verdadeira para Service Packs, Service Packs de segurança, Pacotes de recursos estendidos, Pacotes de recursos cumulativos, patches e assim por diante. Portanto, é necessário adicioná-lo às propriedades antes da instalação.

### Problema conhecido do AEM Sites {#known-issues-aem-sites-6526}

* **Problema conhecido com uma correção disponível para o AEM Foundation**

  Depois de atualizar de um pacote de serviços anterior para o Experience Manager 6.5.26.0, a ordenação de versão do pacote de CRXDE Lite pode impedir a Experience Manager de selecionar o pacote desejado. Para corrigir a solicitação de versão, instale o Service Pack 26 e baixe e instale o hotfix [`CRXDE Lite hotfix GRANITE-76725`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fgranite-76725%2Fcq-6.5.26-hotfix-GRANITE-76725-1.0.zip) da Distribuição de Software. A correção é uma atualização somente de versão. Ele não contém alterações funcionais ou de código. (GRANITE-76725)

* A visualização dos fragmentos de conteúdo falha devido à proteção do DoS para uma grande árvore de fragmentos. Consulte o artigo [KB sobre as opções de configuração padrão do GraphQL Query Executor](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conhecidos do AEM Forms {#known-issues-aem-forms-6526}

* Quando um formulário contendo um campo **Anexo de Arquivo** que usa `bindref` é enviado a um Fluxo de Trabalho do AEM com uma etapa **Atribuir Tarefa**, os anexos não são exibidos. Como resultado, eles não aparecem quando a tarefa é aberta da Caixa de entrada. Os arquivos são salvos corretamente no repositório, mas a interface do usuário da etapa Atribuir tarefa não exibe os anexos. (FORMS-23722)

* Quando um PDF assinado digitalmente é anexado a uma tarefa no AEM Forms JEE Workspace, o upload permanece preso no estado de upload ou falha com um erro &quot;Arquivo inválido&quot;. Como resultado, anexos maiores e assinados do PDF não podem ser adicionados à tarefa. Esse problema foi corrigido em uma versão posterior. Para obter uma correção para a versão do, entre em contato com o Suporte da Adobe. (FORMS-28517)

#### Problemas conhecidos com Hotfixes disponíveis {#aem-forms-issues-with-hotfixes}

Os seguintes problemas têm uma correção disponível para download e instalação. Você pode [baixar e instalar o Hotfix](/help/release-notes/aem-forms-hotfix.md) para resolver estes problemas:

* Depois de instalar o AEM Forms JEE Service Pack 21 (6.5.21.0), se você encontrar entradas duplicadas de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` na pasta `<AEM_Forms_Installation>/lib/caching/lib`, execute as seguintes etapas para resolver o problema (FORMS-14926):

  1. Pare os localizadores, se eles estiverem em execução.
  1. Pare o servidor do AEM.
  1. Vá para o `<AEM_Forms_Installation>/lib/caching/lib`.
  1. Remova todos os arquivos de correção Geode, exceto `geode-*-1.15.1.2.jar`. Confirme se apenas os jars Geode com `version 1.15.1.2` estão presentes.
  1. Abra o prompt de comando no modo de administração.
  1. Instale o patch Geode usando o arquivo `geode-*-1.15.1.2.jar`.

## Pacotes da OSGi e pacotes de conteúdo inclusos{#osgi-bundles-and-content-packages-included}

Os arquivos zip a seguir contêm os documentos de texto que listam os pacotes OSGi e os Pacotes de Conteúdo incluídos nesta versão do Service Pack do [!DNL Experience Manager] 6.5:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de Pacotes de Conteúdo incluídos no Experience Manager 6.5.26.0](/help/release-notes/assets/65260-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites estão disponíveis somente para clientes do. Se você for cliente e precisar de acesso, entre em contato com o seu gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Fale com o suporte ao cliente da Adobe](https://experienceleague.adobe.com/pt-br/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/br/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65)
>* [Inscreva-se para obter atualizações de produto prioritárias da Adobe](https://www.adobe.com/br/subscription/priority-product-update.html)




