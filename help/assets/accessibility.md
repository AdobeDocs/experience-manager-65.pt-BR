---
title: Recursos e interfaces acessíveis do  [!DNL Experience Manager Assets]
description: Saiba como os recursos de acessibilidade do  [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] ajudam usuários portadores de deficiências.
contentOwner: AG
feature: Asset Management
role: User, Developer, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Recursos de acessibilidade em [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

O [!DNL Adobe Experience Manager] permite que criadores e editores de conteúdo ofereçam experiências surpreendentes na Web. A Adobe se esforça para incluir os criadores com deficiência melhorando a acessibilidade do [!DNL Experience Manager]. O software é aprimorado continuamente para atender às necessidades de todos os tipos de usuários e aderir aos padrões mundiais que incluem indivíduos com deficiências visuais, auditivas, de mobilidade ou outras.

O [!DNL Experience Manager] publica informações de conformidade que descrevem os padrões aos quais segue, descreve os recursos de acessibilidade no produto e o nível de conformidade. Os relatórios de conformidade de acessibilidade ajudam [!DNL Experience Manager] usuários a entender o nível de adesão a vários padrões. Os aprimoramentos feitos no [!DNL Assets] permitem que todos os usuários usem as interfaces facilmente por meio de teclado, leitor de tela, ampliadores e outras tecnologias de assistência.

O [!DNL Experience Manager] fornece vários níveis de suporte para os seguintes padrões:

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Seção 508 revisada da Lei de Reabilitação](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Iniciativa de Acessibilidade - WAI-ARIA (Aplicativos Rich Internet Acessíveis) por W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)

