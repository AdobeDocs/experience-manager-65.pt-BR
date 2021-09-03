---
title: '[!DNL Experience Manager] Notas de versão do service pack 6.5'
description: Notas de versão específicas do  [!DNL Adobe Experience Manager] 6.5 service pack 10
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 2095159a76380f7d17abcea9965ed6f82da69c8c
workflow-type: tm+mt
source-wordcount: '4245'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de versão do service pack 6.5 {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.10.0 |
| Tipo | Lançamento do Service Pack |
| Data | 26 de agosto de 2021 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## O que está incluído em [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] A versão 6.5.10.0 inclui novos recursos, principais melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização da versão 6.5 em abril de 2019. O service pack é instalado em [!DNL Adobe Experience Manager] 6.5.

Os principais recursos e aprimoramentos introduzidos no [!DNL Adobe Experience Manager] 6.5.10.0 são:

* **Modelos e  [!DNL Content Fragment] editor** aprimorados: Agora é possível criar modelos complexos e personalizados para conteúdo estruturado usando  [!DNL Content Fragment] modelos aninhados. As estruturas de conteúdo são modularizadas em elementos básicos que são modelados como subfragmentos. Os fragmentos de nível superior fazem referência a esses subfragmentos. Mais aprimoramentos de tipo de dados, como regras de validação avançadas, aprimoram ainda mais a flexibilidade da modelagem de conteúdo com [!DNL Content Fragments]. O editor [!DNL Experience Manager] [!DNL Content Fragment] oferece suporte a estruturas de fragmento aninhadas em uma sessão de editor comum, com aprimoramentos como visualização de árvore de estrutura e navegação de navegação estrutural por guias por meio de hierarquias de fragmento.

* **API GraphQL para[!DNL Content Fragments]**: A nova API GraphQL é o método padrão para fornecer conteúdo estruturado no formato JSON. As consultas GraphQL permitem que os clientes solicitem apenas os itens de conteúdo relevantes para renderizar uma experiência. Essa seleção elimina a entrega excessiva de conteúdo (possibilidade com APIs REST HTTP) que requer análise de conteúdo no lado do cliente. Os esquemas GraphQL são derivados de [!DNL Content Fragment] modelos e as respostas da API são feitas no formato JSON. Em [!DNL Experience Manager] como um [!DNL Cloud Service], [as consultas GraphQL persistem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) e processam solicitações de GET amigáveis ao cache. Ainda não é possível em [!DNL Experience Manager] 6.5.10.0.

* **Gestão de hierarquia e pré-visualização** futura: Agora, os usuários têm uma interface para acessar as estruturas de conteúdo de suas  [!DNL Experience Manager] inicializações, incluindo a capacidade de adicionar e remover páginas em um lançamento. Esse recurso melhora a flexibilidade de [!DNL Experience Manager] inicializações para criar versões de conteúdo direcionadas para publicação futura. [O recurso de ](/help/sites-authoring/working-with-page-versions.md#timewarp) distorção de tempo permite que os usuários visualizem inicializações como estados de conteúdo futuros.

* **Ativos** conectados:  [!DNL Experience Manager] estende a  [!DNL Connected Assets] funcionalidade ao uso de  [!DNL Dynamic Media] imagens nos componentes principais aplicáveis. Consulte [usar Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* **Opções de compartilhamento de link para baixar ativos ou representações**: Ao compartilhar ativos e coleções como link, os usuários podem escolher permitir o download dos ativos originais, suas execuções ou ambos usando o link compartilhado. Além disso, os usuários que baixam os ativos compartilhados com eles por meio de um link obtêm a opção de baixar apenas os ativos originais, somente as execuções ou ambos.

* **Limitar subativos gerados**: Os administradores podem limitar o número de subativos  [!DNL Experience Manager] gerados para ativos compostos, como arquivos PDF, PowerPoint, InDesign e Keynote. Consulte [Gerenciar ativos compostos](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Suporte** Camera Raw: Um novo  [!DNL Camera Raw] pacote está disponível e oferece suporte à  [!DNL Adobe Camera Raw] v10.4. Consulte  [Processar imagens usando [!DNL Camera Raw]](/help/assets/camera-raw.md).

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para 1.22.8.

* **Aprimoramentos de acessibilidade**:

   * [!DNL Dynamic Media] O fornece muitos aprimoramentos de acessibilidade para visualizadores. Consulte [[!DNL Dynamic Media] atualizações](#dynamic-media-65100).

   * A Platform oferece algumas melhorias de acessibilidade. Consulte [Atualizações da plataforma](#platform-65100).

* **Melhorias** na experiência do usuário:

   * [!DNL Experience Manager] exibe diretamente uma lista de todos os modelos de conteúdo em uma pasta, sem que os autores de conteúdo tenham que navegar pela estrutura do arquivo. O recurso agora requer menos cliques e melhora a eficiência da criação.

   * O campo de caminho no editor [!DNL Sites] permite que os autores arraste ativos de [!DNL Content Finder].

* Adição de suporte para `GuideBridge#getGuidePath` API em [!DNL AEM Forms].

* Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão e espanhol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model) para formulários adaptáveis.

* **Mensagens de erro no navegador** Propriedades: Adicionadas mensagens de erro para cada propriedade no navegador Adaptive Forms Properties. Essas mensagens ajudam a entender os valores permitidos para um campo.

* **Suporte para usar a opção literal para definir o valor para uma variável** do tipo JSON: Você pode usar a opção literal para definir um valor para uma variável do tipo JSON na etapa Definir variável de um fluxo de trabalho AEM. A opção literal permite especificar um JSON no formato de uma string.

<!--

* [Platform Updates](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
  * [!DNL Adobe Acrobat 2020]
  * [!DNL Ubuntu 20.04]
  * [!DNL Open Office 4.1.10]
  * [!DNL Microsoft Office 2019]
  * [!DNL Microsoft Windows Server 2019]
  * [!DNL RHEL8]

  -->

Para obter uma lista de todos os recursos e aprimoramentos introduzidos em [!DNL Experience Manager] 6.5.10.0, consulte [novidades no [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

Esta é a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.10.0.

### [!DNL Sites] {#sites-65100}

* O foco muda para outro campo ao digitar o campo **[!UICONTROL Valor padrão]** na guia **[!UICONTROL Propriedades]** do Editor de fragmento de conteúdo (NPR-36992).

* Enquanto filtra [!DNL Content Fragment] modelos em um caminho especificado, [!DNL Experience Manager] pesquisa retorna todos os nós com `cq:Template` em vez de retornar caminhos e nós somente para o modelo [!DNL Content Fragment] (SITES-1453).
* [!DNL Content Fragments] return  `null` como o status das pastas (SITES-1157).
* [!DNL Experience Manager] O não permite que os usuários desabilitem e habilitem  [!DNL Content Fragment] Modelos (SITES-1088).
* Quando um usuário move, renomeia ou exclui [!DNL Content Fragments] ou ativos de mídia, os [!DNL Content Fragments] referenciados não são atualizados automaticamente (SITES-196).
* Colar componentes de uma página em outra produz erros de JavaScript (NPR-37030).
* Quando as propriedades da página são visualizadas rapidamente, as Propriedades da página para uma página diferente são abertas (NPR-37025).
* O Fragmento do conteúdo permite que o Fragmento do conteúdo faça referência a ele mesmo. O seletor não suporta a operação (NPR-36993).
* Após a atualização para o service pack 9, alguns usuários não podem mover pastas no Experience Manager e ver erros nos logs (SITES-1481).
* Ao ajustar a largura do componente no contêiner de layout no modo de edição, observa-se uma cintilação (NPR-36961).
* Ao promover um lançamento, as alterações no lançamento promovido são implantadas duas vezes nas outras inicializações. Se um usuário promover a inicialização dupla de roll-out, o conteúdo duplicado será refletido na página de origem (NPR-36893).
* [!DNL Experience Manager] adiciona uma borda cinza a algumas imagens PNG com transparência se você adicionar as imagens a uma página usando o Componente principal de imagem ou se redimensionar usando o componente Imagem de base (NPR-36879).
* [!DNL Experience Manager Sites] A interface do usuário do administrador com um alto número de modelos resulta em navegação lenta (NPR-36870).
* A atualização para o service pack 9 impede a criação de alguns componentes. Esse problema não permite que [!DNL Sites] usuários criem novas páginas (NPR-36857).
* O método `ContextHubImpl` cria um `ResourceResolver` que não está fechado. Ele leva a mensagens de aviso sobre `ResourceResolver` de longa duração e o serviço retorna resultados inesperados às vezes (NPR-36853).
* Ao sincronizar uma única live copy a partir das propriedades da página do blueprint, todas as outras live copies também serão sincronizadas (NPR-36829, NPR-36522).
* Quando apenas o tipo XLS MIME é usado, a função de upload de arquivo não funciona conforme o esperado (NPR-36785).
* Novas tags com letras maiúsculas e minúsculas e todas as palavras maiúsculas não são exibidas no campo de tag dentro de [!DNL Content Fragments] (NPR-36742).
* A opção Elemento de texto único ao adicionar um [!DNL Content Fragment] faz com que o texto esteja ausente e cria uma formatação ímpar relacionada a listas e listas aninhadas (NPR-36565).
* Quando um autor anota qualquer componente em uma página, exclui o componente e executa uma ação de desfazer na operação de exclusão, um erro é encontrado ao tentar exibir os dados da Linha do tempo da página no console Sites (NPR-36528).
* A opção [!UICONTROL Save &amp; Close] do Editor de itens em massa das propriedades da página salva as alterações, mas não fecha o editor (NPR-36527).
* Quando um usuário tenta arrastar e soltar um novo componente de Texto em uma página, o componente desaparece imediatamente (NPR-36442).
* Quando um usuário digita uma tag sob demanda que inclui espaço (a tag que não existe no sistema) e pressiona Enter, a tag aparece abaixo do campo. No entanto, quando o [!DNL Content Fragment] é salvo e reaberto, a tag sob demanda não é exibida (NPR-36441).
* O template não pode ser excluído quando a instância é acessada pelo Dispatcher (NPR-36385).
* Quando uma página é movida, uma atualização manual do navegador é necessária para renderizar as alterações (NPR-36381).
* Ao selecionar um componente, você pode recortá-lo ou copiá-lo com Ctrl+X ou Ctrl+C (e Command+X ou Command+C no Mac). Ao clicar em outro componente, você pode colar com a barra de ferramentas, mas não com o teclado (Ctrl+V ou Command+V) (NPR-36379).
* Quando um usuário tenta cortar componentes usando o ícone de tesoura para movê-los para outro lugar, ocorre um erro de console. Além disso, ao colar apenas um componente é movido (NPR-36378).
* [!DNL Experience Manager] tem uma consulta sem índice no WCM ou notificações, o desempenho é retardado (NPR-36303).
* Quando um autor restaura a herança no componente herdado excluído, a opção disponível é sincronizar todo o conteúdo da página. Os autores de conteúdo são solicitados a sincronizar a página completa mesmo se a herança for restaurada somente em um componente. Uma sincronização completa pode resultar na sincronização de conteúdo indesejado (NPR-34456, CQ-4310183).
* O Uso em tempo real de um componente na instância do autor não exibe todas as ocorrências. Alguns componentes são usados em mais de 1.000 páginas, mas o relatório exibe apenas cerca de 40 páginas (CQ-4323724).
* Quando há uma estrutura de site que tem muitas subpáginas, o carregamento das subpáginas na exibição de coluna leva mais tempo no Experience Manager 6.5.8, em comparação ao Experience Manager 6.4.8.2 (CQ-4322766).
* Desmarque &quot;Todos&quot; e não funcione na opção &quot;Página de implantação&quot; (NPR-37070).
* Ao abrir uma versão de componente v3 existente de uma página, a caixa de diálogo Propriedades da página não abre e um `NullPointerException` é registrado (SITES-1830).

### [!DNL Assets] {#assets-65100}

Os seguintes problemas foram corrigidos em [!DNL Assets]:

* O valor da propriedade `jcr:title` não é atualizado na instância de publicação depois que uma pasta é movida. Renomear e republicar uma pasta no autor não atualiza o valor da propriedade `jcr:title` do mesmo na instância de publicação (NPR-36369).

* Se dois ou mais ativos forem selecionados e um ou mais campos de metadados forem editados, a operação de salvamento falhará com o código de erro 500 no navegador Safari (NPR-36413).

* A importação de metadados em massa falha devido ao formato de data incorreto (NPR-36428).

* Quando uma seleção é feita na página [!UICONTROL Properties] para atualizar metadados, a interface fica lenta para responder quando há muitas opções fornecidas pelo esquema (NPR-36430).

* O Filtro de Pesquisa usando o predicado [!UICONTROL Status de Expiração] não está funcionando (NPR-36436).

* O menu pop-up para vários campos nas propriedades [!UICONTROL Metadados da pasta] não exibe os últimos valores selecionados (NPR-36937, CQ-4314429).

* Ao pesquisar arquivos e pastas, se o usuário aplicar um filtro e selecionar [!UICONTROL Arquivos e pastas], somente os arquivos serão exibidos, mas não a pasta (CQ-4319543, NPR-36627).

* As opções da barra de ferramentas são diferentes quando a mesma Coleção é selecionada de uma pasta e quando é selecionada de um resultado de pesquisa (NPR-36620).

* A opção [!UICONTROL Publicação rápida] não está disponível na página de resultados da pesquisa (NPR-36904, CQ-4317748).

* Quando os usuários criam uma live copy de um ativo sem especificar sua extensão, depois de baixar o arquivo da live copy não é utilizável (NPR-36903, CQ-4326305).

* Quando um usuário é adicionado como proprietário de uma pasta filho, ele obtém a permissão de proprietário da pasta pai para e, portanto, das outras pastas filhas do pai. Além disso, o usuário não é removido como proprietário da pasta pai ao tentar removê-la. (NPR-36801, CQ-4323737)

* [!DNL Experience Manager] gera uma exceção de falta de memória ao tentar criar sub-ativos para ativos compostos, como uma apresentação do PowerPoint (NPR-3668).

* Quando os usuários movem um ativo que já é usado em uma página de sites publicados, a página de sites é publicada novamente mesmo se a opção para publicar não estiver selecionada (NPR-36636, CQ-4323500).

* Ao usar o recurso de detecção de tipo MIME do Apache Tika, os ativos carregados usando o método `AssetManager.createAsset` deixam um arquivo temporário chamado `apache-tika-*.tmp` no diretório temporário. Esse arquivo temporário usa todo o espaço livre em disco disponível (NPR-36545).

* Todos os ativos protegidos por DRM são baixados e a seleção do usuário para baixar um ativo específico não é seguida (CQ-4327422).

* Não é possível arrastar ativos para `pathfield` na interface do usuário (NPR-36849).

* Quando você seleciona um ativo na Exibição de coluna, o painel Detalhes do ativo desaparece (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Aprimoramentos de acessibilidade**

Os seguintes aprimoramentos de acessibilidade estão disponíveis em [!DNL Dynamic Media Viewers].

* Os leitores de tela agora narram o texto do espaço reservado para pesquisar e adicionar Endereço de email como um campo obrigatório em compartilhar ativos como uma caixa de diálogo de link, e também anunciam a dica de ferramenta [!UICONTROL Preencha este campo] (CQ-4327761).

* Agora, os leitores de tela registram corretamente os nomes e as finalidades de vários campos no [!UICONTROL Editor de predefinição de imagem] ao acessar os campos da interface do usuário usando teclado (CQ-4325677).

* O foco do teclado agora se move apropriadamente para a guia de pesquisa da caixa de diálogo [!UICONTROL Predefinições do visualizador] do seletor de ativos da opção [!UICONTROL Tipo de mídia avançada] (CQ-4324736).

* Ao navegar no modo de formulários usando teclas do teclado, os leitores de tela registram os rótulos correspondentes às opções de incremento e decremento na guia [!UICONTROL Create] de [!UICONTROL Predefinições de imagem] (CQ-4323900).

* Os leitores de tela agora anunciam a opção [!UICONTROL Pesquisar e adicionar endereço de email] em compartilhar ativos como uma caixa de diálogo de link (CQ-4323352).

* O foco do teclado é mantido na barra de ferramentas ao navegar pelos ativos usando as teclas do teclado (CQ-4322037).

* Os leitores de tela agora narram as informações de campo recém-adicionadas [!UICONTROL Edit] após selecionar a opção [!UICONTROL Add Crop] dentro do [!UICONTROL Responsive Image Crop] na página [!UICONTROL Edit Image Processing Profile] (CQ-4290734).

* Nas páginas [!UICONTROL Editar predefinição de imagem] e [!UICONTROL Criar vídeo interativo], os leitores de tela agora anunciam apropriadamente o cabeçalho da página ao navegarem pelas páginas usando as teclas de atalho do teclado do cabeçalho (CQ-4290730)(CQ-4290701).

* Os leitores de tela agora podem reconhecer as várias regiões da tela (como região do painel direito, painel esquerdo, barra de ferramentas de ação, ponto de referência da barra de ferramentas do visualizador e ponto de referência de imagem com zoom) usando teclas de atalho de ponto e região ao navegar pelas páginas a seguir.

   * [!UICONTROL Editor de predefinições do visualizador]  (CQ-4290729)

   * [!UICONTROL Editor]  de conjunto de imagens (CQ-4290710)

   * [!UICONTROL Criar vídeo interativo]  (CQ-4290702).

* Agora, os leitores de tela anunciam o nome da opção de compartilhamento no quadro de vídeo, ao navegar usando a tecla de seta para baixo (CQ-4290728).

* Os leitores de tela agora narram os nomes de várias opções nas guias [!UICONTROL Sprite] e [!UICONTROL Background] na guia [!UICONTROL Aparência] no [!UICONTROL Editor de predefinição do visualizador] (CQ-4290727).

* Campos obrigatórios, como o campo para editar [!UICONTROL Largura], na guia [!UICONTROL Básico] da página [!UICONTROL Editar codificação de vídeo] agora têm um símbolo de asterisco (*) (CQ-4290725).

* Os leitores de tela agora anunciam o rótulo das opções na página [!UICONTROL Image Profiles] (CQ-4290723).

* Os usuários do Windows agora podem sair do editor de CSS expandido no [!UICONTROL Editor de predefinições do visualizador] quando o foco estiver no Editor de CSS (CQ-4290720).

* Na guia [!UICONTROL Básico] de [!UICONTROL Editar predefinição de imagem] ao navegar no modo Formulário, os leitores de tela agora narram os rótulos de vários campos e opções de edição (CQ-4290717).

* Agora, os leitores de tela narram a função e o estado (selecionado ou não) das opções da interface do usuário na página de detalhes da navegação à esquerda nos ativos (CQ-4290709).

* Agora, os leitores de tela registram corretamente o estado (selecionado ou não selecionado) e o link da imagem é alternado na guia [!UICONTROL Content] da página [!UICONTROL Create Interative Video] (CQ-4290707).

* Agora, os leitores de tela registram corretamente o nome, a função e o estado de vários segmentos na escala da linha do tempo do vídeo ao navegarem usando a tecla de seta para baixo na página [!UICONTROL Criar vídeo interativo] (CQ-4290706).

* Os leitores de tela agora narram o nome, a função e o estado padrão (selecionado ou não selecionado) e a propriedade ao navegar pelas opções na página [!UICONTROL Criar vídeo interativo] (CQ-4290704).

* Os leitores de tela agora narram o nome, a função e o estado padrão (selecionado ou não selecionado) das opções em [!UICONTROL Todos os ativos] e [!UICONTROL Todas as coleções] ao navegar na página [!UICONTROL Publicar] (CQ-4290705).

* Ao carregar um formato de vídeo não suportado (diferente de MP4) na página [!UICONTROL Criar vídeo interativo], o Experience Manager exibe e anuncia mensagens de erro (CQ-4290700).

* O contraste dos números (tempo em segundos) na escala da linha do tempo na página [!UICONTROL Criar vídeo interativo] agora atende à relação de luminosidade mínima exigida, de modo que os usuários com percepção limitada de cor possam ler facilmente (CQ-4290699).

* Os leitores de tela agora anunciam o rótulo do campo [!UICONTROL Nome do produto] ao navegar na página [!UICONTROL Criar vídeo interativo] (CQ-4290697).

**Problemas corrigidos**

As seguintes correções de erros estão disponíveis em [!DNL Dynamic Media].

* Vídeos carregados para [!DNL Experience Manager] exibir `Process failed` depois que `dynamicmedia_scene7` runmode é ativado e a sincronização é desativada (CQ-4327791).

### Plataforma {#platform-65100}

Os seguintes aprimoramentos são fornecidos neste service pack:

* Quando um usuário seleciona um item na exibição em Árvore, os leitores de tela anunciam as opções de seleção e da barra de ferramentas exibidas na parte superior (NPR-36504).
* Alguns nomes de texto e controle são mais fáceis de ler para usuários com problemas visuais, pois a taxa de luminosidade atende à proporção mínima exigida de 4.5:1 (NPR-36503).
* Quando um usuário usa os controles do calendário, o leitor de tela narra a data descritiva, o mês e as informações de dias da semana. Quando um usuário usa a tecla de atalho calendário, o leitor de tela narrará a alteração em data, mês e ano (NPR-36498).
* Suporte fornecido para executar JavaScript personalizado `Clientlibs` usando recursos do ECMAScript 6 sem estar em conformidade com o modo estrito. Especificamente, o sinalizador `emitUseStrict` é adicionado ao `GCCScriptProcessor` (NPR-36411).

As seguintes correções de erros fazem parte deste service pack:

* As verificações de integridade personalizadas são executadas com mais frequência do que o agendado (NPR-36985).
* O método `Resourceresolver map` retorna um resultado incorreto para páginas de alias (NPR-36767).
* [!DNL Experience Manager] a inicialização é atrasada devido ao carregamento de workflows (NPR-36615).

### Integrações {#integrations-65100}

* O Experience Manager fica sem resposta quando o nó principal do MongoDB é alternado para outro nó (NPR-36566).
* [!DNL Sling content distribution] falha ao executar a operação de exclusão do membro da coleção (NPR-36521, CQ-4323578).

### Interface do usuário {#user-interface-65100}

* O painel lateral **[!UICONTROL Referências]** não exibe referências de ativos e sites (GRANITE-35078, GRANITE-34892).

### Projetos de tradução {#translation-65100}

* As subpáginas extras em uma cópia de idioma de um projeto de várias traduções são excluídas (NPR-36622).

### Fluxo de trabalho {#workflow-65100}

* Se o servidor receber uma mensagem de ausência do escritório, ele reportará alertas de memória e deixará de responder (NPR-36768).

### [!DNL Communities] {#communities-65100}

* As páginas do site da comunidade estão sendo abertas no estado `LoggedIn` para usuários convidados anônimos (NPR-36908).

* Quando há mais de uma página na página **[!UICONTROL Comunidade]** > **[!UICONTROL Ideias]** > **[!UICONTROL Comentários]**, a navegação da página não funciona (NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>O service pack permite que você execute [!DNL AEM Forms] nos sistemas operacionais de servidor, servidores de aplicativos e bancos de dados mais recentes. Ele também oferece alguns recursos disponíveis no ambiente Cloud Service para local e fornece correções para problemas relatados por clientes. [!DNL AEM Forms] O service pack do OSGi está disponível para download e instalação. [!DNL AEM Forms on JEE]  service pack estaria disponível em 09 de setembro de 2021.

**Formulários adaptáveis**

<!--

* When the validations performed on the field values in an adaptive form are successful, [!DNL AEM Forms] fails to invoke the Form Data Model (CQ-4325491).

-->

* Ao adicionar um dicionário de idiomas a um projeto de tradução e, em seguida, abrir o projeto, [!DNL AEM Forms] exibe uma mensagem de erro (CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* Problemas de desempenho após instalar o [!DNL AEM Forms] Service Pack 7 (CQ-4326828).

**Gerenciamento de correspondência**

* Atraso na exibição de caracteres na guia [!UICONTROL Data], bem como na visualização da letra HTML (NPR-37020).

* Ao editar um fragmento de documento de texto, as novas palavras são exibidas como tags HTML após salvar o fragmento (NPR-36837).

* Não é possível exibir as letras salvas como rascunhos (NPR-36816).

* Ao editar um fragmento de documento de texto e, em seguida, visualizar a carta, o AEM Forms exibe o idioma da expressão na visualização da carta HTML (CQ-4322331).

* Problemas ao renderizar dados com um modelo de carta de autoatendimento (NPR-37161).


**Comunicações interativas**

* Um caractere de tabulação duplica entre duas palavras cada vez que você imprime uma visualização de Comunicação interativa após editar um fragmento de documento de texto (NPR-37021).

* [!DNL AEM Forms] exibe um erro ao salvar um fragmento de documento de texto que excede o limite máximo de tamanho (NPR-36874).

* Quando você adiciona uma imagem a uma Comunicação interativa, um bloco vazio adicional é exibido após a imagem (NPR-36659).

* Ao selecionar todo o texto em um editor, não é possível alterar o texto da fonte para Arial (NPR-36646).

<!--

* When you create a URL in an editor and preview the changes, a black background displays instead of the URL text (NPR-36640).

-->

* Ao copiar e colar texto em um editor, há problemas ao alterar a fonte para Arial para marcadores disponíveis no documento (NPR-36628).

* Problemas de recuo para marcadores no editor de texto (NPR-36513).

<!--
**Designer**

* Screen Reader fails to read floating field data placed inside text label on the Master page or on Subform pages in a dynamic PDF (CQ-4321587).

-->

**Serviços de documento**

* Quando você converte arquivos XDP em arquivos PDF e monta o PDF resultante, as gerações de PDF falham e exibe a seguinte mensagem de erro (CQ-4328666):

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Fluxo de trabalho dos formulários**

* Não é possível enviar um formulário para um processo do Workbench após a atualização para o AEM Forms Service Pack 8 (CQ-4325846).

**Formulários HTML5**

* Ao definir o valor para a propriedade `mfAllowAttachments` como `True` no repositório CRX DE, o `dataXml` é corrompido ao enviar o formulário HTML5 (NPR-37035).

* Ao renderizar um XDP como HTML usando `dataXml`, [!DNL AEM Forms] exibe um erro `Page Unresponsive` (NPR-36631).

### Commerce {#commerce-65100}

* O valor no campo **[!UICONTROL Publicado por]** exibido está incorreto na exibição Coluna (NPR-36902).
* Quando um Catálogo é implementado, novos produtos são marcados incorretamente como produtos modificados (NPR-36666).
* Quando você recria um produto excluído, a página do produto não é recriada (NPR-36665).
* As páginas modificadas são atualizadas, mas os produtos vinculados correspondentes não são atualizados na implantação do catálogo (CQ-4321409, NPR-36422).
* Os workflows **[!UICONTROL Publish later]** e **[!UICONTROL Unpublish later]** não funcionam (CQ-4327679).

Para obter informações sobre atualizações de segurança, consulte a [[!DNL Experience Manager] página de marcadores de segurança](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.10.0 {#install}

**Requisitos de configuração e mais informações**

* O Experience Manager 6.5.10.0 requer o Experience Manager 6.5. Consulte [atualizar documentação](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale o Experience Manager 6.5.10.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o pacote [!DNL Adobe Experience Manager] 6.5.10.0.

### Instalar o service pack {#install-service-pack}

Para instalar o service pack em uma instância [!DNL Adobe Experience Manager] 6.5, siga estas etapas:

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da sua instância [!DNL Experience Manager].

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador de Pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre no navegador [!DNL Safari], mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente o [!DNL Experience Manager] 6.5.10.0 em uma instância de trabalho:

A. Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use a API HTTP [do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.10.0 não suporta a instalação do Bootstrap.

**Validar a instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres de versão atualizada `Adobe Experience Manager (6.5.10.0)` em [!UICONTROL Produtos instalados].

1. Todos os pacotes OSGi são **[!UICONTROL ATIVE]** ou **[!UICONTROL FRAGMENTO]** no Console OSGi (Use o Console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é da versão 1.22.3 ou posterior (Use o Console da Web: `/system/console/bundles`).

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Instalar o pacote complementar do Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Pule se você não estiver usando o Experience Manager Forms. As correções no Experience Manager Forms são entregues por meio de um pacote complementar separado por uma semana após a versão agendada do [!DNL Experience Manager] Service Pack.

1. Certifique-se de ter instalado o Adobe Experience Manager Service Pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>O Experience Manager 6.5.10.0 inclui uma nova versão do [Pacote de Compatibilidade AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Se você estiver usando uma versão mais antiga do Pacote de Compatibilidade do AEM Forms e estiver atualizando para o Experience Manager 6.5.10.0, instale a versão mais recente da instalação do pacote após a instalação do Pacote de Suplementos do Forms.

<!--

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.10.0 está disponível no [Repositório Central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a tag `dependency`.

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos com [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | A tela de aceitação **[!UICONTROL AEM Cloud Services]** está obsoleta, pois a integração [!DNL Experience Manager] e [!DNL Adobe Target] é atualizada no Experience Manager 6.5. A integração oferece suporte à API Adobe Target Standard. A API usa autenticação pelo Adobe IMS e [!DNL Adobe I/O] e oferece suporte à função crescente do Adobe Launch para preparar [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configure conexões do sistema, autenticação Adobe IMS e [!DNL Adobe I/O] integrações por meio dos respectivos serviços em nuvem [!DNL Experience Manager]. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para o Experience Manager 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!--

* (For JBoss on Microsoft Windows only) To continue using the Create PDF service on [!DNL AEM Forms on JEE], download [omniORB_4.1.1_x86_win32_vc10.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/omniORB_4.1.1_x86_win32_vc10.zip) from Software Distribution, extract and copy the folder available in the Zip file to the following location:
`[AEM Forms Installation]\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\CommonNatives\lib`

* As [!DNL Microsoft Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] does not support turnkey installations for [!DNL AEM Forms 6.5.10.0].

-->

* Se estiver atualizando sua instância [!DNL Experience Manager] da versão 6.5 para 6.5.10.0, você poderá visualizar as exceções `RRD4JReporter` no arquivo `error.log`. Para resolver o problema, reinicie a instância.

* Se você instalar o [!DNL Experience Manager] 6.5 Service Pack 10 ou um service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado de ativos (criado em `/var/workflow/models/dam`) será excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do Experience Manager 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no Experience Manager usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de reg não registrada.

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos em [!DNL Experience Manager] 6.5.10.0:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.10.0](assets/65100_bundles.txt)

* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.10.0](assets/65100_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [como entrar em contato com o Atendimento ao Cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de versão 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

