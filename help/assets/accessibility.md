---
title: Recursos e interfaces acessíveis do  [!DNL Experience Manager Assets]
description: Saiba como os recursos de acessibilidade em [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] ajudam usuários portadores de deficiência.
contentOwner: AG
feature: Gerenciamento de ativos
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1926'
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

[!DNL Adobe Experience Manager] O permite que criadores e editores de conteúdo vejam experiências incríveis na Web. O Adobe se esforça para incluir os criadores com deficiência, melhorando a acessibilidade de [!DNL Experience Manager]. O software é aprimorado continuamente para atender às necessidades de todos os tipos de usuários e seguir os padrões mundiais que incluem indivíduos com deficiências visuais, auditivas, de mobilidade ou outras.

[!DNL Experience Manager] O publica informações de conformidade que descrevem os padrões que ele adere, descreve os recursos de acessibilidade do produto e descreve o nível de conformidade. Os relatórios de conformidade de acessibilidade ajudam os usuários a entender o nível de adesão a vários padrões. [!DNL Experience Manager] As melhorias feitas em [!DNL Assets] permitem que todos os usuários usem as interfaces facilmente por meio de teclado, leitor de tela, ampliadores e outras tecnologias de assistência.

[!DNL Experience Manager] fornece níveis variáveis de suporte para os seguintes padrões:

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Seção 508 da Lei](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines) de Reabilitação revista.
* [Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) by W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [PT 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para ler um relatório com detalhes do nível de conformidade, consulte a página [Relatório de conformidade de acessibilidade](https://www.adobe.com/accessibility/compliance.html) (ACR) .

Para saber como [!DNL Dynamic Media] é acessível, consulte [acessibilidade em [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologias de assistência {#at-support}

Os usuários portadores de deficiências dependem frequentemente de hardware e software para acessar conteúdo da Web e usar produtos de software. Essas ferramentas são conhecidas como tecnologias de assistência. [!DNL Experience Manager Assets] O pode trabalhar com os seguintes tipos de tecnologias de assistência (AT) ao usar as funcionalidades principais do software:

* Leitores de tela e ampliador de tela.
* Software de reconhecimento de voz.
* Uso do teclado - navegação e atalhos.
* Hardware auxiliar, incluindo controles de switch, exibições em Braille atualizáveis e outros dispositivos de entrada de computador.
* Ferramentas de aumento da interface do usuário.

## [!DNL Experience Manager Assets] casos de uso acessíveis {#accessible-assets-use-cases}

Em [!DNL Experience Manager], os recursos de acessibilidade atendem a dois requisitos principais de [!DNL Experience Manager] usuários e seus clientes.

* Para designers e criadores de conteúdo, há recursos para criar e publicar conteúdo acessível que é usado por sua vez pelos clientes e visitantes do site. Os indivíduos com deficiência usam o conteúdo com a ajuda de tecnologias de assistência. Para obter detalhes, consulte [diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] O também permite que os usuários e administradores com deficiência acessem a interface do usuário e os controles para criar e gerenciar conteúdo. O indivíduo com deficiência pode usar tecnologias de assistência para navegar, usar e gerenciar o recurso [!DNL Assets].

Os recursos principais em [!DNL Assets] são mais acessíveis do que antes e são atualizados regularmente para melhorar a conformidade com os padrões globais. As operações CRUD em [!DNL Assets] têm algum grau de acessibilidade incorporado nelas. Fluxos de trabalho do DAM como adicionar, gerenciar, pesquisar e distribuir ativos são acessíveis com a ajuda de atalhos do teclado, texto do leitor de tela, contraste de cores e assim por diante.

## Suporte para uso de teclado {#keyboard-use}

Muitos elementos da interface do usuário que são clicáveis ou acionáveis com um ponteiro também podem ser envolvidos com o uso do teclado. Usando um teclado, os usuários podem se concentrar em elementos da interface do usuário e tomar uma ação apropriada. Os usuários podem usar os atalhos de teclado diretamente para acionar um comando ou uma ação sem precisar se concentrar nos elementos da interface do usuário e acioná-la usando o teclado. Por exemplo, os usuários podem abrir a linha do tempo de um ativo no lado esquerdo da interface do usuário navegando até o controle da interface do usuário usando um teclado, selecionando `Return` e selecionando `Alt + 2` o atalho do teclado.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Atalhos de teclado em [!DNL Assets] {#keyboard-shortcuts}

As seguintes ações em [!DNL Assets] funcionam com os atalhos de teclado listados. A maioria dos atalhos de teclado que se aplicam aos Consoles [!DNL Experience Manager] também se aplica a [!DNL Assets]. Consulte [atalhos de teclado para Consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Consulte como [ativar ou desativar os atalhos do teclado](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interface do usuário ou cenário | Atalho de teclado | Ação |
|---|---|---|
| Exibição em coluna na interface do usuário [!DNL Assets] | Teclas de seta para cima e para baixo | Navegue até arquivos e pastas dentro da mesma hierarquia. |
| Exibição em coluna na interface do usuário [!DNL Assets] | Teclas de seta para a esquerda e para a direita | Navegue até arquivos e pastas acima ou abaixo da pasta atual. |
| Procurar pastas em [!DNL Assets] | `/` | Chame a pesquisa abrindo a caixa Omnisearch. |
| [!DNL Assets] Console | &amp;grave; | Alternar painéis laterais |
| [!DNL Assets] Console | `Alt + 1` | Abra a árvore de conteúdo. |
| [!DNL Assets] Console | `Alt + 2` | Abra o painel esquerdo [!UICONTROL Navegação]. |
| [!DNL Assets] Console | `Alt + 3` | Exibir [!UICONTROL Linha do tempo] de um ativo selecionado. |
| [!DNL Assets] Console | `Alt + 4` | Abrir referências da Live Copy do ativo selecionado. |
| [!DNL Assets] Console | `Alt + 5` | Iniciar pesquisa e pesquisa na pasta selecionada. |
| Ativo ou pasta selecionado | Backspace | Excluir o ativo ou a pasta selecionada. |
| Ativo ou pasta selecionado | `p` | Abra a página Propriedades do ativo selecionado. |
| Ativo ou pasta selecionado | `e` | Editar o ativo selecionado. |
| Ativo ou pasta selecionado | `m` | Mova o ativo selecionado. |
| Ativo ou pasta selecionado | `Ctrl + c` | Copie o ativo selecionado. |
| Ativo ou pasta selecionado | `Esc` | Cancelar a seleção. |
| A caixa de diálogo é aberta e está em foco | `Esc` | Caixa de diálogo Fechar. |
| Dentro de uma pasta no DAM | `Ctrl + v` | Cole o ativo copiado. |
| [!DNL Assets] Console | `Ctrl + A` | Selecione todos os ativos. |
| Páginas de propriedade do ativo | `Ctrl + S` | Salve as alterações. |
| [!DNL Assets] Console | `?` | Consulte uma lista de atalhos do teclado. |

## Fazer logon e navegar pela interface do usuário [!DNL Assets] {#login}

Os usuários podem usar o teclado para navegar até o campo de logon e preenchê-lo para fazer logon. As mensagens de erro devido a combinações incorretas de nome de usuário e senha na página de logon são anunciadas pelos leitores de tela sempre que o erro ocorrer.

Depois de fazer logon, os usuários do DAM podem navegar na interface do usuário [!DNL Assets] usando o teclado. Os elementos da interface do usuário, como o painel à esquerda, menus, perfil do usuário, barra de pesquisa, arquivos e pastas, e as configurações de administração e configuração são navegáveis usando o teclado. A ordem de navegação do teclado é da esquerda para a direita e de cima para baixo. Ao navegar usando um teclado, uma opção acionável quando focalizado é realçada com melhor contraste de cor e é narrada por um leitor de tela. Quando apropriado, o estado — por exemplo, expandido, recolhido e de estado misto — das opções focadas no menu é anunciado por um leitor de tela. Além disso, o leitor de tela anuncia a finalidade da opção acionável, em vez de, digamos a aparência ou o posicionamento da interface.

Se um usuário expandir a opção de ajuda ou perfil de usuário do menu, o leitor de tela anunciará a opção ou o status apropriado. Se um usuário expandir a opção de perfil do usuário, as opções disponíveis poderão ser selecionadas com teclado. Por exemplo, um administrador pode representar um usuário diferente. Se um usuário pesquisar uma string na opção [!UICONTROL Ajuda], um narrador anuncia &quot;Ajuda para pesquisa&quot; para indicar que uma pesquisa está em andamento.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Procurar ativos e exibir as informações relacionadas {#browse}

Na interface do usuário [!DNL Assets], os usuários podem usar o teclado para navegar pela lista de ativos digitais existentes no repositório DAM, visualizar ou baixar um ativo, ver representações geradas, alternar visualizações, ver as representações geradas, ver a linha do tempo e o histórico da versão, ver comentários e referências e exibir e gerenciar metadados.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Ao navegar pelo repositório de ativos, a seguinte funcionalidade melhora a acessibilidade:

* O leitor de tela anuncia alternativas em texto que representam a finalidade ou a funcionalidade dos ícones, em vez de seus nomes.
* Os usuários podem acessar e focalizar as opções interativas da interface do usuário na lista Referências de ativos usando teclas do teclado.
* Os elementos em cada linha na exibição de lista são anunciados como elementos da mesma linha pelos leitores de tela.
* Ao navegar usando a tecla `Tab`, o foco pode se mover para a opção fechar na visualização da versão.
* Ao usar o teclado para navegar, as opções destacadas da interface acionável têm foco visual mais proeminente com contraste aprimorado. Isso torna a área focada mais identificável para o usuário.
* Usar a tecla `Esc` para remover os ícones de ação rápida da exibição em miniatura não remove o foco do teclado do último item focado.
* Com um ativo selecionado, selecionar `Alt + 4` atalho de teclado abre a lista [!UICONTROL Referências] no painel esquerdo. Usando a tecla `Tab`, os usuários podem navegar pelas entradas de referência diferentes de zero. Navegar apenas pelas entradas de referência diferentes de zero também economiza esforço e pressionamentos de teclas.
* Comentários em um ativo estão disponíveis na linha do tempo do ativo. É acessível se o painel esquerdo for acessado usando um teclado ou um atalho de teclado.
* [!UICONTROL As ] configurações de visualização no  [!DNL Experience Manager] podem ser acessadas pelo teclado. Os usuários podem navegar pelos tamanhos de cartão disponíveis usando as teclas de seta e selecionar e percorrer para navegar e definir outros elementos na exibição Configurações de exibição existente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Gerenciar ativos digitais {#manage-assets}

Muitas tarefas de gerenciamento de ativos, como operações CRUD, download de um ativo e adição de metadados, podem ser acessadas em vários graus. [!DNL Assets] permite realizar as tarefas usando várias tecnologias de assistência, como um leitor de tela e um teclado.

Veja uma demonstração em vídeo de como usar um teclado para [navegar pelo repositório e baixar um ativo](https://youtu.be/K3dgqMRQJys).

Para operações de metadados normalmente realizadas por funções como profissionais de marketing e administradores, os seguintes recursos melhoram a acessibilidade:

* [!UICONTROL A opção Salvar e ] fechar em   Propriedades do ativo agora pode ser acessada usando o teclado.
* Os leitores de tela anunciam as opções para excluir as tags selecionadas na guia [!UICONTROL Basic] do ativo [!UICONTROL Properties].
* Os usuários podem usar a caixa de diálogo pop-up Datepicker com um teclado. O elemento da interface do usuário do Datepicker é usado para definir horários e horários e selecionar data.
* A funcionalidade de arrastar usando o teclado funciona corretamente no [!UICONTROL Editor de esquema de metadados] no modo de navegação do leitor de tela.
* Um usuário pode mover o foco usando o teclado para o campo Adicionar usuário ou grupo sob [!UICONTROL Grupo de usuários fechado] na guia [!UICONTROL Permissões] da pasta [!UICONTROL Propriedades].

## Pesquisar ativos digitais {#search-assets}

Uma experiência de pesquisa de ativos rápida e contínua aumenta a velocidade do conteúdo. Os casos de uso de velocidade do conteúdo são parte da funcionalidade principal [!DNL Assets]. Para iniciar uma pesquisa na barra Omnisearch, os usuários podem usar o atalho de teclado `/` ou usar `Tab` junto com leitores de tela para localizar rapidamente a opção de pesquisa. O leitor de tela narra o nome da opção como &quot;Botão de pesquisa&quot; quando o foco está na opção de pesquisa ![opção de pesquisa](assets/do-not-localize/search_icon.png). Os usuários podem selecionar `Return` para abrir a caixa Omnisearch. O leitor de tela não apenas narra a palavra-chave digitada na caixa de pesquisa, como também narra as sugestões oferecidas por [!DNL Experience Manager Assets]. Os usuários podem usar uma combinação de teclas de seta, `Return` e `Tab` para acessar as várias opções para acionar uma pesquisa.

A funcionalidade de pesquisa é disponibilizada pela seguinte funcionalidade:

* O título da página, conforme disponível para um leitor de tela, ajuda a identificar a página como a página de pesquisa dos ativos.
* Os usuários pesquisam ativos no campo Omnisearch . Os usuários podem abri-lo usando a navegação do teclado ou o atalho de teclado `/`.
* Os usuários podem começar a digitar a palavra-chave de pesquisa e, em seguida, selecionar as sugestões automáticas usando teclas de seta. A sugestão realçada pode ser selecionada usando a chave `Return` e os ativos são pesquisados para a sugestão selecionada.
* Os leitores de tela podem identificar e anunciar as caixas de seleção de estado misto (nas quais, a menos que você selecione todos os predicados aninhados, as caixas de seleção de primeiro nível não estão selecionadas e são filtradas) no painel Filtros ao filtrar os resultados da pesquisa.
* O foco do usuário é movido para as opções de pesquisa depois que a caixa Omnisearch é fechada.

Ao filtrar os resultados da pesquisa:

* A página de resultados da pesquisa tem um título informativo para entender melhor os usuários de leitores de tela.
* Um leitor de tela anuncia as opções no filtro de pesquisa como opções expansíveis.
* Os predicados que têm opções de estado misto são anunciados pelos leitores de tela.

## Compartilhar ativos {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Ao compartilhar ativos, as seguintes funcionalidades melhoram a acessibilidade:

* Um usuário pode mover o foco usando o teclado no campo Pesquisar e adicionar endereço de email na caixa de diálogo de compartilhamento de links.

* Na caixa de diálogo de compartilhamento de link, ao navegar no modo de navegação, os leitores de tela,

   * Não narre as informações da tabela quando a caixa de diálogo for carregada.
   * É possível navegar até todas as sugestões listadas.
   * Restrinja as sugestões exibidas para os campos Adicionar endereço de email e Pesquisar .

## Documentação acessível {#accessible-docs}

[!DNL Experience Manager] O fornece documentação acessível para uso por pessoas com deficiência. O seguinte ajuda a tornar a oferta de conteúdo acessível por enquanto, enquanto o Adobe continua a melhorar o modelo e o conteúdo:

* Leitores de tela podem ler o texto.
* Imagens e ilustrações têm o texto alternativo disponível.
* A navegação por teclado é possível.
* As relações de contraste ajudam a destacar algumas partes do site da documentação.

## Fornecer feedback {#a11y-feedback}

Para fornecer feedback, fazer perguntas e solicitar aprimoramentos de produtos relacionados à acessibilidade, use os seguintes métodos:

* Preencha o formulário em [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envie um email para access@adobe.com.

>[!MORELIKETHIS]
>
>* [Recursos de acessibilidade em [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notas de versão das melhorias feitas em cada versão](/help/release-notes/new-features-latest-service-pack.md) do Service Pack.
>* [[!DNL Adobe Experience Manager] orientação sobre acessibilidade](/help/managing/web-accessibility.md).
>* [Relatórios de conformidade (ACR) e lista de VPAT para soluções](https://www.adobe.com/accessibility/compliance.html) do Adobe.