Para ler um relatório com detalhes sobre o nível de conformidade, consulte a página [Relatório de conformidade para acessibilidade](https://www.adobe.com/accessibility/compliance.html) (ACR).

Para saber como o [!DNL Dynamic Media] está acessível, consulte [acessibilidade em [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologias assistivas {#at-support}

Os usuários portadores de deficiências frequentemente dependem de hardware e software para acessar conteúdo da Web e usar produtos de software. Essas ferramentas são conhecidas como tecnologias assistivas. O [!DNL Experience Manager Assets] pode trabalhar com os seguintes tipos de tecnologias assistivas (AT) ao usar as funcionalidades principais do software:

* Leitores de tela e ampliadores de tela.
* Software de reconhecimento de voz.
* Uso do teclado - navegação e atalhos.
* Hardware de assistência, incluindo controles de switch, monitores Braille atualizáveis e outros dispositivos de entrada de computador.
* Ferramentas de ampliação da interface do usuário.

## [!DNL Experience Manager Assets] casos de uso acessíveis {#accessible-assets-use-cases}

No [!DNL Experience Manager], os recursos de acessibilidade atendem a dois requisitos principais de [!DNL Experience Manager] usuários e seus clientes.

* Para designers e criadores de conteúdo, há recursos para criar e publicar conteúdo acessível que é usado por sua vez pelos clientes e visitantes do site. Os indivíduos com deficiência usam o conteúdo com a ajuda de tecnologias assistivas. Para obter detalhes, consulte [diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md).
* O [!DNL Experience Manager] também permite que seus usuários e administradores com deficiência acessem a interface e os controles do usuário para criar e gerenciar conteúdo. O indivíduo com deficiência pode usar tecnologias assistivas para navegar, usar e gerenciar o recurso [!DNL Assets].

Os recursos principais do [!DNL Assets] estão mais acessíveis do que antes e são atualizados regularmente para melhorar a conformidade com os padrões globais. As operações CRUD em [!DNL Assets] têm algum grau de acessibilidade interna. Fluxos de trabalho do DAM, como adicionar, gerenciar, pesquisar e distribuir ativos, podem ser acessados com a ajuda de atalhos de teclado, texto de leitor de tela, contraste de cores etc.

## Suporte para uso do teclado {#keyboard-use}

Muitos elementos da interface do usuário que são clicáveis ou acionáveis com um ponteiro também podem ser envolvidos com o uso do teclado. Usando um teclado, os usuários podem se concentrar em elementos da interface do usuário e realizar a ação apropriada. Os usuários podem usar atalhos do teclado diretamente para acionar um comando ou uma ação sem precisar se concentrar em elementos da interface do usuário e acioná-la usando o teclado. Por exemplo, os usuários podem abrir a linha do tempo de um ativo no lado esquerdo da interface do usuário navegando até o controle da interface do usuário com o teclado e selecionando `Return` e o atalho de teclado `Alt + 2`.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Atalhos de teclado em [!DNL Assets] {#keyboard-shortcuts}

As seguintes ações em [!DNL Assets] funcionam com os atalhos de teclado listados. A maioria dos atalhos de teclado que se aplicam aos Consoles do [!DNL Experience Manager] também se aplicam ao [!DNL Assets]. Consulte [atalhos de teclado para Consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Veja como [habilitar ou desabilitar os atalhos de teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interface do usuário ou cenário | Atalho de teclado | Ação |
|---|---|---|
| Exibição de coluna na interface do usuário [!DNL Assets] | Teclas de seta para cima e para baixo | Navegue até os arquivos e pastas dentro da mesma hierarquia. |
| Exibição de coluna na interface do usuário [!DNL Assets] | Teclas de seta para a esquerda e para a direita | Navegar para arquivos e pastas acima ou abaixo da pasta atual. |
| Procurando pastas em [!DNL Assets] | `/` | Chame a pesquisa abrindo a caixa Omnisearch. |
| Console [!DNL Assets] | &grave; | Alternar painéis laterais |
| Console [!DNL Assets] | `Alt + 1` | Abra a árvore de conteúdo. |
| Console [!DNL Assets] | `Alt + 2` | Abra o painel esquerdo [!UICONTROL Navegação]. |
| Console [!DNL Assets] | `Alt + 3` | Exibir [!UICONTROL Linha do tempo] de um ativo selecionado. |
| Console [!DNL Assets] | `Alt + 4` | Abrir referências da Live Copy do ativo selecionado. |
| Console [!DNL Assets] | `Alt + 5` | Iniciar pesquisa na pasta selecionada. |
| O ativo ou a pasta está selecionado | Backspace | Excluir o ativo ou pasta selecionada. |
| O ativo ou a pasta está selecionado | `p` | Abra a página Propriedades do ativo selecionado. |
| O ativo ou a pasta está selecionado | `e` | Editar o ativo selecionado. |
| O ativo ou a pasta está selecionado | `m` | Mova o ativo selecionado. |
| O ativo ou a pasta está selecionado | `Ctrl + c` | Copie o ativo selecionado. |
| O ativo ou a pasta está selecionado | `Esc` | Cancele a seleção. |
| A caixa de diálogo é aberta e está em foco | `Esc` | Fechar caixa de diálogo. |
| Dentro de uma pasta no DAM | `Ctrl + v` | Cole o ativo copiado. |
| Console [!DNL Assets] | `Ctrl + A` | Selecione todos os ativos. |
| Páginas de propriedades de ativos | `Ctrl + S` | Salve as alterações. |
| Console [!DNL Assets] | `?` | Consulte uma lista de atalhos de teclado. |

## Entrar e navegar na interface de usuário do [!DNL Assets] {#login}

Os usuários podem usar o teclado para navegar até o campo de logon e preenchê-lo. As mensagens de erro resultantes de combinações incorretas de nome de usuário e senha na página de logon são anunciadas por leitores de tela sempre que o erro ocorre.

Depois de fazer logon, os usuários do DAM podem navegar na interface do usuário do [!DNL Assets] usando o teclado. Os elementos da interface do usuário, como painel esquerdo, menus, perfil do usuário, barra de pesquisa, arquivos e pastas, e as configurações e administração podem ser navegados usando o teclado. A ordem de navegação do teclado é da esquerda para a direita e de cima para baixo. Ao navegar usando um teclado, uma opção acionável quando focalizado é realçada com melhor contraste de cores e é narrada por um leitor de tela. Quando apropriado, o estado — por exemplo, expandido, recolhido e misturado — das opções focadas no menu é anunciado por um leitor de tela. Além disso, o leitor de tela anuncia a finalidade da opção acionável, em vez de, digamos, a aparência ou a disposição da interface.

Se um usuário expandir a ajuda ou a opção de perfil do usuário no menu, o leitor de tela anunciará a opção ou o status apropriado. Se um usuário expandir a opção de perfil do usuário, as opções disponíveis poderão ser selecionadas usando um teclado. Por exemplo, um administrador pode representar um usuário diferente. Se um usuário procurar uma cadeia de caracteres na opção [!UICONTROL Ajuda], o narrador anunciará &quot;Procurando Ajuda&quot; para indicar que uma pesquisa está em andamento.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Procurar ativos e exibir as informações relacionadas {#browse}

Na interface do usuário do [!DNL Assets], os usuários podem usar o teclado para navegar pela lista de ativos digitais existentes no repositório do DAM, visualizar ou baixar um ativo, ver representações geradas, alternar exibições, ver as representações geradas, ver o histórico da linha do tempo e da versão, ver comentários e referências, e ver e gerenciar metadados.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Ao navegar pelo repositório de ativos, a seguinte funcionalidade melhora a acessibilidade:

* O leitor de tela anuncia alternativas em texto que descrevem a finalidade ou a funcionalidade dos ícones em vez de seus nomes.
* Os usuários podem acessar e focalizar as opções da interface do usuário interativa na lista de referências de ativos usando teclas de teclado.
* Os elementos em cada linha na exibição de lista são anunciados como os elementos da mesma linha pelos leitores de tela.
* Ao navegar usando a tecla `Tab`, o foco pode se mover para a opção fechar na pré-visualização da versão.
* Ao usar o teclado para navegar, as opções da interface do usuário acionáveis destacadas têm foco visual mais proeminente com contraste aprimorado. Isso torna a área focada mais identificável para o usuário.
* O uso da tecla `Esc` para remover os ícones de ação rápida da exibição de miniatura não remove o foco do teclado do último item focalizado.
* Com um ativo selecionado, selecionar o atalho de teclado `Alt + 4` abre a lista [!UICONTROL Referências] no painel esquerdo. Usando a chave `Tab`, os usuários podem navegar pelas entradas de referência diferentes de zero. Navegar somente pelas entradas de referência diferentes de zero também economiza esforço e pressionamentos de tecla.
* Comentários em um ativo estão disponíveis na linha do tempo do ativo. Ele é acessível se o painel esquerdo for acessado pelo teclado ou por um atalho de teclado.
* As [!UICONTROL Configurações de Exibição] em [!DNL Experience Manager] podem ser acessadas com teclado. Os usuários podem navegar pelos tamanhos de cartão disponíveis usando as teclas de seta e selecionar e navegar pela guia para navegar e definir outros elementos na visualização Configurações de exibição existente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Gerenciar ativos digitais {#manage-assets}

Muitas tarefas de gerenciamento de ativos, como operações CRUD, download de um ativo e adição de metadados, estão acessíveis em vários graus. O [!DNL Assets] permite que você realize as tarefas usando várias tecnologias de assistência, como um leitor de tela e um teclado.

Veja uma demonstração em vídeo de como usar um teclado para [navegar no repositório e baixar um ativo](https://youtu.be/K3dgqMRQJys).

Para operações de metadados que normalmente são realizadas por funções, como profissionais de marketing e administradores, os seguintes recursos melhoram a acessibilidade:

* A opção [!UICONTROL Salvar e fechar] na página [!UICONTROL Propriedades] do ativo agora pode ser acessada com o teclado.
* Os leitores de tela anunciam as opções para excluir as marcas selecionadas na guia [!UICONTROL Básico] do ativo [!UICONTROL Propriedades].
* Os usuários podem usar a caixa de diálogo pop-up do Datepicker com um teclado. O elemento da interface do usuário do Datepicker é usado para definir horários de ativação e desativação e selecionar data.
* A funcionalidade de arrastar usando o teclado funciona corretamente no [!UICONTROL Editor de Esquema de Metadados] no modo de navegação do leitor de tela.
* Um usuário pode mover o foco usando o teclado para o campo Adicionar usuário ou grupo em [!UICONTROL Grupo de usuários fechado] na guia [!UICONTROL Permissões] da pasta [!UICONTROL Propriedades].

## Pesquisar ativos digitais {#search-assets}

Uma experiência de pesquisa de ativos rápida e contínua aumenta a velocidade do conteúdo. Os casos de uso de velocidade do conteúdo fazem parte da funcionalidade principal [!DNL Assets]. Para iniciar uma pesquisa na barra Omnisearch, os usuários podem usar o atalho de teclado `/` ou usar `Tab` junto com leitores de tela para localizar rapidamente a opção de pesquisa. O leitor de tela narra o nome da opção como &quot;Botão de Pesquisa&quot; quando o foco está na opção de pesquisa ![opção de pesquisa](assets/do-not-localize/search_icon.png). Os usuários podem selecionar `Return` para abrir a caixa Omnisearch. O leitor de tela não só narra a palavra-chave digitada na caixa de pesquisa como também narra as sugestões oferecidas por [!DNL Experience Manager Assets]. Os usuários podem usar uma combinação de teclas de seta, `Return` e `Tab` para acessar as várias opções para acionar uma pesquisa.

A funcionalidade de pesquisa se torna acessível pela seguinte funcionalidade:

* O título da página, conforme disponível para um leitor de tela, ajuda a identificar a página como a página de pesquisa dos ativos.
* Os usuários pesquisam ativos no campo Omnisearch. Os usuários podem abri-lo usando a navegação pelo teclado ou o atalho de teclado `/`.
* Os usuários podem começar a digitar a palavra-chave de pesquisa e, em seguida, selecionar as sugestões automáticas usando as teclas de seta. A sugestão realçada pode ser selecionada usando a chave `Return` e os ativos são pesquisados para a sugestão selecionada.
* Os leitores de tela podem identificar e anunciar as caixas de seleção de estado misto (nas quais, a menos que você selecione todos os predicados aninhados, as caixas de seleção de primeiro nível não estão marcadas e estão marcadas) no painel Filtros ao filtrar os resultados da pesquisa.
* O foco do usuário passa para as opções de pesquisa depois que a caixa Omnisearch é fechada.

Ao filtrar os resultados da pesquisa:

* A página de resultados da pesquisa tem um título informativo para entender melhor os usuários de leitores de tela.
* Um leitor de tela anuncia as opções no filtro de pesquisa como acordeões expansíveis.
* Os predicados que têm opções de estado misto são anunciados por leitores de tela.

## Compartilhar ativos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Ao compartilhar ativos, as seguintes funcionalidades melhoram a acessibilidade:

* Um usuário pode mover o foco usando o teclado no campo Pesquisar e adicionar endereço de email na caixa de diálogo de compartilhamento de link.

* Na caixa de diálogo de compartilhamento de links, no modo de navegação, os leitores de tela

   * Não narre as informações da tabela quando a caixa de diálogo for carregada.
   * Pode navegar por todas as sugestões listadas.
   * Narre as sugestões exibidas para Adicionar endereço de email e Pesquisar campos.

## Documentação acessível {#accessible-docs}

O [!DNL Experience Manager] fornece documentação acessível para uso por pessoas com deficiência. Os itens a seguir ajudam a tornar a oferta de conteúdo acessível por enquanto, enquanto o Adobe continua a melhorar o modelo e o conteúdo:

* Os leitores de tela podem ler o texto.
* Imagens e ilustrações têm texto alternativo disponível.
* A navegação pelo teclado é possível.
* As taxas de contraste ajudam a destacar algumas partes do site de documentação.

## Fornecer feedback {#a11y-feedback}

Para fornecer feedback, fazer perguntas e solicitar aprimoramentos do produto relacionados à acessibilidade, use os seguintes métodos:

* Preencha o formulário em [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envie um email para access@adobe.com.

>[!MORELIKETHIS]
>
>* [Recursos de acessibilidade em [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de versão das melhorias feitas em cada versão do Service Pack](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] orientação de acessibilidade](/help/managing/web-accessibility.md).
>* [Relatórios de conformidade (ACR) e listagem VPAT para soluções da Adobe](https://www.adobe.com/accessibility/compliance.html).
