---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista detalhada de alterações para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: a27e460a19d3f986ee87b33263b8db1e45897497
workflow-type: tm+mt
source-wordcount: '4036'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5 Notas de versão mais recentes do Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | 24 de novembro de 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] O 6.5.15.0 inclui novos recursos, principais melhorias solicitadas pelo cliente, correções de bugs e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este service pack](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Se a movimentação de um ativo no Experience Manager falhar, o ativo ainda poderá ser renomeado. (NPR-38753)
* Ao visualizar os ativos em uma [!UICONTROL Exibição de lista], alguns dos títulos estão faltando. (CQ-4345746)
* O leitor de tela não anuncia o submenu do [!UICONTROL Relacionar] na guia Básico na página Propriedades de ativos . (ATIVO-6938)
* O leitor de tela detecta incorretamente os ícones de pasta na página Navegação de ativos com a lista de pastas. (ATIVO-6936)
* Ao copiar uma coleção, a imagem não apresenta um campo vazio `alt` attribute ou role=&quot;presentation&quot;. Como resultado, a imagem é exposta aos usuários de leitores de tela. (ATIVO-6932)
* O texto exibido ao anotar um ativo não tem um 4:5:1 relação de contraste em comparação com a cor do plano de fundo. (ATIVO-6931)
* Na guia IPTC da página de propriedades do ativo, ao ajustar a largura da página, o conteúdo da página não se ajusta corretamente e resulta na rolagem horizontal. (ATIVO-6929)
* Ao filtrar ativos, o texto do filtro na [!UICONTROL min] e [!UICONTROL max] os campos desaparecem depois que um valor é inserido. (ATIVO-6925)
* Em Experience Manager Collections, o leitor de tela não anuncia a variável [!UICONTROL email] na tela Download. (ATIVO-6923)
* Um texto alternativo está ausente ao anotar os elementos. (ATIVO-6922)
* Se o texto for escrito em Horas e Minutos no campo do seletor de datas, nenhuma mensagem de erro de texto será exibida. O erro só é identificado usando a cor vermelha. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* O texto alternativo em `[role='img']` no filtro Arquivos está ausente. (ATIVO-6919)
* Anúncio incorreto do leitor de tela para o [!UICONTROL Criar] submenu. (ATIVO-6916)
* Em Experience Manager Collections, o botão remover `X` não tem texto para anunciar para os leitores de tela. (ATIVO-6912)
* Ao usar o Analisador de contraste de cores no Experience Manager, não há diferenciação de cores entre a data atual e a data escolhida no seletor de datas do widget de calendário. Ele não tem pelo menos 3:1 de relação de contraste em relação às cores adjacentes. (ATIVO-6911)
* Em Arquivos do Experience Manager, ao selecionar uma das opções de [!UICONTROL Agendamento] botão de opção em Gerenciar publicação, o nome e o estado das opções do botão de opção são anunciados pelo leitor de tela. No entanto, a variável **Agendamento** não é anunciada. (ASSETS-6908, ASSETS-6906)
* O texto alternativo está ausente no ícone Classificar . (ATIVO-6904)
* Na página Propriedades do ativo , o nome do campo `Person` na guia Extensão IPTC, as etiquetas não são anunciadas pelos leitores de tela. O leitor de tela só anuncia um campo editável e atualmente em branco, mas não o nome do rótulo. (ASSETS-6903, ASSETS-6848)
* A ferramenta de anotação não pode ser exibida usando o teclado. Um mouse é usado para desenhar uma imagem para exibir a ferramenta Anotar. (ATIVO-6899)
* Em Experience Manager Collections, um campo vazio no **Avançado** exibe uma relação de contraste incorreta entre o limite e a cor adjacente. (ATIVO-6895)
* Valores de atributo ARIA incorretos para alguns dos elementos ao editar ativos. (ATIVO-6894)
* O leitor de tela não identifica corretamente o cabeçalho ao criar um fluxo de trabalho. (ATIVO-6892)
* Ao copiar uma coleção, o botão remover imagem do SVG `X` com role=&quot;img&quot; está faltando um role=&quot;presentation&quot;. Como resultado, a imagem é exposta aos usuários de leitores de tela. (ATIVO-6890)
* No **Básico** das propriedades do Ativo, o leitor de tela não anuncia apropriadamente o estado de expansão ou recolhimento do campo Tags. (ATIVO-6889)
* O **Básico** em Propriedades de ativos contém páginas com ID duplicada. (ASSETS-6888)
* O rótulo do campo de texto para definir um título ao criar um fluxo de trabalho desaparece quando você especifica um valor na caixa de texto. (ATIVO-6887)
* A lista de recipients ao compartilhar um link é exibida como uma tabela de dados com cabeçalhos, mas não é semanticamente identificada como uma tabela de dados para os usuários de leitores de tela. (ATIVO-6886)
* Nenhuma mensagem de erro para representar um campo vazio é exibida em `Add Email Address` campo. O erro é representado apenas usando uma cor. (ASSETS-6885, ASSETS-6843)
* Os textos de espaço reservado, Caminho e Texto alternativo não têm pelo menos uma relação de contraste de 4.5:1 em comparação com a cor de fundo. (ASSETS-6884, ASSETS-6865)
* Valores inválidos para alguns dos atributos ARIA ao salvar uma coleção inteligente. (ASSETS-6882)
* Quando você salva uma coleção inteligente, alguns dos rótulos não são associados adequadamente ao leitor de tela. (ASSETS-6881)
* Na guia IPTC das propriedades do Ativo, o leitor de tela não anuncia o rótulo dos campos de formulário de palavra-chave. (ATIVO-6879)
* Em Experience Manager Collections, a variável [!UICONTROL Email] não é identificado como um campo obrigatório e nenhuma mensagem de erro será exibida se um valor não for especificado. (ATIVO-6877)
* Nos arquivos do Experience Manager, nenhuma mensagem de erro em **Compartilhamento de link** é exibida em `Add Email Address`. O erro só é identificado no uso de uma cor. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL Cortar e mapear] opções não têm os nomes programáticos ao editar um ativo. (ATIVO-6874)
* O texto do filtro não tem uma proporção de contrato 4.5:1 em comparação à cor de fundo. (ATIVO-6873)
* O texto para o nome da pasta na página de navegação principal não tem uma relação de contraste de 4.5:1 em comparação com a cor de fundo. (ATIVO-6872)
* Ao executar a variável [!UICONTROL Copiar] para Coleções, a **[!UICONTROL Adicionar usuário]** o controle de formulário da caixa de combinação não está associado corretamente ao rótulo visível. (ATIVO-6870)
* O leitor de tela não anuncia o [!UICONTROL Criar] opções de submenu de botões. (ATIVO-6869)
* As opções Escopo, Fluxos de trabalho e Fuso horário não têm uma relação de contraste de 4.5:1 em comparação com a cor do fundo. (ASSETS-6868)
* O leitor de tela anuncia incorretamente o estado de recolhimento do **Linha do tempo** coluna. (ATIVO-6864)
* Elementos filho ausentes para algumas das funções ARIA ao salvar uma coleção inteligente. (ATIVO-6862)
* Ao compartilhar um ativo, os atributos ARIA necessários para `Search/Add Email Address` campo não especificado. (ASSETS-6860)
* O **mapa** não é possível exibir a caixa de diálogo usando o teclado. Em vez disso, é necessário um clique do mouse para exibir a caixa de diálogo do mapa. (ATIVO-6859)
* Elementos filho ausentes para algumas das funções ARIA na guia Básico da página Propriedades do ativo . (ATIVO-6858)
* Os campos de entrada de texto vazios, disponíveis na guia IPTC das propriedades do Ativo, não têm uma relação de contraste de 3:1 em comparação às cores adjacentes. (ASSETS-6854, ASSETS-6847)
* Os ícones de perfil no **Linha do tempo** são detectadas incorretamente pelos leitores de tela. (ATIVO-6850)
* O leitor de tela não anuncia que a caixa de combinação Revisar status , disponível na guia Básico das propriedades do ativo, é um campo somente leitura. (ATIVO-6849)
* O leitor de tela não anuncia o rótulo das caixas de seleção Selecionar tudo e anotação apropriadamente. (ATIVO-6846)
* O foco do teclado ignora o `About Adobe Experience Manager` disponível na **Mostrar ajuda** menu. (ATIVO-6845)
* Os leitores de tela não anunciam corretamente as pastas selecionadas ao navegar pela lista de pastas usando as teclas de seta do teclado na exibição de Cartão. (ATIVO-6844)
* Ao fazer o upload de um PDF para o Experience Manager, o uso da memória aumenta constantemente. (ATIVO-16889)
* Quando um fluxo de trabalho converte um arquivo .ZIP em um nome de pasta no Assets, ele não retém o uso do nome do arquivo .ZIP. (ATIVO-16712)
* Ao alternar do Brand Portal para o Experience Manager 6.5, o filtro de predicado do usuário não exibe os resultados apropriados quando você aplica o filtro pela primeira vez. (ATIVO-15932)
* Não é possível anotar um vídeo. (ATIVO-15217)
* **Gerenciar publicação** desaparece para um usuário sem acesso replicado e `READ` e `WRITE` acesso a `ETC` e `VAR`. (ATIVO-15007)
* O tempo de carregamento da página de propriedades aumenta para um ativo com várias referências. (ATIVO-14182)
* Quando uma imagem não é publicada no Brand Portal, o Experience Manager também a desmarca do Dynamic Media e, como resultado, não há imagem exibida no site ativo. (ATIVO-14118)
* Problemas de XSS em cartões Smart Crop no Dynamic Media. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* Problema XSS nas Predefinições do visualizador no Dynamic Media. (ATIVO-13822)
* Valide o acesso do usuário ao visualizar ativos do DM no AEM. (CQ-4314757)


