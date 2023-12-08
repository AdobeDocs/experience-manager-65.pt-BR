---
title: Notas de versão do [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre versões, novidades, instruções de instalação e uma lista de alterações detalhada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '4233'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] Notas de versão do Service Pack 6.5 mais recente {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 07 de dezembro de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] O 6.5.19.0 inclui novos recursos, importantes melhorias solicitadas por clientes, correções de erros e melhorias de desempenho, estabilidade e segurança que foram lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este pacote de serviços](#install) em [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

## Principais recursos e melhorias

Alguns dos principais recursos e aprimoramentos desta versão incluem:

* Ativação do usuário do Editor de páginas do Sites/Componente de imagem para fazer referência a ativos do Cloud Service remoto de Ativos. (SITES-13448, SITES-13433)
* O AEM agora é compatível com a classificação do lado do servidor para agilizar a navegação do projeto na exibição em lista. Os nós de projeto são classificados com base na coluna selecionada pelo usuário antes de aparecer na interface.

### [!DNL Forms]

* **Novos componentes principais do formulário adaptável**: guias verticais, Termos e condições e Caixa de seleção são adicionados para aprimorar a escalabilidade dos formulários.
   * **[Componente da caixa de seleção](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de caixa de seleção. Permite que os usuários façam escolhas binárias, selecionando ou desmarcando uma opção específica. Normalmente, ela aparece como uma pequena caixa que pode ser clicada ou tocada para alternar entre dois estados: marcado e desmarcado. A caixa de seleção é um elemento de formulário comum usado para apresentar uma opção sim/não ou verdadeira/falsa.

   * **[Componente dos Termos e condições](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de Termos e condições. Ele permite que os autores de formulários introduzam uma seção específica no formulário em que os usuários recebem os termos, condições ou contratos legais associados ao uso de um serviço, produto ou plataforma. Esse componente foi projetado para informar os usuários sobre as regras, regulamentos e obrigações aos quais eles estão concordando ao enviar o formulário.

     ![Guias verticais, Termos e condições e componentes Caixa de seleção](/help/forms/using/assets/forms-components.png)

   * **[Componente de guias verticais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: o Forms adaptável baseado em Componentes principais agora pode organizar o conteúdo do formulário em uma lista vertical de guias, fornecendo um layout estruturado e navegável. O uso de guias verticais em um formulário pode aprimorar a experiência geral do usuário simplificando a navegação e melhorando a organização do conteúdo do formulário, especialmente em situações em que um formulário contém várias seções ou informações complexas.

* **[Versão de 64 bits do AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: A versão de 64 bits do AEM Forms Designer oferece desempenho, escalabilidade e gerenciamento de memória aprimorados para potencializar a experiência de criação de formulários. Com a arquitetura de 64 bits, você pode executar projetos ainda maiores e mais complexos com facilidade, garantindo fluxos de trabalho de design ininterruptos e eficiência otimizada. Aumente os recursos de design de formulário e abrace o futuro do AEM Forms Designer com esta versão de última geração.

* **[Conectar um Forms adaptável com a lista Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: o AEM Forms fornece uma integração OOTB para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você use os recursos de Listas do SharePoint. Você pode configurar a Lista de SharePoint do Microsoft como uma fonte de dados para um Modelo de dados de formulário e usar a ação de envio Enviar usando Modelo de dados de formulário para conectar um Formulário adaptável à Lista de SharePoint.

* **[Suporte para configurar propriedades do documento de registro para fragmentos de formulário adaptável](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Agora é possível personalizar facilmente os fragmentos do Formulário adaptável e seus campos no editor de Formulário adaptável.


**Recurso obsoleto**

* O AtiveMQ no AEM está obsoleto. O AtiveMQ foi usado para comunicação entre duas instâncias de publicação do AEM. A Adobe recomenda que os clientes agora usem um balanceador de carga.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correção de problemas no Service Pack 19 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### Acessibilidade{#sites-accessibility-6519}

* Em uma página do AEM Sites, ao ampliar em 200% a página, os links **[!UICONTROL Cópia de idioma]** e **[!UICONTROL Relatório CSV]** no painel Referências desaparecem. (SITES-11011)

#### Interface do usuário do administrador{#sites-adminui-6519}

* Canal do AEM Screens **[!UICONTROL Visualizar]** A funcionalidade do não funciona ou é exibida no Painel. (SITES-15730)
* Durante uma operação de movimentação de página, se a interface do usuário não puder exibir as referências, mas indicar que elas são automaticamente republicadas, elas serão *não* republicado. (SITES-16435)
* No AEM 6.5 com Service Pack 16 ou 17, quando estiver na exibição em lista de sites com a coluna &quot;Fluxo de trabalho&quot; ativada, você não poderá classificar a lista com base nos itens dessa coluna. Não ocorre classificação. (SITES-15385)
* Para um modelo de página de redirecionamento, o campo de redirecionamento se tornou obrigatório. No entanto, a validação do campo obrigatório não é aplicada nem funciona nesses dois cenários: quando uma página é criada sem um valor de redirecionamento obrigatório, o não pode criar uma página de redirecionamento. A validação não funciona ao navegar usando atalhos de teclado e quando o campo é marcado como inválido, ela não continua. (SITES-15903)
* Alguns **Links de entrada** não estavam sendo incluídos na contagem exibida no **Referências** painel. Por exemplo, o painel estava sendo exibido **Links de entrada (6)** mas na verdade havia nove links recebidos. (SITES-14816)

#### IU Clássica{#sites-classicui-6519}

* Depois de instalar o hotfix no SITES-15827, os títulos da caixa de diálogo que tinham espaço em branco entre as palavras eram substituídos por `" "`. Quebras de linha também foram removidas. (SITES-16089)
* Os títulos da caixa de diálogo codificados agora resultam em uma codificação dupla do título. (SITES-15841)
* A atualização de servidores AEM do service pack 6.5.16 para 6.5.17 resultou em uma codificação dupla dos títulos da caixa de diálogo da interface clássica. (SITES-15634)

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* Uma mensagem de erro interno do servidor é exibida no Editor de fragmento de conteúdo. (SITES-13550)
* A atualização do `org.json` biblioteca por meio do NPR-41291 causou conversões de erros de dados no `DefaultDataTypeConverter` do `cfm-impl` pacote. A conversão do tipo de dados deve ser mais flexível. (SITES-16473)
* Ao receber a mensagem pop-up de erro, &quot;Esta versão do fragmento de conteúdo não pode ser comparada com a versão atual devido ao conteúdo incompatível&quot;. Os fragmentos de conteúdo devem ser comparáveis, mas não são. (SITES-16317)
* Alteração do URL JS do seletor de ativos de
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
para
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068)
* Adapte o novo esquema de resposta da API de metadados Polaris para a integração CFM-Polaris. (SITES-15166)
* Todos os fragmentos de conteúdo devem ser listados onde o fragmento de conteúdo selecionado é referenciado. Em vez disso, as referências de ativo no painel de referência do fragmento de conteúdo mostram 0 (zero) referências. (SITES-15036)

#### Infraestrutura principal{#sites-core-backend-6519}

* Melhorar `StyleImpl`. (SITES-15164)
* Melhore a ramificação release/650 do pipeline do WCM para poder executar testes de integração para seus módulos. (SITES-12938)

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Integração do Campaign{#sites-campaign-integration-6519}

* No componente de assinatura (`/apps/fpl/components/campaign/signature`), o link Externalizer não estava funcionando. O domínio não estava sendo anexado à fonte da imagem se o comentário HTML acima da tag da imagem fosse removido. Esse problema foi encontrado somente com o componente de assinatura no ambiente de produção, não no ambiente de preparo. (SITES-16120)

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### Componentes de base (herdados){#sites-foundation-components-legacy-6519}

* O componente de Pesquisa do Sites do Adobe Experience Manager (AEM) interrompe a interface do usuário. (SITES-15087)

#### Editor de consultas GraphQL{#sites-graphql-query-editor-6519}

* A interface do usuário do Editor do GraphQL não permite percorrer todas as consultas persistentes quando há um número alto de consultas (por exemplo, mais de 25). (SITES-16008)
* O Editor do GraphQL não está salvando o status de publicação de consultas persistentes. O botão Cancelar publicação é exibido no Editor do GraphQL, mas o ícone que indica que a consulta persistente foi publicada não é exibido. Atualizar a página mostra que a consulta persistente nem mesmo foi publicada. (SITES-15858)

#### Lançamentos{#sites-launches-6519}

* As alterações no repositório não são salvas devido a `Oak0001` entra em conflito quando várias páginas estão sendo editadas ou o conteúdo está sendo criado. É normal executar uma nova tentativa em tal evento, mas isso não ocorre. (SITES-14840)

#### MSM - Live Copies{#sites-msm-live-copies-6519}

* O botão Implantação do MSM não funciona na interface gráfica do usuário de toque. (SITES-16991)
* A referência de link não é atualizada no Fragmento de experiência ao criar uma live copy ou implantar um Fragmento de experiência. (SITES-15460)

#### Editor de página{#sites-pageeditor-6519}

* Em Forms > Temas, se você tiver aberto um tema no editor de temas, feito algumas alterações e salvo e, em seguida, clicar em Visualizar, um ícone de carregamento ficará visível, mas a visualização real não carregará. (SITES-17164)
* A seleção de vários tipos de arquivo de documento no filtro de tipo de ativo não funciona no console de páginas. Nenhum resultado é encontrado mesmo se os resultados de um tipo de arquivo específico estiverem disponíveis. Como resultado, os autores não conseguem filtrar vários documentos. Eles devem usar vários tipos de documentos e precisam filtrá-los um de cada vez. (SITES-14047)
* Depois de atualizar uma instância do AEM 6.5.17 e do AEM 6.5.18, de dentro do Editor de páginas, se você selecionou **[!UICONTROL Publicar página]**, você será redirecionado para um URL que não existe. O usuário deve ser redirecionado para o Assistente de publicação. (SITES-15856)
* Cópia redundante da área de transferência AEM durante uma colagem da área de transferência do sistema operacional. (SITES-15704)
* No Assets, seleção **[!UICONTROL Documentos]**, depois em **[!UICONTROL Filtertype]**, selecionando **[!UICONTROL Microsoft® Word]** ou **[!UICONTROL Microsoft® Excel]** O não mostra resultados mesmo se houver arquivos de ambos os tipos. (SITES-14837)

### [!DNL Assets]{#assets-6519}

* Ao criar ou salvar uma pasta pública, três grupos são criados em um painel de administração. (ASSETS-26700)
* Não foi possível diferenciar os ativos de publicação no Experience Manager ou Brand Portal. (NPR-41320)
* No painel de pesquisa, ao marcar caixas de seleção e desmarcar qualquer uma delas, todas as caixas de seleção serão desmarcadas. (ASSETS-26377)

#### [!DNL Dynamic Media]{#assets-dm-6519}

* Depois que um ativo é carregado para AEM, a variável `update_asset` fluxo de trabalho é acionado. O fluxo de trabalho nunca é concluído. Ao examinar as instâncias de fluxo de trabalho, o fluxo de trabalho é concluído até a etapa de carregamento do produto. A próxima etapa é o upload em lote do Scene7. O usuário pode ver que o ativo está no Scene7 no aplicativo Dynamic Media Classic. (ASSETS-30443)
* Um Servlet personalizado (endpoint da API) está retornando um nome de arquivo Dynamic Media (Scene7) incorreto. Isso ocorre quando um ativo é excluído e substituído por um ativo com o mesmo nome. O servlet personalizado retorna o nome de arquivo antigo do Dynamic Media (Scene7), enquanto uma chamada de API &quot;jcr&quot; retorna o nome de arquivo correto. (ASSETS-29476)
* Mesmo depois que a Sincronização está desativada no nível da Pasta, os Logs mostram o acionador de &quot;Scene7 ReplicateOnModifyListener&quot;. A variável `ReplicateOnModifyListener/Worker` O deve ignorar o processamento de ativos de pastas e fragmentos de conteúdo que não sejam da Dynamic Media. (ASSETS-26705)
* As pessoas com pouca visão serão afetadas se o Foco não estiver visível nos elementos suspensos (Somente conteúdo, Exibir, Mais opções) nos modos de alto contraste em preto-e-branco. (ASSETS-25759)
* As pessoas com pouca visão serão afetadas se a taxa de contraste de luminosidade do texto em uma página for menor que 4.5:1. (ASSETS-25756)
* Os leitores de tela não estão narrando a mensagem pop-up exibida após o envio dos dados. (ASSETS-25755)
* Os leitores de tela não estão reconhecendo marcos na página (Dynamic Media; criando um perfil de codificação de vídeo), quando navegados usando a tecla de atalho de ponto de referência/região `D/R`. (ASSETS-25752)
* Os leitores de tela não estão reconhecendo vários pontos de referência na página (Dynamic Media; criando vídeo interativo) quando navegam usando a tecla de atalho de ponto de referência/região `D/R`. (ASSETS-25750)
* Os leitores de tela (NVDA/JAWS/Narrador) não estão reconhecendo os pontos de referência no **Editar ativo** página ao navegar usando as teclas de atalho `D/R`. (ASSETS-25744)
* O usuário recebe uma mensagem de trabalho assíncrono vazia/falsa, mas o ativo conectado foi publicado com êxito. (ASSETS-29342)

### [!DNL Forms]{#forms-6519}

#### [!DNL Adaptive Forms]

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.19.0 Forms add-on package release is scheduled for Thursday, November 30, 2023. A list of Forms fixes and enhancements would be added to this section post the release.-->

<!--* Adding Access Control List for `fd-cloudservice` user to be able to read or update the Microsoft&reg; configurations under `cloudconfigs/microsoftoffice`. (FORMS-11142) -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

* Quando um usuário adiciona uma barra de ferramentas ao Formulário adaptável, o Rótulo do contêiner de formulário mostra um comportamento irregular, pois não altera para o idioma preferencial que o Autor selecionou para o Forms. (FORMS-11371)
* No AEM Forms Workspace, o campo suspenso seleciona a primeira opção por padrão na interface do usuário. (FORMS-11346)
* A configuração de idioma no AEM não terá nenhum efeito se você usar localidades com cinco caracteres e o separador decimal não for renderizado corretamente na letra. (FORMS-11344)
* Quando um usuário gera a saída XML usando o processo do Workbench, ela falha em alguns dos arquivos. (FORMS-11314)
* Quando um usuário gera a pré-visualização do Documento de registro (DOR) em idiomas diferentes do inglês, ele não funciona. (FORMS-11106)
* Quando um usuário converte alguns arquivos de imagem com PDFG em uma instância OSGI baseada no Linux com JDK11, ele não converte. (FORMS-11105)
* Quando o usuário instala o complemento AEM Forms, ele quebra o painel da árvore de conteúdo no AEM Sites. (FORMS-10912)
* Quando um usuário copia datas usando o leitor de tela NVDA do componente Seletor de datas, ele não lê corretamente. (FORMS-10805) 
* No editor de regras do Forms, o usuário não pode definir o valor do botão de opção/caixa de seleção quando o tipo de valor de dados é Booleano. (FORMS-10713)
* Quando um usuário adiciona itens adicionados em um Formulário adaptável, ele é adicionado em ordem inversa a uma lista suspensa. (FORMS-10456)
* Quando uma lista suspensa é limpa usando o editor de regras, o primeiro valor fornecido ainda aparece mesmo que o valor tenha sido limpo. (FORMS-9963) 
* Os usuários não podem acessar o Título do formulário usando leitores de tela como o NVDA. (FORMS-8815) 
* Os usuários não podem acessar o Subtítulo em um Formulário usando leitores de tela, como o NVDA. (FORMS-8814) 
* Na fonte da página do formulário html, o atributo da chave de acesso está vazio e não funciona. (FORMS-5753) 
* Na caixa de diálogo Sobre o Workspace, o texto &quot;Adobe Experience Manager - Forms&quot; é apresentado como texto. (FORMS-5748)

#### [!DNL Forms Designer]{#forms-designer-6519}

* Quando um usuário tenta ler PDF forms não interativos por meio de leitores de tela, alguns itens da lista não são lidos ou ignorados. (LC-3921645) 
* Quando um usuário navega pelos campos editáveis, ele não atravessa todos os campos de formulário de PDF de forma consistente. (LC-3921631) 
* A ordenação das tags é alterada aleatoriamente na marcação PDF, mesmo que esteja correto no Forms Designer. (LC-3921313) 
* Uma lista não é exibida corretamente nas tags na Adobe Acrobat Reader ou no Adobe Acrobat DC. (LC-3921306)
* Os níveis de cabeçalho atribuídos corretamente no Forms Designer são alterados aleatoriamente para uma `<P>` no Adobe Acrobat. (LC-3921305) 
* Em uma tabela, a ID de qualquer objeto não pode ser modificada depois de atribuída. (LC-3921134) 
* Se as células mescladas estiverem na tabela, nenhuma GUI estará disponível para definir o span (linha e coluna) e o escopo em uma tabela complexa no AEM Forms Designer. (LC-3919532) 

### Foundation{#foundation-6519}

* Criar uma cópia de idioma no nível da raiz de idioma não ajusta caminhos na página. No caso em que a cópia de idioma foi criada, não para a raiz de idioma, mas para as páginas sob ela, o caminho foi alterado corretamente. (NPR-41364)
* A dica de ferramenta &quot;Apresentação em Data Relativa&quot; só pode ser fechada pressionando Escape (ESC) no teclado. A dica de ferramenta deve ser fechada quando o usuário selecionar qualquer parte da interface. (NPR-41394)
* String não localizada `Something went wrong while adding the private key.` ao adicionar o arquivo de chave privada incorreto no **Editar Usuário** > **Armazenamento de chaves**. (NPR-41366)
* Os ícones são necessários para o Microsoft® SharePoint e o Microsoft® One Drive no ambiente do AEM 6.5. (NPR-41354)
* &quot;Incompatibilidade de UserId/Password&quot; deslocalizada. sequência de caracteres em **Segurança** > **Usuário** > **Criar** caixa de diálogo. (NPR-41245)
* O código Popover e os manipuladores de eventos são carregados duas vezes, quebrando as interfaces de usuário baseadas no Coral3 criadas pelo usuário. (NPR-41171)
* O cancelamento da seleção não funciona corretamente depois de usar &quot;Selecionar tudo&quot; no console do AEM Sites. (NPR-41304)

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### Integrações{#integrations-6519}

* Os links de SMS em uma campanha de email do AEM não são gravados corretamente; eles contêm um elemento de âncora HTML. (NPR-41211)
* O texto usado na tela de configuração da conta não deve usar o novo tipo de credencial. (NPR-41210)
* Mover o programador de importação de relatórios do Analytics de `ManagedPollConfig` para sling jobs. Quando duas estruturas de análise diferentes foram anexadas com conjuntos de relatórios diferentes a dois sites diferentes, `ManagedPollConfig` pesquisa apenas um deles. (NPR-41209)
* Quando o valor é redefinido para o padrão, o botão de período selecionado anteriormente permanece ativado. No painel de insight de conteúdo do AEM, por padrão, o período de tempo é definido na semana e mostra insights de conteúdo como dados semanais. Agora, se o usuário selecionar outras opções de intervalo de tempo, como hora, dia, mês e ano, os dados serão alterados de acordo com o valor selecionado. No entanto, se os valores forem redefinidos, por padrão, o intervalo de tempo visível é a semana, mas ainda a opção de intervalo de tempo selecionado anteriormente será selecionada. (NPR-41246)

#### Oak{#oak-6519}

* Utilitário de backport para limitar a taxa de gravações para AEM caso a indexação assíncrona esteja atrasada. (NPR-40985)

#### Platform{#foundation-platform-6519}

* Consultas do QueryBuilder com colchetes são traduzidas incorretamente para xpath . (NPR-41298)

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### Projetos de tradução{#foundation-translation-6519}

* Ao criar a cópia de idioma da página &quot;A&quot;, ele deve criar automaticamente as cópias de idioma das páginas, fragmentos de experiência, fragmentos de conteúdo e ativos referenciados. Além disso, a cópia de idioma recém-criada da página &quot;A&quot; no novo caminho deve ter suas referências atualizadas para as respectivas cópias de idioma recém-criadas das páginas, Fragmentos de experiência, Fragmentos de conteúdo e Ativos. (NPR-41076)

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### Fluxo de trabalho{#foundation-workflow-6519}

* Não é possível concluir uma tarefa na Caixa de entrada. Somente um valor &quot;indefinido&quot; é observado no menu suspenso ao tentar concluir a tarefa e selecionar uma ação. Isso significa que os usuários não podem aplicar o service pack AEM 6.5.18. (NPR-41402 e NPR-41473)
* Não é possível concluir tarefas na Caixa de entrada. Não há valor (apenas &quot;indefinido&quot;) na lista suspensa ao tentar concluir a tarefa para arquivos zip, relatórios de ativos, mover (sucesso ou falha) ou expiração de ativos. (NPR-41305)
* Quando um usuário seleciona **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > instâncias, seleciona o fluxo de trabalho em execução e selecione **[!UICONTROL Exibir carga]**, isso resulta em uma página de erro 500. (NPR-41325)

## Instalar [!DNL Experience Manager] 6.5.19.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] O 6.5.19.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do pacote de serviços está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.19.0 em uma das instâncias do Autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda que você remova ou desinstale o [!DNL Experience Manager] 6.5.19.0 pacote. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-la. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o pacote de serviços em [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.

1. Baixe o pacote de serviços de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, um diálogo na interface do usuário do Gerenciador de pacotes é fechado durante a instalação do pacote de serviços. A Adobe recomenda que você aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que a instalação será bem-sucedida. Normalmente, esse problema ocorre no [!DNL Safari] navegador, mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL Experience Manager] 6.5.19.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.19.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.19.0)` em [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` O é versão 1.22.17 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar o Service Pack do [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o pacote de serviços no Experience Manager Forms, consulte [Instruções de instalação do Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>O recurso de formulários adaptáveis, disponível no [Início rápido do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=pt-BR), foi projetado apenas para fins de exploração e avaliação. Para usá-lo na produção, é essencial obter uma licença válida para o AEM Forms, pois a funcionalidade de formulários adaptáveis requer uma licença adequada.

### Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager{#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [Fragmento de conteúdo do Experience Manager com pacote de índice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam.

A falha na instalação deste pacote pode resultar em consultas lentas ou com falha do GraphQL.

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar{#uber-jar}

O UberJar para [!DNL Experience Manager] O 6.5.19.0 está disponível na [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Então, não há `classifier`, com `apis` como o valor, para o `dependency` tag.

## Recursos obsoletos e removidos{#removed-deprecated-features}

Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md/).

## Problemas conhecidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



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

   1. Exclua as duas pastas a seguir de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale o Service Pack ou reinicie o Experience Manager as a Cloud Service.
Novas pastas de `cache` e `diff-cache` são criadas automaticamente e você não enfrenta mais uma exceção relacionada ao `mvstore` no `error.log`.

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Uma consulta do GraphQL pode usar o `damAssetLucene` índice em vez de `fragments` índice. Essa ação pode resultar em consultas GraphQL que falham ou demorar muito para ser executada.

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

  Depois que a definição do índice é alterada, é necessária uma reindexação (`reindex` = `true`).

  Após essas etapas, as consultas do GraphQL devem ser executadas mais rapidamente.

* Ao tentar mover, excluir ou publicar fragmentos de conteúdo, sites ou páginas, há um problema quando as referências de fragmento de conteúdo são buscadas, já que a consulta em segundo plano falha. Ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se você atualizar seu [!DNL Experience Manager] 6.5.0 - 6.5.4 para o pacote de serviços mais recente no Java™ 11, você verá `RRD4JReporter` exceções na `error.log` arquivo. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada no [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado no [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usar a API do Target Standard (autenticação IMS) e, em seguida, exportar os Fragmentos de experiência para o Target resulta na criação de tipos de oferta errados. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão não registrada da alteração de registro.

* A partir do AEM 6.5.15, o mecanismo Rhino JavaScript fornecido pelo ```org.apache.servicemix.bundles.rhino``` tem um novo comportamento de elevação. Scripts que usam o modo estrito (```use strict;```) precisam declarar corretamente as variáveis, caso contrário, elas não serão executadas, gerando um erro de tempo de execução.

### Problemas conhecidos do AEM Forms

#### Plataformas compatíveis

* O JDK 11.0.20 não é compatível com a instalação do AEM Forms no instalador do JEE. Somente o JDK 11.0.19 ou versões anteriores são compatíveis com a instalação do AEM Forms no instalador do JEE. (FORMS-10659)

#### Instalação

* Na plataforma JBoss® 7.1.4, quando o usuário instala o Experience Manager 6.5.16.0 ou o service pack posterior, `adobe-livecycle-jboss.ear` falha na implantação. (CQ-4351522, CQDOC-20159)
* Depois de atualizar para o ambiente do instalador completo do AEM Forms 6.5.18.0 JBoss® Turnkey no Windows Server 2022, ao compilar o código do aplicativo cliente de saída usando o Java™ 11, o seguinte erro de compilação pode ocorrer:

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  Para resolver o problema, execute as seguintes etapas:
   1. Navegue até `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` e descompactar `adobe-output-client.jar` para extrair o `Manifest.mf` arquivo.
   1. Atualize o `Manifest.mf` arquivo removendo a entrada `${clover.jar.name}` do atributo class-path.

      >[!NOTE]
      >
      > Também é possível usar uma ferramenta de edição no local, por exemplo, 7-zip, para atualizar a `Manifest.mf` arquivo.

   1. Salve o atualizado o `Manifest.mf` no `adobe-output-client.jar` arquivo.
   1. Salvar os modificados `adobe-output-client.jar` e execute novamente a configuração. (CQDOC-20878)
* Após instalar o instalador completo do AEM Service Pack 6.5.19.0, a implantação do EAR falha no JEE usando o JBoss® Turnkey.
Para resolver o problema, localize o `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` arquivo e atualização `Adobe_Adobe_JAVA_HOME` para `Adobe_JAVA_HOME` para todas as ocorrências antes de executar o gerenciador de configurações. (CQDOC-20803)

#### Instalar o fragmento do servlet (AEM Service Pack 6.5.14.0 ou anterior)

* Se você estiver atualizando para o AEM Service Pack 6.5.15.0 ou superior e sua instância AEM estiver operando no Tomcat 8.5.88, é obrigatório instalar o fragmento de servlet *antes* você continua com a instalação do Service Pack 6.5.15.0 ou superior.
* É obrigatório instalar o fragmento de servlet para todos os servidores de aplicações, exceto aqueles executados no JBoss® EAP 7.4.0.

**Para instalar o fragmento de servlet:**

1. Baixe o fragmento do servlet de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Inicie o servidor de aplicativos.
1. Aguarde os registros estabilizarem e verifique o estado do pacote.
1. Abra os Pacotes de console da Web. O URL padrão é `http://[Server]:[Port]/system/console/bundles`.
1. Selecionar **[!UICONTROL Instalar]** ou **[!UICONTROL Atualizar]**.
1. Selecionar o fragmento baixado
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Selecionar **[!UICONTROL Instalar]** ou **[!UICONTROL Atualizar]**.
1. Aguarde o servidor de aplicativos estabilizar.
1. Interrompa o servidor de aplicativos.

#### Adaptive Forms

* Quando um Formulário adaptável é publicado, todas as suas dependências, incluindo políticas, são republicadas, mesmo que nenhuma modificação tenha sido feita nelas. (FORMS-10454)
* Quando um usuário opta por configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar algum outro campo do Formulário adaptável no mesmo editor resolve o problema.
* Quando os usuários executam a ação de envio, o envio falha com um erro:
  ` javax.servlet.ServletException: java.lang.NoSuchMethodError`
Para resolver o problema, [recompile os scripts do Sling, como JSP, Java e Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=en#resolution). (FORMS-8542)


## Pacotes OSGi e pacotes de conteúdo incluídos{#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos em [!DNL Experience Manager] 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.19.0](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos no Experience Manager 6.5.19.0](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos{#restricted-sites}

Esses sites só estão disponíveis para clientes do. Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta da Adobe.

* [Download do produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscrever-se para obter atualizações de produtos de prioridade Adobe](https://www.adobe.com/subscription/priority-product-update.html)
