---
title: Acessibilidade em [!DNL Experience Manager Assets]
description: Saiba como os recursos de acessibilidade [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] ajudam os usuários portadores de deficiências.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 00f5a6194c8c29d358f362441c155c9c2a52cac7
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 2%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Recursos de acessibilidade em [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permite que criadores de conteúdo e editores sirvam experiências incríveis na Web. A Adobe esforça-se para incluir os criadores com deficiências, melhorando a acessibilidade de [!DNL Experience Manager]. O software é continuamente aprimorado para atender às necessidades de todos os tipos de usuários e para atender aos padrões mundiais que incluem indivíduos com deficiências visuais, auditivas, de mobilidade ou outras.

[!DNL Experience Manager] publica informações de conformidade que descrevem os padrões aos quais ele obedece, descreve os recursos de acessibilidade do produto e descreve o nível de conformidade. Os relatórios de conformidade de acessibilidade ajudam [!DNL Experience Manager] os usuários a entender o nível de adesão a vários padrões. Os aprimoramentos feitos no [!DNL Assets] permitem que todos os usuários usem as interfaces facilmente por meio do teclado, leitor de tela, ampliadores e outras tecnologias de assistência.

[!DNL Experience Manager] fornece níveis variáveis de suporte para os seguintes padrões:

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Revisão da seção 508 da Lei](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)de Reabilitação.
* [Iniciativa de acessibilidade - Aplicativos de Internet ricos acessíveis (WAI-ARIA) por W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [PT 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para ler um relatório com detalhes do nível de conformidade, consulte a página Relatório [de conformidade de](https://www.adobe.com/accessibility/compliance.html) acessibilidade (ACR).

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](/). -->

## Tecnologias de assistência {#at-support}

Os usuários portadores de deficiências dependem frequentemente de hardware e software para acessar conteúdo da Web e usar produtos de software. Essas ferramentas são conhecidas como tecnologias de assistência. [!DNL Experience Manager Assets] pode trabalhar com os seguintes tipos de tecnologias de assistência (AT) ao usar as funcionalidades principais do software:

* Leitores de tela e lente de aumento de tela.
* Software de reconhecimento de voz.
* Uso do teclado - navegação e atalhos.
* Hardware de assistência, incluindo controles de comutador, exibições em Braille atualizáveis e outros dispositivos de entrada de computador.
* Ferramentas de aumento da interface do usuário.

## [!DNL Experience Manager Assets] casos de uso acessíveis {#accessible-assets-use-cases}

Além disso, [!DNL Experience Manager]os recursos de acessibilidade atendem a dois requisitos principais dos [!DNL Experience Manager] usuários e de seus clientes.

* Para designers de conteúdo e criadores, há recursos para criar e publicar conteúdo acessível que é usado por sua vez pelos clientes e visitantes do site. As pessoas com deficiências usam o conteúdo com a ajuda de tecnologias de assistência. Para obter detalhes, consulte as diretrizes [de acessibilidade da](/help/managing/web-accessibility.md)Web.
* [!DNL Experience Manager] também permite que seus usuários e administradores com deficiências acessem a interface do usuário e controles para criar e gerenciar conteúdo. O indivíduo com deficiências pode usar tecnologias de assistência para navegar, usar e gerenciar os [!DNL Assets] recursos.

Os recursos principais em [!DNL Assets] são mais acessíveis do que antes e são atualizados regularmente para melhorar a conformidade com os padrões globais. As operações CRUD em [!DNL Assets] têm algum grau de acessibilidade incorporado a elas. Workflows DAM como adicionar, gerenciar, pesquisar e distribuir ativos podem ser acessados com a ajuda de atalhos do teclado, texto do leitor de tela, contraste de cores e assim por diante.

## Suporte para uso do teclado {#keyboard-use}

Muitos elementos da interface do usuário que podem ser clicados ou ativados com um ponteiro também podem ser envolvidos com o uso do teclado. Usando um teclado, os usuários podem se concentrar nos elementos da interface do usuário e realizar uma ação apropriada. Os usuários podem usar atalhos do teclado diretamente para acionar um comando ou uma ação sem precisar se concentrar nos elementos da interface e acioná-la usando o teclado. Por exemplo, os usuários podem abrir a linha do tempo de um ativo no lado esquerdo da interface do usuário navegando até o controle da interface do usuário usando um teclado, selecionando `Return`e selecionando um atalho do `Alt + 2` teclado.

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Atalhos de teclado em [!DNL Assets] {#keyboard-shortcuts}

As ações a seguir funcionam [!DNL Assets] com os atalhos de teclado listados. A maioria dos atalhos do teclado que se aplicam a [!DNL Experience Manager] Consoles também se aplicam a [!DNL Assets]. See [keyboard shortcuts for Consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte como [ativar ou desativar os atalhos](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)do teclado.

| Interface do usuário ou cenário | Atalho de teclado | Ação |
|---|---|---|
| Visualização de colunas na interface [!DNL Assets] do usuário | Teclas de seta para cima e para baixo | Navegue até arquivos e pastas dentro da mesma hierarquia. |
| Visualização de colunas na interface [!DNL Assets] do usuário | Teclas de seta para a esquerda e para a direita | Navegue até arquivos e pastas acima ou abaixo da pasta atual. |
| Procurando pastas em [!DNL Assets] | `/` | Chame a pesquisa abrindo a caixa Omnisearch. |
| [!DNL Assets] Console | ` | Alternar painéis laterais |
| [!DNL Assets] Console | `Alt + 1` | Abra a árvore de conteúdo. |
| [!DNL Assets] Console | `Alt + 2` | Abra o painel esquerdo [!UICONTROL Navegação] . |
| [!DNL Assets] Console | `Alt + 3` | Exibir [!UICONTROL Linha do tempo] de um ativo selecionado. |
| [!DNL Assets] Console | `Alt + 4` | Abrir referências de Live Copy do ativo selecionado. |
| [!DNL Assets] Console | `Alt + 5` | Pesquisa e pesquisa de start dentro da pasta selecionada. |
| Ativo ou pasta selecionado | Backspace | Exclua o ativo ou pasta selecionado. |
| Ativo ou pasta selecionado | `p` | Abra a página Propriedades do ativo selecionado. |
| Ativo ou pasta selecionado | `e` | Editar o ativo selecionado. |
| Ativo ou pasta selecionado | `m` | Mover o ativo selecionado. |
| Ativo ou pasta selecionado | `Ctrl + c` | Copie o ativo selecionado. |
| Ativo ou pasta selecionado | `Esc` | Desmarque a seleção. |
| A caixa de diálogo é aberta e está em foco | `Esc` | Caixa de diálogo Fechar. |
| Dentro de uma pasta no DAM | `Ctrl + v` | Cole o ativo copiado. |
| [!DNL Assets] Console | `Ctrl + A` | Selecione todos os ativos. |
| Páginas de propriedades do ativo | `Ctrl + S` | Salve as alterações. |
| [!DNL Assets] Console | `?` | Consulte uma lista de atalhos do teclado. |

## Fazer logon e navegar na interface [!DNL Assets] do usuário {#login}

Os usuários podem usar o teclado para navegar e preencher o campo de logon para fazer logon. As mensagens de erro devido a combinações incorretas de nome de usuário e senha na página de logon são anunciadas pelos leitores de tela sempre que o erro ocorrer.

Depois de fazer logon, os usuários do DAM podem navegar na interface [!DNL Assets] do usuário usando o teclado. Os elementos da interface do usuário, como o painel esquerdo, menus, perfil do usuário, barra de pesquisa, arquivos e pastas e configurações de administração e configuração são navegáveis usando o teclado. A ordem de navegação do teclado é da esquerda para a direita e de cima para baixo. Ao navegar usando um teclado, uma opção acionável quando focalizada é realçada com melhor contraste de cor e é narrada por um leitor de tela. Quando apropriado, o estado — por exemplo, expandido, recolhido e em estado misto — das opções focadas no menu é anunciado por um leitor de tela. Além disso, o leitor de tela anuncia a finalidade da opção acionável, em vez de, digamos, a aparência ou o posicionamento da interface.

Se um usuário expandir a opção de ajuda ou perfil do usuário no menu, o leitor de tela anunciará a opção ou o status apropriado. Se um usuário expandir a opção perfil do usuário, as opções disponíveis poderão ser selecionadas usando um teclado. Por exemplo, um administrador pode representar um usuário diferente. Se um usuário pesquisar por uma string na opção [!UICONTROL Ajuda] , um narrador anuncia &quot;Procurando ajuda&quot; para indicar que uma pesquisa está em andamento.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Procurar ativos e visualização nas informações relacionadas {#browse}

Na interface do [!DNL Assets] usuário, os usuários podem usar o teclado para navegar pela lista de ativos digitais existentes no repositório DAM, pré-visualização ou download de um ativo, ver renderizações geradas, alternar visualizações, ver as renderizações geradas, ver a linha do tempo e o histórico da versão, ver comentários e referências e visualização e gerenciar metadados.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Ao navegar pelo repositório de ativos, a seguinte funcionalidade melhora a acessibilidade:

* O leitor de tela anuncia alternativas em texto que descrevem a finalidade ou a funcionalidade dos ícones em vez de seus nomes.
* Os usuários podem acessar e focar as opções interativas da interface do usuário na lista Referências de ativos usando as teclas do teclado.
* Os elementos em cada linha na visualização da lista são anunciados como os elementos da mesma linha pelos leitores de tela.
* Ao navegar usando a `Tab` tecla, o foco pode se mover para a opção Fechar na pré-visualização da versão.
* Ao usar o teclado para navegar, as opções destacadas da interface do usuário acionável têm foco visual mais destacado com contraste aprimorado. Isso torna a área focada mais identificável para o usuário.
* O uso da `Esc` tecla para remover os ícones de ação rápida da visualização em miniatura não remove o foco do teclado do último item focalizado.
* Com um ativo selecionado, a seleção do atalho do `Alt + 4` teclado abre a lista [!UICONTROL Referências] no painel esquerdo. Usando a `Tab` chave, os usuários podem navegar pelas entradas de referência diferentes de zero. Navegar apenas pelas entradas de referência diferentes de zero também economiza esforço e pressionamentos de teclas.
* Os comentários em um ativo estão disponíveis na linha do tempo do ativo. É acessível se o painel esquerdo for acessado usando um teclado ou um atalho do teclado.
* [!UICONTROL As configurações] de visualização em [!DNL Experience Manager] estão acessíveis usando um teclado. Os usuários podem navegar pelos tamanhos de cartão disponíveis usando as teclas de seta e selecionar e percorrer para navegar e definir outros elementos na visualização de Configurações de Visualização existente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Gerenciar ativos digitais {#manage-assets}

Muitas tarefas de gerenciamento de ativos, como operações CRUD, download de um ativo e adição de metadados, estão acessíveis em vários graus. [!DNL Assets] permite que você realize as tarefas usando várias tecnologias de assistência, como um leitor de tela e um teclado.

Veja uma demonstração em vídeo de como usar um teclado para [navegar no repositório e baixar um ativo](https://youtu.be/K3dgqMRQJys).

Para operações de metadados que normalmente são feitas por funções como comerciantes e administradores, os seguintes recursos melhoram a acessibilidade:

* [!UICONTROL A opção Salvar e fechar] na página [!UICONTROL Propriedades] do ativo agora pode ser acessada usando o teclado.
* Os leitores de tela anunciam as opções para excluir as tags selecionadas na guia [!UICONTROL Básico] de [!UICONTROL Propriedades]do ativo.
* Os usuários podem usar a caixa de diálogo pop-up Datepicker com um teclado. O elemento da interface do usuário do Datepicker é usado para definir horários e horários de funcionamento e data de seleção.
* A funcionalidade de arrastar usando o teclado funciona corretamente no Editor [!UICONTROL de Schema de] Metadados no modo de navegação do leitor de tela.
* Um usuário pode mover o foco usando o teclado para o campo Adicionar usuário ou grupo em Grupo [!UICONTROL de usuários] fechado na guia [!UICONTROL Permissões] de [!UICONTROL Propriedades]da pasta.

## Pesquisar ativos digitais {#search-assets}

Uma experiência de pesquisa rápida e contínua de ativos aumenta a velocidade do conteúdo. Os casos de uso da velocidade de conteúdo são parte da [!DNL Assets] funcionalidade principal. Para start de uma pesquisa na barra Omnisearch, os usuários podem usar o atalho do teclado `/` ou usar `Tab` junto com os leitores de tela para localizar rapidamente a opção de pesquisa. O leitor de tela narra o nome da opção como &quot;Botão de pesquisa&quot; quando o foco está na opção ![de](assets/do-not-localize/search_icon.png)pesquisa da opção de pesquisa. Os usuários podem selecionar `Return` para abrir a caixa Omnisearch. O leitor de tela não apenas narra a palavra-chave digitada na caixa de pesquisa, como também narra as sugestões oferecidas por [!DNL Experience Manager Assets]. Os usuários podem usar uma combinação de teclas de seta `Return`e acessar `Tab` as várias opções para acionar uma pesquisa.

A funcionalidade de pesquisa é tornada acessível pela seguinte funcionalidade:

* O título da página, conforme disponível para um leitor de tela, ajuda a identificar a página como página de pesquisa dos ativos.
* Os usuários pesquisam ativos no campo Omnisearch. Os usuários podem abri-lo usando a navegação do teclado ou o atalho do teclado `/`.
* Os usuários podem start ao digitar a palavra-chave de pesquisa e selecionar as sugestões automáticas usando as teclas de seta. A sugestão realçada pode ser selecionada usando a `Return` chave e os ativos são pesquisados para a sugestão selecionada.
* Os leitores de tela podem identificar e anunciar as caixas de seleção de estado misto (nas quais, a menos que você marque todos os predicados aninhados, as caixas de seleção de primeiro nível não serão selecionadas e serão filtradas) no painel Filtros ao filtrar os resultados da pesquisa.
* O foco do usuário é movido para as opções de pesquisa depois que a caixa Omnisearch é fechada.

Ao filtrar os resultados da pesquisa:

* A página de resultados da pesquisa tem um título informativo para melhor compreensão dos usuários do leitor de tela.
* Um leitor de tela anuncia as opções no filtro de pesquisa como acordeões expansíveis.
* As previsões com opções de estado misto são anunciadas pelos leitores de tela.

## Compartilhar ativos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Ao compartilhar ativos, as seguintes funcionalidades melhoram a acessibilidade:

* Um usuário pode mover o foco usando o teclado no campo Pesquisar e Adicionar endereço de email na caixa de diálogo de compartilhamento de links.

* Na caixa de diálogo de compartilhamento de links, ao navegar no modo de navegação, os leitores de tela,

   * Não narre as informações da tabela quando a caixa de diálogo for carregada.
   * Pode navegar até todas as sugestões listadas.
   * Restrinja as sugestões exibidas para os campos Adicionar endereço de email e Pesquisar.

## Documentação acessível {#accessible-docs}

[!DNL Experience Manager] fornece documentação acessível para uso por pessoas com deficiência. O seguinte ajuda a tornar a oferta de conteúdo acessível por enquanto, enquanto o Adobe continua a melhorar o modelo e o conteúdo:

* Os leitores de tela podem ler o texto.
* Imagens e ilustrações têm texto alternativo disponível.
* A navegação do teclado é possível.
* As taxas de contraste ajudam a realçar algumas partes do site da documentação.

## Fornecer feedback {#a11y-feedback}

Para fornecer feedback, fazer perguntas e solicitar aprimoramentos de produtos relacionados à acessibilidade, use os seguintes métodos:

* Preencha o formulário em [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envie-nos um e-mail em access@adobe.com.

>[!MORELIKETHIS]
>
>* [Notas de versão de aprimoramentos feitos em cada versão](/help/release-notes/new-features-latest-service-pack.md).
>* [[!DNL Adobe Experience Manager] orientação](/help/managing/web-accessibility.md)sobre acessibilidade.
>* [Relatórios de conformidade (ACR) e lista VPAT para soluções](https://www.adobe.com/accessibility/compliance.html)de Adobe.