## Commerce {#commerce-6515}

* Falha na criação de uma página de loja, parando o processo geral de implementação do catálogo. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### Principais recursos {#keyfeatures}

* O AEM Forms Designer agora está disponível em [Localidade espanhola](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). (LC-3920051)
* Agora você pode usar [OAuth2 para autenticar com protocolos de servidor de e-mail do Microsoft® Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* Você pode definir [Revalidar no servidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) para true para identificar os campos ocultos para exclusão de um Documento de registro no lado do servidor. (NPR-38149)
* O AEM Forms Designer requer a versão de 32 bits do Visual C++ 2019 Redistribuível (x86).  (NPR-36690)

### Correções {#fixes}

* Quando a propriedade data-disabled de um formulário adaptável é alternada, a aparência dos grupos de botões de opção e caixas de seleção não muda. (NPR-39368)
* Quando um formulário adaptável é traduzido, algumas traduções são perdidas e não são exibidas corretamente. (NPR-39367)
* Quando a propriedade de uma página é definida como oculta, a página não é removida do conjunto de formulários. (NPR-39325)
* Em um Documento de registro, a seção de nota de rodapé dinâmica no final da página não está presente. (NPR-39322)
* Quando um Documento de registro é gerado para um formulário adaptável, somente o alinhamento vertical é permitido para botões de opção e caixas de seleção. O usuário não pode definir o alinhamento horizontal de botões de opção e caixas de seleção. (NPR-39321)
* Depois de implantar o Gerenciamento de correspondência, se vários usuários tentarem acessar um formulário, org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentialLanguageRoots se tornará um gargalo e a maioria dos threads será atingida. Muitas vezes, várias solicitações de página de formulários demoravam mais de 1 minuto para carregar cada, mesmo quando o servidor tinha uma carga muito baixa. (NPR-39176, CQ-4347710)
* Em um formulário adaptável, quando você usa um campo Rich Text em um fragmento de formulário adaptável carregado lentamente, alguns dos seguintes erros são sentidos:
   * Não é possível editar o conteúdo nem anexar nada ao campo Rich Text .
   * O padrão de exibição aplicado ao rich text não é respeitado. 
   * A mensagem de erro para o comprimento mínimo do campo não é exibida ao enviar o formulário.
   * O conteúdo desse campo rich text é incluído várias vezes no submit-XML produzido. (NPR-39168)
* Quando a opção Seletor de data é usada em um formulário adaptável, ele falha ao converter o valor no formato correto. (NPR-39156)
* Ao visualizar um formulário adaptável como um formulário HTML, ele não é renderizado corretamente, pois alguns dos subformulários se sobrepõem ao formulário pai. (NPR-39046)
* Se o painel tiver uma tabela oculta e o formulário adaptável for renderizado usando a exibição em tabelas, os campos na primeira guia não serão exibidos corretamente. (NPR-39025)
* O `Body` está ausente para o modelo OOTB (pronto para uso). (NPR-39022)
* O Documento de registro não é gerado no idioma do Formulário adaptável. É sempre gerada em inglês. (NPR-39020)
* Quando um formulário adaptável tem vários painéis e alguns desses painéis usam o formulário pronto para uso **Anexo de arquivo** componente, o `Error occurred while draft saving` ocorre . (NPR-38978)
* When `=` o sinal é usado nos campos caixa de seleção, lista suspensa ou botão de opção de um formulário adaptável e o documento de registro é gerado, então `=` não está visível no Documento de registro gerado.(NPR-38859)
* Há um aumento múltiplo no número de erros de processamento em lote de avisos após a atualização do service pack 6.5.11.0. (NPR-39636)
* Quando você não fornece dados de teste, as cartas de Gerenciamento de correspondência não são carregadas na interface do usuário do agente. (CQ-4348702)
* Quando o usuário aplica o AEM Forms Service Pack 14 (SP14) do AEM Forms implantado com o IBM® WebSphere®, o bootstrapping falha ao inicializar um banco de dados e o `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` ocorre.(NPR-39414)
* Em um Formulário AEM no servidor OSGi, ao usar a API do Serviço de documento para certificar o PDF, ele falha com o erro: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311-003. (NPR-38855)
* Quando o usuário tenta usar o serviço wrapper para renderizar cartas com o AEM 6.3 Forms, a variável `java.lang.reflect.UndeclaredThrowableException` ocorre. (CQ-4347259)
* Quando um XDP é renderizado como formulário HTML5, o conteúdo da página principal é renderizado primeiro, independentemente do posicionamento dos objetos em um formulário adaptável. (CQ-4345218)
* A configuração do aplicativo no servidor de destino muda para as configurações definidas no servidor de origem, mesmo que a variável **Substituir configuração quando a importação estiver concluída** não está marcada no momento da importação do aplicativo. (NPR-39044)
* Quando um usuário tenta atualizar a configuração do conector usando o Configuration Manager, ele falha.(CQ-4347077)
* Quando o usuário tenta executar um Formulário AEM no patch JEE após alterar a senha padrão do usuário administrador, uma exceção `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` ocorre. (CQ-4348277)
* No AEM Designer, campos de formulário sem legendas são colocados em células de tabela, incluindo caixas de seleção.(LC-3920410)
* Quando o usuário tenta abrir a Ajuda no AEM Forms Designer, ela não é exibida corretamente. (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* O console Lançamentos do Experience Manager Sites estava em branco. (NPR-39188)
* As referências não eram ajustadas quando a página que tinha a referência também precisava ser ativada durante a movimentação da página. (NPR-39061)
* Quando um contêiner de Layout é desoculto usando um contêiner pai, as alterações de layout não são aplicadas a todos os componentes dentro do contêiner aninhado. (NPR-39041)
* O conteúdo agora não se sobrepõe mais com outro conteúdo de 320 pixels de largura. (SITES-8885)
* Adição de foco após fechar uma caixa de diálogo. (SITES-8885)

### Acessibilidade {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* O **[!UICONTROL Anotação]** está faltando o nome de acessibilidade. (SITES-2892)
* O estado de um componente ATIVO da interface do usuário (**[!UICONTROL Recortar]**, **[!UICONTROL Copiar]**, **[!UICONTROL Colar]**, **[!UICONTROL Inserir componentes]**, **[!UICONTROL Grupo]** e assim por diante) não tem pelo menos uma relação de contraste de luminosidade de três a um com o fundo adjacente interno ou externo. (SITES-8889, SITES-8756, SITES-8885)
* Mensagem de status não anunciada automaticamente. (SITES-8889, SITES-8756, SITES-8885)
* O conteúdo do texto não tem relação de contraste de 4.5:1. (SITES-8756, SITES-8885)
* O texto do link ou do botão não tem a relação de contraste 4.5:1 ao passar o mouse ou focalizar. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL gera uma exceção. Por exemplo, não é possível obter tags de variação de um fragmento de conteúdo. Não há variação com o nome &quot;elétrico&quot;. Esse problema é devido à chamada de `getVariationTags` para uma variação não existente que suscite uma exceção. (SITES-8898)
* Classificação de ordens de título na exibição em Lista, ascendentes e decrescentes, como os títulos com a ordem A, C, B. (SITES-7585)
* Adição do suporte à marcação para variações de fragmento de conteúdo. (SITES-8168)
* Identificado e removido o código específico do Odin do Experience Manager 6.5 que era desnecessário. (SITES-3574)
* Ao publicar um fragmento de cópia de idioma na interface do usuário do Editor de fragmento de conteúdo, as referências associadas eram publicadas na pasta em inglês. (NPR-39182)
* Os campos de data estão sendo pré-preenchidos com uma data. (NPR-39124)
* As tags desapareceram na segunda vez que você selecionou a opção de botão de opção. (NPR-39071)

### Fluido XP {#sites-fluidxp-6515}

* Ativar o suporte de compilação ES6 para a biblioteca cliente `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* O Multicampo em um Modelo de fragmento de conteúdo não pode ser esvaziado e salvo porque a validação ocorre mesmo se **[!UICONTROL Obrigatório]** não está selecionada. (NPR-39063)
* Em **[!UICONTROL Copiar]** ou **[!UICONTROL Livecopy]** , as `cq:targetMetadata` as informações estavam sendo duplicadas incorretamente. Essa funcionalidade fazia com que dois ou mais Fragmentos de experiência no Experience Manager apontassem para a mesma oferta exportada no target. (NPR-38970)
* Após uma ação Restaurar árvore, a mensagem `Un-publication pending. #0 in the queue` aparece na interface do usuário para uma página que nunca foi publicada. (NPR-38847)

### Editor de página {#sites-pageeditor-6515}

* Desfazer não excluiu a última alteração feita no texto que foi adicionado ao componente. Em vez disso, quando a página foi atualizada, todo o componente foi excluído. (SITES-8597)
* Atualização `jquery-ui` Para a versão mais recente, o Editor de páginas não funcionava corretamente. (NPR-38596)
* O conteúdo agora não se sobrepõe mais com outro conteúdo de 320 pixels de largura. (SITES-8756)
* foi adicionado foco após fechar o diálogo (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` não suportava a criação ou gestão de grupos com espaço em branco no nome principal porque o nome do grupo era tratado como uma cadeia de caracteres e não suportava a citação. (SLING-10952)
* Os logs são preenchidos inadvertidamente com mensagens de erro e exceções. (NPR-39024)

## Projetos de tradução {#translation-6515}

* A página de destino estava sendo adicionada ao trabalho de tradução para Cópias de idioma atualizadas por meio do painel Projetos; a página de origem não foi atualizada. (NPR-39278)
* O processo de tradução falhava ao gerar uma pré-visualização para todas as páginas em um projeto de tradução. (NPR-39059)
* Se a localidade do idioma não existir, ela ainda será criada em uma pasta de localidade quando as regras de referência forem configuradas para um evento. (NPR-39054)

## Interface do usuário {#ui-6515}

* Erros de JavaScript ocorrem dentro do arquivo `multifield.js` para determinados campos no modelo de Fragmento de conteúdo no editor de modelo de Fragmento de conteúdo e também no editor de Fragmento de conteúdo. (NPR-39350)

## Fluxo de trabalho {#workflow-6515}

* Os workflows executados com êxito no Experience Manager 6.5.11 não eram executados consistentemente no 6.5.13 do Experience Manager. (NPR-39023)

## Instalar [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.15.0 em uma das instâncias do autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>O Adobe não recomenda remover ou desinstalar o [!DNL Experience Manager] Pacote 6.5.15.0. Assim, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->

### Instalar o service pack em [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL Experience Manager] 6.5.15.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.15.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience Manager (6.5.15.0)` under [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.13 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar [!DNL Experience Manager] Pacote do complemento Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorar se não estiver usando [!DNL Experience Manager] Forms.

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. Verifique se você instalou o [!DNL Experience Manager] service pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Se você usar letras no Experience Manager 6.5 Forms, instale o [Pacote de compatibilidade AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Instalar [!DNL Experience Manager] Forms no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções na [!DNL Experience Manager] O Forms no JEE é fornecido por meio de um instalador separado.

Execute as etapas a seguir para todos os ambientes AEM Forms em JEE usando qualquer servidor de aplicativos que não seja JBoss EAP 7.4.0.
1. Instalar [Patch do AEM Forms JEE](jee-patch-installer-65.md). O inclui todos os problemas corrigidos para todos os componentes do AEM 6.5 Forms no JEE.
1. Instale o [Fragmento para AEM 6.5 Forms no JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar). O fragmento adiciona as dependências necessárias para instalar AEM Service Pack 15 (6.5.15.0).
1. Depois de instalar o fragmento, aguarde a estabilização do servidor de aplicativos.
1. [Instale o service pack no Experience Manager 6.5](#install-service-pack).

   >[!NOTE]
   >
   >Se você instalar o [AEM service pack (6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), antes de instalar o [Fragmento para AEM 6.5 Forms no JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) no ambiente AEM 6.5 Forms no JEE, o CRX/bundle e a página inicial podem parar de funcionar e você encontra o erro de serviço indisponível. Para resolver o problema, execute as ações [listado aqui](/help/forms/using/aem-service-pack-installation-solution.md).

1. Instale o [pacote complementar mais recente do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html), exclua o pacote do complemento Forms do `crx-repository\install` e reinicie o servidor.

### UberJar {#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.15.0 está disponível no [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a variável `dependency` .

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] a integração do é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Ele suporta o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O Runtime] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM Fragmento de conteúdo com o Pacote de índice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Esse pacote é necessário para clientes que usam o GraphQL; isso permite que eles adicionem a definição de índice necessária com base nos recursos que realmente usam.

* As [!DNL Microsoft® Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] não suporta instalações turnkey para [!DNL AEM Forms 6.5.10.0].

* Se estiver atualizando seu [!DNL Experience Manager] da versão 6.5 para 6.5.10.0, você pode visualizar `RRD4JReporter` exceções na `error.log` arquivo. Para resolver o problema, reinicie a instância.

* Se você instalar [!DNL Experience Manager] 6.5 Service Pack 10 ou service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado dos ativos (criado em `/var/workflow/models/dam`) é excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada em [!DNL Experience Manager] usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de registro não registrada.

* Ao tentar mover/excluir/publicar Fragmentos de conteúdo ou Sites/Páginas, há um problema quando as referências do Fragmento de conteúdo são buscadas, uma vez que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (não é necessária reindexação):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.15.0](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.15.0](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao Cliente Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

