---
title: '[!DNL Adobe Experience Manager] 6.5 Notas de versão do Service Pack.'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 7.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 34e41cf5984f5f69ae0ccead137fe4f180bd84ad
workflow-type: tm+mt
source-wordcount: '3787'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] Notas de versão do Service Pack 6.5 {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.7.0 |
| Tipo | Lançamento do Service Pack |
| Data | 26 de novembro de 2020 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## What&#39;s included in [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a versão 6.5 lançada em abril de 2019. O service pack é instalado em [!DNL Adobe Experience Manager] 6.5.

Os principais recursos e melhorias introduzidos na versão [!DNL Adobe Experience Manager] 6.5.7.0 incluem:

* Classificação das páginas de Live Copy disponíveis para implantação usando as propriedades [!UICONTROL Nome], [!UICONTROL Data da] última modificação e Data [!UICONTROL da] última implantação.

* Executar as movimentações de página e as implantações de MSM como operações assíncronas para reduzir seu impacto no desempenho do tempo de execução.

* Os usuários podem classificar ativos digitais em visualizações de cartão e coluna.

* [!DNL Assets] e [!DNL Dynamic Media] fornecer vários aprimoramentos de acessibilidade. Os aprimoramentos estão relacionados à navegação do teclado, ao uso de leitores de tela e à habilitação dos usuários para usar a tecnologia de assistência similar (AT). Consulte [[!DNL Assets] aprimoramentos](#assets-6570) e [[!DNL Dynamic Media] aprimoramentos](#dynamic-media-6570).

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.22.5.

Para obter uma lista completa dos recursos e aprimoramentos introduzidos na versão [!DNL Experience Manager] 6.5.7.0, consulte [Novidades do [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

A seguir está a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Quando você abre a opção [!UICONTROL Timewrap] para uma página, mantém a opção do painel lateral Linha do tempo aberta e navega até o console [!UICONTROL Sites] , o `Failed to Load` erro ocorre (NPR-34951).

* A opção [!UICONTROL Timewrap] não exibe imagens para a data e o intervalo de tempo selecionados (NPR-34951).

* Quando um filtro chama `getHeader()` de uma página que contém um Fragmento de conteúdo, o `java.lang.AbstractMethodError` erro ocorre (NPR-34942).

* Quando o caminho de uma página contém várias subsequências de conteúdo, o pré-visualização não consegue renderizar e a função de comparação de versão também falha (NPR-34740).

* Quando você define um valor numérico para a propriedade de rótulo do `String` tipo de um componente, pode excluir o componente e desfazer a operação de exclusão. Entretanto, após desfazer a exclusão, a propriedade label muda de `String` para `Long` (NPR-34739).

* A seguinte exceção ocorre ao adicionar um Fragmento de experiência com base em um modelo com um layout bloqueado a uma página (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Quando você move uma pasta, isso resulta em problemas transversais e o seguinte erro ocorre (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Quando novos ativos são criados, publicados e movidos para um novo local, o fluxo de `Request to complete move operation` trabalho é criado e resulta em um estado Abortado. Fazer upload de um novo ativo e executar uma `move` operação resulta na criação do fluxo de `Request to complete move operation` trabalho no estado pendente (NPR-34543).

* Quando você exporta um Fragmento de experiência do ambiente [!DNL Experience Manager] 6.5.2 para o [!DNL Target] Standard, a chamada da API falha porque a propriedade de espaço de trabalho não está disponível para o [!DNL Target] Standard (NPR-34557).

* Os usuários não podem publicar páginas por meio da opção [!UICONTROL gerenciar publicação] porque a opção [!UICONTROL Publicar] desaparece (NPR-34542).

* Quando você adiciona alguns estilos ao texto, uma `<div>` tag é adicionada ao texto e o estilo não pode mais ser aplicado ao texto (NPR-34531).

* Quando você seleciona um item em um menu pop-up e atualiza os arquivos necessários, isso não permite salvar os valores da caixa de diálogo, pois o outro menu tem um campo obrigatório vazio (NPR-34529).

* Quando você cria uma página a partir de um modelo personalizado e a move dentro da hierarquia do blueprint, os componentes excluídos anteriormente dos start da página que aparecem na página dentro da hierarquia de live copy (NPR-34527).

* Depois que um estilo de artigo é aplicado a um conteúdo, ele não pode ser removido (NPR-34486).

* Todas as cópias ao vivo e cópias de um Fragmento de experiência apontam para a mesma ID de [!DNL Adobe Target] oferta (NPR-34469).

* Os itens de lista com marcadores são exibidos além da lista numerada (NPR-34455).

* A opção de comparação com a fonte não mostra a diferença entre a página de origem e a versão editada de uma página (NPR-34285).

* Quando você exclui uma página, os detalhes do controle de versão não são configuráveis (NPR-34159).

* Quando um usuário seleciona a opção de diálogo [!UICONTROL Abrir seleção] , o foco do teclado se move para o controle oculto presente na página (CQ-4307779, CQ-4293601).

* Quando você move uma pasta publicada no Autor, os caminhos da pasta não são atualizados de acordo com a instância Publicar (CQ-4305144).

* Quando um usuário seleciona a `Enter` tecla na opção [!UICONTROL Selecionar tudo] , o foco do teclado não se move para a opção [!UICONTROL Criar controle] (CQ-4293599).

* Quando você seleciona a `Esc` tecla, o foco não é restaurado para o controle pai (CQ-4293593, CQ-4293590).

* Aprimoramento da conformidade com WCAG para [!DNL Sites] interface do usuário e componentes principais (CQ-4293448).

* [!UICONTROL As funções Zoom] e [!UICONTROL Escala] estão desativadas para a [!DNL Sites Editor] página (CQ-4282353).

* Depois de usar a opção Girar para a direita, o leitor de tela para de narrar a rotação ou o estado de giro atual (CQ-4282128).

* Os botões de diálogo Concluído e Cancelar configuração têm mais de uma parada de guia (CQ-4274601).

* Não é permitido mover páginas com um nome semelhante no mesmo nível (NPR-35041).

* Depois de selecionar a opção Limpar (x), o foco do teclado não se move para o campo [!UICONTROL Filtro] (CQ-4293581).

* Quando você atualiza para a versão [!DNL Experience Manager] 6.5.6.0, o comportamento do sistema de parágrafo herdado muda e ele não funciona corretamente (NPR-35117).

* Os usuários de teclado não conseguem alternar o foco da guia em uma ordem apropriada depois de selecionar a seção [!UICONTROL Ação] em uma [!DNL AEM Sites] página (CQ-4307786).

* Depois de selecionar uma opção na lista do menu público alvo do link da barra de ferramentas do RTE ao editar um fragmento de conteúdo, a caixa de diálogo do autor do fragmento de conteúdo é start para oscilar (CQ-4305532).

* Os usuários de teclado não conseguem selecionar as opções na lista suspensa [!UICONTROL Adicionar componente] usando a tecla de seta para baixo (CQ-4295097).

* O foco da guia não se desloca em uma ordem apropriada ao selecionar uma data no menu Calendário na guia [!UICONTROL Ativos] de uma [!DNL Sites] página (CQ-4293600).

* O foco da guia não muda para a próxima opção ou para as opções anteriores para usuários do teclado depois de excluir as opções de Link ou Texto disponíveis ao editar uma página Sites (CQ-4293597).

* Os usuários de teclado não conseguem voltar o foco da guia para Mais opções na seção [!UICONTROL Ações] depois de visualizar as opções disponíveis e pressionar a `Esc` tecla (CQ-4293592).

* Quando você ativa a opção [!UICONTROL Girar] para uma imagem no modo [!UICONTROL Editar] , o foco da guia, em vez de permanecer em Girar, muda para a opção [!UICONTROL Refazer] para os usuários do teclado (CQ-4293587).

* Na caixa de diálogo [!UICONTROL Abrir seleção] disponível na guia [!UICONTROL Link e ações] , o foco da guia muda para elementos ocultos na página após a opção [!UICONTROL Cancelar] (CQ-4293579).

* Quando os usuários do teclado editarem uma imagem, navegarem até a opção [!UICONTROL Concluir] e pressionarem a tecla Enter, os leitores de tela não anunciarão a conclusão (CQ-4282351).

* As opções Mover para cima e Mover para baixo disponíveis na caixa de diálogo [!UICONTROL Link e ações] não estão disponíveis para os usuários de leitores de tela e teclado (CQ-4281120).

* Os usuários de teclado não conseguem restaurar o foco da guia depois de navegar até a opção Fechar (X) na página [!UICONTROL Propriedades] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] A versão 6.5.7.0 [!DNL Assets] corrige os seguintes problemas e fornece os seguintes aprimoramentos.

* Os seguintes aprimoramentos são feitos para acessibilidade em [!DNL Experience Manager Assets]:

   * Ao navegar pela linha do tempo usando um teclado, a `Esc` tecla pode recolher a opção [!UICONTROL Mostrar tudo] sem perder o foco (CQ-4293598).
   * Ao navegar usando a tecla de guia do teclado, depois de remover a última tag das tags adicionadas, o campo de tag retém o foco (NPR-35109).
   * [!DNL Experience Manager] os componentes agora contêm informações apropriadas para nome, função e valor a serem usados pelos leitores de tela (NPR-34255).
   * Depois que você exclui a caixa de combinação Tipo/Tamanho, a caixa de combinação Link, a caixa de combinação Idioma ou a caixa de edição de texto, o foco do teclado retorna para os elementos da interface do usuário anterior ou seguinte ou para um elemento da interface do usuário mais relevante (CQ-4293585).
   * Ao passar o ponteiro do mouse sobre várias opções, dicas como Selecionar e Download são exibidas. Os usuários que usam ampliação de tela podem ter dificuldade para visualizar as miniaturas do arquivo devido ao conteúdo exibido devido ao passar o mouse. Agora é possível preservar o foco, depois de remover a opção usando uma `Escape` chave (CQ-4293554).
   * Ao selecionar uma célula de grade da grade presente na página, o foco muda para a barra de ação que aparece na tela (CQ-4282127).
   * Os usuários visuais podem diferenciar entre o texto normal e um link, à medida que as pistas visuais (ícone sublinhado e divisa) são exibidas para links para todas as soluções no [!DNL Experience Manager] home page (CQ-4282072).

* O seguinte aprimoramento da experiência do usuário é feito em [!DNL Assets]:

   * Ative a classificação de ativos na visualização de cartão e na visualização de coluna (NPR-35097).

* Após a atualização para a versão 6.5, se um arquivo JSON for gerado usando a API HTTP Assets, há problemas com a codificação usada no arquivo (NPR-35129).

* Os usuários de um grupo que não tem permissão para criar coleções (a opção Criar coleção não está disponível) ainda podem criar coleções acessando diretamente o URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Quando classificados por nome, os ativos pesquisados são classificados de maneira que diferencia maiúsculas e minúsculas. Isso cria duas listas separadas separadas separadas com base na capitalização que aparece de maneira ordenada nos resultados da pesquisa (NPR-35068).

* Quando um Fragmento de conteúdo é aberto no editor, as mensagens de aviso (`Invalid value specified for a metadata property`) são registradas nos registros de erro (NPR-35012).

* Os usuários sem privilégio de administrador podem editar ativos expirados usando o aplicativo para desktop [Experience Manager] . (NPR-34993).

* Quando o mesmo ativo é arrastado na interface do usuário do Assets e uma nova versão é criada, as alterações nos metadados não são persistentes (NPR-34940).

* Ao editar coleções, um usuário pode excluir o título da coleção e salvar as alterações com êxito (NPR-34889).

* Ao carregar uma imagem de duplicado, uma opção de exclusão é apresentada. Selecionar excluir permite que as imagens sejam carregadas. O fluxo de trabalho do Ativo de atualização do DAM também é acionado (NPR-34744).

* Ao usar [!DNL Adobe Asset Link] com [!DNL Adobe InDesign], os resultados da pesquisa não contêm pastas e coleções, mas contêm apenas ativos (NPR-34699, CQ-4303666).

* Passar o ponteiro sobre a visualização do cartão faz com que a tela role como resultado do foco (automático) nas ações rápidas disponíveis no cartão (NPR-34514).

* Ao editar as propriedades de vários ativos em massa, selecionar a opção [!UICONTROL Salvar] fecha a visualização do editor em massa e redireciona para a [!DNL Assets] página principal. Esse comportamento é igual ao comportamento da opção [!UICONTROL Salvar e fechar] e não é esperado (NPR-34546).

* A coleção inteligente não apresenta a configuração correta da interface do usuário após salvar. O query é salvo corretamente, mas a interface sempre exibe o último predicado de Opção adicionado (NPR-34539).

* Ao adicionar ativos [!DNL Experience Manager], os metadados sem uma namespace não são importados (NPR-34530).

* Ao arrastar um ativo em uma pasta para movê-lo, a interface do usuário também exibe a opção para [!UICONTROL Soltar no Lightbox] e [!UICONTROL Soltar na coleção]. Mesmo se a operação de movimentação for cancelada, a interface do usuário continuará a exibir as duas últimas opções (NPR-34526).

* O símbolo `%>` é exibido na página de coleções (NPR-34499).

* Na visualização da coluna, [!DNL Assets] exibe a pasta do duplicado e os nomes dos ativos ao rolar para cima e para baixo antes que todos os ativos sejam exibidos (NPR-34464).

* Se você criar uma pasta privada imediatamente após a criação de uma pasta pública, a pasta pública usará as configurações de pasta privada (NPR-34415).

* Na visualização do cartão, os cartões não estão listados em ordem alfabética e os cartões não podem ser classificados alfabeticamente (NPR-34234).

* Ao reabrir regras em cascata, as opções não são mantidas na interface do usuário (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Os principais aprimoramentos a seguir são feitos para acessibilidade em [!DNL Dynamic Media] (CQ-4290306). Para obter detalhes, consulte recursos de acessibilidade em [!DNL Dynamic Media].  <!-- TBD: link to DM content post GA -->

   * Os leitores de tela (JAWS, Narrador) registram o nome, a função e o estado dos itens de menu na opção de menu Incorporar tamanho (CQ-4290927).
   * Os usuários podem navegar na caixa de diálogo Link de email usando a `Tab` chave (CQ-4290926).
   * O fluxo de trabalho para criar perfis de codificação de vídeo é mais fácil de usar, dado o aprimoramento do leitor de tela (CQ-4290623, CQ-4290622).
   * Ao navegar usando a `Tab` tecla, o foco move para os elementos apropriados da interface do usuário no fluxo de trabalho para criar um vídeo interativo (CQ-4290621, CQ-4290620, CQ-4290619).
   * A página Publicar, a página Editar ativo, a página Editar recortes inteligentes e a página Editor de conjuntos de imagens são aprimoradas para atender aos padrões da Web. Os usuários da tecnologia assistiva (AT) agora podem navegar facilmente nessas páginas e realizar ações como imagens recortadas (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-429 00610, CQ-4290614).
   * Os visualizadores são aprimorados para permitir que os usuários naveguem usando um teclado (CQ-4290615).
   * Os usuários do teclado e do leitor de tela podem usar a funcionalidade de corte (CQ-4290609).
   * Os usuários de teclado podem gerenciar melhor os pontos de conexão (CQ-4290604, CQ-4290603).

* Os Conjuntos de imagens remotos não são editáveis se o nome da empresa e o nome da pasta forem os mesmos (NPR-31340). [!DNL Experience Manager]

* A ordem do índice z está incorreta quando você tenta pré-visualização na saída depois de adicionar um ponto de acesso a uma [!DNL Dynamic Media] imagem ou depois de editar um [!DNL Dynamic Media] vídeo ou um [!DNL Experience Fragment] com uma imagem (CQ-4307267).

* [!DNL Dynamic Media] falha de sincronização quando conjuntos de mídia mista são reprocessados (CQ-4307184).

* Se um ativo for movido para uma pasta na qual a sincronização automática [!DNL Dynamic Media] está configurada, o ativo não será sincronizado (CQ-4307122).

* [!DNL Dynamic Media] o vídeo não está sendo reproduzido em dispositivos iOS com controles de vídeo HTML5 nativos (CQ-4306977, CQ-4306727).

* Não é possível baixar imagens nas quais o SmartCrop é aplicado (CQ-4304558).

* Não é possível publicar seletivamente pastas no Dynamic Media (CQ-4304526).

* Desfazer a publicação de um arquivo de vídeo de [!DNL Experience Manager] não cancela a publicação do Conjunto de vídeos adaptáveis de uma implantação configurada do Scene7 (CQ-4304405).

* Adicionar um ativo de imagem panorâmica em um componente de mídia panorâmica e atualizar a página resulta em `Uncaught ReferenceError: $ is not defined` erro (CQ-4302810).

* No Editor [!UICONTROL de predefinições do]visualizador, ao editar a predefinição [!UICONTROL PanorâmicaImage/PanorâmicaImage_VR] , no `PanoramicView` componente, o rótulo do `PANORAMICVIEW_AUTOROTATE` modificador não está disponível (CQ-4302443).

* As legendas de vídeo não são exibidas se o vídeo não for o primeiro em um MixedMediaSet (CQ-4298161).

* O Visualizador de eCatalog HTML5 em dispositivos móveis iPhones não pode virar as páginas nem virar as páginas (CQ-4296611).

* Ao rolar amostras em um dispositivo móvel, as amostras rolam para a direita e para fora da área visível por alguns segundos antes de rolar de volta para a visualização (CQ-4296439).

* Quando um registro Principal predefinido do visualizador é criado, o CSS e a arte-final não são publicados e somente a predefinição do visualizador é publicada (CQ-4262205).

* Ao tentar vincular um Fragmento de experiência para um determinado ponto de acesso no componente Vídeo/imagens  interativas, ele não mostra o caminho selecionado do Fragmento de experiência. Em vez disso, retorna um valor vazio do campo de caminho (NPR-35146, CQ-4298136).

* Não é possível pré-visualização de um fragmento de experiência no Editor IVV (CQ-4308560).

* Ao adicionar um ponto de acesso a uma imagem e selecionar um Fragmento de experiência, não é possível selecionar as subpastas e as variantes do Fragmento de experiência (CQ-4307455).

* Os ativos que não são de imagem não são exibidos como publicados após o upload (CQ-4306415).

#### [!DNL Experience Manager] Ativos 3D {#three-d-assets-6570}

* `DAM CQ MIME Type` o serviço aplica tipos MIME incorretos a ativos 3D, resultando em renderização incorreta (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* A interface de usuário da coleção de produtos Commerce não lista mais de 15 produtos em uma coleção (NPR-34502).

### Plataforma {#platform-6570}

* Uma sessão HTTP sobre HTTPS não é invalidada (NPR-35083).
* Um `NullPointerException` é retornado ao iniciar tarefas de manutenção diárias ou semanais na interface do usuário (NPR-34953).
* O validador W3C relata avisos para arquivos JavaScript da biblioteca de cliente compatíveis (NPR-34898).
* A `AudienceOmniSearchHandler` função usa um índice obsoleto (NPR-34870).
* Sair do Experience Manager não limpa os cookies (NPR-34743).
* A `findByTitle` função da `TagManager` API não funciona se o nome da tag contiver um caractere especial (NPR-34357).
* Falha no processo de importação do pacote de sincronização do usuário (NPR-34399).
* Adicionado suporte para `ariaLabel` e `ariaLabelledby` propriedades ao `Coral.Masonry` componente (GRANITE-29962).
* O cache do Dispatcher não é atualizado para páginas com fragmentos de conteúdo após a instalação dos pacotes de componentes principais mais recentes (CQ-4306788).
* Nomes de tags localizados com aspas (`"`) não são exibidos corretamente na interface do usuário (CQ-4305439).

### Interface do usuário {#ui-6570}

* O campo [!UICONTROL Link para] nas propriedades do componente exibe sugestões de preenchimento automático que não correspondem à string especificada (NPR-34865).

* AEM exibe a seguinte mensagem de erro ao programar uma janela de manutenção diária distribuída entre 2 dias (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integrações {#integrations-6570}

* Falha na edição de uma [!DNL Adobe Launch] configuração existente (NPR-35045).
* Não é possível exportar [!DNL Experience Fragments] para [!DNL Adobe Target] se estiver usando a configuração e o [!DNL Adobe Target Standard] ambiente do IMS (NPR-34555).
* A opção [!UICONTROL Criar] é exibida na página [!UICONTROL Audiência] ao navegar de uma pasta para a página [!UICONTROL Audiência] (NPR-35151).

### Sling {#sling-6570}

* A verificação de integridade de logon padrão valida as credenciais de um usuário que não existe (NPR-34686).

### Projetos de tradução {#translation-6570}

* Ao cancelar um projeto de tradução no, [!DNL Experience Manager]a solicitação para cancelá-lo não é enviada ao provedor de tradução (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Todos os casos de terminologia não equitativa no produto são substituídos por equivalentes aceites (NPR-34311).
* [!DNL Google+] é removido da lista de opções de compartilhamento em redes sociais (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* A interface do usuário não responde ao selecionar os ativos na Visualização [!UICONTROL da] Lista (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libera os pacotes de complementos uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.

Para obter informações sobre atualizações de segurança, consulte a página [de boletins de segurança do](https://helpx.adobe.com/security/products/experience-manager.html)Experience Manager.

## Install 6.5.7.0 {#install}

**Requisitos de configuração e mais informações**

* AEM 6.5.7.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* O download do service pack está disponível na Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale o AEM 6.5.7.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>Adobe does not recommend removing or uninstalling the [!DNL Adobe Experience Manager] 6.5.7.0 package.

### Instale o Service Pack {#install-service-pack}

Execute as seguintes etapas para instalar o Service Pack em uma instância Adobe Experience Manager 6.5 existente:

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior). O Adobe também recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um backup atualizado da sua instância do [Experience Manager] .

1. Baixe o service pack da [Software Distribution (Distribuição](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)de software).

1. Abra o Gerenciador de pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador](/help/sites-administering/package-manager.md)de pacotes.

1. Select the package and click **[!UICONTROL Install]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte Armazenamento de dados [Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, a caixa de diálogo na interface do usuário do Package Manager sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Instalação automática**

Há duas maneiras de instalar automaticamente o Adobe Experience Manager 6.5.7.0 em uma instância em funcionamento:

A. Coloque o pacote na `../crx-quickstart/install` pasta quando o servidor estiver disponível on-line. O pacote é instalado automaticamente.

B. Use a API [HTTP do Gerenciador](https://docs.adobe.com/content/docs/pt/crx/2-3/how_to/package_manager.html)de pacotes. Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.7.0 não suporta a instalação do Bootstrap.

**Validar instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.7.0)` em Produtos instalados.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é a versão 1.22.3 ou posterior (Use o console da Web: `/system/console/bundles`).

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

### Instalar o pacote suplementar do Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libera os pacotes de complementos uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms. Correções no Adobe Experience Manager Forms são fornecidas por meio de um pacote complementar separado.

1. Verifique se você instalou o Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalar o Adobe Experience Manager Forms no JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções no Adobe Experience Manager Forms em JEE são entregues por meio de um instalador separado.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.7.0 está disponível no repositório [do](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)Maven Central.

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Adobe Public Maven (`repo.adobe.com`). O arquivo UberJar principal foi renomeado para `uber-jar-<version>.jar`. Então, não há `classifier`, com `apis` o valor, para a `dependency` etiqueta.

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e capacidades marcados como obsoletos com [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e depois removidos em uma versão futura. Uma opção alternativa geralmente é fornecida.

Analise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | A tela Aceitação **[!UICONTROL dos serviços da]** AEM Cloud está obsoleta. Com a integração de AEM e Público alvo atualizada no AEM 6.5 para suportar a API do Target Standard, que usa autenticação via Adobe IMS e E/S, e a função crescente de inicialização de Adobe para instrumentar AEM páginas para análise e personalização, o assistente de aceitação se tornou funcionalmente irrelevante. | Configure as conexões do sistema, a autenticação Adobe IMS e as integrações de E/S de Adobe por meio dos respectivos serviços em nuvem do AEM. |
| Conectores | O Conector JCR do Adobe para Microsoft SharePoint 2010 e Microsoft SharePoint 2013 está obsoleto para o AEM 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* Ignore os seguintes erros no `error.log` arquivo durante a instalação do Experience Manager 6.5.7.0:

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* Se você estiver atualizando sua [!DNL Experience Manager] instância da versão 6.5 para a 6.5.7.0, poderá visualização `RRD4JReporter` exceções no `error.log` arquivo. Reinicie a instância para resolver o problema.

* Se você instalar o [!DNL Experience Manager] 6.5 Service Pack 5 ou um service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado dos ativos (criado em `/var/workflow/models/dam`) será excluída.
Para recuperar sua cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com sua cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Entre em contato com o Atendimento ao cliente do Adobe se tiver problemas ao editar e criar regras em cascata no Schema de metadados da [!UICONTROL pasta do Forms Editor] e do Schema de [!UICONTROL metadados do Forms Editor] usando a caixa de diálogo [!UICONTROL Definir regra] . As regras que já foram criadas e salvas estão funcionando como esperado.

* Se uma pasta na hierarquia for renomeada [!DNL Experience Manager Assets] e a pasta aninhada que contém um ativo for publicada, o título da pasta não será atualizado [!DNL Brand Portal][!DNL Brand Portal] até que a pasta raiz seja publicada novamente.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Se o Assistente de configuração [!UICONTROL de ativos] conectados retornar uma mensagem de erro 404 após a instalação, reinstale manualmente os pacotes `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` o usando o Gerenciador de pacotes.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do AEM 6.5.x.x:
   * &quot;Quando a integração do Target é configurada no AEM usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granito/operações/manutenção.
   * A validação do lado do servidor do Formulário adaptável falha quando funções de agregação, como SUM, MAX e MIN são usadas. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Não foram encontradas janelas de manutenção no granito/operações/manutenção.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner que pode ser comprado.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no AEM 6.5.7.0:

* [Lista de pacotes OSGi incluídos no AEM 6.5.7.0](assets/6570_bundles.txt)

* [Lista de pacotes de conteúdo incluídos no AEM 6.5.7.0](assets/6570_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [como entrar em contato com o suporte](https://experienceleague.adobe.com/docs/customer-one/using/home.html)ao cliente.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de versão 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página do produto](https://www.adobe.com/br/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 Documentação](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

